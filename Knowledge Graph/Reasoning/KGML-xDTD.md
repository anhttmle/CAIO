Paper này (KGML-xDTD) đề xuất một framework 2-module trên biomedical knowledge graph để vừa **dự đoán** thuốc có thể điều trị bệnh nào (drug repurposing) vừa **giải thích cơ chế tác động (MOA)** bằng các đường đi trên KG, với phần trực giác khá rõ ràng nếu nhìn nó như một graph-RAG cho thuốc–bệnh.  

Dưới đây mình sẽ trình bày theo hướng “intuition-first”, rồi giải thích chi tiết các công thức và khái niệm chính.

***

## 1. Bài toán và trực giác tổng thể

Mục tiêu:  
- Cho một đồ thị tri thức sinh học rất lớn (RTX-KG2c: ~6.4M node, ~39M edge, sau khi lọc còn ~3.6M node, ~18.3M edge).  
- Sử dụng dữ liệu từ nhiều nguồn (MyChem, SemMedDB, NDF-RT, RepoDB) để biết cặp drug–disease nào là “treat”, “not treat” hoặc “contraindication/failed”.  
- Xây một hệ thống:
  - Module 1: dự đoán xác suất một thuốc điều trị một bệnh (link prediction).  
  - Module 2: tìm các đường đi ngắn (3-hop) từ drug đến disease trên KG, sao cho đường đi này có ý nghĩa sinh học (MOA path).  

Trực giác:  
- Module 1 giống như một mô hình embedding + classifier trên KG: học embedding node (drug/disease) dùng GraphSAGE, concat và cho vào random forest để phân loại “treat / not treat / unknown”.  
- Module 2 giống một agent RL đi dọc theo KG từ drug đến disease, được **shape reward** bằng:
  - Kết quả dự đoán của Module 1 (terminal reward).  
  - Một tập “demonstration paths” từ kiến thức và publication (DrugBank, Molecular Data Provider, PubMed NGD) để cung cấp intermediate reward thông qua 2 discriminator.  

Bạn có thể xem cả framework như:  
- Module 1: “scoring function f(drug, disease)”.  
- Module 2: “policy π trên graph, ưu tiên đi theo các kiểu meta-path giống demonstration, và kết thúc tại các disease mà f dự đoán là treat”.

***

## 2. Dữ liệu và chuẩn bị KG

### Customized RTX-KG2c

- Xuất phát từ RTX-KG2c canonicalized: chuẩn Biolink, merge synonym node, lấy từ ~70 nguồn (DrugBank, ChEMBL, HMDB,...).  
- Họ áp dụng 4 bước lọc để phù hợp bài toán repurposing:  
  1. Loại các category không liên quan (GeographicLocation, Device, ...).  
  2. Lọc edge chất lượng thấp theo tiêu chí riêng (chi tiết trong supplement).  
  3. Loại edge dư thừa về thứ bậc (hierarchical redundancy).  
  4. Bỏ hết edge drug–disease trực tiếp để việc dự đoán link là thật sự “novel”.  

Sau lọc:  
- 3,659,165 nodes với 33 category (Drug, SmallMolecule, Gene, Disease, Pathway,...).  
- 18,291,237 edges với 74 predicate (increases activity of, interacts with, gene associated with condition,...).  

### Bộ dữ liệu label cho DRP module

4 nguồn chính:  

- MyChem: label “indication” = true positive (treat), “contraindication” = true negative (not treat).  
- SemMedDB: từ PubMed, quan hệ “treats” = true positive, “negatively treats” = true negative.  
- NDF-RT: từ VHA, “indications” vs “contraindications”.  
- RepoDB: clinical trials “approved” vs “terminated”.  

Với SemMedDB, họ thêm một bước lọc dựa trên **co-occurrence** và **normalized Google distance (NGD)** để giảm bias và lỗi NLP:  

Ngữ nghĩa: NGD đo “khoảng cách semantic” giữa 2 concept dựa trên số PubMed co-occurrence.

Công thức (1):  
$$
NGD(c_1, c_2) = \frac{\max\{\log N(c_1), \log N(c_2)\} - \log N(c_1, c_2)}{\log N - \min\{\log N(c_1), \log N(c_2)\}}
$$
  

