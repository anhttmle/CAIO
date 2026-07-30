Paper này là **“Go for a Walk and Arrive at the Answer: Reasoning Over Paths in Knowledge Bases using Reinforcement Learning”** (ICLR 2018), giới thiệu **MINERVA**: một agent Reinforcement Learning (RL) trả lời truy vấn trên Knowledge Graph bằng cách “đi bộ” qua các cạnh quan hệ để tới entity đáp án. Ý tưởng then chốt là: thay vì chấm điểm mọi entity trong graph như các model embedding, agent học một **policy phụ thuộc vào query** để chỉ khám phá các đường đi có triển vọng. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## Bài toán trực giác

Knowledge Base (KB) lưu fact dưới dạng triple:

\[
(e_1, r, e_2)
\]

Trong đó:

- \(e_1, e_2 \in \mathcal{E}\): entity, ví dụ `Malala_Yousafzai`, `Pakistan`
- \(r \in \mathcal{R}\): quan hệ nhị phân, ví dụ `Nationality`, `WorksFor`
- \(\mathcal{E}\): tập tất cả entity
- \(\mathcal{R}\): tập tất cả relation

Từ KB, ta có Knowledge Graph có hướng, có nhãn:

\[
G = (V, E, \mathcal{R})
\]

- \(V = \mathcal{E}\): node là entity.
- \(E \subseteq V \times \mathcal{R} \times V\): cạnh là fact có dạng `(source entity, relation, destination entity)`.
- Đây là **directed labeled multigraph**: cạnh có chiều, có nhãn relation, và có thể có nhiều cạnh khác nhãn nối cùng hai node. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

Query cần trả lời có dạng:

\[
(e_1^q, r_q, ?)
\]

Ví dụ:

\[
(\text{Toronto}, \text{LocatedIn}, ?)
\]

Mục tiêu là suy ra entity \(e_2^q\), chẳng hạn `Canada`. Nhưng điều quan trọng là lời giải không nhất thiết là cạnh trực tiếp. Agent có thể tìm một **reasoning path** như:

\[
\text{Toronto}
\xrightarrow{\text{LocatedIn}}
\text{Ontario}
\xrightarrow{\text{LocatedIn}}
\text{Canada}
\]

Trực giác: relation query `LocatedIn` không chỉ là “nhãn cần dự đoán”; nó là **mục đích điều hướng**. Cùng đứng ở một node, nếu câu hỏi là `WorksFor` thì agent nên ưu tiên quan hệ dẫn tới tổ chức/công ty; nếu là `BornIn` thì ưu tiên đường qua location. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## Vì sao cần MINERVA?

Các model Knowledge Graph embedding như DistMult, ComplEx, ConvE thường tính score cho mọi candidate answer \(x \in \mathcal{E}\):

\[
\operatorname{score}(e_1^q, r_q, x)
\]

