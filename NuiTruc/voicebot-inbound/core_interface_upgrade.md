# Plan: Shared Resources & Super User Templates

> **Ngày tạo:** 2026-08-09  
> **Nguồn tham chiếu API hiện tại:** [`API_REFERENCE.md`](API_REFERENCE.md)

## Quyết định đã chốt (từ stakeholder)

| # | Chủ đề | Lựa chọn |
|---|--------|----------|
| 1 | Copy template | **Snapshot + version pinning** — tenant copy workflow definition; mọi dependency global (tool/KB/credential/variable) được **pin theo version tại thời điểm copy** (xem §3.0). *(Cập nhật so với bản đầu: không phải "luôn theo latest" mà là "pin theo version".)* |
| 2 | AI resource | **Super User quản lý global mặc định; tenant có thể override** — nếu tenant tự nhập API key riêng, config đó **ưu tiên hơn** global config (giữ nguyên hành vi override hiện tại của `PUT /user/configurations/user`). *(Cập nhật so với bản đầu: ban đầu chốt "tenant không override" — nay đảo lại theo yêu cầu mới nhất.)* |
| 3 | Visibility | **`scope` enum:** `organization` \| `global` |
| 4 | Output | File plan tại root repo |
| 5 | Lifecycle global resource | **Versioning + soft-delete:** Super User sửa → tạo version mới, version cũ vẫn tồn tại cho các workflow đã pin; Super User xóa → soft-delete, **chặn tenant mới copy/reference** kể từ thời điểm xóa, nhưng **không** phá vỡ workflow đã pin version cũ |
| 6 | Trigger khi copy | **Auto-enable** — copy template có node `trigger` sẽ tự động sync + kích hoạt `agent_triggers` cho org tenant, không cần bước bật thủ công |
| 7 | Workflow template model | **Gộp vào `WorkflowModel`** với flag `is_template=true` (+ `scope=global`); tái dùng `workflow_definitions`/`is_current` sẵn có làm cơ chế versioning cho template |
| 8 | `POST /workflow/create/template` (MPS) | **Giữ nguyên** — tenant vẫn tự tạo workflow riêng bằng mô tả ngôn ngữ tự nhiên, độc lập với catalog template global |
| 9 | Unique constraint tên resource | **Unique theo scope:** `(scope=organization, organization_id, name)` và `(scope=global, name)` là hai không gian tên độc lập |
| 10 | Extraction variables | **Promote thành shared variable resource** (`/variables`, `scope=global \| organization`) — node chỉ lưu reference (`variable_key` + `variable_scope`), không còn inline `{name, type, prompt}` |
| 11 | Draft vs Published (global resource) | **Tenant chỉ thấy/reference version đã `published`.** Version mới tạo (do sửa) là **draft**, chỉ Super User nhìn thấy trong trang quản trị; phải publish rõ ràng mới hiện trong catalog tenant và cho phép tạo reference mới |

---

## 1. Mục tiêu

### 1.1 Super User — workflow template + shared dependencies

Super User có thể:

- Tạo/sửa/xóa **workflow template** (`scope=global`) kèm metadata (tên, mô tả, category).
- Tạo **global resources** dùng làm dependency của template: tool, knowledge base document, variable definition, **webhook credential** (và credential gắn HTTP tool).
- Publish template để mọi tenant **copy và dùng ngay** mà không cần tự tạo lại dependency.

### 1.2 AI resource dùng chung

