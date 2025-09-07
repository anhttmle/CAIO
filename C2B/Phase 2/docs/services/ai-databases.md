# AI Databases Service

## 🎯 Mục đích

AI Databases Service quản lý tất cả các operations liên quan đến database, bao gồm Milvus vector database và PostgreSQL metadata database.

## 🏗️ Service Overview

- **Port**: 8001
- **Framework**: FastAPI
- **Type**: Stateful
- **Dependencies**: Milvus, PostgreSQL

### Responsibilities
1. **Vector Database Management**: Milvus operations
2. **Metadata Database Management**: PostgreSQL operations
3. **Data Consistency**: Ensure data integrity
4. **Connection Management**: Database connections
5. **Query Optimization**: Performance optimization

## 🔧 Implementation

### Main Components

#### 1. FastAPI Application
```python
app = FastAPI(
    title="AI Databases Service",
    description="Vector DB (Milvus) and Metadata DB (PostgreSQL) service",
    version="1.0.0"
)
```

#### 2. Database Connections
```python
# Milvus connection
async def connect_milvus(retries=10, delay=5):
    """Connect to Milvus database with retry"""
    for attempt in range(retries):
        try:
            connections.connect("default", host=MILVUS_HOST, port=MILVUS_PORT)
            logger.info(f"Connected to Milvus at {MILVUS_HOST}:{MILVUS_PORT}")
            return True
        except Exception as e:
            logger.error(f"Failed to connect to Milvus (attempt {attempt+1}/{retries}): {e}")
            await asyncio.sleep(delay)
    return False

# PostgreSQL connection
async def connect_postgres(retries=10, delay=5):
    """Connect to PostgreSQL database with retry"""
    for attempt in range(retries):
        try:
            postgres_conn = psycopg2.connect(
                host=POSTGRES_HOST,
                port=POSTGRES_PORT,
                user=POSTGRES_USER,
                password=POSTGRES_PASSWORD,
                database=POSTGRES_DB
            )
            logger.info(f"Connected to PostgreSQL at {POSTGRES_HOST}:{POSTGRES_PORT}")
            return True
        except Exception as e:
            logger.error(f"Failed to connect to PostgreSQL (attempt {attempt+1}/{retries}): {e}")
            await asyncio.sleep(delay)
    return False
```

#### 3. Router Structure
```python
# Import routers
from routers.vector_router import router as vector_router
from routers.metadata_router import router as metadata_router
from routers.specs_router import router as specs_router

# Include routers
app.include_router(vector_router)
app.include_router(metadata_router)
app.include_router(specs_router)
```

## 📡 API Endpoints

### Health Check
```http
GET /health
```

**Response**:
```json
{
  "success": true,
  "status": "HEALTHY",
  "service": "ai_databases",
  "dependencies": {
    "vector_db": "HEALTHY",
    "metadata_db": "HEALTHY"
  },
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Vector Database Operations

#### Insert Documents
```http
POST /vector/insert
Content-Type: application/json

{
  "collection_name": "sections",
  "documents": [
    {
      "id": "doc_1",
      "content": "COBOL code content",
      "embedding": [0.1, 0.2, ...],
      "metadata": {
        "file_path": "/path/to/file.cbl",
        "file_type": "COBOL"
      }
    }
  ]
}
```

#### Search Documents
```http
POST /vector/search
Content-Type: application/json

{
  "collection_name": "sections",
  "query_embedding": [0.1, 0.2, ...],
  "top_k": 10,
  "search_params": {
    "metric_type": "COSINE",
    "params": {"nprobe": 10}
  }
}
```

#### Get Collection Stats
```http
GET /vector/collections/{collection_name}/stats
```

### Metadata Database Operations

#### Insert File
```http
POST /metadata/files
Content-Type: application/json

{
  "file_path": "/path/to/file.cbl",
  "file_name": "file.cbl",
  "file_type": "COBOL",
  "file_size": 1024,
  "hash_value": "abc123"
}
```

#### Get Files
```http
GET /metadata/files?file_type=COBOL&limit=10&offset=0
```

#### Insert Chunks
```http
POST /metadata/chunks
Content-Type: application/json

{
  "file_id": 1,
  "chunks": [
    {
      "chunk_index": 0,
      "content": "COBOL code chunk",
      "metadata": {
        "division": "DATA",
        "section": "FILE-SECTION"
      }
    }
  ]
}
```

### Specs Operations

#### Save Specs
```http
POST /specs/save
Content-Type: application/json

{
  "file_id": 1,
  "spec_type": "Repository Overview",
  "content": "Generated documentation content",
  "metadata": {
    "sections": ["overview", "structure"],
    "created_at": "2024-01-01T00:00:00Z"
  }
}
```

#### Get Specs
```http
GET /specs/{spec_id}
```

#### Delete Specs
```http
DELETE /specs/{spec_id}
```

## 🔄 Data Flow

### 1. Vector Data Flow
```mermaid
graph LR
    A[Client Request] --> B[Vector Router]
    B --> C[Validate Request]
    C --> D[Connect to Milvus]
    D --> E[Execute Operation]
    E --> F[Return Response]
