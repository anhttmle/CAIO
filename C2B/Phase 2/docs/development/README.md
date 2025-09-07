# Development Documentation

## 📋 Mục lục

- [Setup & Installation](./setup.md)
- [Development Workflow](./workflow.md)
- [Testing](./testing.md)
- [Deployment](./deployment.md)
- [Troubleshooting](./troubleshooting.md)

## 🎯 Mục đích

Tài liệu này hướng dẫn developers về cách setup, develop, test và deploy hệ thống COBOL Assistant.

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- Python 3.8+
- Git

### Setup
```bash
# Clone repository
git clone <repository-url>
cd NewRepository

# Start services
docker-compose up -d

# Check health
curl http://localhost:8000/health
```

### Access Points
- **Webapp**: http://localhost:8501
- **API Gateway**: http://localhost:8000
- **API Docs**: http://localhost:8000/docs

## 🔧 Development Workflow

### 1. Local Development
```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f <service-name>

# Stop services
docker-compose down
```

### 2. Service Development
```bash
# Work on specific service
cd api_gateway
pip install -r requirements.txt
uvicorn main:app --reload

# Test service
curl http://localhost:8000/health
```

### 3. Database Access
- **PostgreSQL**: `docker-compose exec postgres psql -U cobol -d cobol_assistant`
- **Milvus**: Access via Attu UI at http://localhost:3000

## 🧪 Testing

### Unit Tests
```bash
# Run tests for specific service
cd tools_inventory
python -m pytest tests/

# Run all tests
python -m pytest tests/ -v
```

### Integration Tests
```bash
# Test API endpoints
curl -X POST http://localhost:8000/core-workflows/indexing/index-zip \
  -F "zip_file=@test_files.zip"

# Test health checks
curl http://localhost:8000/health
```

### End-to-End Tests
```bash
# Run E2E tests
python tests/e2e/test_full_workflow.py
```

## 🚀 Deployment

### Development Deployment
```bash
# Build and start
docker-compose up --build -d

# Check status
docker-compose ps
```

### Production Deployment
```bash
# Use production compose file
docker-compose -f docker-compose.prod.yml up -d

# Set environment variables
export OPENAI_API_KEY=your_key
export COHERE_API_KEY=your_key
```

## 🔍 Troubleshooting

### Common Issues

#### 1. Service Won't Start
```bash
# Check logs
docker-compose logs <service-name>

# Check dependencies
docker-compose ps

# Restart service
docker-compose restart <service-name>
```

#### 2. Database Connection Issues
```bash
# Check database status
docker-compose exec postgres pg_isready

# Check Milvus status
docker-compose exec standalone milvus status
```

#### 3. API Gateway Issues
```bash
# Check service health
curl http://localhost:8000/health

# Check service connectivity
curl http://localhost:8000/ai-databases/health
```

### Debug Commands
```bash
# Access service shell
docker-compose exec <service-name> /bin/bash

# Check service logs
docker-compose logs -f <service-name>

# Check resource usage
docker stats
```

## 📊 Monitoring

### Health Checks
- **API Gateway**: `GET /health`
- **AI Databases**: `GET /ai-databases/health`
- **Core Workers**: `GET /core-workers/health`
- **Core Workflows**: `GET /core-workflows/health`
- **Tools Inventory**: `GET /tools-inventory/health`

### Logs
- **Location**: `/app/shared/logs/`
- **Format**: Structured JSON
- **Rotation**: Daily rotation

### Metrics
- **Request Count**: Total requests per service
- **Response Time**: Average response time
- **Error Rate**: Error percentage
- **Memory Usage**: Memory consumption per service

## 🔗 Liên kết

- [Setup & Installation](./setup.md) - Detailed setup instructions
- [Development Workflow](./workflow.md) - Development best practices
- [Testing](./testing.md) - Testing strategies and tools
- [Deployment](./deployment.md) - Deployment procedures
- [Troubleshooting](./troubleshooting.md) - Common issues and solutions