Trong đó:  
- $c_1, c_2$: hai concept (drug/disease) trong KG.  
- $N(c_1), N(c_2)$: số PubMed ID unique có chứa lần lượt $c_1, c_2$.  
- $N(c_1, c_2)$: số PubMed ID unique chứa **cả** $c_1$ và $c_2$.  
- $N$: tổng số cặp MeSH term annotation trong toàn bộ PubMed.  

Trực giác:  
- Nếu $c_1, c_2$ **hay xuất hiện cùng nhau**, thì $\log N(c_1, c_2)$ lớn ⇒ numerator nhỏ ⇒ NGD nhỏ (gần 0).  
- NGD càng nhỏ ⇒ 2 concept càng “gần nhau” về mặt thông tin.  
- Họ giữ chỉ những cặp SemMedDB có ≥10 publication và NGD ≤ 0.6 ⇒ đảm bảo relationship “treats” là có nền tảng mạnh.  

Sau hợp, mapping ID và loại trùng lặp: tổng cộng ~21,437 treat pairs và 33,189 not-treat pairs, với một phần là “shared” xuất hiện ở ≥2 nguồn.  

### DrugMechDB cho MOA evaluation

- DrugMechDB: database human-curated của 3,593 MOA paths cho 3,327 cặp drug–disease, trích từ DrugBank, Wikipedia,..., theo schema Biolink.  
- Khớp node của DrugMechDB sang RTX-KG2c bằng Node Synonymizer.  
- Do RL chỉ tìm path tối đa 3-hop, họ định nghĩa một path 3-hop trong KG là “correct” nếu **tất cả 4 node** xuất hiện trong một MOA path đầy đủ của DrugMechDB cho cặp drug–disease đó.  
- Tìm được 472 cặp drug–disease có ít nhất 1 path 3-hop như vậy, dùng để làm external validation cho MOA prediction.  

***

## 3. DRP module: GraphSAGE + Random Forest

### Notation và bài toán

- KG $G = \{V, E\}$: directed.  
  - Node $v \in V$: entity sinh học (drug, disease, gene, pathway,...).  
  - Edge $e \in E$: relationship (e.g. interacts-with).  
- $V_{drug}$: tập node thuộc category “Drug” hoặc “Small Molecule”.  
- $V_{disease}$: tập node “Disease”, “PhenotypicFeature”, “BehavioralFeature”, “DiseaseOrPhenotypicFeature”.  
- **Embedding notation**: ký hiệu in đậm là embedding, ví dụ $ \mathbf{v}$ là embedding của node $v$.  

Drug repurposing được mô hình hóa như link prediction:  
- Input: cặp $(v_i, v_j)$ với $v_i \in V_{drug}$, $v_j \in V_{disease}$.  
- Output: probability “drug i treats disease j”.

### Learning node embeddings: 2 nguồn thông tin

Trực giác: mỗi node embedding nên encode:  
1. **Neighborhood structure** (topology).  
2. **Attribute / semantic** (tên + category, ngôn ngữ tự nhiên).  

#### (a) Neighborhood bằng GraphSAGE với random walk loss

Họ dùng GraphSAGE để học embedding sao cho:  
- Node hàng xóm (co-occurs trong random walks) có embedding giống nhau.  
- Node không liên quan được “push away”.  

Cho một node $u$, loss (2):  
$$
L_G(\mathbf{z}_u) = - \log(\sigma(\mathbf{z}_u^\top \mathbf{z}_v)) - k \cdot \mathbb{E}_{v_n \sim P_n(v)} \log(\sigma(\mathbf{z}_u^\top \mathbf{z}_{v_n}))
$$
  

Giải thích từng đại lượng:

- $\mathbf{z}_u, \mathbf{z}_v$: embedding của node $u, v$.  
- $\sigma$: sigmoid, $\sigma(x) = 1 / (1 + e^{-x})$.  
- $v$: node xuất hiện cùng $u$ trong random walks cố định độ dài (positive context).  
- $P_n$: distribution để negative sampling (chọn node không thuộc neighborhood).  
- $k$: số negative sample cho mỗi positive.  

