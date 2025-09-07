# Development Workflow

## 🎯 Mục đích

Tài liệu này mô tả quy trình phát triển cho hệ thống COBOL Assistant, bao gồm coding standards, git workflow, testing, và deployment.

## 🔄 Development Process

### Development Lifecycle

```mermaid
graph LR
    A[Feature Request] --> B[Design]
    B --> C[Implementation]
    C --> D[Testing]
    D --> E[Code Review]
    E --> F[Deployment]
    F --> G[Monitoring]
    G --> H[Maintenance]
```

### Development Phases

| Phase | Activities | Duration | Deliverables |
|-------|------------|----------|--------------|
| **Planning** | Requirements, Design, Architecture | 1-2 days | Design docs, API specs |
| **Development** | Coding, Unit tests, Integration | 3-5 days | Feature code, Tests |
| **Testing** | QA testing, Performance testing | 1-2 days | Test results, Bug reports |
| **Review** | Code review, Security review | 1 day | Review comments, Approvals |
| **Deployment** | Staging, Production deployment | 0.5 day | Deployed feature |
| **Monitoring** | Performance monitoring, Bug tracking | Ongoing | Metrics, Alerts |

## 🔧 Coding Standards

### Python Code Style

#### PEP 8 Compliance
```python
# Good: Clear, readable code
def calculate_user_score(user_id: int, activity_data: Dict[str, Any]) -> float:
    """Calculate user score based on activity data."""
    if not activity_data:
        return 0.0
    
    base_score = activity_data.get('base_score', 0)
    multiplier = activity_data.get('multiplier', 1.0)
    
    return base_score * multiplier

# Bad: Unclear, hard to read
def calc(u, d):
    if not d: return 0
    return d.get('bs', 0) * d.get('m', 1)
```

#### Type Hints
```python
from typing import List, Dict, Optional, Union, Any
from pydantic import BaseModel

class UserRequest(BaseModel):
    user_id: int
    username: str
    email: Optional[str] = None
    preferences: Dict[str, Any] = {}

def process_user_request(request: UserRequest) -> Dict[str, Any]:
    """Process user request with type safety."""
    return {
        "user_id": request.user_id,
        "username": request.username,
        "processed_at": datetime.now().isoformat()
    }
```

#### Error Handling
```python
import logging
from typing import Optional

logger = logging.getLogger(__name__)

def safe_divide(a: float, b: float) -> Optional[float]:
    """Safely divide two numbers."""
    try:
        if b == 0:
            raise ValueError("Division by zero")
        return a / b
    except (ValueError, TypeError) as e:
        logger.error(f"Division error: {e}")
        return None
    except Exception as e:
        logger.error(f"Unexpected error: {e}")
        raise
```

### API Design Standards

#### RESTful API Design
```python
from fastapi import FastAPI, HTTPException, status
from pydantic import BaseModel

app = FastAPI(title="COBOL Assistant API", version="1.0.0")

class ErrorResponse(BaseModel):
    success: bool = False
    error: str
    error_code: str
    details: Optional[Dict[str, Any]] = None

@app.get("/api/v1/files/{file_id}", response_model=FileResponse)
async def get_file(file_id: int):
    """Get file by ID."""
    try:
        file_data = await get_file_by_id(file_id)
        if not file_data:
            raise HTTPException(
                status_code=status.HTTP_404_NOT_FOUND,
                detail="File not found"
            )
        return file_data
    except Exception as e:
        logger.error(f"Error getting file {file_id}: {e}")
        raise HTTPException(
            status_code=status.HTTP_500_INTERNAL_SERVER_ERROR,
            detail="Internal server error"
        )
```

#### Response Format
```python
class StandardResponse(BaseModel):
    success: bool
    data: Optional[Dict[str, Any]] = None
    error: Optional[str] = None
    timestamp: str
    service: str

def create_success_response(data: Dict[str, Any], service: str) -> StandardResponse:
    """Create standardized success response."""
    return StandardResponse(
        success=True,
        data=data,
        timestamp=datetime.now().isoformat(),
        service=service
    )

def create_error_response(error: str, service: str) -> StandardResponse:
    """Create standardized error response."""
    return StandardResponse(
        success=False,
        error=error,
        timestamp=datetime.now().isoformat(),
        service=service
    )
```