```

### 2. Metadata Data Flow
```mermaid
graph LR
    A[Client Request] --> B[Metadata Router]
    B --> C[Validate Request]
    C --> D[Connect to PostgreSQL]
    D --> E[Execute Query]
    E --> F[Return Response]
```

### 3. Specs Data Flow
```mermaid
graph LR
    A[Client Request] --> B[Specs Router]
    B --> C[Validate Request]
    C --> D[PostgreSQL + Milvus]
    D --> E[Execute Operations]
    E --> F[Return Response]
```

## 🛠️ Configuration

### Environment Variables
```bash
# Milvus Configuration
MILVUS_HOST=standalone
MILVUS_PORT=19530

# PostgreSQL Configuration
POSTGRES_HOST=postgres
POSTGRES_PORT=5432
POSTGRES_USER=cobol
POSTGRES_PASSWORD=your_password
POSTGRES_DB=cobol_assistant

# Logging
LOG_LEVEL=INFO
LOG_FILE=/app/shared/ai_databases.log
```

### Docker Configuration
```yaml
ai-databases:
  build: ./ai_databases
  container_name: ai-databases
  ports:
    - "8001:8000"
  depends_on:
    postgres:
      condition: service_healthy
    standalone:
      condition: service_healthy
  environment:
    - MILVUS_HOST=standalone
    - MILVUS_PORT=19530
    - POSTGRES_HOST=postgres
    - POSTGRES_PORT=5432
    - POSTGRES_USER=cobol
    - POSTGRES_PASSWORD=your_password
    - POSTGRES_DB=cobol_assistant
  networks:
    - backend
  volumes:
    - ./shared:/app/shared
```

## 🔍 Error Handling

### Database Connection Errors
```python
async def handle_db_connection_error(operation: str, error: Exception):
    """Handle database connection errors"""
    logger.error(f"Database connection error during {operation}: {error}")
    
    # Attempt to reconnect
    if "milvus" in operation.lower():
        await connect_milvus()
    elif "postgres" in operation.lower():
        await connect_postgres()
    
    raise HTTPException(
        status_code=503,
        detail=f"Database connection failed during {operation}"
    )
```

### Query Errors
```python
async def handle_query_error(operation: str, error: Exception):
    """Handle database query errors"""
    logger.error(f"Query error during {operation}: {error}")
    
    raise HTTPException(
        status_code=500,
        detail=f"Database query failed during {operation}"
    )
```

## 📊 Performance Optimization

### Connection Pooling
```python
from psycopg2 import pool

# Create connection pool
connection_pool = psycopg2.pool.SimpleConnectionPool(
    1, 20,  # min and max connections
    host=POSTGRES_HOST,
    port=POSTGRES_PORT,
    user=POSTGRES_USER,
    password=POSTGRES_PASSWORD,
    database=POSTGRES_DB
)

def get_postgres_connection():
    """Get connection from pool"""
    return connection_pool.getconn()

def return_postgres_connection(conn):
    """Return connection to pool"""
    connection_pool.putconn(conn)
```

### Query Optimization
```python
# Use prepared statements
def get_file_by_path(file_path: str):
    """Get file by path with prepared statement"""
    conn = get_postgres_connection()
    cursor = conn.cursor()
    
    # Use parameterized query
    cursor.execute("SELECT * FROM files WHERE file_path = %s", (file_path,))
    result = cursor.fetchone()
    
    return_postgres_connection(conn)
    return result
```

### Caching
```python
import redis

# Redis connection for caching
redis_client = redis.Redis(host='redis', port=6379, db=0)

def cache_query_result(key: str, result: dict, ttl: int = 300):
    """Cache query result"""
    redis_client.setex(key, ttl, json.dumps(result))

def get_cached_result(key: str):
    """Get cached result"""
    cached = redis_client.get(key)
    if cached:
        return json.loads(cached)
    return None
```

## 🔒 Security

### Database Security
```python
# Use SSL connections
DATABASE_URL = f"postgresql+psycopg2://{user}:{password}@{host}:{port}/{database}?sslmode=require"

# Milvus with authentication
connections.connect(
    alias="default",
    host=MILVUS_HOST,
    port=MILVUS_PORT,
    user=MILVUS_USER,
    password=MILVUS_PASSWORD
)
```

### Input Validation
```python
from pydantic import BaseModel, validator

class VectorInsertRequest(BaseModel):
    collection_name: str
    documents: List[Dict]
    
    @validator('collection_name')
    def validate_collection_name(cls, v):
        allowed_collections = ['sections', 'wiki', 'summaries']
        if v not in allowed_collections:
            raise ValueError('Invalid collection name')
        return v
```

## 🔗 Liên kết

- [API Gateway Service](./api-gateway.md)
- [Core Workers Service](./core-workers.md)
- [Core Workflows Service](./core-workflows.md)
- [Tools Inventory Service](./tools-inventory.md)
- [Database Design](../architecture/databases.md)
