# Troubleshooting

## 🎯 Mục đích

Tài liệu này cung cấp hướng dẫn troubleshooting cho hệ thống COBOL Assistant, bao gồm common issues, error messages, và solutions.

## 🔍 Common Issues

### Service Startup Issues

#### Issue: Services fail to start
**Symptoms:**
- Docker containers exit immediately
- Health checks fail
- Services return 500 errors

**Causes:**
- Missing environment variables
- Database connection issues
- Port conflicts
- Missing dependencies

**Solutions:**
```bash
# 1. Check environment variables
docker-compose config

# 2. Check service logs
docker-compose logs service-name

# 3. Verify database connectivity
docker-compose exec postgres psql -U cobol -d cobol_assistant -c "SELECT 1;"

# 4. Check port availability
netstat -tulpn | grep :8000

# 5. Restart services
docker-compose down
docker-compose up -d
```

#### Issue: Database connection errors
**Symptoms:**
- "Connection refused" errors
- "Database not found" errors
- Timeout errors

**Solutions:**
```bash
# 1. Check database status
docker-compose ps postgres

# 2. Check database logs
docker-compose logs postgres

# 3. Verify connection string
echo $POSTGRES_HOST
echo $POSTGRES_PORT
echo $POSTGRES_USER
echo $POSTGRES_DB

# 4. Test connection
docker-compose exec postgres psql -h localhost -U cobol -d cobol_assistant

# 5. Reset database
docker-compose down -v
docker-compose up -d postgres
```

### API Issues

#### Issue: API Gateway returns 502 errors
**Symptoms:**
- 502 Bad Gateway errors
- Service unavailable errors
- Timeout errors

**Solutions:**
```bash
# 1. Check API Gateway logs
docker-compose logs api-gateway

# 2. Check backend services
curl http://localhost:8001/health  # AI Databases
curl http://localhost:8002/health  # Core Workers
curl http://localhost:8003/health  # Core Workflows
curl http://localhost:8004/health  # Tools Inventory

# 3. Check service dependencies
docker-compose ps

# 4. Restart API Gateway
docker-compose restart api-gateway
```

#### Issue: Authentication failures
**Symptoms:**
- 401 Unauthorized errors
- Login failures
- Session timeouts

**Solutions:**
```bash
# 1. Check authentication service
docker-compose logs webapp

# 2. Verify credentials
cat webapp/credentials.yaml

# 3. Check session configuration
grep -r "session" webapp/

# 4. Clear browser cache and cookies
# 5. Restart webapp service
docker-compose restart webapp
```

### File Processing Issues

#### Issue: File upload failures
**Symptoms:**
- Upload timeout errors
- File too large errors
- Invalid file type errors

**Solutions:**
```bash
# 1. Check file size limits
grep -r "max_file_size" .

# 2. Check disk space
df -h

# 3. Check upload directory permissions
ls -la shared/uploads/

# 4. Check file type validation
grep -r "file_type" tools_inventory/parsers/

# 5. Test with smaller files
```

#### Issue: Parsing errors
**Symptoms:**
- Parser crashes
- Invalid output format
- Missing chunks

**Solutions:**
```bash
# 1. Check parser logs
docker-compose logs core-workers

# 2. Test parser with sample file
python -c "
from tools_inventory.parsers.cobol_parser import CobolParserTool
parser = CobolParserTool()
result = parser.parse('test.cbl', 'IDENTIFICATION DIVISION.\\nPROGRAM-ID. TEST.')
print(result)
"

# 3. Check file encoding
file -i your_file.cbl

# 4. Verify parser configuration
grep -r "max_chunk_size" .
```

### Vector Search Issues

#### Issue: Search returns no results
**Symptoms:**
- Empty search results
- Low relevance scores
- Search timeouts

**Solutions:**
```bash
# 1. Check Milvus status
docker-compose logs standalone

# 2. Verify collection exists
curl http://localhost:8001/vector/collections

# 3. Check embedding generation
curl -X POST http://localhost:8002/embedding/generate \
  -H "Content-Type: application/json" \
  -d '{"content": "test", "file_path": "test.cbl"}'

# 4. Verify search parameters
grep -r "search_params" .

# 5. Check index status
curl http://localhost:8001/vector/collections/sections/stats
```

#### Issue: Embedding generation failures
**Symptoms:**
- OpenAI API errors
- Invalid embedding format
- Timeout errors