## 🔀 Git Workflow

### Branch Strategy

#### Branch Types
```bash
# Main branches
main                    # Production-ready code
develop                 # Integration branch
release/*              # Release preparation
hotfix/*               # Critical fixes

# Feature branches
feature/user-auth       # New features
feature/api-gateway     # Feature development
feature/parsing         # Feature implementation

# Bug fix branches
bugfix/login-error      # Bug fixes
bugfix/parsing-issue    # Bug resolution
```

#### Branch Naming Convention
```bash
# Feature branches
feature/description-of-feature
feature/user-authentication
feature/api-gateway

# Bug fix branches
bugfix/description-of-bug
bugfix/login-error
bugfix/parsing-issue

# Hotfix branches
hotfix/critical-security-fix
hotfix/urgent-bug-fix

# Release branches
release/v1.2.0
release/v1.3.0
```

### Commit Standards

#### Commit Message Format
```bash
# Format: type(scope): description
# Types: feat, fix, docs, style, refactor, test, chore

# Examples
feat(auth): add user authentication system
fix(parser): resolve COBOL parsing issue
docs(api): update API documentation
style(ui): improve button styling
refactor(db): optimize database queries
test(auth): add authentication tests
chore(deps): update dependencies
```

#### Commit Examples
```bash
# Good commits
git commit -m "feat(api): add file upload endpoint"
git commit -m "fix(parser): handle empty COBOL files"
git commit -m "docs(readme): update installation instructions"
git commit -m "test(integration): add API integration tests"

# Bad commits
git commit -m "fix"
git commit -m "update"
git commit -m "changes"
```

### Pull Request Process

#### PR Template
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No breaking changes
```

#### Review Process
```bash
# 1. Create feature branch
git checkout -b feature/new-feature

# 2. Make changes and commit
git add .
git commit -m "feat: implement new feature"

# 3. Push branch
git push origin feature/new-feature

# 4. Create pull request
# 5. Request review from team members
# 6. Address review comments
# 7. Merge after approval
```

## 🧪 Testing Strategy

### Test Types

#### Unit Tests
```python
import pytest
from unittest.mock import Mock, patch
from tools_inventory.parsers.cobol_parser import CobolParserTool

class TestCobolParser:
    def setup_method(self):
        self.parser = CobolParserTool()
    
    def test_parse_cobol_file(self):
        """Test parsing COBOL file."""
        content = """
        IDENTIFICATION DIVISION.
        PROGRAM-ID. TEST-PROGRAM.
        """
        
        result = self.parser.parse("test.cbl", content)
        
        assert len(result) > 0
        assert all("content" in chunk for chunk in result)
        assert all("metadata" in chunk for chunk in result)
    
    @patch('openai.OpenAI')
    def test_generate_embedding(self, mock_openai):
        """Test embedding generation."""
        mock_client = Mock()
        mock_openai.return_value = mock_client
        mock_client.embeddings.create.return_value = Mock(
            data=[Mock(embedding=[0.1, 0.2, 0.3])]
        )
        
        result = self.parser.generate_embedding("Test content")
        
        assert result == [0.1, 0.2, 0.3]
```

#### Integration Tests
```python
import pytest
import httpx
from fastapi.testclient import TestClient
from api_gateway.main import app

@pytest.fixture
def client():
    return TestClient(app)

def test_file_upload_endpoint(client):
    """Test file upload endpoint."""
    with open("test_files/sample.zip", "rb") as f:
        response = client.post(
            "/api/v1/upload",
            files={"file": ("sample.zip", f, "application/zip")}
        )
    
    assert response.status_code == 200
    data = response.json()
    assert data["success"] == True
    assert "file_id" in data["data"]
```

#### End-to-End Tests
```python
@pytest.mark.e2e
async def test_full_workflow():
    """Test complete workflow from upload to QA."""
    # 1. Upload file
    upload_result = await upload_test_file()
    assert upload_result["success"] == True
    
    # 2. Index file
    index_result = await index_file(upload_result["file_id"])
    assert index_result["success"] == True
    
    # 3. Ask question
    qa_result = await ask_question("What does this program do?")
    assert qa_result["success"] == True
    assert "answer" in qa_result["data"]
