# C4 Level 4 - API Gateway Component

## 1. Main API Structure
```mermaid
classDiagram
    class FastAPIApp
    class ProxyRouter {
        +proxy_ai_databases(path, request)
        +proxy_workers(path, request)
        +proxy_workflows(path, request)
        +proxy_tools(path, request)
        +proxy_parser(path, request)
        +proxy_indexing(path, request)
        +proxy_vector_search(path, request)
        +proxy_retrieval(path, request)
        +proxy_qa(path, request)
        +proxy_feedback(path, request)
        +proxy_specs(path, request)
        +proxy_specs_v2(path, request)
        +proxy_embedding(path, request)
        +proxy_parsers(path, request)
        +proxy_configuration(path, request)
    }
    class OpenAPIMerger {
        +load_phase2_openapi()
        +custom_openapi()
    }
    FastAPIApp --> ProxyRouter : sử dụng
    FastAPIApp --> OpenAPIMerger : sử dụng
```
- `FastAPIApp` là entrypoint, định nghĩa các route API, health check, config.
- `ProxyRouter` định nghĩa các hàm proxy cho từng service, nhận request từ webapp hoặc client, forward sang service backend.
- `OpenAPIMerger` merge spec OpenAPI từ nhiều phase.

## 2. API chính
- `/ai-databases/*`, `/workers/*`, `/workflows/*`, `/tools/*`, ...: Proxy request đến các service tương ứng.
- `/health`, `/config`, `/services`: Health check, config, service discovery.

## 3. Liên kết với các component khác
- Là entrypoint duy nhất cho webapp và client bên ngoài.
- Route request đến các service backend: Core Workers, Core Workflows, Tools Inventory, AI Databases.
- Merge OpenAPI spec để hỗ trợ doc, test, mở rộng API.

---

> Xem thêm các file C4 Level 4 khác cho LLM, Parser, Embedding, Rerank, Vector Search, AI Databases để hiểu toàn bộ kiến trúc code. 