Sau đó xếp hạng toàn bộ entity. Cách này mạnh với pattern thống kê nhưng inference thường có chi phí phụ thuộc vào tổng số entity, xấp xỉ \(O(|\mathcal{E}|)\) cho mỗi query.  [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

MINERVA thay góc nhìn:

> “Đừng hỏi entity nào trong hàng triệu entity là đáp án; hãy bắt đầu từ entity nguồn và học cách đi tới vùng graph nơi đáp án có khả năng nằm.”

Do đó inference chỉ xét các cạnh lân cận dọc các path được policy chọn. Nó vừa có khả năng tạo reasoning chain nhiều bước, vừa trả về path như một dạng **provenance / lời giải có thể diễn giải**. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## Query answering khác fact prediction

Paper phân biệt hai bài toán thường bị gộp chung:

| Bài toán | Input | Output | Agent có biết answer lúc ra quyết định? |
|---|---|---|---|
| Fact prediction | \((e_1,r,e_2)\) | Fact có đúng không? | Có, vì \(e_2\) nằm trong input |
| Query answering | \((e_1,r,?)\) | Tìm \(e_2\) | Không, phải tự tìm |
| MINERVA | \((e_1^q,r_q,?)\) | Node đáp án | Không biết \(e_2^q\) trong quá trình walk |

Điểm này giải thích khác biệt với DeepPath. DeepPath tìm path khi đã biết cả source lẫn target, nên phù hợp hơn với việc xác minh fact. MINERVA khó hơn: target bị che giấu và agent phải khám phá graph để suy ra target. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## MDP: biến suy luận thành điều hướng

MINERVA mô hình hóa KB-QA thành một **finite-horizon deterministic partially observable Markov decision process** (POMDP/MDP quan sát một phần) trên graph. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Trạng thái thật

Ở step \(t\), trạng thái môi trường là:

\[
S_t = (e_t, e_1^q, r_q, e_2^q)
\]

Ý nghĩa từng đại lượng:

- \(e_t\): node hiện tại của agent sau \(t\) bước.
- \(e_1^q\): entity đầu vào của query, tức điểm xuất phát.
- \(r_q\): query relation cần trả lời.
- \(e_2^q\): entity đáp án đúng trong training triple.

Tại training, môi trường biết \(e_2^q\) để tính reward. Nhưng agent **không được nhìn thấy** \(e_2^q\), bởi test time không có đáp án. Đây là nguyên nhân bài toán là *partially observable*. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Observation

Observation mà agent thực sự nhận là:

\[
O(S_t) = (e_t, e_1^q, r_q)
\]

Nó biết:

- Đang ở đâu: \(e_t\)
- Ban đầu xuất phát từ đâu: \(e_1^q\)
- Đang cần trả lời loại quan hệ nào: \(r_q\)

Nó không biết \(e_2^q\). Nếu agent thấy target, bài toán sẽ biến thành route finding “đến node đã biết”, thay vì QA thực sự. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Action

Tại node hiện tại \(e_t\), agent có thể chọn một outgoing edge:

\[
A_t = (e_t, r, v)
\]

Trong đó:

- \(r\): relation label của cạnh được chọn
- \(v\): destination entity
- Chọn action này tức là đi từ \(e_t\) đến \(v\)

Tập action hợp lệ tại trạng thái \(S_t\) là:

\[
\mathcal{A}_{S_t}
=
\{(e_t, r, v) \in E\}
\cup
\{\text{NOOP}\}
\]

`NOOP` là self-loop: ở nguyên node hiện tại. Nó cho phép triển khai mọi query với cùng horizon \(T\), kể cả khi câu hỏi dễ chỉ cần một bước. Nếu đáp án đã đạt được ở step sớm, agent tiếp tục chọn `NOOP` cho các bước còn lại. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Inverse relations

Với mỗi triple:

\[
(e_1, r, e_2)
\]

paper thêm cạnh ngược:

\[
(e_2, r^{-1}, e_1)
\]

Ví dụ:

\[
(\text{Toronto}, \text{LocatedIn}, \text{Canada})
\Rightarrow
(\text{Canada}, \text{LocatedIn}^{-1}, \text{Toronto})
\]

Đây không phải chỉ để tăng dữ liệu. Nó có chức năng điều hướng quan trọng: agent đi nhầm có thể quay lại node trước thay vì bị kẹt. Thí nghiệm minh họa agent có thể đi sai ở bước đầu, dùng inverse edge quay lại, rồi đi theo relation đúng để đến đáp án. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Transition

Transition là deterministic:

\[
\delta(S_t, A_t)
=
(v, e_1^q, r_q, e_2^q)
\]

Nếu action là \(A_t=(e_t,r,v)\), agent chắc chắn đến \(v\). Không có randomness từ môi trường; randomness chỉ đến từ policy khi sampling action. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Reward thưa

Reward chỉ cấp ở terminal step \(T\):

\[
R(S_T) =
\begin{cases}
1, & \text{nếu } e_T=e_2^q \\
0, & \text{ngược lại}
\end{cases}
\]

Nói cách khác, không có reward cho “đi đúng hướng”, “đi qua relation hợp lý”, hay “đến gần đáp án”. Chỉ khi endpoint đúng chính xác thì reward bằng 1. Đây là **sparse terminal reward**, khiến credit assignment khó: nếu path thất bại, agent không biết chính xác bước nào đã sai. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## Policy network

Policy phải trả lời: “Với query này, lịch sử đã đi này, và các cạnh hiện có, tôi nên chọn cạnh nào tiếp theo?”

Paper dùng **LSTM** để nhớ path history, embedding cho entity/relation, rồi dùng MLP để chấm điểm các action hợp lệ. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Embedding

Hai embedding matrix được học:

\[
\mathbf{r} \in \mathbb{R}^{|\mathcal{R}| \times d}
\]

\[
\mathbf{e} \in \mathbb{R}^{|\mathcal{E}| \times d}
\]

Trong đó:

- \(d\): embedding dimension
- \(\mathbf{r}\): mỗi relation có một vector \(d\)-chiều
- \(\mathbf{e}\): mỗi entity có một vector \(d\)-chiều

Paper dùng embedding relation và entity kích thước 200 trong các thí nghiệm chính. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

Một action thực chất chứa cả loại cạnh lẫn node đích. Với action đi qua relation \(l\) đến entity \(d\), embedding action là:

\[
[\mathbf{r}_l ; \mathbf{e}_d]
\]

Dấu \([\, ; \,]\) là phép **concatenation**, nên vector action có kích thước \(2d\). Trực giác: chỉ relation là chưa đủ, vì hai cạnh cùng relation có thể dẫn đến hai entity rất khác nhau; chỉ destination cũng chưa đủ, vì relation đã đi mang ý nghĩa reasoning riêng. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### LSTM nhớ lịch sử

Lịch sử tại step \(t\) được ký hiệu:

\[
H_t = (H_{t-1}, A_{t-1}, O_t)
\]

LSTM nén lịch sử đó thành hidden state:

\[
\mathbf{h}_t
=
\operatorname{LSTM}
\left(
\mathbf{h}_{t-1},
[\mathbf{a}_{t-1}; \mathbf{o}_t]
\right)
\tag{1}
\]

Trong đó:

- \(\mathbf{h}_{t-1}\): memory trước đó của agent
- \(\mathbf{a}_{t-1}\): relation embedding của action vừa chọn ở step trước
- \(\mathbf{o}_t\): embedding entity tại node hiện tại \(e_t\)
- \(\mathbf{h}_t \in \mathbb{R}^{2d}\): biểu diễn liên tục của path history theo paper
- \([\mathbf{a}_{t-1}; \mathbf{o}_t]\): input tại step \(t\), ghép “vừa đi qua quan hệ gì” với “hiện đứng ở entity nào” [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

Intuition của \(\mathbf{h}_t\): current node đơn lẻ thường không đủ để chọn action đúng. Một entity như `Washington` có thể được đến từ nhiều route và mang vai trò reasoning khác nhau theo từng query. LSTM lưu lại các relation/entity đã gặp, nhờ đó policy có thể chọn action phụ thuộc vào **toàn bộ chain**, không chỉ local neighborhood. Ablation bỏ history gây giảm mạnh: trên KINSHIP, HITS@1 giảm 27 điểm phần trăm và HITS@10 giảm 13 điểm. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Query-conditioned action scoring

Tại \(e_t\), giả sử có \(k=|\mathcal{A}_{S_t}|\) action hợp lệ. Paper tạo action matrix:

\[
\mathbf{A}_t
\in
\mathbb{R}^{k \times 2d}
\]

Mỗi hàng là embedding \([\mathbf{r}_l;\mathbf{e}_d]\) của một outgoing edge. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

Context vector để quyết định gồm:

\[
[\mathbf{h}_t;\mathbf{o}_t;\mathbf{r}_{q}]
\]

Trong đó \(\mathbf{r}_{q}\) là embedding của query relation \(r_q\). Qua MLP hai tầng:

\[
\mathbf{z}_t
=
\mathbf{W}_2
\operatorname{ReLU}
\left(
\mathbf{W}_1
[\mathbf{h}_t;\mathbf{o}_t;\mathbf{r}_{q}]
\right)
\]

Sau đó score từng action và normalize:

\[
\mathbf{d}_t
=
\operatorname{softmax}
\left(
\mathbf{A}_t \mathbf{z}_t
\right)
\]

\[
A_t \sim \operatorname{Categorical}(\mathbf{d}_t)
\]

Ý nghĩa:

- \(\mathbf{W}_1,\mathbf{W}_2\): tham số MLP học cách biến context thành “hướng đi mong muốn”.
- \(\operatorname{ReLU}\): phi tuyến, giúp model học logic điều kiện phức tạp.
- \(\mathbf{A}_t\mathbf{z}_t\): dot product giữa “mỗi action đang có” và “action profile mà context mong muốn”.
- \(\operatorname{softmax}\): biến score thành phân phối xác suất trên chỉ các cạnh hợp lệ.
- \(\operatorname{Categorical}\): sampling một action rời rạc từ phân phối đó. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

Công thức trong PDF có ký hiệu hơi không nhất quán ở phần observation/query embedding; cách diễn giải đúng theo đoạn văn là policy phải kết hợp **history \(h_t\)**, **entity hiện tại \(e_t\)**, và **query-relation \(r_q\)**. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Một policy dùng cho mọi relation

Thay vì train một classifier hoặc rule-set cho từng query relation, MINERVA train **một policy chung**. Nhờ đó, knowledge học từ relation phổ biến có thể hỗ trợ relation ít dữ liệu hơn, đồng thời không phải maintain hàng nghìn model khi graph có nhiều relation type. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## Mục tiêu tối ưu

Paper tối đa hóa expected terminal reward:

\[
J(\theta)
=
\mathbb{E}_{
(e_1,r,e_2)\sim \mathcal{D},
A_1,\ldots,A_{T-1}\sim \pi_\theta
}
\left[
R(S_T)
\mid
S_1=(e_1,e_1,r,e_2)
\right]
\]

Trong đó:

- \(\theta\): toàn bộ parameter của policy, gồm entity/relation embeddings, LSTM, MLP weights và biases.
- \(\mathcal{D}\): phân phối dữ liệu training triples.
- \(S_1=(e_1,e_1,r,e_2)\): ở đầu episode, agent đứng tại source \(e_1\); source query cũng là \(e_1\).
- \(\pi_\theta\): policy sinh distribution trên action.
- \(A_1,\dots,A_{T-1}\): chuỗi action được sample.
- \(S_T\): terminal state.
- \(R(S_T)\in\{0,1\}\): reward cuối.

Nói đơn giản: tối ưu \(\theta\) sao cho nếu lấy một fact training, cho agent khởi hành từ head/source và chọn đường đi theo policy, xác suất kết thúc đúng tail/answer cao nhất có thể. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## REINFORCE và vấn đề gradient

Không thể backprop trực tiếp qua action sampling rời rạc:

\[
A_t \sim \operatorname{Categorical}(\mathbf{d}_t)
\]

Do đó paper dùng **REINFORCE**, một policy-gradient estimator. Dạng trực giác:

\[
\nabla_\theta J(\theta)
\approx
\sum_{t}
(R-b)\nabla_\theta \log \pi_\theta(A_t \mid H_t)
\]

Trong đó:

- \(\log \pi_\theta(A_t \mid H_t)\): log-probability policy gán cho action đã lấy.
- \(\nabla_\theta \log \pi_\theta(\cdot)\): hướng điều chỉnh parameter để action này trở nên xác suất hơn hoặc ít xác suất hơn.
- \(R\): outcome cuối episode.
- \(b\): baseline/control variate.

Nếu rollout đạt đáp án, \(R=1\), gradient tăng probability của toàn bộ action sequence đã dẫn tới thành công. Nếu thất bại, reward thấp, policy giảm xu hướng lặp lại trajectory đó. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Baseline giảm variance

Do reward rất sparse và sampling gây nhiễu lớn, paper dùng moving average của cumulative discounted reward làm baseline \(b\). Trực giác:

- Nếu reward tốt hơn mức trung bình, \(R-b>0\): củng cố hành động.
- Nếu reward kém hơn mức trung bình, \(R-b<0\): làm hành động bớt được chọn.
- Baseline không đổi expected gradient, nhưng giảm variance, giúp train ổn định hơn. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

Paper dùng 20 rollouts cho mỗi training example để xấp xỉ expectation trên các trajectory mà policy có thể sinh ra. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Entropy regularization

Loss còn có entropy regularization với hệ số \(\beta\):

\[
\mathcal{L}
\approx
-\mathbb{E}[R]
-
\beta \sum_t \mathcal{H}(\pi_\theta(\cdot\mid H_t))
\]

Entropy của policy là:

\[
\mathcal{H}(\pi)
=
-\sum_{a \in \mathcal{A}_{S_t}}
\pi(a)\log \pi(a)
\]

Entropy cao nghĩa là action distribution còn đa dạng; entropy thấp nghĩa là policy quá tự tin vào ít action. Thêm term này trong training ngăn policy sớm collapse vào một vài path tình cờ thành công, khuyến khích khám phá alternative paths. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## Train và inference

### Training

Với mỗi triple train \((e_1,r,e_2)\):

1. Khởi tạo agent tại \(e_1\), query là \((e_1,r,?)\).
2. Sample một hoặc nhiều trajectory dài tối đa \(T\).
3. Chỉ cấp reward 1 nếu endpoint đúng là \(e_2\).
4. Dùng REINFORCE, baseline và entropy regularization để update \(\theta\).
5. Lặp lại đến khi policy học được path patterns tổng quát. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Inference

Ở test time, agent không có \(e_2\). Paper dùng **beam search** với beam width 50:

- Giữ 50 partial trajectories có xác suất cao nhất.
- Mở rộng các trajectory qua action hợp lệ.
- Rank entity đích theo xác suất của trajectory dẫn đến nó.
- Entity không được beam reach nhận rank vô cực. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

Beam search thay sampling ngẫu nhiên bằng một chiến lược tìm kiếm có kiểm soát, phù hợp khi cần top-\(k\) answers và đánh giá theo ranking metrics. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## Các concept reasoning quan trọng

### Multi-hop reasoning

Nếu fact cần suy luận qua nhiều relation:

\[
\text{Person}
\xrightarrow{r_1}
\text{Organization}
\xrightarrow{r_2}
\text{Location}
\]

thì MINERVA thực hiện hard discrete selection ở từng hop. Đây là khác biệt lớn với embedding model, vốn thường suy luận gián tiếp qua hình học không gian vector hơn là sinh một evidence path rõ ràng. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Rule learning ngầm

MINERVA không xuất rule symbolic rõ ràng, nhưng có thể học policy tương ứng với rule như:

\[
\operatorname{LocatedIn}(X,Y)
\Leftarrow
\operatorname{NeighborOf}(X,Z)
\land
\operatorname{LocatedIn}(Z,Y)
\]

hoặc rule ba bước:

\[
\operatorname{LocatedIn}(X,Y)
\Leftarrow
\operatorname{NeighborOf}(X,Z)
\land
\operatorname{NeighborOf}(Z,W)
\land
\operatorname{LocatedIn}(W,Y)
\]

Trực giác: path type \((\text{NeighborOf}, \text{LocatedIn})\) hoạt động như một Horn rule body; endpoint là conclusion. Khác với ILP cổ điển, rule này được biểu diễn ngầm trong parameters của LSTM + MLP policy. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

### Path type

Paper gọi **path type** là chuỗi relation, bỏ qua entity cụ thể:

\[
(r_1,r_2,\dots,r_L)
\]

Ví dụ mọi path dạng:

\[
\text{Person}
\xrightarrow{\text{WorksFor}}
\text{Company}
\xrightarrow{\text{LocatedIn}}
\text{City}
\]

có chung path type \((\text{WorksFor},\text{LocatedIn})\). MINERVA tổng quát hóa tốt khi path type có tính lặp lại đủ nhiều trong graph, vì agent có thể học rằng loại chain này dự báo tốt cho một query relation. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

## Kết quả thực nghiệm

MINERVA mạnh khi dữ liệu cần reasoning path và relation pattern lặp lại; không phải lúc nào cũng thắng embedding model, nhất là graph nhỏ hoặc benchmark thiên về link-prediction thống kê. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)

| Dataset / thiết lập | Kết quả đáng chú ý |
|---|---|
| COUNTRIES S3 | MINERVA đạt AUC-PR 95.10, cao hơn các baseline được báo cáo; S3 là task đòi hỏi reasoning khó nhất trong bộ này.  [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735) |
| WN18RR | MINERVA đạt HITS@1 0.413, cao hơn ComplEx 0.382, ConvE 0.403 và DistMult 0.410; HITS@10 là 0.513.  [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735) |
| NELL-995 | MINERVA đạt HITS@1 0.663 và HITS@10 0.831; cạnh tranh với embedding baselines và vượt path-baseline rõ rệt.  [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735) |
| FB15K-237 | MINERVA HITS@10 0.456, thấp hơn ConvE 0.600; paper giải thích tập này có nhiều one-to-many relation và benchmark chỉ chọn một target triple, không hoàn toàn phù hợp với endpoint-based QA.  [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735) |
| WikiMovies | Với câu hỏi tự nhiên dạng template, MINERVA đạt accuracy 96.7, cao hơn NeuralLP 94.6 trong bảng paper.  [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735) |
| Gridworld | Agent giảm ít hơn NeuralLP khi path length tăng, cho thấy khả năng xử lý reasoning chain dài.  [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735) |

## WikiMovies: bước sang câu hỏi ngôn ngữ

Với WikiMovies, query không còn relation schema cố định mà là câu như “Which is a film written by Herb Freed?”. Paper entity-link entity trong câu vào KB bằng string matching, rồi biểu diễn phần query relation bằng trung bình embedding của các từ trong question:

\[
\mathbf{r}_q
\approx
\frac{1}{n}
\sum_{i=1}^{n}
\mathbf{w}_i
\]

Trong đó:

- \(n\): số token trong câu hỏi.
- \(\mathbf{w}_i\): embedding học được của token thứ \(i\).
- Vector trung bình đóng vai trò query representation thay cho embedding relation schema.

Đây là “partially structured query”: entity source được link rõ vào KB, còn ý định relation lấy từ text. Paper thừa nhận WikiMovies chỉ cần \(T=1\), nên chưa chứng minh được năng lực natural-language multi-hop reasoning ở mức khó; nhưng nó cho thấy policy MINERVA không bị buộc phải nhận relation ID cố định.

## Hiệu quả tính toán

Embedding models cần rank mọi entity nên test-time thường có chi phí \(O(|\mathcal{E}|)\). MINERVA chủ yếu tính score cho outgoing edges dọc beam/path, nên chi phí phụ thuộc vào degree distribution và search horizon hơn là số entity toàn graph.

Paper báo cáo trên test set:

- WN18RR: MINERVA mất 63 giây, DistMult GPU mất 211 giây.
- NELL-995: MINERVA mất 35 giây, DistMult GPU mất 115 giây. 

Điểm cần hiểu đúng: lợi thế này rõ nhất khi graph lớn, degree local không quá cực đoan, và beam width/horizon được kiểm soát. Nếu node hub có degree cực lớn hoặc beam quá rộng, policy scoring vẫn có thể tốn đáng kể.

## Hạn chế

- **Sparse reward:** reward chỉ có ở endpoint nên exploration ban đầu khó, đặc biệt khi đáp án xa hoặc graph nhiều nhánh.
- **Closed-world entity set:** agent chỉ trả lời được bằng node đã tồn tại trong graph; không sinh entity mới hay dùng evidence văn bản ngoài graph.
- **Reachability:** nếu đáp án đúng không có path còn lại trong observed graph sau khi loại train/test leakage, agent không thể đến nó.
- **One-to-many evaluation mismatch:** một query có thể có nhiều đáp án đúng về ngữ nghĩa, nhưng benchmark có thể chỉ đánh giá một triple target; agent đi tới đáp án “cũng đúng” nhưng khác target vẫn bị phạt.
- **Interpretability có điều kiện:** path là evidence dễ xem, nhưng không mặc định là quan hệ nhân quả hay proof logic hợp lệ tuyệt đối; nó là trajectory policy thấy hữu ích để tối đa reward.

## Liên hệ với Graph RAG hiện nay

Nếu diễn giải bằng ngôn ngữ Graph RAG hiện đại, MINERVA gần với một **learned graph retriever / reasoning controller** hơn là LLM generator:

- **Retriever:** policy chọn node/cạnh để retrieve một subgraph/path liên quan query.
- **Planner:** LSTM state ghi nhớ route đã đi, tương tự latent reasoning state.
- **Evidence:** endpoint path và relation chain là provenance có thể đưa vào LLM.
- **Generator:** không có trong paper; answer chính là entity endpoint.

Một kiến trúc hiện đại có thể dùng LLM để parse câu hỏi thành \((e_1^q,r_q)\) hoặc query embedding, dùng policy kiểu MINERVA/Graph Neural Search để lấy top-\(k\) evidence paths, rồi dùng LLM tổng hợp đáp án có citation theo path. Điểm mạnh của paper vẫn rất relevant: **retrieval trên graph nên query-aware, step-wise, và có mục tiêu rõ**, thay vì random walk hoặc lấy neighborhood cố định. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/105690343/61a3fabf-6c29-41ec-86ce-77a8dd9291ca/2.-Go4aWalk.pdf?AWSAccessKeyId=ASIA2F3EMEYEZQHY3WQS&Signature=R3f2SNdOyYDSp4RIXcpYCbjKtaI%3D&x-amz-security-token=IQoJb3JpZ2luX2VjEMT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJHMEUCIQCY3mxoIA4H8PuFpY94k2%2FWjZnDhq0sDlkTws3f5EjbrwIgeGSXH%2FuGKxo07%2FqnADLP7fJTSg6UrRGPLPayApDcE%2BQq%2FAQIjP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARABGgw2OTk3NTMzMDk3MDUiDKwoBMyBnY6WfsTlZirQBNIs7qV7ljLuDjHT%2F%2FEhw29Bv9zV18CwUFgk9AcEcCMguzWUEPuZOipZSAefv4wLW%2FXwKQQFxPVWKGra3OmmkUOf5zSqWleNB3asLqiIJNvNYAuuaksipu6FuUZAflNZKYGKzZ4ygz5WNE8leaFwExH53Mcn1OsFKVnz8ciOUM%2B2SyA6GHLEIdXcGixFRKG6JPBNcOBiiIKrY%2BTvBPFiNtHDailpRnSbMXfuGSq6x2E%2BOljvIt99qb3ToeYgsFGA9BmRx2%2FaTz4A4Il7IQkns5l6KBOHRgnJ%2F%2FKunaEUPZkT7pITrZMYCrb6huIxJJ05YkrOoU4BWNfDRFeUASVhE%2BpGy05Ur8aBg4UHmKhQdnYKgq9RiaT%2BzUdxN87x6ML7PPEHbGg9hcn9qtXbbXNGgpshpM78FJSmbS99XaIABtEmTOUN45NyMmdUWj%2Fuo5sJU5H0ahj8Dt8MvWjuuLx88RumPL%2Bo0dH8MTUX3VAkmh%2BF%2B6Q80q9lhLOfA%2FaNipB8V6%2Fot%2Fj1TcO0dk1EgAwvgEA3cZS1NbpzZtZfEQIepUhZV2F7lFv4Jl4vxtKAI%2BCaAG1OVTcgkv5ysn7sM2pH%2Fs1eNneBdCmJgkY4WvXTOfTSXtZFB%2BhfES%2FkF4PKf%2BjophxHcfSMPxYCS1NXhGc1tNDYt0NkYIJ9NgPxonUrKNsRDHqcXAK90ktjz%2FY0T9ssfdxTq4LLQEPRn3tDacliq8JCRUBS8NP44VoxBc2BDSHs9OiKkLKG63%2FyFJPcZjefisNg6XlShx6LFupyFs4sm6cwzIKr0wY6mAG5pyywA6SbMfeZOlpL%2BiikQSo7xSzvwIN%2BLAspIq6lKkqFRoNFSUEgL6DgzZwMdoX2wVixvuO6IWoLu2JVjTqj%2BqljIPdg8KTFtJf9UObVawFO3mbJWlUOto1S1JU4N4LJUBylNWhOW9B6t6ZYLk2YwNZXVlTrbBtjjwJ2UJ6m4gRwY8fyizQ0dMdh3ZAC%2BbkAnLbf1pO7sQ%3D%3D&Expires=1785384735)