```

### Test Configuration

#### Pytest Configuration
```ini
# pytest.ini
[tool:pytest]
testpaths = tests
python_files = test_*.py
python_classes = Test*
python_functions = test_*
addopts = 
    -v
    --tb=short
    --strict-markers
    --disable-warnings
    --cov=.
    --cov-report=html
    --cov-report=term-missing
markers =
    unit: Unit tests
    integration: Integration tests
    e2e: End-to-end tests
    slow: Slow tests
```

#### Test Data Management
```python
# conftest.py
import pytest
import tempfile
import os

@pytest.fixture
def temp_dir():
    """Create temporary directory for tests."""
    with tempfile.TemporaryDirectory() as tmp_dir:
        yield tmp_dir

@pytest.fixture
def sample_cobol_file(temp_dir):
    """Create sample COBOL file for testing."""
    file_path = os.path.join(temp_dir, "sample.cbl")
    content = """
    IDENTIFICATION DIVISION.
    PROGRAM-ID. SAMPLE.
    DATA DIVISION.
    WORKING-STORAGE SECTION.
    01 WS-VARIABLE PIC X(10).
    PROCEDURE DIVISION.
    MAIN-PARAGRAPH.
        DISPLAY "Hello World".
        STOP RUN.
    """
    
    with open(file_path, 'w') as f:
        f.write(content)
    
    return file_path
```

## 🚀 Deployment Process

### Environment Management

#### Environment Configuration
```bash
# Development
export ENV=development
export DEBUG=true
export LOG_LEVEL=DEBUG

# Staging
export ENV=staging
export DEBUG=false
export LOG_LEVEL=INFO

# Production
export ENV=production
export DEBUG=false
export LOG_LEVEL=WARNING
```

#### Docker Configuration
```dockerfile
# Dockerfile
FROM python:3.9-slim

WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application
COPY . .

# Set environment variables
ENV PYTHONPATH=/app
ENV ENV=production

# Expose port
EXPOSE 8000

# Run application
CMD ["python", "main.py"]
```

### Deployment Pipeline

#### CI/CD Pipeline
```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.9
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest tests/
  
  deploy-staging:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/develop'
    steps:
      - name: Deploy to staging
        run: ./deploy.sh staging
  
  deploy-production:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Deploy to production
        run: ./deploy.sh production
```

#### Deployment Scripts
```bash
#!/bin/bash
# deploy.sh

ENVIRONMENT=$1

if [ "$ENVIRONMENT" = "staging" ]; then
    echo "Deploying to staging..."
    docker-compose -f docker-compose.staging.yml up -d
elif [ "$ENVIRONMENT" = "production" ]; then
    echo "Deploying to production..."
    docker-compose -f docker-compose.prod.yml up -d
else
    echo "Invalid environment: $ENVIRONMENT"
    exit 1
fi

echo "Deployment completed successfully"
```

## 📊 Code Quality

### Code Review Checklist

#### Pre-Review Checklist
- [ ] Code follows style guidelines
- [ ] All tests pass
- [ ] Documentation updated
- [ ] No hardcoded values
- [ ] Error handling implemented
- [ ] Logging added where needed
- [ ] Security considerations addressed

#### Review Focus Areas
- **Functionality**: Does the code work as intended?
- **Performance**: Are there any performance issues?
- **Security**: Are there any security vulnerabilities?
- **Maintainability**: Is the code easy to understand and maintain?
- **Testing**: Are there adequate tests?

### Code Metrics

#### Quality Metrics
```python
# Code coverage target: >80%
# Cyclomatic complexity: <10
# Function length: <50 lines
# Class length: <200 lines
# File length: <500 lines
```

#### Monitoring Tools
```bash
# Code quality tools
pylint src/
black --check src/
isort --check-only src/
mypy src/

# Security scanning
bandit -r src/
safety check

# Performance profiling
python -m cProfile main.py
```

## 🔗 Liên kết

- [Setup & Installation](./setup.md)
- [Testing](./testing.md)
- [Deployment](./deployment.md)
- [Troubleshooting](./troubleshooting.md)
- [Architecture Overview](../architecture/README.md)
