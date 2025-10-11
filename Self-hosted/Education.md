# Self-hosted model

| Tên              | Tổng tham số (parameters)            | Số tham số *kích hoạt* mỗi token (active parameters) |
| ---------------- | ------------------------------------ | ---------------------------------------------------- |
| **gpt-oss-120B** | khoảng 117B parameters               | ~ 5.1B active parameters mỗi token ([OpenAI][1])     |
| **gpt-oss-20B**  | khoảng 21B parameters                | ~-3.6B active parameters mỗi token ([OpenAI][1])     |

[1]: https://openai.com/blog/introducing-gpt-oss/?utm_source=chatgpt.com "Introducing gpt-oss | OpenAI"

# GPU

| Tên              | RAM            | FLOPs  |
| RTX 3060/4090    | 



# Performance
|                  | RTX 3060/4090           | GeForce RTX 5090   | NVIDIA H100/A100    |
| ---------------- | ----------------------- | ------------------ | ------------------- |
| **gpt-oss-120B** | 60 tokens/s             | 256 tokens/s       | ------------------- |
| **gpt-oss-20B**  | khoảng 21B parameters                | ~-3.6B active parameters mỗi token ([OpenAI][1])     | cần ~16GB GPU            |
