# Core Workers Service

## 🎯 Mục đích

Core Workers Service chứa business logic chính của hệ thống, bao gồm parsing, embedding generation, LLM operations, vector search, và reranking.

## 🏗️ Service Overview

- **Port**: 8002
- **Framework**: FastAPI
- **Type**: Stateless
- **Dependencies**: Tools Inventory, AI Databases

### Responsibilities
1. **File Parsing**: COBOL, COPY, JCL, TEXT parsing
2. **Embedding Generation**: Vector embeddings
3. **LLM Operations**: Summary, QA, Specs generation
4. **Vector Search**: Similarity search
5. **Reranking**: Result reranking

## 🔧 Implementation

### Main Components

#### 1. FastAPI Application
```python
app = FastAPI(
    title="Core Workers Service",
    description="Parser, Embedding, LLM Workers APIs",
    version="1.0.0"
)
```

#### 2. Worker Classes
```python
from workers.llm_services.llm_worker import LLMWorker
from workers.rerank.rerank_worker import RerankWorker
from workers.vector_search.vector_search_worker import VectorSearchWorker

# Initialize workers
llm_worker = LLMWorker()
rerank_worker = RerankWorker()
vector_search_worker = VectorSearchWorker()
```

#### 3. Service Dependencies
```python
# Service URLs
AI_DATABASES_URL = os.getenv("AI_DATABASES_URL", "http://ai-databases:8000")
TOOLS_INVENTORY_URL = os.getenv("TOOLS_INVENTORY_URL", "http://tools-inventory:8000")
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
  "service": "core_workers",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Parser Operations

#### Parse ZIP File
```http
POST /parser/parse-zip
Content-Type: multipart/form-data

zip_file: [binary data]
max_chunk_size: 6000
hash_dir: optional_hash
```

**Response**:
```json
{
  "success": true,
  "data": {
    "files_processed": 5,
    "chunks_created": 25,
    "processing_time": 30.5,
    "files": [
      {
        "file_path": "file1.cbl",
        "file_type": "COBOL",
        "chunks": 5,
        "summary": "File summary"
      }
    ]
  }
}
```

#### Parse Single File
```http
POST /parser/parse-file
Content-Type: application/json

{
  "file_path": "/path/to/file.cbl",
  "content": "COBOL code content",
  "file_type": "COBOL",
  "max_chunk_size": 6000
}
```

### Embedding Operations

#### Generate Embedding
```http
POST /embedding/generate
Content-Type: application/json

{
  "content": "Text to embed",
  "file_path": "/path/to/file.cbl",
  "model_name": "text-embedding-3-small"
}
```

**Response**:
```json
{
  "success": true,
  "data": {
    "embedding": [0.1, 0.2, ...],
    "model_name": "text-embedding-3-small",
    "dimensions": 1536
  }
}
```

#### Batch Generate Embeddings
```http
POST /embedding/batch-generate
Content-Type: application/json

{
  "contents": ["Text 1", "Text 2", "Text 3"],
  "file_paths": ["/path1", "/path2", "/path3"],
  "model_name": "text-embedding-3-small"
}
```

### LLM Operations

#### Generate Summary
```http
POST /llm/summary
Content-Type: application/json

{
  "content": "COBOL code content",
  "file_path": "/path/to/file.cbl",
  "summary_type": "file",
  "model_name": "gpt-4"
}
```

**Response**:
```json
{
  "success": true,
  "data": {
    "summary": "This COBOL program processes customer data...",
    "model_name": "gpt-4",
    "tokens_used": 150
  }
}
```

#### Question Answering
```http
POST /llm/qa
Content-Type: application/json

{
  "question": "What does this COBOL program do?",
  "context": [
    {
      "content": "COBOL code content",
      "metadata": {"file_path": "file.cbl"}
    }
  ],
  "model_name": "gpt-4",
  "temperature": 0.7,
  "max_tokens": 1000
}
```

**Response**:
```json
{
  "success": true,
  "data": {
    "answer": "This COBOL program processes customer data...",
    "references": [
      {
        "file_path": "file.cbl",
        "line_start": 10,
        "line_end": 20
      }
    ],
    "model_name": "gpt-4",
    "tokens_used": 150
  }
}
```

#### Generate Specs
```http
POST /llm/specs
Content-Type: application/json

{
  "content": "Repository content",
  "spec_type": "Repository Overview",
  "model_name": "gpt-4",
  "max_tokens": 4000
}
```

### Vector Search Operations

#### Search Documents
```http
POST /vector-search/search
Content-Type: application/json

{
  "query": "COBOL program structure",
  "collections": ["sections", "wiki"],
  "top_k": 10
}
```

**Response**:
```json
{
  "success": true,
  "data": {
    "results": [
      {
        "content": "COBOL code snippet",
        "metadata": {"file_path": "file.cbl"},
        "score": 0.95
      }
    ],
    "total_results": 10,
    "search_time": 0.5
  }
}
```

#### Multi-Collection Search
```http
POST /vector-search/multi-collection
Content-Type: application/json

{
  "query": "COBOL program structure",
  "collections": ["sections", "wiki", "summaries"],
  "top_k_per_collection": 5
}
```

### Rerank Operations

#### Rerank Results
```http
POST /rerank/rerank
Content-Type: application/json

