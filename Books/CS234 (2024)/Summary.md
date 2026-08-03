# Lecture 1:
Các chủ đề chính được nhắc đến trong bài giảng:

- Tổng quan về Reinforcement Learning (RL): Khái niệm cốt lõi về việc tác nhân tự động (automated agent) học hỏi thông qua trải nghiệm để đưa ra quyết định (0:20).
- Các ứng dụng thực tế của RL:
  - Trò chơi Go (Cờ vây) và sự đột phá của DeepMind (2:55).
  - Điều khiển phản ứng Fusion (nhiệt hạch) (4:00).
  - Kiểm soát dịch bệnh COVID-19 (triển khai tại Hy Lạp) (4:48).
  - ChatGPT và quá trình huấn luyện sử dụng RLHF (Reinforcement Learning from Human Feedback) (5:34).
- Sự khác biệt giữa các phương pháp học:
  - Phân biệt giữa Imitation Learning (Học bắt chước/Behavior Cloning) và Reinforcement Learning (23:43).
  - Khi nào nên dùng RL thay vì IL (học bắt chước ) (30:13).
- Logic và cấu trúc khóa học:
  - Các thành phần của Markov Decision Process (MDP) bao gồm:
    - Không gian trạng thái (State space)
    - Không gian hành động (Action space)
    - Mô hình động học (Dynamics model)
    - Phần thưởng (Reward) (41:07).
  - Giải thích về Markov Chains và Markov Reward Processes (115:22).

Logistics khóa học: Phương pháp giảng dạy, bài tập về nhà, dự án cuối khóa và tầm quan trọng của việc học chủ động (active learning) thông qua bài tập thay vì chỉ xem video (36:12).

## Khi nào nên dùng RL thay vì IL
Giáo sư Emma Brunskill đã giải thích rất rõ về lý do tại sao chúng ta cần đến Reinforcement Learning (RL) thay vì chỉ dựa vào Imitation Learning (Học bắt chước). Dưới đây là các điểm chính:
  - Vượt qua giới hạn của con người: Nếu bạn chỉ học bằng cách bắt chước (Imitation Learning), mô hình của bạn tối đa chỉ có thể đạt được hiệu suất ngang bằng với dữ liệu mà nó học được (thường là dữ liệu do con người cung cấp). Để vượt qua trình độ chuyên gia, hệ thống cần tự khám phá các chiến lược mới mà con người chưa từng nghĩ tới, điều mà RL có thể làm được (30:25).
  - Thiếu dữ liệu về hành động tối ưu: Trong nhiều lĩnh vực như y tế hoặc giáo dục, chúng ta không có đủ các "ví dụ mẫu" (demonstrations) hoàn hảo về cách xử lý mọi tình huống. RL cho phép tác nhân học từ chính kinh nghiệm của nó thông qua việc thử và sai (trial and error), thay vì cần một kho dữ liệu khổng lồ từ chuyên gia (30:20).
  - Khám phá chiến lược mới: Một ví dụ điển hình được nhắc đến là AlphaGo (30:10). AI này đã tìm ra những nước đi sáng tạo trong cờ vây mà con người chưa bao giờ thực hiện trước đây. Nếu chỉ dùng học bắt chước, AlphaGo sẽ không bao giờ có thể "vượt mặt" những người chơi giỏi nhất thế giới.

Tóm lại:
  - Dùng Imitation Learning khi: Bạn đã có sẵn nguồn dữ liệu chất lượng cao về cách thực hiện tác vụ và muốn mô hình sao chép hành vi đó một cách nhanh chóng.
  - Dùng RL khi: Bạn muốn hệ thống tự cải thiện để đạt kết quả tốt nhất có thể, hoặc khi việc thu thập dữ liệu chuyên gia là quá tốn kém, không khả thi, hoặc khi bạn muốn AI tìm ra những giải pháp đột phá nằm ngoài hiểu biết hiện tại của con người.

# Lecture 2:
