# Phát triển phần mềm trong kỷ nguyên AI

## Mở đầu:

<img width="1028" height="230" alt="image" src="https://github.com/user-attachments/assets/4d5fea55-e529-426a-82af-f9fb975358d9" />

Bài viết này được thiết kế dành cho bất kỳ ai đang xây dựng phần mềm (dù đơn giản hay phức tạp) muốn hiểu sâu từ trực quan (intuition) đến chi tiết triển khai (workflow, công cụ, best practices) về phát triển phần mềm trong kỷ nguyên AI — đặc biệt là kỷ nguyên **Agentic AI**, nơi các AI agent có khả năng tự lập kế hoạch, sử dụng công cụ, ghi nhớ ngữ cảnh và thực thi tác vụ end-to-end.

**Mục tiêu**:
- Nắm được sự chuyển dịch vai trò của con người trong quá trình phát triển phần mềm.
- Hiểu rõ các cấu phần (building blocks) của phần mềm hiện đại. Chẳng hạn như:
  - Phần mềm truyền thống (Software 1.0 như theo định nghĩa của [Andrej Kapathy](https://karpathy.medium.com/software-2-0-a64152b37c35)).
  - AI blocks (Software 2.0 & Software 3.0).
- Các phương pháp tiếp cận khi phát triển phần mềm (TDD, SDD, DDD, BDD, GitOps, v.v.) và lựa chọn như thế nào khi phát triển cùng AI agent.
- Phát triển phần mềm với **SDD + TDD** và AI agent.
- Giới thiệu các một số công cụ AI agent cho coding và automation.

<br>

## 1. Rise of AI in coding: Sự chuyển dịch cách sử dụng AI trong phát triển phần mềm
<br>
<img width="1005" height="422" alt="image" src="https://github.com/user-attachments/assets/e249d409-290f-48cf-8c2f-fd0172251522" />

<br>
<br>

Quá trình áp dụng AI trong coding (từ khi ChatGPT ra đời vào năm 2022) đã trải qua ba giai đoạn chính, mỗi giai đoạn đánh dấu một bước nhảy vọt về mức độ tự động hóa và giá trị mang lại.

| Giai đoạn | Mô tả | Ví dụ công cụ | Đặc điểm nổi bật |
|---|---|---|---|
| **Ask/Copy to chatbot** | Lập trình viên hỏi chatbot (ChatGPT, Claude) rồi copy-paste code vào dự án | ChatGPT, Claude (chat interface) | Code được sinh ra nhưng thiếu ngữ cảnh dự án, dễ lỗi tích hợp, khó maintain. Phù hợp với viết function nhỏ. |
| **Auto-complete** | AI gợi ý code ngay trong IDE dựa trên ngữ cảnh file đang mở | GitHub Copilot, Cursor, OpenCode | Tích hợp sâu vào workflow, giảm thời gian gõ code, nhưng chỉ mang tính gợi ý, con người vẫn kiểm soát hoàn toàn. Phù hợp với vai trò trợ lý cho lập trình viên |
| **Agent AI** | AI tự lập kế hoạch, viết code across nhiều file, chạy test, tương tác với môi trường phát triển, fix lỗi, submit PR | Claude Code, Cursor, Codex, OpenCode | Tự động hóa end-to-end, giảm đáng kể thời gian coding thủ công, chuyển vai trò con người sang "người giám sát và định hướng" |

<br>

**Ví dụ:**
Trước đây, khi cần viết một API endpoint để lấy danh sách user từ database, bạn sẽ:
- Tự viết query SQL hoặc ORM code.
- Tạo route trong Express/FastAPI.
- Viết test case.
- Chạy test, debug nếu lỗi.

Với **Agent AI**, bạn chỉ cần mô tả mục tiêu: *"Tạo API GET /users trả về danh sách user từ bảng `users` trong PostgreSQL, có pagination và filter theo status"*. Agent sẽ:
- Phân tích schema database (nếu được cung cấp).
- Sinh code backend (Node.js/Python).
- Viết test case (unit test + integration test).
- Chạy test, tự fix lỗi nếu có.
- Commit code và tạo pull request.

<br>

## 2. Programming in Agentic AI era: Phần mềm trong kỷ nguyên AI agent

### A. Software is made by combining & structuring building blocks

<img width="982" height="215" alt="image" src="https://github.com/user-attachments/assets/253a1863-a8ac-4aca-98be-fdd0e74a2524" />

<br>

#### i. Non-AI blocks
Đây là các thành phần truyền thống, vẫn cần thiết và thường được cung cấp bởi các dịch vụ managed hoặc open-source:
- **UI components**: React, Vue, Flutter widgets, ...
- **Databases**: PostgreSQL, MongoDB, Firebase, ...
- **Identity & Auth**: Auth0, Firebase Auth, Keycloak, ...
- **Payment**: Stripe, PayPal, Momo API, ...
- **Observability**: Prometheus, Grafana, Loki, Sentry, ...
- **Message Queue**: Kafka, RabbitMQ, AWS SQS, ...
- **CI/CD**: GitHub Actions, GitLab CI, Jenkins.

#### ii. AI blocks
Đây là các thành phần mới, đặc trưng cho kỷ nguyên AI, thường được cung cấp dưới dạng API, SDK hoặc nền tảng managed:
- **ML/DL models**
- **Foundation models**: OpenAI GPT, Anthropic Claude, Google Gemini, Meta Llama.
- **LLMs**: Mô hình ngôn ngữ lớn dùng cho chat, code generation, summarization.
- **RAG (Retrieval-Augmented Generation)**: Kết hợp LLM với vector database (Milvus, Pinecone, Weaviate, Qdrant) để truy xuất kiến thức bên ngoài parametric memory.
- **Agentic workflows**: Các workflow mà AI agent tự lập kế hoạch, gọi tool, ghi nhớ ngữ cảnh và thực thi.
- **Evals & Error Analysis**: Công cụ đánh giá chất lượng output của AI (ví dụ: LangChain Evals, RAGAS, TruLens).
- **Memory**: Cơ chế lưu trữ ngữ cảnh dài hạn cho agent (vector store, SQL, Redis).
- **Voice stack**: Speech-to-text (Whisper, Google Speech), text-to-speech (ElevenLabs, Azure TTS), voice agent (Vapi, Retell AI).

**Ví dụ:** Một hệ thống chatbot hỗ trợ khách hàng cho ngân hàng có thể được xây dựng như sau:
- **Frontend**: React + Tailwind (non-AI).
- **Backend**: FastAPI + PostgreSQL (non-AI).
- **Auth**: Firebase Auth (non-AI).
- **AI core**: 
  - LLM: Claude Sonnet (Foundation model).
  - RAG: Vector store chứa tài liệu nghiệp vụ ngân hàng (AI block).
  - Agent workflow: Agent tự gọi API kiểm tra số dư, chuyển khoản, tra cứu giao dịch (AI block).
  - Memory: Lưu lịch sử hội thoại trong Redis (AI block).
  - Evals: Đánh giá độ chính xác của câu trả lời bằng RAGAS (AI block).
  - Voice: Whisper + ElevenLabs cho voicebot (AI block).
- **Observability**: Sentry + LangSmith (non-AI + AI).

### B. New philosophies: Triết lý mới trong phát triển phần mềm

#### i. Code is no longer as valuable artifact as it used to be

Trước đây, code là tài sản quý giá nhất của đội kỹ thuật. Viết code tốn thời gian, khó maintain, và việc lựa chọn kiến trúc là quyết định "một chiều" (1-way door) — rất khó thay đổi sau khi đã triển khai. 

Trong kỷ nguyên AI:
- **Code trở nên "rẻ" và nhanh chóng được sinh ra bởi AI**. 
- **Lựa chọn kiến trúc trở thành quyết định "hai chiều" (2-way door)**: Dễ dàng thay đổi, refactor hoặc rewrite nhờ AI hỗ trợ. 
- **Giá trị thực sự nằm ở việc quyết định "cái gì cần xây dựng" (what to build)**, không phải "làm thế nào để xây dựng" (how to build).

> **Ví dụ:** Trước đây, việc chuyển từ monolith sang microservices có thể tốn 6–12 tháng với đội 10 kỹ sư. Với AI agent, quá trình này có thể rút ngắn xuống 1–2 tháng (tuỳ vào quy mô), và nếu sai, có thể rollback hoặc refactor nhanh chóng.

#### ii. Building is easier → Deciding what to build is the bottleneck

Khi AI tăng tốc coding lên **10x–100x**, bottleneck trong phát triển sản phẩm dịch chuyển từ **kỹ thuật** sang **sản phẩm, thiết kế, marketing và compliance**. 

<img width="929" height="333" alt="image" src="https://github.com/user-attachments/assets/0e44b4f6-ed2e-4681-9ab5-3ff8ec28a351" />


**Sự chuyển dịch về thời gian phát triển**

Khi con người dần **hand-off** khỏi quá trình coding (tạo code và review code), thời gian phát triển được phân bổ lại.

| Giai đoạn | Trước AI (2020–2024) | Với AI Agent (2025–2026) |
|---|---|---|
| **Yêu cầu & thiết kế** | 20% | 40–50% |
| **Viết code** | 50% | 10–20% |
| **Review code** | 20% | 10–15% |
| **Test & deploy** | 10% | 15–20% |

Giải thích:
- **Viết code** giảm mạnh vì AI sinh code nhanh.
- **Yêu cầu & thiết kế** tăng vì cần định nghĩa rõ mục tiêu, nghiệp vụ, ràng buộc.
- **Test & deploy** tăng nhẹ vì cần đảm bảo chất lượng khi code được sinh ra nhanh.

**Thay đổi tỉ lệ đối ứng giữa các role**

Trước kia, tỷ lệ **Engineer : PM/Design/Marketing/Compliance** khoảng **5-10 : 1** (5-10 kỹ sư hỗ trợ 1 người thuộc các vai trò khác).
Với AI agent:
- Tỷ lệ này dịch chuyển về **1 : 1** hoặc **1 : 2**. 
- **PM, Design, Marketing, Compliance** trở thành nút thắt mới vì họ cần đưa ra quyết định nhanh, chính xác về sản phẩm, trải nghiệm người dùng, chiến lược marketing và tuân thủ pháp lý.

**Ví dụ:** Một startup fintech có thể xây dựng MVP (Minimum Viable Product) trong 2 tuần với 1 PM + 1 Engineer + AI agent, thay vì 2 tháng với 1 PM + 5 Engineers như trước đây.

**Thành phần team chuyển từ Specialist sang Generalist**

Trước đây, đội ngũ phát triển phần mềm thường gồm các **Specialist**:
- Frontend Developer (React, Vue).
- Backend Developer (Node.js, Python).
- DevOps Engineer (Kubernetes, Terraform).
- QA Engineer (Selenium, Cypress).
- Data Engineer (Spark, Kafka).

Với AI hỗ trợ, đội ngũ chuyển sang **Generalist**:
- Mỗi thành viên có thể làm nhiều vai trò nhờ AI hỗ trợ viết code, deploy, test.
- **Kỹ sư AI-native** có thể:
  - Viết frontend + backend.
  - Thiết kế database schema.
  - Viết test case.
  - Deploy lên cloud.
  - Phân tích dữ liệu.

## 3. Các phương pháp tiếp cận khi xây dựng phần mềm

Dưới đây là bảng tổng hợp các phương pháp phát triển phần mềm phổ biến, kèm trọng tâm cốt lõi và ví dụ áp dụng trong kỷ nguyên AI:

| Nhóm Phân Loại | Ký Hiệu | Tên Tiếng Anh | Tên Tiếng Việt | Trọng Tâm Cốt Lõi | Ví dụ áp dụng với AI |
|---|---|---|---|---|---|
| **Kiểm thử & Chất lượng** | TDD | Test-Driven Development | Phát triển hướng kiểm thử | Viết test trước, code sau (Red-Green-Refactor) | AI viết test case từ spec, chạy test, tự fix lỗi |
| | BDD | Behavior-Driven Development | Phát triển hướng hành vi | Viết kịch bản test bằng ngôn ngữ tự nhiên (Given-When-Then) | AI sinh scenario từ user story, chuyển thành test automation |
| | ATDD | Acceptance Test-Driven Development | Phát triển hướng kiểm thử chấp nhận | Toàn đội thống nhất tiêu chí nghiệm thu trước khi code | AI tạo acceptance test từ requirement document |
| **Thiết kế & Nghiệp vụ** | DDD | Domain-Driven Design | Thiết kế hướng miền nghiệp vụ | Lấy logic nghiệp vụ làm trung tâm kiến trúc | AI phân tích domain, đề xuất bounded context, aggregate root |
| | SDD | Specification-Driven Development | Phát triển hướng đặc tả | Spec là nguồn chân lý, AI sinh code từ spec | Viết spec chi tiết (OpenAPI, Markdown), AI sinh code + test |
| | MDD | Model-Driven Development | Phát triển hướng mô hình | Thiết kế mô hình UML trước, tự động sinh mã | AI chuyển UML diagram thành code skeleton |
| **Kiến trúc dữ liệu & Luồng đi** | EDD | Event-Driven Development | Phát triển hướng sự kiện | Hệ thống giao tiếp bằng sự kiện (event) | AI thiết kế event schema, sinh producer/consumer code |
| | DDD (Data) | Data-Driven Development | Phát triển hướng dữ liệu | Ra quyết định dựa trên phân tích dữ liệu | AI phân tích data pipeline, đề xuất optimization |
| **Giao diện & Trải nghiệm** | CDD | Component-Driven Development | Phát triển hướng thành phần | Xây UI từ component nhỏ rồi ghép lại | AI sinh React/Vue component từ design system |
| | UXDD | User Experience-Driven Development | Phát triển hướng trải nghiệm | Đặt UX làm thước đo tính năng | AI phân tích user behavior, đề xuất UX improvement |
| **Quản lý & Vận hành** | FDD | Feature-Driven Development | Phát triển hướng tính năng | Chia dự án thành danh sách tính năng ngắn hạn | AI ưu tiên backlog, ước lượng effort |
| | GitOps | Git-Driven Operations | Vận hành hướng Git | Dùng Git làm trung tâm tự động hóa hạ tầng | AI tạo Terraform code, deploy qua GitOps pipeline |

***


### TDD (Test-Driven Development) với AI

**Quy trình Red-Green-Refactor**: 
1. **Red**: Viết (hoặc nhờ AI viết) một test case mô tả hành vi mong đợi. Test này **phải thất bại** ban đầu.
2. **Green**: Viết (hoặc nhờ AI viết) code tối thiểu để test **thành công**.
3. **Refactor**: Cải thiện code (clean code, optimization) nhưng **giữ nguyên test passing**.

**Ví dụ với AI:**
```markdown
Yêu cầu: "Viết hàm `calculate_discount(price, user_type)` trả về giá sau chiết khấu.
- user_type = 'premium': giảm 20%
- user_type = 'standard': giảm 10%
- user_type khác: không giảm

Bước 1 (Red): Yêu cầu AI viết test case:
- Input: price=100, user_type='premium' → Expected: 80
- Input: price=100, user_type='standard' → Expected: 90
- Input: price=100, user_type='guest' → Expected: 100

Bước 2 (Green): Yêu cầu AI viết code tối thiểu để pass test.

Bước 3 (Refactor): Yêu cầu AI refactor code (thêm docstring, type hint, error handling).
```

**Best practices**: 
- Bắt đầu với hành vi có giá trị cao, không phải edge case.
- Đặt tên test mô tả rõ hành vi (ví dụ: `test_calculate_discount_premium_user`).
- Giữ test scope tight: một hành vi per prompt.
- Để AI refactor: "Clean up the logic but keep all tests green".
- Dùng pre-commit hook để chạy test tự động.

### SDD (Specification-Driven Development) với AI

**Định nghĩa:** SDD là phương pháp trong đó **specification (đặc tả)** là nguồn chân lý duy nhất, không phải code. AI agent sinh code từ spec, đảm bảo implementation luôn aligned với requirement. 

**Workflow 4 pha**:
1. **Capture Intent**: Viết spec chi tiết (Markdown, OpenAPI, YAML) mô tả **what** hệ thống cần làm.
2. **Derive Plan**: AI phân tích spec, đề xuất implementation plan (kiến trúc, công nghệ, task breakdown).
3. **Generate Code**: AI sinh code từ plan, kèm test case.
4. **Execute & Validate**: Chạy test, validate output, cập nhật spec nếu cần.

**Ví dụ spec (Markdown + OpenAPI)**: 
```markdown
# Spec: User Management API

## Mục tiêu
Cung cấp API để quản lý user (create, read, update, delete) với authentication và authorization.

## Yêu cầu chức năng
1. POST /users: Tạo user mới (email, password, name).
2. GET /users/{id}: Lấy thông tin user theo ID.
3. PUT /users/{id}: Cập nhật thông tin user.
4. DELETE /users/{id}: Xóa user.
5. Authentication: JWT token qua header `Authorization: Bearer <token>`.
6. Authorization: Chỉ admin mới được xóa user.

## OpenAPI Spec
(openapi: 3.0.0
info:
  title: User Management API
  version: 1.0.0
paths:
  /users:
    post:
      summary: Create user
      requestBody:
        content:
          application/json:
            schema:
              type: object
              properties:
                email: { type: string }
                password: { type: string }
                name: { type: string }
      responses:
        201:
          description: User created
  /users/{id}:
    get:
      summary: Get user by ID
      parameters:
        - name: id
          in: path
          required: true
          schema: { type: string }
      responses:
        200:
          description: User data
)
```

**Công cụ hỗ trợ SDD**:
- **GitHub Spec Kit**: Plugin tích hợp spec vào CI/CD, tự động validate code against spec.
- **Claude Code + Spec**: Viết spec trong Markdown, Claude Code sinh code + test.
- **Cursor + Spec**: Import spec vào Cursor, AI sinh code across files.

***

## 4. Step by step working with SDD + TDD

Kết hợp **SDD** (định nghĩa what) và **TDD** (kiểm soát how) là phương pháp mạnh mẽ nhất trong kỷ nguyên AI. Dưới đây là quy trình step-by-step chi tiết:

### Bước 1: Viết Specification (SDD Phase 1)

**Mục tiêu:** Định nghĩa rõ **what** hệ thống cần làm, không quan tâm **how**.

**Công cụ:** Markdown, OpenAPI, YAML, Notion, Confluence.

**Ví dụ spec cho tính năng "Tính giá đơn hàng với discount và shipping":**
```markdown
# Spec: Order Pricing Calculator

## Mục tiêu
Tính tổng giá trị đơn hàng sau khi áp dụng discount và shipping fee.

## Yêu cầu chức năng
1. Input: 
   - `items`: danh sách sản phẩm (mỗi item có `price`, `quantity`).
   - `user_type`: 'premium', 'standard', 'guest'.
   - `shipping_address`: tỉnh/thành phố (ví dụ: 'Ha Noi', 'Ho Chi Minh').
2. Output: 
   - `subtotal`: tổng giá trước discount.
   - `discount_amount`: số tiền giảm.
   - `shipping_fee`: phí vận chuyển.
   - `total`: tổng cuối cùng.
3. Rules:
   - Discount:
     - 'premium': giảm 20% subtotal.
     - 'standard': giảm 10% subtotal.
     - 'guest': không giảm.
   - Shipping fee:
     - 'Ha Noi', 'Ho Chi Minh': 20,000 VND.
     - Khác: 40,000 VND.
   - Total = subtotal - discount_amount + shipping_fee.
4. Edge cases:
   - `items` rỗng → trả về lỗi 400.
   - `price` hoặc `quantity` âm → trả về lỗi 400.
```

### Bước 2: Derive Plan & Write Test Cases (SDD Phase 2 + TDD Red)

**Mục tiêu:** AI phân tích spec, đề xuất plan và viết test case.

**Prompt cho AI (Claude Code, Cursor, Copilot):**
```markdown
Dựa vào spec trên, hãy:
1. Đề xuất implementation plan (ngôn ngữ, kiến trúc, thư viện).
2. Viết test cases (pytest hoặc Jest) cho các scenario:
   - Normal case: premium user, Ha Noi shipping.
   - Standard user, Ho Chi Minh shipping.
   - Guest user, other province shipping.
   - Edge case: items rỗng.
   - Edge case: price âm.

Yêu cầu: Test phải mô tả rõ hành vi, đặt tên rõ ràng, cover edge cases.
```

**Output từ AI (ví dụ test case bằng pytest):**
```python
# test_order_pricing.py

def test_premium_user_ha_noi():
    items = [{"price": 100000, "quantity": 2}]
    user_type = "premium"
    shipping_address = "Ha Noi"
    result = calculate_order_price(items, user_type, shipping_address)
    assert result["subtotal"] == 200000
    assert result["discount_amount"] == 40000  # 20%
    assert result["shipping_fee"] == 20000
    assert result["total"] == 180000

def test_standard_user_hcm():
    items = [{"price": 50000, "quantity": 3}]
    user_type = "standard"
    shipping_address = "Ho Chi Minh"
    result = calculate_order_price(items, user_type, shipping_address)
    assert result["subtotal"] == 150000
    assert result["discount_amount"] == 15000  # 10%
    assert result["shipping_fee"] == 20000
    assert result["total"] == 155000

def test_guest_user_other_province():
    items = [{"price": 200000, "quantity": 1}]
    user_type = "guest"
    shipping_address = "Da Nang"
    result = calculate_order_price(items, user_type, shipping_address)
    assert result["subtotal"] == 200000
    assert result["discount_amount"] == 0
    assert result["shipping_fee"] == 40000
    assert result["total"] == 240000

def test_empty_items():
    items = []
    user_type = "premium"
    shipping_address = "Ha Noi"
    with pytest.raises(ValueError):
        calculate_order_price(items, user_type, shipping_address)

def test_negative_price():
    items = [{"price": -10000, "quantity": 1}]
    user_type = "standard"
    shipping_address = "Ha Noi"
    with pytest.raises(ValueError):
        calculate_order_price(items, user_type, shipping_address)
```

**Chạy test (Red phase):** Test **phải thất bại** vì chưa có code chính thức. [cloud.google](https://cloud.google.com/discover/how-test-driven-development-amplifies-ai-success)

### Bước 3: Generate Code (SDD Phase 3 + TDD Green)

**Prompt cho AI:**
```markdown
Viết hàm `calculate_order_price(items, user_type, shipping_address)` bằng Python để pass tất cả test cases trên.
Yêu cầu:
- Code tối thiểu, chỉ đủ để pass test.
- Thêm type hint, docstring.
- Xử lý edge cases (items rỗng, price âm).
```

**Output từ AI (ví dụ code):**
```python
# order_pricing.py

from typing import List, Dict, Any

def calculate_order_price(
    items: List[Dict[str, Any]],
    user_type: str,
    shipping_address: str
) -> Dict[str, int]:
    """
    Tính tổng giá trị đơn hàng sau khi áp dụng discount và shipping fee.
    
    Args:
        items: Danh sách sản phẩm, mỗi item có 'price' và 'quantity'.
        user_type: 'premium', 'standard', hoặc 'guest'.
        shipping_address: Tỉnh/thành phố (ví dụ: 'Ha Noi', 'Ho Chi Minh').
    
    Returns:
        Dict chứa 'subtotal', 'discount_amount', 'shipping_fee', 'total'.
    
    Raises:
        ValueError: Nếu items rỗng hoặc price/quantity âm.
    """
    if not items:
        raise ValueError("Items cannot be empty")
    
    subtotal = 0
    for item in items:
        price = item["price"]
        quantity = item["quantity"]
        if price < 0 or quantity < 0:
            raise ValueError("Price and quantity must be non-negative")
        subtotal += price * quantity
    
    # Discount
    discount_rates = {
        "premium": 0.2,
        "standard": 0.1,
        "guest": 0.0
    }
    discount_rate = discount_rates.get(user_type, 0.0)
    discount_amount = int(subtotal * discount_rate)
    
    # Shipping fee
    free_shipping_cities = ["Ha Noi", "Ho Chi Minh"]
    shipping_fee = 20000 if shipping_address in free_shipping_cities else 40000
    
    # Total
    total = subtotal - discount_amount + shipping_fee
    
    return {
        "subtotal": subtotal,
        "discount_amount": discount_amount,
        "shipping_fee": shipping_fee,
        "total": total
    }
```

**Chạy test (Green phase):** Test **phải passing**. [cloud.google](https://cloud.google.com/discover/how-test-driven-development-amplifies-ai-success)

### Bước 4: Refactor & Validate (SDD Phase 4 + TDD Refactor)

**Prompt cho AI:**
```markdown
Refactor code trên để:
- Clean code (DRY, SOLID).
- Thêm error handling chi tiết.
- Tối ưu performance (nếu có thể).
- Giữ nguyên tất cả test passing.
```

**Output từ AI (refactored code):**
```python
# order_pricing.py (refactored)

from typing import List, Dict, Any
from dataclasses import dataclass

@dataclass
class OrderItem:
    price: int
    quantity: int

class OrderPricingError(ValueError):
    pass

def calculate_order_price(
    items: List[Dict[str, Any]],
    user_type: str,
    shipping_address: str
) -> Dict[str, int]:
    """
    Tính tổng giá trị đơn hàng sau khi áp dụng discount và shipping fee.
    """
    _validate_items(items)
    subtotal = _calculate_subtotal(items)
    discount_amount = _calculate_discount(subtotal, user_type)
    shipping_fee = _calculate_shipping_fee(shipping_address)
    total = subtotal - discount_amount + shipping_fee
    
    return {
        "subtotal": subtotal,
        "discount_amount": discount_amount,
        "shipping_fee": shipping_fee,
        "total": total
    }

def _validate_items(items: List[Dict[str, Any]]) -> None:
    if not items:
        raise OrderPricingError("Items cannot be empty")
    for item in items:
        if item["price"] < 0 or item["quantity"] < 0:
            raise OrderPricingError("Price and quantity must be non-negative")

def _calculate_subtotal(items: List[Dict[str, Any]]) -> int:
    return sum(item["price"] * item["quantity"] for item in items)

def _calculate_discount(subtotal: int, user_type: str) -> int:
    discount_rates = {"premium": 0.2, "standard": 0.1, "guest": 0.0}
    return int(subtotal * discount_rates.get(user_type, 0.0))

def _calculate_shipping_fee(shipping_address: str) -> int:
    free_shipping_cities = {"Ha Noi", "Ho Chi Minh"}
    return 20000 if shipping_address in free_shipping_cities else 40000
```

**Chạy test lại (Refactor phase):** Test vẫn **passing**, code sạch hơn, dễ maintain. 

### Bước 5: Execute, Validate & Update Spec (SDD Phase 4)

- **Execute:** Deploy code lên staging/production.
- **Validate:** Chạy integration test, end-to-end test, monitor logs/metrics.
- **Update Spec:** Nếu có thay đổi requirement, cập nhật spec trước, sau đó lặp lại quy trình từ Bước 2. 

***

## 5. Tools: Giới thiệu các một số công cụ AI agent cho coding và automation.

### Workflow tools: Dify vs n8n

| Tiêu chí | **n8n** | **Dify** |
|---|---|---|
| **Primary paradigm** | Workflow-first: trigger drives the flow   | AI-first: LLM là core actor   |
| **Tích hợp** | 400+ integrations (Slack, Gmail, Google Sheets, API, v.v.)  | Tích hợp sâu với LLM, RAG, agent skills |
| **Use case** | Automation (ops, RevOps), AI là một bước trong workflow lớn   | Xây AI agent, chatbot, RAG pipeline, workflow AI-centric   |
| **Self-hostable** | Có | Có |
| **Visual builder** | Node-based workflow editor | Visual workflow + agent builder 
| **Learning curve** | Dễ cho ops/automation teams | Dễ cho AI/ML engineers |

**Khi nào chọn n8n:**
- Bạn cần automation đa dạng (gửi email, update database, gọi API) và AI chỉ là một phần nhỏ. 
- Đội ngũ quen với workflow automation (Zapier, Make).

**Khi nào chọn Dify:**
- Bạn xây AI agent, chatbot, RAG system làm core product. 
- Cần tích hợp sâu với LLM, vector store, agent skills.

### AI as Coworker tools

| Công cụ | Mô tả | Use case |
|---|---|---|
| **ChatGPT Work** | ChatGPT tích hợp vào workflow (Slack, Notion, Google Docs) | Brainstorm ý tưởng, viết content, tóm tắt tài liệu |
| **Claude Cowork** | Claude tích hợp vào IDE, terminal, workflow | Coding, debugging, writing spec, refactoring   |
| **Grokbot** | AI agent làm việc theo nhóm | Social media automation, content generation |
| **Cursor** | IDE tích hợp AI agent | Coding across files, chat, refactor, test   |
| **GitHub Copilot Workspace** | AI agent tích hợp GitHub | Tạo branch, viết code, chạy CI, tạo PR  |
| **Devin** | Agent tự động end-to-end | Nhận yêu cầu, lập kế hoạch, viết code, deploy   |

**Best practices khi dùng AI as Coworker**: 
- **Duy trì human oversight:** AI sinh code, con người review, validate business logic. 
- **Xem AI như partner, không phải replacement:** Con người guide, critique, refine output.
- **Giữ test readable, maintainable:** Refactor test do AI sinh để align với team convention.
- **Align AI với team standards:** Dùng style guide, linting rule để AI sinh code consistent.
- **Reinforce TDD cycle discipline:** Không skip bước Red-Green-Refactor. 

***

## Key takeaway

Hãy tập trung vào các kỹ năng cốt lõi và phương thức làm việc hơn là chạy đua theo các công cụ đang ngày một nhiều:

1. **Thành thạo AI coding assistant:** Học cách dùng Claude Code, Cursor, GitHub Copilot hiệu quả.
2. **Áp dụng SDD + TDD:** Viết spec chi tiết trước, coi đó như source of truth và dùng AI sinh code + test, refactor iteratively.
3. **Phát triển tư duy product:** Học cách ra quyết định "what to build", không chỉ "how to build".
4. **Trở thành Generalist AI-native:** Làm quen với nhiều vai trò (frontend, backend, DevOps, data) với sự hỗ trợ từ AI.
5. **Chọn công cụ phù hợp:** Dify cho AI agent, n8n cho automation, Claude/Cursor cho coding.
