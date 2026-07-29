### Single-hop reasoning (suy luận một bước)
> là dạng suy luận trong đó câu trả lời có thể được tìm ra trực tiếp từ một nguồn thông tin duy nhất hoặc qua một bước tra cứu/tìm kiếm mà không cần kết hợp nhiều mảnh thông tin rời rạc

- **Đặc điểm**:
  - **Một bước tìm kiếm**: Hệ thống chỉ cần truy vấn một lần vào cơ sở tri thức, database, hoặc tài liệu để có đủ thông tin trả lời.
  - **Câu hỏi đơn giản**: Thường áp dụng cho các câu hỏi dạng "Who is...", "What is...", "When did..." mà đáp án nằm gọn trong một đoạn văn bản hoặc một fact.
  - **Không cần chaining**: Không yêu cầu nối nhiều bước suy luận (không cần A → B → C, chỉ cần A → đáp án).
- **Benchmark tiêu biểu**: TriviaQA, NaturalQuestions

### Multi-hop reasoning (suy luận đa bước) 
> là khả năng của hệ thống AI kết nối nhiều mảnh thông tin rời rạc từ các nguồn khác nhau để suy ra câu trả lời hoặc quyết định, thay vì trích xuất trực tiếp từ một nguồn duy nhất

- **Đặc điểm**:
  - **Tổng hợp thông tin phân tán**: Kết hợp các sự kiện, ngữ cảnh từ nhiều tài liệu, cơ sở tri thức, hoặc hệ thống khác nhau
  - **Suy luận gián tiếp**: Đưa ra kết luận không được nêu trực tiếp trong văn bản, mà phải thông qua chuỗi logic nhiều bước
  - **Đọc hiểu sâu + lập luận**: Hiểu ngôn ngữ phi cấu trúc, truy xuất sự kiện liên quan, kết nối chúng theo logic, và đối chiếu để tạo ra inference
- **Benchmark tiêu biểu**: HotpotQA, Musique
- **Phương pháp phổ biến cho không gian rời rạc**: Path-Ranking Algorithm (PRA) — dùng random walk rời rạc để dò đường đi


### Deep Path
> biến việc "tìm đường đi suy luận" thành một bài toán quyết định tuần tự (sequential decision making), giải bằng RL.
> 
> Agent đứng ở một thực thể nguồn, tại mỗi bước phải "chọn" một quan hệ để nhảy sang thực thể kế tiếp, giống như đi bộ trên graph nhưng có mục tiêu rõ ràng (đến thực thể đích) và có "phần thưởng" định hướng chất lượng đường đi.
> 
> Vì trạng thái được biểu diễn bằng embedding liên tục (thay vì ký hiệu rời rạc), agent có thể "cảm nhận" được sự tương đồng ngữ nghĩa giữa các thực thể/quan hệ khác nhau — đây là điểm khác biệt mấu chốt so với PRA

- KG với các triple: Entity - Relation - Entity
- Thực thể: $e_{\text{entity}} \in \mathbb{R}^{200}$
- Quan hệ: $r_{\text{relation}} \in \mathbb{R}^{200}$

#### Markov Decision Process
> Biểu diễn bởi tuple ⟨S, A, P, R⟩:
> 
> **S (State space)**: không gian trạng thái liên tục.
> Trạng thái tại bước $t$ được định nghĩa là $s_t = (e_t, e_{target} - e_t)$, trong đó:
>  >  
>  > $e_t$ là embedding của thực thể hiện tại
>  >
>  > $e_{target}$ là embedding của thực thể đích.
>  > Vector hiệu $\(e_{target}-e_t\)$ cho agent biết "còn cách đích bao xa/theo hướng nào" trong không gian vector.
>
> **A (Action space)**: tập tất cả các quan hệ có trong KG (bao gồm cả [quan hệ nghịch](####Quan-hệ-nghịch), ký hiệu $\(r^{-1}\))$
>
>  > agent "hành động" bằng cách chọn một quan hệ để đi tiếp.
> 
> **$P$**: ma trận xác suất chuyển trạng thái $\(P(S_{t+1}=s'|S_t=s, A_t=a)\)$.
>  
> **$R\(s,a\)$**: hàm phần thưởng cho mỗi cặp (trạng thái, hành động).

### Annotation
#### Quan hệ nghịch
Cho quan hệ $\(r\)$:

$$(h,\, r,\, t) \Longleftrightarrow (t, r^{-1}, h)$$

- $\(h\)$: head (thực thể đầu)
- $\(t\)$: tail (thực thể cuối)
- $\(r^{-1}\)$: quan hệ nghịch của $\(r\)$
