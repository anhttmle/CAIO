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
