
# 1. Context:

```mermaid

    graph TB
    subgraph Users
        SME["SME (Software Engineer)<br>Understands source code"]
        BA["BA (Business Analyst)<br>Understands business logic"]
    end

    subgraph Assistant_System["Assistant System (Local Deployment)"]
        Assistant["Assistant"]
    end

    SME -->|Uploads repo, reviews knowledge| Assistant
    BA -->|Asks questions| Assistant


```

- SME tương tác với Assistant để upload source code, kiểm tra kiến thức mà AI xây dựng và tinh chỉnh lại.
- BA sử dụng Assistant để đặt câu hỏi và tạo tài liệu dựa trên tri thức được xây dựng.
- Assistant hoạt động cục bộ (Local), không kết nối với hệ thống ngoài.

# 2. Component:

```mermaid

graph TB
    subgraph LUser["User Layer"]
        SME["SME (Software Engineer)"]
        BA["BA (Business Analyst)"]
    end

    subgraph LFrontend["Frontend Layer"]
        WebApp["WebApp (Chat Interface)"]
    end

    subgraph LAPI["API Layer"]
        APIGateway["API Gateway (Integration Point)"]
    end

    subgraph LService["Service Layer"]
        AICore["AI Core Service<br>(Indexing, RAG Control, Tool Calls)"]
        RAGPlatform["RAG Platform<br>(e.g., Dify, LangGraph)"]
        ToolInventory["Tool Inventory<br>(MCP Tool Server)"]
        Worker["Task Queue / Worker Pool"]
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
    
    WebApp --> APIGateway
    APIGateway --> AICore

    LService --> LExternal

    AICore --> RAGPlatform
    RAGPlatform --> ToolInventory
    AICore --> Worker
    Worker --> ToolInventory

    ToolInventory --> LData
    ToolInventory --> LExternal
    RAGPlatform --> LExternal

```

# 3. Component

```mermaid

graph TB
    subgraph LUser["User Layer"]
        SME["SME (Software Engineer)"]
        BA["BA (Business Analyst)"]
    end

    subgraph LFrontend["Frontend Layer"]
        WebApp["WebApp (Chat Interface)"]
    end

    subgraph LAPI["API Layer"]
        APIGateway["API Gateway (Integration Point)"]
    end

    subgraph LService["Service Layer"]
        subgraph AICore["AI Core Service"]
            IndexFlow["IndexFlow Manager"]
            SpecGenFlow["SpecGenFlow Manager"]
            RetrievalFlow["RetrievalFlow Manager"]
            Worker["Task Queue / Worker Pool"]
        end

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
    WebApp --> APIGateway

    APIGateway --> IndexFlow
    APIGateway --> SpecGenFlow
    APIGateway --> RetrievalFlow

    IndexFlow --> Worker
    SpecGenFlow --> RAGPlatform
    RetrievalFlow --> RAGPlatform
    Worker --> ToolInventory

    RAGPlatform --> LExternal
    RAGPlatform --> ToolInventory

    ToolInventory --> LData
    ToolInventory --> LExternal


```

- IndexFlow Manager
    - Workflow for indexing Repo source code
    - Workflow for indexing Generated Specs
    - 

RAG Orchestrator

Task Queue / Worker Pool