Intuition:  
- Term $- \log(\sigma(\mathbf{z}_u^\top \mathbf{z}_v))$: muốn $\mathbf{z}_u^\top \mathbf{z}_v$ lớn (similar) ⇒ sigmoid gần 1 ⇒ loss nhỏ.  
- Term $- k \mathbb{E}_{v_n} \log(\sigma(\mathbf{z}_u^\top \mathbf{z}_{v_n}))$: với negative, muốn dot product nhỏ ⇒ sigmoid nhỏ ⇒ log nhỏ (âm), càng âm càng tốt ⇒ giảm loss.  
- Đây giống negative sampling loss của word2vec, nhưng áp dụng lên node embedding.

#### (b) Node attribute bằng PubMedBERT + PCA

- Với mỗi node, họ lấy string **name + category**, cho vào PubMedBERT (pretrained LM cho biomedical text) để tạo attribute embedding.  
- Sau đó giảm chiều bằng PCA xuống 100 dimensions để tiết kiệm memory.  
- Embedding này được dùng như initial feature cho GraphSAGE, nên final node embedding kết hợp được cả **text semantics** và **graph structure**.  

### Từ embedding đến classification: Random Forest

- Với cặp $(v_{drug}, v_{disease})$, họ concat embedding: $\mathbf{z}_{pair} = [\mathbf{z}_{drug} ; \mathbf{z}_{disease}]$.  
- Cho vào random forest để phân loại 3 lớp: “not treat”, “treat”, “unknown”.  

Nhãn:  
- “treat” / “not treat” lấy từ 4 nguồn như trên.  
- “unknown” sinh bằng negative sampling: với mỗi cặp treat, họ:  
  - Thay drug bằng một drug random ≠ original  
  - Thay disease bằng một disease random ≠ original  
  - Cặp mới không xuất hiện trong cả treat và not-treat ⇒ label “unknown”.  

Trực giác:  
- “unknown” = cặp chưa biết, không chắc là không điều trị, giúp mô hình học thêm phân biệt giữa “chắc chắn không” và “chưa biết”.  
- Kết quả ablation cho thấy việc thêm lớp “unknown” cải thiện mạnh các ranking metrics (MRR, Hit@K) vì giảm false positives.  

### Đánh giá DRP module và insight

Các metric:

