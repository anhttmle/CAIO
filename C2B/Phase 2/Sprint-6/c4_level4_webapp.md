# C4 Level 4 - Webapp Component

## 1. Main Module Structure
```mermaid
classDiagram
    class app_py {
        +api_get_health()
        +api_get_collections()
        +api_index_zip(uploaded_file)
        +api_ask_question_stream(query, ...)
        +api_ask_question_complete(query, ...)
        +api_get_feedback(...)
        +api_save_feedback(...)
        +api_generate_specs(...)
        +api_generate_specs_v2(...)
        +api_generate_detailed_specs_v2(...)
        +display_feedback_panel()
        +display_wiki_panel()
        +process_uploaded_file(...)
        +process_query(...)
        +init_session_state()
        +cleanup_temp_dir()
        ...
    }
    class auth_py {
        +setup_authenticator(...)
        +is_admin(...)
        +is_authenticated(...)
        +get_username(...)
        +get_user_info(...)
    }
    app_py --> auth_py : sử dụng
```
- `app.py` là entrypoint, định nghĩa toàn bộ UI, các hàm gọi API backend, xử lý upload, chat, specs, feedback.
- `auth.py` quản lý xác thực, phân quyền, thông tin user.
- Các hàm `api_*` wrap call đến API Gateway.

## 2. Liên kết với các component khác
- Giao tiếp với **API Gateway** qua HTTP REST (API_BASE_URL).
- Nhận dữ liệu từ user, upload file, gửi câu hỏi, nhận kết quả QA/specs/feedback.
- Hiển thị kết quả, feedback, specs cho user.

---

> Xem thêm các file C4 Level 4 khác cho LLM, Parser, Embedding, Rerank, Vector Search, AI Databases, API Gateway để hiểu toàn bộ kiến trúc code. 