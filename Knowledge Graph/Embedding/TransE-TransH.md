

# Translation-based Embedding: Từ Ký Hiệu Rời Rạc Sang Không Gian KG Liên Tục

Trong kiến trúc của DeepPath, bước đầu tiên và quan trọng nhất để biến một Knowledge Graph (KG) từ tập dữ liệu thô thành môi trường mà agent Reinforcement Learning (RL) có thể "đi lại" và suy luận chính là quá trình nhúng (embedding). Phần này giải thích lý do tại sao DeepPath lựa chọn họ mô hình **Translation-based** (cụ thể là TransE và TransH) để chuyển đổi các entity và relation từ dạng ký hiệu rời rạc (discrete symbols) sang các vector liên tục trong không gian $\mathbb{R}^d$, từ đó tạo nền tảng cho agent RL thực hiện các phép tính toán học và suy luận hình học. [sites.cs.ucsb:1][ieeexplore.ieee:2]

## 1. Bài Toán Gốc: Tại Sao Ký Hiệu Rời Rạc Không "Tính Toán" Được?

Một Knowledge Graph truyền thống được cấu thành từ các bộ ba (triples) có dạng:

$$(\text{Paris}, \text{capitalOf}, \text{France})$$

Ở dạng gốc, `Paris`, `capitalOf`, và `France` chỉ là các ID hoặc chuỗi ký tự (string). Đối với máy tính, nếu không có sự chuyển đổi, chúng chỉ là các nhãn rời rạc. Máy không thể tự nhiên biết rằng:
*   Entity `Paris` có ý nghĩa "gần" với `London` hơn là `Banana`.
*   Relation `capitalOf` có ngữ nghĩa tương đồng với `locatedIn` hơn là `bornIn`.
*   Làm thế nào để thực hiện phép "cộng" `Paris` với `capitalOf` để ra kết quả là `France`.

Để agent RL có thể so sánh, nội suy (interpolate) và tổng quát hóa (generalize), ta cần ánh xạ mỗi ký hiệu này thành một điểm trong không gian vector liên tục $\mathbb{R}^d$. Đây chính là nhiệm vụ của **Knowledge Graph Embedding**. [ieeexplore.ieee:2] DeepPath chọn họ mô hình **Translation-based** (TransE, TransH) với chiều vector $d=200$ (đảm bảo tương thích với các baseline như TransE/TransR được sử dụng trong bài). [sites.cs.ucsb:1]

## 2. Intuition Chung: Quan Hệ Là Phép Tịnh Tiến

Ý tưởng cốt lõi của họ mô hình này rất trực quan và mang tính hình học: **Mỗi quan hệ $r$ được xem như một phép tịnh tiến (translation) trong không gian vector.**

Nếu một triple $(h, r, t)$ là đúng (valid), thì trong không gian embedding, vector của head entity ($\mathbf{h}$) cộng với vector của relation ($\mathbf{r}$) sẽ xấp xỉ bằng vector của tail entity ($\mathbf{t}$):

$$\mathbf{h} + \mathbf{r} \approx \mathbf{t}$$

Hình dung đơn giản: Nếu bạn đang đứng tại điểm $\mathbf{h}$ trên bản đồ, và bạn "bước" một đoạn theo hướng và độ dài của mũi tên $\mathbf{r}$, bạn sẽ rơi vào vị trí rất gần điểm $\mathbf{t}$. 

**Ví dụ minh họa:**
*   $\mathbf{v}_{\text{Paris}} + \mathbf{v}_{\text{capitalOf}} \approx \mathbf{v}_{\text{France}}$
*   $\mathbf{v}_{\text{LeBron}} + \mathbf{v}_{\text{playsFor}} \approx \mathbf{v}_{\text{Lakers}}$

Hàm tính điểm (score function) để đánh giá độ "hợp lý" của một triple thường dựa trên khoảng cách (distance metric):

$$f_r(h, t) = \|\mathbf{h} + \mathbf{r} - \mathbf{t}\|_{L_1 \text{ hoặc } L_2}$$

Giá trị này càng nhỏ thì triple càng có khả năng là đúng (plausible). 

## 3. TransE: Mô Hình Cơ Bản Và Hạn Chế

