# Translation-based Embedding: từ ký hiệu rời rạc sang không gian KG liên tục

Phần này giải thích vì sao DeepPath dùng **translation-based embedding** để biến entity và relation từ ký hiệu rời rạc thành vector liên tục, rồi dùng các vector đó làm state cho agent RL suy luận trong knowledge graph.[1][2]

## 1. Bài toán gốc: ký hiệu rời rạc không “tính toán” được

Knowledge graph gốc chỉ chứa các triple như:

```text
(Paris, capitalOf, France)
```

Ở dạng này, `Paris`, `capitalOf`, và `France` chỉ là ID hoặc string; máy tính không tự biết `Paris` gần `London` hơn `Banana`, hay `capitalOf` giống `locatedIn` hơn `bornIn`.[2] Vì thế, nếu chỉ làm việc trong không gian rời rạc, agent rất khó so sánh, nội suy và tổng quát hóa giữa các entity hoặc relation tương tự.[2]

Cách giải là ánh xạ mỗi entity và relation thành một vector trong không gian thấp chiều, tức knowledge graph embedding.[3] DeepPath nói rõ rằng nó dùng các **translation-based embeddings** như TransE và TransH để biểu diễn entity/relation, từ đó xây dựng continuous state cho RL agent.[2]

## 2. Intuition của translation-based embedding

Ý tưởng cốt lõi là xem mỗi quan hệ như một phép tịnh tiến trong không gian vector.[2][4] Nếu triple \
$$ (h, r, t) \
$$ là đúng, mô hình muốn thỏa điều kiện:

$$
\mathbf{h} + \mathbf{r} \approx \mathbf{t}
$$

Hiểu hình học thì rất đơn giản: đứng ở điểm `h`, đi theo “mũi tên” `r`, sẽ đến gần điểm `t`.[4] Vì vậy, một triple càng hợp lý thì khoảng cách giữa \
$$ \mathbf{h} + \mathbf{r} \
$$ và \
$$ \mathbf{t} \
$$ càng nhỏ.[4]

Một score function điển hình là:

$$
f_r(h,t) = \|\mathbf{h} + \mathbf{r} - \mathbf{t}\|_{L1/L2}
$$

Giá trị này càng nhỏ thì triple càng plausible theo embedding model.[4]

## 3. TransE: mô hình đơn giản nhất

Trong TransE, mọi entity và relation đều nằm chung trong một không gian \
$$ \mathbb{R}^d \
$$, và mô hình học sao cho triple đúng có score tốt hơn triple sai với một khoảng margin.[4][2] DeepPath cũng xếp TransE vào nhóm embedding baselines và dùng cùng tinh thần biểu diễn liên tục cho state của agent.[2]

Loss kinh điển của TransE là margin ranking loss:

$$
\mathcal{L} = \sum_{(h,r,t)\in S^+} \sum_{(h',r,t')\in S^-}
\big[ f_r(h,t) + \gamma - f_r(h',t') \big]_+
$$

Trong đó \
$$
[x]_+ = \max(0, x) \
$$, nghĩa là triple đúng phải “gần” hơn triple sai ít nhất một lượng \
$$ \gamma \
$$.[4]

### Điểm mạnh của TransE

- Đơn giản, dễ huấn luyện, scale tốt trên KG lớn.[4]
- Hoạt động khá tốt với quan hệ 1-1.[4]
- Trực giác hình học rõ ràng, dễ dùng để tạo state liên tục cho RL.[2]

### Hạn chế của TransE

TransE gặp khó với các quan hệ 1-N, N-1 và N-N vì một phép cộng \
$$ \mathbf{h} + \mathbf{r} \
$$ rất khó đồng thời gần nhiều đích khác nhau.[2] Đây là một lý do khiến DeepPath không chỉ nhắc đến TransE mà còn dùng cả TransH như một lựa chọn embedding để biểu diễn tốt hơn các kiểu quan hệ phức tạp.[2]

## 4. TransH: giữ ý tưởng translation nhưng thêm hyperplane

TransH mở rộng TransE bằng cách cho mỗi relation có một hyperplane riêng, thay vì ép mọi quan hệ phải dùng cùng một kiểu dịch chuyển trong toàn bộ không gian.[2] Cụ thể, với mỗi relation \
$$ r \
$$, mô hình học một vector pháp tuyến \
$$ \mathbf{w}_r \
$$ để xác định hyperplane, và một vector dịch chuyển \
$$ \mathbf{d}_r \
$$ nằm trên hyperplane đó.[2]

Trước tiên entity được chiếu lên hyperplane của relation:

$$
\mathbf{h}_{\perp} = \mathbf{h} - \mathbf{w}_r^\top \mathbf{h}\,\mathbf{w}_r
$$

$$
\mathbf{t}_{\perp} = \mathbf{t} - \mathbf{w}_r^\top \mathbf{t}\,\mathbf{w}_r
$$

Sau đó mới áp điều kiện translation:

$$
\mathbf{h}_{\perp} + \mathbf{d}_r \approx \mathbf{t}_{\perp}
$$

Điểm hay của TransH là cùng một entity có thể có “vai trò hình học” khác nhau dưới các relation khác nhau, nên mô hình hóa các quan hệ nhiều-ngôi linh hoạt hơn TransE.[2] Với DeepPath, điều này quan trọng vì state embedding càng phản ánh đúng cấu trúc quan hệ thì policy network càng dễ học cách chọn bước đi hợp lý.[2]