- Toàn hệ thống dùng **một pool AI config mặc định** (LLM/TTS/STT/embeddings) do Super User quản lý.
- **Tenant vẫn có thể override:** nếu tenant tự nhập API key/model riêng qua `PUT /user/configurations/user`, config đó được **ưu tiên hơn** global default cho org đó (giữ hành vi hiện tại, không breaking change). Không nhập → fallback global config.
- Mỗi workflow run vẫn ghi **usage theo `organization_id`** (dograh tokens, duration, USD) — không đổi mô hình billing hiện tại ở [`/organizations/usage`](API_REFERENCE.md#8-organization-usage); response có thêm field cho biết run dùng `ai_config_source: "global" | "organization_override"`.

### 1.3 Tenant — private + public mix

- Tenant (org) vẫn tạo resource `scope=organization`: tool, KB, variable, credential, workflow riêng.
- Workflow của tenant có thể reference **cả hai**:
  - Global resources (read-only đối với tenant)
  - Organization resources (CRUD trong org)

---

## 2. Hiện trạng (gap so với yêu cầu)

| Khả năng | API / model hiện tại | Gap |
|----------|----------------------|-----|
| Workflow template | `GET /workflow/templates`, `POST /workflow/templates/duplicate` — bảng `workflow_templates`, **không có CRUD superuser**, không có `scope` | Cần superuser quản lý template global; duplicate cần resolve global deps |
| Tool | `/tools/*` — `ToolModel.organization_id` bắt buộc | Chưa có `scope=global`; list chỉ trả org tools |
| Knowledge Base | `/knowledge-base/*` — org-scoped | Chưa có global KB; search cần merge org + global |
| Variable | Không có API riêng — nằm trong `workflow.template_context_variables` và node `extraction_variables` | Cần **resource variable** có thể reference cross-workflow (global + org) |
| Credential | `/credentials/*` — org-scoped; ref từ webhook node + HTTP tool | **THIẾU** — cần `scope=global` cho webhook/tool template |
| AI config | `GET/PUT /user/configurations/user` — per user | Cần thêm **global config mặc định** do Super User quản lý; tenant vẫn giữ quyền override như hiện tại (không đổi contract `PUT`) |
| Superuser | 3 endpoint (impersonate, workflow-runs, comment) | Thiếu toàn bộ quản trị template + global resources + AI config |

### 2.1 Phân loại dependency workflow (rà soát codebase)

Workflow phụ thuộc tài nguyên ở **3 lớp**. Chỉ một số cần mô hình `scope=global` — phần còn lại copy inline hoặc là prerequisite per-tenant.

A (Share global)     → Tool, KB, Credential, Variable (kể cả extraction variable), AI config
                       Tenant copy → GIỮ reference + PIN version, dùng chung bản Super User

B (Copy inline)      → globalNode prompt, workflow_configurations, ...
                       Tenant copy → NHÚN NGUYÊN vào workflow mới

C (Per-tenant)       → Trigger, telephony, API keys, disposition mapping
                       Tenant copy → TẠO MỚI hoặc TỰ CẤU HÌNH

#### A. Cần share (`scope=global`) — **bổ sung vào plan**

| # | Dependency | Vị trí trong workflow | JSON / field | API hiện tại | Ghi chú |
|---|------------|----------------------|--------------|--------------|---------|
| 1 | **Tool** | Node `startCall`, `agentNode` | `nodes[].data.tool_uuids[]` | `/tools/*` | Đã có trong plan |
| 2 | **KB document** | Node `startCall`, `agentNode` | `nodes[].data.document_uuids[]` | `/knowledge-base/*` | Đã có trong plan |
| 3 | **Variable (template)** | Workflow record | `template_context_variables` | *(inline, chưa có API)* | Đã có trong plan (`/variables`) |
| 4 | **Credential** | Node `webhook` | `nodes[].data.credential_uuid` | `/credentials/*` | **THIẾU trong plan** — webhook auth tới bên thứ ba |
| 5 | **Credential (transitive)** | HTTP tool definition | `tools.definition.config.credential_uuid` | `/credentials/*` | **THIẾU** — global HTTP tool **bắt buộc** global credential |
| 6 | **AI config** | Runtime (không trong JSON) | — | `/user/configurations/user` | Đã có trong plan (`/superuser/ai-config`); tenant override vẫn ưu tiên |
| 7 | **Extraction variable (promoted)** | Node `agentNode`/`extraction` | `nodes[].data.extraction_variables[].variable_key` + `variable_scope` | *(mới)* `/variables` | **Quyết định mới:** không còn inline `{name,type,prompt}` — reference sang variable resource (global hoặc org) |

Cả 7 loại dependency ở bảng A đều thuộc nhóm **versioned + soft-delete** (xem §3.0) khi `scope=global`.

#### B. Copy inline cùng workflow — **không cần resource global riêng**

| Dependency | Vị trí | Hành vi khi tenant copy template |
|------------|--------|----------------------------------|
| `globalNode` prompt | `type: globalNode` + `add_global_prompt` | Copy nguyên cấu trúc graph |
| `workflow_configurations` | Field workflow | VAD, ambient noise, `max_call_duration`, `dictionary` — copy inline |
| `call_disposition_codes` | Field workflow | Copy inline (metadata lọc run trên UI) |
| Webhook URL / payload | `webhook` node | `endpoint_url`, `payload_template` copy inline; chỉ **credential** là ref ngoài |
| Edge conditions | `edges[].data` | Copy inline (không có UUID ref) |
| Built-in tools | Runtime | Calculator, timezone — hardcoded engine, không ref |

#### C. Per-tenant khi copy — **không share, tạo mới hoặc prerequisite**

| Dependency | Lý do | Hành vi đề xuất |
|------------|-------|-----------------|
| **API trigger** | `trigger_path` gắn `agent_triggers` + `POST /public/agent/{uuid}` theo org | **Regenerate** UUID mỗi lần copy (giữ `regenerate_trigger_uuids` hiện có); sync **và auto-enable** `agent_triggers` cho org tenant ngay sau copy — tenant không cần bật thủ công |
| **Telephony config** | Org-level (`/organizations/telephony-config`) | Tenant tự cấu hình trước khi gọi; template catalog ghi **prerequisite** |
| **Org API keys** | Auth cho public agent trigger | Tenant dùng API key org của mình — không share |
| **Disposition mapping** | `DISPOSITION_CODE_MAPPING` org config | Tenant tùy chọn map disposition; không block copy template |

#### D. Không liên quan template runtime — **out of scope**

| Dependency | Ghi chú |
|------------|---------|
| Nango integrations (`/integration/*`) | Chỉ campaign Google Sheet — không ref trong workflow definition |
| Service keys (`/user/service-keys`) | Chỉ MPS tạo workflow từ NL |
| Embed token (`/workflow/{id}/embed-token`) | Deploy widget — tách khỏi template deps |
| Campaign (`/campaign/*`) | FK `workflow_id` — link ngoài, không phải dep của definition |

#### Sơ đồ phân lớp

```
workflow_definition.nodes[].data
  ├── tool_uuids[]                     → global | organization  [SHARE, versioned]
  ├── document_uuids[]                 → global | organization  [SHARE, versioned]
  ├── credential_uuid                  → global | organization  [SHARE, versioned]
  ├── extraction_variables[].variable_key → global | organization [SHARE, versioned] ← promoted
  └── trigger_path                     → per-org regenerate + auto-enable [REGEN]

workflow record (ngoài definition)
  ├── template_context_variables → variable resource   [SHARE, versioned]
  ├── workflow_configurations    → inline             [COPY]
  └── call_disposition_codes     → inline             [COPY]

runtime (không trong JSON)
  ├── LLM/TTS/STT/embeddings → global AI config (tenant override cho phép) [SHARE]
  └── telephony                → org prerequisite      [PER-TENANT]
```

---

## 3. Mô hình dữ liệu (đề xuất)

### 3.0 Versioning & lifecycle cho global resource (mới)

Áp dụng cho **mọi resource `scope=global`** dùng làm dependency của workflow: Tool, KB document, Credential, Variable. (Workflow **template** dùng cơ chế riêng — xem cuối mục này.)

**Vấn đề (snapshot risk):** Super User sửa/xóa global tool/KB/credential/variable đang được nhiều tenant reference → có thể làm workflow tenant chạy sai/lỗi ngay lập tức nếu resolve theo "latest".

**Chính sách đã chốt:**

1. **Edit → version mới, không ghi đè.** Mỗi lần Super User sửa nội dung (tool definition, KB doc, credential secret/config, variable default) hệ thống tạo **version row mới** (`version` tăng dần), giữ nguyên version cũ trong DB. Resource chính (`ToolModel`, `CredentialModel`, ...) luôn trỏ `current_version` = version mới nhất (có thể là **draft**, xem mục 2).
2. **Draft vs Published — tenant chỉ thấy bản đã publish.** Version mới tạo mặc định là **draft** (`is_published=false`) — chỉ Super User thấy được trong trang quản trị (`GET /superuser/.../{id}` và `.../versions`). Super User phải gọi endpoint **publish** rõ ràng để version đó trở thành `published_version` — lúc đó mới:
   - Hiện trong catalog tenant (`GET /tools?scope=global`, `GET /knowledge-base/documents?scope=global`, `GET /credentials?scope=global`, `GET /variables?scope=global`).
   - Được phép **pin làm reference mới** khi tenant copy template hoặc gắn resource vào workflow.

   Resource chính có 2 con trỏ: `current_version` (bản mới nhất, có thể đang là draft Super User đang soạn) và `published_version` (bản tenant đang thấy/dùng — có thể khác `current_version` nếu Super User đang soạn draft tiếp theo mà chưa publish).
3. **Pin theo version tại thời điểm reference được tạo.** Khi workflow (definition JSON) reference một global resource — lúc tenant copy template, hoặc lúc tenant/superuser gắn resource vào node — hệ thống **ghi kèm `*_version`** (luôn là `published_version` tại thời điểm đó) vào bên cạnh `*_uuid`. Runtime luôn resolve theo version đã pin, **không tự nâng cấp lên latest/published mới**.
   → Vì vậy: "Tenant sử dụng dependency cũ vẫn chạy được" ngay cả sau khi Super User sửa/publish version mới — vì version cũ vẫn còn trong DB và được pin sẵn (dù version đó không còn là `published_version` hiện tại, workflow đã pin vẫn resolve trực tiếp theo version cụ thể, không qua "published" check).
4. **Delete → soft-delete, chỉ chặn reference MỚI.** Xóa global resource = set `is_deleted=true` (hoặc `deprecated_at`), **không xóa vật lý** version rows. Tương đương "unpublish + khóa vĩnh viễn": ẩn khỏi catalog, chặn tạo reference mới (`POST /workflow/templates/{id}/copy`, `PUT /workflow/{id}` reject nếu ref mới), nhưng reference **đã pin từ trước** tiếp tục resolve bình thường.
5. **Không có "restore" tự động** — nếu cần dùng lại, Super User tạo resource mới (out of scope: phase sau có thể thêm `undelete`).
6. **KB document re-process = re-embed toàn bộ.** Mỗi version mới của KB document re-embed **toàn bộ** nội dung (không chunk-level diff) — đơn giản, đánh đổi chi phí compute cho tài liệu lớn; có thể tối ưu sau nếu cần.
7. **Không có retention policy theo số lượng/thời gian.** Version history giữ **vô hạn** theo thời gian, **không tự xóa theo N version/N ngày**. Version/resource vật lý chỉ bị xóa khi **đồng thời**: (a) không còn workflow nào reference (`referencing_workflow_count == 0`), **và** (b) Super User chủ động xóa (hard delete, khác với soft-delete "chặn reference mới" ở mục 4). Cần job/cron đếm `referencing_workflow_count` để Super User biết resource nào an toàn để hard-delete.

**Data model (đề xuất chung):**

```
{Resource}Model (Tool / Credential / Variable / KnowledgeBaseDocument)
  + current_version: int (default 1)         — bản mới nhất, có thể là draft
  + published_version: int | null (default 1) — bản tenant đang thấy/reference; null nếu chưa từng publish
  + is_deleted: bool (default false)          — soft-delete: chặn reference mới
  + deprecated_at: datetime | null

{Resource}VersionModel (mới — 1 bảng version per resource type)
  id, resource_id (FK), version (int), snapshot (JSON), is_published (bool), published_at, created_at, created_by
  unique(resource_id, version)
```

**Hard delete (dọn dữ liệu):** Khác với soft-delete ở trên (chỉ ẩn/chặn ref mới, dữ liệu vẫn còn), **hard delete** xóa vật lý resource + toàn bộ version. Chỉ cho phép khi `referencing_workflow_count == 0` (không còn workflow nào — của bất kỳ tenant nào — reference tới bất kỳ version nào của resource) **và** do Super User chủ động thực hiện (không tự động theo thời gian/số lượng version). Cần một query/job tính `referencing_workflow_count` (scan `workflow_definitions.definition` theo `*_uuid`) để hiển thị cho Super User trước khi cho phép hard-delete.

Workflow definition reference mở rộng: `tool_uuid` + `tool_version`, `document_uuid` + `document_version`, `credential_uuid` + `credential_version`, `variable_key` + `variable_version` (xem JSON mẫu ở §3.2).

**Workflow template versioning (riêng):** Vì template = `WorkflowModel(is_template=true, scope=global)` (xem quyết định #7), template **tái dùng `workflow_definitions` + `is_current`** đã có sẵn trong codebase — mỗi lần Super User sửa definition template tạo một row `WorkflowDefinitionModel` mới, `is_current` chuyển sang bản mới, bản cũ vẫn giữ để xem lịch sử/rollback. Cơ chế **publish/unpublish** hiện có ở `POST /superuser/workflow-templates/{id}/publish` đóng vai trò tương đương "draft vs published" (mục 2) — template chưa publish không hiện trong `GET /workflow/templates` catalog tenant. Vì copy template là **snapshot toàn bộ JSON** (không phải reference), việc Super User sửa template sau đó **không ảnh hưởng** các bản đã copy — versioning ở đây chủ yếu phục vụ audit/rollback cho Super User, không phải cơ chế an toàn chính (cơ chế an toàn chính là pin-version ở dependency, mục 1–4 trên).

### 3.1 Field `scope` chung

Thêm enum `ResourceScope`: `organization` | `global`.

| Resource | `scope=global` | `scope=organization` |
|----------|----------------|---------------------|
| Tool | `organization_id = NULL`, có `current_version`/`is_deleted` | `organization_id` bắt buộc, không versioned |
| KB document | `organization_id = NULL`, có `current_version`/`is_deleted` | `organization_id` bắt buộc, không versioned |
| Variable | `organization_id = NULL`, có `current_version`/`is_deleted` | `organization_id` bắt buộc, không versioned |
| Credential | `organization_id = NULL`, có `current_version`/`is_deleted` | `organization_id` bắt buộc, không versioned |
| Workflow template | `WorkflowModel` với `is_template=true` + `scope=global` (không còn bảng `workflow_templates` riêng) | *(không áp dụng — template luôn global; tenant tự tạo workflow thường không set `is_template`)* |

**Quy tắc truy cập:**

- `global`: tenant **chỉ read** version đã **`published`** (catalog + tạo reference mới) — **draft không hiện với tenant**, chỉ Super User thấy trong trang quản trị. Workflow đã pin version cụ thể từ trước vẫn resolve được version đó dù nó không còn là bản `published` hiện tại (xem §3.0 mục 3). Chỉ `get_superuser` **write** (tạo version/draft, publish, soft-delete, hard-delete) — có versioning + soft-delete (§3.0).
- `organization`: chỉ user thuộc org **read/write** (giữ hành vi hiện tại, không versioned, không có khái niệm draft/published — tenant tự chịu trách nhiệm sửa resource của mình).

> **Lý do chỉ version resource `global`:** resource `organization` do chính tenant sở hữu và sửa, không có rủi ro "bên thứ ba sửa làm hỏng workflow của mình" — nên giữ đơn giản, không thêm version overhead.

### 3.2 Workflow dependency reference

Workflow definition (nodes) lưu reference dạng:

```json
{
  "tool_uuid": "abc-...",
  "tool_scope": "global",
  "tool_version": 3,
  "document_uuid": "doc-...",
  "document_scope": "global",
  "document_version": 1,
  "credential_uuid": "cred-...",
  "credential_scope": "global",
  "credential_version": 2,
  "variable_key": "customer_name",
  "variable_scope": "organization"
}
```

*(`*_version` chỉ áp dụng khi `*_scope == "global"` — resource `organization` không versioned nên không có field version.)*

**Validation rule:** Global HTTP tool (`scope=global`) chỉ được reference `credential_uuid` có `scope=global`.

Runtime resolve: `global` → lookup theo `(uuid, version)` đã pin, không filter org, không tự nâng version; `organization` → lookup theo `uuid`, filter `selected_organization_id`, luôn dùng bản mới nhất (không versioned).

### 3.3 Copy template (snapshot + version pin)

`POST /workflow/templates/{id}/copy` (tenant) — template ở đây là `WorkflowModel(is_template=true, scope=global)`:

1. Clone `workflow_definition` JSON (definition hiện hành, `is_current=true`) + các field inline: `workflow_configurations`, `call_disposition_codes`.
2. **Giữ nguyên UUID + pin `published_version` hiện tại** của mọi global dep: tool, KB document, credential, variable keys (ghi `*_version` vào node JSON — xem §3.2). Từ lúc này workflow tenant **không tự nâng version** dù Super User publish version mới sau đó.
3. **Regenerate** `trigger_path` trên mọi trigger node, sync `agent_triggers` cho org tenant, và **auto-enable** trigger (không cần tenant bật tay).
4. Tạo `WorkflowModel` mới thuộc org tenant (`is_template=false`), lưu `source_template_id` + `source_template_version` (definition id đã copy) để audit.
5. Validate trước khi copy: mọi global ref phải có `published_version` hợp lệ (không null) và `is_deleted=false` tại thời điểm copy; global tool → global credential hợp lệ. Nếu một dep chưa từng publish hoặc đã bị Super User xóa, block copy và trả lỗi `unresolved_dependencies[]`.

---

## 4. API — Thay đổi (existing)

### 4.1 Workflow (`/workflow`)

| Method | Path | Thay đổi |
|--------|------|----------|
| GET | `/workflow/templates` | Trở thành query `WorkflowModel WHERE is_template=true AND scope=global AND published=true` (bỏ bảng `workflow_templates` riêng); thêm filter `category`, `published_only`; response thêm `dependency_summary` (tool, KB, credential, variable refs + version + `prerequisites`: telephony) |
| POST | `/workflow/templates/duplicate` | **Đổi tên/alias** → `POST /workflow/templates/{template_id}/copy`; pin version cho global deps (§3.3); auto-enable trigger; response báo `unresolved_dependencies[]` nếu có dep đã `is_deleted` |
| POST | `/workflow/{workflow_id}/validate` | Validate thêm: ref **global mới** phải trỏ tới `published_version` hợp lệ và `is_deleted=false`; ref **đã pin từ trước** luôn hợp lệ dù version đó không còn `published` hoặc resource đã bị xóa; tenant không được sửa global resource qua workflow |
| GET | `/workflow/fetch/{workflow_id}` | Response workflow definition có thể chứa mixed-scope refs (kèm `*_version`) — thêm `resolved_dependencies` (optional, cho UI) |
| PUT | `/workflow/{workflow_id}` | Khi save definition: kiểm tra quyền trên từng ref (org ref phải thuộc org; global ref read-only); nếu thêm ref global mới → phải là `published_version` và chưa `is_deleted` |

**Không đổi:** `create/definition`, `create/template` (MPS — tenant vẫn tự tạo workflow bằng NL, độc lập catalog template global), runs, count, fetch list, summary, status.

**Migration:** Data cũ trong bảng `workflow_templates` được migrate 1 lần sang `workflows` (`is_template=true`, `scope=global`, definition đầu tiên trong `workflow_definitions`), sau đó bảng `workflow_templates` deprecate/drop.

### 4.2 Tools (`/tools`)

| Method | Path | Thay đổi |
|--------|------|----------|
| GET | `/tools/` | Query `scope` optional (`organization` \| `global` \| `all` default `all`); trả org tools + **chỉ global tool có `published_version`** (ẩn draft-only và `is_deleted`); global tools **read-only** với tenant |
| GET | `/tools/{tool_uuid}` | Cho phép đọc tool `scope=global` bởi mọi tenant — trả **`published_version`** (default: version đã pin trong workflow, hoặc `published_version` nếu xem catalog); tenant không truy vấn được draft |
| POST | `/tools/` | Tenant chỉ tạo `scope=organization` (mặc định); reject nếu client gửi `scope=global`; unique constraint theo `(organization_id, name)` |
| PUT | `/tools/{tool_uuid}` | Org tool: sửa trực tiếp (không version). Chặn tenant sửa `scope=global` (403) — superuser sửa global tool tạo version mới, không ghi đè (§3.0) |
| DELETE | `/tools/{tool_uuid}` | Org tool: xóa như hiện tại. Chặn tenant xóa `scope=global` (403) — superuser xóa global tool = soft-delete (`is_deleted=true`), chặn reference mới, không ảnh hưởng workflow đã pin |
| POST | `/tools/{tool_uuid}/unarchive` | Tương tự — chỉ org tools hoặc superuser với global |

### 4.3 Credentials (`/credentials`)

| Method | Path | Thay đổi |
|--------|------|----------|
| GET | `/credentials/` | Query `scope`; merge org credentials + **global chỉ những resource có `published_version`** (ẩn draft-only, `is_deleted`) |
| GET | `/credentials/{credential_uuid}` | Cho phép đọc credential `scope=global` — trả `published_version` (không trả secret của draft) |
| POST | `/credentials/` | Tenant chỉ tạo `scope=organization`; unique `(organization_id, name)`. Đổi unique constraint hiện có `unique_org_credential_name` → thêm nhánh `(scope=global, name)` cho superuser |
| PUT | `/credentials/{credential_uuid}` | Chặn tenant sửa `scope=global` (403) — superuser sửa global credential tạo version mới (secret mới không ghi đè version cũ) |
| DELETE | `/credentials/{credential_uuid}` | Chặn tenant xóa global credential (403) — superuser xóa = soft-delete, chặn reference mới |

**Runtime:** `api/tasks/run_integrations.py` (webhook node), `api/services/workflow/tools/custom_tool.py` (HTTP tool) — resolve credential theo scope.

### 4.4 Knowledge Base (`/knowledge-base`)

| Method | Path | Thay đổi |
|--------|------|----------|
| GET | `/knowledge-base/documents` | Query `scope`; merge org documents + **global chỉ resource có `published_version`** (ẩn draft-only, `is_deleted`) |
| GET | `/knowledge-base/documents/{document_uuid}` | Cho phép đọc document global — trả `published_version` |
| POST | `/knowledge-base/search` | Search trong **org documents + global documents đã published** (filter `scope` optional) |
| POST | `/knowledge-base/upload-url` | Tenant chỉ upload `scope=organization` |
| POST | `/knowledge-base/process-document` | Tenant chỉ process org docs; superuser re-upload/re-process global doc tạo version mới (chunk/embedding theo version) |
| DELETE | `/knowledge-base/documents/{document_uuid}` | Chặn tenant xóa global doc (403) — superuser xóa = soft-delete, chặn reference mới |

### 4.5 User (`/user`)

| Method | Path | Thay đổi |
|--------|------|----------|
| GET | `/user/configurations/user` | Trả field `source: "global" \| "organization_override"` cho biết config hiện tại đến từ đâu. Nếu tenant chưa tự nhập → trả **global AI config** (masked). Nếu tenant đã nhập riêng → trả config của tenant (override) |
| PUT | `/user/configurations/user` | **Giữ nguyên hành vi hiện tại** (không breaking change) — tenant vẫn có thể tự nhập LLM/TTS/STT/embeddings API key; nếu nhập → **override global default** cho org đó. Không nhập → tiếp tục dùng global default |
| GET | `/user/configurations/user/validate` | Validate theo config đang hiệu lực (override nếu có, else global) |
| GET | `/user/configurations/voices/{provider}` | Dùng global service key / MPS config nếu tenant chưa override |

**Không đổi:** `configurations/defaults`, `auth/user`, org API keys (`/user/api-keys/*`) — API keys ở đây là Dograh platform keys, khác AI provider keys.

### 4.6 Organization Usage (`/organizations/usage`)

| Method | Path | Thay đổi |
|--------|------|----------|
| GET | `/organizations/usage/current-period` | Không đổi contract — đảm bảo usage ghi nhận dù chạy trên global AI pool |
| GET | `/organizations/usage/runs` | Thêm field optional `ai_config_source: "global"` trên mỗi run (transparency) |
| GET | `/organizations/usage/daily-breakdown` | Không đổi contract |

### 4.7 Superuser (`/superuser`)

| Method | Path | Thay đổi |
|--------|------|----------|
| GET | `/superuser/workflow-runs` | Không đổi (có thể thêm filter `template_id` sau) |

**Giữ nguyên:** `impersonate`, `workflow-runs`, `comment`.

### 4.8 Các nhóm API **không thay đổi** (liên quan gián tiếp)

Campaign, Integration, LoopTalk, Organization (telephony-config), Reports, S3, Service Keys, Workflow Embed, Telephony, WebRTC, Public Agent/Download/Embed — **không đổi contract** trong phase 1.

> Credentials **có thay đổi** — xem [§4.3](#43-credentials-credentials).

> **Lưu ý:** Workflow run runtime (pipecat pipeline) cần đọc global AI config nội bộ — không nhất thiết expose endpoint mới cho tenant.

---

## 5. API — Thêm mới

### 5.1 Superuser — Workflow Templates

Prefix đề xuất: `/superuser/workflow-templates`. **Lưu ý:** template = `WorkflowModel(is_template=true, scope=global)`, các endpoint dưới đây là **lớp quản trị riêng cho template** (khác `/workflow` thông thường) để lọc theo `is_template=true` và thêm hành vi publish/version.

| Method | Path | Chức năng |
|--------|------|-----------|
| GET | `/superuser/workflow-templates` | Liệt kê `WorkflowModel WHERE is_template=true` (phân trang, filter published) |
| POST | `/superuser/workflow-templates` | Tạo `WorkflowModel(is_template=true, scope=global)` từ `workflow_definition` + metadata |
| GET | `/superuser/workflow-templates/{id}` | Chi tiết template + dependency manifest (tool/KB/credential/variable + version đang dùng) |
| PUT | `/superuser/workflow-templates/{id}` | Cập nhật definition/metadata → tạo `WorkflowDefinitionModel` mới, `is_current=true` (bản cũ giữ lại cho lịch sử) |
| DELETE | `/superuser/workflow-templates/{id}` | Xóa hoặc archive template (ẩn khỏi catalog; không ảnh hưởng workflow đã copy trước đó vì là snapshot) |
| POST | `/superuser/workflow-templates/{id}/publish` | Đánh dấu published (hiện cho tenant) |
| POST | `/superuser/workflow-templates/{id}/unpublish` | Ẩn khỏi catalog tenant |
| GET | `/superuser/workflow-templates/{id}/versions` | Liệt kê lịch sử definition (`workflow_definitions` của template, mới → cũ) |
| POST | `/superuser/workflow-templates/{id}/versions/{definition_id}/restore` | Rollback: set definition cũ thành `is_current=true` (tương đương tạo version mới với nội dung cũ) |

### 5.2 Superuser — Global Tools

Prefix: `/superuser/tools` *(hoặc `POST /tools/` với `scope=global` + `get_superuser` — chọn 1 pattern, đề xuất namespace riêng cho rõ ràng)*

| Method | Path | Chức năng |
|--------|------|-----------|
| GET | `/superuser/tools` | Liệt kê tools `scope=global` (thấy cả draft, khác `GET /tools` của tenant) |
| POST | `/superuser/tools` | Tạo global tool (`current_version=1`, mặc định **draft**, `published_version=null`) |
| GET | `/superuser/tools/{tool_uuid}` | Chi tiết — bao gồm cả draft `current_version` |
| PUT | `/superuser/tools/{tool_uuid}` | Cập nhật → tạo version mới **dạng draft** (`current_version += 1`), không ghi đè version cũ, không tự publish |
| POST | `/superuser/tools/{tool_uuid}/versions/{version}/publish` | Publish 1 version cụ thể → `published_version = version`; từ lúc này tenant thấy + có thể pin version này |
| POST | `/superuser/tools/{tool_uuid}/unpublish` | Gỡ khỏi catalog tenant (`published_version = null`) — không xóa data, chỉ ẩn cho reference mới; ref đã pin vẫn chạy |
| DELETE | `/superuser/tools/{tool_uuid}` | Soft-delete (`is_deleted=true`) — chặn reference mới, giữ nguyên version cho workflow đã pin |
| GET | `/superuser/tools/{tool_uuid}/versions` | Liệt kê lịch sử version (kèm trạng thái draft/published) |
| GET | `/superuser/tools/{tool_uuid}/referencing-workflows` | Đếm/liệt kê workflow đang reference (mọi version) — dùng để quyết định hard-delete |
| DELETE | `/superuser/tools/{tool_uuid}?hard=true` | **Hard delete** — chỉ cho phép khi `referencing_workflow_count == 0`; xóa vật lý resource + version history |
| POST | `/superuser/tools/{tool_uuid}/unarchive` | Khôi phục (`is_deleted=false`) |

### 5.3 Superuser — Global Knowledge Base

Prefix: `/superuser/knowledge-base`

| Method | Path | Chức năng |
|--------|------|-----------|
| POST | `/superuser/knowledge-base/upload-url` | Presigned URL upload doc global (tạo/thêm version **draft**) |
| POST | `/superuser/knowledge-base/process-document` | Trigger processing global doc — **re-embed toàn bộ**, kết quả là version draft mới |
| GET | `/superuser/knowledge-base/documents` | Liệt kê docs global (thấy cả draft) |
| GET | `/superuser/knowledge-base/documents/{uuid}` | Chi tiết — bao gồm draft `current_version` |
| POST | `/superuser/knowledge-base/documents/{uuid}/versions/{version}/publish` | Publish version → `published_version = version`, tenant thấy trong search/catalog |
| POST | `/superuser/knowledge-base/documents/{uuid}/unpublish` | Gỡ khỏi catalog/search tenant (`published_version = null`) |
| GET | `/superuser/knowledge-base/documents/{uuid}/versions` | Liệt kê lịch sử version (mỗi lần re-upload/re-process **re-embed toàn bộ** tài liệu — không chunk-diff; kèm trạng thái draft/published) |
| DELETE | `/superuser/knowledge-base/documents/{uuid}` | Soft-delete global doc — chặn reference mới, giữ version cho workflow đã pin |
| DELETE | `/superuser/knowledge-base/documents/{uuid}?hard=true` | **Hard delete** — chỉ khi `referencing_workflow_count == 0`; xóa vật lý doc + toàn bộ version/embeddings |
| POST | `/superuser/knowledge-base/search` | Search global KB (debug/preview) |

### 5.4 Superuser — Global Credentials

Prefix: `/superuser/credentials`

| Method | Path | Chức năng |
|--------|------|-----------|
| GET | `/superuser/credentials` | Liệt kê credentials `scope=global` |
| POST | `/superuser/credentials` | Tạo global credential (API key, Bearer, Basic Auth, custom header) |
| GET | `/superuser/credentials/{credential_uuid}` | Chi tiết (không trả secret) — bao gồm draft |
| PUT | `/superuser/credentials/{credential_uuid}` | Cập nhật → tạo version **draft** mới, secret cũ vẫn resolve được cho ref đã pin |
| POST | `/superuser/credentials/{credential_uuid}/versions/{version}/publish` | Publish version → tenant có thể pin từ giờ |
| POST | `/superuser/credentials/{credential_uuid}/unpublish` | Gỡ khỏi catalog tenant (`published_version = null`) |
| DELETE | `/superuser/credentials/{credential_uuid}` | Soft-delete — chặn reference mới |
| DELETE | `/superuser/credentials/{credential_uuid}?hard=true` | **Hard delete** — chỉ khi `referencing_workflow_count == 0`; xóa vật lý credential + version/secret history |
| GET | `/superuser/credentials/{credential_uuid}/versions` | Liệt kê lịch sử version (metadata, không trả secret) |

Dùng cho webhook node và `credential_uuid` trong global HTTP tools.

### 5.5 Variables (mới — cả superuser & tenant)

Prefix: `/variables`. Đây là resource **thay thế cho `extraction_variables` inline** (quyết định #10) — node workflow không còn lưu `{name, type, prompt}` trực tiếp mà reference `variable_key` + `variable_scope` (+ `variable_version` nếu global).

| Method | Path | Auth | Chức năng |
|--------|------|------|-----------|
| GET | `/variables` | `get_user` | Liệt kê variables `scope=organization` + **`scope=global` chỉ bản `published`** (ẩn draft, `is_deleted`) |
| POST | `/variables` | `get_user` | Tenant tạo `scope=organization`; unique `(organization_id, key)` |
| GET | `/variables/{key}` | `get_user` | Chi tiết (org: bản hiện tại; global: `published_version`) |
| PUT | `/variables/{key}` | `get_user` | Sửa org variable (không versioned) |
| DELETE | `/variables/{key}` | `get_user` | Xóa org variable |

Superuser mirror tại `/superuser/variables` (CRUD `scope=global`, có version + draft/published + soft-delete như §3.0, unique `(scope=global, key)`):

| Method | Path | Chức năng |
|--------|------|-----------|
| GET/POST | `/superuser/variables` | Liệt kê (kèm draft) / tạo global variable (mặc định draft) |
| PUT | `/superuser/variables/{key}` | Cập nhật → tạo version **draft** mới (VD: đổi `type`/`default_value`/prompt-hint cho extraction) |
| POST | `/superuser/variables/{key}/versions/{version}/publish` | Publish version → tenant thấy + có thể pin |
| POST | `/superuser/variables/{key}/unpublish` | Gỡ khỏi catalog tenant |
| DELETE | `/superuser/variables/{key}` | Soft-delete — chặn reference mới |
| DELETE | `/superuser/variables/{key}?hard=true` | **Hard delete** — chỉ khi `referencing_workflow_count == 0`; xóa vật lý variable + version history |
| GET | `/superuser/variables/{key}/versions` | Lịch sử version (kèm trạng thái draft/published) |

**Variable schema đề xuất:** `key`, `name`, `description`, `type` (string/number/boolean/json), `default_value`, `extraction_prompt` (dùng khi variable gắn với node extraction), `scope`, `organization_id`, `current_version`, `is_deleted`.

**Migration extraction_variables:** Với workflow hiện có, `nodes[].data.extraction_variables[]` inline (`name`, `type`, `prompt`) được migrate thành: (a) tạo `VariableModel(scope=organization)` tương ứng cho mỗi biến chưa tồn tại, (b) thay node field bằng `variable_key` + `variable_scope=organization` tham chiếu tới variable vừa tạo. Super User có thể sau đó "promote" variable org lên `scope=global` nếu muốn dùng lại cho nhiều template.

### 5.6 Superuser — Global AI Configuration

Prefix: `/superuser/ai-config`

| Method | Path | Chức năng |
|--------|------|-----------|
| GET | `/superuser/ai-config` | Lấy global config **mặc định** (LLM, TTS, STT, embeddings) — masked secrets |
| PUT | `/superuser/ai-config` | Cập nhật global config mặc định (không versioned — chỉ 1 config hệ thống) |
| GET | `/superuser/ai-config/validate` | Validate API keys / connectivity |
| GET | `/superuser/ai-config/usage` | Tổng usage toàn hệ thống, breakdown theo org đang dùng global vs override (optional) |

### 5.7 Tenant — Template catalog

| Method | Path | Auth | Chức năng |
|--------|------|------|-----------|
| GET | `/workflow/templates` | `get_user` hoặc `public` | Catalog template **published** (thay thế list hiện tại) |
| POST | `/workflow/templates/{template_id}/copy` | `get_user` | Copy template vào org (snapshot semantics) |

---

## 6. Ma trận tổng hợp API

| Nhóm | Đổi | Thêm | Giữ nguyên |
|------|-----|------|------------|
| Health | | | 1 |
| Campaign | | | 9 |
| Credentials | | | 5 |
| Integration | | | 5 |
| Credentials | 5 | | |
| Knowledge Base | 6 | | |
| LoopTalk | | | 10 |
| Organization | | | 3 |
| Organization Usage | 2 (optional fields) | | 1 |
| Reports | | | 3 |
| S3 | | | 3 |
| Service Keys | | | 4 |
| User | 3 (không breaking) | | 6 |
| Tools | 6 | | |
| Workflow | 5 | 1 (`copy`) | 8 |
| Workflow Embed | | | 3 |
| Telephony | | | 14 |
| WebRTC | | | 2 |
| Public * | | | 6 |
| Superuser | 0 | ~46 (bao gồm `.../versions`, `.../publish`, `.../unpublish`, `.../referencing-workflows`) | 3 |
| **Variables** | | **14** (bao gồm superuser mirror + versions + publish/unpublish) | *(module mới)* |

**Ước tính endpoint mới:** ~50–55 (superuser namespaces + versioning/publish sub-endpoints + variables + credentials).

**Tổng resource types cần `scope=global` + versioning:** 4 — Tool, KB document, Variable, Credential. Workflow template versioned riêng qua `workflow_definitions` (đã có). AI config **không versioned** (config hệ thống đơn, tenant override lưu ở `UserConfigurationModel`/org level như hiện tại).

---

## 7. Luồng chính (sequence)

### 7.1 Super User publish template

```
Super User
  → POST /superuser/credentials (cho webhook + HTTP tools)          [current_version=1, draft]
  → POST /superuser/credentials/{uuid}/versions/1/publish            [published_version=1]
  → POST /superuser/tools, /superuser/knowledge-base/*, /superuser/variables  [current_version=1, draft]
  → POST .../versions/1/publish (từng resource)                      [published_version=1]
  → POST /superuser/workflow-templates (definition references global UUID + published_version)
  → POST /superuser/workflow-templates/{id}/publish

Tenant
  → GET /workflow/templates
  → POST /workflow/templates/{id}/copy
      → pin *_version cho từng global dep tại thời điểm copy
      → regenerate trigger_path + auto-enable agent_triggers
  → POST /workflow/{id}/validate  ✓
  → POST /workflow/{id}/runs       (dùng global AI default hoặc override + global tools/KB theo version đã pin)

--- Sau đó, Super User sửa 1 global tool ---
  → PUT /superuser/tools/{tool_uuid}   → current_version: 1 → 2 (draft, published_version vẫn = 1)
  → Workflow tenant ở trên vẫn resolve version=1 (published_version lúc pin) → KHÔNG bị ảnh hưởng
  → Tenant KHÔNG thấy version=2 (draft) trong catalog cho tới khi Super User publish
  → POST /superuser/tools/{tool_uuid}/versions/2/publish  → published_version: 1 → 2
  → Tenant copy MỚI từ giờ sẽ pin version=2

--- Super User xóa global tool đó ---
  → DELETE /superuser/tools/{tool_uuid}  (is_deleted=true)
  → Ẩn khỏi catalog; POST .../copy hoặc PUT /workflow reject nếu chọn tool này làm dep MỚI
  → Workflow tenant đã pin version=1 vẫn chạy bình thường
```

### 7.2 Tenant workflow hỗn hợp deps

```
Tenant tạo POST /tools (org), POST /variables (org)
Tenant sửa workflow definition: mix global tool_uuid + org tool_uuid
PUT /workflow/{id} → validate refs
Runtime → resolve từng ref theo scope
Usage → ghi theo organization_id của workflow run
```

---

## 8. Phase triển khai đề xuất

| Phase | Phạm vi | API chính |
|-------|---------|-----------|
| **P0** | Global AI config mặc định (tenant vẫn override như hiện tại) | `/superuser/ai-config` |
| **P1** | `scope` + **versioning + draft/publish + soft-delete** trên Tool + KB + Credential + list merge (tenant chỉ thấy published) | `/tools/*`, `/knowledge-base/*`, `/credentials/*` + superuser mirrors + `.../versions`, `.../publish`, `.../unpublish` |
| **P2** | Variables resource (thay `extraction_variables` inline) + migrate data cũ | `/variables`, `/superuser/variables`, migration script |
| **P3** | Merge `workflow_templates` → `WorkflowModel.is_template` + Superuser workflow templates + tenant copy (version pin + auto-enable trigger) | `/superuser/workflow-templates`, `POST .../copy`, migration script |
| **P4** | UI: template catalog, dependency picker (global vs org, hiển thị version), version history viewer | — |

---

## 9. Rủi ro & câu hỏi mở (đã chốt — lưu lại quyết định)

Tất cả câu hỏi mở ở bản trước đã được stakeholder trả lời. Giữ lại đây làm decision log:

1. ~~**Snapshot risk**~~ → **Đã chốt:** Versioning + soft-delete (§3.0). Edit → version mới, ref cũ vẫn resolve. Delete → soft-delete, chỉ chặn reference mới, không phá workflow đã pin.
2. ~~**Credential trong global tool**~~ → **Đã chốt:** Credential là resource `scope=global` thứ 4; global HTTP tool chỉ ref global credential.
3. ~~**API trigger regenerate**~~ → **Đã chốt:** Auto-enable ngay sau copy, tenant không cần bật tay.
4. ~~**Workflow template vs WorkflowModel**~~ → **Đã chốt:** Gộp vào `WorkflowModel` với flag `is_template`; versioning tái dùng `workflow_definitions`/`is_current`.
5. ~~**MPS `POST /workflow/create/template`**~~ → **Đã chốt:** Giữ nguyên, tenant vẫn tự tạo workflow riêng bằng NL.
6. ~~**Breaking change `PUT /user/configurations/user`**~~ → **Đã chốt:** Không bỏ; tenant tự nhập API key sẽ override global default (không breaking change).
7. ~~**Unique constraint**~~ → **Đã chốt:** Unique theo từng scope — `(organization_id, name)` cho org, `(scope=global, name)` cho global (2 namespace độc lập).
8. ~~**extraction_variables vs /variables**~~ → **Đã chốt:** Promote thành shared variable resource (`/variables`); node chỉ giữ reference.
9. ~~**KB document versioning — chunk-level diff?**~~ → **Đã chốt:** Không tối ưu ở phase 1 — mỗi version **re-embed toàn bộ** tài liệu.
10. ~~**Retention policy cho version history?**~~ → **Đã chốt:** Không có retention theo số lượng/thời gian. Version chỉ bị hard-delete khi `referencing_workflow_count == 0` **và** Super User chủ động xóa (xem §3.0 mục 7).
11. ~~**Draft vs Published cho global resource?**~~ → **Đã chốt:** Tenant chỉ thấy/reference version đã `published`; version mới tạo là draft, chỉ Super User thấy trong trang quản trị (xem §3.0 mục 2, quyết định #11).

Không còn câu hỏi mở nào cho phase 1 — mọi quyết định đã được chốt ở trên.

---

## 10. Out of scope (phase 1)

> Đây là những thứ đã được cân nhắc trong quá trình thiết kế nhưng **chủ động quyết định không làm ở phase 1** (khác với "câu hỏi mở" — mọi câu hỏi mở đã được trả lời ở §9).

- **Fork semantics** (clone global deps vào org — hiện tại là snapshot + version-pin, không phải fork độc lập).
  Tenant chỉ **giữ reference** (pin version) tới resource global gốc, không sở hữu bản sao riêng để tự sửa. Nếu muốn tùy biến độc lập, tenant phải tạo resource `scope=organization` mới từ đầu, không "tách nhánh" (fork) từ global resource.

- **Per-tenant quota trên global AI pool** (chỉ ghi usage, chưa throttle riêng).
  Mọi tenant dùng chung 1 pool AI config; usage vẫn được **ghi nhận riêng** theo `organization_id` cho billing/báo cáo, nhưng phase 1 **không giới hạn** (rate limit/quota) riêng cho từng tenant trên pool chung — một tenant dùng nhiều có thể ảnh hưởng tenant khác qua rate limit chung của provider.

- **"Undelete" tự động cho global resource đã soft-delete.**
  Sau khi Super User soft-delete (ẩn khỏi catalog, chặn reference mới), dữ liệu vẫn còn trong DB nhưng **không có API khôi phục** để đưa resource trở lại catalog. Muốn dùng lại phải tạo resource mới.

- **Chunk-level diff khi re-process KB document** (luôn re-embed toàn bộ).
  Mỗi lần sửa/re-upload KB document global, hệ thống re-embed **toàn bộ** tài liệu để tạo version mới, dù chỉ thay đổi một phần nhỏ. Tối ưu chunk-level (chỉ re-embed phần thay đổi) không làm ở phase 1 — đơn giản hơn, đổi lại tốn compute hơn cho tài liệu lớn.

- **Retention policy tự động theo N version/N ngày** (chỉ hard-delete thủ công khi `referencing_workflow_count == 0`).
  Version history giữ **vô hạn**, không tự dọn theo số lượng hoặc thời gian. Cách duy nhất để xóa dữ liệu vật lý là Super User **chủ động hard-delete**, và chỉ được phép khi không còn workflow nào (của bất kỳ tenant nào) còn reference tới resource đó.

- **Thay đổi telephony / campaign / embed APIs.**
  Không phải tính năng bị hoãn, mà chỉ nhắc lại rằng các nhóm API này (đã liệt kê ở [§4.8](#48-các-nhóm-api-không-thay-đổi-liên-quan-gián-tiếp)) **không nằm trong phạm vi** thay đổi của plan này — giữ nguyên hoàn toàn.

---

## Phụ lục: Mapping file code dự kiến chạm

| Area | Files |
|------|-------|
| Models | `api/db/models.py` — thêm `scope`, `current_version`, `published_version`, `is_deleted` (Tool/Credential/KB doc), `VariableModel` + `VariableVersionModel`, version model cho từng resource (`ToolVersionModel` + `is_published`, `CredentialVersionModel`, `KnowledgeBaseDocumentVersionModel`), `WorkflowModel.is_template` + `source_template_id`/`source_template_version` |
| Enums | `api/enums.py` — `ResourceScope` |
| Routes mới | `api/routes/superuser_*.py` (tools/kb/credentials/variables/ai-config/workflow-templates + `.../versions`), `api/routes/variables.py` |
| Routes sửa | `workflow.py` (template = `is_template` filter, copy = version pin + auto-enable trigger), `tool.py`, `knowledge_base.py`, `credentials.py`, `user.py` (giữ override), `superuser.py` |
| Services | `api/services/configuration/*` (ai config override resolution), `run_integrations.py`, `custom_tool.py` (resolve theo version pin), workflow validate (chặn ref mới tới resource `is_deleted`), service tính `referencing_workflow_count` (scan `workflow_definitions.definition` theo `*_uuid`) cho hard-delete |
| Migrations | Alembic — scope + versioning columns, `*_versions` tables, `VariableModel`, migrate `workflow_templates` → `workflows(is_template=true)`, migrate `extraction_variables` inline → `VariableModel` refs, unique index theo scope (partial index cho global) |
| UI | Template catalog, resource picker scope badge + version selector, version history/rollback viewer, superuser admin pages |
