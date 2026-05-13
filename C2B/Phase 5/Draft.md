# Phase 2 – Đặc tả chi tiết 3 tính năng cốt lõi
1. Diff nghiệp vụ (Business-Level Diff)  
2. Impact Analysis trên knowledge graph (Call Graph + Business Logic)  
3. Living Documentation trên graph (Docs-as-Code + Versioned Graph)

Bối cảnh: hệ thống đã có khả năng trích xuất **call graph** từ COBOL/RPG, dùng LLM để bóc tách các tầng nghiệp vụ, modules, luồng logic chi tiết, và lưu trữ chúng như một **knowledge graph của codebase**.

---

## 1. Diff nghiệp vụ, không chỉ diff code

### 1.1. Mục tiêu

- Cho dev/BA/QA thấy **PR/commit này thay đổi nghiệp vụ gì**, chứ không chỉ là thay đổi file/line thuần túy.[web:17][web:36]  
- Giúp review và phê duyệt thay đổi dựa trên **impact nghiệp vụ** (business impact), không chỉ dựa trên coding style hay diff text.[web:17]  

### 1.2. Phạm vi

Áp dụng cho:

- Các ngôn ngữ legacy (COBOL, RPG, PL/1, CL, SQL script batch, v.v.).  
- Các luồng nghiệp vụ đã được map từ phase 1:
  - Program → Business Function (ví dụ: “Tính lãi ngày”).
  - Call chain → Business Flow (ví dụ: “Luồng Debit Card Authorization”).
  - Business Rule (ví dụ: “Nếu customer VIP thì miễn phí duy trì”).

### 1.3. Mô hình dữ liệu liên quan

**Các entity chính trong knowledge graph (đã có từ phase 1):**[web:18][web:22][web:32]

- `ProgramNode`  
  - Thuộc tính: `id`, `name`, `language`, `path`, `type` (batch, on-line, utility, v.v.), `tags` (domain, module).  
- `CallEdge`  
  - `from_program_id`, `to_program_id`, `call_type` (static/dynamic), `via` (copybook, include, v.v.).  
- `BusinessFunction`  
  - `id`, `name`, `description`, `confidence`, `owned_programs` (list `ProgramNode`).  
- `BusinessFlow`  
  - `id`, `name`, `description`, `main_entry_program`, `path_nodes` (ordered list `ProgramNode`).  
- `BusinessRule`  
  - `id`, `name`, `description`, `condition`, `effect`, `attached_code_spans` (list {file, start_line, end_line}).  

**Đối tượng diff nghiệp vụ mới:**  

- `BusinessDiff`  
  - `id` (per commit/PR).  
  - `from_revision`, `to_revision`.  
  - `changed_business_functions`: list `BusinessFunctionChange`.  
  - `changed_business_flows`: list `BusinessFlowChange`.  
  - `changed_business_rules`: list `BusinessRuleChange`.  

Trong đó:

- `BusinessFunctionChange`:  
  - `function_id`  
  - `change_type`: `added` | `removed` | `modified`  
  - `before_summary`, `after_summary` (text do LLM sinh).  
- `BusinessFlowChange`:  
  - `flow_id`, `change_type`  
  - `before_path`, `after_path` (list program ids).  
  - `before_summary`, `after_summary`.  
- `BusinessRuleChange`:  
  - `rule_id`, `change_type`  
  - `before_condition/effect`, `after_condition/effect`.  

### 1.4. Luồng xử lý backend

**Trigger:** push commit, mở/udpate PR, hoặc chạy thủ công trong UI.

1. **Lấy diff code**  
   - Lấy danh sách file thay đổi, hunks, và commit range từ Git.  
2. **Xác định vùng code bị ảnh hưởng trong graph**  
   - Map các đoạn code thay đổi (file + line range) đến:
     - `ProgramNode` tương ứng.
     - `BusinessRule`/`BusinessFunction` đã gắn với các code span đó (từ phase 1).
3. **Re-parse subset + cập nhật graph mới (`G_new`)**  
   - Parse lại các `ProgramNode` bị chạm.  
   - Rebuild local subgraph (call edges liên quan).  
   - Chạy LLM lại trên các node/flow liên quan để:
     - Update mô tả `BusinessFunction`, `BusinessRule`, `BusinessFlow` khi cần.  
4. **So sánh graph cũ (`G_old`) và `G_new`**  
   - So sánh theo:
     - Program-level call graph (node/edge khác nhau).  
     - Mô tả BusinessFunction/BusinessFlow/BusinessRule (semantic diff).
5. **Sinh `BusinessDiff`**  
   - Lưu vào DB/graph DB.  
   - Attach `BusinessDiff` vào commit/PR.  

### 1.5. UX/Screen chính: Business Diff View (trong PR)

- **Header**:  
  - “Business Impact Summary”  
  - TL;DR 2–3 câu do LLM sinh, ví dụ:
    > “PR này thay đổi cách tính phí duy trì tài khoản cho khách hàng VIP, thêm bước kiểm tra trạng thái blacklist trước khi trừ phí.”  

