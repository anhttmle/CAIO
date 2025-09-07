# Tools Inventory Service

## 🎯 Mục đích

Tools Inventory Service cung cấp các tool implementations thực tế, bao gồm parsers, embedding tools, LLM services, reranking, và vector search tools.

## 🏗️ Service Overview

- **Port**: 8004
- **Framework**: FastAPI
- **Type**: Stateless
- **Dependencies**: AI Databases, External APIs

### Responsibilities
1. **Tool Implementations**: Actual tool logic
2. **API Wrappers**: Wrap external services
3. **Configuration Management**: Tool configurations
4. **Error Handling**: Tool-specific error handling
5. **Performance Optimization**: Tool optimization

## 🔧 Implementation

### Main Components

#### 1. FastAPI Application
```python
app = FastAPI(
    title="Tools Inventory Service",
    description="Tool implementations and API wrappers",
    version="1.0.0"
)
```

#### 2. Tool Classes
```python
from parsers.cobol_parser import CobolParserTool
from parsers.copy_parser import CopyParserTool
from parsers.jcl_parser import JclParserTool
from parsers.text_parser import TextParserTool

from embedding.embedding_tool import OpenAIEmbeddingTool

from llm_services.summary_tool import SummaryTool
from llm_services.qa_tool import QATool
from llm_services.specs_tool import SpecsTool

from vector_search.vector_search_tool import VectorSearchTool
from rerank.rerank_tool import RerankTool
```

#### 3. Service Dependencies
```python
# Service URLs
AI_DATABASES_URL = os.getenv("AI_DATABASES_URL", "http://ai-databases:8000")

# External API Keys
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
COHERE_API_KEY = os.getenv("COHERE_API_KEY")
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
  "service": "tools_inventory",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Parser Operations

#### COBOL Parser
```http
POST /parsers/cobol
Content-Type: application/json

{
  "file_path": "/path/to/file.cbl",
  "content": "COBOL code content",
  "max_chunk_size": 6000
}
```

**Response**:
```json
{
  "success": true,
  "data": {
    "chunks": [
      {
        "content": "IDENTIFICATION DIVISION.\nPROGRAM-ID. TEST.",
        "metadata": {
          "file_path": "/path/to/file.cbl",
          "division": "IDENTIFICATION",
          "chunk_index": 0
        }
      }
    ],
    "file_type": "COBOL",
    "total_chunks": 1
  }
}
```

#### COPY Parser
```http
POST /parsers/copy
Content-Type: application/json

{
  "file_path": "/path/to/file.cpy",
  "content": "COPY file content",
  "max_chunk_size": 6000
}
```

#### JCL Parser
```http
POST /parsers/jcl
Content-Type: application/json

{
  "file_path": "/path/to/file.jcl",
  "content": "JCL file content",
  "max_chunk_size": 6000
}
```

#### Text Parser
```http
POST /parsers/text
Content-Type: application/json

{
  "file_path": "/path/to/file.txt",
  "content": "Text file content",
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
POST /embedding/batch
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
        "score": 0.95,
        "collection": "sections"
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
        "score": 0.95,
        "rerank_score": 0.98
      }
    ]
  }
}
```

## 🔄 Tool Implementation

### 1. Parser Tools

#### COBOL Parser Implementation
```python
class CobolParserTool:
    def __init__(self, max_chunk_size: int = 6000):
        self.max_chunk_size = max_chunk_size
        self.supported_extensions = [".cob", ".cbl", ".cobol"]
    
    def parse(self, file_path: str, content: str) -> List[Dict]:
        """Parse COBOL file into structured chunks"""
        # Split by divisions
        divisions = self._split_by_divisions(content)
        
        chunks = []
        for division_name, division_content in divisions.items():
            if not division_content.strip():
                continue
            
            # Create chunks for this division
            division_chunks = self._create_chunks(
                division_content, 
                file_path, 
                division_name
            )
            chunks.extend(division_chunks)
        
        return chunks
    
    def _split_by_divisions(self, content: str) -> Dict[str, str]:
        """Split COBOL content by divisions"""
        divisions = {}
        current_division = None
        current_content = []
        
        for line in content.split('\n'):
            line = line.strip()
            if line.endswith(' DIVISION.'):
                if current_division:
                    divisions[current_division] = '\n'.join(current_content)
                current_division = line
                current_content = [line]
            else:
                current_content.append(line)
        
        if current_division:
            divisions[current_division] = '\n'.join(current_content)
        
        return divisions
```

#### COPY Parser Implementation
```python
class CopyParserTool:
    def __init__(self, max_chunk_size: int = 6000):
        self.max_chunk_size = max_chunk_size
        self.supported_extensions = [".cpy"]
    
    def parse(self, file_path: str, content: str) -> List[Dict]:
        """Parse COPY file into structured chunks"""
        # Split by copybook sections
        sections = self._split_by_sections(content)
        
        chunks = []
        for section_name, section_content in sections.items():
            chunk = {
                "content": section_content,
                "metadata": {
                    "file_path": file_path,
                    "file_type": "COPY",
                    "section": section_name,
                    "chunk_index": len(chunks)
                }
            }
            chunks.append(chunk)
        
        return chunks
