## Basic

| Nhóm chức năng           | Tính năng đề xuất                   | Mô tả                                                                           |
| ------------------------ | ----------------------------------- | ------------------------------------------------------------------------------- |
| Quản lý tài khoản        | Quản lý user nội bộ                 | Tenant Admin tạo/xoá tài khoản Operator, phân quyền lễ tân                      |
| Cấu hình Clinic          | Thông tin phòng khám                | Cập nhật giờ làm việc, danh sách dịch vụ, bảng giá, chi nhánh                   |
| Cấu hình Channel         | Kết nối kênh liên lạc               | Kết nối số điện thoại (SIP), Zalo OA, widget WebRTC cho website riêng           |
| Cấu hình Domain features | Bật/tắt & tuỳ chỉnh kịch bản        | Cấu hình kịch bản Reminder, Recall, FAQ triage, Upsell theo nhu cầu clinic      |
| Cấu hình Domain features | Quản lý kịch bản hội thoại (script) | Chỉnh nội dung câu thoại mẫu, ngưỡng chuyển tiếp sang người (Fallback to Human) |
| Tích hợp                 | Kết nối hệ thống vệ tinh            | Liên kết PMS/CRM, Google Calendar để đồng bộ lịch hẹn                           |
| Vận hành hàng ngày       | Quản lý lịch hẹn (Appointment)      | Xem/sửa/huỷ lịch hẹn được AI tạo ra, xử lý xung đột lịch                        |
| Vận hành hàng ngày       | Hàng đợi Fallback to Human          | Nhận và xử lý các cuộc gọi/chat được AI chuyển tiếp cho lễ tân                  |
| Báo cáo & phân tích      | Dashboard hiệu quả AI               | Số cuộc gọi xử lý tự động, tỷ lệ chuyển đổi upsell, tỷ lệ no-show giảm          |
| Báo cáo & phân tích      | Lịch sử tương tác User              | Xem lại transcript/ghi âm cuộc gọi, lịch sử chat theo từng khách hàng           |
| AI Coach                 | Chỉ định hỗ trợ Operator             | Chỉ định AI sẽ chạy ở Shadow Mode và gợi ý nội dung trả lời cho lễ tân nào      |
| Thông báo                | Cấu hình cảnh báo                   | Thiết lập email/SMS cảnh báo khi có sự cố tích hợp (VD: mất kết nối PMS)        |

## Advance

| Cơ chế                             | Mô tả                                                                                                                                                 | Áp dụng cho                                  |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| Visual Flow Builder                | Giao diện kéo-thả trên Tenant Portal để Clinic tự thiết kế luồng hội thoại (câu hỏi, nhánh rẽ, điều kiện) mà không cần code rasa+1                    | Reminder, Recall, Upsell, Inbound flow       |
| Versioned workflow definitions     | Mỗi khi Tenant Admin sửa flow, hệ thống lưu một version mới; các cuộc gọi đang chạy dở vẫn dùng version cũ, chỉ cuộc gọi mới áp dụng version mới nhất | Toàn bộ Workflow Engine                      |
| Script/prompt template theo tenant | Cho phép chỉnh nội dung câu thoại mẫu (TTS script), tone giọng, ngưỡng chuyển Fallback to Human                                                       | Conversation Engine                          |
| Extension points có kiểm soát      | Với các case không fit vào cấu hình chuẩn (VD: tích hợp API riêng của Clinic), cung cấp "custom action/webhook" thay vì sửa core code flowwright      | Domain Backend, Integration layer            |
| Hybrid tenancy (shared + custom)   | Cung cấp sẵn flow mẫu dùng chung (shared, tenant_id rỗng); Tenant có thể "fork" thành bản riêng để chỉnh sửa mà không ảnh hưởng tenant khác dev       | Tất cả domain features                       |
| Tag/feature flag theo gói dịch vụ  | Gắn tag cho từng flow để giới hạn quyền truy cập theo gói (Basic/Pro) mà Tenant đã đăng ký workflowengine                                             | Admin Portal cấu hình, Tenant Portal sử dụng |
