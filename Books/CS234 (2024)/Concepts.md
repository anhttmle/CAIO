# [Lecture 1](https://www.youtube.com/watch?v=WsvFL-LjA6U)

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
