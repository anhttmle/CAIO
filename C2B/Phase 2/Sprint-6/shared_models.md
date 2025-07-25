# Shared Models - Mô tả các data structure dùng chung

## Tổng quan
Tất cả các service đều dùng chung models định nghĩa trong `shared/models.py` để đảm bảo type safety, consistency, auto-doc, maintainability.

## 1. Enum
- `FileType`: COBOL, COPY, JCL, TEXT, UNKNOWN
- `ServiceStatus`: HEALTHY, UNHEALTHY, UNREACHABLE, DEGRADED, ERROR
- `DivisionType`: IDENTIFICATION, ENVIRONMENT, DATA, PROCEDURE

## 2. Base Models
- `BaseResponse`: Base cho mọi API response
- `HealthCheckResponse`: Health check response

## 3. Parser Models
- `ChunkMetadata`, `ParsedChunk`: Metadata & nội dung chunk sau khi parse
- `ParseFileRequest/Response`, `ParseZipRequest/Response`: Request/response cho parse file/zip

## 4. Embedding Models
- `EmbeddingRequest/Response`: Sinh embedding cho text/chunk

## 5. Vector Database Models
- `CollectionSchema`, `VectorDocument`, `VectorSearchRequest/Response`, `VectorSearchResult`, `CollectionStats`

## 6. LLM Models
- `SummaryRequest/Response`: Sinh summary
- `QARequest/Response`: Hỏi đáp tự động
- `SpecsRequest/Response`: Sinh specs

## 7. Rerank Models
- `RerankRequest/Response`: Rerank kết quả search

## 8. Workflow Models
- `IndexingRequest/Response`: Indexing workflow
- `RetrievalRequest/Response`: Retrieval workflow

## 9. Feedback Models
- `FeedbackData`, `FeedbackRequest/Response`, `FeedbackStats`

## 10. Configuration Models
- `Configuration`: Thông tin cấu hình hệ thống

---

## Utility Functions
- `create_error_response(error_message, service)`
- `create_success_response(data, service)`
- `validate_file_type(file_path)`

### Ví dụ sử dụng
```python
from shared import ParseFileRequest, FileType
req = ParseFileRequest(file_path="a.cbl", content="...", file_type=FileType.COBOL)
```

---

## Lợi ích
- **Type Safety**: Pydantic validation cho input/output
- **Consistency**: Chuẩn hóa data structures giữa services
- **Documentation**: Auto-generated docs từ Pydantic models
- **Maintainability**: Single source of truth cho data models
- **IDE Support**: Better autocomplete, error detection

---

## Migration Guide
### Từ dict-based sang model-based
```python
# Old
return {"success": True, "results": [...], "count": 10}
# New
return VectorSearchResponse(success=True, results=results, collection="COBOL", total_results=10)
```

### Từ manual validation sang Pydantic
```python
# Old
if not request.get("query"): raise HTTPException(400, "Query is required")
# New
request: QARequest = QARequest(**request_data)  # Pydantic tự validate
```

---

## Testing
```python
import pytest
from shared import QARequest

def test_qa_request_validation():
    request = QARequest(query="What is COBOL?")
    assert request.query == "What is COBOL?"
    with pytest.raises(Exception):
        QARequest()  # Missing required field
```

---

## Docker & Integration
- Mount shared vào tất cả container: `- ./shared:/app/shared`
- Add vào PYTHONPATH: `sys.path.append('/app/shared')`
- Cài requirements: `pip install -r /app/shared/requirements.txt`

---

> Xem tiếp các file trong BotDocs để biết hướng dẫn dev, specs DB, ... 