### Cách Hoạt Động
TransE là mô hình đơn giản nhất trong họ này. Nó đặt tất cả các entity và relation vào chung một không gian $\mathbb{R}^d$. Mô hình được huấn luyện bằng **Margin Ranking Loss**, yêu cầu các triple đúng phải có khoảng cách nhỏ hơn các triple sai (được tạo ra bằng cách thay thế head hoặc tail - gọi là corrupt triple) một khoảng margin $\gamma$ nhất định:

$$\mathcal{L} = \sum_{(h,r,t)\in S^+} \sum_{(h',r,t')\in S^-} \left[\, f_r(h,t) + \gamma - f_r(h',t') \,\right]_+$$

Trong đó $[x]_+ = \max(0, x)$. 

### Điểm Mạnh
*   **Đơn giản và hiệu quả:** Dễ triển khai và scale tốt cho dữ liệu lớn.
*   **Bắt tốt quan hệ 1-1:** Với các quan hệ mà mỗi head chỉ có một tail duy nhất, TransE hoạt động rất tốt.
*   **Tính đối xứng của vector nghịch:** Vector của quan hệ nghịch đảo xấp xỉ bằng vector âm của quan hệ gốc ($\mathbf{r}^{-1} \approx -\mathbf{r}$), vì nếu $\mathbf{h} + \mathbf{r} \approx \mathbf{t}$ thì $\mathbf{t} + (-\mathbf{r}) \approx \mathbf{h}$.

### Hạn Chế (Lý Do Cần TransH)
TransE gặp khó khăn lớn với các quan hệ phức tạp trong thực tế do giả định không gian quá cứng nhắc:

| Loại Quan Hệ | Ví Dụ | Vấn Đề Của TransE |
| :--- | :--- | :--- |
| **1-N** | `hasChild` (1 cha $\to$ nhiều con) | Một vector $\mathbf{h} + \mathbf{r}$ không thể đồng thời gần nhiều vector $\mathbf{t}$ khác nhau. |
| **N-1** | `bornIn` (nhiều người $\to$ 1 thành phố) | Nhiều $\mathbf{h}$ khác nhau cộng cùng $\mathbf{r}$ phải ra cùng $\mathbf{t}$, ép các vector $\mathbf{h}$ phải gần nhau một cách sai lệch. |
| **N-N** | `friendOf`, `coAuthor` | Càng khó khăn hơn trong việc biểu diễn. |
| **Phản xạ / Đối xứng** | `spouse` | Nếu $\mathbf{h} + \mathbf{r} \approx \mathbf{t}$ và $\mathbf{t} + \mathbf{r} \approx \mathbf{h}$, mô hình bị ép buộc $\mathbf{r} \approx 0$. |

## 4. TransH: Khắc Phục Bằng Hyperplane

Để giải quyết các hạn chế trên, TransH (Translating on Hyperplanes) giữ nguyên ý tưởng "tịnh tiến" nhưng cho phép mỗi quan hệ $r$ có một **mặt phẳng riêng (hyperplane)**. [en.wikipedia:5]

### Cơ Chế
Với mỗi quan hệ $r$, TransH học hai vector:
1.  **Vector pháp tuyến $\mathbf{w}_r$:** Xác định hướng của hyperplane đặc trưng cho quan hệ $r$.
2.  **Vector tịnh tiến $\mathbf{d}_r$:** Nằm trên hyperplane đó, thực hiện việc dịch chuyển.

Trước khi thực hiện phép cộng, các entity được **chiếu (project)** lên hyperplane của quan hệ đó:

$$\mathbf{h}_{\perp} = \mathbf{h} - \mathbf{w}_r^\top \mathbf{h}\, \mathbf{w}_r$$
$$\mathbf{t}_{\perp} = \mathbf{t} - \mathbf{w}_r^\top \mathbf{t}\, \mathbf{w}_r$$

Sau đó, yêu cầu cơ bản vẫn là:
$$\mathbf{h}_{\perp} + \mathbf{d}_r \approx \mathbf{t}_{\perp}$$

### Intuition Hình Học
Cơ chế này cho phép một entity (ví dụ: `Obama`) có thể "hiện diện" dưới các hình chiếu khác nhau tùy thuộc vào quan hệ:
*   Trên hyperplane của `bornIn`: `Obama` được chiếu theo vai trò "người được sinh ra".
*   Trên hyperplane của `presidentOf`: `Obama` được chiếu theo vai trò "người lãnh đạo".

