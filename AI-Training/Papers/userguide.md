# NuiTruc Voice AI Platform – Hướng dẫn sử dụng

**Phiên bản tài liệu:** 1.0  
**Phiên bản sản phẩm:** Môi trường phát triển (`dev.app.nuitruc.ai`); cổng không hiển thị số phiên bản  
**Cập nhật lần cuối:** 23/11/2026  
**Đối tượng:** Quản trị viên cơ sở (Tenant Admin) / Nhân viên cơ sở (Tenant User)  
**Chủ sở hữu tài liệu:** [Nhóm Sản phẩm / Chăm sóc khách hàng]  
**Phân loại:** [Công khai / Bảo mật dành cho khách hàng]

---

# 1. Thông tin tài liệu

## 1.1 Mục đích

Tài liệu này hướng dẫn sử dụng cổng doanh nghiệp của **NuiTruc Voice AI Platform** (tên trên màn hình: **Voice AI Platform – Cổng Doanh Nghiệp**).

Nội dung gồm: đăng ký, đăng nhập, xem lại cuộc gọi và hội thoại do trợ lý AI xử lý, quản lý lịch hẹn và khách hàng, cấu hình trợ lý cùng các kênh liên lạc, và xử lý sự cố thường gặp.

## 1.2 Đối tượng sử dụng

| Đối tượng | Nhãn trên cổng | Mô tả |
|---|---|---|
| Quản trị viên cơ sở (Tenant Admin) | **Quản trị viên** | Chủ không gian làm việc của cơ sở. Dùng được mọi menu, gồm **Cài đặt hệ thống** và **Cài đặt nâng cao**. |
| Nhân viên cơ sở (Tenant User) | **Nhân viên** (Operator) | Tài khoản do quản trị viên tạo. Làm việc với các menu vận hành: tổng quan, lịch sử cuộc gọi, lưu lượng, lịch hẹn. |

Cổng có hai vai trò. Vai trò chỉ xem riêng biệt chưa có trong hệ thống.

## 1.3 Phạm vi

Tài liệu bao gồm:

- Đăng ký, đăng nhập và điều hướng
- Tổng quan, lịch sử cuộc gọi, lịch sử hội thoại, lưu lượng AI và lịch hẹn
- Bảng giá, gói cước và mã ưu đãi
- Mini CRM: thông tin cơ sở, tổng đài và kênh liên lạc, công cụ, trợ lý AI, tài liệu tri thức, khách hàng
- Cấu hình nâng cao: mô hình AI, chiến dịch gọi đi, nhân viên, thông tin xác thực
- Xử lý sự cố thường gặp

Tài liệu không bao gồm:

- Quản trị cấp nền tảng của NuiTruc (cổng Super Admin)
- Hạ tầng, triển khai và bảo trì hệ thống
- API nội bộ và chi tiết kỹ thuật dành cho lập trình viên
- Các bước thực hiện trong trang quản trị của bên thứ ba (OMICALL, Meta for Developers, Zalo Developers)

## 1.4 Quy ước

