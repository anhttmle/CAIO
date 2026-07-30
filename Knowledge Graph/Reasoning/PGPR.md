# Reinforcement Knowledge Graph Reasoning for Explainable Recommendation (PGPR)

Paper SIGIR 2019 của Yikun Xian, Zuohui Fu và cộng sự (Rutgers University) đề xuất **Policy-Guided Path Reasoning (PGPR)** — khung học tăng cường (RL) để vừa gợi ý sản phẩm vừa sinh **đường đi suy luận tường minh** trên knowledge graph, làm bằng chứng giải thích cho mỗi recommendation.  

***

## 1. Động lực và ý tưởng cốt lõi

### Vấn đề của các hướng trước

Hệ gợi ý dùng knowledge graph (KG) thường chia hai nhánh:

- **Embedding-based** (TransE, node2vec, CKE…): nhúng entity/relation thành vector, đo độ tương đồng. Hạn chế: không khám phá được quan hệ **multi-hop**; nếu có “giải thích” thì thường là **post-hoc** (chọn item trước, rồi mới tìm path khớp embedding sau).  
- **Path-based** (meta-path, path embedding + RNN): liệt kê mọi path user–item rồi học ranking. Hạn chế: không khả thi trên KG lớn vì số path bùng nổ.  

### Intuition chính

Một agent “thông minh” không chỉ nhúng đồ thị rồi so khớp vector, mà phải **đi thật** trên KG: bắt đầu từ user, nhảy nhiều bước qua entity/relation, đến item phù hợp. **Lịch sử đường đi** chính là lời giải thích nhân quả: *“Vì sao gợi ý item này?”* = *“Vì agent đã đi theo path này.”*  

Ví dụ (Hình 1 paper): từ User A có thể tới Item B qua  
`UserA → ItemA → BrandA → ItemB`,  
hoặc tới Item F qua `UserA → FeatureB → ItemF`.  

***

## 2. Bài toán KGRE-Rec

### Knowledge graph cho recommendation $G_R$

