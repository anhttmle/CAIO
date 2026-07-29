| Nhóm chức năng    | Tính năng đề xuất                   | Mô tả                                                                                             |
| ----------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------- |
| Quản lý Tenant    | Tạo/kích hoạt/tạm ngưng Tenant      | Đăng ký Clinic mới, cấu hình gói dịch vụ, khoá tài khoản khi vi phạm/nợ phí                       |
| Quản lý Tenant    | Xem chi tiết & "Impersonate" tenant | Đăng nhập giả lập vào tài khoản Client để hỗ trợ debug mà không cần mật khẩu reddit               |
| Quản lý tài khoản | Quản lý user/role toàn hệ thống     | Reset mật khẩu, phân quyền, khoá tài khoản Tenant Admin/Operator                                  |
| Cấu hình hệ thống | Quản lý Channel & Gateway           | Cấu hình SIP Trunk/PBX, Zalo OA, WebRTC cho từng tenant hoặc toàn hệ thống                        |
| Cấu hình hệ thống | Quản lý Domain features             | Bật/tắt tính năng (Appointment, Reminder, Recall, Upsell...) theo từng gói/tenant                 |
| Cấu hình hệ thống | Quản lý tích hợp (Integration)      | Kết nối/kiểm tra trạng thái PMS, CRM, Calendar, SMS/Email gateway                                 |
| Giám sát vận hành | Dashboard giám sát toàn hệ thống    | Theo dõi uptime, số cuộc gọi, lỗi tích hợp, hiệu năng AI Core Engine theo thời gian thực frontegg |
| Giám sát vận hành | Log & audit trail                   | Ghi log truy cập, thay đổi cấu hình, hành động impersonate để phục vụ audit/bảo mật               |
| Vận hành nội bộ   | Quản lý billing & sử dụng           | Theo dõi usage (số phút gọi, số request AI) để tính phí theo tenant                               |
| Vận hành nội bộ   | Quản lý knowledge base chung        | Cập nhật dữ liệu huấn luyện/template dùng chung cho AI Core Engine (không riêng tenant)           |
| Bảo mật           | Quản lý chính sách bảo mật          | Cấu hình password policy, 2FA, RBAC theo từng tenant                                     |
