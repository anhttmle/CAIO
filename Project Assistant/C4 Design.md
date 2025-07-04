

# 1. Context:

```mermaid

    graph TB
    subgraph Users
        SME["SME (Software Engineer)<br>Understands source code"]
        BA["BA (Business Analyst)<br>Understands business logic"]
    end

    subgraph Assistant_System["Assistant System"]
        Assistant["Assistant"]
    end

    SME -->|Uploads repo, reviews knowledge| Assistant
    BA -->|Asks questions| Assistant


```

- SME tương tác với Assistant để upload source code, kiểm tra kiến thức mà AI xây dựng và tinh chỉnh lại.
- BA sử dụng Assistant để đặt câu hỏi và tạo tài liệu dựa trên tri thức được xây dựng.
- Assistant hoạt động cục bộ (Local), không kết nối với hệ thống ngoài.

# 2. Container:

```mermaid

graph TB
    subgraph LUser["User Layer"]
        SME["SME (Software Engineer)"]
        BA["BA (Business Analyst)"]
    end

    subgraph LFrontend["Frontend Layer"]
        WebApp["WebApp (Chat Interface)"]
    end

    subgraph LAPI["API Gateway"]
        BE["Backend Service (Integration Point)"]
    end

    subgraph LService["Service Layer"]
        AI["AI Core Service<br>(Indexing, RAG Control, Tool Calls)"]
        Worker["Task Queue / Worker Pool"]
        RAGPlatform["RAG Platform<br>(e.g., Dify, LangGraph)"]
        ToolInventory["Tool Inventory<br>(MCP Tool Server)"]
    end

    subgraph LData["Data Layer"]
        RelDB["Relational DB"]
        VecDB["Vector DB"]
        GraphDB["Graph DB"]
        TextDB["Text DB"]
    end

    subgraph LExternal["External Services"]
        OpenAI["OpenAI"]
        Gemini["Gemini"]
        Cohere["Cohere"]
    end

    LUser --> LFrontend
    WebApp --> LAPI
    LAPI --> AI

    AI --> RAGPlatform
    AI --> Worker
    Worker --> ToolInventory
    RAGPlatform --> ToolInventory

    ToolInventory --> LData
    ToolInventory --> LExternal
    RAGPlatform --> LExternal

```

# 3. Component

- [3.1 - Web App (Chat Interface)](3.1-WebApp.md)
- [3.2 - API Gateway (Backend Service)](3.2-APIGateway.md)
- [3.3 - AI Core Service](3.3-AICoreService.md)
- [3.4 - Task Queue / Worker Pool](3.4-TaskQueueWorkerPool.md)
- [3.5 - RAG Platform](3.5-RAGPlatform.md)
- [3.6 - Tool Inventory (MCP Tool Server)](3.6-ToolInventory.md)
- [3.7 - Data Layer](3.7-DataLayer.md)
- [3.8 - External Services](3.8-ExternalServices.md)