Nhờ việc chiếu khác nhau này, TransH có thể mô hình hóa tốt các quan hệ 1-N, N-1, và N-N mà vẫn giữ được tính hình học đơn giản của phép tịnh tiến. 

## 5. Cấu Trúc State 200 Chiều Trong DeepPath

Paper DeepPath quy định rõ về kích thước vector để đảm bảo tính nhất quán với các hệ thống baseline:

> "We use the same dimension as TransE/R to embed the entities. Specifically, the state vector we use has a dimension of 200…" [sites.cs.uscb:1]

Cụ thể, kiến trúc state của DeepPath được thiết kế như sau:
*   Mỗi entity $e$ được nhúng thành vector $\mathbf{e} \in \mathbb{R}^{100}$ (hoặc chiều tương đương sao cho tổng state là 200).
*   State tại bước thời gian $t$, ký hiệu $\mathbf{s}_t$, là sự kết hợp của vị trí hiện tại và vectơ chỉ hướng tới đích:

$$\mathbf{s}_t = \big(\mathbf{e}_t,\;\; \mathbf{e}_{\text{target}} - \mathbf{e}_t\big) \in \mathbb{R}^{200}$$

| Thành Phần | Ý Nghĩa Hình Học |
| :--- | :--- |
| $\mathbf{e}_t$ | **Vị trí hiện tại:** "Tôi đang đứng ở đâu" trên bản đồ KG. |
| $\mathbf{e}_{\text{target}} - \mathbf{e}_t$ | **Vector đích:** "Quãng đường còn lại" – bao gồm cả hướng và khoảng cách trong không gian embedding. |

Policy network của agent nhận đầu vào là $\mathbf{s}_t$ (một vector 200 số thực liên tục) và đưa ra phân phối xác suất cho các action (chọn relation nào để đi tiếp, bao gồm cả relation nghịch đảo $r^{-1}$). Vì state là liên tục, hai entity gần nhau trong không gian embedding sẽ tạo ra state gần nhau, dẫn đến policy cho hành vi tương tự, giúp agent **generalize** tốt hơn. [sites.cs.uscb:1]

## 6. "Không Gian KG Liên Tục" Nghĩa Là Gì Trong Thực Tế?

Sự chuyển đổi từ ký hiệu rời rạc sang không gian liên tục mang lại những khả năng tính toán mà KG gốc không có:

### Trước Embedding (Rời Rạc)
*   Entity = Tập hữu hạn các ID $\{e_1, e_2, \dots, e_{75000}\}$.
*   So sánh: Chỉ có thể kiểm tra bằng nhau (`equal`) hoặc khác nhau (`not equal`). Không có khái niệm "gần" hay "xa".

### Sau Embedding (Liên Tục)
*   Mỗi $e_i$ là một điểm trong $\mathbb{R}^d$.
*   Mỗi $r_j$ là một vector tịnh tiến.
*   Tồn tại các phép toán: Khoảng cách (distance), góc (angle), cộng/trừ vector.

**Hệ quả quan trọng cho Agent RL:**
1.  **Đo lường Similarity:** Có thể tính $\cos(\mathbf{e}_{\text{LeBron}}, \mathbf{e}_{\text{Kobe}})$. Nếu giá trị cao, agent hiểu hai người này có "style" tương tự và có thể áp dụng chiến lược suy luận giống nhau.
2.  **Composition (Phép hợp thành):** Phép cộng vector cho phép suy luận đường đi. Ví dụ: đi từ `bornIn` rồi `cityInCountry` xấp xỉ bằng đi thẳng `nationality`:
    $$\mathbf{r}_{\text{bornIn}} + \mathbf{r}_{\text{cityInCountry}} \approx \mathbf{r}_{\text{nationality}}$$
    (DeepPath tận dụng điều này cho phần *diversity reward* bằng cách tổng hợp embedding các relation trong path).
3.  **Suy luận triple mới (Link Prediction):** Với cặp $(h, r)$ chưa từng thấy, agent có thể tìm $t$ sao cho $\mathbf{h} + \mathbf{r}$ gần $t$ nhất.
4.  **State mượt cho RL:** Gradient của policy network có thể lan truyền (backpropagate) qua các state liên tục này, hiệu quả hơn nhiều so với việc dùng one-hot encoding hàng chục nghìn chiều.

