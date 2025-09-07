# COBOL Assistant - Documentation Hub

## 🏗️ Tổng quan hệ thống

COBOL Assistant là một hệ thống AI hỗ trợ phân tích và tài liệu hóa mã COBOL, được xây dựng theo kiến trúc microservices với các công nghệ AI hiện đại.

### 🎯 Mục đích chính
- Phân tích và chunking mã COBOL, COPY, JCL
- Tạo embedding và lưu trữ trong vector database (Milvus)
- Tạo tài liệu kỹ thuật tự động (wiki)
- Hỗ trợ Q&A thông minh về mã nguồn
- Quản lý metadata trong PostgreSQL

## 📚 Cấu trúc tài liệu

### 1. 🏛️ [Kiến trúc hệ thống](./architecture/README.md)
- [Tổng quan kiến trúc](./architecture/overview.md)
- [Microservices Architecture](./architecture/microservices.md)
- [Database Design](./architecture/databases.md)
- [API Design](./architecture/apis.md)
- [Security Architecture](./architecture/security.md)

### 2. 🔧 [Services](./services/README.md)
- [API Gateway](./services/api-gateway.md)
- [AI Databases](./services/ai-databases.md)
- [Core Workers](./services/core-workers.md)
- [Core Workflows](./services/core-workflows.md)
- [Tools Inventory](./services/tools-inventory.md)
- [Webapp](./services/webapp.md)

### 3. 🔄 [Workflows](./workflows/README.md)
- [Indexing Workflow](./workflows/indexing.md)
- [Specs Generation](./workflows/specs-generation.md)
- [QA Workflow](./workflows/qa.md)
- [Retrieval Workflow](./workflows/retrieval.md)
- [Task Processing](./workflows/tasks.md)

### 4. 🛠️ [Technical Implementation](./technical/README.md)
- [Parsers](./technical/parsers.md)
- [Embedding System](./technical/embeddings.md)
- [Vector Search](./technical/vector-search.md)
- [LLM Services](./technical/llm-services.md)
- [Database Operations](./technical/database-ops.md)

### 5. 🚀 [Development](./development/README.md)
- [Setup & Installation](./development/setup.md)
- [Development Workflow](./development/workflow.md)
- [Testing](./development/testing.md)
- [Deployment](./development/deployment.md)
- [Troubleshooting](./development/troubleshooting.md)

### 6. 📊 [Operations](./operations/README.md)
- [Monitoring](./operations/monitoring.md)
- [Logging](./operations/logging.md)
- [Performance](./operations/performance.md)
- [Maintenance](./operations/maintenance.md)

## 🗺️ Navigation Guide

### Cho Developer mới
1. Bắt đầu với [Kiến trúc tổng quan](./architecture/overview.md)
2. Đọc [Setup & Installation](./development/setup.md)
3. Khám phá [Services](./services/README.md)
4. Hiểu [Workflows](./workflows/README.md)

### Cho System Architect
1. [Kiến trúc hệ thống](./architecture/README.md)
2. [Database Design](./architecture/databases.md)
3. [API Design](./architecture/apis.md)
4. [Security Architecture](./architecture/security.md)

### Cho Developer
1. [Development Workflow](./development/workflow.md)
2. [Technical Implementation](./technical/README.md)
3. [Testing](./development/testing.md)
4. [Troubleshooting](./development/troubleshooting.md)

### Cho DevOps
1. [Deployment](./development/deployment.md)
2. [Operations](./operations/README.md)
3. [Monitoring](./operations/monitoring.md)
4. [Performance](./operations/performance.md)

## 🔗 Quick Links

- [Technical Debt Report](../TECHNICAL_DEBT_REPORT.md)
- [Developer Documentation](../DEVELOPER_DOCUMENTATION.md)
- [API Reference](./api-reference/README.md)
- [Troubleshooting Guide](./development/troubleshooting.md)

## 📝 Cập nhật tài liệu

Tài liệu này được cập nhật thường xuyên. Nếu bạn tìm thấy thông tin không chính xác hoặc thiếu sót, vui lòng:
1. Tạo issue trong repository
2. Submit pull request với cập nhật
3. Liên hệ team lead

---

**Last Updated**: $(date)
**Version**: 1.0.0
**Maintainer**: Development Team