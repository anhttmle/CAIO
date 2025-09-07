# Setup & Installation

## 🎯 Mục đích

Hướng dẫn chi tiết về cách setup và cài đặt hệ thống COBOL Assistant cho development và production.

## 📋 Prerequisites

### System Requirements
- **OS**: Linux, macOS, Windows (with WSL2)
- **RAM**: Minimum 8GB, Recommended 16GB
- **Storage**: Minimum 10GB free space
- **CPU**: 4+ cores recommended

### Software Requirements
- **Docker**: Version 20.10+
- **Docker Compose**: Version 2.0+
- **Git**: Version 2.0+
- **Python**: Version 3.8+ (for local development)

## 🚀 Quick Setup

### 1. Clone Repository
```bash
git clone <repository-url>
cd NewRepository
```

### 2. Environment Configuration
```bash
# Copy environment template
cp .env.template .env

# Edit environment variables
nano .env
```

### 3. Start Services
```bash
# Start all services
docker-compose up -d

# Check status
docker-compose ps
```

### 4. Verify Installation
```bash
# Check API Gateway
curl http://localhost:8000/health

# Check Webapp
curl http://localhost:8501
```

## 🔧 Detailed Setup

### Environment Variables

#### Required Variables
```bash
# Database Configuration
POSTGRES_HOST=postgres
POSTGRES_PORT=5432
POSTGRES_USER=cobol
POSTGRES_PASSWORD=your_password
POSTGRES_DB=cobol_assistant

# Milvus Configuration
MILVUS_HOST=standalone
MILVUS_PORT=19530

# Redis Configuration
REDIS_URL=redis://redis:6379/0

# API Keys
OPENAI_API_KEY=your_openai_key
COHERE_API_KEY=your_cohere_key
```

#### Optional Variables
```bash
# Service URLs (for local development)
API_BASE_URL=http://localhost:8000
AI_DATABASES_URL=http://localhost:8001
CORE_WORKERS_URL=http://localhost:8002
CORE_WORKFLOWS_URL=http://localhost:8003
TOOLS_INVENTORY_URL=http://localhost:8004

# Logging
LOG_LEVEL=INFO
LOG_FILE=/app/shared/logs

# Performance
MAX_CONCURRENT_REQUESTS=100
BATCH_SIZE=100
CHUNK_SIZE=6000
```

### Docker Services

#### Service Ports
| Service | Port | Description |
|---------|------|-------------|
| API Gateway | 8000 | Main API endpoint |
| AI Databases | 8001 | Database service |
| Core Workers | 8002 | Business logic |
| Core Workflows | 8003 | Workflow orchestration |
| Tools Inventory | 8004 | Tool implementations |
| Webapp | 8501 | User interface |
| PostgreSQL | 5432 | Database |
| Milvus | 19530 | Vector database |
| Redis | 6379 | Cache/Queue |
| Attu | 3000 | Milvus UI |
| pgAdmin | 5050 | PostgreSQL UI |

#### Service Dependencies
```yaml
api-gateway:
  depends_on:
    - core-workers
    - core-workflows
    - tools-inventory
    - ai-databases

core-workers:
  depends_on:
    - tools-inventory
    - ai-databases

core-workflows:
  depends_on:
    - core-workers
    - ai-databases
    - redis

ai-databases:
  depends_on:
    - postgres
    - standalone
```

## 🧪 Development Setup

### Local Development

#### 1. Start Infrastructure
```bash
# Start only infrastructure services
docker-compose up -d postgres standalone redis

# Wait for services to be ready
docker-compose logs -f postgres
docker-compose logs -f standalone
```

#### 2. Run Services Locally
```bash
# API Gateway
cd api_gateway
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000

# Core Workers
cd core_workers
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8002

# Other services...
```

#### 3. Environment Variables for Local Development
```bash
# Set environment variables
export POSTGRES_HOST=localhost
export MILVUS_HOST=localhost
export REDIS_URL=redis://localhost:6379/0
```

### IDE Setup

#### VS Code
```json
{
  "python.defaultInterpreterPath": "./venv/bin/python",
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true,
  "python.formatting.provider": "black",
  "files.exclude": {
    "**/__pycache__": true,
    "**/.pytest_cache": true
  }
}
```

#### PyCharm
- Configure Python interpreter
- Set up run configurations for each service
- Configure debugging settings

## 🚀 Production Setup

### Production Environment

#### 1. Security Configuration
```bash
# Use strong passwords
POSTGRES_PASSWORD=strong_random_password
REDIS_PASSWORD=strong_random_password

# Use HTTPS
API_BASE_URL=https://your-domain.com

# Configure CORS
CORS_ORIGINS=https://your-domain.com
```

#### 2. Resource Limits
```yaml
services:
  api-gateway:
    deploy:
      resources:
        limits:
          memory: 512M
          cpus: '0.5'
        reservations:
          memory: 256M
          cpus: '0.25'
```

#### 3. Health Checks
```yaml
services:
  api-gateway:
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

### Monitoring Setup

#### 1. Logging
```yaml
services:
  api-gateway:
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
```

#### 2. Metrics Collection
```yaml
services:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./monitoring/prometheus.yml:/etc/prometheus/prometheus.yml
```

## 🔍 Troubleshooting

### Common Setup Issues

#### 1. Port Conflicts
```bash
# Check port usage
netstat -tulpn | grep :8000

# Kill process using port
sudo kill -9 <PID>
```

#### 2. Docker Issues
```bash
# Clean up Docker
docker system prune -a

# Rebuild images
docker-compose build --no-cache
```

#### 3. Database Connection Issues
```bash
# Check database status
docker-compose exec postgres pg_isready

# Check Milvus status
docker-compose exec standalone milvus status
```

#### 4. Memory Issues
```bash
# Check memory usage
docker stats

# Increase Docker memory limit
# Docker Desktop -> Settings -> Resources -> Memory
```

### Debug Commands

#### Service Health
```bash
# Check all services
docker-compose ps

# Check specific service logs
docker-compose logs -f api-gateway

# Check service health
curl http://localhost:8000/health
```

#### Database Access
```bash
# PostgreSQL
docker-compose exec postgres psql -U cobol -d cobol_assistant

# Milvus (via Attu)
# Open http://localhost:3000 in browser
```

#### Service Shell Access
```bash
# Access service container
docker-compose exec api-gateway /bin/bash

# Run commands inside container
docker-compose exec api-gateway python -c "print('Hello')"
```

## ✅ Verification

### 1. Service Health Checks
```bash
# API Gateway
curl http://localhost:8000/health

# AI Databases
curl http://localhost:8000/ai-databases/health

# Core Workers
curl http://localhost:8000/core-workers/health

# Core Workflows
curl http://localhost:8000/core-workflows/health

# Tools Inventory
curl http://localhost:8000/tools-inventory/health
```

### 2. Database Connectivity
```bash
# PostgreSQL
docker-compose exec postgres psql -U cobol -d cobol_assistant -c "SELECT 1;"

# Milvus
curl http://localhost:19530/health
```

### 3. Webapp Access
```bash
# Open browser
open http://localhost:8501
```

## 🔗 Liên kết

- [Development Workflow](./workflow.md) - Development best practices
- [Testing](./testing.md) - Testing setup and procedures
- [Deployment](./deployment.md) - Production deployment
- [Troubleshooting](./troubleshooting.md) - Common issues and solutions
