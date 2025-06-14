<img width="763" alt="image" src="https://github.com/user-attachments/assets/73a7c497-0010-404a-8d3c-36120fa97139" />


# 1. Front End (Streamlit)
- Login/Logout
- Configuration
- Upload repo as zip file
- Generate Specs
- Q&A
- Feedback on Answer

# 2. API Gateway (FastAPI)
- Setting configuration
- Authorization (Login/Logout)
- Parsing COBOL/COPY/JCL file
- Index source code
- Generate Specs
- Index generated Specs
- Context retrieval base on query
- Generate answer base on query
- Feedback on Answer

# 3. RAG (FastAPI or Dify Flow APIs)
- Parsing Flow
- Index source code Flow
- Generate Specs Flow
  - Generate "Overview" Flow
  - Generate "COBOL file" Flow
  - Generate "COPY file" Flow
  - Generate "JCL File" Flow
- Index Generate Specs Flow
- Context retrieval Flow

# 4. Tool Inventory (FastAPI)
- Parsing COBOL file tool
- Parsing COPY file tool
- Parsing JCL file tool
- Chunking COBOL file
- Chunking COPY file
- Chunking JCL file
- ReRank chunks
- Vector Search tool

# 5. AI Database
- PostgreSQL (Required)
- Milvus (Required)