## 5. DeepPath dùng embedding này như thế nào

DeepPath mô tả state của agent là continuous state dựa trên knowledge graph embeddings.[2] Trong paper, state tại bước \
$$ t \
$$ được viết là:

$$
\mathbf{s}_t = (\mathbf{e}_t, \mathbf{e}_{target} - \mathbf{e}_t)
$$

Trong đó \
$$ \mathbf{e}_t \
$$ là embedding của entity hiện tại và \
$$ \mathbf{e}_{target} \
$$ là embedding của entity đích.[2] Thành phần thứ nhất cho biết agent đang ở đâu trên “bản đồ” KG, còn thành phần thứ hai cho biết hướng và độ lệch còn lại tới đích.[2]

Paper cũng nói rõ: “the state vector we use has a dimension of 200”, và DeepPath dùng cùng dimension với TransE/TransR để embed entity.[2] Điều này có nghĩa policy network không nhận one-hot vector khổng lồ của hàng chục nghìn entity, mà nhận một vector thực 200 chiều gọn hơn và có ngữ nghĩa hình học.[2]

## 6. Vì sao continuous state giúp RL tốt hơn

Nếu chỉ dùng ký hiệu rời rạc, hai entity giống nhau về ngữ nghĩa vẫn hoàn toàn tách biệt ở đầu vào; mô hình không có khái niệm “gần nhau”.[2] Khi dùng embedding liên tục, hai entity gần nhau trong KG vector space sẽ tạo ra state gần nhau, nên policy có thể học hành vi tương tự và generalize tốt hơn sang các entity chưa gặp nhiều trong train.[2]

DeepPath nhấn mạnh chính điểm này khi đối chiếu với PRA: PRA hoạt động trong không gian hoàn toàn rời rạc, còn DeepPath reason trong continuous vector space của KG.[2] README của codebase cũng mô tả hệ thống là policy-based agent with continuous states based on knowledge graph embeddings.[1]

## 7. Action, transition và reward trong môi trường DeepPath

Trong DeepPath, action space là tập tất cả relation trong KG.[2] Agent bắt đầu từ source entity, mỗi bước chọn một relation để mở rộng path; nếu relation đó nối sang entity mới thì agent chuyển state sang entity tiếp theo.[2]

Reward của DeepPath không chỉ có đúng/sai toàn cục mà còn cộng thêm efficiency và diversity.[2] Đáng chú ý, diversity reward dùng embedding của cả path bằng cách cộng các relation trên path, tức \
$$ p = \sum_i r_i \
$$, rồi đo cosine similarity với các path đã có.[2] Điều này cho thấy embedding không chỉ dùng ở mức entity state mà còn được tận dụng để đánh giá chất lượng reasoning path.[2]

## 8. Pipeline đầy đủ

Toàn bộ pipeline có thể hiểu ngắn gọn như sau:

```text
KG triples
  -> train TransE / TransH offline
  -> tạo entity2vec / relation2vec
  -> RL environment dùng state s_t = (e_t, e_target - e_t)
  -> policy network chọn relation tiếp theo
  -> reward đánh giá path theo accuracy, efficiency, diversity
```

README của DeepPath ghi rõ các file như `entity2vec.bern` và `relation2vec.bern` được dùng để biểu diễn RL states, đồng thời các thư mục task còn chứa TransH, TransD và TransR embeddings cho từng tác vụ.[1] Điều này xác nhận embedding được huấn luyện trước rồi dùng như representation cố định trong môi trường RL, thay vì học end-to-end cùng policy trong lúc reasoning.[1][2]

## 9. Ví dụ trực quan nhỏ

Giả sử có embedding hai chiều để minh họa:

| Ký hiệu | Vector giả định |
|---|---|
| Paris | (1.0, 2.0) |
| capitalOf | (2.0, 0.5) |
| France | (3.0, 2.5) |
| London | (1.2, 1.8) |
| UK | (3.1, 2.3) |

Khi đó:

$$
\mathbf{Paris} + \mathbf{capitalOf} = (3.0, 2.5) \approx \mathbf{France}
$$

và

$$
\mathbf{London} + \mathbf{capitalOf} = (3.2, 2.3) \approx \mathbf{UK}
$$

Ví dụ này cho thấy relation `capitalOf` thực sự đóng vai trò như một vector dịch chuyển; các thành phố thủ đô khác nhau có thể chia sẻ cùng một “hướng đi” tới quốc gia tương ứng. Đây chính là loại cấu trúc hình học mà DeepPath muốn tận dụng để agent có thể suy luận path tốt hơn trên KG liên tục.[2][4]

## 10. Ý nghĩa quan trọng nhất

Điểm cốt lõi không phải chỉ là “đổi ID thành vector”, mà là biến KG từ một tập ký hiệu không có phép đo thành một không gian có khoảng cách, hướng và phép cộng vector.[3][2] Nhờ vậy, DeepPath có thể xây agent RL hoạt động trên continuous state, chọn relation như một chuỗi quyết định có định hướng, và học được các reasoning path hiệu quả hơn so với cách tìm đường thuần rời rạc.[2][1]

Nói ngắn gọn, **translation-based embedding là lớp biểu diễn nền** giúp DeepPath nối hai thế giới: phía dưới là KG rời rạc, phía trên là policy network cần đầu vào số thực liên tục để học và generalize.[2][1]
