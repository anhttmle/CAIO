Paper này đề xuất một framework fact-checking giải thích được dựa trên reinforcement learning (RL) và knowledge graph embeddings, nơi agent học cách “đi dạo” trong KG để tìm các đường dẫn (paths) làm bằng chứng cho (hoặc chống lại) một claim, rồi dùng tập các path đó để bỏ phiếu ra verdict true/false cho claim.  

Dưới đây mình sẽ trình bày theo hướng “intuition-first”, rồi giải nghĩa chi tiết từng đại lượng và concept trong phần toán/MDP/RL.

***

## 1. Bức tranh tổng thể và intuition

### Vấn đề tác giả giải

- Input: một **fact claim** dạng triple $\langle h, r, t\rangle$ (head entity, relation, tail entity), ví dụ $\langle\text{Dick Cheney}, \text{worksFor}, \text{Halliburton}\rangle$.  
- Knowledge graph (KG): tập các triple $\langle e_i, r_j, e_k\rangle$ chứa tri thức đã biết.  
- Mục tiêu:
  1. Xác định claim là đúng hay sai (veracity verdict).
  2. Trả về các path trong KG dùng làm **explanation** cho verdict đó (giải thích được, human-readable).  

Thay vì làm fact-checking thuần NLP hoặc rule-mining, paper:
- Biến bài toán thành một **multi-hop reasoning** trên KG: agent RL xuất phát từ head entity, lần lượt chọn quan hệ để nhảy qua các entity, hình thành một **evidential path**.  
- Các path này sau đó được dùng để:
  - Đo xem có path nào kết thúc ở đúng tail entity “true” không (dạng link prediction).  
  - Đếm và bỏ phiếu (voting) trên tail entity xuất hiện ở cuối các path, để ra verdict.  

Intuition quan trọng:
- Nếu claim $\langle h, r, t\rangle$ là **true**, thì lý tưởng sẽ tồn tại một hoặc nhiều đường dẫn “semantically phù hợp” từ $h$ tới $t$ trong KG.  
- Nếu claim là **false**, các đường dẫn “khớp về semantics” sẽ đi đến một entity khác, không phải $t$, hoặc chỉ tạo ra path mơ hồ/inconclusive.  
- Bởi vì agent hoạt động trong **embedding space** (ComplEx) nên nó không cần pattern thủ công; policy được học để “thích” những bước nhảy đưa đến tail entity có embedding phù hợp với claim.  

Framework có hai phần chính:
1. **Evidential path extraction**: RL agent + beam search sinh ra nhiều path từ head entity.  
2. **Veracity verdict & voting**: đếm tail entity cuối các path, weighted by heuristic, rồi so sánh với claimed tail.  

***

## 2. Evidential path extraction: MDP, policy, beam search

### MDP formulation: $\langle S, A, T, R\rangle$

Paper mô hình hoá tương tác Agent–KG như một **Markov Decision Process (MDP)**.  

1. **State $S$**  
   Trực giác: state chứa toàn bộ thông tin mà agent cần để quyết định bước tiếp theo. Gồm:
   - Claim đầu vào: $\langle \text{claimedTarget}, \text{claimedRelation}, \text{beginningOfPath}, \dots \rangle$.  
   - Path đã **traversed** đến hiện tại: chuỗi cặp (relation, entity) từ head đến current entity.  
   - Current location: entity mà agent đang đứng (current tail của path).  

   Có **hai representation song song**:
   - Human-readable: các entity và relation dưới dạng tên/ID thật trong KG.  
   - Embedding-based: vector embeddings (ComplEx) của các entity và relations đó.  

   Vì policy network của RL cần input fixed-size, embedded state được:
   - Padding bằng zero vectors ở những vị trí chưa có bước path.  
   - Khi agent đi tiếp, zero vectors dần được thay bằng cặp (relation embedding, entity embedding).  
   - Entity cuối cùng trong chuỗi này là **finalEntity**, được dùng để đưa ra veracity verdict.  

   Intuition: state là “claim + lịch sử reasoning + vị trí hiện tại”, được nhúng thành một vector để NN suy nghĩ.