- **Section 1 – Business Functions thay đổi**  
  - Bảng:
    - Function  
    - Type (Added/Removed/Modified)  
    - Summary trước → sau  
    - Confidence (mức tự tin của LLM)  

- **Section 2 – Business Flows thay đổi**  
  - Hiển thị sơ đồ flow cũ vs mới (Mermaid hoặc SVG) với highlighting node/edge mới/xóa.  
  - Tooltip cho mỗi node: tên program, short business description.  

- **Section 3 – Business Rules thay đổi**  
  - Diff “condition” và “effect” của rule ở dạng text, highlight phần đổi.  

---

## 2. Impact Analysis dựa trên knowledge graph

### 2.1. Mục tiêu

- Giúp dev/QA/BA trả lời: “Nếu merge commit này, **những chức năng/luồng nào có thể bị ảnh hưởng**?”
- Ưu tiên QA tập trung test vào các path có risk cao, dựa trên **call graph + data-flow + trọng số nghiệp vụ**.

### 2.2. Khái niệm core

- **Impact Region**: tập các node (program, rule, flow) có thể chịu ảnh hưởng nếu node bị thay đổi được merge.  
- **Impact Score** (0–100): ước lượng rủi ro, kết hợp:
  - Centrality trong graph (độ “hub”).
  - Số lượng business flows liên quan.  
  - Lịch sử bug hoặc incidents (nếu tích hợp được).  
  - Loại thay đổi (logic core vs thay đổi log/debug).  

### 2.3. Thuật toán (mức khung)

1. **Xác định seed nodes**  
   - Từ diff code → xác định các `ProgramNode` bị thay đổi (P_changed).  
   - Từ BusinessDiff → lấy `BusinessFunction`/`BusinessRule` thay đổi (B_changed).  

2. **Forward impact (call graph)**  
   - Từ mỗi node trong P_changed:
     - Chạy BFS/DFS theo call graph để tìm tất cả programs downstream (reachable).  
   - Gắn nhãn “directly impacted” vs “transitively impacted” theo độ sâu.

3. **Impact lên business flows**  
   - Với mỗi `BusinessFlow`:
     - Nếu path của flow chứa node thuộc `impact region` → flow bị impact.  
   - Ánh xạ flows này sang business capability / product feature (nếu có).  

4. **Tính Impact Score**  
   Với mỗi entity E trong impact region:

   - `centrality_score(E)` – đo bằng degree / betweenness / hub scores trong graph.[web:36][web:39]  
   - `flow_coverage(E)` – số lượng business flow có E.  
   - `historical_risk(E)` – số lượng bug/incidents gắn với E (nếu tích hợp được bug tracker).  
   - `change_intensity(E)` – độ lớn diff (lines changed, loại thay đổi).  

   Kết hợp đơn giản (có thể tinh chỉnh sau):

   \[
   ImpactScore(E) = w_c \cdot centrality + w_f \cdot flow\_coverage + w_h \cdot historical\_risk + w_i \cdot change\_intensity
   \]

   (Các hệ số w được cấu hình per project.)

5. **Tạo Impact Report**  
   - Top-N flows có risk cao.  
   - Top-N programs/business functions “hotspot”.  
   - Gợi ý test scope/regression suite tương ứng.  

### 2.4. API gợi ý

- `GET /impact?from=<rev1>&to=<rev2>`  
  - Trả về:
    - `impacted_programs`: list {id, name, impact_score, depth}.  
    - `impacted_flows`: list {id, name, impact_score}.  
    - `impacted_business_rules`: list {id, name, impact_score}.  

- `GET /impact/flow/<flow_id>?rev=<rev>`  
  - Chi tiết impact cho 1 flow cụ thể: node nào trong flow bị ảnh hưởng, gợi ý test.  

### 2.5. UX/Screen: Impact Analysis Dashboard

- **Section 1 – Risk Summary**  
  - Overall risk score cho commit/PR (0–100).  
  - Tag: `low`, `medium`, `high` (tham số cấu hình).  

- **Section 2 – Impacted Business Flows**  
  - Bảng:
    - Flow  
    - Impact Score  
    - Các entry point (jobs, API, transactions) liên quan.  

- **Section 3 – Impacted Programs & Rules**  
  - Bảng:
    - Program / Rule  
    - Loại (core/batch/utility/rule)  
    - Impact Score  
    - Liên kết tới code + tài liệu.  

- **Section 4 – Suggested Regression Tests (optional)**  
  - Nếu có mapping test case ↔ flow, hiển thị danh sách test case nên chạy.  

---

## 3. Living Documentation trên graph

### 3.1. Mục tiêu

- Biến tài liệu từ “snapshot phase 1” thành **living documentation**: luôn phản ánh trạng thái code/graph hiện tại, và được version hóa cùng với code.
- Cho phép xem tài liệu theo **node** (program, flow, rule) và theo **timeline**, với trace đầy đủ “doc này được sinh từ commit nào, cập nhật bởi PR nào”.

### 3.2. Docs-as-Code: chiến lược lưu trữ

