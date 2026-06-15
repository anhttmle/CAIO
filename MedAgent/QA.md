# Đấu thầu
### Problems:
> đọc, lọc và so sánh thủ công hàng trăm hồ sơ dự thầu (cả bản PDF lẫn bản giấy) rất tốn kém thời gian và chi phí
Document Extraction: (_Trade off giữa chuẩn hoá đầu vào vs fiction khi triển khai_)
- PDF scan
- Paper scan

> Data mining
- các bệnh viện có dùng chung interface ko? Nếu ko, việc phát triển các adapter có thể tốn cost
- cần focus giải các bài toán data ready?

> Chấm thầu tự động: AI có khả năng đọc bản scan PDF, bóc tách dữ liệu để tự động tạo bảng so sánh các chỉ tiêu/tiêu chí của hồ sơ dự thầu so với hồ sơ mời thầu.
- Document Intelligent problems -> multi stage & can be not accurate

> Agent của mình lấy các data đó để tổng hợp và phân tích, đưa ra báo cáo theo các yêu cầu của ban quản lý => đóng vai trò như 1 trợ lý toàn năng
- Workflow có thể cần thiết kế kỹ, vì agent dễ hallucinate với những công việc đặc thù như bệnh viện, chính phủ
