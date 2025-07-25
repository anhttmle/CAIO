# C4 Architecture - COBOL AI Assistant (Microservices)

## 1. Context Diagram
Hệ thống COBOL AI Assistant phục vụ người dùng cuối (developer, analyst) thao tác với code COBOL/COPY/JCL qua giao diện web, sử dụng các dịch vụ AI, lưu trữ, và workflow tự động.

```mermaid
graph TD
    User["User (Dev/Analyst)"]
    Webapp["Webapp (Streamlit UI)"]
    APIGW["API Gateway"]
    CoreWorkers["Core Workers"]
    CoreWorkflows["Core Workflows"]
    Tools["Tools Inventory"]
    DB["AI Databases (Milvus, Postgres)"]
    Shared["Shared Storage"]

    User-->|HTTP|Webapp
    Webapp-->|REST|APIGW
    APIGW-->|REST|CoreWorkers
    APIGW-->|REST|CoreWorkflows
    APIGW-->|REST|Tools
    APIGW-->|REST|DB
    CoreWorkers-->|REST|Tools
    CoreWorkers-->|REST|DB
    CoreWorkflows-->|REST|CoreWorkers
    CoreWorkflows-->|REST|DB
    CoreWorkers-->|Mount|Shared
    CoreWorkflows-->|Mount|Shared
    Tools-->|Mount|Shared
    DB-->|Mount|Shared
    Webapp-->|Mount|Shared
```

---

## 2. Container Diagram
Các container chính trong hệ thống:
- **Webapp**: Giao diện người dùng, upload, chat, xem kết quả.
- **API Gateway**: Route request, bảo vệ, hợp nhất API.
- **Core Workers**: Xử lý parser, embedding, LLM, rerank, vector search.
- **Core Workflows**: Orchestrate các workflow phức tạp (indexing, retrieval, QA, specs).
- **Tools Inventory**: API hóa các tool parser, embedding, LLM, rerank, chunker.
- **AI Databases**: Milvus (vector DB), Postgres (metadata, specs, feedback).
- **Shared Storage**: Mount chung cho log, models, file tạm, upload.

```mermaid
graph LR
    subgraph User
        A["Web Browser"]
    end
    subgraph Frontend
        B["Webapp (Streamlit)"]
    end
    subgraph Backend
        C["API Gateway"]
        D["Core Workers"]
        E["Core Workflows"]
        F["Tools Inventory"]
        G["AI Databases"]
    end
    subgraph Storage
        H["Shared Volume"]
    end
    A-->|HTTP|B
    B-->|REST|C
    C-->|REST|D
    C-->|REST|E
    C-->|REST|F
    C-->|REST|G
    D-->|REST|F
    D-->|REST|G
    E-->|REST|D
    E-->|REST|G
    D-->|Mount|H
    E-->|Mount|H
    F-->|Mount|H
    G-->|Mount|H
    B-->|Mount|H
```

---

## 3. Component Diagram (ví dụ: Core Workers)
Các component chính trong Core Workers:
- **Parser**: Phân tích file COBOL, COPY, JCL, TEXT thành các chunk.
- **Embedding**: Sinh embedding cho chunk/text.
- **LLM Services**: Gọi LLM sinh summary, QA, specs.
- **Rerank**: Rerank kết quả search.
- **Vector Search**: Tìm kiếm vector DB.

```mermaid
graph TD
    CoreWorkers["Core Workers"]
    Parser["Parser Component"]
    Embedding["Embedding Component"]
    LLM["LLM Services Component"]
    Rerank["Rerank Component"]
    VectorSearch["Vector Search Component"]
    CoreWorkers-->|API|Parser
    CoreWorkers-->|API|Embedding
    CoreWorkers-->|API|LLM
    CoreWorkers-->|API|Rerank
    CoreWorkers-->|API|VectorSearch
    Parser-->|Call|ToolsInventory
    Embedding-->|Call|ToolsInventory
    LLM-->|Call|ToolsInventory
    Rerank-->|Call|ToolsInventory
    VectorSearch-->|Call|ToolsInventory
```

---

## 4. Deployment Diagram
Triển khai hệ thống bằng Docker Compose, mỗi service là một container độc lập, mount chung shared volume.

```mermaid
graph TD
    subgraph Host
        subgraph Docker
            WebappC["Webapp Container"]
            APIGWC["API Gateway Container"]
            CoreWorkersC["Core Workers Container"]
            CoreWorkflowsC["Core Workflows Container"]
            ToolsC["Tools Inventory Container"]
            AIDBC["AI Databases Container"]
            PostgresC["Postgres Container"]
            MilvusC["Milvus Container"]
            MinioC["Minio Container"]
            EtcdC["Etcd Container"]
            AttuC["Attu Dashboard"]
            RedisC["Redis Container"]
            CeleryC["Celery Worker"]
        end
        SharedV["Shared Volume"]
    end
    WebappC-->|Mount|SharedV
    APIGWC-->|Mount|SharedV
    CoreWorkersC-->|Mount|SharedV
    CoreWorkflowsC-->|Mount|SharedV
    ToolsC-->|Mount|SharedV
    AIDBC-->|Mount|SharedV
    PostgresC-->|Mount|SharedV
    MilvusC-->|Mount|SharedV
    MinioC-->|Mount|SharedV
    EtcdC-->|Mount|SharedV
    AttuC-->|Mount|SharedV
    RedisC-->|Mount|SharedV
    CeleryC-->|Mount|SharedV
```

---

> Tài liệu này mô tả kiến trúc C4 cho hệ thống COBOL AI Assistant dựa trên microservices. Xem thêm chi tiết các flow, API, models trong các file khác của BotDocs. 