---
name: verify-spec
description: >-
  Rà soát spec của một feature để tìm mâu thuẫn, mismatch giữa các
  file (requirements.md, design.md, tasks.md, decision_log.md) và kiểm
  tra tính nhất quán của thuật ngữ (glossary). Dùng khi user nói
  "verify spec", "check spec", "kiểm tra spec", "mâu thuẫn spec",
  "thuật ngữ không nhất quán", "spec có mismatch không", hoặc trước
  khi bắt đầu implement một feature mới.
disable-model-invocation: true
---

# Verify Spec — Consistency & Terminology Check

## Mục tiêu

Phát hiện:
1. **Mâu thuẫn nội dung** — requirement A nói X, design nói Y cho cùng
   một behavior.
2. **Mismatch giữa tầng** — AC trong requirements không có task tương
   ứng; API trong design không xuất hiện trong tasks; endpoint trong
   tasks khác với design.
3. **Thuật ngữ không nhất quán** — cùng một khái niệm được gọi bằng
   nhiều tên khác nhau trong các file.

---

## Workflow

### Bước 1: Xác định phạm vi

Feature nào cần verify? (ví dụ: F01, F04…)

Đọc song song tất cả file spec của feature đó:

| File | Đọc để lấy |
|------|-----------|
| `specs/FXX-*/requirements.md` | AC, entities, role, constraint |
| `specs/FXX-*/design.md` | API endpoints, data model, flow |
| `specs/FXX-*/tasks.md` | task list, AC mapping, file target |
| `specs/FXX-*/decision_log.md` | quyết định đã có, tránh re-audit |

### Bước 2: Xây dựng bảng thuật ngữ

Từ 4 file trên, liệt kê tất cả **danh từ chuyên môn** (entity, role,
action, status, field name) xuất hiện ≥ 2 lần. Ghi vào bảng:

```
| Thuật ngữ | Dùng trong requirements | Dùng trong design | Dùng trong tasks |
```

Đánh dấu ô nào dùng thuật ngữ khác nhau cho cùng khái niệm (synonym
conflict).

### Bước 3: Cross-check AC ↔ Task

Với mỗi Acceptance Criterion (AC) trong `requirements.md`:
- Có ít nhất một task trong `tasks.md` cover AC đó không?
- Task đó có đúng AC label (ví dụ `[AC-1.1]`) không?

Với mỗi task trong `tasks.md`:
- Task reference AC nào? AC đó có tồn tại trong requirements không?

### Bước 4: Cross-check Design ↔ Tasks

Với mỗi API endpoint / data model trong `design.md`:
- Có task nào implement nó không?
- Field names trong schema design có khớp với field names trong task
  description không?

Với mỗi task implement một endpoint:
- Method + path có khớp với design không?
- Request/response schema có khớp không?

### Bước 5: Kiểm tra constraint & rule

Từ `requirements.md` (phần Constraints / Business Rules):
- Design có vi phạm constraint nào không?
- Tasks có bỏ sót constraint nào không?

### Bước 6: Báo cáo

Xuất kết quả theo cấu trúc:

```
## Verify Spec — FXX: <Feature Name>

### A. Thuật ngữ không nhất quán
| Khái niệm | Tên trong requirements | Tên trong design | Tên trong tasks | Gợi ý chuẩn hóa |
|-----------|----------------------|-----------------|----------------|-----------------|
| ...       | ...                   | ...              | ...             | ...             |

### B. AC không có task cover
| AC ID | Nội dung AC | Tình trạng |
|-------|-------------|-----------|
| ...   | ...         | Thiếu task |

### C. Task không khớp AC
| Task ID | AC tham chiếu | Vấn đề |
|---------|--------------|--------|
| ...     | ...           | AC không tồn tại |

### D. Design ↔ Tasks mismatch
| Endpoint / Model | Trong design | Trong tasks | Vấn đề |
|-----------------|-------------|------------|--------|
| ...             | ...          | ...         | Field name khác |

### E. Constraint bị bỏ sót
| Constraint | Nguồn | Thiếu ở đâu |
|-----------|-------|------------|
| ...       | ...   | ...         |

### Tóm tắt
- Số lỗi thuật ngữ: N
- Số AC không cover: N
- Số mismatch design-tasks: N
- Số constraint bỏ sót: N
- Đánh giá chung: [PASS | WARN | FAIL]
```

**PASS**: Không có lỗi.  
**WARN**: Có lỗi nhỏ (synonym, label) không ảnh hưởng logic.  
**FAIL**: Mâu thuẫn logic hoặc AC không có task cover.

### Bước 7: Gợi ý fix

Với mỗi issue được tìm thấy, đề xuất cụ thể:
- File nào cần sửa
- Dòng / section nào
- Sửa thành gì

**Không tự sửa file** trừ khi user xác nhận. Hỏi trước.

---

## Quy tắc

- Chỉ audit, không tự ý sửa spec trừ khi được yêu cầu.
- Nếu `decision_log.md` đã ghi nhận một quyết định gây ra sự khác
  biệt → đánh dấu là "intentional, documented" thay vì lỗi.
- Không gắn nhãn FAIL cho sự khác biệt đã có decision log cover.