## 7. Pipeline Đầy Đủ Trong DeepPath

Quy trình xử lý dữ liệu trong DeepPath diễn ra theo các bước tuần tự:

1.  **Input:** Các triples của KG gốc.
2.  **Training Embedding (Offline):** Huấn luyện mô hình TransE hoặc TransH trên toàn bộ KG trước khi chạy RL.
3.  **Lookup Tables:** Tạo bảng tra cứu:
    *   `entity_id` $\to$ vector (entity2vec).
    *   `relation_id` $\to$ vector (relation2vec).
4.  **RL Environment:**
    *   **Quan sát:** $\mathbf{s}_t = (\mathbf{e}_t, \mathbf{e}_{\text{target}} - \mathbf{e}_t)$ (vector 200 chiều liên tục).
    *   **Action:** Chọn một relation (cạnh) để di chuyển.
    *   **Transition:** Di chuyển đến entity kề tiếp theo nếu có cạnh đó.
    *   **Reward:** Tính dựa trên global accuracy, efficiency (độ dài path), và diversity.
5.  **Policy Network:** Học hàm $\pi_\theta(\mathbf{s}, a)$ để chọn action tối ưu.

*Lưu ý:* Trong quá trình RL, các embedding này là **cố định** (frozen), đóng vai trò là hệ tọa độ không gian để agent di chuyển, không được cập nhật trọng số trong lúc học policy. 

## 8. Ví Dụ Số Minh Họa (Giả Định $d=2$)

Để dễ hình dung, giả sử không gian chỉ có 2 chiều (thực tế là 100-200):

| Ký Hiệu | Vector Học Được (Giả Định) |
| :--- | :--- |
| **Paris** | $(1.0, 2.0)$ |
| **France** | $(3.0, 2.5)$ |
| **capitalOf** | $(2.0, 0.5)$ |
| **London** | $(1.2, 1.8)$ |
| **UK** | $(3.1, 2.3)$ |

**Kiểm tra tính đúng đắn:**
*   $\mathbf{Paris} + \mathbf{capitalOf} = (1.0+2.0, 2.0+0.5) = (3.0, 2.5) = \mathbf{France}$ $\to$ Khớp chính xác.
*   $\mathbf{London} + \mathbf{capitalOf} = (1.2+2.0, 1.8+0.5) = (3.2, 2.3) \approx \mathbf{UK}$ $\to$ Rất gần (sai số nhỏ).

Nhờ sự gần nhau này, dù model có thể ít thấy cặp (London, UK) lúc train, nó vẫn "đoán" được mối quan hệ `capitalOf` dựa trên vị trí hình học.

**Góc nhìn của Agent:**
Khi agent đứng ở `Paris` với đích là `France`, state của nó là:
$$\mathbf{s}_t = ((1.0, 2.0),\; (2.0, 0.5))$$
Policy network học được quy luật: Khi "vector còn lại" trông giống hệt vector `capitalOf`, hãy chọn action `capitalOf`.

## 9. Tóm Tắt

Translation-based embedding biến mỗi entity thành một điểm và mỗi relation thành một mũi tên tịnh tiến trong không gian $\mathbb{R}^d$ (DeepPath dùng $d$ sao cho state tổng cộng 200 chiều). Điều này đảm bảo các triple đúng thỏa mãn công thức $\mathbf{h} + \mathbf{r} \approx \mathbf{t}$ (với TransE) hoặc $\mathbf{h}_{\perp} + \mathbf{d}_r \approx \mathbf{t}_{\perp}$ (với TransH). [sites.cs.uscb:1] Nhờ phép biến đổi này, KG từ một tập ký hiệu rời rạc trở thành một "bản đồ số" liên tục, cho phép agent RL đo khoảng cách, so sánh hướng đi và tổng quát hóa hành vi giữa các entity và relation có ngữ nghĩa tương đồng.

***
**References:**
[sites.cs.uscb:1] DeepPath Paper (UCSB)
[ieeexplore.ieee:2] Knowledge Graph Embedding Overview
 Electronics MDPI - KG Embedding
 TransE Topic Overview
[en.wikipedia:5] Wikipedia - Knowledge Graph Embedding
 Towards Data Science - KG Embeddings 101
 DeepPath GitHub Repository
