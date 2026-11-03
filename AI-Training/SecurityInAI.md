# 1. AI development lifecycle

```mermaid

  flowchart LR
  pd["Problem Definition"]
  dc["Data Collection"]
  dp["Data Preparation"]
  md["Model Development"]
  mt["Model Training"]
  me["Model Evaluation"]
  ds["Deployment & Serving"]
  mm["Monitoring & Maintenance"]

  pd --> dc
  dc --> dp
  dp --> md
  md --> mt
  mt --> me
  me --> ds
  ds --> mm

  mm --> pd
  mm --> dc
  mm --> dp
  mm --> md
  mm --> mt
  mm --> me
  mm --> ds

  ds --> pd
  ds --> dc
  ds --> dp
  ds --> md
  ds --> mt
  ds --> me

  me --> pd
  me --> dc
  me --> dp
  me --> md
  me --> mt

  mt --> pd
  mt --> dc
  mt --> dp
  mt --> md

  md --> pd
  md --> dc
  md --> dp

  dp --> pd
  dp --> dc

  dc --> pd

```

1. **Problem Definition**:	Xác định bài toán, mục tiêu, yêu cầu
2. **Data Collection**:	Thu thập dữ liệu từ các nguồn
3. **Data Preparation**:	Làm sạch, xử lý, labeling, validation
4. **Model Development**:	Chọn kiến trúc, xây dựng model
5. **Model Training**:	Huấn luyện và tối ưu model
6. **Model Evaluation**:	Đánh giá hiệu năng của model
7. **Deployment & Serving**:	Đóng gói và triển khai model
8. **Monitoring & Maintenance**:	Giám sát, phản hồi

# 2. Security in AI

# 3. Usecase: Data Poisoning
