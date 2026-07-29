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
> **A (Action space)**: tập tất cả các quan hệ có trong KG (bao gồm cả [quan hệ nghịch](#Quan-hệ-nghịch), ký hiệu $\(r^{-1}\))$
>
>  > agent "hành động" bằng cách chọn một quan hệ để đi tiếp.
> 
> **$P$**: ma trận xác suất chuyển trạng thái $\(P(S_{t+1}=s'|S_t=s, A_t=a)\)$.
>  
> **$R\(s,a\)$**: hàm phần thưởng cho mỗi cặp (trạng thái, hành động).

#### Agent
> được biểu diễn bằng một **policy network** $\(\pi_\theta(s,a) = p(a|s;\theta)\)$
>
> kiến trúc mạng neural 2 lớp ẩn (ReLU) + softmax ở đầu ra, ánh xạ trạng thái sang phân phối xác suất trên các action.
> 
> Tác giả chọn phương pháp **policy-based** (thay vì DQN dạng value-based) vì hai lý do:
>  > (1) không gian hành động rất lớn khiến DQN khó hội tụ
>  > (2) policy ngẫu nhiên (stochastic) giúp agent không bị "kẹt" tại một trạng thái trung gian — khác với chính sách greedy của DQN

#### Reward
hàm reward tổng hợp 3 tiêu chí: độ chính xác, hiệu quả, và đa dạng.

- **Global accuracy** $r_{GLOBAL}$: +1 nếu đường đi tới được thực thể đích, -1 nếu không. Vì số lượng chuỗi hành động sai tăng theo cấp lũy mũ với độ dài đường đi, reward này là cơ chế cơ bản định hướng agent đến đích. [sites.cs.ucsb](https://sites.cs.ucsb.edu/~william/papers/DeepPath.pdf)
- **Path efficiency** $r_{EFFICIENCY} = \dfrac{1}{length(p)}$ , trong đó $\(length(p)\)$ là số quan hệ trong đường đi $\(p = r_1 \to r_2 \to ... \to r_n\)$. Ý tưởng: đường đi ngắn thường đáng tin cậy hơn và giúp suy luận hiệu quả hơn, nên được thưởng cao hơn khi ngắn. 
- **Path diversity** $r_{DIVERSITY} = -\dfrac{1}{|F|}\sum_{i=1}^{|F|} \cos(p, p_i)$ , trong đó $\(p = \sum_{i=1}^n r_i\)$ là embedding của đường đi (tổng embedding các quan hệ), $\(p_i\)$ là các đường đi đã tìm được trước đó trong tập $\(F\)$ , và $\(\cos(\cdot,\cdot)\)$ là độ tương đồng cosine. Vì nhiều mẫu huấn luyện có trạng thái tương tự nhau, agent dễ tìm ra các đường đi "giống nhau về cú pháp/ngữ nghĩa" — chứa thông tin dư thừa. Reward này phạt các đường đi quá giống các đường đi cũ, khuyến khích agent khám phá đường đi mới, đa dạng hơn.

Tổng reward khi thành công là tổ hợp tuyến tính: $\(R_{total} = \lambda_1 r_{GLOBAL} + \lambda_2 r_{EFFICIENCY} + \lambda_3 r_{DIVERSITY}\)$, với $\(\lambda_1,\lambda_2,\lambda_3\)$ là các trọng số cân bằng ba tiêu chí.

### Annotation
#### Quan hệ nghịch
Cho quan hệ $\(r\)$: $(h,\, r,\, t) \Longleftrightarrow (t, r^{-1}, h)$

- $\(h\)$: head (thực thể đầu)
- $\(t\)$: tail (thực thể cuối)
- $\(r^{-1}\)$: quan hệ nghịch của $\(r\)$

#### Pipeline khái quát
1. RL agent roll out nhiều episode
        ↓
2. Mỗi episode thành công → một instance path
        ↓
3. Bóc tách chuỗi quan hệ → path formula
        ↓
4. Gom vào tập F (tối đa ~10 formula / target relation)
        ↓
5. Dùng F như feature (kiểu PRA):
   với cặp (h,t) mới, formula nào “chạy” được trên KG?
        ↓
6. Classifier / ranking → link prediction / fact prediction
