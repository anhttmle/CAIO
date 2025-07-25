# Hướng dẫn setup Environment Variables cho từng service

## 1. Webapp
- **Biến env chính:**
  - `API_BASE_URL`: Địa chỉ API Gateway (mặc định: http://api-gateway:8000)
- **Ví dụ .env:**
  ```env
  API_BASE_URL=http://api-gateway:8000
  ```
- **Lưu ý:**
  - Nếu chạy local, có thể đổi sang http://localhost:8000

---

## 2. API Gateway
- **Biến env chính:**
  - Không bắt buộc, nhưng có thể cần cho logging, debug.
- **Lưu ý:**
  - Đọc file `swagger_phase2.yaml` nếu cần merge OpenAPI spec.

---

## 3. Core Workers
- **Biến env chính:**
  - `AI_DATABASES_URL`: Địa chỉ AI Databases (mặc định: http://ai-databases:8000)
  - `TOOLS_INVENTORY_URL`: Địa chỉ Tools Inventory (mặc định: http://tools-inventory:8000)
  - `OPENAI_API_KEY`: API key cho OpenAI (nếu dùng embedding/LLM)
  - `COHERE_API_KEY`: API key cho Cohere (nếu dùng rerank)
- **Ví dụ .env:**
  ```env
  AI_DATABASES_URL=http://ai-databases:8000
  TOOLS_INVENTORY_URL=http://tools-inventory:8000
  OPENAI_API_KEY=sk-xxx
  COHERE_API_KEY=xxx
  ```
- **Lưu ý:**
  - Không commit file .env chứa key lên git.

---

## 4. Core Workflows
- **Biến env chính:**
  - `AI_DATABASES_URL`, `CORE_WORKERS_URL`, `TOOLS_INVENTORY_URL`, `REDIS_URL`
- **Ví dụ .env:**
  ```env
  AI_DATABASES_URL=http://ai-databases:8000
  CORE_WORKERS_URL=http://core-workers:8000
  TOOLS_INVENTORY_URL=http://tools-inventory:8000
  REDIS_URL=redis://redis:6379/0
  ```

---

## 5. Tools Inventory
- **Biến env chính:**
  - `OPENAI_API_KEY`, `COHERE_API_KEY`
- **Ví dụ .env:**
  ```env
  OPENAI_API_KEY=sk-xxx
  COHERE_API_KEY=xxx
  ```

---

## 6. AI Databases
- **Biến env chính:**
  - `MILVUS_HOST`, `MILVUS_PORT`: Địa chỉ Milvus
  - `POSTGRES_HOST`, `POSTGRES_PORT`, `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`: Thông tin Postgres
- **Ví dụ .env:**
  ```env
  MILVUS_HOST=standalone
  MILVUS_PORT=19530
  POSTGRES_HOST=db
  POSTGRES_PORT=5432
  POSTGRES_USER=cobol
  POSTGRES_PASSWORD=cobol12345
  POSTGRES_DB=cobol_assistant
  ```
- **Lưu ý:**
  - Đặt password mạnh cho DB khi deploy production.

---

## 7. Redis, Celery, Minio, Etcd, Milvus, Postgres
- **Thường dùng biến mặc định trong docker-compose.**
- Có thể cấu hình thêm user/pass, port nếu cần bảo mật.

---

## Lưu ý chung
- Không commit file `.env` chứa key/token lên git.
- Sử dụng biến env cho mọi thông tin nhạy cảm (API key, DB password).
- Có thể dùng file `.env.example` để hướng dẫn setup cho dev mới.

---

> Xem thêm các file hướng dẫn deploy, dev, C4 để hiểu tổng thể hệ thống. 