$$
G_R = \{(e, r, e') \mid e, e' \in \mathcal{E},\; r \in \mathcal{R}\}
$$

- $\mathcal{E}$: tập entity (User, Item, Brand, Category, Feature, …)
- $\mathcal{R}$: tập quan hệ (Purchase, Mention, Described_by, Belong_to, …)
- $U, I \subseteq \mathcal{E}$, $U \cap I = \emptyset$: user và item là hai tập con đặc biệt.  

### $k$-hop path

Đường đi $k$ bước từ $e_0$ đến $e_k$:

$$
p_k(e_0, e_k) = \bigl\langle e_0 \overset{r_1}{\longleftrightarrow} e_1 \overset{r_2}{\longleftrightarrow} \cdots \overset{r_k}{\longleftrightarrow} e_k \bigr\rangle
$$

Mũi tên hai chiều $\longleftrightarrow$ cho phép cạnh **thuận** $(e_{i-1}, r_i, e_i) \in G_R$ hoặc **ngược** $(e_i, r_i, e_{i-1}) \in G_R$. Điều này giúp path “đi ngược” (ví dụ từ item về user khác rồi sang item mới — kiểu collaborative filtering).  

### Định nghĩa bài toán

Cho $G_R$, user $u \in U$, số nguyên $K$ (độ dài path tối đa) và $N$ (số item gợi ý): tìm tập $\{i_n\}_{n=1}^N \subseteq I$ sao cho mỗi cặp $(u, i_n)$ gắn với **một** reasoning path $p_k(u, i_n)$ với $2 \le k \le K$.  

Ba thách thức thiết kế:

1. **Không có target item cố định** → không dùng binary reward “đúng/sai”.
2. **Out-degree rất lớn** ở một số node → cần pruning action thông minh.
3. **Đa dạng path** → tránh agent luôn lặp một kiểu path.  

***

## 3. Mô hình hóa MDP

Paper coi KGRE-Rec là **Markov Decision Process xác định** trên KG.  

### Bổ sung cạnh đặc biệt

- **Reverse edges**: nếu $(e,r,e') \in G_R$ thì thêm $(e',r,e)$.
- **Self-loop NO-OP**: $(e, r_{\text{noop}}, e)$ — agent có thể “dừng tại chỗ” nếu cần.  

### State $s_t$

$$
s_t = (u,\; e_t,\; h_t)
$$

| Ký hiệu | Ý nghĩa |
|--------|---------|
| $u$ | User xuất phát (cố định trong episode) |
| $e_t$ | Entity agent đang đứng ở bước $t$ |
| $h_t$ | Lịch sử $k$ bước gần nhất: $\{e_{t-k}, r_{t-k+1}, \ldots, e_{t-1}, r_t\}$ |

- State ban đầu: $s_0 = (u, u, \emptyset)$
- State kết thúc (horizon $T$): $s_T = (u, e_T, h_T)$  

**Intuition**: state không chỉ “đang ở đâu”, mà còn “bắt đầu từ ai” và “đã đi qua đâu” — cần cho policy cá nhân hóa theo user và tránh vòng lặp.

### Action $A_t$

Toàn bộ cạnh ra từ $e_t$, **loại** entity/relation đã đi qua (tránh cycle):

$$
A_t = \bigl\{ (r,e) \mid (e_t, r, e) \in G_R,\; e \notin \{e_0,\ldots,e_{t-1}\} \bigr\}
$$

### User-conditional action pruning

Out-degree theo long-tail → một số node có hàng nghìn cạnh. Paper cắt action space còn tối đa $\alpha$ cạnh “hứa hẹn nhất” theo user $u$:

$$
\tilde{A}_t(u) = \bigl\{ (r,e) \mid \operatorname{rank}\bigl(f((r,e)|u)\bigr) \le \alpha,\; (r,e) \in A_t \bigr\} \tag{1}
$$

- $f((r,e)|u)$: điểm số “edge $(r,e)$ có liên quan tới user $u$ không” (định nghĩa ở mục 4).
- $\alpha$: upper bound kích thước action space (thực nghiệm mặc định 250).  

**Intuition**: thay vì explore toàn bộ lân cận, chỉ giữ các bước “có vẻ hợp với user này” theo embedding multi-hop — vừa giảm chi phí vừa hướng agent về vùng đồ thị hữu ích.

### Reward (soft reward)

Không có item đích biết trước → **không** dùng reward nhị phân. Chỉ thưởng ở **terminal state**, và là **soft** (liên tục):

$$
R_T =
\begin{cases}
\max\left(0,\; \dfrac{f(u, e_T)}{\max_{i \in I} f(u,i)}\right) & \text{nếu } e_T \in I \$$6pt]
0 & \text{ngược lại}
\end{cases} \tag{2}
$$

| Đại lượng | Ý nghĩa |
|-----------|---------|
| $f(u, e_T)$ | Điểm “user $u$ thích entity $e_T$” (khi $e_T$ là item) |
| $\max_{i \in I} f(u,i)$ | Chuẩn hóa theo item “tốt nhất” của user trong không gian điểm |
| $\max(0,\cdot)$ | Cắt phần âm về 0 |
| Kết quả | $R_T \in [0,1]$ |

**Intuition**: path “tốt” là path dẫn tới item có điểm relevance cao với user theo KG embedding — không cần nhãn click/purchase cứng tại mỗi bước, agent được khuyến khích khám phá nhiều path tốt thay vì một target duy nhất.[file:1]

### Transition

Trên đồ thị, transition **xác định**:

$$
P\bigl[s_{t+1}=(u,e_{t+1},h_{t+1}) \mid s_t=(u,e_t,h_t),\; a_t=(r_{t+1},e_{t+1})\bigr] = 1 \tag{3}
$$

Riêng $s_0$ stochastic theo phân phối đều trên users.[file:1]

### Objective và REINFORCE

Học stochastic policy $\pi$ tối đa hóa expected cumulative reward:

$$
J(\theta) = \mathbb{E}_{\pi}\Biggl[\sum_{t=0}^{T-1} \gamma^t R_{t+1} \Bigm| s_0=(u,u,\emptyset)\Biggr] \tag{4}
$$

- $\gamma \in (0,1)$: discount factor (mặc định 0.99) — reward gần terminal quan trọng hơn một chút nhưng vẫn lan ngược.
- $R_{t+1}$: trong thiết kế paper, reward chủ yếu ở terminal ($R_T$); các bước giữa có thể 0.[file:1]

**Policy network + Value network** (cùng feature layers):

