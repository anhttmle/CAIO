---
name: update-backlog
description: >-
  Cập nhật specs/BACKLOG.md sau mỗi khi có thay đổi về trạng thái task
  (hoàn thành, bắt đầu, blocked, cancelled). Dùng khi user nói "cập nhật
  backlog", "update backlog", "đánh dấu task xong", hoặc sau khi agent
  thực thi xong một task SDD (cuối skill sdd-task-execute).
---

# Update Backlog

## Khi nào cần chạy skill này

- Sau khi hoàn thành một task SDD (cuối `sdd-task-execute`)
- Khi user yêu cầu đánh dấu task là `in_progress`, `done`, `blocked`,
  hoặc `cancelled`
- Khi bắt đầu làm một task mới (cập nhật sang `in_progress`)

---

## Bước 1: Đọc trạng thái hiện tại

Nếu `specs/BACKLOG.md` chưa tồn tại → tạo mới theo template ở Bước 2,
sau đó scan toàn bộ `specs/F*/tasks.md` để populate rows.

Nếu đã tồn tại → đọc file, tìm row cần cập nhật theo `Task ID`.

---

## Bước 2: Cấu trúc BACKLOG.md

```markdown
# Project Backlog

_Cập nhật lần cuối: YYYY-MM-DD_

## Legend

| Status        | Ký hiệu |
|---------------|---------|
| Not started   | ⬜      |
| In progress   | 🔄      |
| Done          | ✅      |
| Blocked       | 🚫      |
| Cancelled     | ❌      |

---

## F01 — Auth Service

| Task ID | Tên task                                    | Status | Updated    | Ghi chú |
|---------|---------------------------------------------|--------|------------|---------|
| F01-1.1 | Scaffold project structure + test runner    | ✅     | 2026-07-01 |         |
| F01-2.1 | SQLAlchemy models + Alembic migration       | ⬜     |            |         |

---

## F02 — API Gateway

| Task ID | Tên task                                    | Status | Updated    | Ghi chú |
|---------|---------------------------------------------|--------|------------|---------|
| F02-1.1 | Scaffold thư mục + test runner              | ⬜     |            |         |
```

**Quy tắc Task ID:** `F<số feature>-<section>.<subsection>`  
Ví dụ: task `2.1` của F01 → `F01-2.1`

---

## Bước 3: Cập nhật đúng row

1. Xác định `Task ID` từ task vừa thực hiện.
2. Tìm row tương ứng trong bảng feature đúng.
3. Thay ký hiệu status theo legend.
4. Ghi ngày hôm nay vào cột `Updated` (định dạng `YYYY-MM-DD`).
5. Ghi thêm vào `Ghi chú` nếu có lý do blocked/cancelled hoặc note đặc biệt.
6. Cập nhật dòng `_Cập nhật lần cuối:_` ở đầu file.

**Chỉ sửa row của task được chỉ định — không thay đổi row khác.**

---

## Bước 4: Nếu task chưa có trong BACKLOG.md

Thêm row mới vào đúng bảng feature, theo thứ tự `Task ID` tăng dần.  
Tên task lấy từ tiêu đề `### X.Y` trong `specs/<feature>/tasks.md`.

---

## Quy tắc tuyệt đối

- Không thay đổi status của task khác ngoài task được yêu cầu.
- Không xoá row đã có — chỉ đổi status sang `❌` nếu cancelled.
- Giữ đúng format bảng Markdown (căn cột bằng space nếu cần).