**Solutions:**
```bash
# 1. Check OpenAI API key
echo $OPENAI_API_KEY

# 2. Test API connectivity
curl -H "Authorization: Bearer $OPENAI_API_KEY" \
  https://api.openai.com/v1/models

# 3. Check rate limits
grep -r "rate_limit" .

# 4. Verify model configuration
grep -r "text-embedding-3-small" .

# 5. Check network connectivity
ping api.openai.com
```

### Performance Issues

#### Issue: Slow response times
**Symptoms:**
- High latency
- Timeout errors
- Resource exhaustion

**Solutions:**
```bash
# 1. Check system resources
docker stats

# 2. Check service logs for errors
docker-compose logs --tail=100

# 3. Monitor database performance
docker-compose exec postgres psql -U cobol -d cobol_assistant -c "
SELECT query, mean_time, calls 
FROM pg_stat_statements 
ORDER BY mean_time DESC 
LIMIT 10;
"

# 4. Check Redis performance
docker-compose exec redis redis-cli info stats

# 5. Optimize configuration
grep -r "timeout" .
grep -r "pool_size" .
```

#### Issue: Memory issues
**Symptoms:**
- Out of memory errors
- Container restarts
- Slow performance

**Solutions:**
```bash
# 1. Check memory usage
docker stats --no-stream

# 2. Increase memory limits
# In docker-compose.yml:
# services:
#   service-name:
#     mem_limit: 2g

# 3. Check for memory leaks
docker-compose exec service-name python -c "
import psutil
print(f'Memory usage: {psutil.virtual_memory().percent}%')
"

# 4. Optimize chunk size
grep -r "max_chunk_size" .

# 5. Restart services
docker-compose restart
```

## 🚨 Error Messages

### Database Errors

#### Error: "Connection refused"
**Message:** `psycopg2.OperationalError: connection to server at "postgres" (172.18.0.2), port 5432 failed: Connection refused`

**Solution:**
```bash
# 1. Check if PostgreSQL is running
docker-compose ps postgres

# 2. Start PostgreSQL if not running
docker-compose up -d postgres

# 3. Wait for PostgreSQL to be ready
sleep 30

# 4. Test connection
docker-compose exec postgres psql -U cobol -d cobol_assistant -c "SELECT 1;"
```

#### Error: "Database does not exist"
**Message:** `psycopg2.OperationalError: FATAL: database "cobol_assistant" does not exist`

**Solution:**
```bash
# 1. Create database
docker-compose exec postgres psql -U cobol -c "CREATE DATABASE cobol_assistant;"

# 2. Or reset database
docker-compose down -v
docker-compose up -d postgres
```

### API Errors

#### Error: "Service unavailable"
**Message:** `HTTPException: 503 Service Unavailable`

**Solution:**
```bash
# 1. Check service status
curl http://localhost:8000/health

# 2. Check service logs
docker-compose logs service-name

# 3. Restart service
docker-compose restart service-name

# 4. Check dependencies
docker-compose ps
```

#### Error: "Request timeout"
**Message:** `httpx.TimeoutException: Request timeout`

**Solution:**
```bash
# 1. Check timeout configuration
grep -r "timeout" .

# 2. Increase timeout values
# In configuration:
# timeout = 120.0

# 3. Check network connectivity
ping target-service

# 4. Check service performance
docker stats
```

### File Processing Errors

#### Error: "File too large"
**Message:** `ValueError: File too large`

**Solution:**
```bash
# 1. Check file size limits
grep -r "max_file_size" .

# 2. Increase limits
# In configuration:
# max_file_size = 100 * 1024 * 1024  # 100MB

# 3. Split large files
# Use file splitting tools

# 4. Check available disk space
df -h
```

#### Error: "Invalid file type"
**Message:** `ValueError: Invalid file type`

**Solution:**
```bash
# 1. Check file type validation
grep -r "file_type" tools_inventory/parsers/

# 2. Add support for new file type
# In parser factory:
# if extension in [".new_ext"]:
#     return "NEW_TYPE"

# 3. Check file extension
file your_file

# 4. Verify parser configuration
```

## 🔧 Debugging Tools

### Logging Configuration

#### Enable Debug Logging
```python
# In main.py
import logging

logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('/app/shared/debug.log'),
        logging.StreamHandler()
    ]
)
```

#### Service-Specific Logging
```python
# In each service
import logging

logger = logging.getLogger(__name__)

# Debug logging
logger.debug(f"Processing file: {file_path}")
logger.info(f"File processed successfully: {file_path}")
logger.warning(f"Low relevance score: {score}")
logger.error(f"Processing failed: {error}")
```

