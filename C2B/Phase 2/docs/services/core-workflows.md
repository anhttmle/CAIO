# Core Workflows Service

## 🎯 Mục đích

Core Workflows Service orchestrate các workflow phức tạp trong hệ thống, bao gồm indexing, QA, specs generation, và retrieval workflows.

## 🏗️ Service Overview

- **Port**: 8003
- **Framework**: FastAPI
- **Type**: Stateless
- **Dependencies**: Core Workers, AI Databases, Redis

### Responsibilities
1. **Workflow Orchestration**: Coordinate complex workflows
2. **Task Management**: Manage Celery tasks
3. **Data Flow**: Control data flow between services
4. **Error Handling**: Handle workflow errors
5. **Monitoring**: Track workflow progress

## 🔧 Implementation

### Main Components

#### 1. FastAPI Application
```python
app = FastAPI(
    title="Core Workflows Service",
    description="Indexing, Retrieval, QA, Specs Workflows APIs",
    version="1.0.0"
)
```

#### 2. Celery Integration
```python
from celery_app_instance import celery_app
from celery.result import AsyncResult

# Celery task management
@app.get("/tasks/{task_id}")
async def get_task_status(task_id: str):
    """Get task status"""
    result = AsyncResult(task_id, app=celery_app)
    return {
        "task_id": task_id,
        "status": result.status,
        "result": result.result if result.ready() else None
    }
```

#### 3. Service Dependencies
```python
# Service URLs
AI_DATABASES_URL = os.getenv("AI_DATABASES_URL", "http://ai-databases:8000")
CORE_WORKERS_URL = os.getenv("CORE_WORKERS_URL", "http://core-workers:8000")
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
  "service": "core_workflows",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Indexing Workflow

#### Index ZIP File
```http
POST /indexing/index-zip
Content-Type: multipart/form-data

zip_file: [binary data]
chunk_size: 6000
batch_size: 100
hash_dir: optional_hash
```

**Response**:
```json
{
  "success": true,
  "data": {
    "task_id": "task_123",
    "status": "PENDING",
    "message": "Indexing started"
  }
}
```

#### Get Indexing Status
```http
GET /indexing/status/{task_id}
```

**Response**:
```json
{
  "success": true,
  "data": {
    "task_id": "task_123",
    "status": "SUCCESS",
    "result": {
      "files_processed": 5,
      "chunks_created": 25,
      "processing_time": 30.5
    }
  }
}
```

### QA Workflow

#### Ask Question
```http
POST /qa/ask
Content-Type: application/json

{
  "question": "What does this COBOL program do?",
  "collections": ["sections", "wiki"],
  "top_k": 10,
  "rerank": true
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
        "content": "COBOL code snippet",
        "file_path": "file.cbl",
        "score": 0.95
      }
    ],
    "processing_time": 2.5
  }
}
```

#### Ask Question Stream
```http
POST /qa/ask-stream
Content-Type: application/json

{
  "question": "What does this COBOL program do?",
  "collections": ["sections"],
  "top_k": 10
}
```

**Response**: Streaming response with answer chunks

### Specs Generation Workflow

#### Generate Specs V2
```http
POST /specs-v2/generate-specs
Content-Type: multipart/form-data

zip_file: [binary data]
spec_type: Repository Overview
output_path: /app/shared/wiki_v2
```

**Response**:
```json
{
  "success": true,
  "data": {
    "task_id": "task_456",
    "status": "PENDING",
    "message": "Specs generation started"
  }
}
```

#### Delete Specs
```http
POST /specs-v2/delete-specs
Content-Type: application/json

{
  "hash_dir": "abc123"
}
```

#### Zoom In Specs
```http
POST /specs-v2/zoom-in
Content-Type: application/json

{
  "hash_dir": "abc123",
  "section_id": "section_1"
}
```

### Retrieval Workflow

#### Search Documents
```http
POST /retrieval/search
Content-Type: application/json

