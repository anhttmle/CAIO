## DQN dạng Value-Based là gì?

**DQN (Deep Q-Network) dạng value-based** là một thuật toán học tăng cường (reinforcement learning) trong đó agent học một **hàm giá trị hành động** \(Q(s, a)\) để ước lượng phần thưởng tương lai kỳ vọng khi thực hiện hành động \(a\) ở trạng thái \(s\), sau đó chọn hành động có giá trị Q cao nhất. [aioconquer.aivietnam.edu](https://aioconquer.aivietnam.edu.vn/posts/reinforcement-learning-overview)

## Bối cảnh: Value-Based Methods trong RL

Trong học tăng cường, có hai cách tiếp cận chính:

- **Value-Based Methods** (phương pháp dựa trên giá trị): học hàm giá trị, rồi suy ra chính sách từ hàm này. [milvus](https://milvus.io/ai-quick-reference/what-are-valuebased-methods-in-reinforcement-learning)
- **Policy-Based Methods** (phương pháp dựa trên chính sách): học trực tiếp chính sách \(\pi(a|s)\) mà không cần hàm giá trị trung gian.  [aioconquer.aivietnam.edu](https://aioconquer.aivietnam.edu.vn/posts/reinforcement-learning-overview)

DQN thuộc nhóm **value-based**, cùng với Q-Learning cổ điển. [phamduytung](https://www.phamduytung.com/blog/2024-10-27-mario-reinfomation-learning-double-dqn/)

## Ý tưởng cốt lõi của DQN value-based

### 1. Hàm Q-value

Ký hiệu \(Q^\pi(s, a)\) là tổng phần thưởng chiết khấu kỳ vọng khi agent ở trạng thái \(s\), thực hiện hành động \(a\), rồi tuân theo chính sách \(\pi\) sau đó. [aioconquer.aivietnam.edu](https://aioconquer.aivietnam.edu.vn/posts/reinforcement-learning-overview)

Mục tiêu: học hàm \(Q^*(s, a)\) tối ưu, sao cho:

\[
Q^*(s, a) = \mathbb{E}\left[ r + \gamma \max_{a'} Q^*(s', a') \mid s, a \right]
\]

đây là phương trình Bellman tối ưu cho Q-function. [milvus](https://milvus.io/ai-quick-reference/what-are-valuebased-methods-in-reinforcement-learning)

### 2. Từ Q-table sang Deep Q-Network

- **Q-Learning cổ điển**: dùng bảng Q-table lưu \(Q(s, a)\) cho từng cặp \((s, a)\). [aioconquer.aivietnam.edu](https://aioconquer.aivietnam.edu.vn/posts/reinforcement-learning-overview)
- **Vấn đề**: khi không gian trạng thái lớn (ví dụ: ảnh pixel trong game), Q-table trở nên không khả thi. [cloudgo](https://cloudgo.vn/reinforcement-learning-la-gi)
- **Giải pháp DQN**: thay vì bảng, dùng một **mạng nơ-ron** với tham số \(\theta\) để xấp xỉ hàm Q:

\[
Q(s, a; \theta) \approx Q^*(s, a)
\]

Mạng nhận đầu vào là trạng thái \(s\) (có thể là ảnh) và xuất ra giá trị Q cho tất cả hành động \(a\). [cloudgo](https://cloudgo.vn/reinforcement-learning-la-gi)

### 3. Huấn luyện DQN: cực tiểu hóa loss

Để huấn luyện mạng, ta cực tiểu hóa sai số giữa **dự đoán** và **mục tiêu** (target). Hàm loss (Mean Squared Error) trong DQN:

\[
L(\theta) = \mathbb{E}_{(s,a,r,s') \sim D} \left[ \left( \underbrace{r + \gamma \max_{a'} Q(s', a'; \theta^-)}_{\text{Target } y_i} - \underbrace{Q(s, a; \theta)}_{\text{Prediction}} \right)^2 \right]
\]

trong đó:

- \(\theta\): tham số mạng chính (main network).
- \(\theta^-\): tham số mạng đích (target network), được giữ cố định trong một khoảng thời gian để ổn định huấn luyện. [studocu](https://www.studocu.vn/vn/document/dai-hoc-hue/machine-learning/bai-tap-trac-nghiem-hoc-tang-cuong-rl-1-4444-30-cau-hoi-dap-an-chi-tiet/163609744)
- \(D\): buffer kinh nghiệm (experience replay), lưu các chuyển tiếp \((s, a, r, s')\) để phá vỡ tương quan giữa các mẫu huấn luyện. [milvus](https://milvus.io/ai-quick-reference/what-are-valuebased-methods-in-reinforcement-learning)

## Tại sao gọi là "value-based"?

DQN được gọi là **value-based** vì:

- Agent **không học trực tiếp chính sách** \(\pi(a|s)\).  [aioconquer.aivietnam.edu](https://aioconquer.aivietnam.edu.vn/posts/reinforcement-learning-overview)
- Thay vào đó, agent học **hàm giá trị** \(Q(s, a)\), tức là "định giá tương lai" của mỗi hành động trong mỗi trạng thái. [aioconquer.aivietnam.edu](https://aioconquer.aivietnam.edu.vn/posts/reinforcement-learning-overview)
- Chính sách được suy ra **gián tiếp** từ Q-value, thường là:

\[
\pi(s) = \arg\max_a Q(s, a; \theta)
\]

hoặc dùng \(\epsilon\)-greedy để cân bằng khám phá/khai thác. [apxml](https://apxml.com/courses/intermediate-reinforcement-learning/chapter-4-policy-gradient-methods/value-based-methods-limitations)

Nói cách khác, DQN như một "nhà phân tích": nhìn vào trạng thái, tính toán lợi nhuận kỳ vọng (Q-value) của từng hành động, rồi mới quyết định. [aioconquer.aivietnam.edu](https://aioconquer.aivietnam.edu.vn/posts/reinforcement-learning-overview)

## So sánh nhanh: Value-Based (DQN) vs Policy-Based

| Đặc điểm | Value-Based (DQN) | Policy-Based (ví dụ PPO) |
|----------|-------------------|--------------------------|
| Học gì? | Hàm giá trị \(Q(s, a)\) | Chính sách \(\pi(a|s)\) trực tiếp |
| Cách ra quyết định | Chọn \(\arg\max_a Q(s, a)\) | Lấy mẫu từ \(\pi(a|s)\) |
| Không gian hành động | Tốt với hành động rời rạc, số lượng vừa phải | Tốt với hành động liên tục hoặc rất nhiều hành động |
| Ổn định | Có thể bị overestimation, cần DDQN, target network | Thường ổn định hơn trong một số môi trường phức tạp |
| Ví dụ | Q-Learning, DQN, DDQN, Dueling DQN | REINFORCE, PPO, A3C (phần policy) |

 [fmit](https://fmit.vn/tu-dien-quan-ly/dueling-dqn-la-gi)

## Một số biến thể value-based của DQN

- **Double DQN (DDQN)**: tách việc **chọn hành động** và **đánh giá giá trị** để giảm thiên lệch ước lượng quá mức (overestimation bias). [phamduytung](https://www.phamduytung.com/blog/2024-10-27-mario-reinfomation-learning-double-dqn/)
- **Dueling DQN**: tách riêng việc học **state-value** \(V(s)\) và **advantage** \(A(s, a)\), rồi kết hợp lại thành \(Q(s, a)\). [fmit](https://fmit.vn/tu-dien-quan-ly/dueling-dqn-la-gi)
- **DQN + Prioritized Replay, Rainbow, v.v.**: các cải tiến về cách lấy mẫu và kiến trúc mạng để tăng hiệu suất. [milvus](https://milvus.io/ai-quick-reference/what-are-valuebased-methods-in-reinforcement-learning)

## Tóm lại

- DQN dạng **value-based** học hàm \(Q(s, a)\) bằng mạng nơ-ron, thay vì học chính sách trực tiếp. [milvus](https://milvus.io/ai-quick-reference/what-are-valuebased-methods-in-reinforcement-learning)
- Policy được suy ra từ Q-value qua \(\arg\max_a Q(s, a)\). [apxml](https://apxml.com/courses/intermediate-reinforcement-learning/chapter-4-policy-gradient-methods/value-based-methods-limitations)
- Kỹ thuật then chốt: **experience replay** và **target network** để ổn định huấn luyện khi dùng deep learning. [studocu](https://www.studocu.vn/vn/document/dai-hoc-hue/machine-learning/bai-tap-trac-nghiem-hoc-tang-cuong-rl-1-4444-30-cau-hoi-dap-an-chi-tiet/163609744)
