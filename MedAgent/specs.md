# Prompt
Hãy giúp tôi phân tích bài toán được phía khách hàng đặt ra sau:

## [Tổng quan] 
phát triển tác nhân AI (AI Agent) chuyên biệt để hỗ trợ quản lý bệnh viện và tối ưu hóa quy trình đấu thầu y tế. Công cụ này được kỳ vọng sẽ thay thế vai trò thư ký, giúp giám đốc bệnh viện tổng hợp dữ liệu tài chính, nhân sự và cảnh báo các định mức tiêu hao từ hệ thống HIS/ERP. Đặc biệt, giải pháp tập trung vào khả năng khai thác dữ liệu (data mining) để so sánh giá cả, chấm thầu và tư vấn lập kế hoạch đấu thầu dựa trên thông tin từ cổng đấu thầu quốc gia. Bằng cách hoạt động như một module độc lập tích hợp qua API, AI Agent giúp lãnh đạo giảm thiểu rủi ro pháp lý và nâng cao năng lực quản trị mà không cần thay đổi hệ thống phần mềm sẵn có. Nhóm phát triển dự định xây dựng bản demo trên Telegram để minh họa khả năng truy vấn thông tin thầu một cách nhanh chóng và hiệu quả.

## [Định hướng] 
Tách biệt hai luồng AI Agent Chiến lược cốt lõi là phát triển và tách bạch hai công cụ rõ ràng để dễ tiếp cận thị trường: 
- AI Agent Quản trị bệnh viện hàng ngày 
- AI Agent hỗ trợ Đấu thầu.

### Agent hỗ trợ Đấu thầu (Tendering Agent)
**Pain point**: 
- Giải quyết "nỗi đau" cực lớn của bệnh viện: Hiện tại, chuyên viên thầu và hội đồng thầu phải đọc, lọc và so sánh thủ công hàng trăm hồ sơ dự thầu (cả bản PDF lẫn bản giấy) rất tốn kém thời gian và chi phí.

**Tính năng cốt lõi**: 
- Data mining: Lọc dữ liệu thầu cũ từ nội bộ bệnh viện và hệ thống Cổng thông tin
đấu thầu quốc gia (EGP) để phục vụ việc lập kế hoạch nguồn vốn.
- Chấm thầu tự động: AI có khả năng đọc bản scan PDF, bóc tách dữ liệu để tự
động tạo bảng so sánh các chỉ tiêu/tiêu chí của hồ sơ dự thầu so với hồ sơ mời
thầu.
- Quản trị rủi ro pháp lý: Giúp kiểm tra, so sánh giá của các loại thuốc, máy móc
so với thị trường và các gói thầu khác để đảm bảo tính hợp lệ (ví dụ: giá thuốc
không được chênh lệch quá 5% so với gói thấp nhất). Điều này giúp Giám đốc
viện tự tin ký duyệt mà không sợ rủi ro.

**Chiến lược kinh doanh**: 
- Có thể phát triển thành một công cụ (SaaS) độc lập hoàn toàn, không phụ thuộc vào hệ thống khác của viện và bán trực tiếp rất nhanh.

### AI Agent Quản trị Bệnh viện (Dành cho Ban Giám đốc)
**Định vị sản phẩm**: 
- Đóng vai trò như một "Thư ký tổng hợp" phục vụ trực tiếp người ra quyết định chi tiêu (Giám đốc bệnh viện). Đây là điểm mấu chốt vì các Giám đốc viện thường đi lên từ chuyên môn y (bác sĩ, dược sĩ) nên gặp khó khăn về thời gian và kỹ năng quản lý, đọc báo cáo tài chính.

**Tính năng cốt lõi**:
- Báo cáo tự động:
  - Lấy dữ liệu vào ban đêm (ví dụ 12h đêm) để chuẩn bị sẵn sàng các báo cáo về doanh thu, vật tư, lượng ca bệnh... phục vụ cho cuộc họp giao ban lúc 8h sáng hàng ngày.
  - Cảnh báo thông minh (Alerts): Theo dõi sát sao và báo cáo ngay nếu phát hiện quỹ lương bị vượt, chi phí tăng bất thường, hoặc mức tiêu hao vật tư trên mỗi giường bệnh vượt định mức cho phép.

**Chiến lược kỹ thuật và kinh doanh**:
- Tuyệt đối không tham vọng thay thế các phần mềm hiện có (như phần mềm khám chữa bệnh HIS, kế toán, hay nhân sự HR) vì bệnh viện rất ngại thay đổi.
- Thay vào đó, AI Agent chỉ làm nhiệm vụ kết nối API (Hub) lấy dữ liệu đầu vào từ các phần mềm này để xử lý và trả ra phân tích đầu ra. Việc đấu nối API sẽ được tính phí hoặc thu phí dùng theo mô hình Token/Credit

## Kế hoạch triển khai (Next steps) ngay sau cuộc họp
- Xây dựng Demo nhanh: Khởi tạo một Bot trên Telegram nhằm demo tính năng data mining cơ bản cho thầu (ví dụ: tra cứu gói thầu theo loại thuốc, theo hoạt chất năm ngoái).
- Phối hợp nội dung: Xin anh Hải các đề mục/yêu cầu cụ thể về chỉ tiêu quản trị từ góc nhìn lãnh đạo bệnh viện để đội ngũ kỹ thuật có cơ sở xây dựng kịch bản demo chuẩn xác.
- Giải quyết bài toán đầu vào: Cần tiếp tục nghiên cứu, liên hệ (có thể qua Cục quản lý thiết bị y tế) để tìm cách lấy và tổng hợp nguồn dữ liệu thầu hiệu quả nhằm phục vụ cho tính năng so sánh giá.

## Notes
- Các skill: hỗ trợ chấm thầu theo tiêu chí
- Dự nguồn vốn từ những năm trước để duyệt nguồn vốn năm nay => lên kế hoạch đấu thầu như thế nào
- So sánh cổng thông tin đấu thầu quốc gia egp và dữ liệu của viện => tổng hợp và so sánh chéo giữa các nguồn để đưa ra thông tin trực quan hơn. VD các gói thầu liên quan đến thuốc (theo hoạt chất), máy móc => hỏi đáp chatbot
- So sánh hồ sơ thầu và hồ sơ dự thầu, so sánh các bên đăng ký hồ sơ và đưa ra gợi ý dựa trên bảng chỉ tiêu chấm thầu (trích dẫn đầy đủ căn cứ trang bao nhiêu, điểm nào trên hồ sơ thầu)
- So sánh lịch sử đấu thầu, lịch sử giá các gói thầu giữa các viện - giữa giá của các đợt trong viện (giá thuốc giữa các đợt thầu không được quá 5% giá đợt thầu trước)
- Agent => quản lý công việc hàng ngày theo cấp bậc, số liệu vận hành hằng ngày, quản lý báo cáo tổng hợp, cảnh báo hiệu quả công việc - rủi ro => luồng xử lý như thế nào
- Thầu là 1 phần trong đó, painpoint là chưa có. Các bên bán hệ thống HIS cho công ty => mình
bán credit cho các công ty, đóng vài trò là 1 module trong cái ERP của các công ty đã có dịch
vụ sẵn như 1 gói nâng cấp.
- HIS là phần mềm nhập liệu tạo hồ sơ => đầu vào dữ liệu
- Agent của mình lấy các data đó để tổng hợp và phân tích, đưa ra báo cáo theo các yêu cầu của ban quản lý => đóng vai trò như 1 trợ lý toàn năng
- Agent tài chính, chuyên môn, nhân sự, thầu, quản lý kho …etc => tính giá trên 1 API, bán credit
