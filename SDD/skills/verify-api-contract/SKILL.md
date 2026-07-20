---
name: verify-api-contract
description: >-
  Rà soát contract mismatch giữa Flutter service, Next.js và FastAPI backend schema
  trong dự án. Dùng khi user nói "verify contract", "check API mismatch",
  "kiểm tra client-BE", "tích hợp client backend", hoặc trước khi chạy thật
  sau khi implement một feature mới.
---

# Verify API Contract — Client ↔ Backend

## Context nhanh

Backend là **source of truth**. Flutter services nằm ở
`client/lib/features/*/data/`. Backend schemas nằm ở
`backend/app/schemas/`. Xem bảng đầy đủ ở `AGENT.md §7`.

## Workflow

### Bước 1: Xác định phạm vi

Feature nào cần verify? (F01–F11)  
Lấy danh sách endpoints từ `backend/app/routers/<feature>.py`.

### Bước 2: Đọc song song

| Đọc | File |
|-----|------|
| Backend schema | `backend/app/schemas/<feature>.py` |
| Backend router | `backend/app/routers/<feature>.py` |
| Flutter service | `client/lib/features/<feature>/data/<name>_service.dart` |

### Bước 3: Kiểm chứng contract giữa backend và client
- Client có gọi endpoint nào mà backend không có hoặc không đúng contract backend đang dùng không?

### Bước 4: Báo cáo

Liệt kê:
```
Feature | Service method | Gap | Cần sửa
```

Với mỗi gap: file cần sửa + dòng thay đổi cụ thể.

### Bước 5: Ghi decision log

Với mỗi gap đã sửa, thêm entry vào `specs/<feature>/decision_log.md`
theo format DL-FXX-N (xem `sdd-task-execute` skill).

## Tham chiếu nhanh

- Field names đúng: `AGENT.md §7` — bảng "Field name dễ nhầm"
- Response shapes: `AGENT.md §7` — bảng "Response shape quan trọng"
- Upload flow F05: `AGENT.md §7` — "Luồng upload ảnh"
- Decision logs đã có: `specs/f*/decision_log.md` (DL-F02-20, DL-F03-14, DL-F05-11, DL-F06-11, DL-F07-11, DL-F10-13)
