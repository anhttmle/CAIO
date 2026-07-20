---
name: fix-bug
description: >-
  Xử lý bug theo workflow có kiểm tra spec và API contract trước khi sửa
  code. Dùng khi user báo bug, lỗi, fix bug, sửa lỗi, không hoạt động
  đúng, regression, hoặc hành vi sai so với yêu cầu.
---

# Fix Bug — Spec & Contract First

## Nguyên tắc

**Không sửa code cho đến khi hoàn thành Bước 1–3.**  
Mọi thay đổi phải truy vết được từ spec hoặc contract gap đã xác nhận.

---

## Bước 0: Thu thập triệu chứng

Ghi rõ trước khi điều tra:

```
- Triệu chứng user báo:
- Layer bị ảnh hưởng: [backend | admin_ui | user_app | gateway | nhiều layer]
- Feature liên quan (F01–F11):
- Steps tái hiện (nếu có):
- Expected vs Actual:
```

Nếu thiếu thông tin quan trọng → hỏi user trước khi sửa.

---

## Bước 1: Kiểm tra spec (bắt buộc)

Xác định feature từ triệu chứng, rồi đọc **song song**:

| File | Mục đích |
|------|----------|
| `specs/FXX-*/requirements.md` | AC, business rules, constraint |
| `specs/FXX-*/design.md` | API, schema, flow mong đợi |
| `specs/FXX-*/decision_log.md` | Quyết định đã ghi — tránh sửa sai hướng |

Trả lời 3 câu trước khi sang bước 2:

1. **Hành vi đúng theo spec là gì?** (trích dẫn section/AC cụ thể)
2. **Bug là implementation sai spec, hay spec thiếu/mâu thuẫn?**
3. **Decision log có entry nào liên quan không?**

### Phân loại

| Loại | Hành động |
|------|-----------|
| Implementation bug | Spec rõ → sửa code cho khớp spec |
| Contract mismatch | Spec rõ nhưng client/BE lệch → sửa layer sai contract |
| Spec gap / mâu thuẫn | **DỪNG** — hỏi user trước; không tự đoán |

Audit chi tiết spec (AC ↔ tasks ↔ design): dùng skill `verify-spec`.

---

## Bước 2: Kiểm tra API contract (bắt buộc nếu chạm API)

Chạy khi bug liên quan request/response, field name, status code,
hoặc hành vi giữa client ↔ backend.

**Backend là source of truth.**

| Layer | Path tham chiếu |
|-------|-----------------|
| Backend schema | `auth_service/app/schemas/` hoặc `onboarding_service/app/schemas/` |
| Backend router | `auth_service/app/routers/` hoặc `onboarding_service/app/routers/` |
| Admin UI client | `admin_ui/src/lib/api/` |
| Flutter client | `user_app/lib/` (feature data layer) |
| Gateway routes | `api_gateway/kong.yaml` |

Checklist nhanh:

- [ ] Method + path client gọi có tồn tại ở backend/gateway không?
- [ ] Request body field names & types khớp schema backend không?
- [ ] Response shape khớp type client parse không?
- [ ] Query params / pagination convention nhất quán không?
- [ ] Error status codes client xử lý có khớp backend trả không?

Audit chi tiết: dùng skill `verify-api-contract`.

Ghi gap tìm được:

```
| Field/Endpoint | Backend | Client | Gap |
```

---

## Bước 3: Xác nhận root cause & phạm vi fix

Tổng hợp từ Bước 1–2:

```
Root cause:
Layer cần sửa:
Files dự kiến:
Out of scope (không sửa):
```

**Chỉ proceed nếu:**
- Spec đã rõ expected behavior, HOẶC user đã xác nhận hướng sửa khi spec mơ hồ
- Contract gap đã xác định layer nào sai

---

## Bước 4: TDD — test tái hiện bug trước

1. Viết test **FAIL** mô tả đúng expected behavior từ spec
2. Chạy test → xác nhận fail đúng triệu chứng
3. Chỉ sau đó mới sửa implementation

| Layer | Test location |
|-------|---------------|
| auth_service | `auth_service/tests/` |
| onboarding_service | `onboarding_service/tests/` |
| admin_ui | `admin_ui/src/test/` |
| user_app | `user_app/test/` |

---

## Bước 5: Sửa bug (surgical)

- Confirm với người dùng trước khi sửa
- Chỉ sửa đủ để test PASS và khớp spec/contract
- Không refactor code lân cận
- Không thêm feature ngoài scope bug
- Match style hiện có của file

Nếu phát sinh design decision không có trong spec → ghi
`specs/FXX-*/decision_log.md`:

```markdown
## DL-F0X-N — <Tên quyết định>

**Date:** YYYY-MM-DD
**Context:** Bug gốc và tại sao cần quyết định này.
**Decision:** Đã chọn cách nào.
**Consequence:** Hệ quả, ai cần biết.
```

---

## Bước 6: Verify

- [ ] Test tái hiện bug PASS
- [ ] Test liên quan không regression
- [ ] Contract client ↔ backend khớp (re-check nếu đã sửa schema/API)
- [ ] Hành vi khớp AC/spec đã trích dẫn ở Bước 1

Chạy test phù hợp:

```bash
# Backend (ví dụ auth_service)
cd auth_service && make test

# Admin UI
cd admin_ui && npm test -- --run <test-file>
```

---

## Bước 7: Tóm tắt cho user

Trả lời ngắn gọn:

1. **Root cause** — bug do gì (implementation / contract / spec)
2. **Spec reference** — AC/section nào làm căn cứ
3. **Đã sửa gì** — file chính và thay đổi
4. **Test** — test nào cover, kết quả chạy
5. **Decision log** — có entry mới không

---

## Quy tắc tuyệt đối

- **KHÔNG** sửa code trước Bước 1–3
- **KHÔNG** sửa spec im lặng khi bug là spec gap — hỏi user
- **KHÔNG** fix client khi backend đúng spec mà không ghi nhận contract gap
- **KHÔNG** fix backend khi spec yêu cầu behavior client đang expect mà chưa có AC
- Mọi changed line phải trực tiếp từ root cause đã xác nhận

## Skills liên quan

- Audit spec: [verify-spec](../verify-spec/SKILL.md)
- Audit contract: [verify-api-contract](../verify-api-contract/SKILL.md)
- Decision log format: [sdd-task-execute](../sdd-task-execute/SKILL.md)