{
  "query": "COBOL program structure",
  "collections": ["sections", "wiki"],
  "top_k_per_collection": 20,
  "final_top_k": 10,
  "rerank": true,
  "elbow_pruning": true
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
        "score": 0.95,
        "collection": "sections"
      }
    ],
    "total_results": 10,
    "search_time": 0.5,
    "collections_searched": ["sections", "wiki"]
  }
}
```

## 🔄 Workflow Implementation

### 1. Indexing Workflow

#### Workflow Steps
```python
async def index_zip_workflow(zip_file: UploadFile, chunk_size: int = 6000):
    """Complete indexing workflow"""
    # Step 1: Parse ZIP file
    parse_result = await call_core_workers_api(
        "/parser/parse-zip",
        {"zip_file": zip_file, "max_chunk_size": chunk_size}
    )
    
    # Step 2: Generate summaries
    for file in parse_result["files"]:
        summary = await call_core_workers_api(
            "/llm/summary",
            {"content": file["content"], "file_path": file["file_path"]}
        )
        file["summary"] = summary["summary"]
    
    # Step 3: Generate embeddings
    embeddings = await call_core_workers_api(
        "/embedding/batch-generate",
        {"contents": [chunk["content"] for chunk in parse_result["chunks"]]}
    )
    
    # Step 4: Store in Milvus
    await call_ai_databases_api(
        "/vector/insert",
        {"collection_name": "sections", "documents": parse_result["chunks"]}
    )
    
    # Step 5: Store metadata in PostgreSQL
    await call_ai_databases_api(
        "/metadata/insert",
        {"table_name": "files", "data": parse_result["files"]}
    )
    
    return parse_result
```

### 2. QA Workflow

#### Workflow Steps
```python
async def qa_workflow(question: str, collections: List[str], top_k: int = 10):
    """Complete QA workflow"""
    # Step 1: Generate question embedding
    question_embedding = await call_core_workers_api(
        "/embedding/generate",
        {"content": question}
    )
    
    # Step 2: Search documents
    search_results = []
    for collection in collections:
        results = await call_ai_databases_api(
            "/vector/search",
            {
                "collection_name": collection,
                "query_embedding": question_embedding["embedding"],
                "top_k": top_k
            }
        )
        search_results.extend(results["results"])
    
    # Step 3: Rerank results
    reranked_results = await call_core_workers_api(
        "/rerank/rerank",
        {"query": question, "documents": search_results}
    )
    
    # Step 4: Generate answer
    context = format_context_for_llm(reranked_results)
    answer = await call_core_workers_api(
        "/llm/qa",
        {"question": question, "context": [{"content": context}]}
    )
    
    return {
        "answer": answer["answer"],
        "references": extract_references(reranked_results),
        "processing_time": time.time() - start_time
    }
```

### 3. Specs Generation Workflow

#### Workflow Steps
```python
async def specs_generation_workflow(zip_file: UploadFile, spec_type: str):
    """Complete specs generation workflow"""
    # Step 1: Parse repository structure
    parse_result = await call_core_workers_api(
        "/parser/parse-zip",
        {"zip_file": zip_file}
    )
    
    # Step 2: Generate repository overview
    overview = await call_tools_inventory_api(
        "/llm/specs",
        {
            "content": parse_result["repository_content"],
            "spec_type": spec_type
        }
    )
    
    # Step 3: Generate detailed specs for each section
    detailed_specs = []
    for section in parse_result["sections"]:
        section_spec = await call_tools_inventory_api(
            "/llm/specs",
            {
                "content": section["content"],
                "spec_type": f"Detailed {section['name']}"
            }
        )
        detailed_specs.append(section_spec)
    
    # Step 4: Combine and format specs
    combined_specs = combine_specs(overview, detailed_specs)
    
    # Step 5: Save specs
    await call_ai_databases_api(
        "/specs/save",
        {
            "spec_type": spec_type,
            "content": combined_specs,
            "metadata": {"sections": len(detailed_specs)}
        }
    )
    
    return combined_specs
```

## 🛠️ Configuration

### Environment Variables
```bash
# Service URLs
AI_DATABASES_URL=http://ai-databases:8000
CORE_WORKERS_URL=http://core-workers:8000
TOOLS_INVENTORY_URL=http://tools-inventory:8000

# Redis Configuration
REDIS_URL=redis://redis:6379/0

# Celery Configuration
CELERY_BROKER_URL=redis://redis:6379/0
CELERY_RESULT_BACKEND=redis://redis:6379/0

