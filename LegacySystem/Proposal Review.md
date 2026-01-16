# Review Plan: Tạo Tài Liệu Cho Legacy Repository

## Tổng Quan

Plan hiện tại có 3 phần chính, logic rõ ràng và phù hợp với mục tiêu tạo tài liệu cho legacy repo. Tuy nhiên, có một số điểm cần bổ sung và cải thiện.

---

## Phân Tích Chi Tiết

### ✅ Phần 1: Tìm Kiếm Entrypoint

#### Điểm Mạnh:
- Logic phân loại file (source_code vs support-file) rõ ràng
- Trích xuất outgoing calls với context (start_line, end_line) hợp lý
- Sử dụng LLM để mô tả ý nghĩa lời gọi là approach tốt
- Xây dựng call-graph và trace ngược để tìm entry point là đúng hướng

#### Vấn Đề & Đề Xuất:

1. **Thiếu xử lý COPY/include files**
   - **Vấn đề**: COPY files (`.cpy`) trong COBOL và include files trong các ngôn ngữ khác cần được xử lý đặc biệt
   - **Đề xuất**: 
     - COPY files nên được track riêng trong call-graph với edge type là "includes" thay vì "calls"
     - Cần resolve path của COPY files (có thể có search path như COPYBOOK library)
     - COPY files có thể được include bởi nhiều file → cần track dependencies

2. **Thiếu xử lý dynamic calls**
   - **Vấn đề**: Một số legacy code có dynamic calls (ví dụ: CALL với variable name)
   - **Đề xuất**: 
     - Pattern matching cho dynamic calls (ví dụ: `CALL USING variable-name`)
     - Ghi nhận trong documentation là "potential call" với confidence level

3. **Thiếu validation cho call resolution**
   - **Vấn đề**: Mapping từ call_name → file_path có thể không chính xác (case sensitivity, naming convention)
   - **Đề xuất**:
     - Log các unresolved calls để review thủ công
     - Hỗ trợ fuzzy matching cho tên file
     - Cấu hình mapping rules cho từng repo (naming convention)

4. **Thiếu xử lý circular dependencies**
   - **Vấn đề**: Call-graph có thể có cycles (A calls B, B calls A)
   - **Đề xuất**: 
     - Detect và report circular dependencies
     - Xử lý đặc biệt khi summarize (tránh infinite loop)

5. **Entry point detection cần cải thiện**
   - **Vấn đề**: Chỉ dựa vào "không được refer" có thể miss một số entry points
   - **Đề xuất**:
     - Kết hợp nhiều signals: không được refer + có PROGRAM-ID + có MAIN section + được gọi từ JCL
     - Priority scoring cho entry points (primary vs secondary)

---

### ⚠️ Phần 2: Tạo Summary Cho Từng File

#### Điểm Mạnh:
- Bottom-up approach (từ leaf nodes lên) là hợp lý
- Sử dụng summary của node con để summarize node cha là đúng

#### Vấn Đề & Đề Xuất:

1. **Thiếu chiến lược summarize rõ ràng**
   - **Vấn đề**: Plan không nêu rõ format và nội dung của summary
   - **Đề xuất**:
     ```
     Summary nên bao gồm:
     - Mục đích của file (purpose)
     - Input/Output parameters (nếu có)
     - Dependencies (files được gọi)
     - Key business logic (tóm tắt)
     - Entry points (nếu là controller)
     ```

2. **Thiếu xử lý cho support files**
   - **Vấn đề**: Plan chỉ focus vào source code, không đề cập summarize support files
   - **Đề xuất**:
     - COPY files: summarize structure, fields, usage
     - Config files: summarize configuration options
     - Documentation files: extract key information

3. **Thiếu caching và optimization**
   - **Vấn đề**: Summarize từng file độc lập có thể tốn kém (LLM calls)
   - **Đề xuất**:
     - Cache summaries để tránh regenerate
     - Batch summarize cho các file tương tự
     - Incremental update (chỉ summarize lại khi file thay đổi)

4. **Thiếu context window management**
   - **Vấn đề**: File lớn có thể vượt quá context window của LLM
   - **Đề xuất**:
     - Chunking strategy cho file lớn
     - Summarize từng section rồi tổng hợp
     - Sử dụng code structure để guide summarization

---

### ⚠️ Phần 3: Tìm Kiếm Các Thành Phần Share Chung

#### Điểm Mạnh:
- Identify shared components là quan trọng để hiểu architecture

