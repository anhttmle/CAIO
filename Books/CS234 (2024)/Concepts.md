# [Lecture 1: Introduction to Reinforcement Learning](https://www.youtube.com/watch?v=WsvFL-LjA6U)

### 1. Khái niệm nền tảng về RL
* **Reinforcement Learning (Học tăng cường):** Tác nhân tự động học hỏi thông qua trải nghiệm để đưa ra quyết định tối ưu (0:26).
* **Sequential Decision Making (Ra quyết định tuần tự):** Bài toán ra quyết định dưới sự không chắc chắn (56:07).
* **Agent (Tác nhân):** Thực thể tương tác với môi trường để nhận quan sát và phần thưởng (56:10).
* **Exploration (Khám phá):** Thử nghiệm các hành động mới để thu thập thông tin (20:10).
* **Generalization (Tổng quát hóa):** Khả năng áp dụng kiến thức vào các không gian trạng thái lớn (21:12).
* **Delayed Consequences (Hậu quả trễ):** Các quyết định hiện tại ảnh hưởng đến phần thưởng trong tương lai (17:02).

### 2. Các thành phần của Markov Decision Process (MDP)
* **State Space (Không gian trạng thái - S):** Tập hợp các trạng thái của môi trường (41:59).
* **Action Space (Không gian hành động - A):** Tập hợp các hành động tác nhân có thể thực hiện (42:01).
* **Dynamics Model (Mô hình động học):** Quy luật chuyển đổi trạng thái $P(s'|s, a)$ (53:27, 1:08:30).
* **Reward Model (Mô hình phần thưởng):** Giá trị nhận được sau hành động (42:03, 1:09:22).
* **Policy (Chính sách - $\pi$):** Ánh xạ từ trạng thái sang hành động (21:20, 1:11:13).
* **Markov Property (Tính chất Markov):** Tương lai độc lập với quá khứ khi biết hiện tại (1:00:48).

### 3. Phương pháp tiếp cận và thuật toán
* **Imitation Learning (Học bắt chước) / Behavior Cloning:** Học từ các ví dụ của chuyên gia (6:35, 23:59).
* **Reinforcement Learning from Human Feedback (RLHF):** Sử dụng phản hồi của con người để định hình phần thưởng (8:55).
* **Model-based RL:** Học dựa trên mô hình của môi trường (8:01, 1:14:27).
* **Model-free RL:** Học mà không cần biết trước mô hình môi trường (33:40).
* **Policy Search (Tìm kiếm chính sách):** Tối ưu hóa trực tiếp chính sách (33:48).
* **Planning (Lập kế hoạch):** Tối ưu hóa khi đã biết mô hình (1:14:27).
* **Policy Evaluation (Đánh giá chính sách):** Tính toán hiệu suất của chính sách (1:13:07).
* **Monte Carlo Tree Search (MCTS):** Phương pháp tìm kiếm kết hợp trong *AlphaGo* (3:31).
* **Value Function (Hàm giá trị):** Kỳ vọng tổng phần thưởng nhận được (1:17:33).

### 4. Các khái niệm liên quan khác
* **Partially Observable (Quan sát một phần):** Khi tác nhân không thấy rõ toàn bộ trạng thái (1:05:07).
* **Discount Factor (Hệ số chiết khấu):** Tầm quan trọng của phần thưởng tương lai so với hiện tại (1:16:38).
* **Horizon (Chân trời thời gian):** Số bước thời gian trong một tập (episode) (1:17:11).

# [Lecture 2: Tabular MDP Planning]()

*   **Markov Decision Process (MDP):** Bài toán ra quyết định tuần tự dưới sự không chắc chắn (0:46, 14:08).
*   **Markov Reward Process (MRP):** Quá trình Markov có thêm hàm phần thưởng để đánh giá chính sách (7:20, 16:03).
*   **Discount Factor (γ - Gamma):** Hệ số chiết khấu ảnh hưởng đến tầm quan trọng của phần thưởng tương lai (0:59, 7:47).
*   **Policy (π):** Chiến lược ra quyết định của tác nhân, có thể là tất định hoặc ngẫu nhiên (15:35).
*   **Value Function (V):** Hàm giá trị, đại diện cho kỳ vọng tổng phần thưởng chiết khấu (8:05, 12:22).
*   **Q-function (Q-value):** Hàm giá trị trạng thái-hành động (24:44).
*   **Policy Search:** Tìm kiếm chính sách tối ưu (22:14).
*   **Policy Iteration:** Thuật toán gồm hai bước: đánh giá chính sách và cải thiện chính sách (23:58).
*   **Value Iteration:** Thuật toán tính toán giá trị tối ưu thông qua việc cập nhật lặp lại (47:45).
*   **Bellman Backup Operator:** Toán tử Bellman dùng để cập nhật giá trị (49:12).
*   **Contraction Operator:** Toán tử co, đảm bảo sự hội tụ của thuật toán (57:47).
*   **Monotonic Improvement:** Sự cải thiện đơn điệu, đảm bảo chính sách mới không tệ hơn chính sách cũ (1:16, 31:38).
*   **Stationary Policy:** Chính sách tĩnh, không phụ thuộc vào bước thời gian (21:38, 112:05).
*   **Finite vs. Infinite Horizon:** Bài toán với giới hạn số bước và bài toán kéo dài mãi mãi (21:44, 108:18).
*   **Dynamic Programming:** Phương pháp quy hoạch động được sử dụng để giải MDP (48:50).

# [Lecture 3: Policy Evaluation](https://www.youtube.com/watch?v=gHdsUUGcBC0)

*   **Markoff Decision Processes (MDPs):** Mô hình toán học cơ bản cho việc ra quyết định trong môi trường không chắc chắn.
*   **Tabular MDP:** Trường hợp các trạng thái (states) đủ ít để có thể biểu diễn giá trị của mỗi trạng thái dưới dạng một bảng.
*   **Policy Evaluation (Đánh giá chính sách):** Quá trình tính toán giá trị của một chính sách cố định (hàm giá trị trạng thái $V^\pi$ hoặc hàm giá trị hành động-trạng thái $Q^\pi$).
*   **Model-free RL:** Cách tiếp cận học tập trực tiếp từ kinh nghiệm môi trường mà không cần mô hình động lực học (dynamics model) hoặc mô hình phần thưởng (reward model) cho trước.
*   **Monte Carlo (MC) Policy Evaluation:** Phương pháp đánh giá dựa trên việc mô phỏng các tập dữ liệu đầy đủ (trajectories) và lấy trung bình các khoản hoàn trả (returns) (14:21).
*   **Temporal Difference (TD) Learning (cụ thể là TD(0)):** Phương pháp kết hợp lấy mẫu và **bootstrapping** (sử dụng ước tính hiện tại để cập nhật chính nó), cho phép cập nhật giá trị ngay sau mỗi bước (37:50).
*   **Bootstrapping:** Kỹ thuật sử dụng giá trị ước tính để làm mục tiêu (target) cho việc cập nhật giá trị đó trong tương lai (14:11, 48:29).
*   **Certainty Equivalence:** Cách tiếp cận trong đó ta ước tính mô hình (như xác suất chuyển trạng thái và phần thưởng) từ dữ liệu, sau đó thực hiện quy hoạch động (dynamic programming) trên mô hình đó (1:02:12).
*   **Batch Policy Evaluation:** Phương pháp thực hiện đánh giá chính sách dựa trên một tập dữ liệu cố định có sẵn thay vì tương tác liên tục (1:05:35).
*   **Consistency:** Đặc tính của thuật toán mà khi có dữ liệu vô hạn, ước tính sẽ hội tụ về giá trị thực của chính sách (29:48).
*   **Sample Efficiency:** Hiệu quả trong việc sử dụng dữ liệu, một yếu tố quan trọng khi dữ liệu thu thập tốn kém hoặc hạn chế (47:24).

# [Lecture 4: Q learning and Function Approximation](https://www.youtube.com/watch?v=b_wvosA70f8)

* **Chính sách (Policy):** 
    * *Stochastic Policy* (Chính sách ngẫu nhiên) và *Deterministic Policy* (Chính sách tất định) (1:30 - 6:00).
    * *Epsilon-Greedy* (Chiến lược chọn hành động ngẫu nhiên để khám phá) (11:00 - 13:00).
* **Q-Learning & Đánh giá chính sách:**
    * *Model-free policy iteration* (Lặp chính sách không dựa trên mô hình) (8:55 - 9:30).
    * *State-action value function* ($Q(s, a)$) (4:24 - 5:55).
    * *Generalized Policy Improvement* (Cải thiện chính sách tổng quát) (8:15 - 8:45).
* **Khám phá & Hội tụ:**
    * *Exploration vs. Exploitation* (Thách thức cân bằng giữa khám phá và khai thác) (9:30 - 11:00).
    * *Glee* (Greedy in the Limit of Infinite Exploration) (33:30 - 36:00).
    * *Stochastic Approximation* (Xấp xỉ ngẫu nhiên) và *Robbins-Monro sequence* (44:45 - 45:40).
* **Các thuật toán học:**
    * *Sarsa* (On-policy TD control) (37:00 - 46:40).
    * *Q-Learning* (Off-policy) (47:17 - 50:00).
    * *Monte Carlo methods* (Phương pháp Monte Carlo) (59:00 - 1:00:15).
* **Xấp xỉ hàm (Function Approximation):**
    * Sử dụng *Deep Neural Networks* (Mạng thần kinh sâu) để đại diện cho hàm giá trị (52:00 - 55:00).
    * *Stochastic Gradient Descent (SGD)* (Xuống dốc gradient ngẫu nhiên) (55:30 - 57:00).
* **Deep Q-Network (DQN):**
    * *Experience Replay* (Bộ nhớ đệm trải nghiệm) (107:11 - 108:30).
    * *Fixed Q-Targets* (Cố định mục tiêu Q) (112:00 - 113:30).
    * *The Deadly Triad* (Bộ ba nguy hiểm gây mất ổn định trong học tăng cường: Function approximation, Bootstrapping, Off-policy learning) (103:00 - 105:00).

# [Lecture 5: Policy Search 1]()

*   **Value-based methods (Phương pháp dựa trên giá trị):** Tập trung vào việc học giá trị của các trạng thái hoặc cặp trạng thái-hành động (ví dụ: *Q-learning*, *Deep Q-Network - DQN*).
*   **Policy Search (Tìm kiếm chính sách):** Trực tiếp tối ưu hóa chính sách (policy) $\pi(a|s)$ mà không cần biểu diễn tường minh hàm giá trị (3:53).
*   **Stochastic Policies (Chính sách ngẫu nhiên):** Các chính sách ánh xạ trạng thái sang phân phối xác suất của hành động, quan trọng trong việc khám phá và xử lý các vấn đề không quan sát được đầy đủ (10:48).
*   **Optimization (Tối ưu hóa):** Coi việc tìm chính sách tốt là bài toán tối ưu hóa các tham số $\theta$ của chính sách để tối đa hóa hàm giá trị (17:57).
*   **Policy Gradient (Gradient chính sách):** Phương pháp dựa trên gradient để cập nhật trực tiếp tham số chính sách, bao gồm thuật toán *REINFORCE* (23:44).
*   **Likelihood Ratio (Tỷ lệ khả năng):** Kỹ thuật toán học dùng để tính gradient của kỳ vọng mà không cần biết mô hình động lực học (35:55).
*   **Score Function (Hàm điểm số):** Đạo hàm của log xác suất chính sách theo tham số (48:18).
*   **Actor-Critic Methods (Phương pháp Actor-Critic):** Sự kết hợp giữa các phương pháp dựa trên giá trị và dựa trên chính sách (10:14).
*   **Realizability (Khả năng thực hiện):** Vấn đề về việc liệu bộ xấp xỉ hàm có đủ khả năng biểu diễn hàm mục tiêu hay không (2:47).
*   **Baseline (Đường cơ sở):** Kỹ thuật dùng để giảm phương sai (variance) trong ước lượng gradient mà không gây ra sai lệch (bias) (1:05:27).
*   **Episodic MDPs (Quá trình quyết định Markov từng tập):** Cấu trúc bài toán trong đó tác nhân thực hiện các hành động theo từng tập (episode) có điểm kết thúc (17:35).
*   **Cross-Entropy Method (CEM):** Một phương pháp tối ưu hóa không dựa trên gradient (20:57).
*   **Partial Observability (Tính quan sát một phần):** Các tình huống mà tác nhân không nhìn thấy toàn bộ trạng thái hệ thống (14:02).


# [Lecture 6: Policy Search 2]()

*   **Policy Gradient Methods (Phương pháp gradient chính sách):** Các phương pháp tìm kiếm trực tiếp trong không gian tham số chính sách (0:09, 3:04).
*   **Baseline (Đường cơ sở):** Kỹ thuật giảm phương sai của ước lượng gradient mà không gây ra sai lệch (bias) (0:30, 5:05).
*   **Likelihood Ratio / Score Function (Tỷ lệ khả năng / Hàm điểm):** Phương pháp ước lượng đạo hàm của giá trị kỳ vọng (3:26).
*   **Temporal Structure (Cấu trúc thời gian):** Tận dụng tính chất phần thưởng tại một thời điểm không phụ thuộc vào các hành động tương lai (4:27).
*   **Actor-Critic Methods (Phương pháp Actor-Critic):** Kiến trúc kết hợp Actor (chính sách) và Critic (hàm giá trị) để giảm phương sai (16:30, 17:05).
*   **On-policy vs Off-policy Estimation:** Sự khác biệt giữa việc học từ dữ liệu do chính sách hiện tại thu thập và việc sử dụng dữ liệu cũ (35:39, 36:12).
*   **Performance Difference Lemma (Bổ đề sai biệt hiệu năng):** Công thức toán học dùng để so sánh hiệu năng của hai chính sách khác nhau (44:06).
*   **Discounted Future State Distribution (Phân phối trạng thái tương lai có chiết khấu):** Trọng số được sử dụng để đánh giá các trạng thái dựa trên nhân tố chiết khấu $\gamma$ (47:16, 50:18).
*   **Important Sampling (Lấy mẫu quan trọng):** Kỹ thuật re-weight (tái trọng số) để ước lượng giá trị của một chính sách mới từ dữ liệu của chính sách cũ (53:46, 54:56).
*   **KL Divergence (Phân kỳ Kullback-Leibler):** Thước đo sự khác biệt giữa hai phân phối xác suất (hành động của hai chính sách), dùng để giới hạn vùng tin cậy (57:34, 59:21).
*   **Trust Region (Vùng tin cậy):** Ý tưởng giới hạn bước cập nhật chính sách để đảm bảo tính ổn định (1:02:30).
*   **Proximal Policy Optimization (PPO):** Thuật toán tối ưu hóa chính sách phổ biến, sử dụng ràng buộc KL hoặc hàm mục tiêu bị cắt (clipped objective) (1:02:45, 1:06:37).
*   **Clipped Objective (Hàm mục tiêu bị cắt):** Cơ chế trong PPO giúp ngăn chặn các bước cập nhật quá lớn (1:06:37, 1:07:05).

# [Lecture 7: Policy Search 3]()

**1. Các phương pháp Gradient Chính sách (Policy Gradient Methods):**
*   **Reinforce (0:46):** Thuật toán cơ bản dựa trên lấy mẫu dữ liệu để tối ưu hóa không gian chính sách.
*   **Baseline (0:13):** Sử dụng hàm cơ sở để giảm phương sai (variance) trong ước tính gradient.
*   **Policy Search (0:07):** Các phương pháp tìm kiếm chính sách tối ưu.
*   **Deterministic vs. Stochastic Policy (3:31 - 3:58):** Vấn đề khi khởi tạo chính sách tất định (không khám phá được toàn bộ không gian hành động).

**2. Cải tiến và tối ưu hóa:**
*   **Monotonic Improvement (4:12):** Đảm bảo cải thiện đơn điệu qua các bước cập nhật chính sách.
*   **PPO (Proximal Policy Optimization) (4:19):** Thuật toán phổ biến nhằm cân bằng giữa hiệu quả mẫu và sự ổn định.
*   **KL Divergence (6:26):** Khoảng cách Kullback-Leibler dùng để ràng buộc sự thay đổi giữa chính sách cũ và mới.
*   **Clipped Objective (6:43):** Phương pháp cắt mục tiêu trong PPO để tránh các bước cập nhật quá lớn.

**3. Ước tính lợi thế (Advantage Estimation):**
*   **Advantage Function (6:55):** Hàm lợi thế đo lường giá trị của hành động so với giá trị trung bình của trạng thái.
*   **Generalized Advantage Estimation (GAE) (4:52 - 26:49):** Kỹ thuật kết hợp có trọng số các ước lượng lợi thế để cân bằng giữa *bias* (độ chệch) và *variance* (phương sai).
*   **Telescoping Sum (11:50):** Kỹ thuật cộng dồn triệt tiêu các thành phần trung gian để đơn giản hóa biểu thức.
*   **Temporal Difference (TD) Learning (7:35):** Phương pháp học dựa trên sự khác biệt thời gian.
*   **Monte Carlo Estimate (7:57):** Phương pháp ước tính giá trị dựa trên các tập mẫu toàn phần.

**4. Học bắt chước (Imitation Learning):**
*   **Behavior Cloning (48:00 - 54:10):** Phương pháp học bắt chước bằng cách coi bài toán RL như học có giám sát (supervised learning).
*   **Compounding Errors (55:01):** Lỗi tích lũy xảy ra khi các dự đoán sai lầm trong quá khứ ảnh hưởng đến các trạng thái tương lai.
*   **DAgger (Dataset Aggregation) (54:40 - 1:03:00):** Thuật toán học bắt chước lặp lại bằng cách thu thập thêm dữ liệu từ các trạng thái mà chính sách chưa từng thấy.
*   **Inverse Reinforcement Learning (IRL) (1:03:50):** Bài toán suy diễn hàm phần thưởng (reward function) từ các biểu diễn của chuyên gia.
*   **Maximum Entropy Inverse Reinforcement Learning (1:18:15):** Phương pháp tối đa hóa entropy để giải quyết vấn đề nhận dạng (identifiability) trong IRL.
*   **Feature Matching (1:17:20):** Kỹ thuật khớp các đặc trưng giữa chính sách của chuyên gia và chính sách đang học.