```

### 2. Embedding Tools

#### OpenAI Embedding Tool
```python
class OpenAIEmbeddingTool:
    def __init__(self, api_key: str = None, model_name: str = "text-embedding-3-small"):
        self.api_key = api_key or os.getenv("OPENAI_API_KEY")
        self.model_name = model_name
        self.client = OpenAI(api_key=self.api_key)
    
    async def generate_embedding(self, content: str) -> List[float]:
        """Generate embedding for content"""
        try:
            response = await self.client.embeddings.create(
                model=self.model_name,
                input=content
            )
            return response.data[0].embedding
        except Exception as e:
            logger.error(f"Error generating embedding: {e}")
            raise
    
    async def batch_generate_embeddings(self, contents: List[str]) -> List[List[float]]:
        """Generate embeddings for multiple contents"""
        try:
            response = await self.client.embeddings.create(
                model=self.model_name,
                input=contents
            )
            return [item.embedding for item in response.data]
        except Exception as e:
            logger.error(f"Error generating batch embeddings: {e}")
            raise
```

### 3. LLM Tools

#### Summary Tool
```python
class SummaryTool:
    def __init__(self, api_key: str = None, model_name: str = "gpt-4"):
        self.api_key = api_key or os.getenv("OPENAI_API_KEY")
        self.model_name = model_name
        self.client = AsyncOpenAI(api_key=self.api_key)
    
    async def generate_summary(self, content: str, file_path: str, summary_type: str = "file") -> str:
        """Generate summary for content"""
        prompt = self._get_summary_prompt(content, file_path, summary_type)
        
        try:
            response = await self.client.chat.completions.create(
                model=self.model_name,
                messages=[
                    {"role": "system", "content": "You are a helpful assistant that summarizes COBOL code."},
                    {"role": "user", "content": prompt}
                ],
                max_tokens=500,
                temperature=0.3
            )
            return response.choices[0].message.content
        except Exception as e:
            logger.error(f"Error generating summary: {e}")
            raise
    
    def _get_summary_prompt(self, content: str, file_path: str, summary_type: str) -> str:
        """Get summary prompt based on type"""
        if summary_type == "file":
            return f"Summarize this COBOL file ({file_path}):\n\n{content}"
        elif summary_type == "chunk":
            return f"Summarize this COBOL code chunk:\n\n{content}"
        else:
            return f"Summarize this content:\n\n{content}"
```

#### QA Tool
```python
class QATool:
    def __init__(self, api_key: str = None, model_name: str = "gpt-4"):
        self.api_key = api_key or os.getenv("OPENAI_API_KEY")
        self.model_name = model_name
        self.client = AsyncOpenAI(api_key=self.api_key)
    
    async def generate_answer(self, question: str, context: List[Dict], model_name: str = "gpt-4") -> Dict:
        """Generate answer for question"""
        formatted_context = self._format_context(context)
        
        try:
            response = await self.client.chat.completions.create(
                model=model_name,
                messages=[
                    {"role": "system", "content": "You are a helpful assistant that answers questions about COBOL code."},
                    {"role": "user", "content": f"Question: {question}\n\nContext:\n{formatted_context}"}
                ],
                max_tokens=1000,
                temperature=0.7
            )
            
            answer = response.choices[0].message.content
            references = self._extract_references(context)
            
            return {
                "answer": answer,
                "references": references,
                "model_name": model_name,
                "tokens_used": response.usage.total_tokens
            }
        except Exception as e:
            logger.error(f"Error generating answer: {e}")
            raise
```

### 4. Vector Search Tools

#### Vector Search Tool
```python
class VectorSearchTool:
    def __init__(self, ai_databases_url: str = None):
        self.ai_databases_url = ai_databases_url or os.getenv("AI_DATABASES_URL")
    
    async def search(self, query: str, collections: List[str], top_k: int = 10) -> Dict:
        """Search documents using vector similarity"""
        # Generate query embedding
        embedding_tool = OpenAIEmbeddingTool()
        query_embedding = await embedding_tool.generate_embedding(query)
        
        all_results = []
        
        for collection in collections:
            # Search in collection
            search_request = {
                "collection_name": collection,
                "query_embedding": query_embedding,
                "top_k": top_k
            }
            
            response = await self._call_ai_databases_api(
                "/vector/search",
                search_request
            )
            
            # Add collection info to results
            for result in response["results"]:
                result["collection"] = collection
                all_results.append(result)
        
        return {
            "results": all_results,
            "total_results": len(all_results),
            "collections_searched": collections
        }
