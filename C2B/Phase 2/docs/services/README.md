# Services Documentation

## 📋 Mục lục

- [API Gateway](./api-gateway.md)
- [AI Databases](./ai-databases.md)
- [Core Workers](./core-workers.md)
- [Core Workflows](./core-workflows.md)
- [Tools Inventory](./tools-inventory.md)
- [Webapp](./webapp.md)

## 🎯 Mục đích

Tài liệu này mô tả chi tiết từng service trong hệ thống COBOL Assistant, bao gồm:
- Chức năng và responsibilities
- API endpoints
- Configuration
- Dependencies
- Implementation details

## 🏗️ Service Overview

### Service Hierarchy

```
┌─────────────────┐
│   Webapp        │ ← User Interface
└─────────────────┘
         │
         ▼
┌─────────────────┐
│   API Gateway   │ ← Central Entry Point
└─────────────────┘
         │
         ├─── Core Workers ← Business Logic
         ├─── Core Workflows ← Orchestration
         ├─── Tools Inventory ← Tool Implementations
         └─── AI Databases ← Data Management
```

### Service Responsibilities

| Service | Primary Responsibility | Port | Dependencies |
|---------|----------------------|------|--------------|
| **Webapp** | User Interface | 8501 | API Gateway |
| **API Gateway** | Request Routing | 8000 | All Services |
| **Core Workers** | Business Logic | 8002 | Tools Inventory, AI Databases |
| **Core Workflows** | Orchestration | 8003 | Core Workers, AI Databases, Redis |
| **Tools Inventory** | Tool Implementations | 8004 | AI Databases, External APIs |
| **AI Databases** | Data Management | 8001 | Milvus, PostgreSQL |

## 🔄 Service Interactions

### Request Flow
1. **User** → Webapp
2. **Webapp** → API Gateway
3. **API Gateway** → Appropriate Service
4. **Service** → Tools Inventory (if needed)
5. **Service** → AI Databases (if needed)
6. **Response** → User

### Data Flow
1. **File Upload** → Core Workflows → Core Workers → Tools Inventory → AI Databases
2. **QA Request** → Core Workflows → Core Workers → AI Databases
3. **Specs Generation** → Core Workflows → Tools Inventory → AI Databases

## 📊 Service Metrics

### Performance Targets
- **API Response Time**: <100ms
- **File Processing**: <30s per file
- **Vector Search**: <500ms
- **Embedding Generation**: <2s

### Scalability
- **Horizontal Scaling**: All services support horizontal scaling
- **Load Balancing**: API Gateway provides load balancing
- **Resource Management**: Each service has resource limits

## 🔗 Quick Navigation

### For Developers
- [Core Workers](./core-workers.md) - Business logic implementation
- [Tools Inventory](./tools-inventory.md) - Tool implementations
- [AI Databases](./ai-databases.md) - Database operations

### For System Administrators
- [API Gateway](./api-gateway.md) - Central routing
- [Core Workflows](./core-workflows.md) - Workflow orchestration
- [Webapp](./webapp.md) - User interface

### For DevOps
- [Service Configuration](./configuration.md) - Service configuration
- [Deployment](./deployment.md) - Deployment strategies
- [Monitoring](./monitoring.md) - Service monitoring