2. **Action $A$**  
   Action space được định nghĩa là tập tất cả các **unique relations** trong KG, cộng thêm một self-loop relation để agent có thể “stay” tại entity hiện tại.  

   - Policy network nhận state, xuất ra một probability distribution trên toàn bộ action space.  
   - Để đảm bảo chỉ chọn các hành động hợp lệ, distribution được **filter** chỉ giữ các relations có thể thực sự nối current entity đến ít nhất một neighbor trong KG.  
   - Self-loop luôn nằm trong action space, cho phép agent quyết định không di chuyển (stay put).  

   Intuition: agent không chọn entity trực tiếp, mà chọn relation; từ relation đó, môi trường sẽ chọn entity (có heuristic). Điều này giống nhiều work multi-hop reasoning trước, nhưng ở đây họ thêm scoring theo entity.  

3. **Transition function $T : S \times A \to S$**  
   Khi agent chọn action $a$ tại state $s$:
   - Environment lấy current entity $e_s$.
   - Tìm các neighbor $e'$ sao cho có edge $\langle e_s, a, e'\rangle$.  
   - Chọn một entity (với heuristic), cập nhật path: thêm (a, e') vào state.  
   - Current location trở thành $e'$.  
   - State mới là “claim + updated path + new current entity”, cả ở dạng readable và embeddings.  

   Intuition: mỗi transition là một bước nhảy qua một relation trong KG.

4. **Reward $R$**  
   Reward chỉ được cấp **cuối tập episode** (n-step).  

   - Khi path traversal hoàn tất (sau số bước cố định, ví dụ 3 steps), ta có finalEntity.  
   - Có một “trueTarget” (ground truth tail entity) cho triple.  
   - Reward được xác định:
     $$
     \text{reward} =
     \begin{cases}
     1 & \text{if } \text{finalEntity} = \text{trueTarget} \\
     0 & \text{otherwise}
     \end{cases}
     $$
  

   Intuition: agent được khuyến khích tìm path kết thúc đúng true tail entity. Đáng chú ý là **reward không dùng claimed tail mà dùng true tail**, tức model được train supervised để dùng path cho classification.  

### Policy network và REINFORCE

- Policy function: $\pi(a \mid s, \theta)$, với $\theta$ là tham số của NN.  
  - Input: embedded state $s$.
  - Output: probability distribution trên action space.  
  - NN: dùng ReLU ở hidden layers, softmax ở output.  
- Training: sử dụng thuật toán **REINFORCE** (policy gradient) để maximize expected reward.  
  - Mỗi episode: 3 steps (fixed), với top-3 actions được sampling một cách stochastic để tăng exploration.  

Intuition:
- NN học mapping từ “claim + path hiện tại + vị trí hiện tại” → “relation nào tiếp theo sẽ đưa đến tail đúng”.
- Vì reward binary và delayed, agent có động lực học các chiến lược path toàn cục thay vì greedy local.

### Beam search và scoring function

#### Beam search

Beam search được dùng để:
- Mở rộng không chỉ **một** path mà là **nhiều** path song song trong mỗi episode (beam size $b$).  
- Ở mỗi step, từ mỗi partial path, ta:
  - Lấy distribution $\pi(a \mid s,\theta)$.
  - Kết hợp với heuristic scoring để đánh giá “độ tốt” của action.  
  - Giữ lại top $b$ path candidate theo score.  

Intuition: beam search giúp khám phá nhiều đường dẫn khác nhau trong KG, tăng khả năng tìm được tail đúng, và đồng thời cung cấp nhiều path để dùng cho explainability/voting.

#### KG scoring function và heuristic

Paper dùng **ComplEx** scoring function $Re(\langle r, e_s, \bar{e}_c\rangle)$.  

Giải nghĩa từng đại lượng:
- $r$: embedding vector của relation.  
- $e_s$: embedding vector của **head entity** (ở đây thường là current entity trong path, hoặc claimed head).  
- $\bar{e}_c$: embedding của tail entity candidate, với $\bar{\cdot}$ là complex conjugate vì ComplEx dùng complex-valued embeddings.  
- $\langle r, e_s, \bar{e}_c\rangle$: dot product (inner product) giữa ba vector (ở không gian phức).  
- $Re(\cdot)$: real part của dot product đó.  

Intuition ComplEx:
- Scoring function cho biết triple $\langle e_s, r, e_c\rangle$ có “phù hợp” với KG hay không (link prediction score).  
- Score càng cao thì triple càng có nhiều khả năng là fact đúng (hoặc nằm trong KG).  

Paper định nghĩa heuristic action score bằng công thức (Equation 1):  

$$
\pi(a \mid s,\theta) + Re(\langle r, e_s, \bar{e}_c\rangle)^{\text{step}}
\tag{1}
$$

Giải nghĩa:
- $\pi(a \mid s,\theta)$: xác suất policy gán cho action $a$ tại state $s$.  
- $Re(\langle r, e_s, \bar{e}_c\rangle)$: score KG cho entity $e_c$ khi dùng relation $r$ từ head $e_s$.  
- $\text{step}$: số bước hiện tại trong episode (1, 2, 3, …).  
- $Re(\cdot)^{\text{step}}$: score được nâng lũy thừa theo step, tạo ra **exponential weighting** – về trực giác:
  - Early steps: tầm quan trọng của entity fitness thấp hơn, vì path còn dài, nhiều khả năng.  
  - Later steps: tầm quan trọng của entity fitness cao hơn (score được phóng đại bởi exponent), vì bước cuối gần với tail.  

Sau đó:
- Tổng $\pi(a \mid s,\theta) + Re(\cdot)^{\text{step}}$ được dùng để rank các lựa chọn action+entity candidate trong beam search.  

Intuition:
- Agent vừa dựa vào **policy (learned strategy)** vừa dựa vào **KG scoring (semantics/local plausibility)**.
- Ở bước cuối, entity fitness được ưu tiên mạnh để chọn các path kết thúc ở tail phù hợp với claim.

***

## 3. Veracity verdict: đếm tail và voting

Sau khi kết thúc path extraction bằng RL+beam search, ta có **tập các path** từ head entity. Mỗi path kết thúc ở một tail entity $e_{\text{final}}$.  

### Bước 1: Đếm tail entities

- Nhóm các path theo **final tail entity** của path.  
- Đếm số path “vote” cho mỗi entity.  
- Straightforward approach: chọn entity với số path lớn nhất (majority vote).  

Vấn đề:
- Có thể có **tie**: hai entity có cùng số path.  
- Có entity được support bởi path “better” (KG score cao) nhưng số path ít hơn.  

### Bước 2: Weighted voting bằng beam heuristic

Paper thêm một heuristic weighting:
- Mỗi path có một **beam search heuristic score ở bước cuối**, dựa trên $Re(\langle r, e_s, \bar{e}_c\rangle)^{\text{step}}$ cho action cuối.  
- Weighted vote: weight của một entity = tổng heuristic score (hoặc một function của nó) từ các path kết thúc ở entity đó.  

Intuition:
- Entities được support bởi path mà agent “confident” hơn (có policy prob cao + KG score cao) sẽ nhận nhiều weight hơn.  
- Điều này giúp:
  - Giảm khả năng tie.  
  - Ưu tiên tail entity phù hợp hơn với KG semantics.  

### Bước 3: Verdict và cập nhật Agent

Veracity verdict:
- **PredictedTarget** = entity thắng voting.  
- Claim được xem là **true** nếu $\text{PredictedTarget} = \text{claimedTarget}$ (tail trong claim).  
- Nếu khác, claim bị đánh dấu là **false**.  

Đồng thời:
- Performance được đánh giá với ground truth trueTarget.  
- Reward được dùng để cập nhật policy parameters $\theta$.  

Intuition:
- Agent học chiến lược tìm path sao cho tail cuối:
  1. Trùng với trueTarget (về training).
  2. Khi áp dụng, tail cuối matching claimed target sẽ được coi là evidence claim true.  

***

## 4. Environment and training details: datasets, embeddings, hyperparameters

### Datasets và statistic

Hai KG benchmark:
- **FB15K-237**:  
  - #Ent = 14,505; #Rel = 237; #Fact = 272,115.  
  - Density ~ 18.8 triples/entity (khá dense).  
- **NELL-995**:  
  - #Ent = 75,492; #Rel = 200; #Fact = 154,213.  
  - Density ~ 2 triples/entity (sparse).  

Các reasoning tasks:
- FB15K-237: relations origin, tvLanguage, nationality, và một subset “combined” chứa cả 3.  
- NELL-995: athletePlaysInLeague, athletePlaysForTeam, worksFor, và subset combined.  

Negative samples:
- Mỗi task có khoảng 10 negative claims cho mỗi positive claim, tạo ra dataset fact-checking.  
- Negative được tạo bằng cách thay tail đúng bằng một fake entity.  

Intuition:
- Điều này cho phép đánh giá agent trên cả true và false claims, xem việc path-based reasoning có phân biệt rõ không.

### Knowledge graph embeddings (ComplEx)

- Model: ComplEx (complex embeddings for link prediction).  
- Hyperparameters:
  - Batch size = 50.  
  - Epochs = 1000.  
  - Embedding dimension = 20.  
  - Optimizer: Adam, learning rate $1e-4$.  
  - Loss: negative log-likelihood.  
  - Regularization: $L_3$ với strength $1e-5$.  
  - Random seed = 0 để reproducibility.  

Intuition:
- Embeddings được train trước để scoring function $Re(\langle r, e_s, \bar{e}_c\rangle)$ có ý nghĩa. Agent RL dựa vào embedding này để đánh giá candidate triples.

### Policy network & RL training

- Algorithm: REINFORCE.  
- Implementation: PyTorch.  
- Network:
  - Hidden size = 128 neurons.  
  - Activation: ReLU trong hidden, Softmax output.  
  - Initialization: Xavier.  
- Training:
  - 100,000 episodes per reasoning task.  
  - Each episode: 3 steps (fixed path length).  
  - Optimizer: Adam, learning rate = 0.001.  
  - Exploration: trong training, ở mỗi state, chọn random một trong top-3 actions theo distribution (re-sampled).  

Evaluation:
- Dùng beam search với các beam sizes: 3, 5, 10.  
- Metrics:
  - **Hits@k**: tỉ lệ test samples mà target đúng nằm trong top k-ranked answers (ở đây coi như thành công nếu bất kỳ path đến được true target).  
  - **Voting accuracy**: tỉ lệ test samples mà entity thắng weighted majority vote là đúng.  

***

## 5. Kết quả và insight quan trọng

### Hits@k vs Voting Accuracy

Quan sát từ tables:  

- Với beam size lớn (10), Hits@k rất cao:
  - FB15K-237: origin đạt 0.66, tvLanguage 0.894, nationality 0.921, combined 0.943.  
  - NELL-995: nhiều task lên đến ~0.99 (athletePlaysInLeague).  
- Voting accuracy thường thấp hơn:
  - Vì từ nhiều path đúng, voting có thể chọn tail entity sai (bị lấn át bởi các entity lân cận).  

Intuition:
- Agent dễ “tìm được ít nhất một path đúng” (Hits@k cao).
- Nhưng việc **chọn một entity duy nhất** dựa trên voting gây trade-off: accuracy giảm, đặc biệt ở task khó, hoặc quan hệ mơ hồ như “origin”.  

### Những case explainability điển hình

Paper cho 6 ví dụ, rất hay để hiểu intuition:  

- **Ví dụ 1 (Dick Cheney – Halliburton)**:
  - Claim: Dick Cheney worksFor Halliburton.
  - Path: Dick Cheney – leadsOrganization → Halliburton.  
  - Intuition: agent học được near-synonym giữa “leads organization” và “works for”. Tuy nhiên KG chứa thông tin outdated (Cheney từng dẫn Halliburton, nhưng không còn), nên ground truth coi claim false, dù reasoning rất tốt.  

- **Ví dụ 2 (John Gruden – Buccaneers)**:
  - Claim: Coach John Gruden worksFor Buccaneers.
  - Path: John Gruden ← organizationHiredPerson – Buccaneers.  
  - Agent tìm relation “organization hired person” như chứng cứ cho “works for”: đúng trong giai đoạn lịch sử 2002–2008, nhưng hiện tại claim không còn true.  
  - Insight: KG phải up-to-date để verdict chính xác; path vẫn informative.

- **Ví dụ 3 (Brendan Shanahan plays Hockey)**:
  - Path: Shanahan – playsForTeam → Devils – teamPlaysSport → Hockey.  
  - Agent không chỉ tìm near-synonym mà là một **multi-hop reasoning** phức tạp: từ người → team → sport.  

- **Ví dụ 4 (Amir Taheri)**:
  - Claim: Journalist Amir Taheri worksFor Los Angeles County.
  - Path: Amir Taheri → Amir Taheri (self-loop, stay put).  
  - Agent “đứng yên” suốt path, tạo ra kết quả inconclusive. Đây là behavior cần cải thiện (increase motivation to move from source entity).  

- **Ví dụ 5 (Ben Folds origin)**:
  - Claim: Ben Folds originates from Nashville.
  - Paths:
    - Path1: Ben Folds – placeOfBirth → Winston-Salem (true origin).  
    - Path2: Ben Folds – location → Nashville (current location).  
  - Quan hệ “origin” mơ hồ giữa birthplace và current location. Voting có thể sai nếu path “location” được nhiều vote.  

- **Ví dụ 6 (Kylie Minogue origin)**:
  - Claim: Kylie Minogue originates from Australia.
  - Paths:  
    - Path1: placeOfBirth → Melbourne.  
    - Path2: placeOfBirth → Melbourne ← contains → Australia.  
  - KG ground truth cho rằng origin = Melbourne (city), còn claim nói Australia (country). Path đến Australia rất explainable nhưng verdict mechanism đánh dấu false.  

Insight chung:
- Framework tạo ra **explainable paths** rất hợp lý.
- Nhưng verdict logic (so sánh entity cuối với ground-truth/claimed target) chưa xử lý tốt:
  - Outdated info.
  - Ambiguous relations.
  - Supportive-but-not-final entities (paths kết thúc ở entity khác nhưng vẫn support ground truth).  

***

## 6. Tổng kết intuition và các điểm mở rộng

Các concept chính và intuition:

- **KG reasoning bằng RL**: Agent học chính sách đi path sao cho tail cuối trùng true target. Điều này đồng thời sinh ra path giải thích được.  
- **Policy + KG scoring**:
  - Policy $\pi(a \mid s,\theta)$ mang tính “global strategy”.
  - Scoring $Re(\langle r, e_s, \bar{e}_c\rangle)^{\text{step}}$ mang tính “local plausibility” của triple.  
  - Kết hợp trong beam search cho phép vừa khám phá vừa khai thác tri thức KG.

- **Veracity verdict bằng weighted voting**:
  - Tập các tail entity cuối path là candidate answer.
  - Weighted voting giúp xử lý tie và ưu tiên path “tốt”.  
  - Tuy nhiên, accuracy giảm khi phải chọn đúng **một** entity duy nhất trong bối cảnh quan hệ mơ hồ.

Các hướng cải tiến mà paper gợi ý:  
- Dùng KG cập nhật liên tục để tránh outdated info.
- Thiết kế lại verdict mechanism để:
  - Nhận diện và xử lý các path **inconclusive** (ví dụ agent stay put).
  - Dùng các path không kết thúc ở target nhưng support ground truth.
  - Học cách xử lý quan hệ ambiguous như “origin”.
- Tăng động lực agent rời khỏi source entity (giảm self-loop bias).  
- Mở rộng framework cho fake news detection và các KG lớn hơn, claims phức tạp hơn.  

***

