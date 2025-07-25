# C4 Level 4 - Vector Search Component (Core Workers & Tools Inventory)

## 1. VectorSearchWorker (Core Workers)
```mermaid
classDiagram
    class VectorSearchWorker {
        +search(request_data)
        -tools_inventory_url
    }
    VectorSearchWorker --> "REST" ToolsInventoryVectorSearchAPI : calls
```
- `VectorSearchWorker` là entrypoint phía Core Workers, nhận request search, gọi API sang Tools Inventory.
- Giao tiếp với Tools Inventory qua HTTP REST.

## 2. Tools Inventory Vector Search Services
```mermaid
classDiagram
    class VectorSearchTool {
        +search(query, collections)
        +search_and_merge(query, collections, final_top_k)
        +get_available_collections()
        +health_check()
        -embedding_tool
        -collection_manager
    }
    class APICollectionManager {
        +search(collection_name, vector, limit)
        +collection_names
    }
    VectorSearchTool --> OpenAIEmbeddingTool : sử dụng
    VectorSearchTool --> APICollectionManager : sử dụng
    APICollectionManager --> "REST" ai_databases : calls
```
- `VectorSearchTool` wrap logic search, merge, mapping collection, gọi embedding, gọi ai_databases.
- Có thể mở rộng thêm các provider vector search khác.

## 3. Liên kết với các component khác
- VectorSearchWorker được gọi bởi **Core Workflows** (retrieval workflow), hoặc sau Embedding.
- Kết quả search là đầu vào cho Rerank, LLM QA, Specs, hoặc trả về user.
- Các tool vector search phía Tools Inventory cũng được các worker khác gọi tương tự.

---

> Xem thêm các file C4 Level 4 khác cho LLM, Parser, Embedding, Rerank để hiểu toàn bộ kiến trúc code. 