- Accuracy: $\text{ACC} = \frac{\# correct}{\# all}$.  
- Macro-F1: trung bình F1 cho mỗi lớp.  
- Ranking metrics: MRR & Hit@K dựa trên việc rank đúng treat cặp giữa nhiều candidate tạo bằng replacement (thay drug, thay disease).  

So với baseline (TransE, TransR, RotatE, DistMult, ComplEx, ANALOGY, SimplE, GAT, GraphSAGE variants):  
- KGML-xDTD có accuracy ~0.935, macro-F1 ~0.923; tương đương hoặc tốt hơn GAT, và vượt hầu hết translational/bilinear models.  
- Về MRR và Hit@K, KGML-xDTD vượt trội rõ rệt (MRR ~0.382, Hit@1 ~0.238, Hit@5 ~0.543 trong setting random replacement).  
- Version “KGML-xDTD w/o NAEs” (không dùng PubMedBERT attribute) có ranking metrics kém hơn rõ => attribute embedding rất **quan trọng**.  
- Version “2-class KGML-xDTD” (chỉ treat vs not-treat, không unknown) có accuracy cao nhưng ranking thấp hơn version 3-class => lớp “unknown” hữu ích cho repurposing thật (giảm false positives).  

Intuition:  
- GraphSAGE + RF là một cách “hybrid”: GNN để embed, RF để classification, lợi thế là RF xử lý tốt feature non-linear và distribution phức tạp, đồng thời cho khả năng rank tốt khi dùng probability “treat”.  

***

## 4. MOA prediction module: Adversarial Actor–Critic RL

Module này giải bài toán:  
- Đã có candidate indication từ DRP module, làm sao giải thích **tại sao** drug đó có thể treat disease đó bằng cách tìm path trên KG.

### State definition

Mỗi state $s_t$ tại time step $t$:  

$$
s_t = (v_{drug}, v_t, (v_{t-1}, e_t), ..., (v_{t-K}, e_{t-(K-1)}))
$$
  

Giải thích:

- $v_{drug} \in V_{drug}$: node drug xuất phát (fixed cho episode).  
- $v_t \in V$: node hiện tại của agent ở bước $t$.  
- $(v_{t-k}, e_{t-(k-1)})$: các node & predicate của K bước trước đó, để RL có context path (history).  
- State embedding $\mathbf{s}_t$: concat embedding của tất cả node & predicate trong state.  
  - Node embedding: dùng attribute embedding từ PubMedBERT (như DRP).  
  - Predicate embedding: one-hot + learned embedding.  
- Với state initial $s_0$: các node/predicate trước đó là dummy node/predicate đặc biệt.  

Intuition:  
- RL agent cần biết đang đi trên path nào (context) để phân biệt các meta-path khác nhau (Drug→Gene→Pathway→Disease vs Drug→Protein→Disease...).  
- Việc encode K-step history vào state giúp actor học các policy “meta-path-aware”.

### Action space

Tại node $v_t$, action space $A_t$:  

$$
A_t = (a_{self}, a_1, ..., a_k, ..., a_{n_{v_t}})
$$
  

Trong đó:

- $a_{self}$: self-loop action (ở lại node).  
- Các $a_k = (e_t, v_{t+1})$: đi theo một outgoing edge $e_t$ đến neighbor $v_{t+1}$.  
- $n_{v_t}$: out-degree của node $v_t$.  

Vì nhiều node có out-degree rất lớn (>3000), họ **prune** neighbor action bằng PageRank score: chỉ giữ những neighbor có PageRank cao để giảm không gian hành động.  

Action embedding $\mathbf{a}_t$: concat embedding predicate + node của action.  

### Reward design

Có 3 loại reward:

1. Terminal reward từ môi trường $R_{e,T}$.  
2. Intermediate reward từ **path discriminator** $R_{p,t}$.  
3. Intermediate reward từ **meta-path discriminator** $R_{m,t}$.  

#### (a) Terminal reward $R_{e,T}$: dùng DRP module

Khi agent dừng tại step T (kết thúc path), node cuối $v_T$, tập $\mathcal{N}_{drug}$ là các disease đã biết là được drug $v_{drug}$ điều trị.  

$$
R_{e,T} =
\begin{cases}
1, & v_T \in \mathcal{N}_{drug} \\
p_{treat}, & v_T \notin \mathcal{N}_{drug}, v_T \in V_{disease} \text{ và } f(v_{drug}, v_T) \text{ dự đoán "treat"} \\
0, & v_T \notin \mathcal{N}_{drug}, v_T \in V_{disease} \text{ và } f(v_{drug}, v_T) \text{ không là "treat"} \\
-1, & v_T \notin V_{disease}
\end{cases}
$$
  

Trong đó:

- $p_{treat}$: probability lớp “treat” từ DRP model $f$.  

Intuition:

- Nếu path kết thúc ở disease đã biết là được treat ⇒ reward = 1 (ground truth).  
- Nếu kết thúc ở disease mới nhưng DRP model dự đoán có khả năng treat ⇒ reward = $p_{treat}$: khuyến khích tìm path đến disease có **tiềm năng** repurposing.  
- Nếu disease nhưng không treat ⇒ 0.  
- Nếu không phải disease ⇒ -1 (đường đi vô nghĩa về MOA).

Note: RL không có intermediate environment reward: $R_{e,t} = 0$ cho $t < T$.  

#### (b) Path discriminator và reward $R_{p,t}$

- Path discriminator $D_p(s, a)$ là một binary classifier: phân biệt segment $(s_t, a_t)$ thuộc:  
  - Demonstration paths (positive).  
  - Actor-generated non-demonstration paths (negative).  

Loss (6):  
$$
L_p = -\mathbb{E}_{(s,a) \sim P_D}[\log D_p(s,a)] - \mathbb{E}_{(s,a) \sim P_A}[\log(1 - D_p(s,a))]
$$
  

Giải thích:  
- $P_D$: distribution của segment từ demonstration paths (true MOA-like paths).  
- $P_A$: distribution của segment từ actor tạo ra nhưng không thuộc demonstration.  
- Training như một logistic regression classifier.

Intermediate reward (7):  
$$
R_{p,t} = \log D_p(s_t, a_t) - \log(1 - D_p(s_t, a_t))
$$
  

Intuition:  
- Nếu segment “giống” demonstration ⇒ $D_p \approx 1$, reward lớn dương.  
- Nếu không giống ⇒ $D_p \approx 0$, reward âm.  
- Đây là dạng **log-odds** reward, làm smooth gradient.

#### (c) Meta-path discriminator và reward $R_{m,t}$

Meta-path = chuỗi category node trên path, ví dụ:  
`Drug → Gene → BiologicalProcess → Disease`.  

- Meta-path embedding $\mathbf{M}$: concat embedding category của node trên path.  
- Discriminator $D_m(M)$: binary classifier xem meta-path có giống meta-path của demonstration paths hay không.  

Loss (8):  
$$
L_m = -\mathbb{E}_{M \sim P_D^M}[\log D_m(M)] - \mathbb{E}_{M \sim P_A^M}[\log (1 - D_m(M))]
$$
  

Intermediate reward (9):  
$$
R_{m,t} = \log D_m(M) - \log(1 - D_m(M))
$$
  

Intuition:  
- Path discriminator nhìn **segment local**, meta-path discriminator nhìn **pattern toàn path** (type-level).  
- Kết hợp cả hai giúp agent học được “kiểu đường đi hợp lý về mặt category” chứ không chỉ copy một số segment.

#### (d) Tổng reward tại bước t

Reward tổng hợp $R_t$ tại bước $t$:  

$$
R_t = \alpha_p R_{p,t} + \alpha_m R_{m,t} + (1 - \alpha_p - \alpha_m)\gamma^{T-t} R_{e,T}
$$
  

Trong đó:

- $\alpha_p \in [0,1]$, $\alpha_m \in [0, 1 - \alpha_p]$: hệ số pha trộn giữa 2 intermediate rewards.  
- $\gamma$: decay coefficient (discounting) để terminal reward ảnh hưởng ít hơn ở bước sớm.  
- $R_{e,T}$: terminal reward từ DRP module.  

Intuition:

- Early steps chủ yếu chịu influence từ $R_{p,t}, R_{m,t}$ (path guidance).  
- Closer to terminal, discount nhỏ hơn ⇒ terminal reward từ DRP bắt đầu quan trọng hơn.  
- Đây là một kiểu **reward shaping** để RL từ sparse reward (chỉ tại T) thành dense reward.

### Actor–Critic kiến trúc

4 subnetworks, cùng kiến trúc MLP^i, khác parameters.  

MLP (3):  
$$
MLP^i(\mathbf{X}) = BA(BA(\mathbf{X}\mathbf{W}_1^i + \mathbf{b}_1^i)\mathbf{W}_2^i + \mathbf{b}_2^i)\mathbf{W}_3^i + \mathbf{b}_3^i
$$
  

Trong đó:

- $\mathbf{W}_k^i, \mathbf{b}_k^i$: weight, bias của linear layer thứ k trong network $i$.  
- BA: batch normalization + ELU activation.  

#### (a) Actor network

Policy $\pi_\theta(a_t | s_t, A_t)$:  

$$
\pi_\theta(a_t | s_t, A_t) = \text{softmax}(\mathbf{A}_t \odot MLP^a(\mathbf{s}_t))
$$
  

- $\mathbf{A}_t$: matrix embedding của action space $A_t$ (mỗi row là $\mathbf{a}$).  
- $\odot$: dot product (ở đây là matrix-vector multiplication, mỗi action embedding dot với vector output của MLP^a).  
- Softmax: chuyển các score thành distribution trên actions.

Intuition:  
- MLP^a học một vector “preference” cho state.  
- Dot với từng action embedding ⇒ score mỗi action.  
- Softmax ⇒ xác suất chọn action: policy gradient RL.

#### (b) Critic network

Critic estimate Q-value $Q_\phi(s_t, a_t)$:  

$$
Q_\phi(s_t, a_t) = MLP^c(\mathbf{s}_t) \odot \mathbf{a}_t
$$
  

- MLP^c tạo vector representation cho state.  
- Dot với action embedding ⇒ ước lượng reward kỳ vọng nếu chọn action đó.

Loss critic (11): TD-error squared:  

$$
L_c = TD^2 = [(R_t + Q_\phi(s_{t+1}, a_{t+1})) - Q_\phi(s_t, a_t)]^2
$$
  

Intuition:  
- Cập nhật critic để xấp xỉ Bellman equation: Q(s,a) gần reward hiện tại + Q(next).

#### (c) Actor optimization với REINFORCE + entropy

Goal: maximize $J(\theta) = \mathbb{E}_{a \sim \pi_\theta}[Q_\phi(s_t, a)]$.  

Dùng REINFORCE với entropy regularization: gradient (12):  

$$
\nabla_\theta L_a = -\nabla_\theta J(\theta) = -\mathbb{E}_{\pi_\theta}[\nabla_\theta TD \cdot \log \pi_\theta(a_t | s_t)] - \alpha \nabla_\theta entropy(\pi_\theta)
$$
  

Trong đó:

- $TD$: TD-error (giống ở critic).  
- $\alpha$: hệ số entropy weight (khuyến khích policy có entropy cao ⇒ hard-exploration).  

Intuition:  
- Term đầu: policy gradient, scale bởi TD-error (advantage).  
- Term entropy: giữ policy “explorative”, tránh collapse vào một vài path.

#### (d) Path & meta-path discriminator training

- Train bằng các loss $L_p, L_m$ như trên, với positive samples là demonstration paths, negative samples là actor-generated segments.  

### Training schedule (multi-stage)

Theo Zhao et al. 2019 (ADAC RL):  

1. **Behavior cloning**:  
   - Khởi tạo actor bằng supervised learning trên demonstration paths (imitate).  
   - Loss = MSE giữa action actor output và “expert” action từ demonstration.  

2. Freeze actor & critic trong **z epoch** đầu, train discriminators:  
   - Train path discriminator $D_p$ minimising $L_p$.  
   - Train meta-path discriminator $D_m$ minimising $L_m$.  

3. Sau z epoch, unfreeze actor & critic, tối ưu joint loss:  
   - $L_{joint} = L_a + L_c$.  

Intuition:  
- Giai đoạn 1: policy bắt chước expert path, giảm khó khăn RL ban đầu.  
- Giai đoạn 2: discriminators học phân biệt expert vs agent paths để cung cấp intermediate reward meaningful.  
- Giai đoạn 3: actor–critic sử dụng reward shaping từ discriminators + DRP để refine policy.

***

## 5. Path scoring và evaluation cho MOA

Sau khi có policy đã train, họ:  
- Tính **path score** cho mỗi đường đi 3-hop giữa drug và disease:  

Công thức (18):  
$$
\text{path score} = \sum_{i=1}^{k} \delta^{i-1} \times \log(P_i \times N_i)
$$
  

Trong đó:

- $k$: số hops (ở đây tối đa 3).  
- $\delta$: decay coefficient (set = 0.9).  
- $P_i$: probability chọn action $a_i$ ở hop i theo policy RL.  
- $N_i$: số action khả dụng ở hop i (kích thước action space).  

Intuition:  
- $\log(P_i \times N_i)$: nếu một action được chọn với probability cao **trong một action space lớn** ⇒ log lớn ⇒ đóng góp cao.  
- Decay $\delta^{i-1}$: hop gần đầu path đóng góp mạnh hơn (phản ánh tầm quan trọng của bước đầu).  
- Summation: score tổng cho path, dùng để rank tất cả các path candidate.

Evaluation:

- Với mỗi cặp drug–disease có DrugMechDB-matched 3-hop path, lấy thứ hạng tốt nhất của các matched path trong toàn bộ 3-hop paths làm rank đại diện.  
- Tính metrics:  
  - MPR (mean percentile rank) path đúng.  
  - MRR và Hit@K (Hit@1, 10, 50, 100, 500).  

Baseline:

- MultiHop RL (Lin et al. 2018), dùng LSTM agent và reward shaping tương tự, nhưng không có demonstration path discriminator/actor-critic.  
- KGML-xDTD w/o DP: ablation set $\alpha_p = \alpha_m = 0$, tức bỏ hết demonstration rewards, chỉ dựa trên terminal reward.  

Kết quả (Table 3):

- MultiHop: MPR ~61.4%, MRR ~0.027, Hit@1 ~0.017.  
- KGML-xDTD w/o DP: MPR ~72.97%, MRR ~0.015, Hit@1 ~0.008.  
- KGML-xDTD full: MPR ~94.70%, MRR ~0.109, Hit@1 ~0.059, Hit@100 ~0.613, Hit@500 ~0.849.  

Intuition:

- Việc dùng demonstration paths như “expert guidance” cực kỳ quan trọng để RL agent tìm được path sinh học reasonable trong search space cực lớn và reward sparse.  
- Actor–critic với discriminator outperform MultiHop LSTM khi có guidance.  
- KGML-xDTD w/o DP > MultiHop về MPR nhưng < về MRR/Hit@K, cho thấy cấu trúc actor–critic tương đương LSTM nếu thiếu guidance; thêm guidance mới tạo gain lớn.

***

## 6. Case study và insight về cơ chế

Hai case chính:

1. **Hemophilia B**  
   - Lấy top predicted drugs, nhiều cái khớp với literature (Eptacog Alfa, Nonacog Alfa, Factor VIIa, Factor IX, Thrombin, Viral vector,...).!  
   - So sánh predicted 3-hop paths với DrugMechDB MOA paths, thấy có các entity quan trọng trong coagulation network: Factor VII, X, IX, TFPI, F2 (thrombin), v.v.  
   - Path graph cho thấy mối liên hệ như “gene product of”, “gene associated with condition”, “entity negatively regulates entity”, tương thích với network ở Fig. 4.  

2. **Huntington’s disease**  
   - Top drugs: cả training (Pimozide, Olanzapine, Riluzole, Antipsychotics) và không trong training (Risperidone, Entinostat, Primaquine, Isradipine, Amifampridine).  
   - Predicted paths cho non-train drugs cho thấy cơ chế liên quan đến:
     - Risperidone: giảm activity các 5-HT receptor gene (HTR1A, 2A, 2C, 7) và DRD2 ⇒ liên quan depression trong HD.  
     - Entinostat: giảm activity HDAC1, HDAC6; tương tác với Histone H4, HIF1A, CTNNB1 ⇒ phù hợp nghiên cứu về HDAC inhibition trong HD.  
     - Primaquine: tương tác IKBKG, NF-κB pathway ⇒ liên quan neurodegeneration.  
     - Isradipine: liên quan CACNA1C, CACNB2 (CaV channels) ⇒ depression/dementia.  
     - Amifampridine: điều tiết KCNA1, KCNC2/3, DLG4, liên quan chorea và neurodegeneration.  

Trực giác:

- MOA paths ở đây giống một graph-RAG explanation: bắt bridge giữa predicted indication và known regulatory network, highlight các gene/protein/quá trình quan trọng.  
- Điều này làm giảm “black-box” cảm giác của DRP module.

***

## 7. Ý nghĩa và hạn chế

Ý nghĩa kỹ thuật:

- Framework **2-module** rất giống pattern bạn đang quan tâm:  
  - Module 1: representation + prediction trên KG (GraphSAGE+RF).  
  - Module 2: graph RL với reward shaping và demonstration (knowledge-guided exploration).  
- Dùng large mixed biomedical KG (RTX-KG2c), không bị bó hạn chỉ literature-based hay database-based.  
- Exploit PubMedBERT để embed node semantics, cho thấy sức mạnh của LM embedding trong KG tasks.  

Hạn chế & hướng phát triển:

- Path chỉ tối đa 3-hop vì memory/time; nhiều MOA sinh học dài hơn, nên explanation vẫn khá coarse.  
- Không xử lý explicit “negative MOA” (tại sao thuốc có hại). Tác giả đề xuất future work cho việc này.  
- Training/inference resource rất lớn (800 GB RAM, 48GB GPU, training ~2 tuần).  

***

Nếu bạn muốn, mình có thể giúp thiết kế một phiên bản “KGML-xDTD for generic graph-RAG on software/tech knowledge” với mô đun RL path-finding tương tự nhưng trên KG domain của bạn (VD: API → service → infra → incident). Bạn muốn đào sâu phần nào trước: DRP module (GraphSAGE+RF) hay RL path-finding + discriminator?  