# Logging
LOG_LEVEL=INFO
LOG_FILE=/app/shared/core_workflows.log
```

### Docker Configuration
```yaml
core-workflows:
  build: ./core_workflows
  container_name: core-workflows
  depends_on:
    - core-workers
    - ai-databases
    - redis
  environment:
    - AI_DATABASES_URL=http://ai-databases:8000
    - CORE_WORKERS_URL=http://core-workers:8000
    - TOOLS_INVENTORY_URL=http://tools-inventory:8000
    - REDIS_URL=redis://redis:6379/0
  networks:
    - backend
  volumes:
    - ./shared:/app/shared
```

## 🔍 Error Handling

### Workflow Error Handling
```python
async def handle_workflow_error(workflow_name: str, error: Exception):
    """Handle workflow errors"""
    logger.error(f"Error in {workflow_name} workflow: {error}")
    
    # Log error details
    error_details = {
        "workflow": workflow_name,
        "error_type": type(error).__name__,
        "error_message": str(error),
        "timestamp": datetime.now().isoformat()
    }
    
    # Send error notification
    await send_error_notification(error_details)
    
    # Return error response
    return {
        "success": False,
        "error": f"Workflow {workflow_name} failed",
        "details": error_details
    }
```

### Task Error Handling
```python
@celery_app.task(bind=True)
def indexing_task(self, zip_file_path: str, chunk_size: int):
    """Celery task with error handling"""
    try:
        # Task implementation
        result = process_indexing(zip_file_path, chunk_size)
        return result
    except Exception as exc:
        # Log error
        logger.error(f"Indexing task failed: {exc}")
        
        # Update task state
        self.update_state(
            state='FAILURE',
            meta={'error': str(exc)}
        )
        
        # Re-raise exception
        raise exc
```

## 📊 Performance Optimization

### Async Processing
```python
async def process_multiple_workflows(workflows: List[Dict]):
    """Process multiple workflows concurrently"""
    tasks = []
    
    for workflow in workflows:
        if workflow["type"] == "indexing":
            task = asyncio.create_task(index_zip_workflow(workflow["data"]))
        elif workflow["type"] == "qa":
            task = asyncio.create_task(qa_workflow(workflow["data"]))
        elif workflow["type"] == "specs":
            task = asyncio.create_task(specs_generation_workflow(workflow["data"]))
        
        tasks.append(task)
    
    results = await asyncio.gather(*tasks, return_exceptions=True)
    return results
```

### Caching
```python
import redis

redis_client = redis.Redis(host='redis', port=6379, db=0)

async def cache_workflow_result(workflow_id: str, result: Dict, ttl: int = 3600):
    """Cache workflow result"""
    cache_key = f"workflow_result:{workflow_id}"
    redis_client.setex(cache_key, ttl, json.dumps(result))

async def get_cached_workflow_result(workflow_id: str) -> Optional[Dict]:
    """Get cached workflow result"""
    cache_key = f"workflow_result:{workflow_id}"
    cached = redis_client.get(cache_key)
    if cached:
        return json.loads(cached)
    return None
```

## 🔒 Security

### Input Validation
```python
from pydantic import BaseModel, validator

class QARequest(BaseModel):
    question: str
    collections: List[str]
    top_k: int = 10
    
    @validator('question')
    def validate_question(cls, v):
        if not v or len(v.strip()) < 3:
            raise ValueError('Question too short')
        if len(v) > 1000:
            raise ValueError('Question too long')
        return v.strip()
    
    @validator('collections')
    def validate_collections(cls, v):
        allowed_collections = ['sections', 'wiki', 'summaries']
        for collection in v:
            if collection not in allowed_collections:
                raise ValueError(f'Invalid collection: {collection}')
        return v
```

### Rate Limiting
```python
from slowapi import Limiter, _rate_limit_exceeded_handler
from slowapi.util import get_remote_address

limiter = Limiter(key_func=get_remote_address)

@app.post("/qa/ask")
@limiter.limit("30/minute")
async def ask_question(request: QARequest):
    """Rate limited QA endpoint"""
    pass
```

## 🔗 Liên kết

- [API Gateway Service](./api-gateway.md)
- [AI Databases Service](./ai-databases.md)
- [Core Workers Service](./core-workers.md)
- [Tools Inventory Service](./tools-inventory.md)
- [Workflows Documentation](../workflows/README.md)