#### Vấn Đề & Đề Xuất:

1. **Định nghĩa "shared component" chưa rõ**
   - **Vấn đề**: "sub-graph được refer từ nhiều node" quá mơ hồ
   - **Đề xuất**:
     - Shared component = file được gọi bởi ≥ N files (N có thể config, default = 2)
     - Shared sub-graph = một nhóm files luôn được gọi cùng nhau
     - Common utilities = files có pattern naming như `*UTIL*`, `*COMMON*`

2. **Thiếu phân tích dependency patterns**
   - **Đề xuất**:
     - Identify common dependency chains
     - Detect shared libraries/modules
     - Find reusable components

3. **Thiếu visualization**
   - **Đề xuất**: 
     - Generate diagram cho shared components (Mermaid/Graphviz)
     - Highlight shared components trong call-graph

---

## Các Phần Thiếu Sót Quan Trọng

### 1. **Output Format & Structure**
- Plan không nêu rõ format output (JSON, Markdown, HTML?)
- Thiếu structure của documentation (tổng quan, từng module, call-graph, etc.)

### 2. **Error Handling & Edge Cases**
- Không có strategy xử lý lỗi (file không đọc được, LLM fail, etc.)
- Thiếu xử lý cho edge cases (empty repo, single file, etc.)

### 3. **Configuration & Customization**
- Không có cơ chế config cho:
  - LLM model selection
  - File type detection rules
  - Call resolution rules
  - Summary style/template

### 4. **Testing & Validation**
- Thiếu strategy để validate kết quả
- Không có cách để verify accuracy của call-graph

### 5. **Performance & Scalability**
- Không đề cập đến xử lý repo lớn (hàng nghìn files)
- Thiếu strategy cho parallel processing

### 6. **Documentation Structure**
- Thiếu outline cho final documentation:
  ```
  - Repository Overview
  - Entry Points
  - Call Graph
  - File Summaries
  - Shared Components
  - Dependencies
  - Architecture Diagram
  ```

---

## So Sánh Với Implementation Hiện Tại (v1.py)

### ✅ Đã Implement Tốt:
- File scanning và encoding detection
- Outgoing calls extraction với context
- Call-graph building
- Entry point detection
- Leaf node identification
- Shared components finding

### ⚠️ Cần Cải Thiện:
1. **Syntax errors trong v1.py**:
   - Line 230, 255: Indentation error (thiếu indent cho `context = ...`)
   - Cần fix trước khi chạy

2. **Thiếu LLM integration trong summarize_file()**:
   - Function `summarize_file()` hiện chỉ tạo summary cơ bản, chưa dùng LLM như plan đề xuất

3. **Thiếu recursive summarization**:
   - Chưa implement logic "summarize dựa vào summary của node con" như plan mô tả

4. **Output format**:
   - Hiện chỉ output JSON, thiếu human-readable documentation

---

## Đề Xuất Cải Thiện Plan

### Bổ Sung Vào Plan:

#### 4. **Xử Lý COPY/Include Files**
- Resolve COPY paths
- Track include dependencies riêng biệt
- Summarize COPY file structure

#### 5. **Tạo Documentation Output**
- Generate Markdown documentation với structure rõ ràng
- Include call-graph visualization
- Create index và navigation

#### 6. **Validation & Quality Checks**
- Verify call-graph completeness
- Check for unresolved calls
- Validate entry point detection

#### 7. **Configuration Management**
- Support config file cho:
  - File type rules
  - Call resolution rules
  - LLM settings
  - Output format preferences

#### 8. **Error Handling Strategy**
- Graceful degradation khi LLM fail
- Fallback strategies
- Error reporting và logging

---

## Kết Luận

Plan hiện tại có **foundation tốt** nhưng cần **bổ sung chi tiết** và **xử lý edge cases**. Implementation trong v1.py đã cover được phần lớn plan nhưng còn một số bugs và thiếu sót.

### Priority Actions:
1. **High**: Fix syntax errors trong v1.py
2. **High**: Implement LLM-based summarization như plan mô tả
3. **Medium**: Bổ sung xử lý COPY files
4. **Medium**: Tạo documentation output format
5. **Low**: Thêm configuration và customization options

### Recommended Next Steps:
1. Fix bugs trong v1.py
2. Implement recursive summarization với LLM
3. Bổ sung COPY file handling
4. Tạo Markdown documentation generator
5. Add tests và validation
