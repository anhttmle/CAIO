# Self-hosted model

<h2>
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS_fqRpfkJ-gTspKZPeLmsAFU5x9qAKoDjVag&s" width="24" style="vertical-align:middle; margin-right:8px;">
  gpt-oss-120B
</h2>
<li># Params: 117B</li> 
<li># Active params: 5.1B</li>

<h2>
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS_fqRpfkJ-gTspKZPeLmsAFU5x9qAKoDjVag&s" width="24" style="vertical-align:middle; margin-right:8px;">
  gpt-oss-20B
</h2>
<li># Params: 21B</li> 
<li># Active params: 3.6B</li>

# Infra

| Tên              | Tổng tham số (parameters)            | Số tham số *kích hoạt* mỗi token (active parameters) | Yêu cầu phần cứng dự kiến|
| ---------------- | ------------------------------------ | ---------------------------------------------------- | ------------------------ |
| **gpt-oss-120B** | khoảng 117B parameters               | ~ 5.1B active parameters mỗi token ([OpenAI][1])     | cần ~80GB GPU            |
| **gpt-oss-20B**  | khoảng 21B parameters                | ~-3.6B active parameters mỗi token ([OpenAI][1])     | cần ~16GB GPU            |

[1]: https://openai.com/blog/introducing-gpt-oss/?utm_source=chatgpt.com "Introducing gpt-oss | OpenAI"
