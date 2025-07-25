# Specs DB - Hệ thống quản lý specs/wiki

## 1. Mục đích
- Lưu trữ cấu trúc tài liệu, trích dẫn, liên kết dạng cây cho file COBOL/COPY/JCL hoặc tài liệu lớn.
- Tối ưu cho truy vấn, phân tích, tái cấu trúc dữ liệu dạng wiki.

## 2. Schema chính
```mermaid
erDiagram
    sections ||--o{ links : "id_A, id_B, link_type"
    sections ||--o{ citations : "section_id"
    citations ||--o{ detailed_citation : "citation_id"
    sections {
        int id
        int parent_id
        int depth
        string title
        ...
    }
    citations {
        int id
        string file
        string source
        ...
    }
    detailed_citation {
        int id
        int citation_id
        int start_line
        int end_line
        ...
    }
    links {
        int id
        int id_A
        int id_B
        string link_type
        string project_id
        ...
    }
```

## 3. Indexing & Truy vấn
- **Indexing citation từ folder:**
  ```python
  from cobol.wiki_json_parser import get_citation_data_from_path
  citation_list = get_citation_data_from_path('test_cobol_files')
  # Insert từng citation vào DB
  ```
- **Parse json và insert dữ liệu:**
  ```python
  from cobol.wiki_json_parser import process_folder_and_json
  process_folder_and_json(session, folder_path, json_data, project_id)
  ```
- **Truy vấn cây section/citation:**
  ```python
  from cobol.wiki_db_ops import get_section_tree_json
  tree_json = get_section_tree_json(session, section_id, project_id)
  ```
- **Xóa toàn bộ dữ liệu của 1 project:**
  ```python
  from cobol.wiki_db_ops import delete_project_data
  delete_project_data(session, project_id)
  ```

## 4. Hướng dẫn test nhanh
- Chạy Postgres bằng Docker:
  ```bash
  docker run --name cobol-postgres -e POSTGRES_PASSWORD=secret -e POSTGRES_USER=cobol -e POSTGRES_DB=cobol_db -p 5432:5432 -d postgres:15
  ```
- Tạo bảng DB:
  ```bash
  export DATABASE_URL='postgresql+psycopg2://cobol:secret@localhost:5432/cobol_db'
  PYTHONPATH=. python cobol/init_db.py
  ```
- Chạy test workflow:
  ```bash
  export DATABASE_URL='postgresql+psycopg2://cobol:secret@localhost:5432/cobol_db'
  PYTHONPATH=. python cobol/test_db_workflow.py
  ```

## 5. Lưu ý tối ưu
- Khi truy vấn lớn, nên tạo index DB: `(project_id, id_A, link_type)` cho bảng `links`.
- Khi insert/xóa hàng loạt, có thể dùng bulk/batch nếu performance là vấn đề.
- Đảm bảo đồng bộ logic hash cite_id giữa indexing và parse json.

## 6. Mở rộng
- Có thể mở rộng cho các loại tài liệu khác, knowledge graph, hoặc phân tích cấu trúc tài liệu lớn dạng cây, có trích dẫn phức tạp.

---

> Xem tiếp các file trong BotDocs để biết hướng dẫn webapp, ... 