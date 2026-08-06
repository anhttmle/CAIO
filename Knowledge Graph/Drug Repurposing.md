# Overview
Drug repurposing (tái sử dụng thuốc) là chiến lược tìm chỉ định điều trị mới cho các thuốc đã tồn tại, giúp rút ngắn thời gian, giảm chi phí và tận dụng dữ liệu an toàn sẵn có so với phát triển thuốc hoàn toàn mới. Hiện nay nó đã trở thành hướng nghiên cứu rất “computational”, nơi AI, knowledge graph và các phương pháp in silico đóng vai trò trung tâm trong sàng lọc ứng viên trước khi đưa sang in vitro, in vivo và thử nghiệm lâm sàng.

# Drug timeline

```mermaid

  graph LR
    silico["in Silico"] --> vitro["in Vitro"]
    vitro["in Vitro"] --> vivo["in Vivo"]

```
### In Silico (Trên máy tính)
- Là phương pháp dùng phần mềm và mô hình toán học
- Chạy mô phỏng trên máy tính
- Giúp sàng lọc nhanh hàng triệu hợp chất hóa học
- Tiết kiệm chi phí và thời gian ở giai đoạn đầu

### In Vitro (Trong ống nghiệm)
- Là phương pháp nghiên cứu trong môi trường nhân tạo.
- Dùng ống nghiệm, đĩa nuôi cấy hoặc đĩa petri.
- Thử nghiệm trên tế bào, mô hoặc enzyme tách rời khỏi cơ thể.
- Dễ kiểm soát các yếu tố tác động nhưng thiếu bức tranh toàn diện của cơ thể.

### In Vivo (Trên cơ thể sống)
- Là phương pháp thử nghiệm trên toàn bộ sinh vật sống.
- Thường thực hiện trên động vật thí nghiệm hoặc con người.
- Phản ánh chính xác cách cơ thể sống phản ứng với thuốc hoặc tác nhân.
- Tốn kém, mất nhiều thời gian và vướng các vấn đề đạo đức nghiêm ngặt.

# Drug repurposing approaches

- **Blinded/phenotypic**: sàng lọc theo phenotype (ví dụ thay đổi hành vi tế bào, mô, hoặc động vật) mà không cần biết rõ cơ chế, thường dùng high‑throughput screening trên thư viện thuốc hiện có.
- **Target‑based**: yêu cầu thông tin cấu trúc 3D của target, cấu trúc hoá học của thuốc/ligand để thực hiện docking, screening cấu trúc và các phương pháp liên quan.
- **Knowledge‑based**: dựa trên drug–target, cấu trúc, ADR, label regulatory, dữ liệu pathway,… để trích luật, mô hình suy luận hoặc thiết kế scoring cho cặp thuốc–bệnh tiềm năng.
- **Signature‑based**: yêu cầu dữ liệu omics của bệnh và của thuốc (ví dụ profile biểu hiện gen khi dùng thuốc), từ đó so khớp hoặc tối ưu tiêu chuẩn “đảo chiều” profile bệnh.

# 