### Monitoring Commands

#### Check Service Health
```bash
#!/bin/bash
# health-check.sh

services=("api-gateway" "ai-databases" "core-workers" "core-workflows" "tools-inventory" "webapp")

for service in "${services[@]}"; do
    echo "Checking $service..."
    if docker-compose ps $service | grep -q "Up"; then
        echo "✓ $service is running"
    else
        echo "✗ $service is not running"
    fi
done
```

#### Check Resource Usage
```bash
#!/bin/bash
# resource-check.sh

echo "=== Docker Stats ==="
docker stats --no-stream

echo "=== Disk Usage ==="
df -h

echo "=== Memory Usage ==="
free -h

echo "=== CPU Usage ==="
top -bn1 | grep "Cpu(s)"
```

#### Check Network Connectivity
```bash
#!/bin/bash
# network-check.sh

echo "=== Internal Services ==="
curl -s http://localhost:8000/health || echo "API Gateway: FAIL"
curl -s http://localhost:8001/health || echo "AI Databases: FAIL"
curl -s http://localhost:8002/health || echo "Core Workers: FAIL"
curl -s http://localhost:8003/health || echo "Core Workflows: FAIL"
curl -s http://localhost:8004/health || echo "Tools Inventory: FAIL"
curl -s http://localhost:8501/_stcore/health || echo "Webapp: FAIL"

echo "=== External Services ==="
ping -c 1 api.openai.com || echo "OpenAI API: FAIL"
ping -c 1 api.cohere.ai || echo "Cohere API: FAIL"
```

### Performance Profiling

#### Python Profiling
```python
# profile.py
import cProfile
import pstats
from main import app

# Profile the application
profiler = cProfile.Profile()
profiler.enable()

# Run your code here
app.run()

profiler.disable()

# Save results
stats = pstats.Stats(profiler)
stats.dump_stats('profile_results.prof')

# Print top functions
stats.sort_stats('cumulative').print_stats(10)
```

#### Memory Profiling
```python
# memory_profile.py
from memory_profiler import profile
import psutil

@profile
def process_large_file(file_path):
    """Process large file with memory profiling"""
    with open(file_path, 'r') as f:
        content = f.read()
    
    # Process content
    result = process_content(content)
    
    return result

# Monitor memory usage
def monitor_memory():
    process = psutil.Process()
    memory_info = process.memory_info()
    print(f"Memory usage: {memory_info.rss / 1024 / 1024:.2f} MB")
```

## 📊 Performance Optimization

### Database Optimization

#### Query Optimization
```sql
-- Check slow queries
SELECT query, mean_time, calls 
FROM pg_stat_statements 
ORDER BY mean_time DESC 
LIMIT 10;

-- Add indexes
CREATE INDEX idx_files_file_path ON files(file_path);
CREATE INDEX idx_chunks_file_id ON chunks(file_id);

-- Analyze tables
ANALYZE files;
ANALYZE chunks;
```

#### Connection Pooling
```python
# database.py
from sqlalchemy import create_engine
from sqlalchemy.pool import QueuePool

engine = create_engine(
    DATABASE_URL,
    poolclass=QueuePool,
    pool_size=20,
    max_overflow=30,
    pool_pre_ping=True
)
```

### Caching Optimization

#### Redis Configuration
```python
# redis_config.py
import redis
from redis.sentinel import Sentinel

# Connection pooling
redis_pool = redis.ConnectionPool(
    host='redis',
    port=6379,
    db=0,
    max_connections=20
)

redis_client = redis.Redis(connection_pool=redis_pool)
```

#### Cache Strategy
```python
# cache.py
import redis
import json
from functools import wraps

redis_client = redis.Redis(host='redis', port=6379, db=0)

def cache_result(ttl=3600):
    """Cache function result"""
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            cache_key = f"{func.__name__}:{hash(str(args) + str(kwargs))}"
            
            # Try to get from cache
            cached = redis_client.get(cache_key)
            if cached:
                return json.loads(cached)
            
            # Execute function
            result = func(*args, **kwargs)
            
            # Cache result
            redis_client.setex(cache_key, ttl, json.dumps(result))
            
            return result
        return wrapper
    return decorator
```

## 🔗 Liên kết

- [Setup & Installation](./setup.md)
- [Development Workflow](./workflow.md)
- [Testing](./testing.md)
- [Deployment](./deployment.md)
- [Operations Documentation](../operations/README.md)