```

### 5. Rerank Tools

#### Rerank Tool
```python
class RerankTool:
    def __init__(self, api_key: str = None, model_name: str = "rerank-v3.5"):
        self.api_key = api_key or os.getenv("COHERE_API_KEY")
        self.model_name = model_name
        self.client = cohere.Client(api_key=self.api_key)
    
    async def rerank(self, query: str, documents: List[Dict], top_k: int = 10) -> List[Dict]:
        """Rerank documents using Cohere"""
        if not documents:
            return []
        
        # Extract document content
        doc_contents = [doc["content"] for doc in documents]
        
        try:
            response = self.client.rerank(
                model=self.model_name,
                query=query,
                documents=doc_contents,
                top_k=top_k
            )
            
            # Map reranked results back to original documents
            reranked_results = []
            for result in response.results:
                original_doc = documents[result.index]
                original_doc["rerank_score"] = result.relevance_score
                reranked_results.append(original_doc)
            
            return reranked_results
        except Exception as e:
            logger.error(f"Error reranking documents: {e}")
            raise
```

## 🛠️ Configuration

### Environment Variables
```bash
# Service URLs
AI_DATABASES_URL=http://ai-databases:8000

# API Keys
OPENAI_API_KEY=your_openai_key
COHERE_API_KEY=your_cohere_key

# Tool Configurations
MAX_CHUNK_SIZE=6000
EMBEDDING_MODEL=text-embedding-3-small
LLM_MODEL=gpt-4
RERANK_MODEL=rerank-v3.5

# Logging
LOG_LEVEL=INFO
LOG_FILE=/app/shared/tools_inventory.log
```

### Docker Configuration
```yaml
tools-inventory:
  build: ./tools_inventory
  container_name: tools-inventory
  depends_on:
    - ai-databases
  environment:
    - AI_DATABASES_URL=http://ai-databases:8000
    - OPENAI_API_KEY=your_openai_key
    - COHERE_API_KEY=your_cohere_key
  networks:
    - backend
  volumes:
    - ./shared:/app/shared
```

## 🔍 Error Handling

### Tool Error Handling
```python
async def handle_tool_error(tool_name: str, error: Exception):
    """Handle tool errors"""
    logger.error(f"Error in {tool_name} tool: {error}")
    
    # Return error response
    return {
        "success": False,
        "error": f"{tool_name} tool failed",
        "details": str(error)
    }
```

### API Error Handling
```python
@app.exception_handler(Exception)
async def global_exception_handler(request: Request, exc: Exception):
    """Global exception handler"""
    logger.error(f"Unhandled exception: {exc}")
    
    return JSONResponse(
        status_code=500,
        content={
            "success": False,
            "error": "Internal server error",
            "details": str(exc) if DEBUG else "An error occurred"
        }
    )
```

## 📊 Performance Optimization

### Caching
```python
import redis

redis_client = redis.Redis(host='redis', port=6379, db=0)

async def cache_tool_result(tool_name: str, input_hash: str, result: Dict, ttl: int = 3600):
    """Cache tool result"""
    cache_key = f"{tool_name}:{input_hash}"
    redis_client.setex(cache_key, ttl, json.dumps(result))

async def get_cached_tool_result(tool_name: str, input_hash: str) -> Optional[Dict]:
    """Get cached tool result"""
    cache_key = f"{tool_name}:{input_hash}"
    cached = redis_client.get(cache_key)
    if cached:
        return json.loads(cached)
    return None
```

### Batch Processing
```python
async def batch_process_embeddings(contents: List[str]) -> List[List[float]]:
    """Process embeddings in batches"""
    batch_size = 10
    embeddings = []
    
    for i in range(0, len(contents), batch_size):
        batch = contents[i:i + batch_size]
        batch_embeddings = await embedding_tool.batch_generate_embeddings(batch)
        embeddings.extend(batch_embeddings)
    
    return embeddings
```

## 🔒 Security

### Input Validation
```python
def validate_tool_input(tool_name: str, input_data: Dict) -> bool:
    """Validate tool input"""
    if tool_name == "cobol_parser":
        return "content" in input_data and "file_path" in input_data
    elif tool_name == "embedding":
        return "content" in input_data
    elif tool_name == "llm":
        return "content" in input_data and "prompt_type" in input_data
    else:
        return True
```

### API Key Management
```python
def get_api_key(service: str) -> str:
    """Get API key for service"""
    if service == "openai":
        key = os.getenv("OPENAI_API_KEY")
    elif service == "cohere":
        key = os.getenv("COHERE_API_KEY")
    else:
        raise ValueError(f"Unknown service: {service}")
    
    if not key:
        raise ValueError(f"API key not found for {service}")
    
    return key
```

## 🔗 Liên kết

- [API Gateway Service](./api-gateway.md)
- [AI Databases Service](./ai-databases.md)
- [Core Workers Service](./core-workers.md)
- [Core Workflows Service](./core-workflows.md)
- [Technical Implementation](../technical/README.md)
