# Self-hosted model

| Tên              | Tổng tham số (parameters)            | Số tham số *kích hoạt* mỗi token (active parameters) |
| ---------------- | ------------------------------------ | ---------------------------------------------------- |
| **gpt-oss-120B** | khoảng 117B parameters               | ~ 5.1B active parameters mỗi token ([OpenAI][1])     |
| **gpt-oss-20B**  | khoảng 21B parameters                | ~-3.6B active parameters mỗi token ([OpenAI][1])     |

[1]: https://openai.com/blog/introducing-gpt-oss/?utm_source=chatgpt.com "Introducing gpt-oss | OpenAI"

# GPU

| Tên                 | RAM            | FLOPs         |
| ------------------- | -------------- | -------------- |
| GeForce RTX 4090    | 24 GB          |  82.6 TFLOPS   |
| GeForce RTX 5090    | 32 GB          | 104.8 TFLOPS   |
| NVIDIA A100         | 80 GB          | 156   TFLOPS   |
| NVIDIA H100         | 80 GB          | 900   TFLOPS   |

# Performance

|                   | GeForce RTX 4090        | GeForce RTX 5090   | NVIDIA A100         | NVIDIA H100         |
| ----------------- | ----------------------- | ------------------ | ------------------- | ------------------- |
| **gpt-oss-20B**   | 200 tokens/s            | 256 tokens/s       |  150 tokens/s       | 350 tokens/s        |
| **gpt-oss-120B**  | N/A                     | N/A                |  50 tokens/s        | 150 tokens/s        |

# Infra for 20 CCU
>> Assume 10 tokens/s for each user
|                   | GeForce RTX 4090        | GeForce RTX 5090   | NVIDIA A100         | NVIDIA H100         |
| ----------------- | ----------------------- | ------------------ | ------------------- | ------------------- |
| **gpt-oss-20B**   | 1                       | 1                  |  2                  | 1                   |
| **gpt-oss-120B**  | N/A                     | N/A                |  5                  | 2                   |
