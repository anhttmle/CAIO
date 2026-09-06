# Các phương pháp phát triển phần mềm

| Nhóm Phân Loại | Ký Hiệu | Tên Tiếng Anh | Tên Tiếng Việt | Trọng Tâm Cốt Lõi |
|---|---|---|---|---|
| Kiểm thử & Chất lượng | TDD | Test-Driven Development | Phát triển hướng kiểm thử | Viết mã kiểm thử tự động trước khi viết code chính. |
| | BDD | Behavior-Driven Development | Phát triển hướng hành vi | Viết kịch bản kiểm thử bằng ngôn ngữ tự nhiên (Given-When-Then). |
| | ATDD | Acceptance Test-Driven Development | Phát triển hướng kiểm thử chấp nhận | Toàn đội (Dev, QA, BA) cùng thống nhất tiêu chí nghiệm thu trước khi code. |
| Thiết kế & Nghiệp vụ | DDD | Domain-Driven Design | Thiết kế hướng miền nghiệp vụ | Lấy logic nghiệp vụ cốt lõi của doanh nghiệp làm trung tâm kiến trúc. |
| | SDD | Specification-Driven Development | Phát triển hướng đặc tả | Dựa trên tài liệu đặc tả kỹ thuật chi tiết làm nguồn chân lý để sinh mã. |
| | MDD | Model-Driven Development | Phát triển hướng mô hình | Thiết kế mô hình trực quan (UML) trước, sau đó tự động sinh mã nguồn. |
| Kiến trúc dữ liệu & Luồng đi | EDD | Event-Driven Development | Phát triển hướng sự kiện | Xây dựng hệ thống giao tiếp bằng cách phát và nhận các sự kiện theo thời gian thực. |
| | DDD (Data) | Data-Driven Development | Phát triển hướng dữ liệu | Thiết kế hệ thống và đưa ra quyết định dựa trên việc phân tích dữ liệu luân chuyển. |
| Giao diện & Trải nghiệm | CDD | Component-Driven Development | Phát triển hướng thành phần | Xây dựng giao diện (UI) từ các mảnh nhỏ độc lập (Component) rồi ghép lại. |
| | UXDD | User Experience-Driven Development | Phát triển hướng trải nghiệm | Đặt hành vi và sự hài lòng của người dùng làm thước đo tính năng. |
| Quản lý & Vận hành | FDD | Feature-Driven Development | Phát triển hướng tính năng | Mô hình Agile chia nhỏ dự án thành danh sách các tính năng cần hoàn thành ngắn hạn. |
| | GitOps | Git-Driven Operations | Vận hành hướng Git | Dùng kho lưu trữ Git làm trung tâm để tự động hóa hạ tầng và triển khai (CI/CD). |

# Ví dụ kết hợp
Khi kết hợp DDD, BDD và TDD, chúng tạo thành một kiềng ba chân hoàn hảo cho các dự án lớn: DDD định hình kiến trúc lớn, BDD làm rõ yêu cầu nghiệp vụ giữa các phòng ban, và TDD đảm bảo mã nguồn chạy chính xác ở mức chi tiết.
Dưới đây là cách bộ ba này phối hợp nhịp nhàng theo từng lớp quy trình từ vĩ mô đến vi mĩ:
------------------------------
## 1. Luồng phối hợp 3 bước (Vòng lặp kép - Double Loop)
Sự kết hợp này thường được vận hành theo mô hình "Vòng lặp bên ngoài" (BDD) bọc lấy "Vòng lặp bên trong" (TDD), tất cả đều dựa trên khung xương là ngôn ngữ chung của miền nghiệp vụ (DDD).

[DDD: Xác định Bounded Context & Nghiệp vụ cốt lõi]
                       │
                       ▼
 ┌────────────────────────────────────────────────────────┐
 │ VÒNG LẶP NGOÀI - BDD (Giao tiếp & Nghiệm thu)          │
 │  1. Viết kịch bản tính năng (Given/When/Then)          │
 │                                                        │
 │   ┌────────────────────────────────────────────────┐   │
 │   │ VÒNG LẶP TRONG - TDD (Lập trình chi tiết)       │   │
 │   │  2. Viết Unit Test cho các Domain logic        │   │
 │   │  3. Viết Code chính để pass test               │   │
 │   │  4. Refactor (Tối ưu hóa mã nguồn)            │   │
 │   └────────────────────────────────────────────────┘   │
 │                                                        │
 │  5. Chạy lại kịch bản BDD -> Đạt yêu cầu (Xanh)       │
 └────────────────────────────────────────────────────────┘

------------------------------
## 2. Sự phân bổ vị trí trong kiến trúc dự án lớn
Trong một dự án lớn áp dụng kiến trúc Hexagonal (Ports & Adapters) hoặc Clean Architecture, bộ ba này được phân bổ vào các lớp như sau:

| Phương pháp | Lớp Kiến trúc áp dụng | Ai tham gia? | Mục tiêu thực hiện |
|---|---|---|---|
| DDD | Domain Layer & Application Layer | BA, Dev, Domain Expert (Chuyên gia nghiệp vụ) | Định nghĩa các khái niệm, thực thể (Entities), Value Objects, và quy tắc kinh doanh (Business Rules). |
| BDD | Acceptance/API Layer (Vòng ngoài) | Product Owner, QA, Dev | Kiểm thử luồng đi của một tính năng từ góc nhìn người dùng (End-to-End hoặc Integration Test). |
| TDD | Domain & Infrastructure Layer (Vòng trong) | Lập trình viên (Developers) | Kiểm thử chi tiết các hàm tính toán logic, các thuật toán xử lý dữ liệu phức tạp (Unit Test). |

------------------------------
## 3. Ví dụ thực tế: Tính năng "Chuyển tiền" trong hệ thống Ngân hàng
Hãy xem cách ba phương pháp này cùng giải quyết một bài toán:
## Bước 1: Áp dụng DDD để định hình ngôn ngữ và mô hình
Đội ngũ phát triển ngồi lại với chuyên gia tài chính để thống nhất Ubiquitous Language (Ngôn ngữ chung).

* Họ xác định Tài khoản (Account) là một Aggregate Root, Số dư (Balance) là một Value Object.
* Quy tắc nghiệp vụ: "Không được chuyển tiền nếu số dư khả dụng nhỏ hơn số tiền chuyển kèm phí".

## Bước 2: Áp dụng BDD để viết kịch bản nghiệm thu (Vòng lặp ngoài)
QA và BA viết kịch bản bằng ngôn ngữ tự nhiên (Gherkin) dựa trên mô hình DDD đã thống nhất:

Feature: Chuyển tiền giữa các tài khoản ngân hàng

  Scenario: Chuyển tiền thành công khi đủ số dư
    Given Tài khoản nguồn có số dư là 1,000,000 VND
    And Tài khoản đích có số dư là 0 VND
    When Người dùng chuyển 200,000 VND sang tài khoản đích
    Then Tài khoản nguồn phải còn lại 800,000 VND
    And Tài khoản đích phải có 200,000 VND

Lúc này, chạy kiểm thử BDD này chắc chắn sẽ Thất bại (Đỏ) vì chưa có code.
## Bước 3: Áp dụng TDD để xây dựng logic chi tiết (Vòng lặp trong)
Để kịch bản BDD ở trên chạy đúng, lập trình viên xuống lớp Domain và viết mã theo TDD:

   1. Viết Test trước: Viết một hàm Unit Test kiểm tra xem phương thức Account.deduct(Amount) có trừ tiền chính xác không. (Kết quả: Đỏ vì chưa viết hàm trừ tiền).
   2. Viết Code: Viết logic tối thiểu cho phương thức deduct để Unit Test chuyển sang Xanh.
   3. Refactor: Tối ưu hóa code của hàm (ví dụ: tách logic kiểm tra số dư âm ra một class riêng).

## Bước 4: Hoàn tất vòng lặp kép
Khi tất cả các Unit Test nhỏ được viết bằng TDD đều chạy thành công, lập trình viên chạy lại kịch bản BDD lớn ở Bước 2. Kịch bản BDD chuyển sang màu Xanh. Tính năng chính thức hoàn thành và đảm bảo đúng 100% nghiệp vụ của doanh nghiệp.
------------------------------
## 4. Lợi ích lớn nhất khi kết hợp bộ ba này

* Tránh hiểu lầm yêu cầu: BDD dịch từ ngôn ngữ của khách hàng sang mã nguồn thông qua bộ từ vựng định nghĩa bởi DDD.
* Mã nguồn không bị lỗi thời với nghiệp vụ: Khi quy tắc kinh doanh thay đổi, bạn sửa kịch bản BDD, hệ thống sẽ báo lỗi ngay những chỗ code cũ không còn đáp ứng nhờ có TDD.
* Hệ thống có tính module hóa cao: DDD giúp bạn chia nhỏ dự án thành các Microservices hoặc Bounded Contexts độc lập, giúp việc viết TDD/BDD không bị chồng chéo, phình to.

Để tiếp tục, bạn có muốn tìm hiểu về các thư viện/công cụ phổ biến hiện nay để triển khai bộ ba này (như Cucumber cho BDD, JUnit/Jest cho TDD) hay muốn xem một đoạn mã nguồn minh họa (Code Example) cụ thể cho luồng phối hợp trên không?