- Nhãn trên màn hình được ghi đúng nguyên văn và **in đậm**.
- Ví dụ lấy từ không gian làm việc của một phòng khám nha khoa. [Mục 2.3](#23-khái-niệm-cơ-sở-tenant) giải thích cách nhãn thay đổi theo lĩnh vực.
- `[Chèn ảnh chụp màn hình: …]` là vị trí dành cho ảnh minh họa.

## 1.5 Lịch sử chỉnh sửa

| Phiên bản | Ngày | Tác giả | Mô tả |
|---|---|---|---|
| 1.0 | 23/11/2026 | [Tác giả] | Phát hành lần đầu, dựa trên môi trường phát triển |

---

# 2. Giới thiệu

## 2.1 Về hệ thống

NuiTruc Voice AI Platform là dịch vụ voicebot và chatbot tiếp nhận cuộc gọi, tin nhắn của khách hàng 24/7. Trợ lý AI trả lời dựa trên tài liệu riêng của cơ sở, thu thập thông tin khách hàng và đặt lịch hẹn.

Cổng doanh nghiệp là nơi cơ sở xem lại những gì trợ lý đã làm và điều chỉnh cách trợ lý hoạt động.

Hệ thống vận hành theo kiến trúc đa cơ sở (multi-tenant). Mỗi cơ sở có không gian làm việc riêng với dữ liệu, cấu hình và người dùng tách biệt.

## 2.2 Tính năng chính

| Tính năng | Mô tả |
|---|---|
| Đăng ký | Tự đăng ký gói miễn phí, trợ lý được chuẩn bị sẵn theo lĩnh vực đã chọn |
| Tổng quan | Trạng thái trợ lý, số cuộc gọi 7 ngày, tỷ lệ thành công, lịch hẹn mới |
| Lịch sử cuộc gọi | Mọi cuộc gọi thoại kèm transcript và bản ghi âm |
| Lịch sử hội thoại | Hội thoại chatbot trên Web, Zalo và Facebook |
| Lưu lượng sử dụng | Số phút gọi, ký tự đọc và token mô hình ngôn ngữ đã dùng |
| Quản lý lịch hẹn | Lịch do AI đặt và lịch do nhân viên nhập |
| Bảng giá / Ưu đãi | Gói cước, hạn mức hàng tháng, mã ưu đãi, yêu cầu nâng cấp |
| Mini CRM | Hồ sơ cơ sở, kênh liên lạc, công cụ, trợ lý, tài liệu tri thức, khách hàng |
| Cấu hình nâng cao | Nhà cung cấp AI riêng, chiến dịch gọi đi, tài khoản nhân viên, thông tin xác thực API (Premium) |
| Khung chat Trợ lý AI | Cửa sổ chat có ở mọi trang để thử trợ lý với kho tri thức |

## 2.3 Khái niệm cơ sở (Tenant)

**Cơ sở (Tenant)** là không gian làm việc của một tổ chức: phòng khám, studio, nhà xe hoặc doanh nghiệp khác.

Mỗi cơ sở có riêng:

- Hồ sơ cơ sở (tên, giờ làm việc, dịch vụ, chi nhánh)
- Người dùng (một quản trị viên và các nhân viên)
- Cuộc gọi, hội thoại, lịch hẹn và khách hàng
- Trợ lý AI, tài liệu tri thức, công cụ và kết nối kênh
- Gói cước, hạn mức hàng tháng và mã ưu đãi

Lĩnh vực chọn khi đăng ký quyết định cách gọi tên trên cổng. Cơ sở nha khoa thấy **Cổng Phòng Khám**, **Thông tin phòng khám** và **Danh sách bệnh nhân**. Lĩnh vực khác thấy nhãn tương ứng với ngành của mình; các bước trong tài liệu giữ nguyên.

## 2.4 Yêu cầu hệ thống

| Yêu cầu | Hỗ trợ |
|---|---|
| Trình duyệt | Trình duyệt máy tính bản mới. Tài liệu được soạn trên trình duyệt nhân Chromium (Chrome, Edge). |
| Micro | Cần cho **Gọi thử (WebRTC)** |
| Mạng | Truy cập Internet tới `https://dev.app.nuitruc.ai` |
| Hệ điều hành, độ phân giải | Chưa công bố cho môi trường phát triển |

---

# 3. Bắt đầu sử dụng

## 3.1 Truy cập hệ thống

**Địa chỉ hệ thống:** <https://dev.app.nuitruc.ai>

Để đăng nhập:

1. Mở địa chỉ hệ thống. Trang **Đăng nhập Cổng Doanh Nghiệp** hiện ra.
2. Nhập email vào **Email tài khoản**.
3. Nhập mật khẩu vào **Mật khẩu**. Biểu tượng con mắt dùng để hiện hoặc ẩn mật khẩu.
4. Bấm **Đăng nhập hệ thống**.

Cổng mở trang **Tổng quan** với giao diện theo lĩnh vực của cơ sở.

[Chèn ảnh chụp màn hình: Trang đăng nhập]

Để đăng xuất, bấm **Đăng xuất** ở cuối menu bên trái.

## 3.2 Đăng ký (lần đầu sử dụng)

Cơ sở mới tự đăng ký. Tài khoản được tạo ở gói miễn phí và trợ lý sẵn sàng ngay, không qua bước chờ duyệt.

1. Tại trang đăng nhập, bấm **Đăng ký Freemium dùng thử miễn phí**. Địa chỉ trang là `/register`.
2. Ở phần **1. Chọn lĩnh vực hoạt động của bạn**, chọn một thẻ.
3. Ở phần **2. Thông tin cơ sở & tài khoản quản trị**, điền biểu mẫu.
4. Tùy chọn: nhập mã vào **Mã ưu đãi (nếu có)** rồi bấm **Áp dụng**.
5. Bấm **Đăng ký tài khoản Freemium & Bắt đầu ngay**.
6. Nếu trang đăng nhập hiện ra, đăng nhập bằng email và mật khẩu vừa đặt.

[Chèn ảnh chụp màn hình: Biểu mẫu đăng ký]

### Lĩnh vực

| Thẻ | Trợ lý được chuẩn bị để |
|---|---|
| **Nha khoa & Y tế** | Tiếp nhận cuộc gọi, đặt lịch khám, tra cứu hồ sơ bệnh nhân |
| **Thiết kế & Kiến trúc** | Tư vấn báo giá theo m², đặt lịch khảo sát công trình |
| **Vận tải & Nhà xe** | Hỗ trợ đặt vé, tra cứu giờ chạy tuyến, đổi trả vé |
| **Dịch vụ & Doanh nghiệp** | Tiếp nhận hotline bán hàng, giải đáp thắc mắc khách hàng |

### Trường nhập liệu

| Trường | Bắt buộc | Mô tả | Ví dụ |
|---|---|---|---|
| **Tên phòng khám / Công ty / Nhà xe** | Có | Tên cơ sở | Nha Khoa Nụ Cười Xinh |
| **Họ và tên người đại diện** | Có | Họ tên người đại diện; cũng là tên quản trị viên | Nguyễn Văn A |
| **Số điện thoại liên hệ** | Không | Số điện thoại liên hệ | 0912 345 678 |
| **Email đăng nhập tài khoản** | Có | Email đăng nhập của quản trị viên | admin@doanhnghiep.vn |
| **Mật khẩu đăng nhập** | Có | Tối thiểu 6 ký tự | — |
| **Mã ưu đãi** | Không | Mã ưu đãi | PROMO30 |

### Kết quả

- Hệ thống tạo không gian làm việc cho cơ sở, người đăng ký là **Quản trị viên**.
- Voicebot và chatbot được kích hoạt, kèm một trợ lý sao chép từ kịch bản mẫu của lĩnh vực.
- Có thể thử trợ lý ngay trên trình duyệt bằng **Gọi thử (WebRTC)**. Đường dây tổng đài là tùy chọn ở bước này.

## 3.3 Tài khoản dùng thử

Sau khi nắm quy trình đăng ký, bạn có thể trải nghiệm một không gian làm việc đã có sẵn dữ liệu.

| Mục | Giá trị |
|---|---|
| Địa chỉ | <https://dev.app.nuitruc.ai> |
| Email | `vietphap@gmail.com` |
| Mật khẩu | `xvJWoDD9iG6S` |
| Cơ sở | **Nha Khoa Việt Pháp** (phòng khám nha khoa), vai trò **Quản trị viên**, gói miễn phí |

Cơ sở này có ba trợ lý, tài liệu tri thức, lịch sử cuộc gọi và hội thoại, lịch hẹn và một hồ sơ bệnh nhân.

Đây là tài khoản dùng chung. Bạn cứ thoải mái xem, và vui lòng giữ nguyên dữ liệu hiện có (tránh xóa hoặc ghi đè). Vì cơ sở ở gói miễn phí, các mục trong **Cài đặt nâng cao** hiện biểu tượng khóa; [mục 6.8](#68-cấu-hình-nâng-cao) mô tả các tính năng đó.

## 3.4 Quản lý mật khẩu

- Mật khẩu được đặt khi đăng ký, tối thiểu 6 ký tự.
- Tài khoản nhân viên nhận mật khẩu tạm khi quản trị viên tạo tài khoản ([mục 6.8.3](#683-nhân-viên-và-phân-quyền)).
- Trang đăng nhập chưa có liên kết **Quên mật khẩu**. Để đặt lại mật khẩu quản trị viên, liên hệ bộ phận hỗ trợ NuiTruc. Với tài khoản nhân viên, quản trị viên có thể xóa rồi tạo lại Operator để nhận mật khẩu tạm mới.
- Quy định về thời hạn và việc dùng lại mật khẩu chưa được công bố.

## 3.5 Chọn cơ sở

Mỗi tài khoản thuộc một cơ sở, và cổng mở thẳng cơ sở đó sau khi đăng nhập. Tên cơ sở hiển thị ở đầu menu bên trái.

---

# 4. Điều hướng hệ thống

## 4.1 Giao diện chính

| Khu vực | Mô tả |
|---|---|
| Đầu menu bên trái | Tên cơ sở và loại cổng (ví dụ **Nha Khoa Việt Pháp – Cổng Phòng Khám**) |
| Thẻ người dùng | Họ tên và vai trò: **Quản trị viên** hoặc **Nhân viên** |
| Menu điều hướng | Ba nhóm, liệt kê bên dưới |
| **Đăng xuất** | Thoát khỏi hệ thống |
| Vùng làm việc chính | Trang của menu đang chọn |
| Nút chat **Trợ lý AI** | Mở khung chat Trợ lý AI ([mục 6.1](#61-tổng-quan)) |

[Chèn ảnh chụp màn hình: Giao diện chính có chú thích]

### Menu

| Nhóm | Mục menu | Mục đích | Mục |
|---|---|---|---|
| Vận hành | **Tổng quan** | Bảng tổng quan | [6.1](#61-tổng-quan) |
| Vận hành | **Lịch sử cuộc gọi** | Lịch sử cuộc gọi | [6.2](#62-lịch-sử-cuộc-gọi) |
| Vận hành | **Lịch sử hội thoại** | Lịch sử chat | [6.3](#63-lịch-sử-hội-thoại) |
| Vận hành | **Lưu lượng sử dụng** | Lưu lượng AI | [6.4](#64-lưu-lượng-sử-dụng-ai-usage) |
| Vận hành | **Lịch hẹn ghi nhận** | Lịch hẹn | [6.5](#65-quản-lý-lịch-hẹn) |
| Vận hành | **Bảng giá & Gói cước** | Bảng giá và gói cước | [6.6](#66-bảng-giá-và-ưu-đãi) |
| **Cài đặt hệ thống** | **Thông tin phòng khám** | Thông tin cơ sở | [6.7.1](#671-thông-tin-cơ-sở) |
| **Cài đặt hệ thống** | **Số tổng đài & Kênh** | Tổng đài và kênh liên lạc | [6.7.2](#672-cấu-hình-tổng-đài-và-kênh-liên-lạc) |
| **Cài đặt hệ thống** | **Công cụ tích hợp** | Công cụ (tool) | [6.7.3](#673-công-cụ-tool-call) |
| **Cài đặt hệ thống** | **Quản lý Trợ lý AI (Agent)** | Trợ lý AI | [6.7.4](#674-quản-lý-trợ-lý-ai-agent) |
| **Cài đặt hệ thống** | **Tài liệu tri thức** | Kho tri thức | [6.7.5](#675-tài-liệu-tri-thức-knowledge-base) |
| **Cài đặt hệ thống** | **Danh sách bệnh nhân** | Khách hàng | [6.7.6](#676-quản-lý-khách-hàng) |
| **Cài đặt nâng cao** | **Cấu hình mô hình AI** | Cấu hình mô hình AI | [6.8.1](#681-cấu-hình-mô-hình-ai) |
| **Cài đặt nâng cao** | **Chiến dịch gọi đi** | Chiến dịch gọi đi | [6.8.2](#682-chiến-dịch-gọi-đi) |
| **Cài đặt nâng cao** | **Nhân viên & Phân quyền** | Nhân viên và phân quyền | [6.8.3](#683-nhân-viên-và-phân-quyền) |
| **Cài đặt nâng cao** | **Thông tin xác thực hệ thống phòng khám** | Thông tin xác thực | [6.8.4](#684-thông-tin-xác-thực) |

Nhóm đầu tiên không có tiêu đề trên màn hình. Hai nhóm cài đặt hiển thị cho quản trị viên. Ở gói miễn phí, mỗi mục trong **Cài đặt nâng cao** có biểu tượng khóa.

## 4.2 Tổng quan bảng điều khiển

**Tổng quan** hiển thị bốn chỉ số, các cuộc gọi gần nhất và lịch hẹn mới nhất. [Mục 6.1](#61-tổng-quan) mô tả từng phần.

## 4.3 Thành phần giao diện thường gặp

| Thành phần | Nhãn trên cổng | Mô tả |
|---|---|---|
| Tìm kiếm | **Tìm kiếm**, **Tìm tên hoặc SĐT...** | Tìm bản ghi theo tên, số điện thoại hoặc nội dung |
| Lọc theo ngày | **Từ ngày** / **Đến ngày**, **Lọc** | Giới hạn danh sách theo khoảng ngày |
| Xóa bộ lọc | **Xóa bộ lọc** | Bỏ toàn bộ điều kiện lọc |
| Làm mới | **Làm mới** | Tải lại danh sách |
| Tạo mới | **Tạo …**, **Thêm …** | Tạo bản ghi |
| Sửa | **Sửa** | Thay đổi bản ghi |
| Xóa | **Xóa** | Xóa bản ghi |
| Lưu | **Lưu** | Lưu biểu mẫu |
| Hủy | **Hủy**, **Đóng** | Đóng mà không lưu |
| Phân trang | **Sau**, **Trang 1 / 4** | Chuyển trang |
| Chi tiết | **Xem chi tiết**, **Xem audio & transcript** | Mở bản ghi |

---

# 5. Quản trị cơ sở

Phần này dành cho người dùng có vai trò **Quản trị viên**. Nội dung tóm tắt công việc quản trị và dẫn tới các bước chi tiết ở [mục 6](#6-tính-năng-chính).

## 5.1 Hồ sơ cơ sở

Hồ sơ cơ sở là trang **Thông tin phòng khám**, gồm tên cơ sở, giờ làm việc từng ngày trong tuần, dịch vụ và chi nhánh. Trợ lý AI đọc hồ sơ này khi khách hỏi về địa chỉ, giờ mở cửa và dịch vụ.

Các bước: [mục 6.7.1](#671-thông-tin-cơ-sở).

## 5.2 Quản lý người dùng

Quản trị viên tạo tài khoản nhân viên tại **Cài đặt nâng cao → Nhân viên & Phân quyền**. Tính năng này yêu cầu Premium.

Các bước: [mục 6.8.3](#683-nhân-viên-và-phân-quyền).

## 5.3 Vai trò và quyền hạn

| Vai trò | Nhãn trên cổng | Quyền truy cập |
|---|---|---|
| Tenant Admin | **Quản trị viên** (`tenant_admin`) | Mọi menu. Tạo và xóa bản ghi, cấu hình trợ lý, quản lý nhân viên. |
| Tenant User | **Nhân viên** (`operator`) | Các menu vận hành để theo dõi hằng ngày: tổng quan, lịch sử cuộc gọi, lưu lượng, lịch hẹn. |

Lưu ý:

- Người đăng ký là quản trị viên. Tài khoản do quản trị viên tạo là nhân viên.
- Cổng có hai vai trò cố định này. Vai trò tùy chỉnh và phân quyền chi tiết chưa có.
- Tài liệu được kiểm chứng bằng tài khoản quản trị viên. Giao diện của nhân viên chưa được kiểm tra bằng một tài khoản nhân viên thực tế; hãy xác nhận với NuiTruc việc nhân viên có thấy **Lịch sử hội thoại** và **Bảng giá & Gói cước** hay không, và nhân viên có được tạo hoặc sửa lịch hẹn hay không.

## 5.4 Cấu hình cơ sở

| Cấu hình | Menu | Gói | Mục |
|---|---|---|---|
| Hồ sơ cơ sở | **Thông tin phòng khám** | Miễn phí | [6.7.1](#671-thông-tin-cơ-sở) |
| Tổng đài, Facebook, Zalo, nút gọi trên website | **Số tổng đài & Kênh** | Miễn phí | [6.7.2](#672-cấu-hình-tổng-đài-và-kênh-liên-lạc) |
| Công cụ trợ lý được gọi | **Công cụ tích hợp** | Miễn phí để xem; Premium để tạo | [6.7.3](#673-công-cụ-tool-call) |
| Trợ lý và kịch bản | **Quản lý Trợ lý AI (Agent)** | Miễn phí khi dùng mẫu; Premium khi tạo trợ lý trống | [6.7.4](#674-quản-lý-trợ-lý-ai-agent) |
| Tài liệu để trợ lý trả lời | **Tài liệu tri thức** | Miễn phí | [6.7.5](#675-tài-liệu-tri-thức-knowledge-base) |
| Danh sách khách hàng | **Danh sách bệnh nhân** | Miễn phí | [6.7.6](#676-quản-lý-khách-hàng) |
| Nhà cung cấp AI | **Cấu hình mô hình AI** | Premium | [6.8.1](#681-cấu-hình-mô-hình-ai) |
| Gọi đi | **Chiến dịch gọi đi** | Premium | [6.8.2](#682-chiến-dịch-gọi-đi) |
| Thông tin xác thực API | **Thông tin xác thực hệ thống phòng khám** | Premium | [6.8.4](#684-thông-tin-xác-thực) |

Cổng chưa có cài đặt ngôn ngữ, múi giờ, tùy chọn thông báo và thời gian lưu trữ dữ liệu. Ngôn ngữ giao diện là tiếng Việt.

---

# 6. Tính năng chính

## 6.1 Tổng quan

### Giới thiệu

**Tổng quan** cho biết nhanh trợ lý đang hoạt động thế nào và việc gì cần theo dõi trong ngày.

### Điều kiện sử dụng

| Yêu cầu | Chi tiết |
|---|---|
| Vai trò | Quản trị viên, Nhân viên |
| Gói | Mọi gói |
| Menu | **Tổng quan** |

### Giao diện

| Thành phần | Mô tả |
|---|---|
| **Trợ lý hoạt động** | Số trợ lý đang hoạt động |
| **Cuộc gọi (7 ngày)** | Số cuộc gọi trong 7 ngày gần nhất |
| **Tỷ lệ thành công** | Tỷ lệ cuộc gọi hoàn thành |
| **Lịch hẹn đã đặt** | Số lịch hẹn đã đặt |
| **Cuộc gọi gần đây** | Các cuộc gọi mới nhất; bấm vào thời gian để mở cuộc gọi, hoặc **Xem tất cả** để mở toàn bộ lịch sử |
| **Lịch hẹn mới nhận** | Lịch hẹn mới nhất; **Xem tất cả** mở danh sách lịch hẹn |
| Thông báo **Chưa cấu hình Kênh tổng đài (SIP Trunk)** | Hiển thị khi chưa kết nối đường dây. Liên kết **Số tổng đài & Kênh** mở trang cấu hình kênh. |

[Chèn ảnh chụp màn hình: Tổng quan]

### Khung chat Trợ lý AI

Khung chat có ở mọi trang. Trợ lý trả lời từ ba kho tri thức của cơ sở, nên đây là cách nhanh nhất để kiểm tra câu trả lời của trợ lý.

1. Bấm **Mở khung chat Trợ lý AI** (nút chat).
2. Bấm một câu trong **Gợi ý kiểm tra nhanh** hoặc gõ vào **Nhập câu hỏi cho Trợ lý AI...**, rồi bấm **Gửi tin nhắn**.
3. Dùng **Làm mới cuộc trò chuyện** để bắt đầu hội thoại mới, **Mở rộng toàn màn hình** để phóng to, **Đóng khung chat** để đóng.

Hội thoại tại đây được lưu trong **Lịch sử hội thoại** ở kênh **Web** kèm tên của bạn. Khung chat cũng nhận đặt lịch; ở cơ sở dùng thử, các lịch này xuất hiện trong danh sách lịch hẹn với nguồn **Hệ thống**.

## 6.2 Lịch sử cuộc gọi

### Giới thiệu

**Lịch sử cuộc gọi** liệt kê mọi cuộc gọi thoại do trợ lý xử lý, từ đường dây điện thoại và từ trình duyệt (WebRTC), gồm cả cuộc gọi thử.

### Điều kiện sử dụng

| Yêu cầu | Chi tiết |
|---|---|
| Vai trò | Quản trị viên, Nhân viên |
| Gói | Mọi gói |
| Menu | **Lịch sử cuộc gọi** |

### Cách sử dụng

#### Bước 1: Tìm cuộc gọi

1. Mở **Lịch sử cuộc gọi**.
2. Tùy chọn: đặt **Từ ngày** và **Đến ngày**, rồi bấm **Lọc**.
3. Bấm **Sau** ở cuối trang để sang trang kế tiếp. Mỗi trang hiển thị 20 cuộc gọi.

[Chèn ảnh chụp màn hình: Danh sách cuộc gọi]

| Cột | Ý nghĩa |
|---|---|
| **THỜI GIAN** | Thời điểm bắt đầu |
| **TRỢ LÝ** | Trợ lý xử lý cuộc gọi |
| **KÊNH** | Kênh, ví dụ **Web** |
| **LOẠI** | Chiều cuộc gọi, ví dụ **Gọi đến** |
| **THỜI LƯỢNG** | Thời lượng tính bằng giây |
| **TRẠNG THÁI** | **Hoàn thành**, **Đang xử lý** hoặc **Thất bại** |
| **CHI TIẾT** | **Xem audio & transcript** |

#### Bước 2: Xem lại cuộc gọi

1. Bấm vào thời gian hoặc **Xem audio & transcript**. Trang **Kết quả cuộc gọi #…** mở ra.
2. Xem phần tóm tắt: **Trạng thái**, **Kênh**, **Loại**, **Thời lượng**, **Bắt đầu**.
3. Đọc **Transcript**. Mỗi dòng được ghi **TRỢ LÝ AI** hoặc **KHÁCH HÀNG**.
4. Ở **Bản ghi âm**, bấm **Mở hoặc tải bản ghi âm** để nghe hoặc tải về.
5. Bấm **← Quay lại lịch sử** để trở về.

[Chèn ảnh chụp màn hình: Chi tiết cuộc gọi]

### Lưu ý

- Cuộc gọi ở trạng thái **Đang xử lý** chưa có thời lượng.
- Khi trợ lý đặt lịch trong cuộc gọi, danh sách lịch hẹn có liên kết về cuộc gọi đó.

## 6.3 Lịch sử hội thoại

### Giới thiệu

**Lịch sử hội thoại** liệt kê các cuộc trò chuyện bằng văn bản giữa khách hàng và chatbot trên Web, Zalo và Facebook.

### Điều kiện sử dụng

| Yêu cầu | Chi tiết |
|---|---|
| Vai trò | Quản trị viên (với nhân viên, xem lưu ý ở [mục 5.3](#53-vai-trò-và-quyền-hạn)) |
| Gói | Mọi gói |
| Menu | **Lịch sử hội thoại** |

### Cách sử dụng

1. Mở **Lịch sử hội thoại**.
2. Thu hẹp danh sách khi cần:
   - **Tìm kiếm**: tên khách hàng, số điện thoại hoặc nội dung tin nhắn
   - **Kênh**: **Tất cả**, **Web**, **Zalo** hoặc **Facebook**
   - **Từ ngày** / **Đến ngày**
3. Bấm **Xóa bộ lọc** để đặt lại, hoặc **Làm mới** để tải lại.
4. Bấm **Xem chi tiết** ở một dòng. Bảng **Chi tiết hội thoại** hiển thị từng tin nhắn kèm thời gian.
5. Bấm **Close** để trở về danh sách.

[Chèn ảnh chụp màn hình: Lịch sử hội thoại]

| Cột | Ý nghĩa |
|---|---|
| **Bệnh nhân** | Tên và số điện thoại khách hàng, hoặc người dùng đang đăng nhập với hội thoại trên cổng |
| **Kênh** | Web, Zalo hoặc Facebook |
| **Tin nhắn gần nhất** | Tin nhắn mới nhất |
| **Số tin nhắn** | Số tin nhắn |
| **Cập nhật lúc** | Lần cập nhật gần nhất |
| **Trạng thái** | Ví dụ **Đã kết thúc** |
| **Thao tác** | **Xem chi tiết** |

## 6.4 Lưu lượng sử dụng (AI usage)

### Giới thiệu

**Lưu lượng sử dụng** cho biết cơ sở đã dùng bao nhiêu thời gian gọi và tài nguyên AI trong một giai đoạn.

### Điều kiện sử dụng

| Yêu cầu | Chi tiết |
|---|---|
| Vai trò | Quản trị viên, Nhân viên |
| Gói | Mọi gói |
| Menu | **Lưu lượng sử dụng** |

### Cách sử dụng

1. Mở **Lưu lượng sử dụng**.
2. Chọn **Hôm nay**, **7 ngày** hoặc **30 ngày**. Dòng **Giai đoạn** xác nhận khoảng ngày.

[Chèn ảnh chụp màn hình: Lưu lượng sử dụng]

| Chỉ số | Ý nghĩa |
|---|---|
| **Tổng cuộc gọi** | Tổng số cuộc gọi; **Cuộc gọi thử** là số cuộc gọi thử trong đó |
| **Tổng thời lượng thoại** | Tổng thời gian đàm thoại tính bằng phút, kèm số giây thực tế |
| **Ký tự TTS đọc hoàn tất** | Số ký tự trợ lý đã đọc (chuyển văn bản thành giọng nói), kèm thời lượng phát âm |
| **STT / TTS audio** | Số giây âm thanh đã nhận dạng (STT) và đã phát (TTS) |
| **LLM input tokens** | Số token ngữ cảnh gửi vào mô hình ngôn ngữ |
| **LLM output tokens** | Số token mô hình ngôn ngữ tạo ra |
| **Tổng tokens LLM** | Đầu vào cộng đầu ra |

### Lưu ý

- Cuộc gọi thử được tính vào lưu lượng.
- Trang này báo cáo mức tiêu thụ theo đơn vị kỹ thuật. Hạn mức hàng tháng tính bằng VNĐ hiển thị ở **Bảng giá & Gói cước**.

## 6.5 Quản lý lịch hẹn

### Giới thiệu

**Lịch hẹn ghi nhận** là danh sách chung cho lịch do AI đặt trong cuộc gọi, trong hội thoại và lịch do nhân viên nhập.

### Điều kiện sử dụng

| Yêu cầu | Chi tiết |
|---|---|
| Vai trò | Quản trị viên: xem, tạo, sửa, xóa. Nhân viên: xem lưu ý ở [mục 5.3](#53-vai-trò-và-quyền-hạn). |
| Gói | Mọi gói |
| Menu | **Lịch hẹn ghi nhận** |

### Giao diện

| Cột | Ý nghĩa |
|---|---|
| **BỆNH NHÂN** | Tên khách hàng |
| **SĐT** | Số điện thoại |
| **NGÀY GIỜ HẸN** | Ngày giờ hẹn |
| **NỘI DUNG KHÁM** | Lý do đến khám |
| **NGUỒN TẠO** | Người tạo: **AI · tên trợ lý**, **Hệ thống**, hoặc tên nhân viên |
| **CUỘC GỌI** | Liên kết tới cuộc gọi mà AI đã đặt lịch |
| **THAO TÁC** | **Sửa**, **Xóa** |

[Chèn ảnh chụp màn hình: Danh sách lịch hẹn]

### Cách sử dụng

#### Tạo lịch hẹn

1. Bấm **Tạo lịch hẹn**.
2. Điền biểu mẫu.
3. Bấm **Tạo lịch**. Bấm **Hủy** để đóng mà không lưu.

| Trường | Bắt buộc | Mô tả | Ví dụ |
|---|---|---|---|
| **Tên bệnh nhân** | Có | Tên khách hàng | Nguyễn Văn B |
| **Số điện thoại** | Có | Số điện thoại | 0912345678 |
| **Ngày giờ hẹn** | Có | Ngày và giờ | 25/11/2026 09:00 |
| **Nội dung khám** | Không | Lý do đến khám | Trám răng |

#### Sửa hoặc xóa lịch hẹn

1. Tìm dòng cần xử lý.
2. Bấm **Sửa**, thay đổi thông tin rồi lưu. Hoặc bấm **Xóa** để xóa lịch hẹn.

### Quy tắc nghiệp vụ

- Trợ lý xác nhận họ tên, số điện thoại, dịch vụ và thời gian với khách trước khi đặt lịch.
- Lịch do AI đặt trong cuộc gọi cũng thêm người gọi vào danh sách khách hàng ([mục 6.7.6](#676-quản-lý-khách-hàng)).
- Trong các kịch bản dùng thử, trợ lý báo với khách rằng nhân viên sẽ gọi lại xác nhận. Hãy theo dõi lịch mới từ danh sách này.

## 6.6 Bảng giá và ưu đãi

### Giới thiệu

**Bảng giá & Gói cước** hiển thị gói hiện tại, các gói đang cung cấp, mã ưu đãi và yêu cầu nâng cấp.

### Điều kiện sử dụng

| Yêu cầu | Chi tiết |
|---|---|
| Vai trò | Quản trị viên (với nhân viên, xem lưu ý ở [mục 5.3](#53-vai-trò-và-quyền-hạn)) |
| Gói | Mọi gói |
| Menu | **Bảng giá & Gói cước** |

### Các gói

Giá là giá niêm yết theo tháng, chưa gồm VAT, theo hiển thị trên môi trường phát triển.

| Gói | Giá / tháng | Hạn mức hàng tháng | Ưu đãi tặng | Cuộc gọi song song | Khách hàng |
|---|---|---|---|---|---|
| **Free** | 0 đ | 200.000 VNĐ | 200.000 VNĐ | [1](#1-thông-tin-tài-liệu) | 100 |
| **Basic** | 1.000.000 đ | 1.200.000 VNĐ | 200.000 VNĐ | [2](#2-giới-thiệu) | 300 |
| **Pro** | 3.000.000 đ | 3.600.000 VNĐ | 600.000 VNĐ | [6](#6-tính-năng-chính) | 1.000 |
| **Pro+** | 10.000.000 đ | 18.000.000 VNĐ | 8.000.000 VNĐ | [10](#10-xử-lý-sự-cố) | Trên 1.000 |
| **Enterprise** | Báo giá | Theo nhu cầu | Theo hợp đồng | Theo yêu cầu | Không giới hạn |

| Gói | Thoại | Chat | Mô hình AI và công cụ |
|---|---|---|---|
| **Free** | Gọi đến qua hotline | Nhận tin trên 1 kênh: Zalo hoặc Facebook | Mô hình tiêu chuẩn NuiTruc |
| **Basic** | Gọi đến qua SĐT, Zalo, Web | Nhận tin trên Web, Zalo, Facebook | Mô hình tiêu chuẩn NuiTruc |
| **Pro** | Gọi đến và gọi đi, toàn bộ kênh | Nhận và gửi, toàn bộ kênh | Tùy chỉnh LLM / TTS / STT; công cụ và trợ lý tùy biến chuyên sâu |
| **Pro+** | Gọi đến và gọi đi, toàn bộ kênh | Nhận và gửi, toàn bộ kênh | Mô hình tùy chỉnh, ưu tiên GPU; công cụ và trợ lý tùy biến chuyên sâu |
| **Enterprise** | SIP Trunk và tổng đài riêng | Bao gồm | GPU riêng hoặc On-Premise; tích hợp HIS / CRM / ERP; SLA 99,9% và hỗ trợ kỹ thuật 24/7 |

[Chèn ảnh chụp màn hình: Trang bảng giá]

### Cách sử dụng

#### Bước 1: Xem gói hiện tại

Dòng **Gói hiện tại** dưới tiêu đề cho biết gói và hạn mức đang dùng, ví dụ **Free (200k Quota)**. Thẻ của gói đó được đánh dấu **Gói đang dùng**.

#### Bước 2: Chọn chu kỳ thanh toán

Bấm **Hàng tháng** hoặc **Hàng năm -20%**. Thanh toán theo năm giảm 20% giá.

#### Bước 3: Áp dụng mã ưu đãi

1. Nhập mã vào **Nhập mã ưu đãi (VD: PROMO30)**.
2. Bấm **Áp dụng**.
3. Khung **Đang kích hoạt Mã ưu đãi** hiển thị mã, mức giảm, các gói được áp dụng và số ngày còn hiệu lực. Thẻ gói hiển thị giá đã giảm bên cạnh giá niêm yết.
4. Bấm **Hủy dùng mã** để gỡ mã.

Mã ưu đãi cũng có thể nhập khi đăng ký.

#### Bước 4: Gửi yêu cầu nâng cấp

1. Bấm nút trên thẻ gói: **Chọn gói Basic**, **Đăng ký gói Pro** hoặc **Chọn gói Pro+**.
2. Xem phần tóm tắt **GÓI BẠN ĐANG CHỌN**: gói, chu kỳ thanh toán, hạn mức, **Cước**, **VAT (10%)** và **Tổng thanh toán**.
3. Bấm **Gửi yêu cầu nâng cấp gói**. NuiTruc sẽ xử lý yêu cầu.
4. Với **Enterprise**, bấm **Liên hệ báo giá**. **Hotline tư vấn** gọi tới tổng đài tư vấn.

### Lưu ý

- Cơ sở dùng thử đang kích hoạt mã `VANHOAVIETNAM` (giảm 100% các gói trả phí trong thời gian giới hạn), nên các thẻ gói hiển thị 0 đ. Bảng trên ghi giá niêm yết.
- Cổng gọi các tính năng nâng cao là **Premium**. Thẻ gói liệt kê mô hình AI tùy chỉnh, kênh gọi đi và công cụ tùy biến từ gói **Pro** trở lên. Hãy xác nhận với NuiTruc gói nào kích hoạt Premium cho cơ sở của bạn.

## 6.7 Mini CRM

Nhóm **Cài đặt hệ thống** là mini CRM của cơ sở. Quản trị viên dùng được ở mọi gói.

### 6.7.1 Thông tin cơ sở

#### Giới thiệu

**Thông tin phòng khám** lưu những thông tin trợ lý cung cấp cho khách: tên, giờ mở cửa, dịch vụ và chi nhánh.

#### Cách sử dụng

1. Mở **Thông tin phòng khám**.
2. Sửa **Tên phòng khám**.
3. Ở **Giờ làm việc**, đặt giờ mở và giờ đóng cho từng ngày từ **Thứ Hai** đến **Chủ Nhật**.
4. Ở **Dịch vụ**, bấm **+ Thêm dịch vụ** rồi nhập **Tên dịch vụ** và **Mô tả**.
5. Ở **Chi nhánh**, bấm **+ Thêm chi nhánh** rồi nhập **Tên chi nhánh** và **Địa chỉ**. **Xóa** dùng để bỏ một chi nhánh.
6. Bấm **Lưu**.

[Chèn ảnh chụp màn hình: Thông tin cơ sở]

#### Quy tắc nghiệp vụ

- Trợ lý trả lời câu hỏi về tên, địa chỉ, giờ làm việc và dịch vụ từ trang này. Hãy giữ thông tin luôn cập nhật.
- Bảng giá chi tiết và chính sách thuộc về kho tri thức ([mục 6.7.5](#675-tài-liệu-tri-thức-knowledge-base)).

### 6.7.2 Cấu hình tổng đài và kênh liên lạc

#### Giới thiệu

**Số tổng đài & Kênh** (tiêu đề trang **Kênh liên lạc**) kết nối trợ lý với các kênh. Trang có ba thẻ, mỗi thẻ có nhãn trạng thái như **Chưa cấu hình**, **Đã cấu hình** hoặc **Đã kết nối**.

| Thẻ | Kênh |
|---|---|
| **Tổng đài Omni** | Đường dây điện thoại qua tổng đài Omni (OMICALL) |
| **Chatbot Facebook & Zalo** | Tin nhắn Fanpage Facebook và Zalo Official Account |
| **WebRTC** | Nút gọi thoại nhúng trên website |

[Chèn ảnh chụp màn hình: Kênh liên lạc]

#### Kết nối đường dây điện thoại (Tổng đài Omni)

1. Mở thẻ **Tổng đài Omni**.
2. Điền thông tin kết nối lấy từ tài khoản OMICALL.
3. Bấm **Lưu cấu hình Omni**.
4. Ở **Inbound Agent**, chọn trợ lý trả lời cuộc gọi đến.

| Trường | Bắt buộc | Mô tả |
|---|---|---|
| **Nhà cung cấp tổng đài** | Có | Hiện có **Omni (OMICALL)**; các nhà cung cấp khác được ghi **Chưa hỗ trợ**. |
| **Địa chỉ kết nối tổng đài** | Có | Địa chỉ kết nối, ví dụ `http://tong-dai:8088` |
| **Tên ứng dụng tổng đài** | Có | Tên ứng dụng tổng đài |
| **Mật khẩu kết nối** | Có | Mật khẩu kết nối |
| **Số hotline đã đăng ký với Omni** | Không | Các số hotline, mỗi dòng một số |
| **Kết nối nâng cao → Tên WebSocket client** | Không | Tùy chọn nâng cao, nếu nhà cung cấp có cấp |

Dòng **Voicebot telephony** cho biết kết nối đã được xác minh hay chưa. Khi chưa kết nối đường dây, trang tổng quan hiển thị thông báo **Chưa cấu hình Kênh tổng đài (SIP Trunk)**.

#### Kết nối Facebook và Zalo (Chatbot Facebook & Zalo)

Đầu thẻ hiển thị **Mã trợ lý AI (Agent ID)**, **Khóa tích hợp (API Key)** dạng che kèm nút **Hiện** và **Sao chép**, liên kết **Tải file Kịch bản (YAML)**, và trạng thái ba kho tri thức.

**Fanpage Facebook**

1. Trong ứng dụng Meta for Developers, khai báo **Callback URL (Webhook)** và **Verify Token** hiển thị trên thẻ. Dùng **Chép URL** và **Chép Token** để sao chép.
2. Trên cổng, nhập **Facebook Page ID** và **Page Access Token**.
3. Bấm **Lưu Cấu Hình Fanpage Facebook**.

**Zalo Official Account**

1. Trong Zalo Developers, khai báo **Webhook URL cho Zalo OA** hiển thị trên thẻ (**Chép Webhook URL**) và đăng ký sự kiện `user_send_text`.
2. Trên cổng, nhập **Zalo OA ID**, **Zalo App ID**, **Secret Key**, **Access Token** và **Refresh Token**. **Hiện các mã bảo mật** dùng để xem các giá trị đang ẩn.
3. Bấm **Lưu Cấu Hình Zalo OA**.

Khi đã lưu Refresh Token, chatbot tự gia hạn quyền truy cập Zalo.

**Cấu hình tùy chỉnh nâng cao** cho phép quản trị viên đổi Agent ID và API Key thủ công. Giữ nguyên phần này khi sử dụng thông thường.

#### Thêm nút gọi vào website (WebRTC)

1. Mở thẻ **WebRTC**.
2. Ở **Inbound Agent**, chọn một trợ lý.
3. Bấm **Generate embed snippet** rồi đặt đoạn mã được tạo vào website.

#### Outbound use cases (Premium)

Với Premium, khối **Outbound use cases** gắn một tên use case với một trợ lý để gọi đi.

1. Nhập **Tên use case**.
2. Chọn **Agent**.
3. Bấm **Thêm use case**.

Chiến dịch gọi đi ([mục 6.8.2](#682-chiến-dịch-gọi-đi)) chọn từ các use case này.

#### Quy tắc nghiệp vụ

- Mỗi kênh có một trợ lý inbound xử lý cuộc gọi và tin nhắn đến.
- Access token, secret key và API key là thông tin mật. Chỉ chia sẻ với người trực tiếp cấu hình tích hợp.
- Khi tài liệu tri thức thay đổi, chatbot trên Facebook và Zalo trả lời theo nội dung mới mà không cần cấu hình lại.

### 6.7.3 Công cụ (Tool call)

#### Giới thiệu

Công cụ là các hành động trợ lý thực hiện trong hội thoại, ví dụ đọc hồ sơ cơ sở hoặc tạo lịch hẹn. **Công cụ tích hợp** liệt kê các công cụ đó.

#### Công cụ hệ thống

Mọi cơ sở được kế thừa các công cụ sau từ nền tảng. Chúng được ghi **CHỈ ĐỌC** và **Kế thừa từ hệ thống**.

| Công cụ | Trợ lý dùng để |
|---|---|
| `read_clinic_profile_nt` | Đọc tên, chi nhánh, giờ làm việc và dịch vụ từ **Thông tin phòng khám** |
| `search_knowledge_nt` | Tra cứu kho tri thức về bảng giá, dịch vụ, bác sĩ và chính sách |
| `add_patient_nt` | Thêm khách hàng vào danh sách, tự chống trùng theo số điện thoại |
| `create_appointment_nt` | Tạo lịch hẹn sau khi khách xác nhận |

Bảng **Danh sách công cụ đã tạo** hiển thị tên, nguồn, mô tả, phương thức HTTP và ID, kèm bộ đếm **Hệ thống** và **Cơ sở**.

[Chèn ảnh chụp màn hình: Công cụ tích hợp]

#### Tạo công cụ HTTP riêng (Premium)

1. Mở **Công cụ tích hợp**. Biểu mẫu **Tạo mới công cụ HTTP API** nằm ở đầu trang.
2. Điền biểu mẫu.
3. Bấm **Tạo công cụ**.
4. Gắn công cụ vào trợ lý trong Builder ([mục 6.7.4](#674-quản-lý-trợ-lý-ai-agent)).

| Trường | Bắt buộc | Mô tả | Ví dụ |
|---|---|---|---|
| **Tên công cụ** | Có | Tên công cụ | Lấy lịch trống |
| **Mô tả** | Có | Giúp trợ lý biết khi nào dùng công cụ | Kiểm tra lịch trống trước khi đề xuất giờ hẹn |
| **Phương thức** | Có | GET, POST, PUT, PATCH hoặc DELETE | GET |
| **URL endpoint** | Có | Địa chỉ API của cơ sở | `https://api.example.com/appointments` |
| **Headers (JSON, tùy chọn)** | Không | Header của yêu cầu, dạng JSON | `{"X-Api-Key": "..."}` |

Ở gói miễn phí, biểu mẫu này được thay bằng thông báo **Premium**.

### 6.7.4 Quản lý trợ lý AI (Agent)

#### Giới thiệu

**Quản lý Trợ lý AI (Agent)** là nơi tạo, thử, chỉnh sửa và xóa trợ lý. Mỗi trợ lý gồm một kịch bản hội thoại và các công cụ đi kèm.

| Thẻ | Nội dung |
|---|---|
| **Trợ lý của tôi** | Các trợ lý của cơ sở, kèm kịch bản mẫu nguồn |
| **Kho kịch bản mẫu AI** | Các kịch bản mẫu có sẵn |
| **Tạo Trợ lý** | Tạo trợ lý trống (Premium) |

[Chèn ảnh chụp màn hình: Danh sách trợ lý]

#### Tạo trợ lý từ kịch bản mẫu

1. Mở thẻ **Kho kịch bản mẫu AI**.
2. Chọn một kịch bản.
3. Nhập tên vào **Đặt tên Trợ lý (bắt buộc)**.
4. Bấm **Áp dụng kịch bản này**. Trợ lý xuất hiện ở **Trợ lý của tôi** và hoạt động độc lập với kịch bản mẫu.

Kịch bản mẫu cho cơ sở nha khoa:

| Kịch bản | Công dụng |
|---|---|
| **Tư Vấn Tri Thức & Đặt Lịch Tự Động (Có RAG Tool)** | Trả lời từ kho tri thức (bảng giá, dịch vụ, bác sĩ, chính sách) và đặt lịch hẹn |
| **Đàm Thoại Giọng Thật & Chốt Lịch Tự Động (Hybrid)** | Dùng giọng người thật thu sẵn để tư vấn và giọng tổng hợp để đọc xác nhận lịch |
| **Đặt Lịch & Tiếp Nhận Khách Hàng (2-3 Phút)** | Cuộc gọi hotline ngắn: phân loại nhu cầu, thu thập họ tên, số điện thoại, giờ hẹn và lưu khách hàng, lịch hẹn |

#### Thử trợ lý

1. Ở **Trợ lý của tôi**, bấm **Gọi thử (WebRTC)**. Trang **Chạy thử Trợ lý ảo (WebRTC)** mở ra.
2. Bấm **Bắt đầu cuộc gọi thử** và cho phép trình duyệt dùng micro.
3. Trò chuyện với trợ lý. **Nhật ký hội thoại thời gian thực** hiển thị nội dung ngay khi diễn ra.
4. Kết thúc cuộc gọi. Cuộc gọi xuất hiện trong **Lịch sử cuộc gọi** với kênh **Web** và được tính vào lưu lượng.

[Chèn ảnh chụp màn hình: Gọi thử]

#### Chỉnh kịch bản (Builder)

1. Bấm **Mở Builder**. Kịch bản mở ra dưới dạng sơ đồ luồng. Giao diện Builder bằng tiếng Anh.
2. Thêm nút từ **Add New Node**:

   | Nhóm | Nút | Mục đích |
   |---|---|---|
   | Triggers | **API Trigger** | Kích hoạt cuộc gọi từ một yêu cầu API |
   | Agent Nodes | **Start Call** | Phần mở đầu cuộc gọi |
   | Agent Nodes | **Agent Node** | Một bước trong hội thoại |
   | Agent Nodes | **End Call** | Phần kết thúc cuộc gọi |
   | Global Nodes | **Global Node** | Chỉ dẫn áp dụng xuyên suốt cuộc gọi |
   | Integrations | **Webhook** | Gửi yêu cầu HTTP sau cuộc gọi |
   | Integrations | **QA Analysis** | Chấm chất lượng sau mỗi cuộc gọi |

3. Bấm **Save**.
4. Bấm nút phiên bản (ví dụ **v1**) để mở **Version History** và xem các phiên bản đã xuất bản.

[Chèn ảnh chụp màn hình: Builder]

#### Tạo trợ lý trống (Premium)

1. Mở thẻ **Tạo Trợ lý**.
2. Nhập **Tên trợ lý ảo mới**.
3. Bấm **Tạo Trợ lý & Mở Builder**. Builder mở ra với nút bắt đầu và kết thúc cơ bản để bạn tự thiết kế kịch bản.

#### Xóa trợ lý

Bấm nút xóa trên thẻ trợ lý (**Xóa trợ lý …**).

#### Quy tắc nghiệp vụ

- Sau khi tạo trợ lý, hãy gán trợ lý tại **Số tổng đài & Kênh → Inbound Agent** để trợ lý nhận cuộc gọi thực tế.
- Trước khi xóa một trợ lý, hãy chọn trợ lý inbound khác cho các kênh trợ lý đó đang phục vụ.

### 6.7.5 Tài liệu tri thức (Knowledge base)

#### Giới thiệu

**Tài liệu tri thức** chứa các tài liệu để trợ lý trả lời. Có ba kho, dùng chung cho voicebot, chatbot Facebook và Zalo, và khung chat Trợ lý AI.

| Kho | Nội dung |
|---|---|
| **Dịch vụ & giá** | Danh mục dịch vụ, bảng giá và các thay đổi về giá |
| **Thông tin công ty** | Giới thiệu, chi nhánh, liên hệ, giờ làm việc |
| **Đặt lịch & chính sách** | Quy trình đặt lịch, đổi lịch và các chính sách áp dụng |

Mỗi kho nhận tệp DOCX, TXT và MD, tối đa 20 MB.

[Chèn ảnh chụp màn hình: Tài liệu tri thức]

#### Cách sử dụng

1. Mở **Tài liệu tri thức** và tới kho cần cập nhật.
2. Bấm **Thay thế tài liệu** rồi chọn tệp.
3. Chờ tệp hiển thị **Sẵn sàng**.
4. Bấm **Áp dụng** ở tệp mới để đưa tệp vào sử dụng.
5. Hỏi một câu liên quan trong khung chat Trợ lý AI để kiểm tra câu trả lời.

Các thao tác khác trên tài liệu:

| Thao tác | Kết quả |
|---|---|
| **Xem** | Xem nội dung |
| **Tải** | Tải tệp về |
| **Xóa** | Xóa tệp đã tải lên và chưa đưa vào sử dụng |
| **Rollback** | Đưa kho về phiên bản trước |

#### Quy tắc nghiệp vụ

- Trợ lý trả lời dựa trên các tài liệu này và hồ sơ cơ sở. Khi kho trống, trợ lý báo với khách rằng thông tin chưa được cập nhật và đề nghị liên hệ trực tiếp.
- Mỗi kho nên giữ một chủ đề để câu trả lời chính xác.
- Loại bỏ dữ liệu cá nhân và ghi chú nội bộ khỏi tài liệu trước khi tải lên.

### 6.7.6 Quản lý khách hàng

#### Giới thiệu

**Danh sách bệnh nhân** là danh sách khách hàng. Khách hàng được thêm thủ công, nhập từ tệp, hoặc do trợ lý tạo trong hội thoại.

[Chèn ảnh chụp màn hình: Danh sách khách hàng]

| Cột | Ý nghĩa |
|---|---|
| **Họ và tên** | Họ tên |
| **Số điện thoại** | Số điện thoại, lưu theo định dạng quốc tế (ví dụ +84341657050) |
| **Email** | Email, nếu có |
| **Ghi chú** | Ghi chú, ví dụ nhu cầu khách nêu trong cuộc gọi |
| **Nguồn** | Nguồn, ví dụ **Trợ lý AI** khi trợ lý tạo bản ghi |
| **Thao tác** | **Sửa**, **Xóa** |

#### Thêm khách hàng

1. Bấm **Thêm khách hàng**.
2. Điền biểu mẫu **Thêm khách hàng mới**.
3. Bấm **Thêm mới**. Bấm **Hủy** để đóng mà không lưu.

| Trường | Bắt buộc | Mô tả | Ví dụ |
|---|---|---|---|
| **Số điện thoại** | Có | Số điện thoại | 0901234567 hoặc +84901234567 |
| **Tên bệnh nhân** | Có | Tên khách hàng | Nguyễn Văn A |
| **Email (tùy chọn)** | Không | Email | email@example.com |

#### Import khách hàng

1. Bấm **Import khách hàng**.
2. Bấm **Tải template mẫu (.csv)** để tải tệp mẫu và điền dữ liệu.
3. Chọn tệp CSV hoặc Excel (.xlsx).
4. Bấm **Bắt đầu import**.

#### Tìm, sửa, xóa

- Gõ vào **Tìm tên hoặc SĐT...** để tìm theo tên hoặc số điện thoại.
- Bấm **Sửa** để thay đổi thông tin, hoặc **Xóa** để xóa khách hàng.

#### Quy tắc nghiệp vụ

- Số điện thoại dùng để nhận diện khách hàng. Trợ lý tránh tạo bản ghi thứ hai cho cùng một số.
- Gói cước quy định quy mô danh sách khách hàng ([mục 6.6](#66-bảng-giá-và-ưu-đãi)).
- Khách hàng trong danh sách này là đối tượng của chiến dịch gọi đi ([mục 6.8.2](#682-chiến-dịch-gọi-đi)).

## 6.8 Cấu hình nâng cao

Nhóm **Cài đặt nâng cao** dành cho quản trị viên và yêu cầu **Premium**.

### Ở gói miễn phí

Mỗi mục có biểu tượng khóa. Khi mở, cổng hiển thị **Mở khoá tính năng …** kèm nút **Xem bảng giá & Nâng cấp** dẫn tới trang bảng giá ([mục 6.6](#66-bảng-giá-và-ưu-đãi)).

[Chèn ảnh chụp màn hình: Khóa Premium]

### Ở Premium

Bốn mục mở bình thường. Premium cũng cho phép tạo công cụ HTTP ([6.7.3](#673-công-cụ-tool-call)), tạo trợ lý trống ([6.7.4](#674-quản-lý-trợ-lý-ai-agent)) và outbound use cases ([6.7.2](#672-cấu-hình-tổng-đài-và-kênh-liên-lạc)).

### 6.8.1 Cấu hình mô hình AI

#### Giới thiệu

**Cấu hình mô hình AI** chọn dịch vụ AI mà các trợ lý của cơ sở sử dụng. Mỗi dịch vụ có thể theo mặc định của NuiTruc (**Dùng global**) hoặc dùng nhà cung cấp và API key riêng của cơ sở (**Cấu hình riêng**).

| Phần | Dịch vụ |
|---|---|
| **LLM — mô hình ngôn ngữ** | Mô hình ngôn ngữ hiểu và soạn câu trả lời |
| **STT — nhận dạng giọng nói** | Chuyển giọng nói thành văn bản |
| **TTS — tổng hợp giọng nói** | Chuyển văn bản thành giọng nói (giọng của trợ lý) |
| **Embedding — vector Knowledge Base** | Lập chỉ mục tài liệu tri thức để tra cứu |

Mỗi phần hiển thị **Đang áp dụng** cùng nhà cung cấp và mô hình đang có hiệu lực.

[Chèn ảnh chụp màn hình: Cấu hình mô hình AI]

#### Cách sử dụng

1. Mở **Cấu hình mô hình AI** và tới phần cần cấu hình.
2. Chọn **Provider**.
3. Nhập **Model**, hoặc để trống để dùng mặc định của nhà cung cấp.
4. Nhập **API key riêng** khi nhà cung cấp yêu cầu.
5. Với TTS, có thể đặt **Voice** và **Speed**. Với Embedding, có thể đặt **Base URL**.
6. Bấm **Lưu cấu hình riêng**. Nhãn đổi thành **Cấu hình riêng**.
7. Để trở về mặc định của NuiTruc, bấm **Chuyển về dùng global**.

#### Quy tắc nghiệp vụ

- Chỉ cấu hình riêng khi cơ sở có tài khoản hoặc API key riêng của nhà cung cấp. Các phần để global tự nhận thay đổi từ NuiTruc.
- API key đã lưu luôn được ẩn. Để trống ô này nếu muốn giữ key hiện tại.
- Thực hiện một cuộc gọi thử sau mỗi lần thay đổi ([mục 6.7.4](#674-quản-lý-trợ-lý-ai-agent)).

### 6.8.2 Chiến dịch gọi đi

#### Giới thiệu

**Chiến dịch gọi đi** (tiêu đề trang **Campaign outbound**) để trợ lý gọi tới một danh sách khách hàng, ví dụ nhắc lịch hẹn.

#### Chuẩn bị

- Kết nối đường dây điện thoại và thêm outbound use case ([mục 6.7.2](#672-cấu-hình-tổng-đài-và-kênh-liên-lạc)).
- Có khách hàng trong danh sách khách hàng ([mục 6.7.6](#676-quản-lý-khách-hàng)).

#### Cách sử dụng

1. Mở **Chiến dịch gọi đi**.
2. Ở **Tạo campaign**, điền biểu mẫu.
3. Bấm **Tạo campaign**. Chiến dịch xuất hiện trong danh sách bên dưới.
4. Trong danh sách, bấm **Start** để bắt đầu gọi. Dùng **Pause** khi đang chạy và **Resume** để tiếp tục.

| Trường | Bắt buộc | Mô tả |
|---|---|---|
| **Tên campaign** | Có | Tên chiến dịch |
| **Kênh** | Có | **Phone (SIP)**. **Zalo OA** và **WebRTC** được ghi **Sắp có**. |
| **Outbound use case** | Có | Use case đã khai báo tại **Số tổng đài & Kênh**; hiển thị trợ lý được dùng |
| **Khách hàng** | Có | Tìm và tích chọn khách hàng cần gọi |

| Cột | Ý nghĩa |
|---|---|
| **TÊN** | Tên chiến dịch |
| **KÊNH** | Kênh |
| **USE CASE** | Outbound use case |
| **STATUS** | Trạng thái chiến dịch |
| **PROGRESS** | Số cuộc hoàn thành, tổng số và số thất bại |
| **ACTIONS** | Start, Pause, Resume |

[Chèn ảnh chụp màn hình: Chiến dịch gọi đi]

#### Lưu ý

- Trang hiển thị **Chưa có outbound use case** hoặc **Chưa có khách hàng** kèm liên kết tới trang tạo mục còn thiếu.
- Cuộc gọi của chiến dịch xuất hiện trong **Lịch sử cuộc gọi** và được tính vào lưu lượng.

### 6.8.3 Nhân viên và phân quyền

#### Giới thiệu

**Nhân viên & Phân quyền** (tiêu đề trang **Người dùng**) là nơi quản trị viên tạo tài khoản nhân viên với vai trò **Nhân viên**.

#### Thêm nhân viên

1. Mở **Nhân viên & Phân quyền**.
2. Ở **Tạo Operator**, nhập **Email** và **Họ tên**.
3. Bấm **Tạo Operator**.
4. Cổng hiển thị email và mật khẩu tạm của tài khoản mới một lần duy nhất. Hãy sao chép và gửi cho nhân viên qua kênh an toàn.

#### Xem hoặc xóa nhân viên

Danh sách có các cột **EMAIL**, **ROLE** và **ACTIONS**. Quản trị viên hiển thị với vai trò `tenant_admin`. Xóa tài khoản nhân viên ngay tại dòng của tài khoản đó; sau khi xóa, tài khoản không đăng nhập được nữa.

[Chèn ảnh chụp màn hình: Danh sách nhân viên]

#### Quy tắc nghiệp vụ

- Tài khoản quản trị viên được tạo khi đăng ký. Tài khoản tạo tại trang này là nhân viên.
- Mỗi người dùng một tài khoản riêng.
- Xóa tài khoản khi nhân viên nghỉ việc.

### 6.8.4 Thông tin xác thực

#### Giới thiệu

**Thông tin xác thực hệ thống phòng khám** lưu API key và tài khoản mà công cụ, webhook riêng của cơ sở dùng để kết nối hệ thống bên ngoài.

Danh sách **Credential của cơ sở** hiển thị tên, loại và mô tả của từng credential. Secret được lưu an toàn và không hiển thị lại.

#### Thêm credential

1. Mở **Thông tin xác thực hệ thống phòng khám**.
2. Ở **Thêm credential**, điền biểu mẫu.
3. Bấm **Lưu credential**.

| Trường | Mô tả | Ví dụ |
|---|---|---|
| **Tên binding** | Tên credential | Dental Booking API |
| **Mô tả** | Mô tả | — |
| **Loại xác thực** | Loại; quyết định các trường còn lại | Xem bên dưới |

| Loại | Trường |
|---|---|
| **API Key** | Tên header (mặc định `X-API-Key`) và API key |
| **Bearer Token** | Token |
| **Basic Auth** | Tên đăng nhập và mật khẩu |
| **Custom Header** | Tên header và giá trị header |

#### Đổi hoặc xóa credential

- Bấm **Đổi secret**, nhập lại đầy đủ secret rồi lưu.
- Bấm **Xóa** và xác nhận trong hộp thoại.

[Chèn ảnh chụp màn hình: Thông tin xác thực]

#### Quy tắc nghiệp vụ

- Credential **NT Built-in API Credential** thuộc về các công cụ có sẵn của nền tảng. Hãy giữ nguyên credential này.
- Xóa một credential làm các công cụ phụ thuộc vào nó ngừng hoạt động.

---

# 7. Quản lý dữ liệu

## 7.1 Xem dữ liệu

Người dùng xem các bản ghi thuộc cơ sở của mình.

| Dữ liệu | Menu |
|---|---|
| Cuộc gọi, transcript, bản ghi âm | **Lịch sử cuộc gọi** |
| Hội thoại chat | **Lịch sử hội thoại** |
| Lịch hẹn | **Lịch hẹn ghi nhận** |
| Khách hàng | **Danh sách bệnh nhân** |
| Tài liệu tri thức | **Tài liệu tri thức** |

Để xem bản ghi:

1. Mở menu.
2. Dùng tìm kiếm hoặc lọc theo ngày khi cần.
3. Mở bản ghi bằng **Xem chi tiết**, **Xem audio & transcript** hoặc **Xem**.

## 7.2 Tạo dữ liệu

| Dữ liệu | Cách tạo | Mục |
|---|---|---|
| Lịch hẹn | **Tạo lịch hẹn** | [6.5](#65-quản-lý-lịch-hẹn) |
| Khách hàng | **Thêm khách hàng** hoặc import | [6.7.6](#676-quản-lý-khách-hàng) |
| Tài liệu tri thức | **Thay thế tài liệu** | [6.7.5](#675-tài-liệu-tri-thức-knowledge-base) |
| Trợ lý | Kịch bản mẫu hoặc **Tạo Trợ lý** | [6.7.4](#674-quản-lý-trợ-lý-ai-agent) |

Cuộc gọi, hội thoại và số liệu lưu lượng do hệ thống ghi nhận, không nhập thủ công.

## 7.3 Sửa dữ liệu

1. Tìm bản ghi.
2. Bấm **Sửa**.
3. Cập nhật thông tin.
4. Lưu.

Lịch hẹn, khách hàng và hồ sơ cơ sở sửa được. Cuộc gọi và hội thoại chỉ để xem.

## 7.4 Xóa dữ liệu

1. Tìm bản ghi.
2. Bấm **Xóa**.
3. Xác nhận khi cổng hỏi.

**Cảnh báo:** Cổng không có thùng rác. Hãy coi việc xóa là vĩnh viễn. Chính sách khôi phục và lưu trữ chưa được công bố cho môi trường phát triển.

## 7.5 Nhập và xuất dữ liệu

### Nhập (Import)

Khách hàng nhập được từ tệp **CSV** hoặc **Excel (.xlsx)**. Thực hiện theo [mục 6.7.6](#676-quản-lý-khách-hàng) và bắt đầu từ tệp mẫu tải về.

### Xuất (Export)

| Dữ liệu | Cách thực hiện |
|---|---|
| Bản ghi âm cuộc gọi | **Mở hoặc tải bản ghi âm** ở trang chi tiết cuộc gọi |
| Tài liệu tri thức | **Tải** bên cạnh tài liệu |
| Kịch bản chatbot | **Tải file Kịch bản (YAML)** ở thẻ Facebook & Zalo |

Cổng chưa có nút xuất danh sách cuộc gọi, hội thoại, lịch hẹn hoặc khách hàng. Hãy yêu cầu bộ phận hỗ trợ NuiTruc khi cần xuất hàng loạt.

---

# 8. Tách biệt dữ liệu và bảo mật

## 8.1 Tách biệt dữ liệu giữa các cơ sở

Mỗi cơ sở hoạt động trong vùng dữ liệu riêng. Người dùng của một cơ sở chỉ làm việc với dữ liệu của chính cơ sở đó:

- Cuộc gọi, transcript và bản ghi âm
- Hội thoại chat
- Lịch hẹn và khách hàng
- Tài liệu tri thức
- Trợ lý, công cụ và thông tin xác thực
- Cấu hình kênh và mô hình AI
- Số liệu lưu lượng

## 8.2 Kiểm soát truy cập

Quản trị viên cơ sở chịu trách nhiệm:

- Tạo tài khoản riêng cho từng nhân viên
- Xóa tài khoản khi nhân viên nghỉ việc
- Bảo vệ tài khoản quản trị viên
- Giới hạn người được nhận token kênh và API key

## 8.3 Bảo mật tài khoản

Khuyến nghị:

- Dùng mật khẩu mạnh và riêng biệt, dài hơn mức tối thiểu 6 ký tự.
- Mỗi người chỉ dùng tài khoản của mình.
- Bấm **Đăng xuất** khi dùng thiết bị chung.
- Lưu token và API key trong trình quản lý mật khẩu.
- Báo ngay cho NuiTruc khi thấy hoạt động bất thường.

Đăng nhập bằng email và mật khẩu. Trang đăng nhập chưa có xác thực nhiều lớp (MFA) hoặc đăng nhập một lần (SSO).

## 8.4 Quyền riêng tư dữ liệu

Hệ thống ghi nhận số điện thoại khách hàng, âm thanh cuộc gọi, transcript và tin nhắn chat. Cơ sở chịu trách nhiệm thông báo cho khách hàng của mình và xử lý dữ liệu này theo quy định pháp luật.

Chính sách quyền riêng tư, Thỏa thuận xử lý dữ liệu và Chính sách bảo mật chưa được công bố trên cổng. Hãy yêu cầu từ NuiTruc.

---

# 9. Thông báo và trạng thái hệ thống

## 9.1 Thông báo

Cổng hiển thị các thông báo trên màn hình:

| Thông báo | Ý nghĩa |
|---|---|
| **Chưa cấu hình Kênh tổng đài (SIP Trunk)** | Chưa kết nối đường dây điện thoại |
| Nhãn trạng thái ở **Kênh liên lạc** | Tình trạng từng kênh |
| **Sẵn sàng** ở tài liệu tri thức | Tài liệu đã xử lý xong |
| Khóa Premium | Tính năng yêu cầu nâng cấp |
| Khung mã ưu đãi | Ưu đãi đang kích hoạt và số ngày còn lại |

Thông báo hiển thị ngay trên từng trang; cổng chưa có trung tâm thông báo. Hãy theo dõi lịch hẹn và cuộc gọi mới ở trang tổng quan.

## 9.2 Trạng thái hệ thống

Trang trạng thái công khai chưa được công bố cho môi trường phát triển.

## 9.3 Bảo trì

Môi trường phát triển có thể thay đổi hoặc tạm ngừng mà không báo trước. Cách thông báo bảo trì cho môi trường chính thức sẽ do NuiTruc xác nhận.

---

# 10. Xử lý sự cố

## 10.1 Sự cố thường gặp

| Sự cố | Nguyên nhân có thể | Cách xử lý |
|---|---|---|
| Không đăng nhập được | Sai email hoặc mật khẩu | Kiểm tra lại; liên hệ hỗ trợ NuiTruc để đặt lại mật khẩu quản trị viên, hoặc quản trị viên với tài khoản nhân viên |
| Thiếu menu cài đặt | Đang đăng nhập với vai trò **Nhân viên** | Liên hệ quản trị viên |
| Menu có biểu tượng khóa | Tính năng yêu cầu Premium | Gửi yêu cầu nâng cấp tại **Bảng giá & Gói cước** |
| Trợ lý không nghe điện thoại | Chưa kết nối đường dây hoặc chưa chọn trợ lý inbound | Hoàn tất **Tổng đài Omni** và chọn **Inbound Agent** |
| Gọi thử không có tiếng | Trình duyệt chặn quyền micro | Cho phép micro với trang này rồi gọi lại |
| **Generate embed snippet** bị mờ | Chưa chọn trợ lý inbound ở thẻ WebRTC | Chọn **Inbound Agent** trước |
| Trợ lý báo thông tin chưa cập nhật | Kho tri thức trống hoặc tệp mới chưa áp dụng | Tải tài liệu lên và bấm **Áp dụng** |
| Trợ lý báo giá cũ | Đang dùng tài liệu cũ | Thay tài liệu ở **Dịch vụ & giá** và áp dụng |
| Tin nhắn Facebook hoặc Zalo không được trả lời | Webhook hoặc token thiếu, hết hạn | Kiểm tra lại webhook URL, verify token và các token; lưu lại |
| Cuộc gọi mãi ở **Đang xử lý** | Cuộc gọi đang được xử lý hoặc kết thúc bất thường | Chờ rồi tải lại; báo hỗ trợ nếu vẫn còn |
| Không tạo được chiến dịch | Chưa có outbound use case hoặc khách hàng | Thêm use case tại **Số tổng đài & Kênh** và thêm khách hàng |
| Tệp tải lên bị từ chối | Sai định dạng hoặc lớn hơn 20 MB | Dùng DOCX, TXT hoặc MD trong giới hạn 20 MB |
| Không tìm thấy bản ghi | Đang bật bộ lọc | Bấm **Xóa bộ lọc** |

## 10.2 Thông báo trên màn hình

Cổng dùng thông báo bằng chữ thay cho mã lỗi.

| Thông báo | Vị trí | Cách xử lý |
|---|---|---|
| **Chưa cấu hình Kênh tổng đài (SIP Trunk)** | Tổng quan | Kết nối đường dây ([6.7.2](#672-cấu-hình-tổng-đài-và-kênh-liên-lạc)) |
| **Voicebot telephony: Chưa xác minh trên Voicebot** | **Tổng đài Omni** | Lưu đúng thông tin kết nối; liên hệ hỗ trợ nếu vẫn còn |
| **Chọn Inbound Agent trước khi tạo embed.** | **WebRTC** | Chọn trợ lý inbound |
| **Tính năng … yêu cầu gói Premium** / **Mở khoá tính năng …** | Tính năng bị khóa | Nâng cấp ([6.6](#66-bảng-giá-và-ưu-đãi)) |
| **Chưa có outbound use case. Cấu hình tại Kênh liên lạc.** | Chiến dịch | Thêm outbound use case ([6.7.2](#672-cấu-hình-tổng-đài-và-kênh-liên-lạc)) |
| **Chưa có khách hàng.** | Chiến dịch | Thêm hoặc import khách hàng ([6.7.6](#676-quản-lý-khách-hàng)) |
| **Chưa có bệnh nhân nào trong danh sách.** | Khách hàng | Danh sách đang trống; thêm hoặc import |

## 10.3 Báo cáo sự cố

Khi báo cáo sự cố, hãy cung cấp:

- Tên cơ sở và email đăng nhập
- Menu hoặc tính năng
- Thời điểm xảy ra
- Thông báo hiển thị trên màn hình
- Các bước tái hiện
- Số cuộc gọi (ví dụ **Kết quả cuộc gọi #162**) hoặc số điện thoại khách hàng, nếu liên quan
- Ảnh chụp màn hình, nếu có

Không gửi mật khẩu, API key, access token hoặc dữ liệu nhạy cảm của khách hàng trong yêu cầu hỗ trợ.

---

# 11. Câu hỏi thường gặp (FAQ)

### Q1. Tôi có xem được dữ liệu của cơ sở khác không?

Không. Mỗi tài khoản làm việc trong cơ sở của mình.

### Q2. Một người dùng có thuộc nhiều cơ sở được không?

Mỗi tài khoản thuộc một cơ sở, và cổng không có bộ chuyển cơ sở. Hãy đăng ký mỗi cơ sở bằng một tài khoản riêng.

### Q3. Ai quản lý người dùng của cơ sở?

Quản trị viên, tại **Nhân viên & Phân quyền**, với Premium.

### Q4. Điều gì xảy ra khi xóa tài khoản nhân viên?

Tài khoản không đăng nhập được nữa.

### Q5. Tôi có xuất được dữ liệu của cơ sở không?

Tải được bản ghi âm, tài liệu tri thức và kịch bản chatbot. Với cuộc gọi, hội thoại, lịch hẹn và khách hàng theo lô, hãy liên hệ hỗ trợ NuiTruc.

### Q6. Làm sao để yêu cầu thêm tính năng hoặc hạn mức cao hơn?

Gửi yêu cầu nâng cấp tại **Bảng giá & Gói cước**, hoặc gọi hotline hiển thị ở trang đó.

### Q7. Tôi có thử trợ lý khi chưa có đường dây điện thoại được không?

Có. Dùng **Gọi thử (WebRTC)** để gọi thoại trên trình duyệt, hoặc khung chat Trợ lý AI để nhắn tin.

### Q8. Làm sao thay đổi nội dung trợ lý nói?

Cập nhật **Thông tin phòng khám** cho thông tin cơ bản, **Tài liệu tri thức** cho bảng giá và chính sách, và Builder cho luồng hội thoại.

### Q9. Cuộc gọi thử có tính vào hạn mức không?

Cuộc gọi thử được thống kê ở **Lưu lượng sử dụng**.

### Q10. Cổng hỗ trợ ngôn ngữ nào?

Giao diện bằng tiếng Việt. Builder chỉnh kịch bản trợ lý bằng tiếng Anh.

---

# 12. Hỗ trợ và liên hệ

## 12.1 Kênh hỗ trợ

| Kênh | Liên hệ |
|---|---|
| Hotline tư vấn | 1900 6868 (liên kết **Hotline tư vấn** ở trang bảng giá của môi trường phát triển) |
| Email hỗ trợ | [NuiTruc cung cấp] |
| Cổng hỗ trợ | [NuiTruc cung cấp] |
| Phụ trách khách hàng | [NuiTruc cung cấp] |

## 12.2 Thời gian hỗ trợ

[NuiTruc cung cấp]

## 12.3 Cam kết dịch vụ

Cam kết dịch vụ chưa được công bố cho môi trường phát triển. Gói **Enterprise** ghi SLA 99,9% và hỗ trợ kỹ thuật 24/7.

| Mức ưu tiên | Mô tả | Thời gian phản hồi |
|---|---|---|
| P1 – Nghiêm trọng | Hệ thống ngừng hoạt động hoặc ảnh hưởng lớn tới kinh doanh | [SLA] |
| P2 – Cao | Tính năng chính không dùng được | [SLA] |
| P3 – Trung bình | Lỗi một phần chức năng | [SLA] |
| P4 – Thấp | Câu hỏi chung hoặc lỗi nhỏ | [SLA] |

---

# Phụ lục A. Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Cơ sở (Tenant) | Không gian làm việc của một tổ chức trên nền tảng |
| Quản trị viên (Tenant Admin) | Người dùng sở hữu và cấu hình cơ sở |
| Nhân viên (Tenant User, Operator) | Tài khoản nhân viên do quản trị viên tạo |
| Trợ lý AI (Agent) | Kịch bản AI xử lý cuộc gọi hoặc tin nhắn |
| Voicebot | Trợ lý trên kênh thoại |
| Chatbot | Trợ lý trên kênh văn bản |
| Inbound / Outbound | Cuộc gọi đến từ khách / cuộc gọi đi tới khách |
| Builder | Trình chỉnh sửa kịch bản trợ lý dạng sơ đồ |
| Công cụ (Tool) | Hành động trợ lý gọi được, ví dụ tạo lịch hẹn |
| Tài liệu tri thức (Knowledge Base) | Tài liệu để trợ lý trả lời |
| RAG | Trả lời dựa trên tài liệu được truy xuất |
| LLM | Mô hình ngôn ngữ lớn |
| STT | Chuyển giọng nói thành văn bản |
| TTS | Chuyển văn bản thành giọng nói |
| Embedding | Chỉ mục số của tài liệu dùng để tra cứu |
| Token | Đơn vị văn bản mô hình ngôn ngữ xử lý |
| SIP Trunk | Kết nối giữa nhà cung cấp điện thoại và voicebot |
| WebRTC | Cuộc gọi thoại trên trình duyệt |
| Zalo OA | Zalo Official Account |
| Webhook | Địa chỉ nhận sự kiện từ hệ thống khác |
| Hạn mức (Quota) | Mức sử dụng hàng tháng của gói, tính bằng VNĐ |
| Freemium / Premium | Gói miễn phí / gói mở khóa cấu hình nâng cao |
| Use case (outbound) | Mục đích gọi đi được đặt tên và gắn với một trợ lý |

# Phụ lục B. Tài liệu tham khảo

- Mẫu hướng dẫn sử dụng: `user-guide-template.md`
- Bản tiếng Anh của tài liệu này: `user-guide.md`
- Ghi chú phát hành, Hướng dẫn quản trị, Tài liệu bảo mật và quyền riêng tư, Điều khoản dịch vụ: [NuiTruc cung cấp]

# Phụ lục C. Danh sách kiểm tra bắt đầu nhanh

- [ ] Đăng ký gói miễn phí, hoặc đăng nhập bằng tài khoản dùng thử
- [ ] Xem trang tổng quan
- [ ] Điền **Thông tin phòng khám**: giờ làm việc, dịch vụ, chi nhánh
- [ ] Tải tài liệu lên ba kho tri thức và áp dụng
- [ ] Hỏi thử vài câu trong khung chat Trợ lý AI
- [ ] Tạo trợ lý từ kịch bản mẫu
- [ ] Chạy **Gọi thử (WebRTC)** và đặt thử một lịch hẹn
- [ ] Kiểm tra cuộc gọi ở **Lịch sử cuộc gọi** và lịch hẹn ở **Lịch hẹn ghi nhận**
- [ ] Kết nối một kênh: đường dây điện thoại, Facebook, Zalo hoặc nút gọi trên website
- [ ] Chọn trợ lý inbound
- [ ] Xem **Lưu lượng sử dụng** và **Bảng giá & Gói cước**
- [ ] Với Premium: thêm nhân viên, thông tin xác thực, mô hình AI riêng và chiến dịch gọi đi