- Tài liệu được lưu ở dạng Markdown trong cùng repo (hoặc repo phụ nhưng vẫn dùng Git), theo mô hình **Docs-as-Code**.
- Ví dụ cấu trúc:

  ```text
  /docs/
    business-flows/
      flow-<id>.md
    business-functions/
      func-<id>.md
    business-rules/
      rule-<id>.md
    overview/
      architecture.md
      data-lineage.md
  ```

- Mỗi file gắn với 1 entity trong graph (`BusinessFlow`, `BusinessFunction`, `BusinessRule`) và chứa:
  - Metadata (YAML front-matter): id, revision, last-updated-commit, tags.  
  - Summary do LLM sinh (có thể edit tay).  
  - Sections: “Business Description”, “Technical Details”, “Known Risks”, “Related Artifacts”.

### 3.3. Pipeline cập nhật doc

**Trigger:** cùng với pipeline phân tích/diff.

1. **Phát hiện entity thay đổi**  
   - Dựa vào `BusinessDiff`.  

2. **Sinh doc patch (draft)**  
   - Dùng LLM sinh hoặc update nội dung Markdown tương ứng:
     - Cập nhật summary, diagrams (Mermaid), sections bị ảnh hưởng.  
   - Sinh ra patch file `.md` giống như code diff:
     - Có thể commit vào branch của PR hoặc mở PR phụ “doc update”.

3. **Review doc như review code**  
   - Dev/BA/architect review patch doc trong PR:
     - Chỉnh wording, bổ sung chi tiết nghiệp vụ.  
   - Sau khi merge PR, doc được cập nhật đồng bộ với code.  

4. **Index lại doc + graph**  
   - Cập nhật links:
     - Node graph ↔ doc path.  
     - Cho phép từ UI graph nhảy sang doc, và ngược lại.  

### 3.4. Nội dung 1 file doc mẫu (Business Flow)

Ví dụ: `docs/business-flows/flow-1234.md`

```markdown
***
id: flow-1234
name: Debit Card Authorization Flow
domain: Payments
last_updated_commit: abcd1234
tags:
  - debit-card
  - authorization
  - online
***

# Debit Card Authorization Flow

## 1. Business Description

Luồng này xử lý yêu cầu thanh toán bằng thẻ ghi nợ, bao gồm kiểm tra số dư,
hạn mức, trạng thái thẻ, và sinh yêu cầu ghi sổ tạm giữ số dư.

## 2. High-Level Steps

1. Nhận yêu cầu từ switch thẻ.
2. Xác thực thẻ và chủ thẻ.
3. Kiểm tra số dư khả dụng.
4. Tạo bản ghi tạm giữ (hold).
5. Phản hồi kết quả cho switch.

## 3. Technical Details

- Entry program: `DC_AUTH_MAIN`
- Main call path:
  - `DC_AUTH_MAIN` → `DC_CHECK_CARD` → `DC_CHECK_BALANCE` → `DC_CREATE_HOLD`
- Datastores:
  - `CARD_MASTER`, `ACCOUNT_BAL`, `CARD_HOLD`

## 4. Change History

- 2025-04-10 (commit abcd1234): Thêm bước kiểm tra blacklist trước khi kiểm tra số dư.
- 2025-02-01 (commit xyz789): Tách logic kiểm tra số dư ra program `DC_CHECK_BALANCE`.

## 5. Related Rules

- `rule-777-check-blacklist`
- `rule-888-limit-check`
```

Việc giữ doc dưới dạng Markdown, versioned bằng Git giúp mọi thay đổi về nghiệp vụ/luồng được trace giống như code.

### 3.5. UX/Screen: Living Doc View

**Entry points chính:**

- Từ **PR/Impact View** → click vào flow/function/rule → mở doc tương ứng.  
- Từ **Graph View** → click node → sidebar hiển thị doc summary + link “Open full doc”.

**Các phần trong UI:**

1. **Doc Summary Panel**
   - Hiển thị metadata, summary, high-level steps.  
2. **Graph-Linked Sections**
   - Phần “Technical Details” hiển thị call path / data-flow được embed diagram (render từ graph).  
3. **Change History Timeline**
   - Timeline các commits/PR đã chạm vào entity này, kèm link trực tiếp đến PR.  
4. **Edit / Propose Changes**
   - Nút “Edit in Git” hoặc “Open in IDE” để sửa doc (docs-as-code flow).  

---

## Gợi ý bước tiếp theo

- Xây 1 POC nhỏ chỉ cho **1–2 Business Flow quan trọng**, implement trọn vẹn:
  - Business Diff + Impact Analysis + Doc markdown sống trên graph backend.  
- Sau đó generalize:
  - Chuẩn hóa schema graph, response JSON, và conventions naming doc file.  

Nếu bạn muốn, tôi có thể tiếp tục chi tiết hóa theo hướng “design docs” cho backend (schema, index, mô hình graph DB cụ thể) hoặc “UX spec” với wireframe cho 3 màn hình: PR view, Impact dashboard, Living doc viewer.
