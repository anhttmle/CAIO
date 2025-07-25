# Deploy Guide - Hướng dẫn triển khai hệ thống

## 1. Yêu cầu hệ thống
- Python >= 3.8, Docker, docker-compose
- RAM >= 8GB (nên 16GB+ nếu chạy Milvus)
- Port mở: 8000, 8001, 8501, 5432, 19530, ...

## 2. Build & Run bằng Docker Compose
- Vào thư mục `microservices/`
- Build và chạy toàn bộ hệ thống:
  ```bash
  docker-compose up --build
  ```
- Dừng hệ thống:
  ```bash
  docker-compose down
  ```

## 3. Cấu hình môi trường
- Các biến env đọc từ file `.env` từng service hoặc set trực tiếp trong docker-compose:
  - `OPENAI_API_KEY`, `COHERE_API_KEY`, ...
  - `MILVUS_HOST`, `POSTGRES_HOST`, ...
- Mount shared volume cho tất cả service:
  ```yaml
  volumes:
    - ./shared:/app/shared
  ```

## 4. Healthcheck
- Mỗi service đều có endpoint `/health` trả về trạng thái service và dependency.
- Docker-compose sẽ tự kiểm tra health, chỉ start service khi dependency đã healthy.

## 5. Log & Monitoring
- Log ghi vào file trong `shared/*.log` (mỗi service 1 file)
- Đọc log bằng tail hoặc mount ra ngoài để collect log tập trung.

## 6. Database
- Milvus (vector DB) và PostgreSQL (metadata) chạy bằng container riêng, mount volume để lưu trữ lâu dài.
- Có thể backup/restore data bằng volume hoặc dump.

## 7. Lưu ý production
- Nên dùng reverse proxy (nginx) để expose webapp/api gateway ra ngoài.
- Đặt strong password cho DB, không để default.
- Cấu hình HTTPS nếu public.
- Giới hạn quyền ghi/đọc của shared volume nếu cần bảo mật.
- Theo dõi log healthcheck để phát hiện lỗi sớm.

## 8. Nâng cấp/rollback
- Khi update code, chỉ cần build lại image và restart docker-compose.
- Có thể rollback bằng cách dùng lại image cũ hoặc backup volume.

---

> Xem tiếp các file trong BotDocs để biết hướng dẫn specs DB, webapp, ... 