{
  "query": "COBOL program structure",
  "documents": [
    {
      "content": "COBOL code snippet",
      "metadata": {"file_path": "file.cbl"},
      "score": 0.95
    }
  ],
  "top_k": 5
}
```

**Response**:
```json
{
  "success": true,
  "data": {
    "reranked_results": [
      {
        "content": "COBOL code snippet",
        "metadata": {"file_path": "file.cbl"},
        "score": 0.98,
        "rerank_score": 0.95
      }
    ]
  }
}
```

## 🔄 Data Flow

### 1. Parsing Flow
```mermaid
graph LR
    A[File Upload] --> B[Detect File Type]
    B --> C[Select Parser]
    C --> D[Parse Content]
    D --> E[Create Chunks]
    E --> F[Generate Metadata]
    F --> G[Return Results]
```

### 2. Embedding Flow
```mermaid
graph LR
    A[Text Content] --> B[Call Tools Inventory]
    B --> C[OpenAI API]
    C --> D[Generate Embedding]
    D --> E[Return Vector]
```

### 3. LLM Flow
```mermaid
graph LR
    A[Request] --> B[Call Tools Inventory]
    B --> C[OpenAI API]
    C --> D[Generate Response]
    D --> E[Return Result]
```

## 🛠️ Configuration

### Environment Variables
```bash
# Service URLs
AI_DATABASES_URL=http://ai-databases:8000
TOOLS_INVENTORY_URL=http://tools-inventory:8000

# API Keys
OPENAI_API_KEY=your_openai_key
COHERE_API_KEY=your_cohere_key

# Logging
LOG_LEVEL=INFO
LOG_FILE=/app/shared/core_workers.log
```

### Docker Configuration
```yaml
core-workers:
  build: ./core_workers
  container_name: core-workers
  depends_on:
    - tools-inventory
    - ai-databases
  environment:
    - AI_DATABASES_URL=http://ai-databases:8000
    - TOOLS_INVENTORY_URL=http://tools-inventory:8000
    - OPENAI_API_KEY=your_openai_key
    - COHERE_API_KEY=your_cohere_key
  networks:
    - backend
  volumes:
    - ./shared:/app/shared
```

## 🔍 Error Handling

### Service Communication Errors
```python
async def call_tools_inventory_api(endpoint: str, data: dict):
    """Call Tools Inventory API with error handling"""
    try:
        async with httpx.AsyncClient() as client:
            response = await client.post(
                f"{TOOLS_INVENTORY_URL}{endpoint}",
                json=data,
                timeout=30.0
            )
            response.raise_for_status()
            return response.json()
    except httpx.TimeoutException:
        logger.error(f"Timeout calling Tools Inventory API: {endpoint}")
        raise HTTPException(status_code=504, detail="Tools Inventory service timeout")
    except httpx.HTTPStatusError as e:
        logger.error(f"HTTP error calling Tools Inventory API: {e}")
        raise HTTPException(status_code=e.response.status_code, detail="Tools Inventory service error")
    except Exception as e:
        logger.error(f"Error calling Tools Inventory API: {e}")
        raise HTTPException(status_code=500, detail="Internal service error")
```

### Validation Errors
```python
from pydantic import BaseModel, validator

class ParseZipRequest(BaseModel):
    max_chunk_size: Optional[int] = 6000
    hash_dir: Optional[str] = None
    
    @validator('max_chunk_size')
    def validate_chunk_size(cls, v):
        if v and (v < 1000 or v > 10000):
            raise ValueError('Chunk size must be between 1000 and 10000')
        return v
```

## 📊 Performance Optimization

### Async Processing
```python
async def process_files_async(files: List[Dict]) -> List[Dict]:
    """Process multiple files asynchronously"""
    tasks = []
    for file in files:
        task = asyncio.create_task(process_single_file(file))
        tasks.append(task)
    
    results = await asyncio.gather(*tasks, return_exceptions=True)
    return results
```

### Caching
```python
import redis

redis_client = redis.Redis(host='redis', port=6379, db=0)

async def get_cached_embedding(content: str) -> Optional[List[float]]:
    """Get cached embedding"""
    cache_key = f"embedding:{hashlib.md5(content.encode()).hexdigest()}"
    cached = redis_client.get(cache_key)
    if cached:
        return json.loads(cached)
    return None

async def cache_embedding(content: str, embedding: List[float]):
    """Cache embedding"""
    cache_key = f"embedding:{hashlib.md5(content.encode()).hexdigest()}"
    redis_client.setex(cache_key, 3600, json.dumps(embedding))  # 1 hour TTL
```

### Batch Processing
```python
async def batch_generate_embeddings(contents: List[str]) -> List[List[float]]:
    """Generate embeddings in batches"""
    batch_size = 10
    embeddings = []
    
    for i in range(0, len(contents), batch_size):
        batch = contents[i:i + batch_size]
        batch_embeddings = await generate_embeddings_batch(batch)
        embeddings.extend(batch_embeddings)
    
    return embeddings
```

## 🔒 Security

### Input Validation
```python
def validate_file_type(file_type: str) -> bool:
    """Validate file type"""
    allowed_types = ['COBOL', 'COPY', 'JCL', 'TEXT']
    return file_type.upper() in allowed_types

def sanitize_content(content: str) -> str:
    """Sanitize content to prevent injection attacks"""
    # Remove potentially dangerous characters
    sanitized = re.sub(r'[<>"\']', '', content)
    return sanitized.strip()
```

### API Key Management
```python
def get_openai_api_key() -> str:
    """Get OpenAI API key securely"""
    api_key = os.getenv("OPENAI_API_KEY")
    if not api_key:
        raise ValueError("OpenAI API key not found")
    return api_key
```

## 🔗 Liên kết

- [API Gateway Service](./api-gateway.md)
- [AI Databases Service](./ai-databases.md)
- [Core Workflows Service](./core-workflows.md)
- [Tools Inventory Service](./tools-inventory.md)
- [Technical Implementation](../technical/README.md)