$$
\begin{align}
x &= \operatorname{dropout}\bigl(\sigma\bigl(\operatorname{dropout}(\sigma(s W_1)) W_2\bigr)\bigr) \tag{5} \\
\pi(\cdot \mid s, \tilde{A}_u) &= \operatorname{softmax}\bigl(\tilde{A}_u \odot (x W_p)\bigr) \tag{6} \\
\hat{v}(s) &= x W_v \tag{7}
\end{align}
$$

| Ký hiệu | Ý nghĩa |
|---------|---------|
| $s \in \mathbb{R}^{d_s}$ | Vector state = concat embedding $[u;\; e_t;\; h_t]$ (thực nghiệm size 400 với 1-step history) |
| $W_1, W_2$ | MLP trích feature ẩn $x \in \mathbb{R}^{d_f}$ |
| $\sigma$ | ELU |
| $\tilde{A}_u \in \{0,1\}^{d_A}$ | Mask nhị phân: 1 = action còn trong pruned space |
| $\odot$ | Hadamard product — **che** action không hợp lệ (prob = 0 sau softmax) |
| $W_p$ | Chiếu ra logits action |
| $\hat{v}(s)$ | Baseline value (giảm variance gradient) |
| $\Theta = \{W_1,W_2,W_p,W_v\}$ | Tham số học |

Policy gradient (REINFORCE with baseline):

$$
\nabla_{\Theta} J(\Theta) = \mathbb{E}_{\pi}\Bigl[\nabla_{\Theta}\log \pi_{\Theta}(\cdot\mid s,\tilde{A}_u)\,(G - \hat{v}(s))\Bigr] \tag{8}
$$

- $G$: discounted return từ $s_t$ tới $s_T$.
- Thêm entropy regularization $H(\pi)$ để khuyến khích **đa dạng path** (trọng số entropy loss ≈ 0.001).[file:1]

**Intuition pipeline**: agent “chơi game” trên KG — mỗi action là chọn cạnh tiếp theo; cuối episode nếu dừng ở item tốt (theo $f$) thì được thưởng; policy học cách đi từ user tới vùng item liên quan, đồng thời value network ước lượng “state này có tiềm năng không”.

***

## 4. Multi-hop scoring function

Đây là “la bàn” dùng cho **cả** action pruning **và** terminal reward, đồng thời huấn luyện embedding entity/relation.[file:1]

### Pattern và 1-reverse $k$-hop pattern

**$k$-hop pattern**: dãy quan hệ $\tilde{r}_k = \{r_1,\ldots,r_k\}$ sao cho khi biết type của $e_0$ và các $r$, type các entity giữa được xác định duy nhất (tính chất type-deterministic của schema KG recommendation).[file:1]

**1-reverse $k$-hop pattern** $\tilde{r}_{k,j}$: $j$ quan hệ đầu **xuôi**, các quan hệ sau **ngược**:

$$
e_0 \xrightarrow{r_1} \cdots \xrightarrow{r_j} e_j \xleftarrow{r_{j+1}} e_{j+1} \cdots \xleftarrow{r_k} e_k
$$

- $j=k$: toàn forward  
- $j=0$: toàn backward[file:1]

### Công thức scoring tổng quát

$$
f(e_0, e_k \mid \tilde{r}_{k,j})
=
\Biggl\langle
e_0 + \sum_{s=1}^{j} r_s,\;
e_k + \sum_{s=j+1}^{k} r_s
\Biggr\rangle
+ b_{e_k} \tag{9}
$$

