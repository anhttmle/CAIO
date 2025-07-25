# Dev Guide - Hướng dẫn phát triển cho developer mới

## 1. Chuẩn bị môi trường
- Python >= 3.8, pip, Docker, docker-compose
- Clone repo, cd vào `microservices/`
- Cài đặt các thư viện:
  ```bash
  pip install -r requirements.txt
  # hoặc từng service: pip install -r ai_databases/requirements.txt ...
  ```
- Cài đặt Milvus, Postgres (nên dùng docker-compose)

## 2. Cấu trúc code
- Mỗi service 1 folder, có Dockerfile, main.py, requirements.txt
- `shared/`: models, log, file tạm, upload, cấu hình dùng chung
- `BotDocs/`: tài liệu dự án

## 3. Chạy dev/test local
- Chạy từng service bằng lệnh:
  ```bash
  uvicorn main:app --reload --host 0.0.0.0 --port 8000
  ```
- Hoặc chạy toàn bộ bằng docker-compose:
  ```bash
  docker-compose up --build
  ```
- Webapp truy cập tại: http://localhost:8501

## 4. Thêm API mới
- Định nghĩa models ở `shared/models.py` nếu cần
- Thêm route mới vào main.py của service
- Đảm bảo có docstring, type hint, response chuẩn
- Test bằng curl/httpie hoặc Postman

## 5. Thêm tool mới (parser, embedding, ...)
- Viết class tool trong `tools_inventory/`
- Đăng ký tool trong main.py của tools_inventory
- Gọi tool từ core_workers/core_workflows qua API

## 6. Debug & Logging
- Log ghi vào `shared/*.log` (mỗi service 1 file)
- Đọc log bằng tail:
  ```bash
  tail -f shared/ai_databases.log
  ```
- Sử dụng print/logging.debug khi dev local

## 7. Test
- Viết test cho models ở `shared/`, test API bằng pytest hoặc test script
- Ví dụ test model:
  ```python
  from shared import QARequest
  def test_qa():
      req = QARequest(query="abc")
      assert req.query == "abc"
  ```
- Có thể test end-to-end bằng upload file trên webapp

## 8. Best Practice
- Luôn dùng models chung, không trả dict tự do
- Đặt tên API rõ ràng, có docstring
- Validate input bằng Pydantic
- Đảm bảo backward compatibility khi đổi model
- Đọc kỹ log khi debug lỗi

## 9. Lưu ý mở rộng
- Khi thêm service mới: tạo folder, Dockerfile, mount shared, đăng ký vào docker-compose
- Khi thêm field model: cập nhật shared/models.py, test lại các service liên quan
- Khi update dependency: cập nhật requirements.txt từng service

---

> Xem tiếp các file trong BotDocs để biết hướng dẫn specs DB, deploy, ... 