| Đại lượng | Ý nghĩa |
|-----------|---------|
| $e, r \in \mathbb{R}^d$ | Embedding $d$-chiều của entity / relation (mặc định $d=100$) |
| $\sum_{s=1}^{j} r_s$ | “Dịch” $e_0$ theo chuỗi quan hệ xuôi (ý tưởng TransE: $e+r \approx e'$) |
| $\sum_{s=j+1}^{k} r_s$ | “Dịch” $e_k$ theo chuỗi quan hệ ngược |
| $\langle\cdot,\cdot\rangle$ | Dot product — đo độ khớp hai phía sau khi translate |
| $b_{e_k}$ | Bias của entity đích |

**Các trường hợp đặc biệt**:

- $k=0$: cosine-like  
  $f(e_0,e_k\mid\tilde{r}_{0,0}) = \langle e_0, e_k\rangle + b_{e_k}$ \quad (10)

- $k=1, j=1$ (TransE-style 1-hop):  
  $f(e_0,e_k\mid\tilde{r}_{1,1}) = \langle e_0 + r_1,\; e_k\rangle + b_{e_k}$ \quad (11)[file:1]

**Intuition hình học**: hai entity “gần nhau” nếu sau khi cộng vector quan hệ dọc theo pattern 1-reverse, chúng khớp trong không gian nhúng. Pattern reverse cho phép mô hình quan hệ kiểu “user–item–user–item” (CF) hoặc “user–feature–item”.

### Áp dụng cụ thể

1. **Action pruning**: với user $u$ và entity $e$, lấy $k_e$ nhỏ nhất sao cho tồn tại pattern hợp lệ;  
   $f((r,e)|u) = f(u, e \mid \tilde{r}_{k_e,j})$.[file:1]

2. **Reward**: chỉ dùng 1-hop user–item qua quan hệ purchase $r_{ui}$:  
   $f(u,i) = f(u,i \mid \tilde{r}_{1,1})$.[file:1]

### Học embedding (negative sampling)

Muốn maximize $P(e'\mid e, \tilde{r}_{k,j})$:

$$
P(e'\mid e,\tilde{r}_{k,j})
=
\frac{\exp\bigl(f(e,e'\mid\tilde{r}_{k,j})\bigr)}
{\sum_{e''\in\mathcal{E}}\exp\bigl(f(e,e''\mid\tilde{r}_{k,j})\bigr)} \tag{12}
$$

Xấp xỉ bằng negative sampling ($m$ mẫu âm $e''$):

$$
\log P \approx
\log\sigma\bigl(f(e,e'\mid\ldots)\bigr)
+ m\,\mathbb{E}_{e''}\bigl[\log\sigma\bigl(-f(e,e''\mid\ldots)\bigr)\bigr] \tag{13}
$$

Objective trên toàn KG:

$$
J(G_R)
=
\sum_{e,e'\in\mathcal{E}}
\sum_{k=1}^{K}
\mathbf{1}\{(e,\tilde{r}_{k,j},e')\}
\log P(e'\mid e,\tilde{r}_{k,j}) \tag{14}
$$

$\mathbf{1}\{\cdot\}=1$ khi pattern hợp lệ giữa $(e,e')$.[file:1]

Mặc định train embedding bằng **1-hop**; ablation cho thấy thêm **2-hop scoring** vào objective còn cải thiện thêm recommendation.[file:1]

***

## 5. Policy-Guided Path Reasoning (suy luận)

Sau khi train policy, **không** chỉ sample ngẫu nhiên theo $\pi$ (dễ lặp path “best” duy nhất). Paper dùng **beam-style search** có hướng dẫn bởi policy + reward (Algorithm 1).[file:1]

### Thuật toán (tóm tắt)

**Input**: user $u$, policy $\pi$, horizon $T$, kích thước sample từng bước $K_1,\ldots,K_T$.

1. Khởi tạo: path $\{u\}$, prob = 1, reward = 0.
2. Với mỗi bước $t = 1..T$:
   - Với mỗi path đang giữ:
     - Lấy pruned action space $\tilde{A}_{t-1}(u)$.
     - Lấy xác suất $p(a)=\pi(a\mid s,\tilde{A})$.
     - Chỉ giữ top-$K_t$ action theo $p(a)$.
     - Mở rộng path, nhân xác suất, cộng reward.
3. Cuối cùng chỉ giữ path **kết thúc bằng item**.
4. Với mỗi cặp $(u,i)$: chọn path có **generative probability** cao nhất làm lời giải thích.
5. Xếp hạng các path đã chọn theo **path reward** $R_T$ → top-$N$ recommendation.[file:1]

Thực nghiệm điển hình: path length $T=3$; CDs & Vinyl dùng $(K_1,K_2,K_3)=(20,10,1)$; dataset khác $(25,5,1)$. Action dropout 0.5 trên pruned space để tăng đa dạng khi train.[file:1]

**Intuition**: $K_t$ lớn ở bước đầu → mở rộng kiểu path; bước cuối $K_T=1$ → chốt item tốt nhất theo policy. Như vậy vừa đa dạng vừa có chất lượng.

***

## 6. Pipeline tổng thể (Hình 2)

```text
[KG Environment]
       ↑ interact
[RL Agent: Policy + Value]
       | train (REINFORCE + soft reward + pruning)
       ↓
[Policy-Guided Beam Search]
       ↓
{ items + reasoning paths }  →  recommendation + explanation
```

Hai giai đoạn tách biệt rõ: (1) học policy trên MDP; (2) suy luận path có hướng dẫn policy để xuất item + giải thích.[file:1]

***

## 7. Thực nghiệm

### Dữ liệu

Bốn domain Amazon: **CDs & Vinyl, Clothing, Cell Phones, Beauty**.  
Mỗi domain: 5 loại entity (User, Item, Feature, Brand, Category), 7 loại quan hệ (Purchase, Mention, Described_by, Belong_to, Produced_by, Also_bought, Also_viewed, Bought_together…). Feature được lọc TF-IDF. Split 70% train / 30% test purchases.[file:1]

### Baseline & metric

BPR, BPR-HFT, VBPR, TransRec, DeepCoNN, CKE, JRL.  
Metric top-10: NDCG, Recall, Hit Rate, Precision.[file:1]

### Kết quả chính

PGPR **vượt** mọi baseline trên cả 4 dataset. Ví dụ cải thiện NDCG so với best baseline (JRL): ~3.9% (CDs), ~65% (Clothing), ~15.5% (Cell Phones), ~24% (Beauty).[file:1]

Thống kê path: ~50%+ path sample là valid (user → … → item trong ≤3 hop); mỗi item gợi ý trung bình ~1.6 path hỗ trợ → có thể đưa nhiều lời giải thích nếu user cần.[file:1]

### Ablation quan trọng

| Yếu tố | Quan sát |
|--------|----------|
| Kích thước pruned action $\alpha$ | $\alpha$ nhỏ hơn thường tốt hơn — scoring pruning lọc đúng; $\alpha$ lớn tốn explore |
| Multi-hop scoring (2-hop) trong train embedding | Cải thiện thêm so với chỉ 1-hop |
| Sampling sizes $(K_1,K_2,K_3)$ | Hai bước đầu quyết định mạnh; cần $K_1,K_2$ đủ lớn |
| History trong state | 0-step kém rõ; 1-step tốt nhất; 2-step hơi kém hơn (nhiễu/thừa) |[file:1]

***

## 8. Case study: path patterns và ví dụ thật

Với $T=3$, model tìm được **15 pattern** path khác nhau. Một pattern điển hình kiểu CF:

$$
\text{user} \xrightarrow{\text{purchase}} \text{item} \xleftarrow{\text{purchase}} \text{user} \xrightarrow{\text{purchase}} \text{item}
$$

(“user khác cũng mua item này / item kia”).[file:1]

Ví dụ diễn giải (Beauty / fashion / electronics):

1. User mua **shampoo** được mô tả bởi feature “nourish”, “lightening” → gợi ý **conditioner** cũng có hai feature đó.  
2. Hai user cùng mention “run”, “comfort” → chuyển purchase history của user này sang user kia (**running shoes**).  
3. User mua iPhone, viewed charger line; pattern also_bought → gợi ý **phone case**.  
4. User mua neck chain thuộc category “Hello Kitty” → gợi ý **keychain** cùng category.[file:1]

Điểm then chốt: path **không** gắn sau khi đã chọn item; chúng **là** quá trình quyết định của agent.

***

## 9. Đóng góp và hướng mở rộng

**Bốn đóng góp** paper nêu:

1. Formal hóa KGRE-Rec: recommendation = reasoning tường minh trên KG.  
2. RL với soft reward + user-conditional pruning + multi-hop scoring.  
3. Policy-guided beam search sinh path đa dạng, hiệu quả.  
4. Thực nghiệm quy mô lớn trên Amazon, vừa accuracy vừa explainability.[file:1]

Hướng future: product search, social recommendation, đồ thị **theo thời gian** (dynamic KG).[file:1]

***

## 10. Tóm tắt intuition một dòng

> **PGPR dạy một agent RL “đi bộ” trên knowledge graph từ user tới item; điểm thưởng lấy từ multi-hop embedding; mỗi lần gợi ý mang theo chính con đường agent đã đi — đó vừa là ranking signal vừa là lời giải thích có thể đọc được.**[file:1]
