# Nhập môn xác suất

Joseph K. Blitzstein và Jessica Hwang

> **Trạng thái:** Bản dịch đang thực hiện. Các trang PDF 15–17, 19–107, 109–153, 155–211 và 213–246 đã được dịch trực tiếp dưới đây; trang 108, 154 và 212 không có văn bản. PDF có 589 trang; những trang khác chưa được dịch. Số trang trong ngoặc là số trang của tệp PDF, khác với số trang in trong sách.

## Lời nói đầu (trang PDF 15–17)

Cuốn sách này giới thiệu xác suất theo cách hiện đại và xây dựng nền tảng để hiểu thống kê, tính ngẫu nhiên và sự bất định. Sách khảo sát nhiều ứng dụng và ví dụ, từ tung đồng xu và nghiên cứu những sự trùng hợp đến Google PageRank và phương pháp Monte Carlo dùng chuỗi Markov. Vì xác suất thường được xem là một môn học trái với trực giác, chúng tôi đưa vào nhiều lời giải thích trực quan, hình vẽ và bài tập. Cuối mỗi chương có một mục hướng dẫn khám phá các ý tưởng của chương bằng R, một môi trường phần mềm miễn phí dành cho tính toán thống kê và mô phỏng.

Video bài giảng của học phần Stat 110 tại Harvard, học phần làm nền tảng cho cuốn sách này (và được Joe giảng dạy hằng năm từ năm 2006), được cung cấp miễn phí tại stat110.net. Trang web này còn có các tài liệu bổ trợ, chẳng hạn mã R và lời giải cho những bài tập được đánh dấu bằng ký hiệu lời giải.

Người đọc cần biết giải tích trước khi học cuốn sách này; không cần học thống kê trước. Thử thách toán học chính không nằm ở việc thực hiện các phép biến đổi giải tích phức tạp, mà ở việc chuyển đổi qua lại giữa khái niệm trừu tượng và ví dụ cụ thể. Dưới đây là một số chủ đề và đặc điểm nổi bật.

1. **Các câu chuyện.** Xuyên suốt cuốn sách, chúng tôi trình bày định nghĩa, định lý và chứng minh thông qua những câu chuyện: cách diễn giải gắn với thực tế nhưng vẫn giữ được tính chính xác và khái quát của toán học. Chúng tôi tìm hiểu các phân phối xác suất thông qua những câu chuyện về cơ chế tạo ra chúng, cũng chính là lý do chúng được sử dụng rộng rãi trong mô hình thống kê. Khi có thể, chúng tôi tránh những phép suy diễn dài dòng và cố gắng giải thích ý nghĩa cũng như trực giác đằng sau các kết quả quan trọng. Theo kinh nghiệm của chúng tôi, cách tiếp cận này giúp người học ghi nhớ lâu hơn vì mang lại sự thấu hiểu, thay vì đòi hỏi học thuộc lòng.

2. **Hình ảnh.** Vì một bức hình có thể kể câu chuyện bằng cả nghìn từ, chúng tôi bổ sung hình minh họa cho các định nghĩa, giúp gắn những khái niệm quan trọng với sơ đồ dễ nhớ. Trong nhiều lĩnh vực, sự khác biệt giữa người mới học và chuyên gia được mô tả như sau: người mới học phải cố ghi nhớ rất nhiều sự kiện và công thức có vẻ rời rạc; chuyên gia lại nhìn thấy một cấu trúc thống nhất, trong đó một vài nguyên lý và ý tưởng liên kết các sự kiện ấy một cách mạch lạc. Để giúp sinh viên thấy được cấu trúc của xác suất, chúng tôi nhấn mạnh các mối liên hệ giữa những ý tưởng, cả bằng lời lẫn hình ảnh. Cuối phần lớn các chương, chúng tôi trình bày lại các sơ đồ khái niệm và phân phối, mỗi lần mở rộng thêm.

3. **Dạy song song khái niệm và chiến lược.** Chúng tôi mong rằng khi đọc cuốn sách này, sinh viên không chỉ học các khái niệm xác suất mà còn học được những chiến lược giải quyết vấn đề có thể áp dụng rộng rãi ngoài lĩnh vực xác suất. Trong các ví dụ có lời giải, chúng tôi giải thích từng bước và đồng thời nói rõ vì sao lại chọn cách tiếp cận đó. Nhiều bài toán được trình bày với nhiều cách giải.

   Chúng tôi nêu rõ và đặt tên cho những chiến lược quan trọng như tính đối xứng và nhận dạng quy luật. Chúng tôi cũng chủ động làm sáng tỏ những hiểu lầm thường gặp, được đánh dấu bằng biểu tượng cảnh báo nguy hại sinh học.

4. **Bài tập thực hành.** Cuốn sách có khoảng 600 bài tập với độ khó khác nhau. Các bài tập nhằm củng cố hiểu biết và nâng cao kỹ năng giải quyết vấn đề, thay vì yêu cầu tính toán lặp đi lặp lại. Một số bài thuộc dạng luyện tập theo chiến lược, được nhóm theo chủ đề để người học rèn luyện một nội dung cụ thể; những bài khác là bài tập tổng hợp, đòi hỏi kết hợp nhiều chủ đề đã học. Khoảng 250 bài có lời giải chi tiết trên mạng để phục vụ việc luyện tập và tự học.

5. **Mô phỏng, Monte Carlo và R.** Nhiều bài toán xác suất quá khó để giải chính xác; dù sao, việc kiểm tra lại đáp án cũng rất quan trọng. Chúng tôi giới thiệu các kỹ thuật tìm hiểu xác suất bằng mô phỏng và cho thấy chỉ vài dòng mã R thường đã đủ để mô phỏng một bài toán tưởng như phức tạp.

6. **Chú trọng ứng dụng thực tế và tư duy thống kê.** Các ví dụ và bài tập trong sách đều có động cơ thực tế rõ ràng, đặc biệt hướng tới việc xây dựng nền tảng vững chắc để tiếp tục học suy luận và mô hình hóa thống kê. Chúng tôi giới thiệu trước những ý tưởng thống kê quan trọng như lấy mẫu, mô phỏng, suy luận Bayes và Monte Carlo dùng chuỗi Markov; các lĩnh vực ứng dụng khác gồm di truyền học, y học, khoa học máy tính và lý thuyết thông tin. Việc lựa chọn ví dụ và bài tập nhằm làm nổi bật sức mạnh, phạm vi ứng dụng và vẻ đẹp của tư duy xác suất.

### Lời cảm ơn

Chúng tôi cảm ơn các đồng nghiệp, các trợ giảng của Stat 110 và hàng nghìn sinh viên Stat 110 vì những nhận xét và ý tưởng liên quan đến học phần và cuốn sách. Đặc biệt, chúng tôi cảm ơn Alvin Siu, Angela Fan, Anji Tang, Carolyn Stein, David Jones, David Rosengarten, David Watson, Johannes Ruf, Kari Lock, Keli Liu, Kevin Bartz, Lazhi Wang, Martin Lysy, Michele Zemplenyi, Peng Ding, Rob Phillips, Sam Fisher, Sebastian Chiu, Sofia Hou, Theresa Gebert, Valeria Espinosa, Viktoriia Liublinska, Viviana Garcia, William Chen và Xander Marcus vì những góp ý của họ.

Chúng tôi đặc biệt cảm ơn Bo Jiang, Raj Bhuptani, Shira Mitchell và các phản biện ẩn danh vì đã nhận xét kỹ lưỡng các bản thảo của cuốn sách; cảm ơn Andrew Gelman, Carl Morris, Persi Diaconis, Stephen Blyth, Susan Holmes và Xiao-Li Meng vì vô số cuộc trao đổi sâu sắc về xác suất.

John Kimmel ở Chapman and Hall/CRC Press đã mang đến chuyên môn biên tập tuyệt vời trong suốt quá trình viết sách. Chúng tôi rất trân trọng sự hỗ trợ của ông.

Cuối cùng, chúng tôi xin bày tỏ lòng biết ơn sâu sắc nhất đến gia đình vì tình yêu thương và sự động viên.

Joe Blitzstein và Jessica Hwang  
Cambridge, Massachusetts và Stanford, California  
Tháng 5 năm 2014

## Chương 1. Xác suất và phép đếm (trang PDF 19)

May mắn. Trùng hợp. Ngẫu nhiên. Bất định. Rủi ro. Hoài nghi. Vận may. Cơ hội.

Có lẽ bạn đã nghe những từ này vô số lần, nhưng rất có thể chúng được dùng một cách mơ hồ, tùy tiện. Đáng tiếc là dù xác suất hiện diện khắp nơi trong khoa học và đời sống, nó vẫn có thể rất trái với trực giác. Nếu dựa vào những trực giác chưa chắc đúng, chúng ta rất dễ đưa ra dự đoán sai hoặc quyết định với sự tự tin thái quá. Mục tiêu của cuốn sách này là giới thiệu xác suất như một khuôn khổ logic để định lượng sự bất định và tính ngẫu nhiên một cách có nguyên tắc. Chúng tôi cũng muốn rèn luyện trực giác, cả khi phỏng đoán ban đầu phù hợp với suy luận logic lẫn khi chúng ta không may mắn như vậy.

### 1.1. Vì sao nên học xác suất?

Toán học là logic của sự chắc chắn; xác suất là logic của sự bất định. Xác suất vô cùng hữu ích trong nhiều lĩnh vực vì cung cấp công cụ để hiểu và giải thích sự biến thiên, tách tín hiệu khỏi nhiễu và mô hình hóa các hiện tượng phức tạp. Dưới đây chỉ là một vài ví dụ trong danh sách ứng dụng ngày càng dài:

1. **Thống kê:** Xác suất là nền tảng và ngôn ngữ của thống kê, cho phép chúng ta dùng nhiều phương pháp mạnh để tìm hiểu thế giới từ dữ liệu.
2. **Vật lý:** Einstein có câu nói nổi tiếng: “Thượng đế không chơi xúc xắc với vũ trụ”, nhưng hiểu biết hiện nay về vật lý lượng tử sử dụng xác suất ngay ở cấp độ cơ bản nhất của tự nhiên. Cơ học thống kê là một nhánh quan trọng khác của vật lý được xây dựng trên xác suất.
3. **Sinh học:** Di truyền học gắn bó mật thiết với xác suất, cả trong quá trình di truyền gen lẫn khi mô hình hóa các đột biến ngẫu nhiên.
4. **Khoa học máy tính:** Thuật toán ngẫu nhiên đưa ra những lựa chọn ngẫu nhiên trong khi chạy; trong nhiều ứng dụng quan trọng, chúng đơn giản và hiệu quả hơn mọi phương án tất định hiện được biết đến. Xác suất cũng giữ vai trò thiết yếu trong việc nghiên cứu hiệu năng thuật toán, học máy và trí tuệ nhân tạo.

### Chương 1, tiếp theo (trang PDF 20–23)

5. **Khí tượng học:** Dự báo thời tiết được (hoặc nên được) tính toán và trình bày bằng xác suất.
6. **Cờ bạc:** Nhiều nghiên cứu đầu tiên về xác suất nhằm trả lời các câu hỏi liên quan đến cờ bạc và trò chơi may rủi.
7. **Tài chính:** Dù có thể hơi trùng với ví dụ vừa nêu, cần chỉ ra rằng xác suất giữ vai trò trung tâm trong tài chính định lượng. Việc mô hình hóa giá cổ phiếu theo thời gian và xác định mức giá “hợp lý” của các công cụ tài chính phụ thuộc rất nhiều vào xác suất.
8. **Khoa học chính trị:** Trong những năm gần đây, khoa học chính trị ngày càng sử dụng nhiều phương pháp định lượng và thống kê. Chẳng hạn, Nate Silver đã dự đoán thành công kết quả bầu cử, bao gồm các cuộc bầu cử tổng thống Hoa Kỳ năm 2008 và 2012, bằng cách dùng mô hình xác suất để diễn giải kết quả thăm dò và chạy mô phỏng (xem Silver [25]).
9. **Y học:** Sự phát triển của các thử nghiệm lâm sàng ngẫu nhiên, trong đó bệnh nhân được phân ngẫu nhiên vào nhóm điều trị hoặc dùng giả dược, đã làm thay đổi nghiên cứu y học trong những năm gần đây. Như nhà thống kê sinh học David Harrington nhận xét: “Có người phỏng đoán rằng đó có thể là bước tiến quan trọng nhất của y học khoa học trong thế kỷ XX... Một điều trớ trêu thú vị của khoa học hiện đại là thử nghiệm ngẫu nhiên ‘điều chỉnh’ cho sự khác biệt giữa các đối tượng, cả quan sát được lẫn không quan sát được, trong một thí nghiệm có kiểm soát bằng cách đưa biến thiên ngẫu nhiên vào thiết kế nghiên cứu.” [17]
10. **Cuộc sống:** Cuộc sống chứa đầy điều bất định, và xác suất là logic của sự bất định. Dù không thực tế khi tính xác suất một cách chính thức cho mọi quyết định trong đời, suy nghĩ kỹ về xác suất vẫn có thể giúp chúng ta tránh một số ngộ nhận thường gặp, hiểu rõ hơn những sự trùng hợp và dự đoán tốt hơn.

Xác suất cung cấp các cách giải quyết vấn đề có nguyên tắc, nhưng cũng có thể dẫn đến những cạm bẫy và nghịch lý. Chẳng hạn, trong chương này chúng ta sẽ thấy ngay cả Gottfried Wilhelm von Leibniz và Sir Isaac Newton, hai người độc lập phát hiện ra giải tích vào thế kỷ XVII, cũng mắc những lỗi xác suất cơ bản. Trong suốt cuốn sách, chúng tôi sẽ dùng những chiến lược sau để tránh các cạm bẫy có thể gặp:

1. **Mô phỏng:** Một nét đẹp của xác suất là nhiều bài toán có thể được nghiên cứu bằng mô phỏng. Thay vì tranh luận mãi với người bất đồng quan điểm, bạn có thể chạy mô phỏng để xem bằng chứng thực nghiệm ủng hộ ai. Cuối mỗi chương của sách có một mục đưa ra các ví dụ tính toán và mô phỏng bằng R, một môi trường tính toán thống kê miễn phí.
2. **Cảnh báo lỗi thường gặp:** Việc nghiên cứu các sai lầm phổ biến giúp ta hiểu vững hơn thế nào là suy luận hợp lệ trong xác suất. Trong sách, những lỗi thường gặp được gọi là *biohazards* (mối nguy hại sinh học) và được đánh dấu bằng một biểu tượng cảnh báo, bởi mắc các lỗi ấy có thể “nguy hại cho sức khỏe”!
3. **Kiểm tra tính hợp lý:** Sau khi giải một bài theo một cách, chúng ta thường thử giải theo cách khác hoặc xem đáp án có hợp lý trong những trường hợp đơn giản và cực hạn hay không.

### 1.2. Không gian mẫu và Thế giới Sỏi

Khuôn khổ toán học của xác suất được xây dựng trên lý thuyết tập hợp. Hãy tưởng tượng ta thực hiện một phép thử và nhận được một trong những kết quả có thể xảy ra. Trước khi thực hiện phép thử, ta chưa biết kết quả nào sẽ xuất hiện; sau khi thực hiện, một kết quả cụ thể “kết tinh” thành hiện thực.

**Định nghĩa 1.2.1 (Không gian mẫu và biến cố).** *Không gian mẫu* $S$ của một phép thử là tập hợp tất cả các kết quả có thể xảy ra. *Biến cố* $A$ là một tập con của không gian mẫu $S$. Ta nói $A$ xảy ra nếu kết quả thực tế thuộc $A$.

**Hình 1.1.** Không gian mẫu được hình dung như một *Thế giới Sỏi*, với hai biến cố $A$ và $B$ được làm nổi bật.

Không gian mẫu của một phép thử có thể hữu hạn, vô hạn đếm được hoặc vô hạn không đếm được (xem mục A.1.5 của phụ lục toán học để biết cách phân biệt các loại tập hợp này). Khi không gian mẫu hữu hạn, ta có thể hình dung nó như Thế giới Sỏi ở Hình 1.1. Mỗi viên sỏi đại diện cho một kết quả; một biến cố là một tập hợp các viên sỏi.

Thực hiện phép thử tương đương với việc chọn ngẫu nhiên một viên sỏi. Nếu mọi viên sỏi có cùng khối lượng, mỗi viên đều có khả năng được chọn như nhau. Trường hợp đặc biệt này là chủ đề của hai mục tiếp theo. Ở mục 1.6, chúng ta sẽ đưa ra định nghĩa tổng quát về xác suất, cho phép các viên sỏi có khối lượng khác nhau.

Lý thuyết tập hợp rất hữu ích trong xác suất vì nó cung cấp một ngôn ngữ phong phú để diễn đạt và xử lý các biến cố; mục A.1 của phụ lục toán học ôn lại lý thuyết tập hợp. Các phép toán tập hợp, đặc biệt là hợp, giao và phần bù, giúp dễ dàng tạo biến cố mới từ những biến cố đã định nghĩa. Chúng cũng cho phép diễn đạt cùng một biến cố theo nhiều cách; thường có cách diễn đạt dễ xử lý hơn hẳn những cách khác.

Chẳng hạn, cho $S$ là không gian mẫu của một phép thử và $A,B\subseteq S$ là hai biến cố. Khi đó, hợp $A\cup B$ xảy ra khi và chỉ khi ít nhất một trong hai biến cố $A$ và $B$ xảy ra; giao $A\cap B$ xảy ra khi và chỉ khi cả $A$ lẫn $B$ xảy ra; phần bù $A^c$ xảy ra khi và chỉ khi $A$ không xảy ra. Ta cũng có các định luật De Morgan:

$$
(A\cup B)^c=A^c\cap B^c,\qquad (A\cap B)^c=A^c\cup B^c.
$$

Thật vậy, nói rằng “không phải ít nhất một trong $A,B$ xảy ra” tương đương với “cả $A$ lẫn $B$ đều không xảy ra”; còn nói rằng “không phải cả hai đều xảy ra” tương đương với “ít nhất một trong hai không xảy ra”. Những kết quả tương tự cũng đúng với hợp và giao của nhiều hơn hai biến cố.

Trong ví dụ ở Hình 1.1, $A$ chứa 5 viên sỏi, $B$ chứa 4 viên, $A\cup B$ chứa 8 viên thuộc $A$ hoặc $B$ (kể cả viên thuộc cả hai), $A\cap B$ chỉ gồm viên sỏi thuộc cả hai, còn $A^c$ chứa 4 viên không thuộc $A$.

Khái niệm không gian mẫu rất tổng quát và trừu tượng, nên việc ghi nhớ một vài ví dụ cụ thể rất quan trọng.

**Ví dụ 1.2.2 (Tung đồng xu).** Tung một đồng xu 10 lần. Ký hiệu mặt ngửa là H và mặt sấp là T. Một kết quả có thể là `HHHTHHTTHT`; không gian mẫu là tập hợp tất cả các chuỗi độ dài 10 gồm H và T. Ta có thể (và sẽ) mã hóa H bằng 1, T bằng 0. Khi ấy, một kết quả là dãy $(s_1,\ldots,s_{10})$ với $s_j\in\{0,1\}$; không gian mẫu là tập hợp tất cả các dãy như vậy. Bây giờ hãy xét một vài biến cố:

1. Gọi $A_1$ là biến cố lần tung đầu tiên ra mặt ngửa. Dưới dạng tập hợp,

   $$A_1=\{(1,s_2,\ldots,s_{10}):s_j\in\{0,1\}\text{ với }2\le j\le10\}.$$

   Đây là tập con của không gian mẫu, nên thực sự là một biến cố. Nói $A_1$ xảy ra tương đương với nói lần tung đầu tiên ra mặt ngửa. Tương tự, với $j=2,3,\ldots,10$, gọi $A_j$ là biến cố lần tung thứ $j$ ra mặt ngửa.
2. Gọi $B$ là biến cố có ít nhất một lần ra mặt ngửa. Dưới dạng tập hợp, $B=\bigcup_{j=1}^{10}A_j$.
3. Gọi $C$ là biến cố mọi lần tung đều ra mặt ngửa. Dưới dạng tập hợp, $C=\bigcap_{j=1}^{10}A_j$.
4. Gọi $D$ là biến cố có ít nhất hai lần liên tiếp ra mặt ngửa. Dưới dạng tập hợp, $D=\bigcup_{j=1}^{9}(A_j\cap A_{j+1})$.

**Ví dụ 1.2.3 (Rút một lá bài).** Rút một lá từ bộ bài chuẩn gồm 52 lá. Không gian mẫu $S$ là tập hợp 52 lá bài (tức có 52 “viên sỏi”, mỗi viên ứng với một lá). Xét bốn biến cố:

- $A$: lá được rút là át.
- $B$: lá được rút thuộc chất đen.
- $D$: lá được rút thuộc chất rô.
- $H$: lá được rút thuộc chất cơ.

Dưới dạng tập hợp, $H$ gồm 13 lá: $\{\text{át cơ},\text{hai cơ},\ldots,\text{già cơ}\}$. Ta có thể tạo nhiều biến cố khác từ $A,B,D,H$. Chẳng hạn, $A\cap H$ là biến cố rút được át cơ; $A\cap B$ là biến cố rút được một trong hai lá $\{\text{át bích},\text{át tép}\}$; còn $A\cup D\cup H$ là biến cố rút được lá đỏ hoặc lá át. Hơn nữa, $(D\cup H)^c=D^c\cap H^c=B$, nên có thể biểu diễn $B$ theo $D$ và $H$. Ngược lại, không thể biểu diễn biến cố rút được lá bích bằng $A,B,D,H$, vì các biến cố này không đủ chi tiết để phân biệt bích với tép.

Có rất nhiều biến cố khác có thể định nghĩa trên không gian mẫu này. Thật vậy, các phương pháp đếm được giới thiệu ở phần sau của chương cho thấy bài toán này có $2^{52}\approx4{,}5\times10^{15}$ biến cố, dù chỉ có 52 “viên sỏi”. Nếu lá rút được lại là lá joker thì sao? Điều đó cho thấy ta đã chọn sai không gian mẫu; ta đang giả định kết quả của phép thử chắc chắn là một phần tử của $S$.

Như các ví dụ trên cho thấy, ta có thể mô tả biến cố bằng ngôn ngữ thông thường hoặc ký hiệu tập hợp. Đôi khi lời mô tả dễ hiểu hơn, còn ký hiệu tập hợp dễ biến đổi hơn. Cho $S$ là một không gian mẫu và $s_{\text{thực tế}}$ là kết quả thực tế của phép thử (viên sỏi cuối cùng được chọn khi thực hiện phép thử). Dưới đây là một bảng thuật ngữ ngắn để chuyển đổi giữa ngôn ngữ thông thường và ký hiệu tập hợp. Chẳng hạn, phát biểu “$A$ kéo theo $B$” có nghĩa là bất cứ khi nào $A$ xảy ra thì $B$ cũng xảy ra; dưới dạng tập hợp, điều đó nghĩa là $A\subseteq B$.

| Ngôn ngữ thông thường | Ký hiệu tập hợp |
|---|---|
| Không gian mẫu | $S$ |
| $s$ là một kết quả có thể xảy ra | $s\in S$ |
| $A$ là một biến cố | $A\subseteq S$ |
| $A$ đã xảy ra | $s_{\text{thực tế}}\in A$ |
| Chắc chắn có một kết quả xảy ra | $s_{\text{thực tế}}\in S$ |
| $A$ hoặc $B$ (có thể cả hai) | $A\cup B$ |
| $A$ và $B$ | $A\cap B$ |
| Không phải $A$ | $A^c$ |
| $A$ hoặc $B$, nhưng không đồng thời | $(A\cap B^c)\cup(A^c\cap B)$ |
| Ít nhất một trong $A_1,\ldots,A_n$ | $A_1\cup\cdots\cup A_n$ |
| Tất cả $A_1,\ldots,A_n$ | $A_1\cap\cdots\cap A_n$ |
| $A$ kéo theo $B$ | $A\subseteq B$ |
| $A$ và $B$ loại trừ nhau | $A\cap B=\varnothing$ |
| $A_1,\ldots,A_n$ tạo thành một phân hoạch của $S$ | $A_1\cup\cdots\cup A_n=S$ và $A_i\cap A_j=\varnothing$ khi $i\ne j$ |

### 1.3. Định nghĩa xác suất sơ khai

Trong lịch sử, định nghĩa đầu tiên về xác suất của một biến cố là đếm số cách để biến cố đó xảy ra rồi chia cho tổng số kết quả có thể có của phép thử. Chúng tôi gọi đây là định nghĩa *sơ khai* vì nó có phạm vi áp dụng hẹp và dựa trên những giả định mạnh. Tuy vậy, điều quan trọng là phải hiểu nó; nếu dùng đúng, nó rất hữu ích.

**Định nghĩa 1.3.1 (Định nghĩa xác suất sơ khai).** Cho $A$ là một biến cố của phép thử có không gian mẫu hữu hạn $S$. Xác suất sơ khai của $A$ là

$$P_{\text{sơ khai}}(A)=\frac{|A|}{|S|}=\frac{\text{số kết quả thuận lợi cho }A}{\text{tổng số kết quả trong }S}.$$

Ký hiệu $|A|$ là số phần tử của $A$ (xem mục A.1.5 của phụ lục toán học).

Trong Thế giới Sỏi, định nghĩa sơ khai chỉ nói rằng xác suất của $A$ bằng tỉ lệ các viên sỏi thuộc $A$. Chẳng hạn, ở Hình 1.1:

$$P_{\text{sơ khai}}(A)=\frac59,\quad P_{\text{sơ khai}}(B)=\frac49,\quad P_{\text{sơ khai}}(A\cup B)=\frac89,\quad P_{\text{sơ khai}}(A\cap B)=\frac19.$$

Với phần bù của các biến cố trên:

$$P_{\text{sơ khai}}(A^c)=\frac49,\quad P_{\text{sơ khai}}(B^c)=\frac59,\quad P_{\text{sơ khai}}((A\cup B)^c)=\frac19,\quad P_{\text{sơ khai}}((A\cap B)^c)=\frac89.$$

Nói chung,

$$P_{\text{sơ khai}}(A^c)=\frac{|A^c|}{|S|}=\frac{|S|-|A|}{|S|}=1-\frac{|A|}{|S|}=1-P_{\text{sơ khai}}(A).$$

Trong mục 1.6, ta sẽ thấy hệ thức về phần bù này luôn đúng với xác suất, ngay cả khi vượt ra ngoài định nghĩa sơ khai. Khi tìm xác suất của một biến cố, nên bắt đầu bằng việc cân nhắc xem tính xác suất của chính biến cố ấy hay của biến cố đối sẽ dễ hơn. Các định luật De Morgan đặc biệt hữu ích trong trường hợp này, vì xử lý một phép giao có thể dễ hơn xử lý một phép hợp, hoặc ngược lại.

Định nghĩa sơ khai rất hạn chế: nó đòi hỏi $S$ hữu hạn và mọi viên sỏi có cùng khối lượng. Nó thường bị áp dụng sai khi người ta tự ý giả định các kết quả có khả năng xảy ra như nhau, rồi lập luận kiểu “hoặc nó xảy ra, hoặc không; chúng ta không biết thế nào, vậy xác suất là 50–50”. Ngoài việc đôi khi cho xác suất vô lý, kiểu lập luận này còn tự mâu thuẫn. Chẳng hạn, nó sẽ cho rằng xác suất có sự sống trên Sao Hỏa là $1/2$ (“hoặc có hoặc không”), nhưng cũng cho rằng xác suất có sự sống thông minh trên Sao Hỏa là $1/2$. Trực giác cho thấy — và các tính chất xác suất ở mục 1.6 xác nhận — trường hợp sau phải có xác suất nhỏ hơn hẳn trường hợp trước. Tuy nhiên, có một số loại bài toán quan trọng mà định nghĩa sơ khai áp dụng được:

- **Khi bài toán có tính đối xứng khiến các kết quả có khả năng xảy ra như nhau.** Thông thường, ta giả định đồng xu có 50% khả năng ra mặt ngửa khi tung, nhờ tính đối xứng vật lý của nó.¹ Với một bộ bài chuẩn được xáo kỹ, có thể giả định hợp lý rằng mọi thứ tự của các lá đều có khả năng như nhau. Không có lá bài nào “quá háo hức” và đặc biệt thích nằm gần đầu bộ bài; mỗi vị trí đều có khả năng chứa bất kỳ lá nào trong 52 lá như nhau.
- **Khi các kết quả được thiết kế để có khả năng xảy ra như nhau.** Chẳng hạn, khi khảo sát $n$ người trong một quần thể $N$ người, mục tiêu thường là có một *mẫu ngẫu nhiên đơn*: chọn ngẫu nhiên $n$ người sao cho mọi tập con gồm $n$ người đều có khả năng được chọn như nhau. Nếu làm được, ta có thể áp dụng định nghĩa sơ khai. Nhưng trong thực tế, việc này có thể khó vì nhiều trở ngại, chẳng hạn không có danh sách thông tin liên hệ đầy đủ và chính xác của mọi người trong quần thể.
- **Khi định nghĩa sơ khai làm mô hình không hữu ích.** Ta tạm giả định định nghĩa sơ khai đúng để xem nó dự đoán điều gì, rồi so sánh dữ liệu quan sát với các giá trị dự đoán, từ đó đánh giá giả thuyết “các kết quả có khả năng như nhau” có đứng vững không.

¹ Xem Diaconis, Holmes và Montgomery [8] về lập luận vật lý cho thấy một đồng xu được tung có xác suất rơi xuống với mặt ban đầu hướng lên khoảng 0,51 (gần nhưng hơi lớn hơn $1/2$); xem Gelman và Nolan [12] để biết vì sao xác suất ra mặt ngửa vẫn gần $1/2$ ngay cả với đồng xu được chế tạo có hai mặt nặng nhẹ khác nhau (nếu tung đồng xu theo cách thông thường; cho đồng xu quay là chuyện khác).

### 1.4. Cách đếm

Để tính xác suất sơ khai của biến cố $A$, ta cần đếm số viên sỏi trong $A$ và trong không gian mẫu $S$. Những tập hợp cần đếm thường rất lớn. Mục này giới thiệu một số phương pháp đếm cơ bản; có thể tìm thêm các phương pháp khác trong sách về *tổ hợp*, ngành toán học nghiên cứu phép đếm.

#### 1.4.1. Quy tắc nhân

Trong một số bài toán, ta có thể đếm trực tiếp số khả năng bằng một nguyên lý đơn giản nhưng linh hoạt, gọi là *quy tắc nhân*. Ta sẽ thấy quy tắc nhân dẫn đến một cách tự nhiên các quy tắc đếm cho việc lấy mẫu có hoàn lại và lấy mẫu không hoàn lại, hai tình huống thường gặp trong xác suất và thống kê.

**Định lý 1.4.1 (Quy tắc nhân).** Xét một phép thử ghép gồm hai phép thử thành phần, phép thử $A$ và phép thử $B$. Giả sử $A$ có $a$ kết quả có thể có, và ứng với mỗi kết quả ấy, $B$ có $b$ kết quả có thể có. Khi đó, phép thử ghép có $ab$ kết quả có thể có.

Để hiểu vì sao quy tắc nhân đúng, hãy hình dung sơ đồ cây như ở Hình 1.2. Cho cây tách thành $a$ nhánh ứng với các khả năng của phép thử $A$; từ mỗi nhánh ấy lại tách thành $b$ nhánh ứng với phép thử $B$. Tổng cộng có $b+b+\cdots+b=ab$ khả năng ($a$ số hạng).

**Lưu ý 1.4.2.** Thường dễ hình dung các phép thử theo thứ tự thời gian, nhưng quy tắc nhân không đòi hỏi phải thực hiện phép thử $A$ trước phép thử $B$.

**Ví dụ 1.4.3 (Kem ốc quế).** Giả sử bạn mua một cây kem ốc quế. Bạn có thể chọn vỏ ốc quế loại bánh xốp hoặc bánh quế và chọn vị sô cô la, vani hoặc dâu. Có thể biểu diễn quá trình chọn này bằng sơ đồ cây, như ở Hình 1.3.

Theo quy tắc nhân, có $2\cdot3=6$ khả năng. Đây là ví dụ rất đơn giản, nhưng xem xét kỹ nó sẽ giúp xây dựng nền tảng để hình dung những ví dụ phức tạp hơn. Chẳng bao lâu nữa, ta sẽ gặp những ví dụ mà nếu vẽ sơ đồ cây ở kích thước đọc được thì cần nhiều không gian hơn cả vũ trụ đã biết, dù về mặt khái niệm ta vẫn có thể suy nghĩ giống như ở ví dụ kem ốc quế. Cần lưu ý:

1. Bạn chọn loại vỏ trước (“Cho tôi vỏ bánh quế với kem sô cô la”) hay chọn vị trước (“Cho tôi kem sô cô la trong vỏ bánh quế”) đều không quan trọng. Cả hai cách đều cho $2\cdot3=3\cdot2=6$ khả năng.
2. Hai loại vỏ có cùng danh sách vị kem hay không cũng không quan trọng. Điều quan trọng là với *mỗi* loại vỏ đều có đúng 3 lựa chọn vị. Nếu vì lý do kỳ lạ nào đó không được chọn kem sô cô la với vỏ bánh quế, và không có vị thay thế nào khác ngoài vani và dâu, thì chỉ có $3+2=5$ khả năng và không thể áp dụng quy tắc nhân như trên. Trong những ví dụ lớn hơn, các ràng buộc như vậy có thể khiến việc đếm số khả năng khó hơn rất nhiều.

Bây giờ giả sử trong một ngày bạn mua hai cây kem, một cây vào buổi chiều và cây kia vào buổi tối. Chẳng hạn, ký hiệu `(xốp-S, quế-V)` có nghĩa là buổi chiều mua kem sô cô la trong vỏ bánh xốp, rồi buổi tối mua kem vani trong vỏ bánh quế.

**Hình 1.3.** Sơ đồ cây cho việc chọn một cây kem ốc quế. Dù chọn loại vỏ hay vị kem trước, vẫn có $2\cdot3=3\cdot2=6$ khả năng.

Theo quy tắc nhân, phép thử ghép “ngon miệng” này có $6^2=36$ khả năng.

Nhưng nếu bạn chỉ quan tâm trong ngày đã ăn những *loại* kem nào, không quan tâm thứ tự ăn, thì bạn sẽ không muốn phân biệt `(xốp-S, quế-V)` và `(quế-V, xốp-S)`. Khi ấy có phải còn $36/2=18$ khả năng không? Không, vì những trường hợp như `(xốp-S, xốp-S)` vốn mỗi trường hợp chỉ được liệt kê một lần. Có $6\cdot5=30$ cặp có thứ tự $(x,y)$ với $x\ne y$. Khi coi $(x,y)$ và $(y,x)$ là như nhau, ta được 15 khả năng; cộng thêm 6 khả năng dạng $(x,x)$, tổng cộng là 21. Lưu ý rằng nếu ban đầu 36 cặp có thứ tự $(x,y)$ có khả năng xảy ra như nhau, thì 21 khả năng sau khi bỏ qua thứ tự *không* có khả năng xảy ra như nhau.

**Ví dụ 1.4.4 (Các tập con).** Một tập hợp có $n$ phần tử sẽ có $2^n$ tập con, tính cả tập rỗng $\varnothing$ và chính tập đó. Điều này suy ra từ quy tắc nhân: với mỗi phần tử, ta chọn đưa nó vào tập con hoặc không. Chẳng hạn, tập $\{1,2,3\}$ có 8 tập con: $\varnothing$, $\{1\}$, $\{2\}$, $\{3\}$, $\{1,2\}$, $\{1,3\}$, $\{2,3\}$ và $\{1,2,3\}$. Kết quả này giải thích vì sao trong Ví dụ 1.2.3 có $2^{52}\approx4{,}5\times10^{15}$ biến cố có thể định nghĩa.

Ta có thể dùng quy tắc nhân để tìm công thức cho việc lấy mẫu có hoàn lại và không hoàn lại. Nhiều phép thử trong xác suất và thống kê có thể được hiểu theo một trong hai tình huống này, nên thật thuận tiện khi cả hai công thức đều suy ra trực tiếp từ cùng một nguyên lý đếm cơ bản.

**Định lý 1.4.5 (Lấy mẫu có hoàn lại).** Xét $n$ đối tượng và chọn $k$ lần từ đó, mỗi lần chọn xong đều hoàn lại (nghĩa là đối tượng đã chọn vẫn có thể được chọn tiếp). Khi đó có $n^k$ kết quả có thể có.

Chẳng hạn, hãy hình dung một chiếc lọ chứa $n$ quả bóng được đánh số từ 1 đến $n$. Ta rút từng quả rồi đặt lại vào lọ sau mỗi lần rút. Mỗi lần rút là một phép thử thành phần có $n$ kết quả có thể có; có tất cả $k$ lần rút. Do đó, theo quy tắc nhân, có $n^k$ cách thu được mẫu gồm $k$ quả bóng.

**Định lý 1.4.6 (Lấy mẫu không hoàn lại).** Xét $n$ đối tượng và chọn $k$ lần từ đó, mỗi lần chọn xong không hoàn lại (nghĩa là đối tượng đã chọn không thể được chọn tiếp). Khi đó có $n(n-1)\cdots(n-k+1)$ kết quả có thể có nếu $k\le n$ (và không có khả năng nào nếu $k>n$).

Kết quả này cũng suy ra trực tiếp từ quy tắc nhân: mỗi lần rút bóng vẫn là một phép thử thành phần, nhưng số kết quả có thể có giảm đi một sau mỗi lần rút. Lưu ý rằng khi lấy $k$ trong số $n$ đối tượng mà không hoàn lại thì phải có $k\le n$; còn khi có hoàn lại, nguồn đối tượng không bị cạn.

**Ví dụ 1.4.7 (Hoán vị và giai thừa).** Một hoán vị của $1,2,\ldots,n$ là một cách sắp xếp chúng theo thứ tự nào đó. Chẳng hạn, $3,5,1,2,4$ là một hoán vị của $1,2,3,4,5$. Theo Định lý 1.4.6 với $k=n$, có $n!$ hoán vị của $1,2,\ldots,n$. Ví dụ, có $n!$ cách để $n$ người xếp hàng mua kem. (Nhắc lại: $n!=n(n-1)(n-2)\cdots1$ với mọi số nguyên dương $n$, và $0!=1$.)

Định lý 1.4.5 và 1.4.6 là các định lý đếm, nhưng khi định nghĩa sơ khai áp dụng được, ta có thể dùng chúng để tính xác suất. Điều này dẫn đến ví dụ tiếp theo: một bài toán xác suất nổi tiếng gọi là *bài toán ngày sinh*. Lời giải sử dụng cả lấy mẫu có hoàn lại lẫn không hoàn lại.

**Ví dụ 1.4.8 (Bài toán ngày sinh).** Có $k$ người trong một căn phòng. Giả sử ngày sinh của mỗi người có khả năng rơi vào bất kỳ ngày nào trong 365 ngày của năm như nhau (bỏ qua ngày 29 tháng 2), và ngày sinh của những người này độc lập với nhau (giả sử trong phòng không có cặp sinh đôi). Xác suất có ít nhất hai người cùng ngày sinh là bao nhiêu?

**Lời giải.** Có $365^k$ cách gán ngày sinh cho những người trong phòng: ta có thể hình dung việc chọn $k$ lần từ 365 ngày trong năm, có hoàn lại. Theo giả định, mọi khả năng này đều có xác suất như nhau, nên định nghĩa xác suất sơ khai áp dụng được.

Nếu áp dụng định nghĩa sơ khai trực tiếp, ta phải đếm số cách gán ngày sinh sao cho ít nhất hai người trùng ngày. Nhưng phép đếm này khó: Emma và Steve có thể trùng ngày sinh, hoặc Steve và Naomi; có thể cả ba người cùng ngày sinh; cũng có thể ba người ấy cùng ngày sinh và hai người khác trong nhóm cùng chia sẻ một ngày sinh khác; còn nhiều trường hợp nữa.

Thay vào đó, hãy đếm biến cố đối: số cách gán ngày sinh sao cho không ai trùng ngày sinh với ai. Việc này tương đương với lấy mẫu không hoàn lại từ 365 ngày, nên số khả năng là $365\cdot364\cdot363\cdots(365-k+1)$ nếu $k\le365$. Do đó, xác suất không có ngày sinh trùng nhau trong một nhóm $k$ người là

$$P(\text{không trùng ngày sinh})=\frac{365\cdot364\cdots(365-k+1)}{365^k},$$

và xác suất có ít nhất một cặp trùng ngày sinh là

$$P(\text{ít nhất một cặp trùng ngày sinh})=1-\frac{365\cdot364\cdots(365-k+1)}{365^k}.$$

Hình 1.4 biểu diễn xác suất có ít nhất một cặp trùng ngày sinh theo $k$. Giá trị $k$ nhỏ nhất làm xác suất này vượt $0{,}5$ là $k=23$. Vậy trong một nhóm 23 người, xác suất có ít nhất hai người cùng ngày sinh lớn hơn 50%. Khi $k=57$, xác suất ấy đã vượt 99%.

**Hình 1.4.** Xác suất có ít nhất hai người cùng ngày sinh trong căn phòng có $k$ người. Xác suất lần đầu vượt $0{,}5$ khi $k=23$.

Tất nhiên, với $k=366$ thì chắc chắn có người trùng ngày sinh. Nhưng điều đáng ngạc nhiên là với số người ít hơn rất nhiều, sự trùng ngày sinh vẫn gần như chắc chắn. Để có trực giác nhanh về điều này, hãy lưu ý rằng 23 người tạo thành $\binom{23}{2}=253$ cặp; bất kỳ cặp nào trong số đó cũng có thể trùng ngày sinh.

Bài tập 24 và 25 cho thấy bài toán ngày sinh không chỉ là một trò vui trong tiệc tùng hay cách rèn trực giác về sự trùng hợp: nó còn có các ứng dụng quan trọng trong thống kê và khoa học máy tính. Bài tập 60 khảo sát trường hợp tổng quát hơn, khi xác suất sinh vào mỗi ngày không nhất thiết bằng $1/365$. Hóa ra trong trường hợp các xác suất không bằng nhau, khả năng có ít nhất một cặp trùng ngày sinh còn cao hơn.

**Cảnh báo 1.4.9 (Gắn nhãn đối tượng).** Việc lấy mẫu từ một quần thể là khái niệm rất cơ bản trong thống kê. Cần xem những đối tượng hoặc những người trong quần thể là các cá thể có tên hoặc nhãn riêng. Chẳng hạn, nếu có $n$ quả bóng trong một chiếc lọ, ta có thể tưởng tượng chúng được đánh số từ 1 đến $n$, ngay cả khi mắt thường thấy chúng giống hệt nhau. Trong bài toán ngày sinh, ta có thể gán mã định danh cho từng người thay vì coi họ là những hạt không thể phân biệt hay một đám đông vô danh.

Một ví dụ liên quan là sai lầm đáng học hỏi của Leibniz trong một bài toán tưởng như đơn giản (xem Gorroochurn [15] để đọc về trường hợp này và nhiều bài toán xác suất khác dưới góc nhìn lịch sử).

**Ví dụ 1.4.10 (Sai lầm của Leibniz).** Nếu gieo hai con xúc xắc cân đối, tổng bằng 11 hay tổng bằng 12 có khả năng xảy ra cao hơn?

**Lời giải.** Đặt tên hai con xúc xắc là $A$ và $B$, coi mỗi lần gieo một con là một phép thử thành phần. Theo quy tắc nhân, có 36 cặp kết quả có thứ tự dạng $(\text{giá trị của }A,\text{giá trị của }B)$; do tính đối xứng, tất cả đều có khả năng như nhau. Trong số đó, $(5,6)$ và $(6,5)$ cho tổng 11, còn chỉ $(6,6)$ cho tổng 12. Vì vậy, tổng 11 có khả năng xảy ra gấp đôi tổng 12: xác suất tương ứng là $1/18$ và $1/36$.

Tuy nhiên, Leibniz đã lập luận sai rằng tổng 11 và tổng 12 có khả năng như nhau. Ông cho rằng gieo được 12 điểm cũng có khả năng như gieo được 11 điểm vì mỗi trường hợp chỉ có một cách. Ở đây, Leibniz mắc lỗi coi hai con xúc xắc không thể phân biệt, xem $(5,6)$ và $(6,5)$ là cùng một kết quả.

Làm sao tránh sai lầm của Leibniz? Trước hết, như Cảnh báo 1.4.9 đã giải thích, nên gắn nhãn cho các đối tượng thay vì xem chúng là không thể phân biệt. Nếu Leibniz gọi hai con xúc xắc là $A$ và $B$, hoặc xanh lá và cam, hoặc trái và phải, ông đã không mắc lỗi này. Thứ hai, trước khi dùng phép đếm để tính xác suất, ta cần tự hỏi định nghĩa sơ khai có áp dụng được không (xem Cảnh báo 1.4.21 để biết một ví dụ khác cho thấy cần thận trọng).

#### 1.4.2. Điều chỉnh khi đếm trùng

Trong nhiều bài toán đếm, không dễ đếm trực tiếp sao cho mỗi khả năng được tính đúng một lần. Tuy nhiên, nếu ta có thể đếm mỗi khả năng đúng $c$ lần, thì chỉ cần chia kết quả cho $c$. Chẳng hạn, nếu mỗi khả năng bị đếm hai lần, chia cho 2 sẽ cho số lượng đúng. Chúng tôi gọi đó là *điều chỉnh khi đếm trùng*.

**Ví dụ 1.4.11 (Ủy ban và đội).** Xét một nhóm bốn người.

(a) Có bao nhiêu cách chọn một ủy ban hai người?

(b) Có bao nhiêu cách chia bốn người thành hai đội, mỗi đội hai người?

**Lời giải.**

(a) Có thể liệt kê trực tiếp: đánh số người là 1, 2, 3, 4 thì các cặp là $12$, $13$, $14$, $23$, $24$, $34$.

Một cách khác là dùng quy tắc nhân rồi điều chỉnh phần đếm trùng. Có 4 cách chọn người thứ nhất vào ủy ban và 3 cách chọn người thứ hai. Nhưng mỗi ủy ban bị tính hai lần, vì chọn 1 rồi 2 cũng chính là chọn 2 rồi 1. Do đó, số khả năng là $(4\cdot3)/2=6$.

(b) Có ba cách thấy rằng chỉ có 3 cách chia đội. Ta có thể liệt kê: $12\mid34$, $13\mid24$ và $14\mid23$. Tuy nhiên, với nhóm lớn hơn, việc liệt kê sẽ sớm trở nên dài dòng hoặc bất khả thi. Cách thứ hai là nhận thấy chỉ cần chọn đồng đội của người số 1; đội còn lại tự xác định. Cách thứ ba là dựa vào (a): có 6 cách chọn một đội, nhưng mỗi cách chia đội bị tính hai lần, vì chọn 1 và 2 vào một đội tương đương với chọn 3 và 4 vào một đội. Vậy đáp án một lần nữa là $6/2=3$.

*Hệ số nhị thức* đếm số tập con có kích thước xác định của một tập hợp, chẳng hạn số cách chọn ủy ban $k$ người từ một nhóm $n$ người. Tập hợp và tập con theo định nghĩa không có thứ tự; ví dụ $\{3,1,4\}=\{4,1,3\}$. Vì thế, ta đang đếm số cách chọn $k$ đối tượng trong $n$ đối tượng, không hoàn lại và không phân biệt thứ tự chọn.

**Định nghĩa 1.4.12 (Hệ số nhị thức).** Với các số nguyên không âm $k,n$, hệ số nhị thức $\binom nk$, đọc là “$n$ chọn $k$”, là số tập con gồm $k$ phần tử của một tập hợp gồm $n$ phần tử.

Chẳng hạn, $\binom42=6$, như đã thấy trong Ví dụ 1.4.11. Hệ số nhị thức $\binom nk$ đôi khi được gọi là *tổ hợp*, nhưng ở đây chúng tôi không dùng tên đó vì từ “tổ hợp” còn hữu ích với nghĩa thông thường rộng hơn. Có thể tính hệ số nhị thức bằng công thức đại số sau.

**Định lý 1.4.13 (Công thức hệ số nhị thức).** Nếu $k\le n$,

$$\binom nk=\frac{n(n-1)\cdots(n-k+1)}{k!}=\frac{n!}{(n-k)!k!}.$$

Nếu $k>n$ thì $\binom nk=0$.

**Chứng minh.** Cho $A$ là một tập hợp có $|A|=n$. Mọi tập con của $A$ đều có nhiều nhất $n$ phần tử, nên $\binom nk=0$ nếu $k>n$. Bây giờ xét $k\le n$. Theo Định lý 1.4.6, có $n(n-1)\cdots(n-k+1)$ cách chọn $k$ phần tử có thứ tự, không hoàn lại. Mỗi tập con cần đếm bị tính $k!$ lần do ta không quan tâm thứ tự của các phần tử đã chọn. Chia cho $k!$ sẽ được số lượng đúng.

**Cảnh báo 1.4.14.** Hệ số nhị thức $\binom nk$ thường được định nghĩa bằng giai thừa, nhưng cần nhớ $\binom nk=0$ khi $k>n$, dù giai thừa của số âm không được định nghĩa. Ngoài ra, biểu thức ở giữa trong Định lý 1.4.13 thường thuận tiện hơn khi tính toán so với biểu thức có giai thừa, vì giai thừa tăng cực nhanh. Chẳng hạn, có thể tính nhẩm $\binom{100}{2}=100\cdot99/2=4950$; còn tính $100!/(98!\cdot2!)$ bằng cách tìm riêng $100!$ và $98!$ vừa lãng phí, vừa dễ gặp rắc rối vì những con số khổng lồ ($100!\approx9{,}33\times10^{157}$).

**Ví dụ 1.4.15 (Ban điều hành câu lạc bộ).** Trong một câu lạc bộ có $n$ người, có $n(n-1)(n-2)$ cách chọn chủ tịch, phó chủ tịch và thủ quỹ; nếu chỉ chọn 3 cán bộ mà không định trước chức danh, số cách là $\binom n3=n(n-1)(n-2)/3!$.

**Ví dụ 1.4.16 (Hoán vị chữ cái của một từ).** Có bao nhiêu cách sắp xếp các chữ cái trong `LALALAAA`? Để xác định một cách sắp xếp, ta chỉ cần chọn vị trí cho 5 chữ A (hoặc tương đương, chọn vị trí cho 3 chữ L). Vậy có $\binom85=\binom83=8\cdot7\cdot6/3!=56$ cách.

Còn với từ `STATISTICS` thì sao? Có hai cách tiếp cận. Ta có thể chọn vị trí cho các chữ S, rồi cho các chữ T trong những vị trí còn lại, tiếp đến các chữ I, rồi chữ A (vị trí chữ C sẽ tự xác định). Hoặc bắt đầu từ $10!$ rồi điều chỉnh phần đếm trùng bằng cách chia cho $3!3!2!$, vì các chữ S có thể đổi chỗ cho nhau, tương tự với các chữ T và các chữ I. Kết quả là

$$\binom{10}{3}\binom73\binom42\binom21=\frac{10!}{3!3!2!}=50400\text{ khả năng}.$$

**Ví dụ 1.4.17 (Định lý nhị thức).** Định lý nhị thức phát biểu rằng

$$ (x+y)^n=\sum_{k=0}^{n}\binom nk x^k y^{n-k}. $$

Để chứng minh, hãy khai triển tích $(x+y)(x+y)\cdots(x+y)$ gồm $n$ thừa số. Tương tự như $(a+b)(c+d)=ac+ad+bc+bd$ là tổng những hạng tử tạo thành bằng cách chọn $a$ hoặc $b$ từ thừa số thứ nhất (không chọn cả hai), rồi chọn $c$ hoặc $d$ từ thừa số thứ hai, các hạng tử của $(x+y)^n$ được tạo thành bằng cách chọn $x$ hoặc $y$ từ mỗi thừa số. Có $\binom nk$ cách chọn đúng $k$ chữ $x$; mỗi cách đều cho hạng tử $x^k y^{n-k}$. Định lý nhị thức được chứng minh.

Ta có thể dùng hệ số nhị thức để tính xác suất trong nhiều bài toán mà định nghĩa sơ khai áp dụng được.

**Ví dụ 1.4.18 (Cù lũ trong poker).** Chia một tay bài 5 lá từ bộ bài chuẩn 52 lá đã xáo kỹ. Trong poker, tay bài được gọi là *cù lũ* nếu có ba lá cùng hạng và hai lá thuộc một hạng khác, chẳng hạn ba lá 7 và hai lá 10 (theo thứ tự bất kỳ). Xác suất được cù lũ là bao nhiêu?

**Lời giải.** Do tính đối xứng, mọi tay bài trong $\binom{52}{5}$ tay có khả năng như nhau, nên có thể dùng định nghĩa sơ khai. Để đếm số tay cù lũ, hãy dùng quy tắc nhân và hình dung sơ đồ cây. Có 13 cách chọn hạng xuất hiện ba lần. Để cụ thể, giả sử đó là hạng 7 và xét nhánh tương ứng. Có $\binom43$ cách chọn ba lá 7. Tiếp theo, có 12 cách chọn hạng xuất hiện hai lần; giả sử đó là hạng 10. Có $\binom42$ cách chọn hai lá 10. Vậy

$$P(\text{cù lũ})=\frac{13\binom43\cdot12\binom42}{\binom{52}{5}}=\frac{3744}{2598960}\approx0{,}00144.$$

Giá trị thập phân gần đúng hữu ích hơn khi chơi poker, nhưng đáp án viết bằng hệ số nhị thức vừa chính xác vừa tự cho thấy nguồn gốc từng số: nhìn thấy $\binom{52}{5}$ gợi ý nhiều hơn hẳn nhìn thấy $2598960$.

**Ví dụ 1.4.19 (Bài toán Newton–Pepys).** Samuel Pepys đã hỏi Isaac Newton bài toán sau vì muốn dùng kết quả trong cờ bạc. Biến cố nào sau đây có xác suất cao nhất?

- $A$: Có ít nhất một mặt 6 khi gieo 6 con xúc xắc cân đối.
- $B$: Có ít nhất hai mặt 6 khi gieo 12 con xúc xắc cân đối.
- $C$: Có ít nhất ba mặt 6 khi gieo 18 con xúc xắc cân đối.

**Lời giải.** Ba phép thử lần lượt có $6^6$, $6^{12}$ và $6^{18}$ kết quả có thể có. Do tính đối xứng, định nghĩa sơ khai áp dụng được cho cả ba.

Với $A$, đếm số cách *không có* mặt 6 dễ hơn đếm số cách có ít nhất một mặt 6. Không có mặt 6 tương đương với chọn có hoàn lại 6 lần từ các số 1 đến 5, nên có $5^6$ kết quả thuận lợi cho $A^c$ (và $6^6-5^6$ kết quả thuận lợi cho $A$). Do đó,

$$P(A)=1-\frac{5^6}{6^6}\approx0{,}67.$$

Với $B$, ta lại đếm các kết quả thuộc $B^c$ trước. Có $5^{12}$ cách không ra mặt 6 trong 12 lần gieo. Có $\binom{12}{1}5^{11}$ cách ra đúng một mặt 6: trước hết chọn con xúc xắc nào ra mặt 6, sau đó chọn có hoàn lại từ 1 đến 5 cho 11 con còn lại. Cộng hai trường hợp này, ta được số cách không đạt ít nhất hai mặt 6. Vậy

$$P(B)=1-\frac{5^{12}+\binom{12}{1}5^{11}}{6^{12}}\approx0{,}62.$$

Với $C$, ta đếm các kết quả thuộc $C^c$, tức số cách ra không, một hoặc hai mặt 6 trong 18 lần gieo. Lần lượt có $5^{18}$, $\binom{18}{1}5^{17}$ và $\binom{18}{2}5^{16}$ cách (trong trường hợp cuối, chọn hai con ra mặt 6 rồi quyết định kết quả của 16 con còn lại). Do đó,

$$P(C)=1-\frac{5^{18}+\binom{18}{1}5^{17}+\binom{18}{2}5^{16}}{6^{18}}\approx0{,}60.$$

Vì vậy, $A$ có xác suất cao nhất.

Newton cũng tìm được đáp án đúng bằng cách tính tương tự. Ông còn giải thích bằng trực giác vì sao $A$ có khả năng cao nhất, nhưng lập luận trực giác ấy không hợp lệ. Như Stigler [27] giải thích, nếu dùng xúc xắc bị chỉnh trọng số, thứ tự xác suất của $A,B,C$ có thể khác đi, trong khi lập luận trực giác của Newton lại không phụ thuộc vào việc xúc xắc có cân đối hay không.

Trong cuốn sách này, chúng ta quan tâm đến phép đếm vì đôi khi nó giúp tính xác suất, chứ không phải chỉ vì bản thân việc đếm. Ví dụ tiếp theo là một bài toán đếm đẹp nhưng dễ gây hiểu nhầm: lời giải rất thanh nhã, song hiếm khi kết quả có thể dùng cùng định nghĩa xác suất sơ khai.

**Ví dụ 1.4.20 (Bose–Einstein).** Có bao nhiêu cách chọn $k$ lần từ một tập gồm $n$ đối tượng, có hoàn lại, nếu thứ tự không quan trọng (ta chỉ quan tâm mỗi đối tượng được chọn bao nhiêu lần)?

**Lời giải.** Khi thứ tự quan trọng, quy tắc nhân cho đáp án $n^k$. Nhưng bài toán này khó hơn nhiều. Ta giải bằng một bài toán *đẳng cấu*: cùng một bài toán dưới dạng khác.

Hãy tìm số cách đặt $k$ hạt không thể phân biệt vào $n$ hộp có thể phân biệt. Nghĩa là hoán đổi các hạt cho nhau không tạo ra một khả năng mới: chỉ số hạt trong mỗi hộp là quan trọng. Có thể mã hóa tự nhiên mỗi cách phân bố bằng một chuỗi ký hiệu `|` và `l`, như ở Hình 1.5.

Để hợp lệ, chuỗi phải bắt đầu và kết thúc bằng `|`; ở giữa phải có đúng $n-1$ ký hiệu `|` và $k$ ký hiệu `l`. Ngược lại, mỗi chuỗi như vậy mã hóa được một cách phân bố hạt vào hộp. Do đó, giữa hai vách ngoài có $n+k-1$ vị trí. Ta chỉ cần chọn vị trí đặt $k$ ký hiệu `l`, nên số khả năng là $\binom{n+k-1}{k}$. Số này được gọi là *giá trị Bose–Einstein*, vì trong thập niên 1920, hai nhà vật lý Satyendra Nath Bose và Albert Einstein đã nghiên cứu các bài toán liên quan đến những hạt không thể phân biệt. Những ý tưởng đó giúp họ dự đoán đúng sự tồn tại của một trạng thái vật chất kỳ lạ, gọi là *ngưng tụ Bose–Einstein*.

**Hình 1.5.** Mã hóa Bose–Einstein: việc đặt $k=7$ hạt không thể phân biệt vào $n=4$ hộp có thể phân biệt được biểu diễn bằng chuỗi ký hiệu `|` (vách ngăn) và `l` (hạt).

Để quay lại câu hỏi ban đầu, cho mỗi hộp ứng với một trong $n$ đối tượng và xem các hạt là những “dấu kiểm đếm” số lần đối tượng ấy được chọn. Chẳng hạn, nếu một hộp chứa đúng 3 hạt thì đối tượng tương ứng được chọn đúng 3 lần. Việc các hạt không thể phân biệt tương ứng với việc ta không quan tâm thứ tự chọn đối tượng. Vậy đáp án của bài toán ban đầu cũng là $\binom{n+k-1}{k}$.

Một bài toán đẳng cấu khác là đếm số nghiệm $(x_1,\ldots,x_n)$ của phương trình $x_1+\cdots+x_n=k$, trong đó các $x_i$ là số nguyên không âm. Hai bài toán tương đương vì ta có thể xem $x_i$ là số hạt trong hộp thứ $i$.

**Cảnh báo 1.4.21.** Không nên dùng kết quả Bose–Einstein trong định nghĩa xác suất sơ khai, trừ những trường hợp rất đặc biệt. Chẳng hạn, xét một cuộc khảo sát lấy mẫu $k$ người từ quần thể $n$ người, chọn từng người một, có hoàn lại và với xác suất bằng nhau. Khi ấy, $n^k$ mẫu *có thứ tự* có khả năng xảy ra như nhau, nên áp dụng được định nghĩa sơ khai. Nhưng $\binom{n+k-1}{k}$ mẫu *không xét thứ tự* (chỉ quan tâm mỗi người được chọn bao nhiêu lần) thì không có khả năng xảy ra như nhau.

Ví dụ khác: với $n=365$ ngày trong năm và $k$ người, có bao nhiêu danh sách ngày sinh không xét thứ tự? Khi $k=3$, ta muốn đếm những danh sách như (1 tháng 5, 31 tháng 3, 11 tháng 4), coi mọi hoán vị là tương đương. Không thể đơn giản lấy $n^k/3!$ để điều chỉnh đếm trùng: có 6 hoán vị của ba ngày sinh vừa nêu, nhưng chỉ có 3 hoán vị của (31 tháng 3, 31 tháng 3, 11 tháng 4). Theo Bose–Einstein, số danh sách là $\binom{n+k-1}{k}$. Tuy nhiên, các danh sách ngày sinh *có thứ tự* mới có khả năng như nhau; danh sách không xét thứ tự thì không. Vì vậy, không nên dùng giá trị Bose–Einstein để tính xác suất trong bài toán ngày sinh.

### 1.5. Chứng minh bằng câu chuyện

*Chứng minh bằng câu chuyện* là chứng minh thông qua diễn giải. Với bài toán đếm, cách này thường có nghĩa là đếm cùng một đối tượng theo hai cách khác nhau, thay vì làm phép biến đổi đại số dài dòng. Nó thường tránh được những phép tính rối rắm và giải thích vì sao kết quả đúng sâu hơn một chứng minh đại số. Từ “câu chuyện” có nhiều nghĩa, có nghĩa mang tính toán học hơn những nghĩa khác, nhưng chứng minh bằng câu chuyện theo cách dùng ở đây vẫn là một chứng minh toán học hoàn toàn hợp lệ. Sau đây là một số ví dụ, đồng thời là những ví dụ bổ sung về phép đếm.

**Ví dụ 1.5.1 (Chọn phần bù).** Với các số nguyên không âm $n,k$ và $k\le n$,

$$\binom nk=\binom n{n-k}.$$

Có thể dễ dàng kiểm tra bằng đại số khi viết hệ số nhị thức dưới dạng giai thừa, nhưng một chứng minh bằng câu chuyện giúp trực giác hiểu kết quả hơn.

**Chứng minh bằng câu chuyện.** Xét việc chọn một ủy ban gồm $k$ người từ nhóm $n$ người. Ta biết có $\binom nk$ khả năng. Nhưng cũng có thể chọn ủy ban bằng cách chỉ ra $n-k$ người *không* thuộc ủy ban. Biết ai ở trong thì xác định được ai ở ngoài, và ngược lại. Vì hai vế đếm cùng một thứ theo hai cách, chúng bằng nhau.

**Ví dụ 1.5.2 (Đội trưởng).** Với các số nguyên dương $n,k$ và $k\le n$,

$$n\binom{n-1}{k-1}=k\binom nk.$$

Một lần nữa, có thể dễ dàng kiểm tra bằng đại số (dùng $m!=m(m-1)!$ với số nguyên dương $m$), nhưng chứng minh bằng câu chuyện mang lại hiểu biết rõ hơn.

**Chứng minh bằng câu chuyện.** Xét nhóm $n$ người, chọn một đội $k$ người và chỉ định một người làm đội trưởng. Để xác định một khả năng, ta có thể chọn đội trưởng trước rồi chọn $k-1$ thành viên còn lại; số cách là vế trái. Tương đương, ta có thể chọn $k$ thành viên trước rồi chọn đội trưởng trong số họ; số cách là vế phải.

**Ví dụ 1.5.3 (Đồng nhất thức Vandermonde).** Một hệ thức nổi tiếng giữa các hệ số nhị thức, gọi là *đồng nhất thức Vandermonde*, phát biểu:

$$\binom{m+n}{k}=\sum_{j=0}^{k}\binom mj\binom n{k-j}.$$

Đồng nhất thức này sẽ xuất hiện vài lần trong cuốn sách. Nếu cố chứng minh bằng cách khai triển thẳng mọi hệ số nhị thức, ta sẽ gặp một mớ phép tính rối rắm. Nhưng một câu chuyện có thể chứng minh kết quả một cách thanh nhã và cho thấy rõ vì sao nó đúng.

**Chứng minh bằng câu chuyện.** Xét một nhóm gồm $m$ nam và $n$ nữ, chọn một ủy ban $k$ người. Có $\binom{m+n}{k}$ khả năng. Nếu ủy ban có $j$ nam thì phải có $k-j$ nữ. Vế phải của đồng nhất thức Vandermonde cộng số khả năng trong từng trường hợp theo $j$.

**Ví dụ 1.5.4 (Ghép cặp).** Hãy dùng chứng minh bằng câu chuyện để chỉ ra rằng

$$\frac{(2n)!}{2^n n!}=(2n-1)(2n-3)\cdots3\cdot1.$$

**Chứng minh bằng câu chuyện.** Ta sẽ cho thấy hai vế đều đếm số cách chia $2n$ người thành $n$ cặp. Đánh số họ từ 1 đến $2n$. Ta có thể ghép cặp bằng cách xếp họ theo một thứ tự nào đó, rồi ghép hai người đầu thành một cặp, hai người tiếp theo thành một cặp, cứ thế. Cách này đếm mỗi kết quả $n!\cdot2^n$ lần, vì thứ tự giữa các cặp không quan trọng và thứ tự của hai người trong từng cặp cũng không quan trọng. Một cách khác là nhận thấy có $2n-1$ lựa chọn bạn cặp cho người số 1; sau đó có $2n-3$ lựa chọn bạn cặp cho người số 2 (hoặc người số 3, nếu số 2 đã ghép với số 1); cứ tiếp tục như vậy.

### 1.6. Định nghĩa xác suất tổng quát

Ta đã biết một số phương pháp đếm kết quả trong không gian mẫu, nhờ đó có thể tính xác suất khi định nghĩa sơ khai áp dụng được. Nhưng định nghĩa ấy chỉ đưa ta đi được đến một mức nhất định: nó đòi hỏi các kết quả có khả năng như nhau và không xử lý được không gian mẫu vô hạn. Để khái quát hóa xác suất, ta sẽ sử dụng một điều tuyệt vời của toán học: được tự đặt ra định nghĩa. Cụ thể, ta viết một danh sách ngắn những tính chất mong muốn của xác suất (trong toán học, chúng được gọi là *tiên đề*), rồi định nghĩa một hàm xác suất là hàm thỏa mãn các tính chất ấy.

Đây là định nghĩa tổng quát về xác suất sẽ được dùng trong phần còn lại của cuốn sách. Nó chỉ cần hai tiên đề, nhưng từ đó có thể chứng minh rất nhiều kết quả.

**Định nghĩa 1.6.1 (Định nghĩa xác suất tổng quát).** Một *không gian xác suất* gồm không gian mẫu $S$ và hàm xác suất $P$. Hàm này nhận một biến cố $A\subseteq S$ làm đầu vào và cho ra $P(A)$, một số thực từ 0 đến 1. Hàm $P$ phải thỏa các tiên đề:

1. $P(\varnothing)=0$ và $P(S)=1$.
2. Nếu $A_1,A_2,\ldots$ là những biến cố đôi một rời nhau, thì

   $$P\!\left(\bigcup_{j=1}^{\infty}A_j\right)=\sum_{j=1}^{\infty}P(A_j).$$

   Nói các biến cố này đôi một rời nhau tức là chúng loại trừ nhau: $A_i\cap A_j=\varnothing$ khi $i\ne j$.

Trong Thế giới Sỏi, định nghĩa này nói rằng xác suất ứng xử như khối lượng: một đống sỏi rỗng có khối lượng 0; tổng khối lượng mọi viên sỏi là 1; nếu các đống sỏi không chồng lấn, ta có thể cộng khối lượng từng đống để được khối lượng chung. Khác với trường hợp sơ khai, giờ đây các viên sỏi có thể có khối lượng khác nhau. Ta cũng có thể có vô hạn đếm được viên sỏi, miễn là tổng khối lượng của chúng bằng 1.

Ta thậm chí có thể có không gian mẫu vô hạn không đếm được, chẳng hạn cho $S$ là một miền trên mặt phẳng. Khi đó, thay vì các viên sỏi, ta có thể hình dung một lớp bùn trải trên miền ấy, với tổng khối lượng bằng 1.

Bất kỳ hàm $P$ nào ánh xạ biến cố sang số trong $[0,1]$ và thỏa hai tiên đề trên đều được xem là một hàm xác suất hợp lệ. Tuy nhiên, các tiên đề không cho biết phải *diễn giải* xác suất như thế nào; có nhiều trường phái tư tưởng khác nhau.

Theo quan điểm *tần suất*, xác suất biểu thị tần suất dài hạn qua một số lượng lớn lần lặp lại phép thử. Nếu nói đồng xu có xác suất ra mặt ngửa là $1/2$, nghĩa là khi tung đi tung lại rất nhiều lần, khoảng 50% số lần sẽ ra mặt ngửa.

Theo quan điểm *Bayes*, xác suất biểu thị mức độ tin tưởng đối với biến cố đang xét. Nhờ đó, ta có thể gán xác suất cho những giả thuyết như “ứng cử viên A sẽ thắng cử” hoặc “bị cáo có tội”, dù không thể lặp lại cùng một cuộc bầu cử hay cùng một tội phạm vô số lần.

Hai quan điểm Bayes và tần suất bổ sung cho nhau; cả hai đều sẽ giúp phát triển trực giác trong các chương sau. Bất kể ta chọn cách diễn giải nào, hai tiên đề vẫn cho phép suy ra các tính chất xác suất khác, và các kết quả ấy đúng với mọi hàm xác suất hợp lệ.

**Định lý 1.6.2 (Các tính chất của xác suất).** Với mọi biến cố $A,B$, xác suất có các tính chất:

1. $P(A^c)=1-P(A)$.
2. Nếu $A\subseteq B$ thì $P(A)\le P(B)$.
3. $P(A\cup B)=P(A)+P(B)-P(A\cap B)$.

**Chứng minh.**

1. Vì $A$ và $A^c$ rời nhau, đồng thời $A\cup A^c=S$, tiên đề thứ hai cho $P(S)=P(A\cup A^c)=P(A)+P(A^c)$. Tiên đề thứ nhất cho $P(S)=1$, nên $P(A)+P(A^c)=1$.
2. Nếu $A\subseteq B$, ta có thể viết $B$ thành hợp của $A$ và $B\cap A^c$, trong đó $B\cap A^c$ là phần thuộc $B$ nhưng không thuộc $A$ (xem hình minh họa trong PDF). Vì hai tập này rời nhau, tiên đề thứ hai cho $P(B)=P(A\cup(B\cap A^c))=P(A)+P(B\cap A^c)$. Xác suất không âm, nên $P(B\cap A^c)\ge0$. Do đó $P(B)\ge P(A)$.
3. Có thể thấy trực giác của kết quả qua biểu đồ Venn trong PDF. Miền $A\cup B$ được tô màu, nhưng xác suất của miền này không đơn giản là $P(A)+P(B)$, vì như vậy vùng giao $A\cap B$ bị tính hai lần. Ta cần trừ $P(A\cap B)$. Đó là trực giác hữu ích, nhưng chưa phải chứng minh.

   Để chứng minh từ các tiên đề, viết $A\cup B$ thành hợp của hai biến cố rời nhau $A$ và $B\cap A^c$. Theo tiên đề thứ hai, $P(A\cup B)=P(A)+P(B\cap A^c)$. Vậy chỉ cần chứng minh $P(B\cap A^c)=P(B)-P(A\cap B)$. Vì $A\cap B$ và $B\cap A^c$ rời nhau, đồng thời hợp của chúng là $B$, áp dụng tiên đề thứ hai lần nữa cho $P(A\cap B)+P(B\cap A^c)=P(B)$. Từ đó có điều cần chứng minh.

Tính chất thứ ba là trường hợp riêng của *nguyên lý bao hàm–loại trừ*, công thức tính xác suất của hợp nhiều biến cố mà không nhất thiết các biến cố phải rời nhau. Ở trên, ta đã chứng minh với hai biến cố $A,B$:

$$P(A\cup B)=P(A)+P(B)-P(A\cap B).$$

Với ba biến cố, nguyên lý bao hàm–loại trừ cho

$$\begin{aligned}P(A\cup B\cup C)={}&P(A)+P(B)+P(C)\\&-P(A\cap B)-P(A\cap C)-P(B\cap C)\\&+P(A\cap B\cap C).\end{aligned}$$

Để có trực giác, hãy xét biểu đồ Venn ba tập trong PDF. Muốn tính tổng diện tích miền $A\cup B\cup C$ được tô màu, trước hết ta cộng diện tích ba hình tròn: $P(A)+P(B)+P(C)$. Các vùng giao từng cặp đều bị tính hai lần, nên ta trừ $P(A\cap B)+P(A\cap C)+P(B\cap C)$. Cuối cùng, vùng chính giữa đã bị cộng ba lần rồi trừ ba lần; để tính nó đúng một lần, ta phải cộng lại một lần. Như vậy, mỗi vùng trong hình được tính đúng một lần.

Bây giờ có thể viết nguyên lý bao hàm–loại trừ cho $n$ biến cố.

**Định lý 1.6.3 (Bao hàm–loại trừ).** Với mọi biến cố $A_1,\ldots,A_n$,

$$\begin{aligned}P\!\left(\bigcup_{i=1}^{n}A_i\right)={}&\sum_iP(A_i)-\sum_{i<j}P(A_i\cap A_j)\\&+\sum_{i<j<k}P(A_i\cap A_j\cap A_k)-\cdots\\&+(-1)^{n+1}P(A_1\cap\cdots\cap A_n).\end{aligned}$$

Có thể chứng minh công thức này bằng quy nạp chỉ từ các tiên đề. Tuy nhiên, sau khi giới thiệu thêm công cụ, chúng tôi sẽ trình bày một chứng minh ngắn hơn ở Chương 4. Lý do cộng và trừ xen kẽ trong công thức tổng quát tương tự như ở các trường hợp riêng vừa xét.

Ví dụ tiếp theo, bài toán khớp số của de Montmort, là một ứng dụng nổi tiếng của nguyên lý bao hàm–loại trừ. Pierre Rémond de Montmort là nhà toán học người Pháp nghiên cứu xác suất trong cờ bạc và viết một chuyên luận [21] phân tích nhiều trò chơi bài. Năm 1708, ông nêu ra bài toán sau, dựa trên trò chơi bài có tên *Treize*.

**Ví dụ 1.6.4 (Bài toán khớp số của de Montmort).** Xét một bộ $n$ lá bài được xáo kỹ, đánh số từ 1 đến $n$. Bạn lật lần lượt từng lá, vừa lật vừa đọc các số từ 1 đến $n$. Bạn thắng nếu tại một thời điểm nào đó, số bạn đọc trùng với số trên lá vừa lật (chẳng hạn lá thứ bảy mang số 7). Xác suất thắng là bao nhiêu?

**Lời giải.** Gọi $A_i$ là biến cố lá bài ở vị trí thứ $i$ mang số $i$. Ta cần tính xác suất của $A_1\cup\cdots\cup A_n$: chỉ cần ít nhất một lá mang số trùng vị trí thì bạn thắng. (Một thứ tự không có vị trí nào khớp được gọi là *hoán vị không điểm cố định*; hy vọng chưa ai phát điên vì thua trò chơi này.)

Để tìm xác suất của hợp, ta dùng bao hàm–loại trừ. Trước hết, $P(A_i)=1/n$ với mọi $i$. Có thể thấy điều này bằng định nghĩa sơ khai trên toàn không gian mẫu: có $n!$ thứ tự của bộ bài với xác suất như nhau, và $(n-1)!$ thứ tự thuận lợi cho $A_i$ (cố định lá số $i$ ở vị trí $i$, rồi tùy ý sắp xếp $n-1$ lá còn lại). Cũng có thể thấy bằng tính đối xứng: lá số $i$ có khả năng nằm ở mỗi vị trí như nhau, nên xác suất nằm ở vị trí thứ $i$ là $1/n$.

Tiếp theo,

$$P(A_i\cap A_j)=\frac{(n-2)!}{n!}=\frac1{n(n-1)},$$

vì ta buộc các lá số $i,j$ nằm đúng vị trí thứ $i,j$, còn $n-2$ lá khác có thể xếp tùy ý. Tương tự, $P(A_i\cap A_j\cap A_k)=1/[n(n-1)(n-2)]$, và quy luật tiếp tục với giao của bốn biến cố trở lên.

Trong công thức bao hàm–loại trừ, có $n$ hạng liên quan đến một biến cố, $\binom n2$ hạng liên quan đến hai biến cố, $\binom n3$ hạng liên quan đến ba biến cố, v.v. Nhờ tính đối xứng, các hạng $P(A_i)$ đều bằng nhau, các hạng $P(A_i\cap A_j)$ đều bằng nhau, nên biểu thức rút gọn đáng kể:

$$\begin{aligned}P\!\left(\bigcup_{i=1}^{n}A_i\right)&=n\frac1n-\binom n2\frac1{n(n-1)}+\binom n3\frac1{n(n-1)(n-2)}-\cdots+(-1)^{n+1}\frac1{n!}\\&=1-\frac1{2!}+\frac1{3!}-\cdots+(-1)^{n+1}\frac1{n!}.\end{aligned}$$

So sánh với chuỗi Taylor của $1/e$ (xem mục A.8 của phụ lục toán học),

$$e^{-1}=1-\frac1{1!}+\frac1{2!}-\frac1{3!}+\cdots,$$

ta thấy khi $n$ lớn, xác suất thắng cực gần $1-1/e$, tức khoảng $0{,}63$. Điều thú vị là khi $n$ tăng, xác suất thắng tiến đến $1-1/e$ chứ không tiến đến 0 hay 1. Khi bộ bài có nhiều lá hơn, số vị trí có thể khớp tăng lên, trong khi xác suất khớp tại một vị trí cụ thể giảm xuống. Hai tác động này bù trừ nhau, tạo nên xác suất khoảng $1-1/e$.

Bao hàm–loại trừ là công thức rất tổng quát để tính xác suất của hợp nhiều biến cố, nhưng hữu ích nhất khi các biến cố $A_j$ có tính đối xứng; nếu không, việc tính tổng có thể rất dài dòng. Nói chung, khi thiếu tính đối xứng, ta nên thử các công cụ khác trước và chỉ dùng bao hàm–loại trừ như biện pháp cuối.

### 1.7. Tóm tắt

Xác suất cho phép ta định lượng sự bất định và tính ngẫu nhiên một cách có nguyên tắc. Xác suất xuất hiện khi ta thực hiện một phép thử: tập hợp tất cả các kết quả có thể xảy ra được gọi là *không gian mẫu*; một tập con của không gian mẫu được gọi là *biến cố*. Khả năng chuyển đổi giữa cách mô tả biến cố bằng lời và cách viết toán học dưới dạng tập hợp — thường dùng hợp, giao và phần bù — rất hữu ích.

Thế giới Sỏi giúp hình dung không gian mẫu và biến cố khi không gian mẫu hữu hạn. Ở đó, mỗi kết quả là một viên sỏi, còn biến cố là một tập hợp các viên sỏi. Nếu mọi viên sỏi có cùng khối lượng (nghĩa là có khả năng được chọn như nhau), ta có thể áp dụng định nghĩa xác suất sơ khai và tính xác suất bằng cách đếm.

Vì vậy, chúng ta đã bàn đến một số công cụ đếm. Khi đếm số khả năng, ta thường dùng quy tắc nhân. Nếu không thể dùng quy tắc nhân trực tiếp, đôi khi ta có thể đếm mỗi khả năng đúng $c$ lần rồi chia cho $c$ để được số lượng thực.

Một sai lầm quan trọng cần tránh là áp dụng sai định nghĩa xác suất sơ khai: ngầm hoặc công khai giả định các kết quả có khả năng như nhau mà không có cơ sở. Một kỹ thuật giúp tránh sai lầm ấy là gắn nhãn cho các đối tượng, vừa để chính xác hơn, vừa để không bị cám dỗ xem chúng là không thể phân biệt.

Vượt ra ngoài định nghĩa sơ khai, ta định nghĩa xác suất là một hàm nhận biến cố và gán cho nó một số thực từ 0 đến 1. Một hàm xác suất hợp lệ phải thỏa hai tiên đề:

1. $P(\varnothing)=0$ và $P(S)=1$.
2. Nếu $A_1,A_2,\ldots$ đôi một rời nhau thì $P(\bigcup_{j=1}^{\infty}A_j)=\sum_{j=1}^{\infty}P(A_j)$.

Từ hai tiên đề này có thể suy ra nhiều tính chất hữu ích. Chẳng hạn, $P(A^c)=1-P(A)$ với mọi biến cố $A$, và với mọi biến cố $A_1,\ldots,A_n$ ta có công thức bao hàm–loại trừ

$$P\!\left(\bigcup_{i=1}^{n}A_i\right)=\sum_iP(A_i)-\sum_{i<j}P(A_i\cap A_j)+\sum_{i<j<k}P(A_i\cap A_j\cap A_k)-\cdots+(-1)^{n+1}P(A_1\cap\cdots\cap A_n).$$

Với $n=2$, công thức có dạng gọn hơn nhiều: $P(A_1\cup A_2)=P(A_1)+P(A_2)-P(A_1\cap A_2)$.

**Hình 1.6.** Hàm xác suất ánh xạ các biến cố thành các số từ 0 đến 1. Cần phân biệt *biến cố* với *xác suất*: cái trước là tập hợp, cái sau là con số. Trước khi thực hiện phép thử, ta thường chưa biết một biến cố cụ thể có xảy ra hay không. Vì thế, ta dùng hàm xác suất $P$ để gán cho nó xác suất xảy ra. Ta có thể dùng phép toán tập hợp để định nghĩa biến cố mới từ biến cố cũ, và dùng các tính chất xác suất để liên hệ xác suất của chúng. Khi tiếp tục tìm hiểu xác suất, chúng ta sẽ bổ sung nhiều khái niệm vào sơ đồ này.

### 1.8. R (trang PDF 45–46)

R là một môi trường tính toán thống kê và đồ họa rất mạnh, phổ biến và miễn phí trên Mac OS X, Windows và UNIX. Biết sử dụng R là một kỹ năng rất hữu ích. Có thể tải R và tìm thông tin liên quan tại http://www.r-project.org. RStudio là một giao diện khác cho R, miễn phí tại http://www.rstudio.com.

Trong mục R cuối mỗi chương, chúng tôi cung cấp mã để bạn thử các ví dụ của chương, nhất là bằng mô phỏng. Những mục này không nhằm giới thiệu đầy đủ về R; trên mạng đã có nhiều tài liệu hướng dẫn miễn phí, và cũng có nhiều sách viết về R. Thay vào đó, chúng cho thấy cách thực hiện các phép mô phỏng, tính toán và trực quan hóa gắn với nội dung từng chương.

#### Vectơ

R được xây dựng xoay quanh vectơ; làm quen với “tư duy vectơ hóa” rất quan trọng để dùng R hiệu quả. Để tạo một vectơ, ta dùng lệnh `c` (viết tắt của *combine* hoặc *concatenate*, nghĩa là kết hợp hoặc nối). Chẳng hạn, `v <- c(3,1,4,1,5,9)` định nghĩa `v` là vectơ $(3,1,4,1,5,9)$. Mũi tên trái `<-` được gõ bằng dấu `<` rồi dấu `-`. Có thể dùng dấu `=` thay thế, nhưng mũi tên thể hiện rõ hơn rằng biến bên trái được gán bằng giá trị bên phải. Tương tự, `n <- 110` gán `n` bằng 110; R xem `n` là một vectơ độ dài 1.

`sum(v)` cộng các phần tử của `v`; `max(v)` cho giá trị lớn nhất; `min(v)` cho giá trị nhỏ nhất; `length(v)` cho độ dài vectơ.

Để lấy vectơ $(1,2,\ldots,n)$, có thể viết ngắn là `1:n`. Tổng quát hơn, nếu $m,n$ là số nguyên, `m:n` cho dãy số nguyên từ $m$ đến $n$ (tăng nếu $m\le n$, ngược lại thì giảm).

Để truy cập phần tử thứ $i$ của vectơ `v`, dùng `v[i]`. Có thể lấy vectơ con bằng `v[c(1,3,5)]`, gồm phần tử thứ nhất, thứ ba và thứ năm của `v`. Cũng có thể chỉ định phần tử cần loại bỏ bằng dấu trừ: `v[-(2:4)]` cho vectơ nhận được khi bỏ các phần tử từ thứ hai đến thứ tư. Dấu ngoặc là cần thiết, vì `-2:4` sẽ là dãy $(-2,-1,\ldots,4)$.

Nhiều phép toán trong R được hiểu theo từng thành phần. Chẳng hạn, trong toán học, “lập phương một vectơ” không có định nghĩa chuẩn; nhưng trong R, `v^3` đơn giản là lập phương riêng từng phần tử. Tương tự, `1/(1:100)^2` là cách viết rất gọn để lấy vectơ $(1,1/2^2,1/3^2,\ldots,1/100^2)$. Trong toán học, $v+w$ không được định nghĩa nếu hai vectơ có độ dài khác nhau; nhưng trong R, vectơ ngắn hơn sẽ được “tái sử dụng” lặp lại! Chẳng hạn, `v+3` cộng 3 vào mỗi phần tử của `v`.

#### Giai thừa và hệ số nhị thức

Ta có thể tính $n!$ bằng `factorial(n)` và $\binom nk$ bằng `choose(n,k)`. Như đã thấy, giai thừa tăng cực nhanh. Giá trị $n$ lớn nhất mà R còn trả về một con số cho `factorial(n)` là bao nhiêu? Sau mức đó, R trả về `Inf` (vô cực) kèm thông báo cảnh báo. Với $n$ lớn hơn, vẫn có thể dùng `lfactorial(n)` để tính $\log(n!)$. Tương tự, `lchoose(n,k)` tính $\log\binom nk$.

#### Lấy mẫu và mô phỏng

Lệnh `sample` là một cách hữu ích để lấy mẫu ngẫu nhiên trong R. Về mặt kỹ thuật, đây là mẫu giả ngẫu nhiên vì phía sau có một thuật toán tất định, nhưng trong hầu hết tình huống thực tế, chúng “trông như” mẫu ngẫu nhiên. Chẳng hạn, `n <- 10; k <- 5` rồi `sample(n,k)` tạo một mẫu ngẫu nhiên có thứ tự gồm 5 số từ 1 đến 10, không hoàn lại, và mỗi số có xác suất như nhau. Để lấy mẫu có hoàn lại, dùng `sample(n,k,replace=TRUE)`.

Để tạo một hoán vị ngẫu nhiên của $1,2,\ldots,n$, có thể dùng `sample(n,n)`; nhờ các giá trị mặc định của R, có thể viết gọn thành `sample(n)`.

Ta cũng có thể dùng `sample` với vectơ không chứa số. Chẳng hạn, `letters` là vectơ có sẵn trong R, chứa 26 chữ cái thường của bảng chữ cái tiếng Anh. `sample(letters,7)` tạo một “từ” ngẫu nhiên dài 7 chữ cái bằng cách lấy mẫu từ bảng chữ cái, không hoàn lại.

Lệnh `sample` còn cho phép chỉ định xác suất riêng khi lấy mẫu mỗi số. Chẳng hạn, `sample(4, 3, replace=TRUE, prob=c(0.1,0.2,0.3,0.4))` lấy 3 số trong khoảng từ 1 đến 4, có hoàn lại, với các xác suất $(0{,}1,0{,}2,0{,}3,0{,}4)$. Nếu lấy mẫu không hoàn lại, ở mỗi bước, xác suất của một số chưa được chọn tỉ lệ với xác suất ban đầu của nó.

Tạo nhiều mẫu ngẫu nhiên cho phép ta mô phỏng một bài toán xác suất. Lệnh `replicate`, được giải thích bên dưới, là một cách thuận tiện để làm việc này.

#### Mô phỏng bài toán khớp số

Hãy dùng mô phỏng để cho thấy xác suất có một lá bài khớp vị trí trong Ví dụ 1.6.4 xấp xỉ $1-1/e$ khi bộ bài đủ lớn. Với R, ta có thể lặp lại phép thử nhiều lần và xem có bao nhiêu lần xuất hiện ít nhất một lá khớp:

```r
n <- 100
r <- replicate(10^4,sum(sample(n)==(1:n)))
sum(r>=1)/10^4
```

Dòng đầu chọn số lá bài trong bộ (ở đây là 100). Ở dòng thứ hai, hãy đọc từ trong ra ngoài:

- `sample(n)==(1:n)` là vectơ độ dài $n$; phần tử thứ $i$ bằng 1 nếu lá bài thứ $i$ khớp vị trí, ngược lại bằng 0. Với hai số $a,b$, biểu thức `a==b` là `TRUE` khi $a=b$ và `FALSE` nếu không. R mã hóa `TRUE` là 1, `FALSE` là 0.
- `sum` cộng các phần tử của vectơ, cho số lá khớp trong một lần chạy phép thử.
- `replicate` lặp lại việc này $10^4$ lần. Kết quả được lưu trong `r`, một vectơ độ dài $10^4$ chứa số lá khớp ở mỗi lần chạy.

Dòng cuối đếm số lần có ít nhất một lá khớp rồi chia cho tổng số lần mô phỏng.

Để giải thích mã ngay trong mã thay vì tài liệu riêng, ta có thể dùng ký hiệu `#` để bắt đầu phần chú thích. R bỏ qua chú thích, nhưng chúng giúp người đọc hiểu mã dễ hơn. Người đọc đó có thể chính là bạn: ngay cả khi chỉ mình bạn dùng mã, sau một tháng nhìn lại thường rất khó nhớ mọi phần có nghĩa gì và mã cần chạy ra sao. Chú thích ngắn có thể nằm cùng dòng với lệnh; chú thích dài nên viết trên dòng riêng. Ví dụ, phiên bản có chú thích của mô phỏng trên là:

```r
n <- 100 # số lá bài
r <- replicate(10^4,sum(sample(n)==(1:n))) # xáo bài; đếm số lá khớp
sum(r>=1)/10^4 # tỉ lệ lần chạy có ít nhất một lá khớp
```

Bạn nhận được kết quả bao nhiêu khi chạy mã? Chúng tôi nhận được $0{,}63$, khá gần $1-1/e$.

#### Tính toán và mô phỏng bài toán ngày sinh

Đoạn mã sau dùng `prod` (tính tích các phần tử của vectơ) để tìm xác suất có ít nhất một cặp trùng ngày sinh trong nhóm 23 người:

```r
k <- 23
1-prod((365-k+1):365)/365^k
```

Thuận tiện hơn, R có sẵn các hàm `pbirthday` và `qbirthday` cho bài toán ngày sinh. `pbirthday(k)` trả về xác suất có ít nhất một cặp trùng ngày sinh trong phòng có $k$ người. `qbirthday(p)` trả về số người cần có để xác suất xuất hiện ít nhất một cặp trùng ngày sinh đạt $p$. Chẳng hạn, `pbirthday(23)` là $0{,}507$ và `qbirthday(0.5)` là 23.

Ta cũng có thể tìm xác suất có ít nhất một bộ ba cùng ngày sinh: chỉ cần thêm `coincident=3` để chỉ định xét các bộ ba. Chẳng hạn, `pbirthday(23,coincident=3)` trả về $0{,}014$: với 23 người, xác suất có bộ ba trùng ngày sinh chỉ là 1,4%. `qbirthday(0.5,coincident=3)` trả về 88: cần 88 người để xác suất có ít nhất một bộ ba trùng ngày sinh đạt từ 50% trở lên.

Để mô phỏng bài toán ngày sinh, ta có thể dùng:

```r
b <- sample(1:365,23,replace=TRUE)
tabulate(b)
```

Đoạn mã tạo ngày sinh ngẫu nhiên cho 23 người rồi đếm số người sinh vào mỗi ngày. Lệnh `table(b)` tạo bảng đẹp hơn nhưng chạy chậm hơn. Có thể lặp lại $10^4$ lần như sau:

```r
r <- replicate(10^4, max(tabulate(sample(1:365,23,replace=TRUE))))
sum(r>=2)/10^4
```

Nếu xác suất sinh vào các ngày không bằng nhau, việc tính chính xác khó hơn nhiều. Nhưng có thể mở rộng mô phỏng dễ dàng vì `sample` cho phép chỉ định xác suất của từng ngày. Mặc định, `sample` gán xác suất như nhau, nên trong đoạn mã trên, mỗi ngày có xác suất $1/365$.

### 1.9. Bài tập (trang PDF 49–50)

Những bài tập được đánh dấu bằng biểu tượng lời giải trong sách có lời giải chi tiết trên stat110.net. Chúng tôi rất khuyến khích bạn tự làm bài trước khi đọc lời giải trên mạng.

#### Phép đếm

**1.** Có bao nhiêu cách sắp xếp các chữ cái trong từ `MISSISSIPPI`?

**2.** (a) Có bao nhiêu số điện thoại gồm 7 chữ số, nếu chữ số đầu không được là 0 hoặc 1? (b) Giải lại (a), nhưng thêm điều kiện số điện thoại không được bắt đầu bằng 911 (đây là số khẩn cấp, và hệ thống không nên phải chờ xem liệu người gọi còn bấm thêm chữ số nào sau 911 hay không).

**3.** Fred dự định ăn tối bên ngoài từ thứ Hai đến thứ Sáu trong một tuần, mỗi tối tại một trong mười nhà hàng yêu thích của mình. (a) Có bao nhiêu lịch ăn tối nếu Fred không muốn đến cùng một nhà hàng quá một lần? (b) Có bao nhiêu lịch nếu Fred chấp nhận đến lại một nhà hàng, nhưng không muốn ăn ở cùng một nơi hai tối liên tiếp (hoặc nhiều hơn)?

**4.** Một giải quần vợt vòng tròn có $n$ người chơi: mỗi người đấu với mọi người khác đúng một lần. (a) Giải có bao nhiêu kết quả tổng thể có thể xảy ra (một kết quả liệt kê người thắng và thua trong từng trận)? (b) Tổng cộng có bao nhiêu trận?

**5.** Một giải quần vợt loại trực tiếp có $2^n$ người chơi. Sau mỗi vòng, người thắng vào vòng sau và người thua bị loại, cho đến khi chỉ còn một người. Chẳng hạn, nếu ban đầu có $2^4=16$ người, vòng đầu có 8 trận; 8 người thắng vào vòng hai; 4 người thắng vào vòng ba; 2 người thắng vào vòng bốn; người thắng vòng bốn là nhà vô địch. (Có nhiều cách quyết định ai gặp ai trong mỗi vòng, nhưng điều đó không ảnh hưởng đến bài này.) (a) Có bao nhiêu vòng? (b) Tính tổng số trận bằng cách cộng số trận ở từng vòng. (c) Tính lại tổng số trận bằng suy luận trực tiếp, gần như không cần phép tính. *Gợi ý:* Cần loại bao nhiêu người?

**6.** Một ngày nọ có 20 người ở câu lạc bộ cờ vua. Họ tìm đối thủ rồi bắt đầu chơi. Có bao nhiêu cách ghép cặp, nếu trong mỗi ván việc ai cầm quân trắng là quan trọng (một người cầm trắng, người kia cầm đen)?

**7.** Hai người chơi cờ, $A$ và $B$, sẽ đấu 7 ván. Mỗi ván có ba kết quả: $A$ thắng ($B$ thua), hòa, hoặc $A$ thua ($B$ thắng). Thắng được 1 điểm, hòa được 0,5 điểm, thua được 0 điểm. (a) Có bao nhiêu chuỗi kết quả từng ván để cuối cùng $A$ có 3 thắng, 2 hòa và 2 thua? (b) Có bao nhiêu chuỗi kết quả từng ván để $A$ được 4 điểm và $B$ được 3 điểm? (c) Giờ giả sử họ đấu theo thể thức tối đa 7 ván, trận đấu kết thúc ngay khi một người đạt 4 điểm. Chẳng hạn, nếu sau 6 ván $A$ dẫn 4–2, $A$ thắng trận và họ không đấu ván thứ bảy. Có bao nhiêu chuỗi kết quả từng ván để trận đấu kéo dài đủ 7 ván và $A$ thắng chung cuộc 4–3?

**8.** (a) Có bao nhiêu cách chia 12 người thành 3 đội, trong đó một đội có 2 người và hai đội còn lại mỗi đội 5 người? (b) Có bao nhiêu cách chia 12 người thành 3 đội, mỗi đội 4 người?

**9.** (a) Có bao nhiêu đường đi từ $(0,0)$ đến $(110,111)$ trên mặt phẳng, nếu mỗi bước chỉ được đi lên một đơn vị hoặc sang phải một đơn vị? (b) Có bao nhiêu đường đi từ $(0,0)$ đến $(210,211)$ với cùng quy tắc, nếu đường đi buộc phải qua $(110,111)$?

**10.** Để đủ điều kiện nhận một bằng cấp, sinh viên được chọn học 7 trong số 20 môn, với điều kiện ít nhất một trong 7 môn phải là môn thống kê. Giả sử có 5 môn thống kê trong danh sách 20 môn. (a) Có bao nhiêu cách chọn 7 môn? (b) Hãy giải thích bằng trực giác vì sao đáp án của (a) không phải là $\binom51\binom{19}{6}$.

**11.** Cho hai tập hợp $A,B$ với $|A|=n$, $|B|=m$. (a) Có bao nhiêu hàm từ $A$ đến $B$ (tức hàm có miền xác định là $A$, gán cho mỗi phần tử của $A$ một phần tử của $B$)? (b) Có bao nhiêu hàm một–một từ $A$ đến $B$ (xem mục A.2.1 của phụ lục toán học để biết về hàm một–một)?

**12.** Bốn người chơi $A,B,C,D$ tham gia một trò chơi bài. Chia hết bộ bài chuẩn 52 lá đã xáo kỹ cho họ (mỗi người nhận 13 lá). (a) Có bao nhiêu tay bài mà $A$ có thể nhận? Thứ tự nhận bài trong một tay không quan trọng. (b) Có bao nhiêu cách chia tay bài cho tất cả người chơi, nếu phân biệt người nào nhận tay bài nào nhưng không xét thứ tự các lá trong từng tay? (c) Hãy giải thích bằng trực giác vì sao đáp án (b) không phải lũy thừa bậc bốn của đáp án (a).

**13.** Một sòng bạc trộn 10 bộ bài chuẩn thành một bộ lớn, gọi là *siêu bộ bài*. Vậy siêu bộ bài có $52\cdot10=520$ lá, gồm 10 bản sao của mỗi lá. Có bao nhiêu tay bài 10 lá khác nhau có thể chia từ đó? Không xét thứ tự các lá, cũng không quan tâm lá thuộc bộ gốc nào trong 10 bộ. Hãy biểu diễn đáp án bằng một hệ số nhị thức. *Gợi ý:* Bose–Einstein.

**14.** Bạn gọi hai chiếc pizza. Mỗi chiếc có thể cỡ nhỏ, vừa, lớn hoặc cực lớn, với bất kỳ tổ hợp nào của 8 loại nhân thêm (có thể không chọn loại nào hoặc chọn cả 8). Có bao nhiêu khả năng cho hai chiếc pizza?

#### Chứng minh bằng câu chuyện

**15.** Hãy dùng một câu chuyện để chứng minh $\sum_{k=0}^{n}\binom nk=2^n$.

**16.** Với mọi số nguyên dương $n,k$ thỏa $n\ge k$, hãy chứng minh

$$\binom nk+\binom n{k-1}=\binom{n+1}{k}$$

bằng hai cách: (a) đại số; (b) một câu chuyện giải thích vì sao hai vế đếm cùng một đối tượng. *Gợi ý cho cách chứng minh bằng câu chuyện:* Hình dung $n+1$ người, trong đó một người được chỉ định trước là “chủ tịch”.

**17.** Với mọi số nguyên dương $n$, hãy dùng câu chuyện để chứng minh

$$\sum_{k=1}^{n}k\binom nk^2=n\binom{2n-1}{n-1}.$$

*Gợi ý:* Chọn một ủy ban gồm $n$ người từ hai nhóm, mỗi nhóm có $n$ người; chỉ thành viên của một trong hai nhóm đủ điều kiện làm chủ tịch.

**18.** (a) Với số nguyên dương $n,k$ thỏa $n\ge k$, hãy dùng câu chuyện để chứng minh

$$\binom kk+\binom{k+1}{k}+\binom{k+2}{k}+\cdots+\binom nk=\binom{n+1}{k+1}.$$

Đây là *đồng nhất thức gậy khúc côn cầu*. *Gợi ý:* Hãy tưởng tượng sắp xếp một nhóm người theo tuổi, rồi xét người nhiều tuổi nhất trong một nhóm con được chọn.

(b) Giả sử một gói lớn kẹo dẻo hình gấu Haribo có từ 30 đến 50 viên. Có 5 vị ngon: dứa (trong suốt), mâm xôi (đỏ), cam (cam), dâu tây (xanh lá, thật khó hiểu) và chanh (vàng). Không có vị nào dở. Có bao nhiêu thành phần kẹo khác nhau mà gói đó có thể có? Có thể để đáp án dưới dạng một vài hệ số nhị thức, nhưng không được là một tổng dài các hệ số nhị thức.

**19.** Định nghĩa $\left\{\!\begin{smallmatrix}n\\k\end{smallmatrix}\!\right\}$ là số cách chia $\{1,2,\ldots,n\}$ thành $k$ tập con không rỗng, hoặc số cách chia $n$ sinh viên thành $k$ nhóm, mỗi nhóm có ít nhất một người. Chẳng hạn, $\left\{\!\begin{smallmatrix}4\\2\end{smallmatrix}\!\right\}=7$ vì có các cách:

- $\{1\},\{2,3,4\}$; $\{2\},\{1,3,4\}$; $\{3\},\{1,2,4\}$; $\{4\},\{1,2,3\}$;
- $\{1,2\},\{3,4\}$; $\{1,3\},\{2,4\}$; $\{1,4\},\{2,3\}$.

Hãy chứng minh các đồng nhất thức sau:

(a) $\left\{\!\begin{smallmatrix}n+1\\k\end{smallmatrix}\!\right\}=\left\{\!\begin{smallmatrix}n\\k-1\end{smallmatrix}\!\right\}+k\left\{\!\begin{smallmatrix}n\\k\end{smallmatrix}\!\right\}$. *Gợi ý:* Hoặc tôi ở một nhóm một mình, hoặc không.

(b) $\sum_{j=k}^{n}\binom nj\left\{\!\begin{smallmatrix}j\\k\end{smallmatrix}\!\right\}=\left\{\!\begin{smallmatrix}n+1\\k+1\end{smallmatrix}\!\right\}$. *Gợi ý:* Trước hết chọn số người không ở cùng nhóm với tôi.

**20.** Nhà toán học Hà Lan R. J. Stroeker nhận xét rằng mọi người mới học lý thuyết số hẳn đều từng kinh ngạc trước sự thật như phép màu: với mỗi số tự nhiên $n$, tổng lập phương của $n$ số nguyên dương liên tiếp đầu tiên là một số chính phương [29]. Hơn nữa, đó chính là bình phương của tổng $n$ số nguyên dương đầu tiên:

$$1^3+2^3+\cdots+n^3=(1+2+\cdots+n)^2.$$

Đồng nhất thức này thường được chứng minh bằng quy nạp, nhưng cách đó ít cho thấy vì sao kết quả đúng, và cũng không giúp nhiều nếu ta muốn tính vế trái mà chưa biết sẵn kết quả. Trong bài này, bạn sẽ chứng minh bằng câu chuyện.

(a) Hãy chứng minh bằng câu chuyện rằng $1+2+\cdots+n=\binom{n+1}{2}$. *Gợi ý:* Xét một giải đấu vòng tròn (xem Bài 4).

(b) Hãy chứng minh bằng câu chuyện rằng

$$1^3+2^3+\cdots+n^3=6\binom{n+1}{4}+6\binom{n+1}{3}+\binom{n+1}{2}.$$

Sau đó chỉ cần đại số cơ bản (bài này không yêu cầu) để kiểm tra bình phương của vế phải ở (a) bằng vế phải ở (b). *Gợi ý:* Hãy tưởng tượng chọn một số từ 1 đến $n$, rồi chọn có hoàn lại 3 số từ 0 đến $n$ nhỏ hơn số ban đầu. Sau đó xét các trường hợp dựa trên số lượng giá trị phân biệt đã chọn.

#### Định nghĩa xác suất sơ khai

**21.** Ba người bước vào thang máy trống ở tầng một của một tòa nhà 10 tầng. Mỗi người bấm nút tầng muốn đến (trừ khi người khác đã bấm nút đó). Giả sử mỗi người có khả năng muốn đến một trong các tầng từ 2 đến 10 như nhau, độc lập với nhau. Xác suất các nút của 3 tầng liên tiếp được bấm là bao nhiêu?

**22.** Một gia đình có 6 con, gồm 3 trai và 3 gái. Giả sử mọi thứ tự sinh đều có khả năng như nhau. Xác suất 3 người con lớn nhất đều là con gái là bao nhiêu?

**23.** Một thành phố có 6 quận xảy ra 6 vụ cướp trong một tuần. Giả sử các vụ cướp phân bố ngẫu nhiên và mọi khả năng về vị trí xảy ra từng vụ đều như nhau. Xác suất có một quận xảy ra hơn một vụ cướp là bao nhiêu?

**24.** Một cuộc khảo sát được thực hiện tại thành phố có một triệu cư dân. Khảo sát toàn bộ là quá tốn kém, nên người ta chọn ngẫu nhiên một mẫu 1.000 người. (Trong thực tế, việc lấy mẫu gặp nhiều khó khăn, như lập danh sách đầy đủ cư dân và xử lý người từ chối tham gia.) Cuộc khảo sát chọn từng người một, có hoàn lại và với xác suất như nhau. (a) Giải thích việc lấy mẫu có hoàn lại và không hoàn lại ở đây liên hệ thế nào với bài toán ngày sinh. (b) Tính xác suất có ít nhất một người được chọn hơn một lần.

**25.** *Bảng băm* là một cấu trúc dữ liệu phổ biến trong khoa học máy tính, cho phép truy xuất thông tin nhanh. Chẳng hạn, ta muốn lưu số điện thoại của một số người và giả sử không ai trùng tên. Với mỗi tên $x$, hàm băm $h$ cho biết vị trí $h(x)$ dùng để lưu số điện thoại của người ấy. Sau khi lập bảng, để tra số của $x$, ta chỉ cần tính lại $h(x)$ rồi xem dữ liệu tại vị trí đó.

Hàm băm $h$ là tất định, vì ta không muốn mỗi lần tính $h(x)$ lại được một kết quả khác. Nhưng $h$ thường được chọn theo cách giả ngẫu nhiên. Trong bài này, giả sử dùng tính ngẫu nhiên thực sự. Có $k$ người; số điện thoại mỗi người được lưu tại một vị trí ngẫu nhiên, biểu diễn bằng một số nguyên từ 1 đến $n$. Mọi vị trí có xác suất như nhau, độc lập với vị trí lưu số của người khác. Hãy tìm xác suất ít nhất một vị trí lưu nhiều hơn một số điện thoại.

**26.** Một trường đại học có 10 khung giờ học không chồng nhau và vô tư xếp các môn vào khung giờ một cách ngẫu nhiên, độc lập. Một sinh viên chọn ngẫu nhiên 3 môn để đăng ký. Xác suất lịch học của sinh viên bị trùng giờ là bao nhiêu?

**27.** Với mỗi ý, điền dấu $=$, $<$ hoặc $>$ vào chỗ trống và giải thích rõ. (a) $P(\text{tổng khi gieo 4 xúc xắc cân đối bằng 21})\;\_\;P(\text{tổng bằng 22})$. (b) $P(\text{một từ ngẫu nhiên dài 2 chữ cái là từ đối xứng})\;\_\;P(\text{một từ ngẫu nhiên dài 3 chữ cái là từ đối xứng})$.

*Chú thích:* Từ đối xứng là chuỗi đọc xuôi và ngược giống nhau, nếu bỏ qua khoảng trắng, chữ hoa và dấu câu; chẳng hạn câu tiếng Anh “A man, a plan, a canal: Panama”. Với bài này, giả sử mọi từ có độ dài đã cho đều có khả năng như nhau, không có khoảng trắng hoặc dấu câu, và bảng chữ cái gồm 26 chữ thường `a,b,...,z`.

**28.** Với định nghĩa như Bài 27, hãy tìm xác suất một từ ngẫu nhiên là từ đối xứng khi độ dài từ là $n=7$ và $n=8$.

**29.** Nai sừng tấm sống trong một khu rừng. Có $N$ con; người ta bắt và đánh dấu một mẫu ngẫu nhiên đơn gồm $n$ con (“mẫu ngẫu nhiên đơn” nghĩa là mọi tập con gồm $n$ con trong $\binom Nn$ tập đều có khả năng như nhau). Sau đó thả chúng lại quần thể và bắt một mẫu mới gồm $m$ con. Đây là phương pháp *bắt–đánh dấu–bắt lại*, được dùng rộng rãi trong sinh thái học. Xác suất đúng $k$ trong $m$ con ở mẫu mới đã được đánh dấu trước đó là bao nhiêu? (Giả sử việc từng bị bắt không làm một con nai dễ hay khó bị bắt lại hơn.)

**30.** Bốn lá bài được đặt úp trên bàn. Bạn được cho biết có hai lá đỏ và hai lá đen; bạn cần đoán lá nào đỏ, lá nào đen. Bạn chỉ vào hai lá mà mình đoán là đỏ (đồng nghĩa đoán hai lá còn lại là đen). Giả sử mọi cách sắp xếp màu đều có khả năng như nhau và bạn không có năng lực ngoại cảm. Hãy tìm xác suất đúng chính xác $j$ lá, với $j=0,1,2,3,4$.

**31.** Một chiếc lọ chứa $r$ quả bóng đỏ và $g$ quả bóng xanh, trong đó $r,g$ là các số nguyên dương cố định. Rút ngẫu nhiên một quả bóng (mọi khả năng như nhau), rồi rút ngẫu nhiên quả thứ hai.

(a) Giải thích bằng trực giác vì sao xác suất quả thứ hai màu xanh bằng xác suất quả thứ nhất màu xanh.

(b) Đặt ký hiệu cho không gian mẫu của bài toán; dùng nó để tính hai xác suất trong (a) và chỉ ra chúng bằng nhau.

(c) Giả sử tổng cộng có 16 quả bóng, và xác suất hai quả cùng màu bằng xác suất hai quả khác màu. $r$ và $g$ bằng bao nhiêu? Hãy liệt kê mọi khả năng.

**32.** Chia ngẫu nhiên một tay poker 5 lá từ bộ bài chuẩn. Hãy tìm xác suất của từng trường hợp sau, dưới dạng hệ số nhị thức. (a) *Thùng*: cả 5 lá cùng chất; không tính *thùng phá sảnh lớn* gồm át, già, đầm, bồi và 10 cùng chất. (b) *Hai đôi*, chẳng hạn hai lá 3, hai lá 7 và một lá át.

**33.** Chia ngẫu nhiên một tay 13 lá từ bộ bài chuẩn. Xác suất tay bài có ít nhất 3 lá của *mỗi* chất là bao nhiêu?

**34.** Gieo đồng thời 30 con xúc xắc. Xác suất mỗi mặt 1, 2, 3, 4, 5, 6 xuất hiện đúng 5 lần là bao nhiêu?

**35.** Xáo kỹ một bộ bài rồi chia từng lá cho đến khi xuất hiện lá át đầu tiên. (a) Tính xác suất không có lá già, đầm hay bồi nào xuất hiện trước lá át đầu tiên. (b) Tính xác suất trước lá át đầu tiên xuất hiện đúng một lá già, một lá đầm và một lá bồi, theo thứ tự bất kỳ.

**36.** Tyrion, Cersei và mười người khác được xếp chỗ ngẫu nhiên quanh bàn tròn. Xác suất Tyrion và Cersei ngồi cạnh nhau là bao nhiêu? Hãy giải theo hai cách: (a) dùng không gian mẫu kích thước $12!$, trong đó mỗi kết quả mô tả đầy đủ chỗ ngồi; (b) dùng một không gian mẫu nhỏ hơn nhiều, chỉ tập trung vào Tyrion và Cersei.

**37.** Một tổ chức có $2n$ người, gồm $n$ cặp vợ chồng. Chọn ngẫu nhiên một ủy ban $k$ người, mọi khả năng như nhau. Tìm xác suất có đúng $j$ cặp vợ chồng trong ủy ban.

**38.** Có $n$ quả bóng trong lọ, mang nhãn $1,2,\ldots,n$. Rút tổng cộng $k$ quả, từng quả một và có hoàn lại, thu được một dãy số. (a) Xác suất dãy thu được *tăng nghiêm ngặt* là bao nhiêu? (b) Xác suất dãy *tăng* là bao nhiêu? (Trong sách này, “tăng” có nghĩa là *không giảm*.)

**39.** Đặt độc lập mỗi quả trong $n$ quả bóng vào một trong $n$ chiếc hộp, mọi hộp có khả năng như nhau. Xác suất đúng một hộp trống là bao nhiêu?

**40.** Một *từ không lặp* là dãy gồm ít nhất một chữ cái (có thể dùng cả 26 chữ) trong bảng chữ cái `a,b,c,...,z`, không cho phép lặp lại. Chẳng hạn, `course` là một từ không lặp, còn `statistics` thì không. Thứ tự quan trọng: `course` khác `source`. Chọn ngẫu nhiên một từ không lặp, mọi từ như vậy đều có khả năng như nhau. Hãy chứng minh xác suất từ ấy sử dụng đủ 26 chữ cái rất gần $1/e$.

#### Các tiên đề xác suất

**41.** Hãy chứng minh với mọi biến cố $A,B$ rằng

$$P(A)+P(B)-1\le P(A\cap B)\le P(A\cup B)\le P(A)+P(B).$$

Với mỗi bất đẳng thức trong ba bất đẳng thức trên, hãy đưa ra một điều kiện đơn giản để nó trở thành đẳng thức (chẳng hạn một điều kiện đơn giản tương đương với $P(A\cap B)=P(A\cup B)$).

**42.** Cho hai biến cố $A,B$. Hiệu $B-A$ được định nghĩa là tập hợp tất cả các phần tử thuộc $B$ nhưng không thuộc $A$. Hãy dùng trực tiếp các tiên đề xác suất để chứng minh: nếu $A\subseteq B$ thì $P(B-A)=P(B)-P(A)$.

**43.** Cho hai biến cố $A,B$. *Hiệu đối xứng* $A\triangle B$ là tập hợp các phần tử thuộc $A$ hoặc $B$, nhưng không thuộc cả hai. Trong logic và kỹ thuật, biến cố này còn gọi là XOR (*hoặc loại trừ*). Hãy dùng trực tiếp các tiên đề xác suất để chứng minh $P(A\triangle B)=P(A)+P(B)-2P(A\cap B)$.

**44.** Cho các biến cố $A_1,A_2,\ldots,A_n$. Gọi $B_k$ là biến cố có ít nhất $k$ trong các $A_i$ xảy ra, còn $C_k$ là biến cố có đúng $k$ trong các $A_i$ xảy ra, với $0\le k\le n$. Hãy tìm biểu thức đơn giản của $P(B_k)$ theo $P(C_k)$ và $P(C_{k+1})$.

**45.** Hai biến cố $A,B$ độc lập nếu $P(A\cap B)=P(A)P(B)$ (tính độc lập sẽ được khảo sát kỹ trong chương sau).

(a) Hãy nêu một ví dụ về hai biến cố độc lập $A,B$ trong một không gian mẫu hữu hạn $S$ (không biến cố nào bằng $\varnothing$ hoặc $S$), và minh họa bằng sơ đồ Thế giới Sỏi.

(b) Xét phép thử chọn ngẫu nhiên một điểm trong hình chữ nhật $R=\{(x,y):0<x<1,\;0<y<1\}$; xác suất điểm nằm trong một miền con bất kỳ của $R$ bằng diện tích miền đó. Cho $A_1,B_1$ là hai hình chữ nhật nằm trong $R$, có diện tích khác 0 và 1. Gọi $A$ là biến cố điểm được chọn thuộc $A_1$, và $B$ là biến cố điểm được chọn thuộc $B_1$. Hãy mô tả về mặt hình học điều kiện để $A,B$ độc lập. Đồng thời, hãy nêu một ví dụ chúng độc lập và một ví dụ chúng không độc lập.

(c) Hãy chứng minh rằng nếu $A,B$ độc lập thì $P(A\cup B)=P(A)+P(B)-P(A)P(B)=1-P(A^c)P(B^c)$.

**46.** Arby có một hệ thống niềm tin, gán số $P_{\text{Arby}}(A)$ từ 0 đến 1 cho mỗi biến cố $A$ (trên một không gian mẫu nào đó). Con số này biểu thị mức độ Arby tin rằng $A$ sẽ xảy ra. Với mọi biến cố $A$, Arby sẵn lòng trả $1000P_{\text{Arby}}(A)$ đô la để mua một chứng chỉ như sau:

> **Chứng chỉ:** Người sở hữu được đổi chứng chỉ lấy 1.000 đô la nếu $A$ xảy ra. Nếu $A$ không xảy ra, chứng chỉ không có giá trị, trừ những gì luật liên bang, tiểu bang hoặc địa phương yêu cầu. Không có ngày hết hạn.

Tương tự, Arby sẵn lòng *bán* chứng chỉ đó với cùng mức giá. Thực tế, Arby sẵn lòng mua hoặc bán bao nhiêu chứng chỉ tùy ý ở giá này, vì cho rằng đó là giá “công bằng”.

Arby nhất quyết không chấp nhận các tiên đề xác suất. Cụ thể, giả sử có hai biến cố rời nhau $A,B$ sao cho $P_{\text{Arby}}(A\cup B)\ne P_{\text{Arby}}(A)+P_{\text{Arby}}(B)$. Hãy chỉ ra cách khiến Arby phá sản: đưa ra một danh sách giao dịch mà Arby sẵn lòng thực hiện nhưng chắc chắn khiến Arby mất tiền. (Có thể giả sử ngày sau khi mua hoặc bán chứng chỉ, người ta sẽ biết $A$ và $B$ có xảy ra hay không.)

#### Bao hàm–loại trừ

**47.** Gieo một con xúc xắc cân đối $n$ lần. Xác suất có ít nhất một trong sáu mặt không xuất hiện lần nào là bao nhiêu?

**48.** Một người chơi được chia tay bài 13 lá từ bộ bài chuẩn đã xáo kỹ. Xác suất tay bài không có lá nào thuộc ít nhất một chất là bao nhiêu?

**49.** Trong một nhóm 7 người, hãy tìm xác suất cả bốn mùa (đông, xuân, hạ, thu) đều có ít nhất một người sinh vào mùa đó, giả sử bốn mùa có khả năng như nhau.

**50.** Một lớp có 20 sinh viên, học vào thứ Hai và thứ Tư trong phòng có đúng 20 chỗ ngồi. Một tuần nọ, cả lớp đều đi học đủ hai buổi. Mỗi buổi, sinh viên chọn chỗ hoàn toàn ngẫu nhiên (mỗi ghế một người). Hãy tìm xác suất không ai ngồi cùng chỗ trong cả hai buổi của tuần đó.

**51.** Fred cần đặt mật khẩu cho một trang web. Giả sử mật khẩu gồm 8 ký tự; các ký tự hợp lệ là chữ thường `a,b,...,z`, chữ hoa `A,B,...,Z` và chữ số `0,1,...,9`. Có bao nhiêu khả năng nếu: (a) mật khẩu phải có ít nhất một chữ thường; (b) phải có ít nhất một chữ thường và một chữ hoa; (c) phải có ít nhất một chữ thường, một chữ hoa và một chữ số?

**52.** Alice học ở một trường nhỏ mà mỗi môn chỉ có một buổi học mỗi tuần. Cô đang chọn giữa 30 môn không trùng giờ. Từ thứ Hai đến thứ Sáu, mỗi ngày có 6 môn để chọn. Tin vào sự ưu ái của ngẫu nhiên, Alice đăng ký ngẫu nhiên 7 trong 30 môn, mọi cách chọn có khả năng như nhau. Xác suất cô có lớp học vào *mọi* ngày từ thứ Hai đến thứ Sáu là bao nhiêu? (Có thể giải trực tiếp bằng định nghĩa sơ khai hoặc dùng bao hàm–loại trừ.)

**53.** Một câu lạc bộ gồm 10 sinh viên năm cuối, 12 sinh viên năm ba và 15 sinh viên năm hai. Chọn ngẫu nhiên ban tổ chức 5 người, mọi tập con gồm 5 người đều có khả năng như nhau. (a) Tính xác suất ban tổ chức có đúng 3 sinh viên năm hai. (b) Tính xác suất ban tổ chức có ít nhất một đại diện từ mỗi khóa năm cuối, năm ba và năm hai.

#### Bài tập tổng hợp

**54.** Với mỗi ý, điền dấu $=$, $<$ hoặc $>$ vào chỗ trống và giải thích rõ. Ở (a) và (b), thứ tự không quan trọng.

(a) (Số cách chọn 5 người trong 10 người) $\;\_\;$ (số cách chọn 6 người trong 10 người).

(b) (Số cách chia 10 người thành hai đội, mỗi đội 5 người) $\;\_\;$ (số cách chia 10 người thành một đội 6 người và một đội 4 người).

(c) (Xác suất cả 3 người trong nhóm đều sinh ngày 1 tháng 1) $\;\_\;$ (xác suất trong nhóm 3 người, mỗi người sinh vào một trong các ngày 1, 2 và 3 tháng 1, mỗi ngày đúng một người).

Martin và Gale chơi trò tung đồng xu cân đối cho đến khi xuất hiện mẫu HH (hai lần ngửa liên tiếp) hoặc TH (sấp rồi ngay sau đó ngửa). Martin thắng khi và chỉ khi HH xuất hiện trước TH.

(d) (Xác suất Martin thắng) $\;\_\;$ $1/2$.

**55.** Hãy hít một hơi thật sâu trước khi làm bài này. Trong cuốn *Innumeracy* [22], John Allen Paulos viết:

> Giờ là một tin vui về một dạng tồn tại bền bỉ gần như bất tử. Trước hết, hãy hít một hơi sâu. Giả sử ghi chép của Shakespeare chính xác và Julius Caesar đã thốt lên “Cả ngươi nữa sao, Brutus!” trước hơi thở cuối cùng. Xác suất bạn vừa hít vào một phân tử mà Caesar đã thở ra trong hơi thở ấy là bao nhiêu?

Giả sử một hơi thở chứa $10^{22}$ phân tử, và khí quyển chứa $10^{44}$ phân tử. (Những số này đơn giản hơn một chút so với ước tính Paulos dùng; trong bài này hãy coi chúng là chính xác. Dĩ nhiên thực tế còn nhiều phức tạp, như các loại phân tử khác nhau trong khí quyển, phản ứng hóa học, dung tích phổi khác nhau, v.v.)

Giả sử các phân tử trong khí quyển ngày nay chính là các phân tử có trong khí quyển thời Caesar còn sống, và trong khoảng 2.000 năm kể từ đó, chúng đã phân tán hoàn toàn ngẫu nhiên khắp khí quyển. Bạn cũng có thể giả định việc lấy mẫu bằng hít thở là *có hoàn lại* (lấy mẫu không hoàn lại hợp lý hơn, nhưng lấy mẫu có hoàn lại dễ tính và xấp xỉ rất tốt, vì số phân tử trong khí quyển lớn hơn số phân tử trong một hơi thở rất nhiều).

Hãy tìm xác suất trong hơi thở bạn vừa hít có ít nhất một phân tử cũng từng nằm trong hơi thở cuối cùng của Caesar, và cho một giá trị xấp xỉ đơn giản theo $e$.

**56.** Một nhân viên kiểm định kiểm tra 12 sản phẩm và thấy đúng 3 sản phẩm bị lỗi. Không may, các sản phẩm sau đó bị trộn lẫn, nên nhân viên phải tìm lại 3 sản phẩm lỗi bằng cách kiểm tra từng chiếc. (a) Tính xác suất nhân viên bây giờ phải kiểm tra ít nhất 9 sản phẩm. (b) Tính xác suất phải kiểm tra ít nhất 10 sản phẩm.

**57.** Có 15 thanh sô cô la và 10 trẻ em. Có bao nhiêu cách chia sô cô la cho các em trong từng trường hợp sau?

(a) Các thanh sô cô la có thể thay thế cho nhau (không phân biệt từng thanh).

(b) Các thanh có thể thay thế cho nhau, và mỗi em phải nhận ít nhất một thanh. *Gợi ý:* Trước hết cho mỗi em một thanh, rồi quyết định cách chia phần còn lại.

(c) Các thanh không thể thay thế cho nhau (phân biệt thanh nào đến tay ai).

(d) Các thanh không thể thay thế cho nhau, và mỗi em phải nhận ít nhất một thanh. *Gợi ý:* Chiến lược ở (b) không áp dụng được. Thay vào đó, hãy hình dung chia ngẫu nhiên các thanh cho các em rồi dùng bao hàm–loại trừ.

**58.** Cho $n\ge2$ số $(a_1,a_2,\ldots,a_n)$ không trùng nhau. Một *mẫu bootstrap* là dãy $(x_1,x_2,\ldots,x_n)$ được tạo bằng cách lấy mẫu có hoàn lại từ các $a_j$, với xác suất như nhau. Mẫu bootstrap xuất hiện trong một phương pháp thống kê phổ biến cùng tên. Chẳng hạn, nếu $n=2$ và $(a_1,a_2)=(3,1)$, các mẫu bootstrap có thể có là $(3,3)$, $(3,1)$, $(1,3)$ và $(1,1)$.

(a) Có bao nhiêu mẫu bootstrap có thể có từ $(a_1,\ldots,a_n)$?

(b) Có bao nhiêu mẫu bootstrap có thể có nếu không xét thứ tự (chỉ quan tâm mỗi $a_j$ được chọn bao nhiêu lần, không quan tâm thứ tự chọn)?

(c) Chọn ngẫu nhiên một mẫu bootstrap bằng cách lấy mẫu có hoàn lại như trên. Hãy chỉ ra rằng không phải mọi mẫu bootstrap *không xét thứ tự* ở (b) đều có xác suất như nhau. Tìm một mẫu không xét thứ tự $b_1$ có khả năng cao nhất và một mẫu $b_2$ có khả năng thấp nhất. Gọi $p_1$ là xác suất thu được *mẫu cụ thể* $b_1$, và $p_2$ là xác suất thu được *mẫu cụ thể* $b_2$. Tỉ số $p_1/p_2$ bằng bao nhiêu? Tỉ số giữa xác suất nhận được *một mẫu không xét thứ tự bất kỳ* có xác suất $p_1$ và xác suất nhận được *một mẫu không xét thứ tự bất kỳ* có xác suất $p_2$ bằng bao nhiêu?

**59.** Có 100 hành khách xếp hàng lên một máy bay 100 ghế (mỗi ghế được chỉ định cho một hành khách). Người đầu tiên bất chợt chọn ngồi một ghế ngẫu nhiên, mọi ghế có khả năng như nhau. Mỗi người tiếp theo ngồi đúng ghế của mình nếu ghế còn trống; nếu không, người đó chọn ngẫu nhiên một ghế trống. Xác suất hành khách cuối cùng được ngồi đúng ghế của mình là bao nhiêu? (Đây là một bài phỏng vấn quen thuộc và là ví dụ đẹp về sức mạnh của tính đối xứng.)

*Gợi ý:* Gọi ghế chỉ định cho hành khách thứ $j$ trong hàng là “ghế $j$” (bất kể hãng bay gọi nó là 23A hay tên khác). Những ghế nào có thể còn trống khi hành khách cuối cùng lên máy bay, và xác suất của từng khả năng là bao nhiêu?

**60.** Trong bài toán ngày sinh, ta đã giả sử 365 ngày trong năm có khả năng như nhau (bỏ qua ngày 29 tháng 2). Thực tế, một số ngày có xác suất sinh cao hơn đôi chút. Chẳng hạn, các nhà khoa học từ lâu đã cố lý giải vì sao số em bé sinh ra vào thời điểm chín tháng sau một kỳ nghỉ lễ lại nhiều hơn. Gọi $\mathbf p=(p_1,p_2,\ldots,p_{365})$ là vectơ xác suất ngày sinh, trong đó $p_j$ là xác suất sinh vào ngày thứ $j$ của năm (vẫn bỏ qua ngày 29 tháng 2, hoàn toàn không có ý xúc phạm người sinh ngày nhuận).

*Đa thức đối xứng sơ cấp bậc $k$* theo các biến $x_1,\ldots,x_n$ được định nghĩa là

$$e_k(x_1,\ldots,x_n)=\sum_{1\le j_1<j_2<\cdots<j_k\le n}x_{j_1}\cdots x_{j_k}.$$

Nói cách khác, lấy tổng của $\binom nk$ tích có thể tạo bằng cách chọn $k$ biến. Chẳng hạn, $e_1(x_1,x_2,x_3)=x_1+x_2+x_3$, $e_2(x_1,x_2,x_3)=x_1x_2+x_1x_3+x_2x_3$, và $e_3(x_1,x_2,x_3)=x_1x_2x_3$. Bây giờ gọi $k\ge2$ là số người.

(a) Hãy tìm biểu thức đơn giản cho xác suất có ít nhất một cặp trùng ngày sinh theo $\mathbf p$ và một đa thức đối xứng sơ cấp.

(b) Hãy xét các trường hợp đơn giản và cực hạn để giải thích bằng trực giác vì sao xác suất có ít nhất một cặp trùng ngày sinh nhỏ nhất khi $p_j=1/365$ với mọi $j$.

(c) Bất đẳng thức nổi tiếng giữa trung bình cộng và trung bình nhân phát biểu rằng với $x,y\ge0$,

$$\frac{x+y}{2}\ge\sqrt{xy}.$$

Bất đẳng thức này suy ra từ $(x-y)^2=x^2-2xy+y^2\ge0$ khi cộng $4xy$ vào hai vế. Định nghĩa $\mathbf r=(r_1,\ldots,r_{365})$ bởi $r_1=r_2=(p_1+p_2)/2$ và $r_j=p_j$ với $3\le j\le365$. Dùng bất đẳng thức trung bình cộng–trung bình nhân và hệ thức sau (bạn nên tự kiểm tra):

$$e_k(x_1,\ldots,x_n)=x_1x_2e_{k-2}(x_3,\ldots,x_n)+(x_1+x_2)e_{k-1}(x_3,\ldots,x_n)+e_k(x_3,\ldots,x_n),$$

hãy chứng minh

$$P(\text{ít nhất một cặp trùng ngày sinh}\mid\mathbf p)\ge P(\text{ít nhất một cặp trùng ngày sinh}\mid\mathbf r),$$

với bất đẳng thức nghiêm ngặt nếu $\mathbf p\ne\mathbf r$. Ký hiệu “cho trước $\mathbf r$” nghĩa là xác suất sinh theo từng ngày được xác định bởi $\mathbf r$. Từ đó, hãy chứng minh vectơ $\mathbf p$ làm xác suất có ít nhất một cặp trùng ngày sinh nhỏ nhất là $p_j=1/365$ với mọi $j$.

## Chương 2. Xác suất có điều kiện (từ trang PDF 59)

Chúng ta đã giới thiệu xác suất như một ngôn ngữ để diễn đạt mức độ tin tưởng hoặc sự bất định của mình đối với các biến cố. Mỗi khi quan sát được bằng chứng mới (tức thu thập dữ liệu), ta có thêm thông tin có thể làm thay đổi sự bất định ấy. Một quan sát phù hợp với niềm tin trước đó có thể khiến ta tin chắc hơn; một quan sát bất ngờ có thể khiến ta phải xem xét lại niềm tin đó. *Xác suất có điều kiện* giải quyết câu hỏi nền tảng này: ta nên cập nhật niềm tin như thế nào trước các bằng chứng quan sát được?

### 2.1. Tầm quan trọng của tư duy có điều kiện

Xác suất có điều kiện thiết yếu trong suy luận khoa học, y học và pháp lý vì nó cho thấy cách đưa bằng chứng vào sự hiểu biết về thế giới một cách hợp logic và nhất quán. Thực ra, một góc nhìn hữu ích là *mọi xác suất đều có điều kiện*: dù có được viết tường minh hay không, mỗi xác suất luôn dựa trên một số hiểu biết hoặc giả định nền.

Chẳng hạn, một buổi sáng ta quan tâm đến biến cố $R$: hôm nay trời mưa. Gọi $P(R)$ là đánh giá xác suất mưa trước khi nhìn ra ngoài. Nếu sau đó ta nhìn ra và thấy mây đen đáng ngại, xác suất mưa có lẽ nên tăng lên. Ta ký hiệu xác suất mới là $P(R\mid C)$, đọc là “xác suất của $R$ khi biết $C$”, với $C$ là biến cố có mây đen đáng ngại. Khi chuyển từ $P(R)$ sang $P(R\mid C)$, ta nói mình *đặt điều kiện theo $C$*. Trong ngày, ta có thể biết thêm ngày càng nhiều thông tin về thời tiết và liên tục cập nhật các xác suất. Nếu quan sát thấy $B_1,\ldots,B_n$ xảy ra, ta viết xác suất mưa mới theo các bằng chứng đó là $P(R\mid B_1,\ldots,B_n)$. Nếu cuối cùng quan sát thấy trời bắt đầu mưa, xác suất có điều kiện của ta trở thành 1.

Hơn nữa, đặt điều kiện là một chiến lược giải quyết vấn đề rất mạnh: nó thường giúp giải bài toán phức tạp bằng cách tách thành các phần có thể xử lý theo từng trường hợp. Giống như trong khoa học máy tính, người ta thường chia một vấn đề lớn thành những phần nhỏ, trong xác suất ta thường chuyển một bài toán khó thành nhiều bài toán xác suất có điều kiện đơn giản hơn. Đặc biệt, ta sẽ bàn về chiến lược *phân tích bước đầu*, thường cho phép tìm lời giải đệ quy cho phép thử gồm nhiều giai đoạn.

Vì đặt điều kiện có vai trò trung tâm, vừa là cách cập nhật niềm tin theo bằng chứng, vừa là chiến lược giải bài toán, chúng tôi nói rằng:

> Đặt điều kiện là linh hồn của thống kê.

### 2.2. Định nghĩa và trực giác

**Định nghĩa 2.2.1 (Xác suất có điều kiện).** Nếu $A,B$ là các biến cố với $P(B)>0$, thì *xác suất có điều kiện của $A$ khi biết $B$*, ký hiệu $P(A\mid B)$, được định nghĩa là

$$P(A\mid B)=\frac{P(A\cap B)}{P(B)}.$$

Ở đây, $A$ là biến cố mà ta muốn cập nhật mức độ bất định, còn $B$ là bằng chứng ta quan sát được (hoặc muốn coi là đã biết). Ta gọi $P(A)$ là *xác suất tiên nghiệm* của $A$, còn $P(A\mid B)$ là *xác suất hậu nghiệm*; “tiên nghiệm” là trước khi cập nhật theo bằng chứng, “hậu nghiệm” là sau khi cập nhật.

Cần hiểu biến cố đứng sau dấu gạch đứng là bằng chứng được quan sát hoặc được dùng làm điều kiện: $P(A\mid B)$ là xác suất của $A$ *khi biết bằng chứng $B$*, chứ không phải xác suất của một thứ gọi là “$A\mid B$”. Như Cảnh báo 2.4.1 sẽ bàn, không tồn tại biến cố mang tên $A\mid B$.

Với một biến cố $A$ có $P(A)>0$, ta có $P(A\mid A)=P(A\cap A)/P(A)=1$. Khi đã quan sát thấy $A$ xảy ra, xác suất cập nhật của $A$ bằng 1. Nếu không như vậy, ta hẳn phải đòi một định nghĩa mới cho xác suất có điều kiện!

**Ví dụ 2.2.2 (Hai lá bài).** Xáo kỹ một bộ bài chuẩn rồi rút ngẫu nhiên hai lá, từng lá một và không hoàn lại. Gọi $A$ là biến cố lá đầu tiên là lá cơ, còn $B$ là biến cố lá thứ hai màu đỏ. Tìm $P(A\mid B)$ và $P(B\mid A)$.

**Lời giải.** Theo định nghĩa xác suất sơ khai và quy tắc nhân,

$$P(A\cap B)=\frac{13\cdot25}{52\cdot51}=\frac{25}{204},$$

vì để có kết quả thuận lợi, ta chọn một trong 13 lá cơ trước, rồi chọn một trong 25 lá đỏ còn lại. Ngoài ra, $P(A)=1/4$ vì bốn chất có khả năng như nhau; và

$$P(B)=\frac{26\cdot51}{52\cdot51}=\frac12,$$

vì có 26 cách chọn lá thứ hai thuận lợi, và với mỗi cách, lá đầu tiên có thể là bất kỳ lá nào khác. Nhớ lại từ Chương 1 rằng quy tắc nhân không đòi hỏi ta phải xét theo thứ tự thời gian. Một cách gọn hơn để thấy $P(B)=1/2$ là dùng tính đối xứng: trước khi thực hiện phép thử, lá thứ hai có khả năng là bất kỳ lá nào trong bộ bài như nhau. Bây giờ ta đã có mọi thành phần để áp dụng định nghĩa:

$$P(A\mid B)=\frac{25/204}{1/2}=\frac{25}{102},\qquad P(B\mid A)=\frac{25/204}{1/4}=\frac{25}{51}.$$

Đây là ví dụ đơn giản, nhưng đã có vài điều đáng lưu ý.

1. Phải hết sức cẩn thận xem đặt biến cố nào ở phía nào của dấu điều kiện. Cụ thể, $P(A\mid B)\ne P(B\mid A)$. Mục tiếp theo khảo sát mối liên hệ tổng quát giữa hai đại lượng này. Nhầm lẫn chúng được gọi là *ngụy biện của công tố viên* và sẽ được bàn ở mục 2.8. Nếu ta định nghĩa $B$ là biến cố lá thứ hai cũng là lá cơ thì hai xác suất có điều kiện sẽ bằng nhau.
2. Cả $P(A\mid B)$ và $P(B\mid A)$ đều có nghĩa, cả về trực giác lẫn toán học; thứ tự thời gian rút bài không quyết định ta được xét xác suất có điều kiện nào. Khi tính xác suất có điều kiện, ta xem việc quan sát một biến cố cung cấp thông tin gì về biến cố khác, chứ không hỏi biến cố này có gây ra biến cố kia hay không.
3. Cũng có thể hiểu trực tiếp vì sao $P(B\mid A)=25/51$: nếu lá đầu là lá cơ, bộ bài còn 25 lá đỏ và 26 lá đen, tất cả đều có khả năng được rút tiếp như nhau. Vậy xác suất có điều kiện rút lá đỏ là $25/(25+26)=25/51$. Tìm $P(A\mid B)$ trực tiếp theo cách này khó hơn: nếu biết lá thứ hai đỏ, ta có thể nghĩ “biết vậy cũng tốt, nhưng điều ta thật sự muốn biết là liệu nó có phải lá cơ không!”. Những kết quả ở phần sau của chương sẽ giúp ta vượt qua khó khăn này.

Để hiểu thêm ý nghĩa của xác suất có điều kiện, dưới đây là hai cách diễn giải bằng trực giác.

**Trực giác 2.2.3 (Thế giới Sỏi).** Xét một không gian mẫu hữu hạn, hình dung mỗi kết quả là một viên sỏi và tổng khối lượng bằng 1. Vì $A$ là biến cố, nó là một tập hợp các viên sỏi; $B$ cũng vậy. Hình 2.1(a) cho một ví dụ.

Giả sử giờ ta biết $B$ đã xảy ra. Ở Hình 2.1(b), sau khi có thông tin này, ta bỏ mọi viên sỏi thuộc $B^c$ vì chúng không phù hợp với điều đã biết. Khi ấy, $P(A\cap B)$ là tổng khối lượng các viên còn lại thuộc $A$. Cuối cùng, ở Hình 2.1(c), ta *chuẩn hóa lại*: chia mọi khối lượng cho cùng một hằng số để tổng khối lượng mới của các viên còn lại vẫn bằng 1. Cụ thể, ta chia cho $P(B)$, tổng khối lượng các viên thuộc $B$. Khối lượng mới của các kết quả ứng với $A$ chính là $P(A\mid B)=P(A\cap B)/P(B)$.

**Hình 2.1.** Trực giác Thế giới Sỏi về $P(A\mid B)$. Từ trái sang phải: (a) $A$ và $B$ là các tập con của không gian mẫu; (b) vì biết $B$ xảy ra, loại bỏ kết quả thuộc $B^c$; (c) trong không gian mẫu thu hẹp, chuẩn hóa lại để tổng khối lượng vẫn là 1.

Như vậy, các xác suất đã được cập nhật theo bằng chứng quan sát. Các kết quả mâu thuẫn với bằng chứng bị loại bỏ, và khối lượng của chúng được phân phối lại cho những kết quả còn lại, trong khi tỉ lệ khối lượng giữa những kết quả còn lại được giữ nguyên. Chẳng hạn, nếu ban đầu viên sỏi 2 nặng gấp đôi viên 1, và cả hai cùng thuộc $B$, thì sau khi đặt điều kiện theo $B$, viên 2 vẫn nặng gấp đôi viên 1. Nhưng nếu viên 2 không thuộc $B$, khối lượng cập nhật của nó là 0.

**Trực giác 2.2.4 (Cách hiểu theo tần suất).** Nhớ lại rằng cách hiểu tần suất dựa trên tần suất tương đối khi lặp lại một phép thử rất nhiều lần. Hãy hình dung ta thực hiện phép thử lặp đi lặp lại và thu được một danh sách dài các kết quả quan sát. Khi đó, xác suất có điều kiện của $A$ khi biết $B$ có thể được hiểu tự nhiên là tỉ lệ các lần $A$ xảy ra *trong số những lần $B$ xảy ra*. Ở Hình 2.2, mỗi kết quả là một chuỗi gồm 0 và 1; $B$ là biến cố chữ số đầu tiên bằng 1, còn $A$ là biến cố chữ số thứ hai bằng 1. Đặt điều kiện theo $B$, ta khoanh tất cả những lần $B$ xảy ra, rồi xét trong số các lần được khoanh có bao nhiêu phần $A$ cũng xảy ra.

Ký hiệu $n_A,n_B,n_{AB}$ lần lượt là số lần $A,B,A\cap B$ xảy ra trong tổng cộng $n$ lần lặp phép thử, với $n$ rất lớn. Theo cách hiểu tần suất,

$$P(A)\approx\frac{n_A}{n},\qquad P(B)\approx\frac{n_B}{n},\qquad P(A\cap B)\approx\frac{n_{AB}}{n}.$$

Vậy $P(A\mid B)$ được hiểu là $n_{AB}/n_B$, bằng $(n_{AB}/n)/(n_B/n)$. Cách hiểu này một lần nữa dẫn đến $P(A\mid B)=P(A\cap B)/P(B)$.

**Hình 2.2.** Trực giác tần suất về $P(A\mid B)$. Những lần $B$ xảy ra được khoanh; trong đó, những lần $A$ cũng xảy ra được in đậm. $P(A\mid B)$ là tần suất tương đối dài hạn của những lần $A$ xảy ra trong tập con các lần $B$ xảy ra.

Để luyện tập áp dụng định nghĩa xác suất có điều kiện, hãy xét thêm vài ví dụ. Ba ví dụ tiếp theo đều bắt đầu từ một gia đình có hai con, nhưng cách xác định chính xác thông tin được dùng làm điều kiện sẽ tạo ra những khác biệt tinh tế.

**Ví dụ 2.2.5 (Con lớn là gái hay có ít nhất một con gái).** Một gia đình có hai con, và ta biết ít nhất một người là con gái. Theo thông tin đó, xác suất cả hai đều là con gái là bao nhiêu? Nếu thay vào đó biết người con lớn là gái thì sao?

**Lời giải.** Giả sử mỗi đứa trẻ có xác suất là trai hoặc gái như nhau, độc lập với nhau.¹ Khi ấy,

$$P(\text{cả hai là gái}\mid\text{ít nhất một là gái})=\frac{P(\text{cả hai là gái và có ít nhất một con gái})}{P(\text{ít nhất một là gái})}=\frac{1/4}{3/4}=\frac13,$$

$$P(\text{cả hai là gái}\mid\text{con lớn là gái})=\frac{P(\text{cả hai là gái và con lớn là gái})}{P(\text{con lớn là gái})}=\frac{1/4}{1/2}=\frac12.$$

Thoạt đầu, việc hai kết quả khác nhau có thể gây ngạc nhiên: ta đâu có lý do gì để quan tâm người con lớn là gái hơn người con nhỏ. Đúng là nhờ tính đối xứng,

$$P(\text{cả hai là gái}\mid\text{con nhỏ là gái})=P(\text{cả hai là gái}\mid\text{con lớn là gái})=\frac12.$$

Tuy nhiên, không có tính đối xứng tương tự giữa các xác suất có điều kiện khi biết *cụ thể một người con* là gái và khi chỉ biết *ít nhất một người con* là gái.

¹ Mục 2.5 sẽ định nghĩa chính thức tính độc lập; hiện tại, ta có thể hiểu bằng trực giác: biết giới tính của người con lớn không cung cấp thông tin về giới tính của người con nhỏ, và ngược lại. Để đơn giản, ta thường giả sử xác suất một trẻ sinh ra là con trai bằng $1/2$, dù $0{,}51$ sát thực tế hơn ở phần lớn quốc gia (số bé trai sinh ra mỗi năm hơi nhiều hơn bé gái; điều này được bù lại phần nào vì trung bình phụ nữ sống lâu hơn nam giới). Xem Matthews [20] về tỉ lệ trẻ trai và trẻ gái sinh ra ở Hoa Kỳ.

Nói rằng con lớn là gái tức là chỉ định một đứa trẻ cụ thể; khi ấy, đứa trẻ còn lại (con nhỏ) có 50% khả năng là gái. Cụm “ít nhất một” không chỉ một đứa trẻ cụ thể. Nếu biết một người con cụ thể là gái, ta loại được 2 trong 4 “viên sỏi” của không gian mẫu $\{GG,GB,BG,BB\}$; nếu chỉ biết ít nhất một người là gái, ta chỉ loại $BB$.

**Ví dụ 2.2.6 (Một đứa trẻ được gặp ngẫu nhiên là gái).** Một gia đình có hai con. Bạn tình cờ gặp ngẫu nhiên một trong hai người và thấy đó là con gái. Theo thông tin này, xác suất cả hai đều là con gái là bao nhiêu? Giả sử khả năng gặp mỗi đứa trẻ như nhau, và việc gặp ai không liên quan đến giới tính.

**Lời giải.** Theo trực giác, đáp án là $1/2$: hãy hình dung đứa trẻ bạn gặp đứng trước mặt, còn người kia ở nhà. “Cả hai đều là gái” lúc này chỉ cần đứa trẻ ở nhà là gái, dường như không liên quan đến việc đứa trẻ trước mặt là gái. Nhưng hãy kiểm tra cẩn thận bằng định nghĩa xác suất có điều kiện. Đây cũng là cơ hội luyện tập viết biến cố bằng ký hiệu tập hợp.

Gọi $G_1,G_2,G_3$ lần lượt là biến cố con lớn, con nhỏ và đứa trẻ được gặp ngẫu nhiên là gái. Nhờ tính đối xứng, $P(G_1)=P(G_2)=P(G_3)=1/2$ (ta ngầm giả định khi không có thông tin khác, mỗi đứa trẻ cụ thể đều có khả năng là trai hoặc gái như nhau). Theo định nghĩa xác suất sơ khai, hoặc theo tính độc lập sẽ được giải thích ở mục 2.5, $P(G_1\cap G_2)=1/4$. Do đó,

$$P(G_1\cap G_2\mid G_3)=\frac{P(G_1\cap G_2\cap G_3)}{P(G_3)}=\frac{1/4}{1/2}=\frac12,$$

vì $G_1\cap G_2\cap G_3=G_1\cap G_2$: nếu cả hai con đều là gái thì đứa trẻ gặp ngẫu nhiên chắc chắn là gái. Vậy xác suất cả hai đều là gái bằng $1/2$, phù hợp với trực giác.

Tuy vậy, cần nhớ rằng để có đáp án $1/2$, ta đã phải giả định cách chọn đứa trẻ được gặp. Theo ngôn ngữ thống kê, ta đã thu thập một *mẫu ngẫu nhiên*; ở đây mẫu là một trong hai đứa trẻ. Một nguyên tắc quan trọng bậc nhất của thống kê là phải xem xét kỹ mẫu được thu thập như thế nào, thay vì chỉ nhìn dữ liệu thô mà không hiểu nguồn gốc của chúng. Xét trường hợp cực đoan: giả sử có một đạo luật hà khắc cấm con trai ra khỏi nhà nếu có chị hoặc em gái. Khi ấy, “đứa trẻ được gặp ngẫu nhiên là gái” tương đương với “ít nhất một trong hai con là gái”, nên bài toán quay về phần đầu của Ví dụ 2.2.5.

**Ví dụ 2.2.7 (Con gái sinh vào mùa đông).** Một gia đình có hai con. Hãy tìm xác suất cả hai là gái, biết rằng ít nhất một người là gái sinh vào mùa đông. Giả sử bốn mùa có xác suất như nhau và giới tính độc lập với mùa sinh (tức biết giới tính không cung cấp thông tin về xác suất các mùa, và ngược lại; xem mục 2.5 để tìm hiểu kỹ hơn).

**Lời giải.** Theo định nghĩa xác suất có điều kiện,

$$P(\text{cả hai là gái}\mid\text{ít nhất một gái sinh mùa đông})=\frac{P(\text{cả hai là gái, ít nhất một gái sinh mùa đông})}{P(\text{ít nhất một gái sinh mùa đông})}.$$

Vì xác suất một đứa trẻ cụ thể là gái sinh mùa đông bằng $1/8$, mẫu số là $P(\text{ít nhất một gái sinh mùa đông})=1-(7/8)^2$.

Để tính tử số, hãy dùng sự kiện “cả hai là gái, ít nhất một gái sinh mùa đông” tương đương với “cả hai là gái, ít nhất một đứa trẻ sinh mùa đông”; rồi dùng giả định giới tính độc lập với mùa sinh:

$$\begin{aligned}P(\text{cả hai là gái, ít nhất một gái sinh mùa đông})&=P(\text{cả hai là gái, ít nhất một trẻ sinh mùa đông})\\&=\frac14P(\text{ít nhất một trẻ sinh mùa đông})\\&=\frac14\bigl(1-P(\text{cả hai không sinh mùa đông})\bigr)\\&=\frac14\bigl(1-(3/4)^2\bigr).\end{aligned}$$

Kết hợp lại,

$$P(\text{cả hai là gái}\mid\text{ít nhất một gái sinh mùa đông})=\frac{(1/4)(1-(3/4)^2)}{1-(7/8)^2}=\frac{7/64}{15/64}=\frac7{15}.$$

Thoạt nhìn kết quả này có vẻ vô lý! Ở Ví dụ 2.2.5, xác suất cả hai đều là gái khi biết ít nhất một người là gái bằng $1/3$; tại sao biết thêm có một bé gái sinh mùa đông lại khác? Điểm mấu chốt là thông tin mùa sinh khiến “ít nhất một người là gái” gần hơn với “một người con cụ thể là gái”. Đặt điều kiện theo thông tin càng cụ thể, xác suất càng tiến gần $1/2$.

Chẳng hạn, nếu biết “ít nhất một người là gái, sinh vào ngày 31 tháng 3 lúc 8 giờ 20 tối”, thì gần như đã chỉ rõ một đứa trẻ. Thông tin về một người con cụ thể không cung cấp thông tin về người còn lại. Thông tin tưởng như không liên quan, chẳng hạn mùa sinh, tạo ra các trường hợp trung gian giữa hai phần của Ví dụ 2.2.5. Bài tập 29 khái quát ví dụ này cho một đặc điểm bất kỳ độc lập với giới tính.

### 2.3. Quy tắc Bayes và định luật xác suất toàn phần

Định nghĩa xác suất có điều kiện rất đơn giản — chỉ là tỉ số của hai xác suất — nhưng hệ quả rất sâu rộng. Hệ quả đầu tiên dễ có được khi chuyển mẫu số của định nghĩa sang vế bên kia.

**Định lý 2.3.1.** Với mọi biến cố $A,B$ có xác suất dương,

$$P(A\cap B)=P(B)P(A\mid B)=P(A)P(B\mid A).$$

Để có kết quả này, ta chỉ cần lấy định nghĩa của $P(A\mid B)$ rồi nhân hai vế với $P(B)$; sau đó lấy định nghĩa của $P(B\mid A)$ rồi nhân hai vế với $P(A)$. Thoạt nhìn định lý dường như không mấy hữu ích: nó chỉ là định nghĩa xác suất có điều kiện viết theo cách khác. Hơn nữa, dùng $P(A\mid B)$ để tìm $P(A\cap B)$ có vẻ vòng quanh, vì $P(A\mid B)$ vốn được định nghĩa thông qua $P(A\cap B)$. Nhưng ta sẽ thấy định lý thực ra rất hữu ích: nhiều khi có thể tìm xác suất có điều kiện mà không cần quay lại định nghĩa; trong những trường hợp ấy, Định lý 2.3.1 giúp ta tìm $P(A\cap B)$ dễ hơn.

Áp dụng Định lý 2.3.1 lặp đi lặp lại, ta khái quát cho giao của $n$ biến cố.

**Định lý 2.3.2.** Với các biến cố $A_1,\ldots,A_n$ có xác suất dương,

$$P(A_1,A_2,\ldots,A_n)=P(A_1)P(A_2\mid A_1)P(A_3\mid A_1,A_2)\cdots P(A_n\mid A_1,\ldots,A_{n-1}).$$

Dấu phẩy biểu thị phép giao. Thật ra, đây là $n!$ định lý gộp làm một: ta có thể hoán vị $A_1,\ldots,A_n$ theo bất kỳ cách nào mà không đổi vế trái. Với một số thứ tự, vế phải thường dễ tính hơn nhiều so với thứ tự khác. Chẳng hạn,

$$P(A_1,A_2,A_3)=P(A_1)P(A_2\mid A_1)P(A_3\mid A_1,A_2)=P(A_2)P(A_3\mid A_2)P(A_1\mid A_2,A_3),$$

và còn bốn cách khai triển dạng này nữa. Biết nên dùng thứ tự nào thường đòi hỏi luyện tập và suy nghĩ.

Giờ ta sẵn sàng giới thiệu hai định lý chính của chương: *quy tắc Bayes* và *định luật xác suất toàn phần*. Chúng cho phép tính xác suất có điều kiện trong rất nhiều bài toán. Quy tắc Bayes là một kết quả cực kỳ nổi tiếng và hữu ích, liên hệ $P(A\mid B)$ với $P(B\mid A)$.

**Định lý 2.3.3 (Quy tắc Bayes).**

$$P(A\mid B)=\frac{P(B\mid A)P(A)}{P(B)}.$$

Quy tắc này suy ra ngay từ Định lý 2.3.1, mà định lý ấy lại suy ra ngay từ định nghĩa xác suất có điều kiện. Tuy nhiên, quy tắc Bayes có ý nghĩa và ứng dụng quan trọng trong xác suất và thống kê: ta rất thường cần tìm xác suất có điều kiện, và nhiều khi $P(B\mid A)$ dễ tìm trực tiếp hơn $P(A\mid B)$, hoặc ngược lại.

Một cách viết khác của quy tắc Bayes sử dụng *tỉ lệ cược* thay cho xác suất.

**Định nghĩa 2.3.4 (Tỉ lệ cược).** *Tỉ lệ cược* của biến cố $A$ là

$$\operatorname{odds}(A)=\frac{P(A)}{P(A^c)}.$$

Chẳng hạn, nếu $P(A)=2/3$, ta nói tỉ lệ cược *ủng hộ* $A$ là 2 so với 1. Đôi khi viết là $2:1$, hoặc nói tỉ lệ cược *chống lại* $A$ là 1 so với 2. Cần thận trọng vì một số nguồn không nêu rõ họ đang nói đến tỉ lệ ủng hộ hay chống lại biến cố. Dĩ nhiên, ta cũng có thể đổi từ tỉ lệ cược về xác suất: $P(A)=\operatorname{odds}(A)/(1+\operatorname{odds}(A))$.

Lấy biểu thức Bayes cho $P(A\mid B)$ chia cho biểu thức Bayes cho $P(A^c\mid B)$, ta được dạng tỉ lệ cược của quy tắc Bayes.

**Định lý 2.3.5 (Quy tắc Bayes ở dạng tỉ lệ cược).** Với các biến cố $A,B$ có xác suất dương, tỉ lệ cược của $A$ sau khi đặt điều kiện theo $B$ là

$$\frac{P(A\mid B)}{P(A^c\mid B)}=\frac{P(B\mid A)}{P(B\mid A^c)}\frac{P(A)}{P(A^c)}.$$

Nói bằng lời, tỉ lệ cược hậu nghiệm $P(A\mid B)/P(A^c\mid B)$ bằng tỉ lệ cược tiên nghiệm $P(A)/P(A^c)$ nhân với $P(B\mid A)/P(B\mid A^c)$, được gọi trong thống kê là *tỉ số khả năng*. Đôi khi làm việc với dạng này của quy tắc Bayes để tìm tỉ lệ cược hậu nghiệm sẽ thuận tiện hơn; sau đó, nếu muốn, ta có thể đổi từ tỉ lệ cược về xác suất.

*Định luật xác suất toàn phần* (LOTP) liên hệ xác suất có điều kiện với xác suất không điều kiện. Nó là công cụ thiết yếu để thực hiện ý tưởng dùng xác suất có điều kiện chia bài toán phức tạp thành những phần đơn giản hơn; nó thường được dùng cùng quy tắc Bayes.

**Định lý 2.3.6 (Định luật xác suất toàn phần).** Cho $A_1,\ldots,A_n$ là một phân hoạch của không gian mẫu $S$ (tức các $A_i$ rời nhau và hợp của chúng là $S$), với $P(A_i)>0$ cho mọi $i$. Khi ấy,

$$P(B)=\sum_{i=1}^{n}P(B\mid A_i)P(A_i).$$

**Chứng minh.** Vì $A_i$ tạo thành một phân hoạch của $S$, ta có thể phân rã $B$ thành $B=(B\cap A_1)\cup(B\cap A_2)\cup\cdots\cup(B\cap A_n)$. Hình 2.3 minh họa việc chia $B$ thành các phần nhỏ hơn $B\cap A_1,\ldots,B\cap A_n$. Vì các phần này rời nhau, tiên đề xác suất thứ hai cho phép cộng xác suất của chúng: $P(B)=P(B\cap A_1)+\cdots+P(B\cap A_n)$. Áp dụng Định lý 2.3.1 cho từng $P(B\cap A_i)$, ta được $P(B)=P(B\mid A_1)P(A_1)+\cdots+P(B\mid A_n)P(A_n)$.

**Hình 2.3.** Các biến cố $A_i$ phân hoạch không gian mẫu; $P(B)$ bằng $\sum_iP(B\cap A_i)$.

Định luật xác suất toàn phần nói rằng để có xác suất không điều kiện của $B$, ta có thể chia không gian mẫu thành các phần rời nhau $A_i$, tìm xác suất có điều kiện của $B$ trong từng phần, rồi lấy tổng có trọng số, với trọng số là $P(A_i)$. Cách chọn phân hoạch rất quan trọng: phân hoạch tốt biến một bài toán khó thành những phần dễ hơn; phân hoạch tệ chỉ làm tình hình tồi thêm, bắt ta tính $n$ xác suất khó thay vì một!

Các ví dụ tiếp theo cho thấy cách dùng quy tắc Bayes cùng định luật xác suất toàn phần để cập nhật niềm tin từ bằng chứng quan sát được.

**Ví dụ 2.3.7 (Đồng xu được chọn ngẫu nhiên).** Bạn có một đồng xu cân đối và một đồng xu lệch có xác suất ra mặt ngửa bằng $3/4$. Bạn chọn ngẫu nhiên một đồng xu rồi tung ba lần. Cả ba lần đều ra mặt ngửa. Theo thông tin này, xác suất bạn đã chọn đồng xu cân đối là bao nhiêu?

**Lời giải.** Gọi $A$ là biến cố đồng xu được chọn ra mặt ngửa cả ba lần và $F$ là biến cố ta chọn đồng xu cân đối. Ta cần $P(F\mid A)$, nhưng $P(A\mid F)$ và $P(A\mid F^c)$ dễ tìm hơn vì biết đang dùng đồng xu nào sẽ hữu ích. Điều này gợi ý dùng quy tắc Bayes và định luật xác suất toàn phần:

$$\begin{aligned}P(F\mid A)&=\frac{P(A\mid F)P(F)}{P(A)}\\&=\frac{P(A\mid F)P(F)}{P(A\mid F)P(F)+P(A\mid F^c)P(F^c)}\\&=\frac{(1/2)^3(1/2)}{(1/2)^3(1/2)+(3/4)^3(1/2)}\approx0{,}23.\end{aligned}$$

Trước khi tung, ta cho rằng khả năng chọn đồng xu cân đối và đồng xu lệch như nhau: $P(F)=P(F^c)=1/2$. Nhưng sau khi quan sát ba lần ngửa, việc ta đã chọn đồng xu lệch trở nên có khả năng hơn, nên $P(F\mid A)$ chỉ khoảng $0{,}23$.

**Cảnh báo 2.3.8 (Tiên nghiệm và hậu nghiệm).** Khi tính ở ví dụ trên, sẽ sai nếu ngay sau bước đầu ta nói “$P(A)=1$ vì đã biết $A$ xảy ra”. Đúng là $P(A\mid A)=1$, nhưng $P(A)$ là xác suất *tiên nghiệm* của $A$, còn $P(F)$ là xác suất *tiên nghiệm* của $F$: cả hai đều là xác suất trước khi ta quan sát dữ liệu của phép thử. Không được nhầm chúng với xác suất hậu nghiệm có điều kiện theo bằng chứng $A$.

**Ví dụ 2.3.9 (Xét nghiệm bệnh hiếm).** Một bệnh nhân tên Fred được xét nghiệm bệnh *conditionitis*, một tình trạng chỉ ảnh hưởng 1% dân số. Kết quả dương tính, tức xét nghiệm cho rằng Fred mắc bệnh. Gọi $D$ là biến cố Fred mắc bệnh, $T$ là biến cố xét nghiệm dương tính.

Giả sử xét nghiệm “chính xác 95%”. Có nhiều cách đo độ chính xác, nhưng trong bài này cụm đó có nghĩa $P(T\mid D)=0{,}95$ và $P(T^c\mid D^c)=0{,}95$. Đại lượng $P(T\mid D)$ được gọi là *độ nhạy* hay *tỉ lệ dương tính thật*; $P(T^c\mid D^c)$ là *độ đặc hiệu* hay *tỉ lệ âm tính thật*. Hãy tìm xác suất Fred mắc bệnh khi đã biết kết quả xét nghiệm.

**Lời giải.** Dùng quy tắc Bayes và định luật xác suất toàn phần:

$$\begin{aligned}P(D\mid T)&=\frac{P(T\mid D)P(D)}{P(T)}\\&=\frac{P(T\mid D)P(D)}{P(T\mid D)P(D)+P(T\mid D^c)P(D^c)}\\&=\frac{0{,}95\cdot0{,}01}{0{,}95\cdot0{,}01+0{,}05\cdot0{,}99}\approx0{,}16.\end{aligned}$$

Vậy Fred chỉ có khoảng 16% khả năng mắc bệnh khi đã xét nghiệm dương tính, dù xét nghiệm có vẻ khá đáng tin cậy!

Nhiều người, kể cả bác sĩ, thấy bất ngờ khi xác suất mắc bệnh sau một kết quả dương tính chỉ là 16%, trong khi xét nghiệm chính xác 95% (xem Gigerenzer và Hoffrage [14]). Để hiểu xác suất hậu nghiệm này, cần nhận ra có hai yếu tố cùng tác động: bằng chứng từ xét nghiệm và thông tin tiên nghiệm về tỉ lệ mắc bệnh. Xét nghiệm cung cấp bằng chứng ủng hộ việc Fred mắc bệnh, nhưng *conditionitis* cũng là bệnh hiếm! Xác suất có điều kiện $P(D\mid T)$ cân bằng hai yếu tố ấy, cân nhắc đúng mức độ hiếm của bệnh so với độ hiếm của kết quả xét nghiệm sai.

Để có thêm trực giác, xét một quần thể 10.000 người như Hình 2.4: 100 người mắc bệnh và 9.900 người không mắc, tương ứng tỉ lệ mắc bệnh 1%. Nếu xét nghiệm toàn bộ, ta kỳ vọng trong 100 người bệnh có 95 người dương tính và 5 người âm tính. Trong 9.900 người khỏe mạnh, ta kỳ vọng $(0{,}95)(9900)=9405$ người âm tính và 495 người dương tính.

**Hình 2.4.** Xét nghiệm bệnh hiếm trong quần thể 10.000 người, tỉ lệ mắc bệnh 1%, độ nhạy và độ đặc hiệu đều bằng 95%. Kích thước các hình trong sơ đồ không theo tỉ lệ thực.

Bây giờ hãy tập trung vào những người có kết quả dương tính, tức đặt điều kiện theo kết quả dương tính. Số người dương tính thật là 95 (vừa dương tính vừa có bệnh), ít hơn rất nhiều so với 495 người dương tính giả (dương tính nhưng không có bệnh). Vậy phần lớn người xét nghiệm dương tính thực ra không mắc bệnh!

### 2.4. Xác suất có điều kiện cũng là xác suất

Khi đặt điều kiện theo biến cố $E$, ta cập nhật niềm tin để phù hợp với điều đã biết, như thể bước vào một thế giới mà ta biết chắc $E$ đã xảy ra. Tuy nhiên, trong thế giới mới ấy, các quy luật xác suất vẫn hoạt động như trước. Xác suất có điều kiện thỏa *mọi* tính chất của xác suất! Vì vậy, mọi kết quả ta đã chứng minh về xác suất vẫn đúng nếu thay tất cả xác suất không điều kiện bằng xác suất có điều kiện theo $E$. Cụ thể:

- Xác suất có điều kiện nằm trong khoảng từ 0 đến 1.
- $P(S\mid E)=1$ và $P(\varnothing\mid E)=0$.
- Nếu $A_1,A_2,\ldots$ rời nhau, thì $P(\bigcup_{j=1}^{\infty}A_j\mid E)=\sum_{j=1}^{\infty}P(A_j\mid E)$.
- $P(A^c\mid E)=1-P(A\mid E)$.
- Bao hàm–loại trừ: $P(A\cup B\mid E)=P(A\mid E)+P(B\mid E)-P(A\cap B\mid E)$.

**Cảnh báo 2.4.1.** Khi viết $P(A\mid E)$, không có nghĩa $A\mid E$ là một biến cố rồi ta lấy xác suất của nó; $A\mid E$ *không* phải biến cố. Đúng hơn, $P(\cdot\mid E)$ là một hàm xác suất gán xác suất theo hiểu biết rằng $E$ đã xảy ra; còn $P(\cdot)$ là một hàm xác suất khác, gán xác suất mà chưa xét $E$ có xảy ra hay không. Đưa biến cố $A$ vào hàm $P(\cdot)$, ta được số $P(A)$; đưa $A$ vào hàm $P(\cdot\mid E)$, ta được số khác là $P(A\mid E)$, đã tính đến thông tin từ $E$ (nếu có).

Để chứng minh về mặt toán học rằng xác suất có điều kiện là xác suất, hãy cố định biến cố $E$ với $P(E)>0$, rồi định nghĩa $\widetilde P(A)=P(A\mid E)$ cho mọi biến cố $A$. Ký hiệu này nhấn mạnh rằng ta cố định $E$ và xem $P(\cdot\mid E)$ là hàm xác suất “mới”. Ta chỉ cần kiểm tra hai tiên đề. Thứ nhất,

$$\widetilde P(\varnothing)=P(\varnothing\mid E)=\frac{P(\varnothing\cap E)}{P(E)}=0,\qquad \widetilde P(S)=P(S\mid E)=\frac{P(S\cap E)}{P(E)}=1.$$

Thứ hai, nếu $A_1,A_2,\ldots$ là các biến cố rời nhau, thì

$$\begin{aligned}\widetilde P(A_1\cup A_2\cup\cdots)&=\frac{P((A_1\cap E)\cup(A_2\cap E)\cup\cdots)}{P(E)}\\&=\frac{\sum_{j=1}^{\infty}P(A_j\cap E)}{P(E)}=\sum_{j=1}^{\infty}\widetilde P(A_j).\end{aligned}$$

Vậy $\widetilde P$ thỏa các tiên đề xác suất.

Ngược lại, có thể xem *mọi* xác suất đều là xác suất có điều kiện: khi nói về một xác suất, ta luôn đặt điều kiện theo một thông tin nền nào đó, dù không nêu rõ. Xét ví dụ trời mưa ở đầu chương. Ta có thể dựa vào tỉ lệ những ngày mưa trong quá khứ để đưa ra xác suất ban đầu hôm nay trời mưa, $P(R)$. Nhưng nên xét những ngày nào? Nếu hôm nay là ngày 1 tháng 11, có nên chỉ đếm ngày mưa trong các mùa thu trước đó, tức đặt điều kiện theo mùa? Hay nên đặt điều kiện theo đúng tháng, thậm chí đúng ngày? Địa điểm cũng vậy: ta nên xét số ngày mưa đúng nơi mình ở, hay mưa ở đâu đó gần đây là đủ? Để xác định một xác suất có vẻ không điều kiện như $P(R)$, thực ra ta phải quyết định nên dựa vào những thông tin nền nào! Những lựa chọn ấy cần suy nghĩ cẩn thận. Người khác nhau có thể đưa ra xác suất “tiên nghiệm” $P(R)$ khác nhau (dù mọi người đều có thể thống nhất cách cập nhật theo bằng chứng mới).

Vì mọi xác suất đều có điều kiện theo thông tin nền, ta có thể hình dung luôn có một dấu gạch điều kiện, với tri thức nền $K$ ở bên phải. Khi ấy, xác suất không điều kiện $P(A)$ chỉ là cách viết ngắn của $P(A\mid K)$: tri thức nền được gói vào chữ $P$ thay vì viết rõ.

Tóm lại:

> Xác suất có điều kiện là xác suất, và mọi xác suất đều có điều kiện.

Giờ ta phát biểu các dạng có thêm điều kiện của quy tắc Bayes và định luật xác suất toàn phần. Chỉ cần lấy dạng thông thường rồi thêm $E$ vào phía bên phải dấu gạch điều kiện ở mọi chỗ.

**Định lý 2.4.2 (Quy tắc Bayes với điều kiện bổ sung).** Nếu $P(A\cap E)>0$ và $P(B\cap E)>0$ thì

$$P(A\mid B,E)=\frac{P(B\mid A,E)P(A\mid E)}{P(B\mid E)}.$$

**Định lý 2.4.3 (Định luật xác suất toàn phần với điều kiện bổ sung).** Cho $A_1,\ldots,A_n$ là một phân hoạch của $S$. Nếu $P(A_i\cap E)>0$ với mọi $i$, thì

$$P(B\mid E)=\sum_{i=1}^{n}P(B\mid A_i,E)P(A_i\mid E).$$

Có thể chứng minh hai dạng có thêm điều kiện này tương tự như cách ta kiểm tra $\widetilde P$ thỏa các tiên đề xác suất. Chúng cũng suy ra trực tiếp từ “siêu định lý”: xác suất có điều kiện cũng là xác suất.

**Ví dụ 2.4.4 (Đồng xu được chọn ngẫu nhiên, tiếp theo).** Tiếp tục tình huống của Ví dụ 2.3.7, giả sử ta vừa thấy đồng xu được chọn ra mặt ngửa cả ba lần. Nếu tung thêm lần thứ tư, xác suất nó lại ra mặt ngửa là bao nhiêu?

**Lời giải.** Như trước, gọi $A$ là biến cố đồng xu được chọn ra mặt ngửa ba lần; gọi $H$ là biến cố lần tung thứ tư ra mặt ngửa. Ta cần $P(H\mid A)$. Biết đồng xu có cân đối hay không sẽ rất hữu ích. Định luật xác suất toàn phần có thêm điều kiện cho $P(H\mid A)$ dưới dạng trung bình có trọng số của $P(H\mid F,A)$ và $P(H\mid F^c,A)$; trong từng trường hợp này, ta đều biết đang dùng loại đồng xu nào:

$$\begin{aligned}P(H\mid A)&=P(H\mid F,A)P(F\mid A)+P(H\mid F^c,A)P(F^c\mid A)\\&=\frac12\cdot0{,}23+\frac34\cdot(1-0{,}23)\approx0{,}69.\end{aligned}$$

Các xác suất hậu nghiệm $P(F\mid A)$ và $P(F^c\mid A)$ lấy từ đáp án Ví dụ 2.3.7.

Một cách giải tương đương là định nghĩa hàm xác suất mới $\widetilde P$ sao cho $\widetilde P(B)=P(B\mid A)$ với mọi biến cố $B$. Hàm mới này gán xác suất đã cập nhật theo thông tin $A$ xảy ra. Khi đó, theo định luật xác suất toàn phần thông thường,

$$\widetilde P(H)=\widetilde P(H\mid F)\widetilde P(F)+\widetilde P(H\mid F^c)\widetilde P(F^c),$$

đúng bằng cách dùng định luật xác suất toàn phần có thêm điều kiện ở trên. Điều này một lần nữa minh họa nguyên lý: xác suất có điều kiện cũng là xác suất.

Ta thường muốn đặt điều kiện theo nhiều thông tin và giờ có vài cách để làm vậy. Chẳng hạn, có thể tìm $P(A\mid B,C)$ theo các cách sau:

1. Xem $B,C$ là một biến cố duy nhất $B\cap C$ rồi dùng định nghĩa: $P(A\mid B,C)=P(A,B,C)/P(B,C)$. Cách này tự nhiên nếu dễ xét $B,C$ cùng lúc. Sau đó ta tính tử và mẫu: có thể dùng định luật xác suất toàn phần cho cả hai, hoặc viết tử là $P(B,C\mid A)P(A)$ (tạo thành một dạng của quy tắc Bayes) rồi dùng định luật xác suất toàn phần để xử lý mẫu.
2. Dùng quy tắc Bayes với điều kiện bổ sung $C$: $P(A\mid B,C)=P(B\mid A,C)P(A\mid C)/P(B\mid C)$. Cách này tự nhiên nếu ta muốn xét mọi thứ trong bài toán dưới điều kiện $C$.
3. Dùng quy tắc Bayes với điều kiện bổ sung $B$: $P(A\mid B,C)=P(C\mid A,B)P(A\mid B)/P(C\mid B)$. Cách này giống cách trên nhưng đổi vai trò $B,C$. Chúng tôi nêu riêng để nhấn mạnh rằng thay số vào công thức mà không suy nghĩ biến cố nào nên giữ vai trò nào là một ý tưởng tệ.

Có nhiều cách tiếp cận dạng bài toán này vừa là thách thức, vừa là sức mạnh của xác suất có điều kiện.

### 2.5. Tính độc lập của các biến cố

Ta đã thấy vài ví dụ mà đặt điều kiện theo một biến cố làm thay đổi niềm tin về xác suất của biến cố khác. Khi các biến cố không cung cấp thông tin về nhau, ta gọi chúng là *độc lập*.

**Định nghĩa 2.5.1 (Hai biến cố độc lập).** Hai biến cố $A,B$ độc lập nếu $P(A\cap B)=P(A)P(B)$. Nếu $P(A)>0$ và $P(B)>0$, điều này tương đương với $P(A\mid B)=P(A)$, và cũng tương đương với $P(B\mid A)=P(B)$.

Nói cách khác, hai biến cố độc lập nếu có thể nhân xác suất riêng của chúng để được xác suất giao. Hoặc, $A,B$ độc lập nếu biết $B$ đã xảy ra không đem lại thông tin nào khiến ta thay đổi xác suất của $A$ (và ngược lại). Lưu ý rằng độc lập là quan hệ đối xứng: $A$ độc lập với $B$ thì $B$ cũng độc lập với $A$.

**Cảnh báo 2.5.2.** *Độc lập* hoàn toàn khác *rời nhau*. Nếu $A,B$ rời nhau, $P(A\cap B)=0$, nên chúng chỉ có thể độc lập nếu $P(A)=0$ hoặc $P(B)=0$. Biết $A$ xảy ra cho ta biết chắc $B$ không xảy ra; rõ ràng $A$ cung cấp thông tin về $B$, nên hai biến cố không độc lập (trừ khi một trong hai vốn có xác suất 0).

Theo trực giác, nếu $A$ không cho biết $B$ có xảy ra hay không, nó cũng không cho biết $B^c$ có xảy ra hay không. Ta chứng minh một kết quả hữu ích theo hướng đó.

**Mệnh đề 2.5.3.** Nếu $A,B$ độc lập, thì $A$ và $B^c$ độc lập, $A^c$ và $B$ độc lập, đồng thời $A^c$ và $B^c$ độc lập.

**Chứng minh.** Cho $A,B$ độc lập. Khi đó, $P(B^c\mid A)=1-P(B\mid A)=1-P(B)=P(B^c)$, nên $A,B^c$ độc lập. Đổi vai trò $A,B$, ta có $A^c,B$ độc lập. Áp dụng tiếp kết quả “độc lập với $B$ thì cũng độc lập với $B^c$” cho $A^c$, ta có $A^c,B^c$ độc lập.

Ta cũng thường cần nói về tính độc lập của ba biến cố trở lên.

**Định nghĩa 2.5.4 (Ba biến cố độc lập).** Các biến cố $A,B,C$ độc lập nếu *tất cả* các đẳng thức sau đều đúng:

$$P(A\cap B)=P(A)P(B),\quad P(A\cap C)=P(A)P(C),\quad P(B\cap C)=P(B)P(C),\quad P(A\cap B\cap C)=P(A)P(B)P(C).$$

Nếu chỉ ba điều kiện đầu đúng, ta nói $A,B,C$ *độc lập từng đôi*. Độc lập từng đôi không kéo theo độc lập toàn bộ: biết riêng $A$ hoặc riêng $B$ có thể không giúp dự đoán $C$ có xảy ra hay không, nhưng biết *cả* $A$ lẫn $B$ có thể rất liên quan đến $C$. Sau đây là một ví dụ đơn giản.

**Ví dụ 2.5.5 (Độc lập từng đôi không kéo theo độc lập toàn bộ).** Xét hai lần tung đồng xu cân đối và độc lập. Gọi $A$ là biến cố lần đầu ra ngửa, $B$ là biến cố lần thứ hai ra ngửa, còn $C$ là biến cố hai lần cho cùng kết quả. Khi ấy, $A,B,C$ độc lập từng đôi nhưng không độc lập toàn bộ, vì $P(A\cap B\cap C)=1/4$, còn $P(A)P(B)P(C)=1/8$. Biết riêng $A$ hoặc riêng $B$ không cho biết gì về $C$; nhưng biết kết quả của cả $A$ và $B$ lại cho thông tin về $C$ (trong ví dụ này là thông tin đầy đủ).

Ngược lại, đẳng thức $P(A\cap B\cap C)=P(A)P(B)P(C)$ không kéo theo độc lập từng đôi. Thấy ngay điều này ở trường hợp cực hạn $P(A)=0$: đẳng thức trở thành $0=0$ và không cho biết $B,C$ có độc lập hay không.

Tương tự, ta có thể định nghĩa tính độc lập của số biến cố bất kỳ. Trực giác là biết chuyện gì đã xảy ra với một tập con bất kỳ của các biến cố không cung cấp thông tin về các biến cố còn lại.

**Định nghĩa 2.5.6 (Nhiều biến cố độc lập).** Để $n$ biến cố $A_1,A_2,\ldots,A_n$ độc lập, ta yêu cầu mọi cặp thỏa $P(A_i\cap A_j)=P(A_i)P(A_j)$ khi $i\ne j$; mọi bộ ba thỏa $P(A_i\cap A_j\cap A_k)=P(A_i)P(A_j)P(A_k)$ khi $i,j,k$ khác nhau; tương tự cho mọi bộ bốn, bộ năm, v.v. Những điều kiện này có thể nhanh chóng trở nên cồng kềnh, nhưng về sau ta sẽ bàn các cách khác để hiểu tính độc lập. Với vô hạn biến cố, ta nói chúng độc lập nếu mọi tập con hữu hạn của chúng đều độc lập.

Tính độc lập có điều kiện được định nghĩa tương tự tính độc lập.

**Định nghĩa 2.5.7 (Độc lập có điều kiện).** Hai biến cố $A,B$ được gọi là *độc lập có điều kiện theo $E$* nếu $P(A\cap B\mid E)=P(A\mid E)P(B\mid E)$.

**Cảnh báo 2.5.8.** Nhầm lẫn độc lập với độc lập có điều kiện rất dễ dẫn đến những sai lầm nghiêm trọng. Hai biến cố có thể độc lập có điều kiện theo $E$ nhưng không độc lập vô điều kiện. Chúng có thể độc lập vô điều kiện nhưng không độc lập khi biết $E$. Chúng cũng có thể độc lập khi biết $E$ nhưng không độc lập khi biết $E^c$. Các ví dụ tiếp theo minh họa những khác biệt này. Cần hết sức cẩn thận khi làm việc với xác suất và tính độc lập có điều kiện!

**Ví dụ 2.5.9 (Độc lập có điều kiện không kéo theo độc lập vô điều kiện).** Trở lại Ví dụ 2.3.7: ta đã chọn hoặc một đồng xu cân đối, hoặc một đồng xu lệch có xác suất ra ngửa $3/4$, nhưng không biết đã chọn đồng xu nào. Ta tung đồng xu một số lần. Nếu biết đã chọn đồng xu cân đối, các lần tung độc lập và mỗi lần có xác suất ra ngửa $1/2$. Tương tự, nếu biết đã chọn đồng xu lệch, các lần tung độc lập và mỗi lần có xác suất ra ngửa $3/4$.

Tuy nhiên, các lần tung *không* độc lập vô điều kiện: khi chưa biết đã chọn đồng xu nào, quan sát chuỗi kết quả cho ta thông tin về khả năng đang cầm đồng xu cân đối hay đồng xu lệch. Nhờ đó, ta dự đoán tốt hơn các lần tung tiếp theo của cùng đồng xu.

Phát biểu chính xác: gọi $F$ là biến cố đã chọn đồng xu cân đối; $A_1,A_2$ lần lượt là biến cố lần tung thứ nhất và thứ hai ra ngửa. Khi biết $F$, $A_1,A_2$ độc lập; nhưng vô điều kiện thì không, vì $A_1$ cung cấp thông tin về $A_2$.

**Ví dụ 2.5.10 (Độc lập vô điều kiện không kéo theo độc lập có điều kiện).** Giả sử Alice và Bob là hai người bạn duy nhất gọi điện cho tôi. Mỗi ngày, họ quyết định độc lập xem có gọi hay không: gọi $A$ là biến cố Alice gọi, $B$ là biến cố Bob gọi; $A,B$ độc lập vô điều kiện. Nhưng giả sử giờ tôi nghe điện thoại reo. Dưới điều kiện này, $A,B$ không còn độc lập: nếu người gọi không phải Alice thì phải là Bob. Nói cách khác, gọi $R$ là biến cố điện thoại reo, ta có $P(B\mid R)<1=P(B\mid A^c,R)$; vậy $B,A^c$ không độc lập có điều kiện theo $R$, và $A,B$ cũng vậy.

**Ví dụ 2.5.11 (Độc lập theo $E$ so với theo $E^c$).** Giả sử có hai loại lớp học: tốt và tệ. Trong lớp tốt, nếu chăm học, bạn rất có khả năng đạt điểm A. Trong lớp tệ, giảng viên cho điểm ngẫu nhiên, bất kể sinh viên cố gắng ra sao. Gọi $G$ là biến cố lớp học tốt, $W$ là biến cố bạn chăm học, $A$ là biến cố bạn nhận điểm A. Khi biết $G^c$ (lớp tệ), $W,A$ độc lập có điều kiện; nhưng khi biết $G$ (lớp tốt), chúng không độc lập!

### 2.6. Tính nhất quán của quy tắc Bayes

Một tính chất quan trọng của quy tắc Bayes là *tính nhất quán*: nếu nhận nhiều thông tin và muốn cập nhật xác suất để tính đến tất cả, kết quả không phụ thuộc việc ta cập nhật tuần tự từng bằng chứng hay cập nhật cùng lúc bằng mọi bằng chứng. Chẳng hạn, giả sử ta làm một thí nghiệm kéo dài một tuần, có dữ liệu cuối mỗi ngày. Ta có thể dùng quy tắc Bayes hằng ngày để cập nhật xác suất theo dữ liệu ngày đó. Hoặc ta đi nghỉ cả tuần, chiều thứ Sáu quay về và cập nhật một lần bằng dữ liệu của cả tuần. Hai cách cho cùng kết quả.

Hãy xem một ứng dụng cụ thể của nguyên lý này.

**Ví dụ 2.6.1 (Xét nghiệm bệnh hiếm, tiếp theo).** Fred, người đã xét nghiệm dương tính với *conditionitis* trong Ví dụ 2.3.9, quyết định xét nghiệm lần thứ hai. Xét nghiệm mới độc lập với xét nghiệm ban đầu khi biết tình trạng bệnh, và có cùng độ nhạy, độ đặc hiệu. Không may cho Fred, lần hai cũng dương tính. Hãy tìm xác suất Fred mắc bệnh theo hai cách: một bước, đặt điều kiện đồng thời theo hai kết quả; và hai bước, cập nhật theo kết quả đầu rồi cập nhật tiếp theo kết quả thứ hai.

**Lời giải.** Gọi $D$ là biến cố Fred mắc bệnh, $T_1$ là biến cố xét nghiệm thứ nhất dương tính, $T_2$ là biến cố xét nghiệm thứ hai dương tính. Trong Ví dụ 2.3.9, ta đã dùng quy tắc Bayes và định luật xác suất toàn phần để tìm $P(D\mid T_1)$. Có cách giải nhanh khác bằng dạng tỉ lệ cược của quy tắc Bayes:

$$\frac{P(D\mid T_1)}{P(D^c\mid T_1)}=\frac{P(D)}{P(D^c)}\frac{P(T_1\mid D)}{P(T_1\mid D^c)}=\frac1{99}\frac{0{,}95}{0{,}05}\approx0{,}19.$$

Vì $P(D\mid T_1)/(1-P(D\mid T_1))=0{,}19$, nên $P(D\mid T_1)=0{,}19/(1+0{,}19)\approx0{,}16$, phù hợp đáp án trước. Dạng tỉ lệ cược nhanh hơn ở đây vì không cần tính xác suất không điều kiện $P(T_1)$ trong mẫu số của quy tắc Bayes thông thường. Giờ hãy tiếp tục dùng dạng tỉ lệ cược để xét chuyện gì xảy ra nếu Fred dương tính lần thứ hai.

**Cách một bước.** Cập nhật cùng lúc theo cả hai kết quả xét nghiệm:

$$\begin{aligned}\frac{P(D\mid T_1\cap T_2)}{P(D^c\mid T_1\cap T_2)}&=\frac{P(D)}{P(D^c)}\frac{P(T_1\cap T_2\mid D)}{P(T_1\cap T_2\mid D^c)}\\&=\frac1{99}\frac{0{,}95^2}{0{,}05^2}=\frac{361}{99}\approx3{,}646.\end{aligned}$$

Tỉ lệ cược này tương ứng với xác suất khoảng $0{,}78$.

**Cách hai bước.** Sau xét nghiệm thứ nhất, tỉ lệ cược hậu nghiệm Fred mắc bệnh là $P(D\mid T_1)/P(D^c\mid T_1)=(1/99)(0{,}95/0{,}05)\approx0{,}19$, như trên. Lấy tỉ lệ cược hậu nghiệm này làm tỉ lệ cược tiên nghiệm mới, rồi cập nhật theo xét nghiệm thứ hai:

$$\begin{aligned}\frac{P(D\mid T_1\cap T_2)}{P(D^c\mid T_1\cap T_2)}&=\frac{P(D\mid T_1)}{P(D^c\mid T_1)}\frac{P(T_2\mid D,T_1)}{P(T_2\mid D^c,T_1)}\\&=\left(\frac1{99}\frac{0{,}95}{0{,}05}\right)\frac{0{,}95}{0{,}05}=\frac{361}{99}\approx3{,}646,\end{aligned}$$

đúng như cách một bước. Sau kết quả dương tính thứ hai, xác suất Fred mắc bệnh tăng từ $0{,}16$ lên $0{,}78$, khiến ta tin chắc hơn nhiều rằng ông thật sự mắc *conditionitis*. Bài học rút ra là xin ý kiến xét nghiệm thứ hai là điều nên làm!

### 2.7. Đặt điều kiện như một công cụ giải bài toán

Đặt điều kiện là công cụ mạnh vì nó cho phép ta suy nghĩ theo điều mình *ước gì biết được*. Nếu bài toán sẽ dễ hơn khi biết biến cố $E$ có xảy ra hay không, ta có thể lần lượt đặt điều kiện theo $E$ và $E^c$, xét riêng hai khả năng, rồi kết hợp chúng bằng định luật xác suất toàn phần.

#### 2.7.1. Chiến lược: đặt điều kiện theo điều bạn muốn biết

**Ví dụ 2.7.1 (Monty Hall).** Trong chương trình trò chơi *Let’s Make a Deal* do Monty Hall dẫn, người chơi chọn một trong ba cánh cửa đóng kín. Hai cửa giấu dê, một cửa giấu ô tô. Monty biết ô tô ở đâu; sau khi người chơi chọn, ông mở một trong hai cửa còn lại. Cửa ông mở luôn giấu dê (ông không bao giờ để lộ ô tô!). Nếu có hai cửa để lựa chọn, ông chọn ngẫu nhiên, mỗi cửa có xác suất như nhau. Sau đó, Monty cho người chơi quyền đổi sang cửa chưa mở còn lại. Nếu muốn lấy ô tô, người chơi có nên đổi cửa không?

**Lời giải.** Đánh số các cửa từ 1 đến 3. Không mất tính tổng quát, giả sử người chơi ban đầu chọn cửa 1. Nếu cô không chọn cửa 1, ta chỉ cần đổi nhãn các cửa hoặc viết lại lời giải theo thứ tự nhãn khác. Monty mở một cửa, để lộ con dê. Khi quyết định có đổi sang cửa chưa mở còn lại hay không, người chơi thật sự muốn biết điều gì? Dĩ nhiên quyết định sẽ dễ hơn nhiều nếu biết ô tô ở đâu! Điều này gợi ý đặt điều kiện theo vị trí ô tô. Gọi $C_i$ là biến cố ô tô ở sau cửa $i$ với $i=1,2,3$. Theo định luật xác suất toàn phần,

$$P(\text{lấy được ô tô})=\frac13P(\text{lấy được ô tô}\mid C_1)+\frac13P(\text{lấy được ô tô}\mid C_2)+\frac13P(\text{lấy được ô tô}\mid C_3).$$

Giả sử người chơi luôn đổi cửa. Nếu ô tô ở cửa 1, đổi sẽ thua: $P(\text{lấy được ô tô}\mid C_1)=0$. Nếu ô tô ở cửa 2 hoặc 3, Monty luôn mở cửa có dê, nên cửa chưa mở còn lại phải có ô tô; đổi sẽ thắng. Vậy $P(\text{lấy được ô tô})=0\cdot(1/3)+1\cdot(1/3)+1\cdot(1/3)=2/3$. Chiến lược đổi cửa thắng $2/3$ số lần; người chơi nên đổi.

**Hình 2.5.** Sơ đồ cây của bài toán Monty Hall. Với chiến lược đổi cửa, người chơi lấy được ô tô $2/3$ số lần.

Có thể diễn giải trực giác theo tần suất: tưởng tượng chơi trò này 1.000 lần. Khoảng 333 lần lựa chọn đầu của bạn đúng vị trí ô tô; khi đó đổi cửa sẽ thua. Khoảng 667 lần còn lại, bạn sẽ thắng nếu đổi cửa.

Tuy nhiên, có một điểm tinh tế: lúc quyết định có đổi cửa hay không, người chơi còn biết *Monty đã mở cửa nào*. Ta vừa chứng minh xác suất thắng *không điều kiện* của chiến lược đổi cửa là $2/3$. Giờ hãy chứng minh xác suất thắng *có điều kiện theo thông tin Monty cung cấp* cũng bằng $2/3$.

Gọi $M_j$ là biến cố Monty mở cửa $j$, với $j=2,3$. Khi ấy, $P(\text{lấy ô tô})=P(\text{lấy ô tô}\mid M_2)P(M_2)+P(\text{lấy ô tô}\mid M_3)P(M_3)$. Do tính đối xứng, $P(M_2)=P(M_3)=1/2$ và $P(\text{lấy ô tô}\mid M_2)=P(\text{lấy ô tô}\mid M_3)$. Tính đối xứng ở đây là vì đề bài không có điểm gì phân biệt cửa 2 và cửa 3; trái lại, Bài 39 xét trường hợp Monty thích mở cửa 2 hơn cửa 3. Đặt $x=P(\text{lấy ô tô}\mid M_2)=P(\text{lấy ô tô}\mid M_3)$. Thay các giá trị đã biết, $2/3=x/2+x/2=x$, đúng như khẳng định.

Quy tắc Bayes cũng cho cách tìm xác suất thắng có điều kiện theo bằng chứng rất gọn. Giả sử Monty mở cửa 2. Với ký hiệu và kết quả trên,

$$P(C_1\mid M_2)=\frac{P(M_2\mid C_1)P(C_1)}{P(M_2)}=\frac{(1/2)(1/3)}{1/2}=\frac13.$$

Vậy khi Monty mở cửa 2, xác suất cửa người chơi chọn ban đầu có ô tô là $1/3$; do đó đổi cửa sẽ thắng với xác suất $2/3$.

Nhiều người gặp bài toán này lần đầu cho rằng đổi cửa không có lợi: “Còn hai cửa và một cửa có ô tô, vậy mỗi cửa có xác suất 50–50.” Sau chương trước, ta nhận ra lập luận ấy áp dụng sai định nghĩa xác suất sơ khai. Tuy nhiên, định nghĩa sơ khai, ngay cả khi dùng sai, vẫn có sức ảnh hưởng mạnh đến trực giác. Khi Marilyn vos Savant trình bày lời giải đúng của bài toán Monty Hall trên chuyên mục báo *Parade* năm 1990, bà nhận được hàng nghìn lá thư của độc giả (kể cả nhà toán học) khẳng định bà sai.

Để xây dựng trực giác đúng, hãy xét trường hợp cực hạn. Giả sử có một triệu cửa: 999.999 cửa giấu dê và một cửa giấu ô tô. Sau lựa chọn đầu của người chơi, Monty mở 999.998 cửa có dê rồi cho người chơi quyền đổi. Ở trường hợp này, rõ ràng xác suất của hai cửa chưa mở không phải 50–50; rất ít người sẽ cố chấp giữ cửa chọn ban đầu. Trường hợp ba cửa cũng vậy.

Giống như Ví dụ 2.2.6 buộc ta giả định cách gặp đứa trẻ được chọn ngẫu nhiên, tỉ lệ thắng $2/3$ ở đây phụ thuộc vào giả định Monty chọn cửa để mở như thế nào. Các bài tập sẽ xét một số biến thể và khái quát của Monty Hall, trong đó có biến thể làm thay đổi lợi ích của việc đổi cửa.

#### 2.7.2. Chiến lược: đặt điều kiện theo bước đầu tiên

Trong các bài toán có cấu trúc đệ quy, đặt điều kiện theo bước đầu tiên của phép thử thường rất hữu ích. Hai ví dụ tiếp theo áp dụng chiến lược này, gọi là *phân tích bước đầu*.

**Ví dụ 2.7.2 (Quá trình phân nhánh).** Một con amip tên Bobo sống trong ao. Sau một phút, Bobo chết, phân chia thành hai con, hoặc giữ nguyên, mỗi khả năng có xác suất bằng nhau. Trong những phút tiếp theo, mọi amip còn sống đều hành xử như vậy, độc lập với nhau. Xác suất quần thể amip cuối cùng tuyệt chủng là bao nhiêu?

**Lời giải.** Gọi $D$ là biến cố quần thể cuối cùng tuyệt chủng; ta cần tìm $P(D)$. Đặt điều kiện theo kết quả bước đầu: gọi $B_i$ là biến cố sau phút đầu Bobo tạo thành $i$ con amip, với $i=0,1,2$.

Ta biết $P(D\mid B_0)=1$ và $P(D\mid B_1)=P(D)$: nếu Bobo không đổi, bài toán trở lại đúng điểm xuất phát. Nếu Bobo phân thành hai, ta có hai bản sao độc lập của bài toán ban đầu. Cả hai nhánh con đều phải cuối cùng tuyệt chủng, nên $P(D\mid B_2)=P(D)^2$. Đã xét hết mọi trường hợp; kết hợp bằng định luật xác suất toàn phần:

$$P(D)=P(D\mid B_0)\frac13+P(D\mid B_1)\frac13+P(D\mid B_2)\frac13=\frac13+\frac{P(D)}3+\frac{P(D)^2}3.$$

Giải phương trình này cho $P(D)$, ta được $P(D)=1$: quần thể amip tuyệt chủng với xác suất 1. Chiến lược phân tích bước đầu hữu ích ở đây vì bài toán có tính tự đồng dạng: khi Bobo giữ nguyên hoặc tách làm hai, ta có một hoặc hai bản sao của bài toán ban đầu. Đặt điều kiện theo bước đầu cho phép biểu diễn $P(D)$ theo chính nó.

**Ví dụ 2.7.3 (Con bạc phá sản).** Hai con bạc $A,B$ liên tục cược mỗi lần 1 đô la. Trong mỗi lượt, $A$ có xác suất thắng $p$, còn $B$ thắng với xác suất $q=1-p$. Ban đầu $A$ có $i$ đô la, $B$ có $N-i$ đô la. Tổng tài sản của họ không đổi: mỗi đô la $A$ thua sẽ chuyển cho $B$, và ngược lại.

Có thể hình dung trò chơi như một chuyển động ngẫu nhiên trên các số nguyên từ 0 đến $N$, trong đó xác suất đi sang phải mỗi bước là $p$: một người bắt đầu ở vị trí $i$, mỗi bước đi một đơn vị sang phải với xác suất $p$ hoặc sang trái với xác suất $q=1-p$. Trò chơi kết thúc khi $A$ hoặc $B$ phá sản, tức chuyển động chạm 0 hoặc $N$. Xác suất $A$ thắng, lấy toàn bộ tiền, là bao nhiêu?

**Lời giải.** Trò chơi này, giống quá trình sinh sản của Bobo, có cấu trúc đệ quy: sau bước đầu, đây vẫn là cùng một trò chơi, chỉ khác tài sản của $A$ thành $i+1$ hoặc $i-1$. Gọi $p_i$ là xác suất $A$ thắng khi ban đầu có $i$ đô la. Ta dùng phân tích bước đầu để tìm $p_i$. Gọi $W$ là biến cố $A$ thắng. Theo định luật xác suất toàn phần, đặt điều kiện theo kết quả lượt đầu:

$$\begin{aligned}p_i&=P(W\mid A\text{ bắt đầu với }i,\text{ thắng lượt 1})p+P(W\mid A\text{ bắt đầu với }i,\text{ thua lượt 1})q\\&=P(W\mid A\text{ bắt đầu với }i+1)p+P(W\mid A\text{ bắt đầu với }i-1)q\\&=p_{i+1}p+p_{i-1}q.\end{aligned}$$

Điều này đúng với mọi $i$ từ 1 đến $N-1$; ta còn có điều kiện biên $p_0=0$ và $p_N=1$. Giờ ta giải *phương trình sai phân* này để tìm $p_i$. Mục A.4 của phụ lục toán học trình bày cách giải phương trình sai phân, nên ở đây ta lược vài bước.

Đa thức đặc trưng là $px^2-x+q=0$, có hai nghiệm $1$ và $q/p$. Nếu $p\ne1/2$, hai nghiệm phân biệt và nghiệm tổng quát là $p_i=a\cdot1^i+b(q/p)^i$. Dùng điều kiện biên $p_0=0$, $p_N=1$, ta được $a=-b=1/[1-(q/p)^N]$; thay vào cho nghiệm cụ thể. Nếu $p=1/2$, hai nghiệm đặc trưng trùng nhau nên nghiệm tổng quát là $p_i=a\cdot1^i+b\,i\cdot1^i$. Điều kiện biên cho $a=0$, $b=1/N$.

Tóm lại, xác suất $A$ thắng khi ban đầu có $i$ đô la là

$$p_i=\begin{cases}\dfrac{1-(q/p)^i}{1-(q/p)^N},&p\ne1/2,\\[6pt]\dfrac{i}{N},&p=1/2.\end{cases}$$

Trường hợp $p=1/2$ phù hợp với trường hợp $p\ne1/2$ theo nghĩa giới hạn $\lim_{p\to1/2}[1-(q/p)^i]/[1-(q/p)^N]=i/N$. Đặt $x=q/p$ và cho $x\to1$; theo quy tắc L’Hôpital,

$$\lim_{x\to1}\frac{1-x^i}{1-x^N}=\lim_{x\to1}\frac{i x^{i-1}}{N x^{N-1}}=\frac{i}{N}.$$

Nhờ tính đối xứng, xác suất $B$ thắng khi ban đầu có $N-i$ đô la được tính bằng cách đổi vai trò $q,p$ và $i,N-i$. Có thể kiểm tra rằng với mọi $i,p$, $P(A\text{ thắng})+P(B\text{ thắng})=1$, nên trò chơi chắc chắn kết thúc: xác suất dao động mãi không dừng bằng 0.

### 2.8. Cạm bẫy và nghịch lý

Hai ví dụ tiếp theo là các kiểu suy luận sai về xác suất có điều kiện từng xuất hiện trong lĩnh vực pháp lý. *Ngụy biện của công tố viên* là nhầm $P(A\mid B)$ với $P(B\mid A)$; *ngụy biện của luật sư bào chữa* là không đặt điều kiện theo toàn bộ bằng chứng.

**Cảnh báo 2.8.1 (Ngụy biện của công tố viên).** Năm 1998, Sally Clark bị xét xử vì tội giết người sau khi hai con trai bà qua đời không lâu sau khi sinh. Tại phiên tòa, một nhân chứng chuyên môn bên công tố khai rằng xác suất một trẻ sơ sinh tử vong do hội chứng đột tử ở trẻ sơ sinh (SIDS) là $1/8500$; vì thế, xác suất hai trẻ trong cùng một gia đình đều tử vong vì SIDS là $(1/8500)^2$, hay khoảng một phần 73 triệu. Ông ta suy tiếp rằng xác suất Clark vô tội là một phần 73 triệu.

Lối lập luận này có ít nhất hai vấn đề lớn. Thứ nhất, nhân chứng tính xác suất giao của hai biến cố “con trai thứ nhất chết vì SIDS” và “con trai thứ hai chết vì SIDS” bằng cách nhân xác suất riêng của chúng. Như ta biết, phép nhân đó chỉ đúng nếu hai cái chết vì SIDS trong cùng gia đình độc lập. Điều này sẽ không đúng nếu yếu tố di truyền hoặc nguy cơ đặc thù của gia đình khiến mọi trẻ sơ sinh ở một số gia đình có rủi ro SIDS cao hơn.

Thứ hai, “chuyên gia” ấy đã nhầm hai xác suất có điều kiện khác nhau: $P(\text{vô tội}\mid\text{bằng chứng})$ khác $P(\text{bằng chứng}\mid\text{vô tội})$. Nhân chứng cho rằng nếu bị cáo vô tội thì xác suất quan sát thấy hai trẻ sơ sinh tử vong cực thấp; tức $P(\text{bằng chứng}\mid\text{vô tội})$ nhỏ. Nhưng điều ta cần biết là $P(\text{vô tội}\mid\text{bằng chứng})$, xác suất bị cáo vô tội khi xét toàn bộ bằng chứng. Theo quy tắc Bayes,

$$P(\text{vô tội}\mid\text{bằng chứng})=\frac{P(\text{bằng chứng}\mid\text{vô tội})P(\text{vô tội})}{P(\text{bằng chứng})}.$$

Để tính xác suất vô tội khi đã biết bằng chứng, ta phải tính đến xác suất vô tội tiên nghiệm $P(\text{vô tội})$. Xác suất này rất cao: hai cái chết vì SIDS hiếm, nhưng hai vụ giết trẻ sơ sinh trong cùng gia đình cũng hiếm! Xác suất vô tội hậu nghiệm cân bằng giữa $P(\text{bằng chứng}\mid\text{vô tội})$ thấp và $P(\text{vô tội})$ cao. Con số $(1/8500)^2$ của nhân chứng, vốn đã đáng nghi, chỉ là một phần trong công thức.

Đáng buồn, Clark bị kết tội giết người và phải ngồi tù, một phần do lời khai sai lầm ấy. Bà ở tù hơn ba năm trước khi bản án bị hủy. Sự phẫn nộ trước việc dùng sai xác suất có điều kiện trong vụ Sally Clark đã dẫn đến việc rà soát hàng trăm vụ án khác mà bên công tố dùng kiểu lập luận sai tương tự.

**Cảnh báo 2.8.2 (Ngụy biện của luật sư bào chữa).** Một phụ nữ bị sát hại; chồng bà bị đưa ra xét xử vì tội này. Có bằng chứng cho thấy bị cáo từng bạo hành vợ. Luật sư bào chữa lập luận rằng bằng chứng bạo hành không liên quan nên phải loại khỏi phiên tòa, vì chỉ một trong 10.000 người đàn ông bạo hành vợ sau đó giết vợ. Thẩm phán có nên chấp nhận yêu cầu này không?

Giả sử tỉ lệ một phần 10.000 của luật sư là đúng, và có thêm các dữ kiện sau: một trong mười người đàn ông bạo hành vợ; một trong năm phụ nữ đã kết hôn bị sát hại là do chồng giết; và 50% số người chồng giết vợ trước đó từng bạo hành họ.

Gọi $A$ là biến cố chồng bạo hành vợ, $G$ là biến cố chồng có tội. Lập luận bào chữa cho rằng $P(G\mid A)=1/10000$, nên ngay cả khi biết người chồng từng bạo hành, khả năng ông ta có tội vẫn cực thấp. Nhưng luật sư đã bỏ qua một sự kiện then chốt khi đặt điều kiện: ta biết người vợ *đã bị sát hại*. Do đó, xác suất liên quan không phải $P(G\mid A)$ mà là $P(G\mid A,M)$, với $M$ là biến cố người vợ bị sát hại.

Quy tắc Bayes với điều kiện bổ sung cho

$$\begin{aligned}P(G\mid A,M)&=\frac{P(A\mid G,M)P(G\mid M)}{P(A\mid G,M)P(G\mid M)+P(A\mid G^c,M)P(G^c\mid M)}\\&=\frac{0{,}5\cdot0{,}2}{0{,}5\cdot0{,}2+0{,}1\cdot0{,}8}=\frac59.\end{aligned}$$

Bằng chứng bạo hành đã làm xác suất có tội tăng từ 20% lên hơn 50%; vì vậy tiền sử bạo hành cho biết thông tin quan trọng về khả năng bị cáo có tội, trái với lập luận của luật sư.

Lưu ý rằng phép tính trên không dùng con số $P(G\mid A)$ của luật sư. Con số đó không liên quan đến phép tính vì không xét sự kiện người vợ đã bị sát hại. Ta phải đặt điều kiện theo *tất cả* bằng chứng.

Chúng ta kết thúc chương bằng một nghịch lý về xác suất có điều kiện và việc gộp dữ liệu.

**Ví dụ 2.8.3 (Nghịch lý Simpson).** Hai bác sĩ Hibbert và Nick đều thực hiện hai loại thủ thuật: phẫu thuật tim và tháo băng cá nhân. Mỗi thủ thuật hoặc thành công hoặc thất bại. Kết quả của từng bác sĩ được cho trong bảng và minh họa ở Hình 2.6; chấm trắng biểu thị ca thành công, chấm đen biểu thị ca thất bại.

| Bác sĩ | Kết quả | Phẫu thuật tim | Tháo băng cá nhân |
|---|---|---:|---:|
| Hibbert | Thành công | 70 | 10 |
| Hibbert | Thất bại | 20 | 0 |
| Nick | Thành công | 2 | 81 |
| Nick | Thất bại | 8 | 9 |

Trong phẫu thuật tim, tỉ lệ thành công của bác sĩ Hibbert cao hơn bác sĩ Nick: 70 trên 90 so với 2 trên 10. Trong tháo băng, bác sĩ Hibbert cũng có tỉ lệ cao hơn: 10 trên 10 so với 81 trên 90. Nhưng nếu gộp hai loại thủ thuật để so sánh tỉ lệ thành công chung, bác sĩ Hibbert thành công 80 trong 100 ca, còn bác sĩ Nick thành công 83 trong 100 ca: tỉ lệ chung của Nick *cao hơn*!

**Hình 2.6.** Ví dụ về nghịch lý Simpson. Chấm trắng là ca thành công, chấm đen là ca thất bại. Bác sĩ Hibbert giỏi hơn ở từng loại thủ thuật nhưng có tỉ lệ thành công chung thấp hơn vì ông thực hiện loại khó nhiều hơn Nick rất nhiều.

Điều xảy ra là bác sĩ Hibbert, có lẽ nhờ tiếng tăm giỏi hơn, thực hiện nhiều ca phẫu thuật tim hơn, mà loại phẫu thuật này vốn rủi ro hơn việc tháo băng. Tỉ lệ thành công chung thấp hơn không phải vì kỹ năng của ông kém hơn ở loại nào, mà vì phần lớn ca của ông thuộc loại rủi ro.

Hãy dùng ký hiệu biến cố để nói chính xác. Với các biến cố $A,B,C$, ta nói có *nghịch lý Simpson* nếu

$$P(A\mid B,C)<P(A\mid B^c,C),\qquad P(A\mid B,C^c)<P(A\mid B^c,C^c),$$

nhưng $P(A\mid B)>P(A\mid B^c)$. Trong ví dụ này, $A$ là biến cố ca thành công, $B$ là biến cố bác sĩ Nick thực hiện, còn $C$ là biến cố ca phẫu thuật tim. Các điều kiện của nghịch lý đều thỏa: dù xét phẫu thuật tim hay tháo băng, xác suất thành công của Nick thấp hơn Hibbert, nhưng xác suất thành công chung của Nick lại cao hơn.

Định luật xác suất toàn phần giải thích bằng toán học vì sao điều đó có thể xảy ra:

$$\begin{aligned}P(A\mid B)&=P(A\mid C,B)P(C\mid B)+P(A\mid C^c,B)P(C^c\mid B),\\P(A\mid B^c)&=P(A\mid C,B^c)P(C\mid B^c)+P(A\mid C^c,B^c)P(C^c\mid B^c).\end{aligned}$$

Dù $P(A\mid C,B)<P(A\mid C,B^c)$ và $P(A\mid C^c,B)<P(A\mid C^c,B^c)$, các trọng số $P(C\mid B)$ và $P(C^c\mid B)$ vẫn có thể đảo ngược so sánh chung. Trong tình huống này, $P(C^c\mid B)>P(C^c\mid B^c)$ vì Nick có khả năng thực hiện ca tháo băng cao hơn nhiều; chênh lệch đó đủ lớn để $P(A\mid B)>P(A\mid B^c)$.

Gộp các loại thủ thuật tạo ra bức tranh sai lệch về năng lực hai bác sĩ vì ta mất thông tin bác sĩ nào thường thực hiện loại nào. Khi nghi ngờ có các biến gây nhiễu như loại thủ thuật, nên xem dữ liệu tách theo từng nhóm để hiểu chuyện gì thực sự xảy ra.

Nghịch lý Simpson xuất hiện trong nhiều bối cảnh thực tế. Với các ví dụ sau, hãy thử xác định các biến cố $A,B,C$ tạo nên nghịch lý:

- **Phân biệt giới trong tuyển sinh đại học:** Vào thập niên 1970, nam giới có tỉ lệ được nhận vào chương trình sau đại học tại Đại học California, Berkeley cao hơn đáng kể so với nữ giới, dẫn đến cáo buộc phân biệt giới. Nhưng ở phần lớn khoa riêng lẻ, nữ giới lại có tỉ lệ được nhận cao hơn nam giới. Người ta nhận thấy nữ giới thường nộp vào các khoa cạnh tranh hơn, còn nam giới thường nộp vào các khoa ít cạnh tranh hơn.
- **Tỉ lệ đánh bóng thành công trong bóng chày:** Cầu thủ 1 có thể có tỉ lệ đánh bóng thành công cao hơn cầu thủ 2 ở nửa đầu mùa giải *và* ở nửa sau, nhưng tỉ lệ chung cả mùa lại thấp hơn. Điều này phụ thuộc số lượt đánh bóng của mỗi cầu thủ trong từng nửa mùa. Một lượt đánh bóng là khi đến lượt cầu thủ cố đánh quả bóng; tỉ lệ đánh bóng thành công bằng số lần đánh trúng chia cho số lượt đánh bóng.
- **Ảnh hưởng sức khỏe của hút thuốc:** Cochran [5] nhận thấy trong mỗi nhóm tuổi, người hút thuốc lá điếu có tỉ lệ tử vong cao hơn người hút xì gà. Nhưng vì người hút thuốc lá điếu trung bình trẻ hơn người hút xì gà, tỉ lệ tử vong chung của họ lại thấp hơn.

### 2.9. Tóm tắt

Xác suất có điều kiện của $A$ khi biết $B$ là $P(A\mid B)=P(A\cap B)/P(B)$. Nó có đúng các tính chất như xác suất thông thường, nhưng hàm $P(\cdot\mid B)$ cập nhật sự bất định của ta về các biến cố theo bằng chứng $B$ được quan sát. Những biến cố có xác suất không đổi sau khi biết $B$ được gọi là độc lập với $B$. Hai biến cố cũng có thể độc lập có điều kiện khi biết biến cố thứ ba $E$. Độc lập có điều kiện không kéo theo độc lập vô điều kiện; chiều ngược lại cũng không đúng.

Hai kết quả quan trọng về xác suất có điều kiện là quy tắc Bayes, liên hệ $P(A\mid B)$ với $P(B\mid A)$, và định luật xác suất toàn phần, cho phép tìm xác suất không điều kiện bằng cách phân hoạch không gian mẫu rồi tính xác suất có điều kiện trong từng phần.

Đặt điều kiện rất hữu ích khi giải toán vì nó cho phép chia bài toán thành các phần nhỏ hơn, xét riêng mọi trường hợp rồi kết hợp lại. Khi dùng chiến lược này, nên đặt điều kiện theo thông tin mà nếu biết thì bài toán sẽ đơn giản hơn — vì vậy mới có câu “đặt điều kiện theo điều bạn ước gì biết”. Nếu phép thử gồm nhiều giai đoạn, đặt điều kiện theo bước đầu có thể giúp tìm một hệ thức đệ quy.

Những lỗi thường gặp khi suy luận có điều kiện gồm:

- nhầm xác suất tiên nghiệm $P(A)$ với xác suất hậu nghiệm $P(A\mid B)$;
- ngụy biện của công tố viên: nhầm $P(A\mid B)$ với $P(B\mid A)$;
- ngụy biện của luật sư bào chữa: không đặt điều kiện theo mọi bằng chứng;
- không nhận ra nghịch lý Simpson và tầm quan trọng của việc cân nhắc kỹ có nên gộp dữ liệu hay không.

Hình 2.7 minh họa cách cập nhật xác suất tuần tự khi có bằng chứng mới. Hãy tưởng tượng có biến cố $A$ ta quan tâm. Sáng thứ Hai, xác suất tiên nghiệm của $A$ là $P(A)$. Nếu chiều thứ Hai ta quan sát thấy $B$ xảy ra, ta có thể dùng quy tắc Bayes (hoặc định nghĩa xác suất có điều kiện) để tính xác suất hậu nghiệm $P(A\mid B)$. Xác suất hậu nghiệm ấy trở thành xác suất tiên nghiệm mới cho sáng thứ Ba, rồi ta tiếp tục thu thập bằng chứng. Giả sử thứ Ba ta quan sát thấy $C$ xảy ra. Ta có thể tính xác suất hậu nghiệm mới $P(A\mid B,C)$ theo nhiều cách (trong bối cảnh này, có lẽ tự nhiên nhất là dùng quy tắc Bayes với điều kiện bổ sung $B$). Xác suất đó lại trở thành xác suất tiên nghiệm mới nếu ta tiếp tục thu thập bằng chứng.

**Hình 2.7.** Xác suất có điều kiện cho biết cách cập nhật xác suất khi có bằng chứng mới. Sơ đồ biểu diễn xác suất của biến cố $A$ lúc đầu, sau bằng chứng $B$, rồi sau bằng chứng thứ hai $C$. Xác suất hậu nghiệm sau $B$ trở thành xác suất tiên nghiệm mới trước khi quan sát $C$. Sau khi đã biết cả $B$ và $C$, ta có thể tìm xác suất hậu nghiệm mới bằng nhiều cách; nếu còn thu thập thêm bằng chứng, nó tiếp tục trở thành tiên nghiệm mới.

### 2.10. R (từ trang PDF 90)

#### Mô phỏng cách hiểu theo tần suất

Nhớ lại rằng khi lặp lại phép thử $n$ lần với $n$ lớn, cách hiểu tần suất cho $P(A\mid B)\approx n_{AB}/n_B$, trong đó $n_{AB}$ là số lần $A\cap B$ xảy ra, còn $n_B$ là số lần $B$ xảy ra. Hãy mô phỏng để kiểm tra kết quả Ví dụ 2.2.5. Ta sẽ mô phỏng $n$ gia đình, mỗi gia đình có hai con:

```r
n <- 10^5
child1 <- sample(2,n,replace=TRUE)
child2 <- sample(2,n,replace=TRUE)
```

Ở đây, `child1` là vectơ độ dài $n$ với mỗi phần tử là 1 hoặc 2. Quy ước 1 là “gái”, 2 là “trai”; vectơ biểu diễn giới tính của con lớn trong mỗi gia đình. Tương tự, `child2` biểu diễn giới tính con nhỏ. Cũng có thể dùng `sample(c("girl","boy"),n,replace=TRUE)`, nhưng làm việc với giá trị số thuận tiện hơn.

Gọi $A$ là biến cố cả hai con đều là gái, $B$ là biến cố con lớn là gái. Theo cách hiểu tần suất, ta đếm số lần $B$ xảy ra và đặt tên là `n.b`; cũng đếm số lần $A\cap B$ xảy ra và đặt tên `n.ab`. Cuối cùng, chia `n.ab` cho `n.b` để xấp xỉ $P(A\mid B)$:

```r
n.b <- sum(child1==1)
n.ab <- sum(child1==1 & child2==1)
n.ab/n.b
```

Ký hiệu `&` là phép VÀ theo từng phần tử, nên `n.ab` là số gia đình có cả con lớn lẫn con nhỏ là gái. Khi chạy mã này, chúng tôi nhận được $0{,}50$, xác nhận kết quả $P(\text{cả hai là gái}\mid\text{con lớn là gái})=1/2$.

Giờ cho $A$ vẫn là biến cố cả hai con là gái, còn $B$ là biến cố có ít nhất một con gái. $A\cap B$ không đổi, nhưng `n.b` phải đếm số lần có ít nhất một con gái.

Ta dùng toán tử HOẶC theo từng phần tử `|` để đếm; đây không phải dấu đặt điều kiện mà là phép HOẶC bao hàm, trả về `TRUE` nếu ít nhất một phần tử đúng:

```r
n.b <- sum(child1==1 | child2==1)
n.ab <- sum(child1==1 & child2==1)
n.ab/n.b
```

Chúng tôi nhận được $0{,}33$, xác nhận $P(\text{cả hai là gái}\mid\text{ít nhất một là gái})=1/3$.

#### Mô phỏng Monty Hall

Nhiều cuộc tranh cãi dai dẳng về Monty Hall có thể tránh được nếu thử mô phỏng. Để xem chiến lược *không bao giờ đổi cửa* hiệu quả ra sao, hãy tạo $10^5$ lượt chơi. Để ký hiệu đơn giản, giả sử người chơi luôn chọn cửa 1. Ta tạo vectơ ghi cửa nào có ô tô ở mỗi lượt:

```r
n <- 10^5
cardoor <- sample(3,n,replace=TRUE)
```

Lúc này ta có thể tạo thêm vectơ ghi Monty mở cửa nào, nhưng không cần: chiến lược không đổi chỉ thắng khi ô tô ở cửa 1! Vì vậy, tỉ lệ thắng là `sum(cardoor==1)/n`; trong mô phỏng của chúng tôi kết quả là $0{,}334$, rất gần $1/3$.

Nếu muốn chơi Monty Hall tương tác thì sao? Ta có thể viết một hàm. Nhập mã sau vào R để định nghĩa hàm `monty`; sau đó, bất cứ khi nào muốn chơi, chỉ cần gọi `monty()`:

```r
monty <- function() {
  doors <- 1:3
  # chọn ngẫu nhiên cửa có ô tô
  cardoor <- sample(doors,1)
  # nhắc người chơi chọn cửa
  print("Monty Hall says ‘Pick a door, any door!’")
  # nhận lựa chọn của người chơi (nên là 1, 2 hoặc 3)
  chosen <- scan(what = integer(), nlines = 1, quiet = TRUE)
  # chọn cửa Monty mở (không thể là cửa đã chọn hoặc cửa có ô tô)
  if (chosen != cardoor) montydoor <- doors[-c(chosen, cardoor)]
  else montydoor <- sample(doors[-chosen],1)
  # hỏi người chơi có muốn đổi cửa không
  print(paste("Monty opens door ", montydoor, "!", sep=""))
  print("Would you like to switch (y/n)?")
  reply <- scan(what = character(), nlines = 1, quiet = TRUE)
  # coi câu trả lời là có nếu bắt đầu bằng "y"
  if (substr(reply,1,1) == "y") chosen <- doors[-c(chosen,montydoor)]
  # thông báo kết quả
  if (chosen == cardoor) print("You won!")
  else print("You lost!")
}
```

Lệnh `print` in đối số ra màn hình. Ta kết hợp với `paste` vì `print("Monty opens door montydoor")` sẽ in nguyên văn “Monty opens door montydoor”. Lệnh `scan` yêu cầu người dùng nhập dữ liệu khi chương trình chạy; dùng `what = integer()` khi muốn nhập số nguyên, `what = character()` khi muốn nhập văn bản. `substr(reply,1,1)` lấy ký tự đầu của câu trả lời, phòng trường hợp người chơi nhập `yes`, `yep` hoặc `yeah!` thay vì chỉ `y`.

### 2.11. Bài tập (từ trang PDF 92)

#### Đặt điều kiện theo bằng chứng

**1.** Một bộ lọc thư rác được thiết kế dựa trên những cụm từ thường xuất hiện trong thư rác. Giả sử 80% thư điện tử là thư rác. Trong 10% thư rác có cụm “free money” (tiền miễn phí), còn chỉ 1% thư hợp lệ có cụm này. Một thư mới đến có chứa “free money”. Xác suất nó là thư rác là bao nhiêu?

**2.** Một phụ nữ đang mang thai đôi hai bé trai. Các cặp sinh đôi có thể là cùng trứng hoặc khác trứng. Nói chung, một phần ba số cặp sinh đôi được sinh ra là cùng trứng. Cặp cùng trứng tất nhiên cùng giới tính; cặp khác trứng có thể cùng hoặc khác giới tính. Giả sử các cặp cùng trứng có khả năng là hai trai hoặc hai gái như nhau; với cặp khác trứng, mọi khả năng giới tính đều như nhau. Theo thông tin trên, xác suất cặp sinh đôi của người phụ nữ là cùng trứng bằng bao nhiêu?

**3.** Theo Trung tâm Kiểm soát và Phòng ngừa Dịch bệnh Hoa Kỳ (CDC), nam giới hút thuốc có khả năng mắc ung thư phổi cao gấp 23 lần nam giới không hút thuốc. CDC cũng cho biết 21,6% nam giới ở Hoa Kỳ hút thuốc. Xác suất một người đàn ông ở Hoa Kỳ hút thuốc là bao nhiêu, nếu biết ông ấy mắc ung thư phổi?

**4.** Fred đang trả lời một câu trắc nghiệm có $n$ lựa chọn, trong đó đúng một lựa chọn là đáp án đúng. Gọi $K$ là biến cố Fred biết đáp án, $R$ là biến cố anh trả lời đúng (nhờ biết hoặc nhờ may mắn). Giả sử nếu biết thì Fred chắc chắn trả lời đúng; nếu không biết, anh đoán hoàn toàn ngẫu nhiên. Cho $P(K)=p$.

(a) Tìm $P(K\mid R)$ theo $p,n$.

(b) Chứng minh $P(K\mid R)\ge p$ và giải thích bằng trực giác. Khi nào, nếu có, $P(K\mid R)=p$?

**5.** Chia ba lá từ bộ bài chuẩn đã xáo kỹ. Lật hai lá đầu, thấy lá đầu là át bích, lá thứ hai là 8 tép. Theo thông tin đó, hãy tìm xác suất lá thứ ba là át theo hai cách: dùng định nghĩa xác suất có điều kiện và dùng tính đối xứng.

**6.** Một chiếc mũ chứa 100 đồng xu, trong đó 99 đồng cân đối và một đồng có cả hai mặt đều là mặt ngửa (luôn ra ngửa). Chọn ngẫu nhiên đều một đồng xu rồi tung 7 lần; cả 7 lần đều ra ngửa. Theo thông tin này, xác suất đã chọn đồng xu hai mặt ngửa là bao nhiêu? (Dĩ nhiên cũng có thể nhìn cả hai mặt đồng xu, nhưng đây là một đồng xu mang tính ẩn dụ.)

**7.** Một chiếc mũ chứa 100 đồng xu; ít nhất 99 đồng cân đối, nhưng có thể có một đồng hai mặt ngửa (luôn ra ngửa). Nếu không có đồng đặc biệt đó thì cả 100 đồng đều cân đối. Gọi $D$ là biến cố tồn tại đồng hai mặt ngửa, và giả sử $P(D)=1/2$. Chọn ngẫu nhiên đều một đồng xu rồi tung 7 lần; cả 7 lần đều ra ngửa.

(a) Theo thông tin này, xác suất trong mũ có một đồng hai mặt ngửa là bao nhiêu?

(b) Theo thông tin này, xác suất đồng đã chọn là đồng hai mặt ngửa là bao nhiêu?

**8.** Màn hình của một loại điện thoại di động do ba công ty $A,B,C$ sản xuất. Tỉ lệ màn hình họ cung cấp lần lượt là $0{,}5$, $0{,}3$ và $0{,}2$; xác suất màn hình bị lỗi của từng công ty lần lượt là $0{,}01$, $0{,}02$ và $0{,}03$. Biết màn hình của một chiếc điện thoại loại này bị lỗi, xác suất nó do công ty $A$ sản xuất là bao nhiêu?

**9.** (a) Hãy chứng minh: nếu $P(A_1)=P(A_2)$, $A_1$ kéo theo $B$ và $A_2$ cũng kéo theo $B$, thì sau khi biết $B$ xảy ra, hai xác suất hậu nghiệm vẫn bằng nhau: $P(A_1\mid B)=P(A_2\mid B)$. (b) Giải thích vì sao (a) hợp lý về mặt trực giác và nêu một ví dụ cụ thể.

**10.** Fred thực hiện một dự án lớn. Khi lập kế hoạch, anh đặt hai mốc tiến độ với ngày cần hoàn thành để theo dõi công việc. Gọi $A_1$ là biến cố Fred hoàn thành mốc thứ nhất đúng hạn, $A_2$ là biến cố hoàn thành mốc thứ hai đúng hạn, $A_3$ là biến cố hoàn thành toàn dự án đúng hạn.

Giả sử $P(A_{j+1}\mid A_j)=0{,}8$, nhưng $P(A_{j+1}\mid A_j^c)=0{,}3$ với $j=1,2$, vì khi đã chậm tiến độ, Fred khó bắt kịp. Cũng giả sử mốc thứ hai thay thế mốc thứ nhất: một khi đã biết anh có hoàn thành mốc hai đúng hạn hay không, tình trạng ở mốc một không còn quan trọng. Ta diễn đạt bằng cách nói $A_1,A_3$ độc lập có điều kiện theo $A_2$, và cũng độc lập có điều kiện theo $A_2^c$.

(a) Tìm xác suất Fred hoàn thành dự án đúng hạn khi biết anh hoàn thành mốc đầu đúng hạn. Đồng thời, tìm xác suất ấy khi biết anh trễ mốc đầu.

(b) Giả sử $P(A_1)=0{,}75$. Tìm xác suất Fred hoàn thành dự án đúng hạn.

**11.** *Thăm dò tại điểm bỏ phiếu* là khảo sát cử tri ngay sau khi họ bỏ phiếu. Một ứng dụng lớn của loại khảo sát này là giúp các hãng tin tìm người thắng sớm nhất có thể, trước khi kiểm phiếu chính thức. Trong nhiều cuộc bầu cử, dự đoán kiểu này đã sai nghiêm trọng, đôi khi vì *thiên lệch chọn mẫu*: những người được mời và đồng ý trả lời khảo sát không đủ giống toàn bộ cử tri.

Xét cuộc bầu cử giữa hai ứng cử viên $A$ và $B$. Mọi cử tri đều được mời tham gia thăm dò tại điểm bỏ phiếu và được hỏi họ đã chọn ai; một số đồng ý, số khác từ chối. Với một cử tri chọn ngẫu nhiên, gọi $A$ là biến cố người đó bỏ phiếu cho ứng cử viên $A$ và $W$ là biến cố người đó sẵn lòng tham gia khảo sát. Giả sử $P(W\mid A)=0{,}7$, nhưng $P(W\mid A^c)=0{,}3$. Trong cuộc thăm dò, 60% người trả lời nói họ đã bỏ phiếu cho $A$ (giả sử họ đều nói thật), gợi ý $A$ thắng khá cách biệt. Hãy tìm $P(A)$, tỉ lệ thực tế cử tri bỏ phiếu cho $A$.

**12.** Alice muốn gửi cho Bob một thông điệp mã hóa nhị phân qua một kênh truyền.

(a) Trong ý này, giả sử Alice chỉ gửi một bit (0 hoặc 1), hai giá trị có xác suất bằng nhau. Nếu cô gửi 0, có 5% khả năng lỗi khiến Bob nhận 1; nếu cô gửi 1, có 10% khả năng lỗi khiến Bob nhận 0. Biết Bob nhận 1, xác suất Alice thật sự gửi 1 là bao nhiêu?

(b) Để giảm nguy cơ truyền sai, Alice và Bob quyết định dùng mã lặp. Alice vẫn muốn truyền 0 hoặc 1, nhưng lần này lặp thêm hai lần: gửi `000` để truyền 0, `111` để truyền 1. Bob giải mã bằng cách chọn giá trị xuất hiện đa số. Giả sử xác suất lỗi như ở (a), và các lỗi ở từng bit độc lập. Biết Bob nhận `110`, xác suất Alice định truyền 1 là bao nhiêu?

**13.** Công ty $A$ vừa phát triển một xét nghiệm chẩn đoán một bệnh ảnh hưởng 1% dân số. Như định nghĩa ở Ví dụ 2.3.9, *độ nhạy* là xác suất xét nghiệm dương tính khi người đó có bệnh, còn *độ đặc hiệu* là xác suất xét nghiệm âm tính khi người đó không bệnh. Giả sử độ nhạy và độ đặc hiệu đều bằng $0{,}95$.

Công ty đối thủ $B$ đưa ra một xét nghiệm cạnh tranh. Công ty $B$ nói xét nghiệm của họ nhanh hơn, rẻ hơn, ít đau hơn (xét nghiệm của $A$ phải rạch da), nhưng có *tỉ lệ chẩn đoán đúng chung* cao hơn, trong đó tỉ lệ chung là xác suất một người chọn ngẫu nhiên được chẩn đoán chính xác.

(a) Hóa ra xét nghiệm của $B$ có thể mô tả và thực hiện rất đơn giản: bất kể bệnh nhân là ai, cứ kết luận họ *không* mắc bệnh. Hãy kiểm tra tuyên bố của $B$ về tỉ lệ chẩn đoán đúng chung.

(b) Giải thích vì sao xét nghiệm của $A$ vẫn có thể hữu ích.

(c) Công ty $A$ muốn phát triển xét nghiệm mới có tỉ lệ chẩn đoán đúng chung cao hơn xét nghiệm của $B$. Nếu độ nhạy bằng độ đặc hiệu, giá trị này phải cao bao nhiêu? Nếu (thật kỳ diệu) họ làm độ nhạy bằng 1, độ đặc hiệu phải cao bao nhiêu? Nếu (thật kỳ diệu) họ làm độ đặc hiệu bằng 1, độ nhạy phải cao bao nhiêu?

**14.** Xét tình huống sau từ Tversky và Kahneman [30]: gọi $A$ là biến cố Peter lắp hệ thống chống trộm trong nhà trước cuối năm sau; gọi $B$ là biến cố nhà Peter bị trộm trước cuối năm sau.

(a) Theo trực giác, bạn nghĩ $P(A\mid B)$ hay $P(A\mid B^c)$ lớn hơn? Hãy giải thích.

(b) Theo trực giác, bạn nghĩ $P(B\mid A)$ hay $P(B\mid A^c)$ lớn hơn? Hãy giải thích.

(c) Hãy chứng minh với mọi biến cố $A,B$ có xác suất khác 0 và 1 rằng $P(A\mid B)>P(A\mid B^c)$ tương đương $P(B\mid A)>P(B\mid A^c)$.

(d) Tversky và Kahneman cho biết 131 trong 162 người được hỏi (a) và (b) đã trả lời $P(A\mid B)>P(A\mid B^c)$ đồng thời $P(B\mid A)<P(B\mid A^c)$. Hãy nêu một lời giải thích hợp lý vì sao ý kiến ấy phổ biến đến vậy, dù (c) cho thấy hai bất đẳng thức không thể cùng đúng.

**15.** Cho hai biến cố $A,B$ thỏa $0<P(A\cap B)<P(A)<P(B)<P(A\cup B)<1$. Bạn mong cả $A$ lẫn $B$ đều đã xảy ra. Trong các thông tin sau, bạn sẽ vui nhất khi biết điều nào: $A$ đã xảy ra, $B$ đã xảy ra, hay $A\cup B$ đã xảy ra?

**16.** Hãy chứng minh $P(A\mid B)\le P(A)$ kéo theo $P(A\mid B^c)\ge P(A)$, rồi giải thích bằng trực giác vì sao điều này hợp lý.

**17.** Trong logic tất định, phát biểu “$A$ kéo theo $B$” tương đương với phản đảo của nó, “không $B$ kéo theo không $A$”. Trong bài này, ta xét các phát biểu tương tự trong xác suất, logic của sự bất định. Cho $A,B$ có xác suất khác 0 và 1.

(a) Hãy chứng minh nếu $P(B\mid A)=1$ thì $P(A^c\mid B^c)=1$. *Gợi ý:* Dùng quy tắc Bayes và định luật xác suất toàn phần.

(b) Tuy nhiên, chứng minh kết quả (a) không còn đúng nói chung nếu thay dấu $=$ bằng “xấp xỉ”. Cụ thể, tìm ví dụ trong đó $P(B\mid A)$ rất gần 1 nhưng $P(A^c\mid B^c)$ rất gần 0. *Gợi ý:* Điều gì xảy ra nếu $A,B$ độc lập?

**18.** Hãy chứng minh nếu $P(A)=1$ thì $P(A\mid B)=1$ với mọi $B$ thỏa $P(B)>0$. Trực giác: nếu ai đó tin một điều chắc chắn tuyệt đối theo kiểu giáo điều, không bằng chứng nào sẽ thay đổi suy nghĩ của họ. Nhà thống kê Dennis Lindley gọi nguyên tắc tránh gán xác suất 0 hoặc 1 cho mọi biến cố (ngoại trừ những điều chắc chắn về toán học) là *quy tắc Cromwell*, theo lời Cromwell nói với Giáo hội Scotland: “Hãy nghĩ rằng có thể chính quý vị đã nhầm.” *Gợi ý:* Viết $P(B)=P(B\cap A)+P(B\cap A^c)$, rồi chứng minh $P(B\cap A^c)=0$.

**19.** Hãy giải thích câu nói sau của Sherlock Holmes bằng xác suất có điều kiện, phân biệt cẩn thận giữa xác suất tiên nghiệm và hậu nghiệm: “Đây là châm ngôn cũ của tôi: khi đã loại trừ điều không thể, phần còn lại, dù khó tin đến đâu, hẳn phải là sự thật.”

**20.** Lấy từ bộ bài bốn lá: bồi bích (với rượu táo), bồi cơ (với bánh tart), đầm bích (nháy mắt), đầm cơ (không có bánh tart). Xáo bốn lá rồi chia hai lá.

(a) Tìm xác suất cả hai lá là đầm, biết lá đầu là đầm.

(b) Tìm xác suất cả hai lá là đầm, biết ít nhất một lá là đầm.

(c) Tìm xác suất cả hai lá là đầm, biết một trong hai là đầm cơ.

**21.** Tung đồng xu cân đối 3 lần. Ghi mỗi kết quả lên một mảnh giấy riêng (`H` nếu ngửa, `T` nếu sấp) rồi bỏ cả ba mảnh vào mũ.

(a) Tìm xác suất cả 3 lần đều ra ngửa, biết ít nhất 2 lần ra ngửa.

(b) Rút ngẫu nhiên hai mảnh giấy từ mũ; cả hai đều ghi `H`. Theo thông tin này, xác suất cả 3 lần tung đều ra ngửa là bao nhiêu?

**22.** Một chiếc túi chứa một viên bi xanh lá hoặc xanh dương, hai khả năng bằng nhau. Bỏ thêm một viên bi xanh lá vào túi (giờ có hai viên), rồi rút ngẫu nhiên một viên. Viên rút ra màu xanh lá. Xác suất viên còn lại cũng xanh lá là bao nhiêu?

**23.** Gọi $G$ là biến cố một người cụ thể có tội trong một vụ cướp. Khi thu thập bằng chứng, người ta biết biến cố $E_1$ đã xảy ra; một lúc sau lại biết thêm $E_2$ xảy ra. Có thể nào từng bằng chứng riêng lẻ đều làm tăng xác suất có tội ($P(G\mid E_1)>P(G)$ và $P(G\mid E_2)>P(G)$), nhưng khi xét chung lại làm xác suất có tội giảm ($P(G\mid E_1,E_2)<P(G)$)?

**24.** Có thể có các biến cố $A_1,A_2,B,C$ sao cho $P(A_1\mid B)>P(A_1\mid C)$ và $P(A_2\mid B)>P(A_2\mid C)$, nhưng $P(A_1\cup A_2\mid B)<P(A_1\cup A_2\mid C)$ không? Nếu có, hãy nêu ví dụ gồm một câu chuyện diễn giải các biến cố và các con số cụ thể; nếu không, hãy chứng minh điều đó bất khả thi.

**25.** Một trong hai nghi phạm $A,B$ đã gây ra một vụ án. Ban đầu, bằng chứng chống lại họ ngang nhau. Điều tra thêm tại hiện trường cho thấy thủ phạm mang nhóm máu có ở 10% dân số. Nghi phạm $A$ có nhóm máu này; chưa biết nhóm máu của $B$.

(a) Theo thông tin mới, xác suất $A$ là thủ phạm là bao nhiêu?

(b) Theo thông tin mới, xác suất nhóm máu của $B$ cũng trùng với nhóm máu tìm thấy ở hiện trường là bao nhiêu?

**26.** Để chống thư rác, Bob cài hai chương trình lọc. Một thư đến có thể hợp lệ (biến cố $L$) hoặc là thư rác (biến cố $L^c$). Chương trình $j$ có thể đánh dấu thư là hợp lệ (biến cố $M_j$) hoặc thư rác (biến cố $M_j^c$), với $j\in\{1,2\}$. Giả sử 10% thư Bob nhận là thư hợp lệ và mỗi chương trình “chính xác 90%” theo nghĩa $P(M_j\mid L)=P(M_j^c\mid L^c)=9/10$. Cũng giả sử khi đã biết thư có phải thư rác hay không, kết quả của hai chương trình độc lập có điều kiện.

(a) Tìm và rút gọn xác suất thư hợp lệ, biết chương trình thứ nhất đánh dấu nó là hợp lệ.

(b) Tìm và rút gọn xác suất thư hợp lệ, biết *cả hai* chương trình đều đánh dấu là hợp lệ.

(c) Bob chạy chương trình thứ nhất và $M_1$ xảy ra. Anh cập nhật xác suất rồi chạy chương trình thứ hai. Gọi $\widetilde P(A)=P(A\mid M_1)$ là hàm xác suất sau khi chạy chương trình thứ nhất. Hãy giải thích ngắn gọn bằng lời liệu $\widetilde P(L\mid M_2)=P(L\mid M_1\cap M_2)$ có đúng không: đặt điều kiện một lần theo $M_1\cap M_2$ có tương đương với đặt điều kiện theo $M_1$, cập nhật xác suất, rồi đặt điều kiện theo $M_2$?

**27.** Giả sử quần thể có 5 nhóm máu, đặt tên loại 1 đến loại 5, với xác suất lần lượt $p_1,p_2,\ldots,p_5$. Một vụ án do hai người cùng gây ra. Một nghi phạm có nhóm máu loại 1, với xác suất tiên nghiệm có tội bằng $p$. Bằng chứng máu tại hiện trường cho thấy một thủ phạm thuộc loại 1, người kia thuộc loại 2.

Hãy tìm xác suất hậu nghiệm nghi phạm có tội theo bằng chứng này. Bằng chứng làm khả năng nghi phạm có tội tăng hay giảm, hay còn tùy các tham số $p,p_1,\ldots,p_5$? Nếu còn tùy, hãy đưa ra một điều kiện đơn giản để bằng chứng làm khả năng có tội tăng.

**28.** Fred vừa có kết quả dương tính với một bệnh.

(a) Theo thông tin này, hãy tìm tỉ lệ cược hậu nghiệm rằng Fred mắc bệnh theo tỉ lệ cược tiên nghiệm, độ nhạy và độ đặc hiệu của xét nghiệm.

(b) Dĩ nhiên, Fred quan tâm đến $P(\text{mắc bệnh}\mid\text{xét nghiệm dương tính})$, gọi là *giá trị tiên đoán dương*, hơn là độ nhạy $P(\text{xét nghiệm dương tính}\mid\text{mắc bệnh})$. Một quy tắc kinh nghiệm hữu ích trong thống kê sinh học và dịch tễ học là: **với bệnh hiếm và xét nghiệm tương đối tốt, độ đặc hiệu ảnh hưởng đến giá trị tiên đoán dương nhiều hơn độ nhạy**. Hãy giải thích bằng trực giác vì sao quy tắc này đúng. Có thể tự chọn các con số cụ thể và hiểu xác suất theo tần suất như tỉ lệ trong một quần thể lớn; chẳng hạn giả sử bệnh ảnh hưởng 1% của 10.000 người, rồi xét các mức độ nhạy và độ đặc hiệu khác nhau.

**29.** Một gia đình có hai con. Gọi $C$ là một đặc điểm mà trẻ có thể có; giả sử mỗi người con có đặc điểm $C$ với xác suất $p$, độc lập với người kia và với giới tính. Chẳng hạn, $C$ có thể là “sinh mùa đông” như Ví dụ 2.2.7. Hãy chứng minh xác suất cả hai con là gái khi biết có ít nhất một bé gái mang đặc điểm $C$ bằng $(2-p)/(4-p)$. Giá trị này bằng $1/3$ khi $p=1$ (khớp phần đầu Ví dụ 2.2.5) và tiến đến $1/2$ từ phía dưới khi $p\to0$ (khớp Ví dụ 2.2.7).

#### Độc lập và độc lập có điều kiện

**30.** Một gia đình có 3 người con, được đặt tên đầy sáng tạo là $A,B,C$. (a) Hãy bàn bằng trực giác nhưng rõ ràng xem biến cố “$A$ lớn tuổi hơn $B$” có độc lập với biến cố “$A$ lớn tuổi hơn $C$” hay không. (b) Tìm xác suất $A$ lớn tuổi hơn $B$ khi biết $A$ lớn tuổi hơn $C$.

**31.** Một biến cố có thể độc lập với chính nó không? Nếu có, trong trường hợp nào?

**32.** Xét bốn con xúc xắc không chuẩn (xúc xắc Efron), có các mặt ghi số như sau; sáu mặt của mỗi con có khả năng ra như nhau:

| Xúc xắc | Sáu mặt |
|---|---|
| $A$ | 4, 4, 4, 4, 0, 0 |
| $B$ | 3, 3, 3, 3, 3, 3 |
| $C$ | 6, 6, 2, 2, 2, 2 |
| $D$ | 5, 5, 5, 1, 1, 1 |

Gieo mỗi con một lần. Gọi $A,B,C,D$ cũng là kết quả của từng con tương ứng. (a) Tìm $P(A>B)$, $P(B>C)$, $P(C>D)$ và $P(D>A)$. (b) Biến cố $A>B$ có độc lập với $B>C$ không? Biến cố $B>C$ có độc lập với $C>D$ không? Hãy giải thích.

**33.** Alice, Bob và 100 người khác sống trong một thị trấn nhỏ. Gọi $C$ là tập hợp 100 người kia; $A$ là tập những người trong $C$ là bạn Alice, $B$ là tập những người trong $C$ là bạn Bob. Giả sử với mỗi người thuộc $C$, Alice có xác suất $1/2$ kết bạn với người ấy; Bob cũng vậy; mọi trạng thái kết bạn đều độc lập.

(a) Cho $D\subseteq C$. Tìm $P(A=D)$.

(b) Tìm $P(A\subseteq B)$.

(c) Tìm $P(A\cup B=C)$.

**34.** Giả sử có hai loại người lái xe: giỏi và kém. Gọi $G$ là biến cố một người đàn ông nhất định lái xe giỏi, $A$ là biến cố ông gặp tai nạn ô tô năm tới, $B$ là biến cố ông gặp tai nạn năm sau nữa. Cho $P(G)=g$, $P(A\mid G)=P(B\mid G)=p_1$ và $P(A\mid G^c)=P(B\mid G^c)=p_2$, với $p_1<p_2$. Giả sử khi đã biết ông ấy lái xe giỏi hay kém, $A,B$ độc lập. Để đơn giản và tránh chi tiết bi thảm, giả sử các tai nạn được xét chỉ nhẹ và không khiến ông mất khả năng lái xe.

(a) Hãy giải thích bằng trực giác xem $A,B$ có độc lập vô điều kiện hay không.

(b) Tìm $P(G\mid A^c)$.

(c) Tìm $P(B\mid A^c)$.

**35.** Bạn sẽ đấu hai ván cờ vua với một đối thủ chưa từng gặp. Đối thủ có khả năng ngang nhau thuộc một trong ba trình độ: mới học, trung cấp hoặc cao thủ. Tùy trình độ, xác suất bạn thắng mỗi ván lần lượt là 90%, 50% hoặc 30%.

(a) Xác suất bạn thắng ván đầu là bao nhiêu?

(b) Chúc mừng: bạn thắng ván đầu! Theo thông tin đó, xác suất bạn cũng thắng ván hai là bao nhiêu? Giả sử khi biết trình độ đối thủ, kết quả các ván độc lập.

(c) Hãy phân biệt giả định kết quả các ván độc lập vô điều kiện với giả định chúng độc lập có điều kiện theo trình độ đối thủ. Giả định nào hợp lý hơn, và vì sao?

**36.** (a) Giả sử trong quần thể người nộp hồ sơ đại học, giỏi bóng chày độc lập với đạt điểm toán cao trong một bài thi chuẩn hóa (theo một tiêu chuẩn “giỏi” nào đó). Một trường có quy trình tuyển sinh đơn giản: nhận người nộp hồ sơ khi và chỉ khi họ giỏi bóng chày *hoặc* có điểm toán cao.

Hãy giải thích bằng trực giác vì sao trong số sinh viên được trường nhận, điểm toán cao lại có mối liên hệ âm với giỏi bóng chày: biết một sinh viên có điểm toán cao làm giảm khả năng người đó giỏi bóng chày.

(b) Chứng minh nếu $A,B$ độc lập và $C=A\cup B$, thì khi biết $C$, $A,B$ phụ thuộc có điều kiện (miễn là $P(A\cap B)>0$ và $P(A\cup B)<1$), với $P(A\mid B,C)<P(A\mid C)$. Hiện tượng này gọi là *nghịch lý Berkson*, đặc biệt trong bối cảnh tuyển vào trường học, bệnh viện, v.v.

**37.** Ta muốn thiết kế bộ lọc thư rác. Như Bài 1 mô tả, một chiến lược quan trọng là tìm các từ hoặc cụm từ xuất hiện trong thư rác thường xuyên hơn nhiều so với thư hợp lệ. Bài 1 chỉ xét một cụm là “free money”. Thực tế hơn, giả sử ta có danh sách 100 từ hoặc cụm từ thường xuất hiện trong thư rác hơn.

Gọi $W_j$ là biến cố thư chứa từ hoặc cụm thứ $j$. Đặt $p=P(\text{thư rác})$, $p_j=P(W_j\mid\text{thư rác})$, và $r_j=P(W_j\mid\text{không phải thư rác})$; “thư rác” ở đây là cách viết gọn của biến cố thư là thư rác.

Giả sử $W_1,\ldots,W_{100}$ độc lập có điều kiện khi biết thư là thư rác, và cũng độc lập có điều kiện khi biết thư không phải thư rác. Phương pháp phân loại thư (hoặc đối tượng khác) dựa trên giả định dạng này gọi là *bộ phân loại Bayes ngây thơ*. “Ngây thơ” chỉ giả định độc lập có điều kiện rất mạnh, chứ không phải Bayes ngây thơ. Giả định ấy có thể đúng hoặc không, nhưng đôi khi bộ phân loại vẫn hoạt động tốt dù giả định không sát thực tế.

Theo giả định này, chẳng hạn, ta có

$$P(W_1,W_2,W_3^c,W_4^c,\ldots,W_{100}^c\mid\text{thư rác})=p_1p_2(1-p_3)(1-p_4)\cdots(1-p_{100}).$$

Nếu không có giả định Bayes ngây thơ, khó khăn về thống kê và tính toán sẽ lớn hơn rất nhiều: ta phải xét $2^{100}\approx1{,}3\times10^{30}$ biến cố dạng $A_1\cap A_2\cap\cdots\cap A_{100}$, trong đó mỗi $A_j$ bằng $W_j$ hoặc $W_j^c$.

Một thư mới đến, chứa mục thứ 23, 64 và 65 trong danh sách, nhưng không chứa 97 mục còn lại. Ta cần tính

$$P(\text{thư rác}\mid W_1^c,\ldots,W_{22}^c,W_{23},W_{24}^c,\ldots,W_{63}^c,W_{64},W_{65},W_{66}^c,\ldots,W_{100}^c).$$

Lưu ý phải đặt điều kiện theo *toàn bộ* bằng chứng, không chỉ việc $W_{23}\cap W_{64}\cap W_{65}$ xảy ra. Hãy tìm xác suất có điều kiện thư mới là thư rác, theo $p$ và các $p_j,r_j$.

#### Monty Hall

**38.** (a) Xét biến thể Monty Hall có 7 cửa. Một cửa có ô tô (bạn muốn), các cửa còn lại có dê (bạn không muốn). Ban đầu, ô tô có khả năng nằm sau mỗi cửa như nhau. Bạn chọn một cửa. Monty Hall mở ba cửa có dê rồi cho bạn quyền đổi sang *bất kỳ* một trong ba cửa chưa mở còn lại.

Giả sử Monty biết ô tô ở đâu, luôn mở ba cửa có dê và luôn cho quyền đổi; khi có nhiều cách chọn ba cửa để mở, ông chọn đều giữa các cách ấy. Bạn có nên đổi không? Nếu đổi sang một trong ba cửa còn lại, xác suất thành công là bao nhiêu?

(b) Khái quát cho $n\ge3$ cửa, Monty mở $m$ cửa có dê, với $1\le m\le n-2$.

**39.** Xét bài toán Monty Hall, nhưng Monty thích mở cửa 2 hơn cửa 3. Nếu được chọn giữa hai cửa ấy, ông mở cửa 2 với xác suất $p$, trong đó $1/2\le p\le1$.

Nhắc lại: có ba cửa, một cửa giấu ô tô (bạn muốn), hai cửa kia giấu dê (bạn không muốn). Ban đầu, ô tô có khả năng nằm sau mỗi cửa như nhau. Bạn chọn cửa 1. Monty mở một cửa để lộ dê rồi cho bạn quyền đổi. Giả sử Monty biết ô tô ở đâu, luôn mở cửa có dê và cho quyền đổi; nếu được chọn giữa cửa 2 và 3, ông chọn cửa 2 với xác suất $p$.

(a) Tìm xác suất không điều kiện chiến lược luôn đổi cửa thành công, tức không đặt điều kiện theo việc Monty mở cửa 2 hay 3.

(b) Tìm xác suất chiến lược luôn đổi cửa thành công khi biết Monty mở cửa 2.

(c) Tìm xác suất chiến lược luôn đổi cửa thành công khi biết Monty mở cửa 3.

**40.** Lượng người xem chương trình của Monty Hall giảm nhẹ. Một nhà sản xuất điều hành hoảng hốt phàn nàn rằng đoạn Monty mở cửa thiếu hồi hộp: ông luôn mở cửa có dê. Monty giải thích làm vậy để không làm hỏng trò chơi bằng việc để lộ ô tô, nhưng đồng ý đổi luật như sau.

Trước mỗi buổi, Monty bí mật tung một đồng xu có xác suất ra ngửa $p$. Nếu ra ngửa, ông quyết định mở một cửa có dê (nếu có lựa chọn thì chọn đều). Nếu không, ông quyết định mở ngẫu nhiên một cửa chưa mở, mỗi cửa có khả năng như nhau.

Người chơi biết $p$ nhưng không biết kết quả đồng xu. Khi chương trình bắt đầu, người chơi chọn một cửa. Monty (biết ô tô ở đâu) mở một cửa. Nếu để lộ ô tô, trò chơi kết thúc; nếu để lộ dê, người chơi được quyền đổi. Giả sử người chơi chọn cửa 1, rồi Monty mở cửa 2 và để lộ dê. Xác suất người chơi thành công nếu đổi sang cửa 3 là bao nhiêu?

**41.** Bạn là người chơi trong chương trình Monty Hall. Monty thử một phiên bản mới với luật sau. Bạn chọn một trong ba cửa: một cửa giấu ô tô, một cửa giấu máy tính, cửa còn lại giấu dê; mọi cách sắp xếp giải thưởng có khả năng như nhau. Monty biết mỗi cửa giấu gì, sẽ mở một cửa khác cửa bạn chọn, rồi cho bạn quyền giữ nguyên hoặc đổi sang cửa chưa mở còn lại.

Giả sử bạn thích ô tô hơn máy tính, máy tính hơn dê, nên ô tô hơn dê.

(a) Chỉ riêng ý này, giả sử Monty luôn mở cửa để lộ giải thưởng bạn *ít thích hơn* trong hai lựa chọn còn lại. Chẳng hạn, nếu phải chọn giữa việc để lộ dê và máy tính, ông mở cửa có dê. Monty mở một cửa và để lộ dê (giả định này cũng chỉ áp dụng cho ý này). Theo thông tin đó, bạn có nên đổi cửa? Nếu đổi, xác suất lấy được ô tô là bao nhiêu?

(b) Giờ giả sử Monty để lộ giải thưởng bạn ít thích hơn với xác suất $p$, giải thưởng bạn thích hơn với xác suất $q=1-p$. Ông mở một cửa và để lộ máy tính. Theo thông tin này, bạn có nên đổi cửa không? Đáp án có thể phụ thuộc $p$. Nếu đổi, xác suất lấy ô tô theo $p$ là bao nhiêu?

#### Phân tích bước đầu và con bạc phá sản

**42.** Gieo đi gieo lại một con xúc xắc cân đối và ghi tổng tích lũy, tức tổng mọi lần gieo từ đầu đến thời điểm đang xét. Gọi $p_n$ là xác suất tổng tích lũy *có lúc* bằng đúng $n$. Giả sử luôn gieo đủ nhiều lần để tổng cuối cùng vượt $n$, dù có thể tổng không bao giờ bằng $n$.

(a) Viết một phương trình đệ quy đơn giản cho $p_n$ theo các giá trị $p_k$ trước đó. Phương trình phải đúng với mọi số nguyên dương $n$, nên hãy định nghĩa $p_0$ và $p_k$ khi $k<0$ sao cho các trường hợp $n$ nhỏ cũng đúng.

(b) Tìm $p_7$.

(c) Giải thích bằng trực giác vì sao $p_n\to1/3{,}5=2/7$ khi $n\to\infty$.

**43.** Thực hiện một dãy $n\ge1$ phép thử độc lập, mỗi phép thử hoặc “thành công” hoặc “thất bại” (không thể đồng thời cả hai). Gọi $p_i$ là xác suất thành công ở lần thứ $i$, $q_i=1-p_i$ và $b_i=q_i-1/2$, với $i=1,2,\ldots,n$. Gọi $A_n$ là biến cố số lần thành công là số chẵn.

(a) Chứng minh với $n=2$, $P(A_2)=1/2+2b_1b_2$.

(b) Chứng minh bằng quy nạp $P(A_n)=1/2+2^{n-1}b_1b_2\cdots b_n$. Kết quả này rất hữu ích trong mật mã học. Nó cũng cho thấy nếu tung $n$ đồng xu, xác suất có số mặt ngửa chẵn bằng $1/2$ khi và chỉ khi ít nhất một đồng xu cân đối. *Gợi ý:* Gộp một số phép thử thành một “siêu phép thử”.

(c) Kiểm tra trực tiếp kết quả (b) trong các trường hợp đơn giản: có $p_i=1/2$ với một $i$; mọi $p_i=0$; mọi $p_i=1$.

**44.** Calvin và Hobbes đấu một trận gồm nhiều ván; Calvin thắng mỗi ván với xác suất $p$, độc lập giữa các ván. Họ dùng luật “thắng cách biệt hai ván”: người đầu tiên thắng nhiều hơn đối thủ hai ván là người thắng trận. Hãy tìm xác suất Calvin thắng trận theo $p$ bằng hai cách: (a) đặt điều kiện và dùng định luật xác suất toàn phần; (b) xem đây là một bài toán con bạc phá sản.

**45.** Một con bạc liên tục chơi trò mà mỗi lượt anh được thêm 1 đô la với xác suất $1/3$, mất 1 đô la với xác suất $2/3$. Chiến lược của anh là “dừng khi lãi 2 đô la”, dù có người vẫn nghi anh nghiện cờ bạc. Giả sử ban đầu anh có một triệu đô la. Hãy chứng minh xác suất anh *từng* lãi 2 đô la nhỏ hơn $1/4$.

**46.** Như trong bài toán con bạc phá sản, hai con bạc $A,B$ đặt cược liên tiếp đến khi một người hết tiền. Ban đầu $A$ có $i$ đô la, $B$ có $N-i$ đô la; $A$ thắng mỗi lượt với xác suất $p$, trong đó $0<p<1/2$. Mỗi lượt cược $1/k$ đô la, với $k$ nguyên dương: $k=1$ là bài toán gốc, $k=20$ nghĩa là mỗi lượt cược 5 xu. Tìm xác suất $A$ thắng cả trò chơi và xác định điều gì xảy ra với xác suất ấy khi $k\to\infty$.

**47.** Có 100 điểm cách đều nhau trên một đường tròn. Ở 99 điểm có cừu; tại điểm còn lại có sói. Mỗi bước, sói ngẫu nhiên đi theo chiều kim đồng hồ hoặc ngược chiều kim đồng hồ một điểm. Nếu điểm nó đến có cừu thì nó ăn cừu. Cừu đứng yên. Xác suất con cừu ban đầu ở đối diện sói là con cuối cùng còn sống bằng bao nhiêu?

**48.** Một người say rượu bất tử đi lang thang ngẫu nhiên trên các số nguyên. Ban đầu ở gốc 0; mỗi bước anh đi sang phải một đơn vị với xác suất $p$ hoặc sang trái một đơn vị với xác suất $q=1-p$, độc lập với mọi bước trước. Gọi $S_n$ là vị trí sau $n$ bước.

(a) Gọi $p_k$ là xác suất anh *từng* đến vị trí $k$, với mọi $k\ge0$. Hãy viết một phương trình sai phân cho $p_k$; ý này chưa cần giải phương trình.

(b) Tìm và rút gọn hoàn toàn $p_k$; nhớ xét cả ba trường hợp $p<1/2$, $p=1/2$ và $p>1/2$. Có thể dùng kết quả sau mà không cần chứng minh: nếu $A_1,A_2,\ldots$ là các biến cố với $A_j\subseteq A_{j+1}$ cho mọi $j$, thì $P(A_n)\to P(\bigcup_{j=1}^{\infty}A_j)$ khi $n\to\infty$. Kết quả này đúng và được gọi là *tính liên tục của xác suất*.

#### Nghịch lý Simpson

**49.** (a) Có thể có các biến cố $A,B,C$ sao cho $P(A\mid C)<P(B\mid C)$ và $P(A\mid C^c)<P(B\mid C^c)$, nhưng $P(A)>P(B)$ không? Nói cách khác, dù biết $C$ đúng hay sai thì $A$ đều ít khả năng hơn $B$, nhưng khi không biết gì về $C$ thì $A$ lại nhiều khả năng hơn $B$. Hãy chứng minh ngắn gọn điều này bất khả thi hoặc nêu phản ví dụ có câu chuyện diễn giải $A,B,C$.

(b) Nếu tình huống (a) có thể xảy ra, nó là trường hợp riêng của nghịch lý Simpson, tương đương với nghịch lý Simpson, hay không thuộc cả hai? Nếu không thể xảy ra, hãy giải thích bằng trực giác vì sao, dù nghịch lý Simpson vẫn có thể xảy ra.

**50.** Xét cuộc đối thoại sau trong một tập phim *The Simpsons*:

> **Lisa:** Bố ơi, con nghĩ ông ấy buôn ngà voi! Ủng của ông ấy bằng ngà voi, mũ cũng bằng ngà voi, và con khá chắc tấm séc kia cũng bằng ngà voi.
>
> **Homer:** Lisa, một người có rất nhiều ngà voi sẽ ít có khả năng làm hại Stampy hơn người có ít ngà voi.

Ở đây Homer và Lisa tranh luận liệu người đàn ông tên Blackheart có khả năng làm hại con voi Stampy nếu họ bán Stampy cho ông ta hay không. Họ rõ ràng bất đồng về cách dùng quan sát về Blackheart để suy luận xác suất ông ta làm hại Stampy khi đã biết bằng chứng.

(a) Hãy đặt ký hiệu rõ ràng cho các biến cố liên quan.

(b) Diễn đạt lập luận của Lisa (một phần ngầm hiểu) và Homer thành các phát biểu xác suất có điều kiện theo ký hiệu ở (a).

(c) Giả sử đúng là người đã có nhiều một loại hàng hóa sẽ ít muốn có thêm loại đó. Hãy giải thích Homer sai ở đâu khi suy luận rằng bằng chứng về Blackheart làm khả năng ông ta gây hại cho Stampy giảm đi.

**51.** (a) Có hai lọ màu đỏ thẫm, ký hiệu $C_1,C_2$, và hai lọ màu tím nhạt, ký hiệu $M_1,M_2$. Mỗi lọ chứa kẹo dẻo hình gấu màu xanh lá và màu đỏ. Hãy nêu ví dụ cho thấy có thể xảy ra tình huống: tỉ lệ kẹo xanh ở $C_1$ cao hơn hẳn $M_1$, và tỉ lệ xanh ở $C_2$ cũng cao hơn hẳn $M_2$; nhưng nếu trộn $C_1,C_2$ vào một lọ mới, đồng thời trộn $M_1,M_2$ vào lọ khác, thì lọ trộn hai lọ đỏ thẫm lại có tỉ lệ kẹo xanh *thấp hơn* lọ trộn hai lọ tím nhạt.

(b) Giải thích (a) liên quan thế nào đến nghịch lý Simpson: vừa bằng trực giác, vừa bằng cách xác định rõ các biến cố $A,B,C$ như trong phát biểu nghịch lý.

**52.** Như đã giải thích trong chương, nghịch lý Simpson cho phép có các biến cố $A,B,C$ sao cho $P(A\mid B,C)<P(A\mid B^c,C)$ và $P(A\mid B,C^c)<P(A\mid B^c,C^c)$, nhưng $P(A\mid B)>P(A\mid B^c)$.

(a) Nghịch lý Simpson có thể xảy ra nếu $A,B$ độc lập không? Nếu có, hãy nêu ví dụ cụ thể gồm số liệu và cách diễn giải; nếu không, hãy chứng minh.

(b) Câu hỏi tương tự nếu $A,C$ độc lập.

(c) Câu hỏi tương tự nếu $B,C$ độc lập.

**53.** Trong cuốn *Red State, Blue State, Rich State, Poor State* của Andrew Gelman [13] có hiện tượng bầu cử sau: trong bất kỳ bang nào ở Hoa Kỳ, một cử tri giàu có nhiều khả năng bầu cho đảng Cộng hòa hơn cử tri nghèo; nhưng các bang giàu hơn lại có xu hướng ủng hộ ứng cử viên đảng Dân chủ! Nói ngắn gọn: cá nhân giàu (ở bất kỳ bang nào) thường bầu Cộng hòa, trong khi bang có tỉ lệ người giàu cao hơn thường ủng hộ Dân chủ.

(a) Để đơn giản, giả sử chỉ có hai bang tên Đỏ và Xanh, mỗi bang 100 người. Mỗi người hoặc giàu hoặc nghèo, và hoặc theo Dân chủ hoặc theo Cộng hòa. Hãy tự đặt các con số phù hợp để cho thấy hiện tượng trên có thể xảy ra: lập một bảng $2\times2$ cho mỗi bang, ghi số người Dân chủ giàu, v.v.

(b) Trong tình huống (a), không nhất thiết dùng đúng số bạn vừa đặt, gọi $D$ là biến cố một người chọn ngẫu nhiên là người Dân chủ (mọi người trong 200 người có khả năng được chọn như nhau), và $B$ là biến cố người đó sống ở bang Xanh. Giả sử 10 người chuyển từ bang Xanh sang bang Đỏ. Ký hiệu $P_{\text{cũ}}$ và $P_{\text{mới}}$ là xác suất trước và sau khi chuyển. Giả sử không ai đổi đảng, nên $P_{\text{mới}}(D)=P_{\text{cũ}}(D)$. Có thể đồng thời có $P_{\text{mới}}(D\mid B)>P_{\text{cũ}}(D\mid B)$ và $P_{\text{mới}}(D\mid B^c)>P_{\text{cũ}}(D\mid B^c)$ không? Nếu có, hãy giải thích vì sao và vì sao điều đó không mâu thuẫn với định luật xác suất toàn phần $P(D)=P(D\mid B)P(B)+P(D\mid B^c)P(B^c)$; nếu không, hãy chứng minh không thể.

#### Bài tập tổng hợp

**54.** Fred quyết định làm $n$ xét nghiệm để xem mình có mắc một bệnh nào đó không. Mỗi xét nghiệm riêng lẻ không hoàn toàn tin cậy, nên anh hy vọng nhiều xét nghiệm sẽ giúp giảm bất định. Gọi $D$ là biến cố Fred mắc bệnh, $p=P(D)$ là xác suất tiên nghiệm anh mắc bệnh, và $q=1-p$. Gọi $T_j$ là biến cố xét nghiệm thứ $j$ dương tính.

(a) Trong ý này, giả sử khi đã biết tình trạng bệnh của Fred, kết quả các xét nghiệm độc lập có điều kiện. Đặt $a=P(T_j\mid D)$, $b=P(T_j\mid D^c)$, trong đó $a,b$ không phụ thuộc $j$. Hãy tìm xác suất hậu nghiệm Fred mắc bệnh nếu cả $n$ xét nghiệm đều dương tính.

(b) Giả sử Fred dương tính cả $n$ lần. Tuy nhiên, một số người có một gen khiến họ luôn xét nghiệm dương tính. Gọi $G$ là biến cố Fred mang gen đó. Giả sử $P(G)=1/2$ và $D,G$ độc lập. Nếu Fred không có gen, kết quả các xét nghiệm độc lập có điều kiện theo tình trạng bệnh. Đặt $a'=P(T_j\mid D,G^c)$ và $b'=P(T_j\mid D^c,G^c)$, không phụ thuộc $j$. Hãy tìm xác suất hậu nghiệm Fred mắc bệnh nếu cả $n$ xét nghiệm đều dương tính.

**55.** Một bệnh di truyền có thể truyền từ mẹ sang con. Nếu mẹ mắc bệnh, từng người con độc lập có xác suất mắc bệnh $1/2$. Nếu mẹ không bệnh, các con cũng không bệnh. Một bà mẹ có xác suất mắc bệnh $1/3$ và có hai con.

(a) Tìm xác suất cả hai con đều không bệnh.

(b) Việc con lớn mắc bệnh có độc lập với việc con nhỏ mắc bệnh không? Hãy giải thích.

(c) Người ta xác định con lớn không bệnh. Một tuần sau, con nhỏ cũng được xác định không bệnh. Theo thông tin này, xác suất người mẹ mắc bệnh là bao nhiêu?

**56.** Tung cùng lúc ba đồng xu cân đối. Hãy giải thích lỗi trong lập luận sau: “Có 50% khả năng cả ba đồng cùng cho một mặt, vì hiển nhiên luôn tìm được hai đồng giống nhau, rồi đồng thứ ba có 50% khả năng giống hai đồng ấy.”

**57.** Một bình chứa bóng đỏ, xanh lá và xanh dương. Gọi $r,g,b$ lần lượt là tỉ lệ từng màu, với $r+g+b=1$.

(a) Rút ngẫu nhiên từng quả, có hoàn lại. Tìm xác suất lần đầu rút được bóng xanh lá đến *trước* lần đầu rút được bóng xanh dương. *Gợi ý:* Liên hệ với xác suất một lần rút là xanh lá khi biết nó là xanh lá hoặc xanh dương.

(b) Rút ngẫu nhiên không hoàn lại. Tìm xác suất lần đầu rút được bóng xanh lá đến trước lần đầu rút được bóng xanh dương. Đáp án giống hay khác (a)? *Gợi ý:* Hãy hình dung mọi quả bóng xếp thành một hàng theo thứ tự sẽ được rút. Vị trí bóng đỏ trong hàng không quan trọng.

(c) Khái quát kết quả (a): thực hiện các phép thử độc lập, mỗi kết quả được phân vào đúng một trong các loại $1,2,\ldots,n$ với xác suất tương ứng $p_1,p_2,\ldots,p_n$. Tìm xác suất lần đầu xuất hiện loại $i$ đến trước lần đầu xuất hiện loại $j$, với $i\ne j$.

**58.** Marilyn vos Savant nhận được câu hỏi sau cho chuyên mục trên báo *Parade*:

> Bạn dự tiệc cùng 199 khách khác thì bọn cướp xông vào và tuyên bố sẽ cướp một người. Chúng bỏ vào mũ 199 mảnh giấy trắng và một mảnh ghi “bạn thua”. Mỗi khách phải rút một mảnh; ai rút “bạn thua” sẽ bị cướp. Bọn cướp cho bạn chọn rút đầu tiên, cuối cùng hoặc vào bất kỳ thời điểm nào ở giữa. Bạn sẽ rút lúc nào?

Các lượt rút không hoàn lại, và ở (a) mọi mảnh giấy còn lại có khả năng được rút như nhau.

(a) Để tối đa hóa xác suất không bị cướp, nên rút đầu, rút cuối, rút ở giữa, hay thứ tự không quan trọng? Hãy giải thích rõ, ngắn gọn và thuyết phục.

(b) Tổng quát hơn, giả sử có một mảnh “bạn thua” với “trọng số” $v$ và $n$ mảnh trắng, mỗi mảnh trọng số $w$. Ở mỗi bước, xác suất rút một mảnh cụ thể tỉ lệ với trọng số của nó: bằng trọng số của nó chia tổng trọng số các mảnh còn lại. Hãy xác định nên rút trước hay rút thứ hai, hoặc thứ tự không quan trọng; $v>0,w>0,n\ge1$ là các hằng số đã biết.

**59.** Gọi $D$ là biến cố một người mắc một bệnh và $C$ là biến cố người đó từng tiếp xúc với một chất nào đó (chẳng hạn $D$ là ung thư phổi, $C$ là hút thuốc lá). Ta quan tâm xem tiếp xúc có liên quan đến mắc bệnh hay không, và liên quan thế nào. *Tỉ số odds* là một thước đo rất phổ biến trong dịch tễ học cho mối liên hệ này:

$$\mathrm{OR}=\frac{\operatorname{odds}(D\mid C)}{\operatorname{odds}(D\mid C^c)},\qquad \operatorname{odds}(A\mid B)=\frac{P(A\mid B)}{P(A^c\mid B)}.$$

Một thước đo phổ biến khác là *nguy cơ tương đối* của bệnh đối với người có tiếp xúc:

$$\mathrm{RR}=\frac{P(D\mid C)}{P(D\mid C^c)}.$$

Nguy cơ tương đối đặc biệt dễ hiểu: chẳng hạn $\mathrm{RR}=2$ nói rằng người có tiếp xúc có khả năng mắc bệnh gấp đôi người không tiếp xúc. Tuy vậy, điều này không nhất thiết nghĩa là chất đó *gây ra* mức nguy cơ tăng; tỉ số odds cũng không nhất thiết có cách hiểu nhân quả.

(a) Chứng minh nếu bệnh hiếm cả trong nhóm có tiếp xúc lẫn nhóm không tiếp xúc, thì $\mathrm{RR}\approx\mathrm{OR}$.

(b) Gọi $p_{ij}$ với $i,j\in\{0,1\}$ là các xác suất trong bảng $2\times2$ sau:

| | $D$ | $D^c$ |
|---|---:|---:|
| $C$ | $p_{11}$ | $p_{10}$ |
| $C^c$ | $p_{01}$ | $p_{00}$ |

Chẳng hạn, $p_{10}=P(C\cap D^c)$. Chứng minh tỉ số odds có thể viết dưới dạng *tỉ số tích chéo*: $\mathrm{OR}=p_{11}p_{00}/(p_{10}p_{01})$.

(c) Chứng minh tỉ số odds có tính đối xứng đẹp: đổi vai trò $C,D$ không làm đổi giá trị,

$$\mathrm{OR}=\frac{\operatorname{odds}(C\mid D)}{\operatorname{odds}(C\mid D^c)}.$$

Tính chất này là một lý do chính tỉ số odds được dùng rộng rãi: nhờ nó, có thể ước lượng tỉ số odds trong nhiều bài toán mà nguy cơ tương đối rất khó ước lượng tốt.

**60.** Một nhà nghiên cứu muốn ước lượng tỉ lệ người trong một quần thể từng dùng chất ma túy bất hợp pháp bằng khảo sát. Vì lo nhiều người sẽ nói dối khi được hỏi câu nhạy cảm như “Bạn từng dùng chất ma túy bất hợp pháp chưa?”, nhà nghiên cứu dùng phương pháp *trả lời ngẫu nhiên*. Ông bỏ các mảnh giấy vào mũ; mỗi mảnh ghi “Tôi từng dùng chất ma túy bất hợp pháp” hoặc “Tôi chưa từng dùng chất ma túy bất hợp pháp”. Gọi $p$ là tỉ lệ mảnh ghi câu thứ nhất; nhà nghiên cứu chọn $p$ từ trước.

Mỗi người tham gia rút ngẫu nhiên một mảnh và trả lời *thật* “có” hoặc “không” tùy câu trên mảnh ấy có đúng với họ không. Sau đó họ bỏ mảnh trở lại mũ. Nhà nghiên cứu không biết người ấy đã rút loại mảnh nào. Gọi $y$ là xác suất một người trả lời “có”, $d$ là xác suất một người từng dùng chất ma túy bất hợp pháp.

(a) Tìm $y$ theo $d,p$.

(b) Giá trị $p$ nào là lựa chọn tệ nhất của nhà nghiên cứu khi thiết kế khảo sát? Hãy giải thích.

(c) Xét hệ thống thay thế: tỉ lệ $p$ mảnh vẫn ghi “Tôi từng dùng chất ma túy bất hợp pháp”, nhưng $1-p$ mảnh còn lại ghi “Tôi sinh vào mùa đông” thay vì “Tôi chưa từng dùng chất ma túy bất hợp pháp”. Giả sử $1/4$ số người sinh vào mùa đông và mùa sinh độc lập với việc từng dùng chất ma túy bất hợp pháp. Hãy tìm $d$ theo $y,p$.

**61.** Ở đầu vở kịch *Rosencrantz and Guildenstern Are Dead* của Tom Stoppard [28], Guildenstern tung đồng xu và Rosencrantz cược vào kết quả từng lần. Đồng xu cứ liên tục ra mặt ngửa, khiến Guildenstern nhận xét:

> Một người yếu lòng hơn có lẽ đã bắt đầu xem lại niềm tin của mình, nếu không ở điều gì khác thì ít nhất ở quy luật xác suất.

Các lần tung đã cho mặt ngửa liên tiếp 92 lần.

(a) Fred và bạn anh xem vở kịch. Thấy tình huống này, họ đối thoại:

> **Fred:** Kết quả ấy cực khó xảy ra nếu đồng xu cân đối. Chắc họ dùng đồng xu bị chỉnh (có thể hai mặt ngửa), hoặc thí nghiệm bị can thiệp (có thể bằng nam châm).
>
> **Bạn Fred:** Đúng là chuỗi $HH\cdots H$ dài 92 rất khó xảy ra; với đồng xu cân đối, xác suất là $1/2^{92}\approx2\times10^{-28}$. Nhưng bất kỳ chuỗi $H,T$ cụ thể nào khác dài 92 cũng có xác suất y hệt! Kết quả có vẻ cực khó xảy ra chỉ vì số kết quả có thể có tăng theo hàm mũ với số lần tung; kết quả nào cũng sẽ có vẻ cực khó. Anh có thể đưa ra lập luận ấy ngay cả trước khi xem kết quả thí nghiệm, vậy thật ra đây không phải bằng chứng chống lại giả thuyết đồng xu cân đối.

Hãy bàn về các nhận xét này để giúp Fred và bạn giải quyết bất đồng.

(b) Giả sử chỉ có hai khả năng: hoặc các đồng xu đều cân đối và được tung công bằng, hoặc người ta dùng đồng xu hai mặt ngửa (khi đó xác suất ra ngửa bằng 1). Gọi $p$ là xác suất tiên nghiệm đồng xu cân đối. Hãy tìm xác suất hậu nghiệm chúng cân đối khi biết 92 trên 92 lần đều ra ngửa.

(c) Tiếp ý (b), với những giá trị $p$ nào thì xác suất hậu nghiệm đồng xu cân đối lớn hơn $0{,}5$? Với giá trị nào nó nhỏ hơn $0{,}05$?

**62.** Có $n$ loại đồ chơi mà bạn sưu tập từng món một. Mỗi lần mua, loại đồ chơi được chọn ngẫu nhiên, các loại có xác suất như nhau. Gọi $p_{ij}$ là xác suất ngay sau khi mua món thứ $i$, bộ sưu tập có đúng $j$ loại, với $i\ge1$ và $0\le j\le n$. Bài này thuộc khuôn khổ *bài toán người sưu tập phiếu*, một bài toán nổi tiếng sẽ được xét ở Ví dụ 4.3.11.

(a) Tìm phương trình đệ quy biểu diễn $p_{ij}$ theo $p_{i-1,j}$ và $p_{i-1,j-1}$, với $i\ge2$ và $1\le j\le n$.

(b) Mô tả cách dùng đệ quy trong (a) để tính $p_{ij}$.

**63.** *Thử nghiệm A/B* là một dạng thí nghiệm ngẫu nhiên mà nhiều công ty dùng để tìm hiểu phản ứng của khách hàng với các phương án khác nhau. Chẳng hạn, công ty có thể muốn xem người dùng phản ứng thế nào với một tính năng mới trên trang web (so với phiên bản hiện tại), hoặc so sánh hai quảng cáo.

Đúng như tên gọi, người ta nghiên cứu hai phương án, A và B. Người dùng đến từng người một; khi đến, họ được phân ngẫu nhiên vào một trong hai phương án. Kết quả với mỗi người được xếp là “thành công” (chẳng hạn người đó mua hàng) hoặc “thất bại”. Xác suất người thứ $n$ nhận phương án A có thể phụ thuộc kết quả của những người trước. Bố trí này được gọi là *bài toán hai máy đánh bạc*.

Đã có nhiều thuật toán phân ngẫu nhiên phương án được nghiên cứu. Sau đây là một thuật toán đặc biệt đơn giản (nhưng dễ dao động), gọi là quy trình *giữ phương án thắng*:

1. Phân ngẫu nhiên người dùng đầu tiên vào A hoặc B, hai khả năng bằng nhau.
2. Nếu thử nghiệm với người thứ $n$ thành công, giữ nguyên phương án cho người thứ $n+1$; nếu không, chuyển sang phương án kia.

Gọi $a$ là xác suất thành công với A và $b$ là xác suất thành công với B. Giả sử $a\ne b$ nhưng chưa biết hai giá trị (đó là lý do cần thử nghiệm). Gọi $p_n$ là xác suất thành công ở lượt thứ $n$ và $a_n$ là xác suất lượt thứ $n$ được phân vào A theo thuật toán trên.

(a) Chứng minh $p_n=(a-b)a_n+b$ và $a_{n+1}=(a+b-1)a_n+1-b$.

(b) Dùng (a) để chứng minh hệ thức đệ quy $p_{n+1}=(a+b-1)p_n+a+b-2ab$.

(c) Dùng (b) tìm xác suất thành công dài hạn của thuật toán, $\lim_{n\to\infty}p_n$, giả sử giới hạn tồn tại.

**64.** Ở người (và nhiều sinh vật khác), gen đi theo cặp. Một gen có hai dạng, gọi là *alen* $a$ và $A$. Kiểu gen của một người đối với gen ấy là cặp dạng gen: $AA$, $Aa$ hoặc $aa$ ($aA$ tương đương $Aa$). Giả sử định luật Hardy–Weinberg áp dụng, tức tần suất $AA$, $Aa$, $aa$ trong quần thể lần lượt là $p^2$, $2p(1-p)$, $(1-p)^2$ với $0<p<1$.

Khi một phụ nữ và một người đàn ông có con, cặp gen của con gồm một gen từ mỗi người. Giả sử mẹ có khả năng truyền mỗi gen trong cặp của mình như nhau; cha cũng vậy, độc lập với mẹ. Giả sử thêm kiểu gen của cha mẹ độc lập, với xác suất theo định luật Hardy–Weinberg.

(a) Tìm xác suất của mỗi kiểu gen có thể có ($AA$, $Aa$, $aa$) ở con của hai người cha mẹ được chọn ngẫu nhiên. Kết quả này nói gì về tính ổn định của định luật Hardy–Weinberg từ thế hệ này sang thế hệ tiếp theo? *Gợi ý:* Đặt điều kiện theo kiểu gen của cha mẹ.

(b) Người mang kiểu gen $AA$ hoặc $aa$ được gọi là *đồng hợp tử* (đối với gen đang xét); người mang kiểu $Aa$ được gọi là *dị hợp tử*. Tìm xác suất con đồng hợp tử khi biết cả cha lẫn mẹ đều đồng hợp tử. Đồng thời, tìm xác suất con dị hợp tử khi biết cả cha lẫn mẹ đều dị hợp tử.

(c) Giả sử kiểu gen $aa$ tạo ra một đặc điểm ngoại hình rất dễ nhận ra, nên chỉ cần nhìn là biết một người có kiểu gen đó hay không. Cha mẹ đều không phải kiểu $aa$ và có một người con. Người con cũng không phải kiểu $aa$. Theo thông tin ấy, hãy tìm xác suất con là dị hợp tử. *Gợi ý:* Dùng định nghĩa xác suất có điều kiện, rồi khai triển cả tử lẫn mẫu bằng định luật xác suất toàn phần, đặt điều kiện theo kiểu gen của cha mẹ.

**65.** Một bộ bài chuẩn sẽ được xáo rồi lật từng lá cho đến khi thấy lá át đầu tiên. Gọi $B$ là biến cố lá *tiếp theo* trong bộ bài cũng là át.

(a) Theo trực giác, bạn nghĩ $P(B)$ lớn hơn, nhỏ hơn hay bằng $1/13$ (tỉ lệ át trong cả bộ bài)? Hãy giải thích trực giác, không cần tính toán; mục tiêu là diễn đạt rõ suy nghĩ của bạn.

(b) Gọi $C_j$ là biến cố lá át đầu tiên ở vị trí thứ $j$ trong bộ bài. Tìm và rút gọn $P(B\mid C_j)$ theo $j$.

(c) Dùng định luật xác suất toàn phần viết $P(B)$ dưới dạng một tổng. Có thể để tổng chưa rút gọn, nhưng nó phải dễ tính bằng phần mềm như R.

(d) Tìm biểu thức rút gọn hoàn toàn của $P(B)$ bằng tính đối xứng. *Gợi ý:* Nếu phải chọn cược rằng lá ngay sau lá át đầu tiên là át hay lá cuối cùng của bộ bài là át, bạn có ưu tiên bên nào không?

## Chương 3. Biến ngẫu nhiên và phân phối của chúng (từ trang PDF 109)

Trong chương này, chúng tôi giới thiệu *biến ngẫu nhiên*, một khái niệm vô cùng hữu ích giúp đơn giản hóa ký hiệu, mở rộng khả năng định lượng bất định và tóm tắt kết quả phép thử. Biến ngẫu nhiên là công cụ thiết yếu xuyên suốt phần còn lại của sách và toàn bộ ngành thống kê. Vì thế, cần suy nghĩ kỹ ý nghĩa của nó, cả bằng trực giác lẫn toán học.

### 3.1. Biến ngẫu nhiên

Để thấy vì sao cách ký hiệu hiện tại nhanh chóng trở nên cồng kềnh, hãy quay lại bài toán con bạc phá sản ở Chương 2. Ta có thể rất quan tâm mỗi con bạc có bao nhiêu tiền tại từng thời điểm. Khi ấy, ta có thể đặt $A_{jk}$ là biến cố con bạc $A$ có đúng $j$ đô la sau $k$ lượt, rồi định nghĩa tương tự $B_{jk}$ cho con bạc $B$, với mọi $j,k$.

Cách đó đã quá phức tạp. Ta còn có thể quan tâm các đại lượng khác, như chênh lệch tài sản của họ (tiền của $A$ trừ tiền của $B$) sau $k$ lượt, hoặc thời lượng trò chơi (số lượt đến khi một người phá sản). Nếu viết biến cố “trò chơi kéo dài $r$ lượt” bằng $A_{jk}$ và $B_{jk}$, ta phải dùng một chuỗi hợp và giao dài, khó đọc. Còn nếu muốn biểu diễn tài sản của $A$ bằng euro thay vì đô la thì sao? Ta có thể nhân *một số tiền* bằng đô la với tỉ giá, nhưng không thể nhân *một biến cố* với tỉ giá.

Thay vì các ký hiệu rối rắm che khuất mối liên hệ giữa những đại lượng cần xét, sẽ thật tiện nếu ta có thể nói như sau:

> Gọi $X_k$ là tài sản của con bạc $A$ sau $k$ lượt. Khi đó $Y_k=N-X_k$ là tài sản của $B$ sau $k$ lượt (với $N$ là tổng tài sản cố định); $X_k-Y_k=2X_k-N$ là chênh lệch tài sản sau $k$ lượt; $c_kX_k$ là tài sản của $A$ tính bằng euro sau $k$ lượt, với $c_k$ là tỉ giá euro trên đô la lúc ấy; và thời lượng trò chơi là $R=\min\{n:X_n=0\text{ hoặc }Y_n=0\}$.

Khái niệm biến ngẫu nhiên cho phép ta làm đúng như vậy! Tuy nhiên, ta cần giới thiệu cẩn thận để nó chính xác cả về khái niệm lẫn kỹ thuật. Đôi khi, định nghĩa “biến ngẫu nhiên” gần như chỉ diễn đạt lại câu “một biến ngẫu nhiên là một biến nhận giá trị ngẫu nhiên”. Kiểu định nghĩa yếu ớt ấy không cho biết tính ngẫu nhiên đến từ đâu. Nó cũng không giúp ta suy ra các tính chất của biến ngẫu nhiên: ta quen làm việc với phương trình đại số như $x^2+y^2=1$, nhưng những phép toán nào hợp lệ nếu $x,y$ là biến ngẫu nhiên? Để nói chính xác, ta định nghĩa biến ngẫu nhiên là một hàm ánh xạ không gian mẫu vào trục số thực. (Xem phụ lục toán học để ôn một số khái niệm về hàm.)

**Hình 3.1.** Một biến ngẫu nhiên ánh xạ không gian mẫu vào trục số thực. Biến $X$ trong hình được định nghĩa trên không gian mẫu gồm 6 phần tử và nhận các giá trị có thể là 0, 1 và 4. Tính ngẫu nhiên đến từ việc chọn ngẫu nhiên một “viên sỏi” theo hàm xác suất $P$ trên không gian mẫu.

**Định nghĩa 3.1.1 (Biến ngẫu nhiên).** Với một phép thử có không gian mẫu $S$, *biến ngẫu nhiên* là một hàm từ $S$ đến tập số thực $\mathbb R$. Thông thường, nhưng không bắt buộc, ta ký hiệu biến ngẫu nhiên bằng chữ hoa.

Vậy biến ngẫu nhiên $X$ gán giá trị số $X(s)$ cho mỗi kết quả có thể xảy ra $s$ của phép thử. Tính ngẫu nhiên nằm ở *phép thử* (với các xác suất do hàm $P$ mô tả); bản thân ánh xạ là tất định, như Hình 3.1 minh họa. Cùng biến ngẫu nhiên ấy được biểu diễn đơn giản hơn ở bên trái Hình 3.2, bằng cách ghi giá trị vào trong từng viên sỏi.

Định nghĩa này trừu tượng nhưng cơ bản. Một trong những kỹ năng quan trọng nhất khi học xác suất và thống kê là chuyển qua lại giữa ý tưởng trừu tượng và ví dụ cụ thể. Cũng cần tập nhận ra mẫu hình hay cấu trúc cốt lõi của một bài toán và mối liên hệ với bài đã học. Ta thường kể các câu chuyện về tung đồng xu hoặc rút bóng từ bình vì chúng đơn giản, dễ làm việc; nhưng nhiều bài toán khác *đẳng cấu*, tức có cùng cấu trúc thiết yếu dưới hình thức khác.

Trước hết, hãy xét ví dụ tung đồng xu. Cấu trúc bài toán là một dãy phép thử, mỗi phép thử có hai kết quả có thể xảy ra. Ta gọi các kết quả là H (ngửa) và T (sấp), nhưng cũng có thể gọi là “thành công” và “thất bại”, hoặc 1 và 0.

**Ví dụ 3.1.2 (Tung đồng xu).** Tung một đồng xu cân đối hai lần. Không gian mẫu có bốn kết quả: $S=\{HH,HT,TH,TT\}$. Sau đây là vài biến ngẫu nhiên trên không gian này (để luyện tập, bạn có thể tự nghĩ thêm). Mỗi biến tóm tắt bằng số một khía cạnh của phép thử.

- Gọi $X$ là số lần ra ngửa. $X$ có thể bằng 0, 1 hoặc 2. Xem như một hàm, $X$ gán 2 cho $HH$, 1 cho $HT$ và $TH$, và 0 cho $TT$: $X(HH)=2$, $X(HT)=X(TH)=1$, $X(TT)=0$.
- Gọi $Y$ là số lần ra sấp. Ta có $Y=2-X$; nói cách khác, $Y$ và $2-X$ là cùng một biến ngẫu nhiên: $Y(s)=2-X(s)$ với mọi $s$.
- Gọi $I$ bằng 1 nếu lần đầu ra ngửa và bằng 0 nếu không. Khi ấy, $I$ gán 1 cho $HH,HT$ và gán 0 cho $TH,TT$. Đây là ví dụ về *biến ngẫu nhiên chỉ báo*: nó báo lần đầu có ra ngửa hay không, dùng 1 cho “có”, 0 cho “không”.

Ta cũng có thể mã hóa không gian mẫu thành $\{(1,1),(1,0),(0,1),(0,0)\}$, với 1 là ngửa, 0 là sấp. Khi đó, có công thức tường minh:

$$X(s_1,s_2)=s_1+s_2,\qquad Y(s_1,s_2)=2-s_1-s_2,\qquad I(s_1,s_2)=s_1.$$

Để gọn, ta viết $X(s_1,s_2)$ thay cho $X((s_1,s_2))$, v.v. Với phần lớn biến ngẫu nhiên ta sẽ gặp, việc viết công thức tường minh kiểu này rất dài dòng hoặc không khả thi. May là thường không cần: như ví dụ trên, có nhiều cách định nghĩa biến; và trong phần còn lại của sách, ta sẽ thấy nhiều cách nghiên cứu tính chất của biến mà không phải tính công thức ánh xạ từng kết quả $s$.

Như các chương trước, nếu không gian mẫu hữu hạn, ta có thể hình dung mỗi kết quả là một viên sỏi, khối lượng của nó tương ứng với xác suất, sao cho tổng khối lượng bằng 1. Biến ngẫu nhiên chỉ việc gắn cho mỗi viên sỏi một con số. Hình 3.2 biểu diễn hai biến ngẫu nhiên trên cùng một không gian mẫu: các viên sỏi, tức kết quả, giống nhau, nhưng giá trị số gán cho chúng khác nhau.

**Hình 3.2.** Hai biến ngẫu nhiên được định nghĩa trên cùng một không gian mẫu.

Như đã nói, nguồn gốc tính ngẫu nhiên của biến ngẫu nhiên là chính phép thử: một kết quả mẫu $s\in S$ được chọn theo hàm xác suất $P$. Trước khi thực hiện, kết quả $s$ chưa thành hiện thực nên ta chưa biết $X$ bằng bao nhiêu, dù có thể tính xác suất $X$ nhận một giá trị hoặc nằm trong một khoảng. Sau phép thử, khi $s$ thành hiện thực, biến ngẫu nhiên “kết tinh” thành con số $X(s)$.

Biến ngẫu nhiên cung cấp bản tóm tắt bằng số của phép thử. Điều này rất tiện vì không gian mẫu thường cực kỳ phức tạp hoặc nhiều chiều, còn các kết quả $s\in S$ có thể không phải số. Chẳng hạn, phép thử có thể là chọn mẫu ngẫu nhiên cư dân trong một thành phố và hỏi nhiều câu, có câu trả lời bằng số (tuổi, chiều cao), có câu không bằng số (đảng chính trị, phim yêu thích). Việc biến ngẫu nhiên nhận giá trị số giúp ta đơn giản hóa rất nhiều so với phải luôn xử lý toàn bộ sự phức tạp của $S$.

### 3.2. Phân phối và hàm khối xác suất

Trong thực tế, có hai loại biến ngẫu nhiên chính: *rời rạc* và *liên tục*. Chương này và chương sau tập trung vào loại rời rạc. Biến liên tục được giới thiệu ở Chương 5.

**Định nghĩa 3.2.1 (Biến ngẫu nhiên rời rạc).** Biến ngẫu nhiên $X$ là *rời rạc* nếu có một danh sách hữu hạn $a_1,\ldots,a_n$ hoặc vô hạn $a_1,a_2,\ldots$ sao cho $P(X=a_j\text{ với một }j)=1$. Với biến rời rạc, tập hữu hạn hoặc vô hạn đếm được các giá trị $x$ thỏa $P(X=x)>0$ được gọi là *giá đỡ* của $X$.

Trong ứng dụng, giá đỡ của biến rời rạc thường là một tập số nguyên. Trái lại, biến liên tục có thể nhận bất kỳ giá trị thực nào trong một khoảng, thậm chí cả trục số thực; chúng sẽ được định nghĩa chính xác hơn ở Chương 5. Cũng có thể có biến pha trộn rời rạc và liên tục, chẳng hạn tung đồng xu rồi tạo biến rời rạc nếu ra ngửa, biến liên tục nếu ra sấp. Nhưng để hiểu loại pha trộn, trước hết cần hiểu hai loại cơ bản.

Với một biến ngẫu nhiên, ta muốn mô tả hành vi của nó bằng ngôn ngữ xác suất. Chẳng hạn, ta muốn biết xác suất nó thuộc một khoảng: nếu $L$ là tổng thu nhập trọn đời của một người tốt nghiệp đại học ở Hoa Kỳ được chọn ngẫu nhiên, xác suất $L$ vượt một triệu đô la là bao nhiêu? Nếu $M$ là số trận động đất lớn ở California trong năm năm tới, xác suất $M=0$ là bao nhiêu?

*Phân phối* của biến ngẫu nhiên trả lời các câu hỏi ấy: nó xác định xác suất của mọi biến cố liên quan đến biến, chẳng hạn biến bằng 3 hoặc ít nhất bằng 110. Ta sẽ thấy nhiều cách tương đương để biểu diễn phân phối. Với biến rời rạc, cách tự nhiên nhất là *hàm khối xác suất*, được định nghĩa sau.

**Định nghĩa 3.2.2 (Hàm khối xác suất).** Hàm khối xác suất (PMF) của biến ngẫu nhiên rời rạc $X$ là hàm $p_X$ cho bởi $p_X(x)=P(X=x)$. Nó dương khi $x$ thuộc giá đỡ của $X$, và bằng 0 ở nơi khác.

**Cảnh báo 3.2.3.** Khi viết $P(X=x)$, ta dùng $X=x$ để chỉ một *biến cố*: tập hợp mọi kết quả $s$ mà $X$ gán giá trị $x$. Biến cố này cũng viết là $\{X=x\}$; định nghĩa hình thức là $\{s\in S:X(s)=x\}$, nhưng $\{X=x\}$ ngắn và dễ hiểu hơn. Trở lại Ví dụ 3.1.2, nếu $X$ là số lần ngửa trong hai lần tung đồng xu cân đối, $\{X=1\}$ gồm $HT,TH$, là hai kết quả được $X$ gán giá trị 1. Vì $\{HT,TH\}$ là tập con của không gian mẫu, nó là biến cố. Do đó, nói $P(X=1)$, hay tổng quát $P(X=x)$, là có nghĩa. Nếu $\{X=x\}$ không phải biến cố, ta không thể tính xác suất của nó! Không thể viết “$P(X)$”: ta chỉ lấy xác suất của *biến cố*, không phải của *biến ngẫu nhiên*.

Hãy xem vài ví dụ về hàm khối xác suất.

**Ví dụ 3.2.4 (Tung đồng xu, tiếp theo).** Ta sẽ tìm PMF của mọi biến trong Ví dụ 3.1.2, với hai lần tung đồng xu cân đối. Sau đây là các biến đã định nghĩa và PMF của chúng:

- $X$, số lần ngửa. $X=0$ khi kết quả $TT$, bằng 1 khi $HT$ hoặc $TH$, bằng 2 khi $HH$. Vậy $p_X(0)=P(X=0)=1/4$, $p_X(1)=P(X=1)=1/2$, $p_X(2)=P(X=2)=1/4$; còn $p_X(x)=0$ với mọi $x$ khác.
- $Y=2-X$, số lần sấp. Lập luận tương tự hoặc dùng $P(Y=y)=P(2-X=y)=P(X=2-y)=p_X(2-y)$, ta được $p_Y(0)=1/4$, $p_Y(1)=1/2$, $p_Y(2)=1/4$; còn $p_Y(y)=0$ với mọi $y$ khác. Lưu ý $X,Y$ có *cùng PMF* (tức $p_X,p_Y$ là cùng một hàm) dù *không phải cùng biến ngẫu nhiên* (chúng là hai hàm khác nhau từ $\{HH,HT,TH,TT\}$ đến trục số thực).
- $I$, chỉ báo lần tung đầu ra ngửa. $I=0$ khi $TH$ hoặc $TT$, và bằng 1 khi $HH$ hoặc $HT$. Vì vậy $p_I(0)=P(I=0)=1/2$, $p_I(1)=P(I=1)=1/2$; còn $p_I(i)=0$ với mọi $i$ khác.

**Hình 3.3.** Từ trái sang phải là PMF của $X$, $Y$, $I$: $X$ đếm số lần ngửa trong hai lần tung đồng xu cân đối, $Y$ đếm số lần sấp, $I$ chỉ báo lần đầu ra ngửa. Biểu đồ vẽ các thanh dọc để dễ so sánh độ cao tại các điểm.

**Ví dụ 3.2.5 (Tổng hai lần gieo xúc xắc).** Gieo hai con xúc xắc cân đối sáu mặt. Gọi $T=X+Y$ là tổng, trong đó $X,Y$ là kết quả từng con. Không gian mẫu có 36 kết quả đồng khả năng: $S=\{(1,1),(1,2),\ldots,(6,5),(6,6)\}$. Chẳng hạn, bảng sau nêu 7 trong 36 kết quả $s$ và giá trị tương ứng của $X,Y,T$. Sau phép thử, ta quan sát $X,Y$; giá trị quan sát của $T$ là tổng hai giá trị ấy.

| $s$ | $X$ | $Y$ | $T=X+Y$ |
|---|---:|---:|---:|
| $(1,2)$ | 1 | 2 | 3 |
| $(1,6)$ | 1 | 6 | 7 |
| $(2,5)$ | 2 | 5 | 7 |
| $(3,1)$ | 3 | 1 | 4 |
| $(4,3)$ | 4 | 3 | 7 |
| $(5,4)$ | 5 | 4 | 9 |
| $(6,6)$ | 6 | 6 | 12 |

Vì xúc xắc cân đối, PMF của $X$ là $P(X=j)=1/6$ với $j=1,2,\ldots,6$, và bằng 0 ở nơi khác. Ta nói $X$ có *phân phối đều rời rạc* trên $1,2,\ldots,6$. Tương tự, $Y$ cũng đều rời rạc trên tập ấy. $Y$ có cùng phân phối với $X$ nhưng không phải cùng biến ngẫu nhiên; thực tế $P(X=Y)=6/36=1/6$.

Hai biến khác trong phép thử có cùng phân phối với $X$ là $7-X$ và $7-Y$. Với xúc xắc chuẩn, nếu $X$ là giá trị mặt trên thì $7-X$ là giá trị mặt dưới. Nếu mặt trên có khả năng bằng mỗi số từ 1 đến 6 như nhau, mặt dưới cũng vậy. Dù $7-X$ có cùng phân phối với $X$, ở một lần gieo cụ thể nó không bao giờ bằng $X$!

Giờ hãy tìm PMF của $T$. Theo định nghĩa xác suất sơ khai,

| Tổng $t$ | $P(T=t)$ |
|---|---|
| 2 hoặc 12 | $1/36$ |
| 3 hoặc 11 | $2/36$ |
| 4 hoặc 10 | $3/36$ |
| 5 hoặc 9 | $4/36$ |
| 6 hoặc 8 | $5/36$ |
| 7 | $6/36$ |

Với các giá trị $t$ khác, $P(T=t)=0$. Ta thấy ngay giá đỡ của $T$ là $\{2,3,\ldots,12\}$ khi xét các tổng có thể có của hai con xúc xắc. Để kiểm tra, $P(T=2)+P(T=3)+\cdots+P(T=12)=1$, cho thấy đã kể hết mọi khả năng. Tính đối xứng $P(T=t)=P(T=14-t)$ cũng hợp lý: mỗi kết quả $\{X=x,Y=y\}$ cho tổng $t$ đều có kết quả tương ứng $\{X=7-x,Y=7-y\}$ có cùng xác suất và cho tổng $14-t$.

**Hình 3.4.** PMF của tổng hai con xúc xắc. Biểu đồ có dạng tam giác và thể hiện rõ tính đối xứng vừa nêu.

**Ví dụ 3.2.6 (Số trẻ em trong một hộ gia đình Hoa Kỳ).** Giả sử chọn ngẫu nhiên một hộ gia đình ở Hoa Kỳ. Gọi $X$ là số trẻ em trong hộ đó. Vì $X$ chỉ nhận giá trị nguyên, nó là biến ngẫu nhiên rời rạc. Xác suất $X=x$ tỉ lệ với số hộ gia đình ở Hoa Kỳ có $x$ trẻ em. Dùng dữ liệu từ Khảo sát Xã hội Tổng quát năm 2010 [26], ta có thể xấp xỉ tỉ lệ hộ không có trẻ em, có một trẻ, hai trẻ, v.v.; từ đó xấp xỉ PMF của $X$, được vẽ ở Hình 3.5.

Sau đây là các tính chất của một PMF hợp lệ.

**Định lý 3.2.7 (PMF hợp lệ).** Cho $X$ là biến ngẫu nhiên rời rạc có giá đỡ $x_1,x_2,\ldots$; giả sử các giá trị phân biệt và để ký hiệu đơn giản, giá đỡ vô hạn đếm được (trường hợp hữu hạn có kết quả tương tự). PMF $p_X$ phải thỏa:

- **Không âm:** $p_X(x)>0$ nếu $x=x_j$ với một $j$, và $p_X(x)=0$ ở nơi khác.
- **Tổng bằng 1:** $\sum_{j=1}^{\infty}p_X(x_j)=1$.

**Hình 3.5.** PMF của số trẻ em trong một hộ gia đình Hoa Kỳ được chọn ngẫu nhiên.

**Chứng minh.** Điều kiện thứ nhất đúng vì xác suất không âm. Điều kiện thứ hai đúng vì $X$ phải nhận một giá trị nào đó, còn các biến cố $\{X=x_j\}$ rời nhau. Do đó,

$$\sum_{j=1}^{\infty}P(X=x_j)=P\!\left(\bigcup_{j=1}^{\infty}\{X=x_j\}\right)=P(X=x_1\text{ hoặc }X=x_2\text{ hoặc }\cdots)=1.$$

Ngược lại, nếu cho các giá trị phân biệt $x_1,x_2,\ldots$ và một hàm thỏa hai điều kiện trên, thì hàm đó là PMF của một biến ngẫu nhiên nào đó. Chương 5 sẽ chỉ cách xây dựng biến ấy.

Trước đây, ta nói PMF là một cách biểu diễn *phân phối* của biến rời rạc. Lý do là khi đã biết PMF của $X$, ta có thể tính xác suất $X$ thuộc một tập con cho trước của trục số thực bằng cách cộng các giá trị thích hợp, như ví dụ sau.

**Ví dụ 3.2.8.** Trở lại Ví dụ 3.2.5, gọi $T$ là tổng hai lần gieo xúc xắc cân đối. Ta đã tính PMF của $T$. Giả sử cần xác suất $T$ thuộc khoảng $[1,4]$. Trong khoảng này chỉ có ba giá trị $T$ có thể nhận: 2, 3 và 4. PMF cho xác suất của từng giá trị, nên

$$P(1\le T\le4)=P(T=2)+P(T=3)+P(T=4)=\frac6{36}.$$

Nói chung, nếu biết PMF của biến rời rạc $X$ và có một tập số thực $B$, ta tìm $P(X\in B)$ bằng cách cộng độ cao của các thanh dọc tại những điểm thuộc $B$ trên đồ thị PMF. Biết PMF của biến rời rạc là biết phân phối của nó.

### 3.3. Bernoulli và Nhị thức

Một số phân phối xuất hiện nhiều đến mức có tên riêng trong xác suất và thống kê. Chúng tôi sẽ lần lượt giới thiệu trong sách, bắt đầu bằng trường hợp rất đơn giản nhưng hữu ích: biến ngẫu nhiên chỉ có thể nhận 0 hoặc 1.

**Định nghĩa 3.3.1 (Phân phối Bernoulli).** Biến $X$ có *phân phối Bernoulli* với tham số $p$ nếu $P(X=1)=p$ và $P(X=0)=1-p$, với $0<p<1$. Ta viết $X\sim\operatorname{Bern}(p)$; ký hiệu $\sim$ đọc là “có phân phối”.

Mọi biến ngẫu nhiên chỉ nhận 0 hoặc 1 đều có phân phối $\operatorname{Bern}(p)$, với $p$ là xác suất biến bằng 1. Số $p$ gọi là *tham số* của phân phối: nó xác định cụ thể phân phối Bernoulli nào. Vì vậy, không chỉ có một phân phối Bernoulli mà có cả một họ được đánh chỉ số bởi $p$. Chẳng hạn, nếu $X\sim\operatorname{Bern}(1/3)$, nói “$X$ là Bernoulli” là đúng nhưng chưa đầy đủ. Để xác định trọn phân phối, cần nêu tên Bernoulli *và* giá trị tham số $1/3$, như ký hiệu trên.

Mỗi biến cố có một biến ngẫu nhiên Bernoulli gắn tự nhiên với nó: bằng 1 khi biến cố xảy ra và bằng 0 nếu không. Đó là *biến ngẫu nhiên chỉ báo* của biến cố; ta sẽ thấy loại biến này cực kỳ hữu ích.

**Định nghĩa 3.3.2 (Biến ngẫu nhiên chỉ báo).** Biến chỉ báo của biến cố $A$ bằng 1 nếu $A$ xảy ra, bằng 0 nếu không. Ký hiệu là $I_A$ hoặc $I(A)$. Lưu ý $I_A\sim\operatorname{Bern}(p)$ với $p=P(A)$.

Ta thường hình dung biến Bernoulli qua việc tung đồng xu, nhưng đây chỉ là cách nói tiện để bàn câu chuyện tổng quát sau.

**Câu chuyện 3.3.3 (Phép thử Bernoulli).** Một phép thử có thể cho “thành công” hoặc “thất bại” (nhưng không đồng thời cả hai) gọi là *phép thử Bernoulli*. Có thể xem biến Bernoulli là chỉ báo thành công trong phép thử ấy: nó bằng 1 nếu thành công, bằng 0 nếu thất bại.

Vì câu chuyện này, tham số $p$ thường được gọi là *xác suất thành công* của phân phối $\operatorname{Bern}(p)$. Khi đã nghĩ về một phép thử Bernoulli, ta tự nhiên sẽ muốn biết chuyện gì xảy ra nếu có nhiều phép thử.

**Câu chuyện 3.3.4 (Phân phối Nhị thức).** Giả sử thực hiện $n$ phép thử Bernoulli độc lập, mỗi phép thử có cùng xác suất thành công $p$. Gọi $X$ là số lần thành công. Phân phối của $X$ gọi là *phân phối Nhị thức* với tham số $n,p$. Ta viết $X\sim\operatorname{Bin}(n,p)$, với $n$ là số nguyên dương và $0<p<1$.

Lưu ý ta định nghĩa phân phối Nhị thức bằng *câu chuyện* về loại phép thử tạo ra nó, thay vì bằng PMF. Những phân phối nổi tiếng nhất trong thống kê đều có câu chuyện giải thích vì sao chúng thường được dùng để mô hình hóa dữ liệu hoặc làm khối xây dựng cho phân phối phức tạp hơn.

Nghĩ về các phân phối có tên trước hết qua câu chuyện của chúng có nhiều lợi ích. Nó giúp nhận dạng cấu trúc, thấy hai bài toán về cơ bản là giống nhau; thường dẫn đến lời giải gọn, không phải tính PMF; và giúp hiểu các phân phối liên hệ với nhau thế nào. Ở đây, rõ ràng $\operatorname{Bern}(p)$ là cùng phân phối với $\operatorname{Bin}(1,p)$: Bernoulli là trường hợp riêng của Nhị thức.

Dùng định nghĩa bằng câu chuyện, ta tìm PMF của phân phối Nhị thức.

**Định lý 3.3.5 (PMF Nhị thức).** Nếu $X\sim\operatorname{Bin}(n,p)$, thì

$$P(X=k)=\binom nk p^k(1-p)^{n-k}$$

với $k=0,1,\ldots,n$; ở nơi khác xác suất bằng 0.

**Cảnh báo 3.3.6.** Để viết ngắn, người ta thường ngầm hiểu PMF bằng 0 tại những nơi không được nêu là khác 0. Dù vậy, cần hiểu giá đỡ của biến ngẫu nhiên và nên kiểm tra tính hợp lệ của PMF. Nếu hai biến rời rạc có cùng PMF, chúng cũng phải có cùng giá đỡ. Vì thế, đôi khi ta nói *giá đỡ của một phân phối rời rạc*: đó là giá đỡ của bất kỳ biến nào mang phân phối ấy.

**Chứng minh.** Một phép thử gồm $n$ phép thử Bernoulli độc lập tạo ra dãy thành công và thất bại. Mỗi dãy cụ thể có $k$ lần thành công và $n-k$ lần thất bại có xác suất $p^k(1-p)^{n-k}$. Có $\binom nk$ dãy như vậy vì chỉ cần chọn vị trí các lần thành công. Do đó, với $X$ là số lần thành công, $P(X=k)=\binom nk p^k(1-p)^{n-k}$ cho $k=0,\ldots,n$, và bằng 0 ở nơi khác. Đây là PMF hợp lệ vì không âm và tổng bằng 1 theo định lý nhị thức.

Hình 3.6 vẽ PMF Nhị thức với vài giá trị $n,p$. PMF của $\operatorname{Bin}(10,1/2)$ đối xứng quanh 5; khi xác suất thành công khác $1/2$, đồ thị lệch. Với số lần thử $n$ cố định, $X$ có xu hướng lớn hơn khi xác suất thành công cao và nhỏ hơn khi xác suất ấy thấp, đúng như câu chuyện phân phối Nhị thức gợi ý.

Lưu ý thêm: trên mọi đồ thị PMF, tổng độ cao các thanh dọc phải bằng 1.

**Hình 3.6.** Một số PMF Nhị thức: $\operatorname{Bin}(10,1/2)$, $\operatorname{Bin}(10,1/8)$, $\operatorname{Bin}(100,0{,}03)$ và $\operatorname{Bin}(9,4/5)$. Với $\operatorname{Bin}(100,0{,}03)$, hình chỉ vẽ từ 0 đến 10 vì xác suất hơn 10 lần thành công gần bằng 0.

Ta vừa dùng Câu chuyện 3.3.4 để tìm PMF của $\operatorname{Bin}(n,p)$. Câu chuyện cũng cho một chứng minh trực tiếp rằng nếu $X$ có phân phối Nhị thức thì $n-X$ cũng có phân phối Nhị thức.

**Định lý 3.3.7.** Cho $X\sim\operatorname{Bin}(n,p)$ và $q=1-p$ (ta thường ký hiệu xác suất thất bại của phép thử Bernoulli là $q$). Khi ấy $n-X\sim\operatorname{Bin}(n,q)$.

**Chứng minh.** Theo câu chuyện Nhị thức, xem $X$ là số lần thành công trong $n$ phép thử Bernoulli độc lập. Khi đó $n-X$ là số lần thất bại. Đổi vai trò thành công và thất bại, ta có $n-X\sim\operatorname{Bin}(n,q)$. Hoặc có thể kiểm tra trực tiếp $n-X$ có PMF $\operatorname{Bin}(n,q)$. Đặt $Y=n-X$.

PMF của $Y$ là

$$P(Y=k)=P(X=n-k)=\binom n{n-k}p^{n-k}q^k=\binom nkq^kp^{n-k},\qquad k=0,1,\ldots,n.$$

**Hệ quả 3.3.8.** Cho $X\sim\operatorname{Bin}(n,p)$ với $p=1/2$ và $n$ chẵn. Phân phối của $X$ đối xứng quanh $n/2$, nghĩa là $P(X=n/2+j)=P(X=n/2-j)$ với mọi số nguyên không âm $j$.

**Chứng minh.** Theo Định lý 3.3.7, $n-X$ cũng có phân phối $\operatorname{Bin}(n,1/2)$, nên $P(X=k)=P(n-X=k)=P(X=n-k)$ với mọi số nguyên không âm $k$. Cho $k=n/2+j$ sẽ được kết quả cần chứng minh. Điều này giải thích vì sao PMF của $\operatorname{Bin}(10,1/2)$ ở Hình 3.6 đối xứng quanh 5.

**Ví dụ 3.3.9 (Tung đồng xu, tiếp theo).** Trở lại Ví dụ 3.1.2, giờ ta biết $X\sim\operatorname{Bin}(2,1/2)$, $Y\sim\operatorname{Bin}(2,1/2)$ và $I\sim\operatorname{Bern}(1/2)$. Đúng như Định lý 3.3.7, $X$ và $Y=2-X$ có cùng phân phối. Đúng như Hệ quả 3.3.8, phân phối của $X$ (và $Y$) đối xứng quanh 1.

### 3.4. Siêu bội

Nếu một bình chứa $w$ quả bóng trắng và $b$ quả bóng đen, thì rút $n$ quả *có hoàn lại* cho phân phối $\operatorname{Bin}(n,w/(w+b))$ đối với số bóng trắng nhận được: các lượt rút là phép thử Bernoulli độc lập, mỗi lượt có xác suất “thành công” $w/(w+b)$. Nếu rút *không hoàn lại*, như Hình 3.7, số bóng trắng có *phân phối Siêu bội*.

**Hình 3.7.** Câu chuyện Siêu bội: bình có $w=6$ bóng trắng và $b=4$ bóng đen. Rút $n=5$ quả không hoàn lại. Số bóng trắng $X$ trong mẫu có phân phối Siêu bội; hình minh họa kết quả $X=3$.

**Câu chuyện 3.4.1 (Phân phối Siêu bội).** Xét bình có $w$ bóng trắng, $b$ bóng đen. Rút ngẫu nhiên $n$ quả, không hoàn lại, sao cho mọi tập mẫu trong $\binom{w+b}{n}$ mẫu đều có khả năng như nhau. Gọi $X$ là số bóng trắng trong mẫu. Khi đó $X$ có *phân phối Siêu bội* với tham số $w,b,n$, ký hiệu $X\sim\operatorname{HGeom}(w,b,n)$.

Như với phân phối Nhị thức, ta có thể suy ra PMF của phân phối Siêu bội từ câu chuyện.

**Định lý 3.4.2 (PMF Siêu bội).** Nếu $X\sim\operatorname{HGeom}(w,b,n)$, thì

$$P(X=k)=\frac{\binom wk\binom b{n-k}}{\binom{w+b}{n}}$$

với các số nguyên $k$ thỏa $0\le k\le w$ và $0\le n-k\le b$; ở nơi khác $P(X=k)=0$.

**Chứng minh.** Để tìm $P(X=k)$, trước hết đếm số cách rút đúng $k$ bóng trắng và $n-k$ bóng đen, không phân biệt thứ tự rút cùng một tập bóng. Nếu $k>w$ hoặc $n-k>b$, kết quả là bất khả thi. Nếu không, quy tắc nhân cho $\binom wk\binom b{n-k}$ cách rút; tổng số cách rút $n$ bóng là $\binom{w+b}{n}$. Mọi mẫu đều đồng khả năng, nên định nghĩa xác suất sơ khai cho công thức trên. PMF này hợp lệ vì tổng tử số theo mọi $k$ bằng $\binom{w+b}{n}$ theo đồng nhất thức Vandermonde (Ví dụ 1.5.3), nên tổng PMF bằng 1.

Phân phối Siêu bội xuất hiện trong nhiều tình huống bề ngoài không liên quan đến bóng trắng, đen. Cấu trúc cốt lõi là các đối tượng trong quần thể được phân loại bằng *hai bộ nhãn*. Trong câu chuyện bình bóng, mỗi quả trắng hoặc đen (bộ nhãn thứ nhất) và được chọn hoặc không được chọn (bộ nhãn thứ hai). Ít nhất một bộ nhãn được gán hoàn toàn ngẫu nhiên: ở đây, ta chọn bóng ngẫu nhiên sao cho mọi tập mẫu đúng kích thước đều có khả năng như nhau. Khi đó, $X\sim\operatorname{HGeom}(w,b,n)$ đếm số đối tượng mang đồng thời hai nhãn: bóng vừa trắng vừa được chọn.

Hai ví dụ tiếp theo có vẻ khác nhau nhưng đều đẳng cấu với câu chuyện bình bóng.

**Ví dụ 3.4.3 (Bắt–đánh dấu–bắt lại nai sừng tấm).** Một khu rừng có $N$ con nai sừng tấm. Hôm nay người ta bắt $m$ con, đánh dấu rồi thả lại. Về sau, bắt lại ngẫu nhiên $n$ con. Giả sử mọi tập gồm $n$ con đều có khả năng được bắt lại như nhau; chẳng hạn, con từng bị bắt không học được cách tránh bẫy.

Theo câu chuyện Siêu bội, số nai đã đánh dấu trong mẫu bắt lại có phân phối $\operatorname{HGeom}(m,N-m,n)$. Ở đây, $m$ con được đánh dấu tương ứng với bóng trắng, còn $N-m$ con chưa đánh dấu tương ứng bóng đen. Thay vì rút $n$ bóng từ bình, ta bắt lại $n$ con từ rừng.

**Ví dụ 3.4.4 (Số lá át trong tay poker).** Trong tay 5 lá được chia ngẫu nhiên từ bộ bài chuẩn đã xáo kỹ, số lá át có phân phối $\operatorname{HGeom}(4,48,5)$: xem át như bóng trắng, lá khác như bóng đen. Theo PMF Siêu bội, xác suất có đúng ba lá át là

$$\frac{\binom43\binom{48}{2}}{\binom{52}{5}}\approx0{,}0017.$$

*Lưu ý về bản gốc:* PDF in “$0{,}0017\%$” ở đây; phép tính bằng khoảng $0{,}0017$, tức $0{,}17\%$.

Bảng sau tóm tắt hai bộ nhãn trong các ví dụ. Ở mỗi hàng, biến cần xét đếm số đối tượng thuộc đồng thời cột nhãn thứ hai và thứ tư: trắng và được chọn; đã đánh dấu và bắt lại; át và thuộc tay bài.

| Câu chuyện | Nhãn loại 1 | Nhãn loại 2 | Nhãn được chọn | Nhãn không được chọn |
|---|---|---|---|---|
| Bình bóng | Trắng | Đen | Được rút | Không được rút |
| Nai sừng tấm | Đã đánh dấu | Chưa đánh dấu | Được bắt lại | Không được bắt lại |
| Bài | Át | Không phải át | Thuộc tay bài | Không thuộc tay bài |

Định lý tiếp theo mô tả tính đối xứng giữa hai phân phối Siêu bội có tham số khác nhau; chứng minh dựa trên việc đổi chỗ hai bộ nhãn trong câu chuyện.

**Định lý 3.4.5.** Hai phân phối $\operatorname{HGeom}(w,b,n)$ và $\operatorname{HGeom}(n,w+b-n,w)$ giống nhau. Nghĩa là nếu $X\sim\operatorname{HGeom}(w,b,n)$ và $Y\sim\operatorname{HGeom}(n,w+b-n,w)$ thì $X,Y$ có cùng phân phối.

**Chứng minh bằng câu chuyện.** Hình dung bình có $w$ bóng trắng, $b$ bóng đen và một mẫu $n$ bóng được rút không hoàn lại. Cho $X\sim\operatorname{HGeom}(w,b,n)$ đếm số bóng trắng trong mẫu: trắng/đen là bộ nhãn thứ nhất, được rút/không được rút là bộ thứ hai. Cho $Y\sim\operatorname{HGeom}(n,w+b-n,w)$ đếm số bóng được rút trong số bóng trắng: đổi hai bộ nhãn cho nhau. Cả $X,Y$ đều đếm bóng vừa trắng vừa được rút, nên chúng có cùng phân phối.

**Chứng minh bằng đại số (trang PDF 124).** Ta cũng có thể kiểm tra trực tiếp rằng hai hàm khối xác suất bằng nhau:

$$
\begin{aligned}
P(X=k)
&=\frac{\binom wk\binom b{n-k}}{\binom{w+b}n}
=\frac{w!b!n!(w+b-n)!}
{(w+b)!\,k!(w-k)!(n-k)!(b-n+k)!},\\
P(Y=k)
&=\frac{\binom nk\binom{w+b-n}{w-k}}{\binom{w+b}w}
=\frac{w!b!n!(w+b-n)!}
{(w+b)!\,k!(w-k)!(n-k)!(b-n+k)!}.
\end{aligned}
$$

Chúng tôi thích chứng minh bằng câu chuyện hơn, vì nó đỡ dài dòng và dễ nhớ hơn. □

**Lưu ý 3.4.6 (Nhị thức và Siêu bội).** Hai phân phối này thường bị nhầm lẫn. Cả hai đều rời rạc, nhận các giá trị nguyên từ 0 đến $n$ nào đó, và đều có thể hiểu là số lần thành công trong $n$ phép thử Bernoulli. Trong câu chuyện Siêu bội, mỗi con nai đã đánh dấu trong mẫu bắt lại được tính là một lần thành công, còn nai chưa đánh dấu là thất bại. Nhưng trong câu chuyện Nhị thức, các phép thử Bernoulli phải *độc lập*. Các phép thử trong câu chuyện Siêu bội *phụ thuộc* nhau vì lấy mẫu không hoàn lại: biết một con nai trong mẫu đã được đánh dấu sẽ làm giảm xác suất con nai thứ hai cũng được đánh dấu.

### 3.5 Phân phối đều rời rạc

Một câu chuyện rất đơn giản, gắn chặt với định nghĩa xác suất sơ khai, là chọn ngẫu nhiên một số từ một tập hữu hạn.

**Câu chuyện 3.5.1 (Phân phối đều rời rạc).** Cho $C$ là tập hữu hạn, không rỗng, gồm các số. Chọn ngẫu nhiên đều một số trong $C$, nghĩa là mọi giá trị trong $C$ đều có khả năng như nhau. Gọi số được chọn là $X$. Khi ấy $X$ có *phân phối đều rời rạc* với tham số $C$, ký hiệu $X\sim\operatorname{DUnif}(C)$. ◇

Hàm khối xác suất (PMF) của $X$ là

$$P(X=x)=\frac1{|C|}\quad\text{nếu }x\in C,$$

và bằng 0 ở ngoài $C$, vì tổng các giá trị PMF phải bằng 1. Cũng như các bài toán dùng định nghĩa xác suất sơ khai, bài toán về phân phối đều rời rạc trở thành bài toán đếm. Cụ thể, với mọi $A\subseteq C$,

$$P(X\in A)=\frac{|A|}{|C|}.$$

**Ví dụ 3.5.2 (Rút phiếu giấy).** Có 100 phiếu giấy trong một chiếc mũ; mỗi phiếu ghi một số trong $1,2,\ldots,100$, mỗi số xuất hiện đúng một lần. Rút lần lượt năm phiếu.

Trước tiên, xét cách rút ngẫu nhiên **có hoàn lại** (mọi phiếu đồng khả năng ở mỗi lượt).

(a) Số phiếu rút được mang số ít nhất là 80 có phân phối gì?

(b) Giá trị của phiếu rút ở lượt $j$ có phân phối gì, với $1\le j\le5$?

(c) Xác suất rút được số 100 ít nhất một lần là bao nhiêu?

Tiếp theo, xét cách rút ngẫu nhiên **không hoàn lại** (mọi tập gồm năm phiếu đều có khả năng được chọn như nhau).

(d) Số phiếu mang số ít nhất là 80 có phân phối gì?

(e) Giá trị của phiếu rút ở lượt $j$ có phân phối gì, với $1\le j\le5$?

(f) Xác suất rút được số 100 ít nhất một lần là bao nhiêu?

**Lời giải.** (a) Theo câu chuyện Nhị thức, phân phối là $\operatorname{Bin}(5,0{,}21)$.

(b) Gọi $X_j$ là giá trị phiếu ở lượt $j$. Theo tính đối xứng, $X_j\sim\operatorname{DUnif}(\{1,2,\ldots,100\})$.

(c) Xét biến cố đối:

$$P(\text{có }j\text{ sao cho }X_j=100)
=1-P(X_1\ne100,\ldots,X_5\ne100)
=1-\left(\frac{99}{100}\right)^5\approx0{,}049.$$

Cách giải này chỉ dùng ký hiệu mới cho những khái niệm ở Chương 1. Ký hiệu mới hữu ích vì ngắn gọn và linh hoạt. Trong phép tính trên, điều quan trọng là hiểu tại sao

$$P(X_1\ne100,\ldots,X_5\ne100)
=P(X_1\ne100)\cdots P(X_5\ne100).$$

Trong trường hợp này, có thể suy ra từ định nghĩa xác suất sơ khai; cách hiểu tổng quát hơn là dựa vào tính độc lập của các biến ngẫu nhiên, sẽ được bàn kỹ ở Mục 3.8.

(d) Theo câu chuyện Siêu bội, phân phối là $\operatorname{HGeom}(21,79,5)$.

(e) Gọi $Y_j$ là giá trị phiếu ở lượt $j$. Theo tính đối xứng, $Y_j\sim\operatorname{DUnif}(\{1,2,\ldots,100\})$. Biết một giá trị $Y_i$ sẽ cho thông tin về các giá trị còn lại, nên $Y_1,\ldots,Y_5$ không độc lập theo định nghĩa ở Mục 3.8. Dù vậy, tính đối xứng vẫn đúng: nếu chưa biết kết quả các lượt khác, phiếu rút ở lượt $j$ có khả năng là bất kỳ phiếu nào như nhau.

(f) Các biến cố $Y_1=100,\ldots,Y_5=100$ xung khắc vì ta rút không hoàn lại. Do đó

$$P(\text{có }j\text{ sao cho }Y_j=100)
=P(Y_1=100)+\cdots+P(Y_5=100)=0{,}05.$$

**Kiểm tra tính hợp lý.** Ta có thể tưởng tượng trước tiên chọn năm phiếu trắng bất kỳ trong 100 phiếu, rồi ghi ngẫu nhiên các số từ 1 đến 100 lên tất cả các phiếu. Khi ấy xác suất số 100 nằm trên một trong năm phiếu được chọn là $5/100$.

Nếu đáp án (c) lớn hơn hoặc bằng đáp án (f) thì rất lạ: rút không hoàn lại giúp tìm số 100 dễ hơn. Cũng vì vậy, khi tìm một món đồ thất lạc, kiểm tra các địa điểm mà không lặp lại sẽ hợp lý hơn. Tuy nhiên, đáp án (c) chỉ nhỏ hơn (f) một chút là điều dễ hiểu: ở (c), việc rút trúng lại cùng một phiếu không mấy khả năng xảy ra, dù bài toán sinh nhật cho thấy khả năng ấy lớn hơn nhiều người nghĩ. ◇

### 3.6 Hàm phân phối tích lũy

Một hàm khác mô tả phân phối của biến ngẫu nhiên là *hàm phân phối tích lũy* (CDF). Khác với PMF chỉ có ở biến ngẫu nhiên rời rạc, CDF được định nghĩa cho mọi biến ngẫu nhiên.

**Định nghĩa 3.6.1.** Hàm phân phối tích lũy của biến ngẫu nhiên $X$ là hàm $F_X$ cho bởi $F_X(x)=P(X\le x)$. Khi không thể nhầm lẫn, đôi khi ta bỏ chỉ số dưới và chỉ viết $F$ (hoặc một chữ cái khác).

Ví dụ tiếp theo cho thấy với biến ngẫu nhiên rời rạc, ta có thể chuyển đổi giữa CDF và PMF.

**Ví dụ 3.6.2.** Cho $X\sim\operatorname{Bin}(4,1/2)$. Hình 3.8 vẽ PMF và CDF của $X$.

- **Từ PMF sang CDF:** Để tính $P(X\le1{,}5)$, tức giá trị CDF tại $1{,}5$, cộng các giá trị PMF ở mọi điểm thuộc miền giá trị khả dĩ không vượt quá $1{,}5$:

  $$P(X\le1{,}5)=P(X=0)+P(X=1)=\left(\frac12\right)^4+4\left(\frac12\right)^4=\frac5{16}.$$

  Tương tự, CDF tại điểm $x$ bất kỳ bằng tổng chiều cao những cột PMF ở các giá trị không vượt quá $x$.

- **Từ CDF sang PMF:** CDF của biến rời rạc gồm những bước nhảy và đoạn nằm ngang. Độ cao bước nhảy tại $x$ bằng giá trị PMF tại $x$. Chẳng hạn, ở Hình 3.8, bước nhảy CDF tại 2 có độ cao bằng cột PMF tại 2; hình đánh dấu điều này bằng dấu ngoặc nhọn. Các đoạn nằm ngang của CDF ứng với những giá trị nằm ngoài miền giá trị khả dĩ của $X$, nên PMF tại đó bằng 0. ◇

*Hình 3.8 (trang PDF 127).* PMF và CDF của $\operatorname{Bin}(4,1/2)$. Chiều cao cột $P(X=2)$ trong PMF cũng là độ cao bước nhảy của CDF tại 2.

Các CDF hợp lệ có những tính chất sau.

**Định lý 3.6.3 (Tính chất của CDF).** Mọi CDF $F$ đều thỏa:

- **Không giảm:** Nếu $x_1\le x_2$ thì $F(x_1)\le F(x_2)$.
- **Liên tục bên phải:** Như Hình 3.8, CDF liên tục, trừ khi có bước nhảy. Tại điểm có bước nhảy, CDF liên tục từ bên phải: với mọi $a$, $F(a)=\lim_{x\to a^+}F(x)$.
- **Giới hạn ở vô cực:** $\lim_{x\to-\infty}F(x)=0$ và $\lim_{x\to\infty}F(x)=1$.

**Chứng minh.** Các tính chất trên đúng với mọi CDF. Để đơn giản, và vì chương này tập trung vào biến rời rạc, ta chỉ chứng minh khi $F$ là CDF của biến ngẫu nhiên rời rạc $X$ có các giá trị khả dĩ $0,1,2,\ldots$. Hình 3.8 minh họa: CDF không giảm, có các đoạn ngang; liên tục từ bên phải, mỗi bước nhảy được vẽ với chấm tròn rỗng ở dưới và chấm đặc ở trên; tiến đến 0 khi $x\to-\infty$ và đến 1 khi $x\to\infty$. Trong ví dụ này, hàm thực sự đạt 0 và 1; ở ví dụ khác, nó có thể chỉ tiến đến một hoặc cả hai giá trị ấy.

Tính chất thứ nhất đúng vì $\{X\le x_1\}\subseteq\{X\le x_2\}$, nên $P(X\le x_1)\le P(X\le x_2)$. Lập luận này không cần $X$ rời rạc.

Với tính chất thứ hai, lưu ý rằng $P(X\le x)=P(X\le\lfloor x\rfloor)$, trong đó $\lfloor x\rfloor$ là số nguyên lớn nhất không vượt quá $x$. Ví dụ, $P(X\le4{,}9)=P(X\le4)$ vì $X$ chỉ nhận giá trị nguyên. Vì thế $F(a+b)=F(a)$ với mọi $b>0$ đủ nhỏ để $a+b<\lfloor a\rfloor+1$; chẳng hạn, nếu $a=4{,}9$ thì $0<b<0{,}1$. Điều này suy ra $F(a)=\lim_{x\to a^+}F(x)$; thực ra, nó còn mạnh hơn vì $F(x)$ bằng hẳn $F(a)$ khi $x$ ở đủ gần bên phải $a$.

Với tính chất thứ ba, $F(x)=0$ nếu $x<0$, và

$$\lim_{x\to\infty}F(x)
=\lim_{x\to\infty}P(X\le\lfloor x\rfloor)
=\lim_{x\to\infty}\sum_{n=0}^{\lfloor x\rfloor}P(X=n)
=\sum_{n=0}^{\infty}P(X=n)=1.\qquad\Box$$

Chiều ngược lại cũng đúng: ở Chương 5, ta sẽ chứng minh rằng với bất kỳ hàm $F$ nào thỏa những tính chất này, ta đều có thể xây dựng một biến ngẫu nhiên có CDF là $F$.

Tóm lại, ta đã thấy ba cách tương đương để diễn tả phân phối của biến ngẫu nhiên. Hai cách là PMF và CDF: chúng chứa cùng một lượng thông tin vì luôn có thể suy ra hàm này từ hàm kia. Với biến ngẫu nhiên rời rạc, PMF thường dễ thao tác hơn vì tính CDF đòi hỏi phép cộng tổng. Cách thứ ba là một câu chuyện giải thích chính xác cách phân phối hình thành. Ta đã dùng câu chuyện Nhị thức và Siêu bội để suy ra PMF tương ứng. Câu chuyện và PMF vì thế cũng chứa cùng thông tin, dù câu chuyện thường giúp chứng minh trực giác hơn việc tính toán với PMF.

### 3.7 Hàm của biến ngẫu nhiên

Ở mục này, ta bàn về việc áp dụng một hàm lên biến ngẫu nhiên và tìm hiểu vì sao kết quả vẫn là một biến ngẫu nhiên. Nếu $X$ là biến ngẫu nhiên thì $X^2$, $e^X$ và $\sin X$ cũng vậy; tổng quát hơn, $g(X)$ là biến ngẫu nhiên với mọi hàm $g:\mathbb R\to\mathbb R$.

Chẳng hạn, hai đội bóng rổ A và B thi đấu bảy trận, và $X$ là số trận thắng của A. Nếu hai đội ngang sức và các trận độc lập thì $X\sim\operatorname{Bin}(7,1/2)$. Đặt $g(x)=7-x$ và $h(x)=1$ khi $x\ge4$, còn $h(x)=0$ khi $x<4$. Khi đó $g(X)=7-X$ là số trận B thắng; $h(X)$ là biến chỉ báo A thắng đa số trận. Cả hai đều là biến ngẫu nhiên.

Để định nghĩa một cách hình thức, hãy trở lại đầu chương. Ta xét biến $X$ trên không gian mẫu sáu phần tử. Hình 3.1 dùng mũi tên biểu diễn cách $X$ gán một số thực cho từng viên sỏi trong không gian mẫu; nửa trái Hình 3.2 biểu diễn cùng việc đó bằng cách viết số vào từng viên sỏi.

Giờ ta áp dụng cùng một hàm $g$ lên mọi số đã viết. Thay cho $X(s_1),\ldots,X(s_6)$, ta được $g(X(s_1)),\ldots,g(X(s_6))$. Đó là một phép gán mới từ kết quả của thí nghiệm đến số thực, tức một biến ngẫu nhiên mới $g(X)$.

**Định nghĩa 3.7.1 (Hàm của biến ngẫu nhiên).** Với thí nghiệm có không gian mẫu $S$, biến ngẫu nhiên $X$ và hàm $g:\mathbb R\to\mathbb R$, $g(X)$ là biến ngẫu nhiên gán cho mỗi $s\in S$ giá trị $g(X(s))$.

Lấy $g(x)=\sqrt{x}$ để minh họa. Hình 3.9 cho thấy $g(X)$ là hàm hợp của $X$ và $g$: trước áp dụng $X$, sau đó áp dụng $g$. Hình 3.10 biểu diễn $g(X)$ ngắn gọn hơn bằng cách gắn giá trị trực tiếp vào từng kết quả mẫu. Cả hai hình đều cho thấy $g(X)$ là biến ngẫu nhiên: nếu $X$ nhận giá trị 4 thì $g(X)$ nhận giá trị 2.

Nếu biết PMF của biến rời rạc $X$, làm sao tìm PMF của $Y=g(X)$? Khi $g$ là hàm một đối một, câu trả lời đơn giản: miền giá trị khả dĩ của $Y$ gồm mọi $g(x)$ với $x$ thuộc miền giá trị khả dĩ của $X$, và

$$P(Y=g(x))=P(g(X)=g(x))=P(X=x).$$

Bảng dưới minh họa: nếu các giá trị khả dĩ phân biệt của $X$ là $x_1,x_2,\ldots$, với xác suất tương ứng $p_1,p_2,\ldots$, thì các giá trị khả dĩ phân biệt của $Y$ là $g(x_1),g(x_2),\ldots$, vẫn có cùng dãy xác suất.

| Giá trị $x$ của $X$ | $P(X=x)$ | Giá trị $y$ của $Y$ | $P(Y=y)$ |
|---|---:|---|---:|
| $x_1$ | $p_1$ | $g(x_1)$ | $p_1$ |
| $x_2$ | $p_2$ | $g(x_2)$ | $p_2$ |
| $x_3$ | $p_3$ | $g(x_3)$ | $p_3$ |
| $\vdots$ | $\vdots$ | $\vdots$ | $\vdots$ |

*Hình 3.9 (trang PDF 130).* Biến ngẫu nhiên $X$ được định nghĩa trên không gian mẫu sáu phần tử, có các giá trị khả dĩ 0, 1, 4. Hàm $g$ là căn bậc hai. Hàm hợp $g(X)=\sqrt X$ là biến ngẫu nhiên có các giá trị khả dĩ 0, 1, 2.

*Hình 3.10.* Vì $g(X)=\sqrt X$ gắn một số với từng viên sỏi, nó là một biến ngẫu nhiên.

Điều này gợi ra một cách tìm PMF của biến ngẫu nhiên có phân phối chưa quen: thử biểu diễn nó thành hàm một đối một của biến ngẫu nhiên có phân phối đã biết.

**Ví dụ 3.7.2 (Bước đi ngẫu nhiên, trang PDF 131).** Một hạt đi $n$ bước trên trục số, bắt đầu từ 0. Mỗi bước hạt đi sang phải hoặc trái một đơn vị với xác suất bằng nhau. Giả sử các bước độc lập. Gọi $Y$ là vị trí của hạt sau $n$ bước. Tìm PMF của $Y$.

**Lời giải.** Coi mỗi bước là một phép thử Bernoulli, trong đó sang phải là thành công, sang trái là thất bại. Số bước sang phải là biến $X\sim\operatorname{Bin}(n,1/2)$. Nếu $X=j$, hạt đi $j$ bước sang phải và $n-j$ bước sang trái, nên vị trí cuối là $j-(n-j)=2j-n$. Vậy $Y=2X-n$, một hàm một đối một của $X$. Vì $X$ nhận giá trị trong $\{0,1,\ldots,n\}$ nên $Y$ nhận giá trị trong $\{-n,2-n,4-n,\ldots,n\}$. Do đó

$$P(Y=k)=P(2X-n=k)
=P\!\left(X=\frac{n+k}{2}\right)
=\binom n{(n+k)/2}\left(\frac12\right)^n,$$

nếu $k$ là số nguyên từ $-n$ đến $n$ và $n+k$ chẵn; ngoài ra xác suất bằng 0. ◇

Nếu $g$ không một đối một, một giá trị $y$ có thể ứng với nhiều giá trị $x$ thỏa $g(x)=y$. Để tính $P(g(X)=y)$, ta cộng xác suất của tất cả các giá trị $x$ ấy.

**Định lý 3.7.3 (PMF của $g(X)$).** Cho biến ngẫu nhiên rời rạc $X$ và hàm $g:\mathbb R\to\mathbb R$. Miền giá trị khả dĩ của $g(X)$ gồm mọi $y$ sao cho $g(x)=y$ với ít nhất một $x$ thuộc miền giá trị khả dĩ của $X$; PMF là

$$P(g(X)=y)=\sum_{x:g(x)=y}P(X=x)$$

với mọi $y$ trong miền giá trị khả dĩ của $g(X)$.

**Ví dụ 3.7.4.** Tiếp tục ví dụ trước, gọi $D$ là khoảng cách từ hạt đến gốc sau $n$ bước. Giả sử $n$ chẵn. Tìm PMF của $D$.

**Lời giải.** Ta có $D=|Y|$, một hàm của $Y$ nhưng không một đối một. Biến cố $D=0$ chính là $Y=0$. Với $k=2,4,\ldots,n$, biến cố $D=k$ là hợp của hai biến cố xung khắc $\{Y=k\}$ và $\{Y=-k\}$. Vì vậy

$$P(D=0)=\binom n{n/2}\left(\frac12\right)^n,$$

$$P(D=k)=P(Y=k)+P(Y=-k)
=2\binom n{(n+k)/2}\left(\frac12\right)^n,\qquad k=2,4,\ldots,n.$$

Bước cuối dùng tính đối xứng $P(Y=k)=P(Y=-k)$. ◇

Lập luận cho hàm của một biến ngẫu nhiên có thể mở rộng sang hàm của nhiều biến. Ta đã gặp hàm cộng, ánh xạ $(x,y)$ thành $x+y$: Ví dụ 3.2.5 coi $T=X+Y$ là một biến ngẫu nhiên, khi $X,Y$ là kết quả gieo xúc xắc.

**Định nghĩa 3.7.5 (Hàm của hai biến ngẫu nhiên).** Với thí nghiệm có không gian mẫu $S$, nếu $X,Y$ lần lượt gán cho $s\in S$ các giá trị $X(s),Y(s)$ thì $g(X,Y)$ là biến ngẫu nhiên gán cho $s$ giá trị $g(X(s),Y(s))$.

Một cách hiểu phép ánh xạ từ $S$ đến $\mathbb R$ do $g(X,Y)$ tạo ra là lập bảng các giá trị $X,Y,g(X,Y)$ dưới những kết quả mẫu khác nhau. Dễ thấy $X+Y$ là biến ngẫu nhiên: khi quan sát được $X=x,Y=y$ thì $X+Y$ nhận giá trị $x+y$. Với ví dụ ít quen hơn như $\max(X,Y)$, nguyên lý vẫn vậy: khi $X=x,Y=y$, biến $\max(X,Y)$ nhận giá trị $\max(x,y)$.

**Ví dụ 3.7.6 (Giá trị lớn hơn trong hai lần gieo xúc xắc).** Gieo hai xúc xắc công bằng sáu mặt. Gọi $X$ là kết quả xúc xắc thứ nhất và $Y$ là kết quả xúc xắc thứ hai. Bảng cho giá trị $X,Y,\max(X,Y)$ dưới 7 trong 36 kết quả của không gian mẫu:

| Kết quả $s$ | $X$ | $Y$ | $\max(X,Y)$ |
|---|---:|---:|---:|
| $(1,2)$ | 1 | 2 | 2 |
| $(1,6)$ | 1 | 6 | 6 |
| $(2,5)$ | 2 | 5 | 5 |
| $(3,1)$ | 3 | 1 | 3 |
| $(4,3)$ | 4 | 3 | 4 |
| $(5,4)$ | 5 | 4 | 5 |
| $(6,6)$ | 6 | 6 | 6 |

Vậy $\max(X,Y)$ thực sự gán một giá trị số cho mỗi kết quả mẫu. PMF của nó là

| $k$ | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---:|---:|---:|---:|---:|---:|
| $P(\max(X,Y)=k)$ | $1/36$ | $3/36$ | $5/36$ | $7/36$ | $9/36$ | $11/36$ |

Có thể liệt kê để đếm, nhưng cách tính sau ít dài dòng và dễ khái quát hơn:

$$\begin{aligned}
P(\max(X,Y)=5)
&=P(X=5,Y\le4)+P(X\le4,Y=5)+P(X=5,Y=5)\\
&=2P(X=5,Y\le4)+\frac1{36}
=2\frac4{36}+\frac1{36}=\frac9{36}.
\end{aligned}$$

◇

**Lưu ý 3.7.7 (Nhầm loại đối tượng và “ma thuật cảm ứng”).** Nhiều lỗi phổ biến trong xác suất xuất phát từ việc nhầm lẫn các đối tượng nền tảng: phân phối, biến ngẫu nhiên, biến cố và con số. Đó là lỗi *nhầm loại đối tượng*. Lỗi này không đơn thuần là trả lời sai, mà chắc chắn sai vì dùng sai loại đối tượng. Chẳng hạn, trả lời câu hỏi “Boston có bao nhiêu dân?” bằng “$-42$”, “$\pi$” hay “voi hồng” là nhầm loại đối tượng. Có thể ta không biết dân số một thành phố, nhưng biết nó là một số nguyên không âm tại mỗi thời điểm. Để tránh sai từ gốc, hãy luôn xem câu trả lời cần thuộc loại đối tượng nào.

Lỗi nhầm loại đặc biệt thường gặp là đồng nhất biến ngẫu nhiên với phân phối của nó. Chúng tôi gọi lỗi này là *ma thuật cảm ứng*, mượn một thuật ngữ nhân học chỉ niềm tin rằng có thể tác động đến vật bằng cách thao tác trên hình ảnh đại diện của nó. Câu nói sau giúp phân biệt hai đối tượng:

> Từ ngữ không phải sự vật; bản đồ không phải lãnh thổ. — Alfred Korzybski

Có thể hình dung phân phối của biến ngẫu nhiên như bản đồ hoặc bản thiết kế mô tả nó. Cũng như nhiều ngôi nhà có thể cùng một bản thiết kế, nhiều biến ngẫu nhiên có thể cùng phân phối dù chúng tóm tắt các thí nghiệm khác nhau và ánh xạ từ những không gian mẫu khác nhau.

Hai ví dụ về “ma thuật cảm ứng”:

- Có biến ngẫu nhiên $X$, rồi tìm PMF của $2X$ bằng cách nhân PMF của $X$ với 2. Điều đó vô lý vì tổng các xác suất không còn bằng 1. Nếu $X$ nhận giá trị $x_j$ với xác suất $p_j$ thì $2X$ nhận giá trị $2x_j$ với cùng xác suất $p_j$. Vì vậy PMF của $2X$ là PMF của $X$ được giãn *theo chiều ngang*, không phải chiều dọc. Hình 3.11 vẽ PMF của $X$ có miền giá trị $\{0,1,2,3,4\}$ và của $2X$ có miền giá trị $\{0,2,4,6,8\}$. $X$ có thể nhận số lẻ, còn $2X$ luôn chẵn.
- Khẳng định rằng vì $X,Y$ cùng phân phối nên chúng luôn bằng nhau, tức $P(X=Y)=1$. Cùng phân phối không có nghĩa hai biến luôn bằng nhau, thậm chí không đảm bảo chúng từng bằng nhau. Ta đã thấy điều này ở Ví dụ 3.2.5. Ví dụ khác: tung đồng xu công bằng một lần, cho $X$ là biến chỉ báo ra ngửa, $Y=1-X$ là biến chỉ báo ra sấp. Cả hai có phân phối $\operatorname{Bern}(1/2)$ nhưng biến cố $X=Y$ là bất khả thi. PMF của chúng là cùng một hàm, nhưng $X,Y$ là hai ánh xạ khác nhau từ không gian mẫu tới số thực. Nếu $Z$ là biến chỉ báo ra ngửa ở lần tung thứ hai, độc lập với lần thứ nhất, thì $Z$ cũng có phân phối $\operatorname{Bern}(1/2)$ nhưng khác biến $X$. Khi ấy $P(Z=X)=P(HH\text{ hoặc }TT)=1/2$.

*Hình 3.11 (trang PDF 134).* PMF của $X$ (trên) và PMF của $2X$ (dưới).

### 3.8 Tính độc lập của các biến ngẫu nhiên

Tương tự tính độc lập của các biến cố, ta có thể định nghĩa tính độc lập của các biến ngẫu nhiên. Theo trực giác, nếu $X,Y$ độc lập thì biết giá trị $X$ không cho thông tin về giá trị $Y$, và ngược lại. Định nghĩa sau diễn đạt chính xác ý đó.

**Định nghĩa 3.8.1 (Hai biến ngẫu nhiên độc lập).** Các biến ngẫu nhiên $X,Y$ được gọi là độc lập nếu

$$P(X\le x,Y\le y)=P(X\le x)P(Y\le y)$$

với mọi $x,y\in\mathbb R$. Trong trường hợp rời rạc, điều này tương đương

$$P(X=x,Y=y)=P(X=x)P(Y=y)$$

với mọi $x,y$ tương ứng thuộc miền giá trị khả dĩ của $X,Y$.

**Định nghĩa 3.8.2 (Nhiều biến ngẫu nhiên độc lập).** Các biến $X_1,\ldots,X_n$ độc lập nếu

$$P(X_1\le x_1,\ldots,X_n\le x_n)
=P(X_1\le x_1)\cdots P(X_n\le x_n)$$

với mọi $x_1,\ldots,x_n\in\mathbb R$. Với vô hạn biến ngẫu nhiên, ta gọi chúng độc lập nếu mọi tập con hữu hạn của chúng đều độc lập.

So với tiêu chí độc lập của $n$ biến cố, ở đây thoạt nhìn chỉ cần một đẳng thức, trong khi với biến cố ta phải kiểm tra mọi cặp, mọi bộ ba, v.v. Nhưng đẳng thức của các biến ngẫu nhiên phải đúng với *mọi* bộ $x_1,\ldots,x_n$: đó là vô hạn điều kiện. Chỉ cần tìm được một bộ giá trị khiến đẳng thức sai là đủ kết luận các biến không độc lập.

**Lưu ý 3.8.3.** Nếu $X_1,\ldots,X_n$ độc lập thì chúng độc lập từng đôi: $X_i$ độc lập với $X_j$ khi $i\ne j$. Ý tưởng chứng minh là cho mọi $x_k$ khác $x_i,x_j$ tiến tới $\infty$ trong định nghĩa độc lập, vì khi đó $\{X_k<\infty\}$ chắc chắn đúng (cần thêm lập luận để biện minh đầy đủ việc lấy giới hạn). Chiều ngược lại nói chung sai, như đã thấy ở Chương 2 với các biến cố. Một phản ví dụ đơn giản là dùng các biến chỉ báo của ba biến cố $A,B,C$ độc lập từng đôi nhưng không độc lập trong Ví dụ 2.5.5.

**Ví dụ 3.8.4 (trang PDF 136).** Khi gieo hai xúc xắc công bằng, gọi $X$ là số ở xúc xắc thứ nhất, $Y$ là số ở xúc xắc thứ hai. Khi ấy $X+Y$ và $X-Y$ không độc lập, vì

$$0=P(X+Y=12,\ X-Y=1)
\ne P(X+Y=12)P(X-Y=1)
=\frac1{36}\cdot\frac5{36}.$$

Ta đã tìm được một cặp giá trị $(s,d)$ khiến đẳng thức độc lập sai. Trực giác cũng vậy: nếu biết tổng là 12 thì hiệu buộc bằng 0; hai biến cung cấp thông tin về nhau. ◇

Nếu $X,Y$ độc lập thì, chẳng hạn, $X^2$ và $Y^3$ cũng độc lập: nếu biết $X^2$ cho thông tin về $Y^3$ thì biết $X$ cũng sẽ cho thông tin về $Y$. Tổng quát, mọi hàm của $X$ đều độc lập với mọi hàm của $Y$. Ở đây ta không đưa ra chứng minh hình thức, nhưng điều này phù hợp với trực giác về thông tin.

**Định nghĩa 3.8.5 (i.i.d.).** Ta thường xét các biến ngẫu nhiên vừa độc lập vừa có cùng phân phối. Chúng được gọi là *độc lập và cùng phân phối*, viết tắt i.i.d.

**Lưu ý 3.8.6 (Độc lập và cùng phân phối).** Đây là hai khái niệm khác nhau thường bị nhầm. Các biến độc lập nếu chúng không cho thông tin về nhau; chúng cùng phân phối nếu có cùng PMF (hoặc tương đương, cùng CDF). Hai tính chất không kéo theo nhau. Có thể có:

- **Độc lập và cùng phân phối:** $X$ là kết quả một lần gieo xúc xắc, $Y$ là kết quả lần gieo thứ hai độc lập.
- **Độc lập nhưng khác phân phối:** $X$ là kết quả gieo xúc xắc; $Y$ là giá đóng cửa của chỉ số Dow Jones sau một tháng. Hai biến không cho thông tin về nhau (ít nhất ta rất mong vậy), và khác phân phối.
- **Phụ thuộc nhưng cùng phân phối:** $X$ là số lần ngửa và $Y$ là số lần sấp trong cùng $n$ lần tung đồng xu công bằng, độc lập. Cả hai có phân phối $\operatorname{Bin}(n,1/2)$, nhưng biết $X$ thì xác định được $Y$.
- **Phụ thuộc và khác phân phối:** $X$ là biến chỉ báo đảng đa số có giữ được quyền kiểm soát Hạ viện Hoa Kỳ sau cuộc bầu cử tiếp theo hay không; $Y$ là mức độ ủng hộ trung bình của đảng đó trong các thăm dò diễn ra trong vòng một tháng trước bầu cử. Hai biến phụ thuộc và khác phân phối.

Lấy tổng các biến Bernoulli i.i.d. cho phép viết câu chuyện Nhị thức dưới dạng đại số.

**Định lý 3.8.7.** Nếu $X\sim\operatorname{Bin}(n,p)$, hiểu là số thành công trong $n$ phép thử Bernoulli độc lập, mỗi phép thử có xác suất thành công $p$, thì $X=X_1+\cdots+X_n$ với các $X_i$ i.i.d. $\operatorname{Bern}(p)$.

**Chứng minh.** Đặt $X_i=1$ nếu phép thử thứ $i$ thành công, bằng 0 nếu thất bại. Hình dung mỗi phép thử có một người phụ trách và người đó giơ tay nếu phép thử thành công. Đếm số tay giơ lên, tức cộng các $X_i$, ta được tổng số thành công $X$. □

Một tính chất quan trọng: tổng các biến Nhị thức độc lập có cùng xác suất thành công lại là một biến Nhị thức. Định lý trước cho chứng minh ngắn, nhưng ta trình bày thêm hai cách khác để so sánh.

**Định lý 3.8.8.** Nếu $X\sim\operatorname{Bin}(n,p)$, $Y\sim\operatorname{Bin}(m,p)$ và $X,Y$ độc lập, thì $X+Y\sim\operatorname{Bin}(n+m,p)$.

**Chứng minh.** Ba cách, mỗi cách minh họa một kỹ thuật hữu ích.

1. **Luật xác suất toàn phần:** Đặt $q=1-p$. Điều kiện hóa theo $X$ để tìm trực tiếp PMF của $X+Y$:

   $$\begin{aligned}
   P(X+Y=k)
   &=\sum_{j=0}^k P(X+Y=k\mid X=j)P(X=j)\\
   &=\sum_{j=0}^k P(Y=k-j)P(X=j)\\
   &=\sum_{j=0}^k\binom m{k-j}p^{k-j}q^{m-k+j}
     \binom nj p^j q^{n-j}\\
   &=p^kq^{n+m-k}\sum_{j=0}^k\binom m{k-j}\binom nj\\
   &=\binom{n+m}k p^kq^{n+m-k}.
   \end{aligned}$$

   Dòng thứ hai dùng tính độc lập để bỏ điều kiện trong $P(Y=k-j\mid X=j)$; dòng cuối dùng đồng nhất thức Vandermonde. Biểu thức thu được chính là PMF của $\operatorname{Bin}(n+m,p)$.

2. **Biểu diễn thành tổng:** Viết $X=X_1+\cdots+X_n$ và $Y=Y_1+\cdots+Y_m$, với tất cả các $X_i,Y_j$ i.i.d. $\operatorname{Bern}(p)$. Vậy $X+Y$ là tổng của $n+m$ biến Bernoulli i.i.d., nên có phân phối $\operatorname{Bin}(n+m,p)$.

3. **Câu chuyện:** $X$ đếm thành công trong $n$ phép thử độc lập, $Y$ đếm thành công trong $m$ phép thử độc lập bổ sung, tất cả cùng xác suất thành công. Tổng $X+Y$ đếm thành công trong $n+m$ phép thử, đúng là câu chuyện $\operatorname{Bin}(n+m,p)$. □

**Định nghĩa 3.8.9 (Độc lập có điều kiện của các biến ngẫu nhiên).** $X,Y$ độc lập có điều kiện theo $Z$ nếu với mọi $x,y\in\mathbb R$ và mọi $z$ thuộc miền giá trị khả dĩ của $Z$,

$$P(X\le x,Y\le y\mid Z=z)
=P(X\le x\mid Z=z)P(Y\le y\mid Z=z).$$

Với các biến rời rạc, điều kiện tương đương là

$$P(X=x,Y=y\mid Z=z)
=P(X=x\mid Z=z)P(Y=y\mid Z=z).$$

Đúng như tên gọi, đây là định nghĩa độc lập khi ta điều kiện hóa mọi xác suất theo $Z=z$ và đòi hỏi đẳng thức đúng với mọi $z$ khả dĩ.

**Định nghĩa 3.8.10 (PMF có điều kiện).** Với hai biến ngẫu nhiên rời rạc $X,Z$, hàm $P(X=x\mid Z=z)$ khi xem như một hàm theo $x$ với $z$ cố định được gọi là PMF có điều kiện của $X$ khi biết $Z=z$.

Độc lập không kéo theo độc lập có điều kiện, và ngược lại.

**Ví dụ 3.8.11 (Trò đồng xu trùng mặt).** Hai người chơi A, B mỗi người có một đồng xu công bằng và tung độc lập. Nếu hai xu cho cùng mặt thì A thắng, khác mặt thì B thắng. Đặt $X=1$ nếu xu A ra ngửa, $X=-1$ nếu ra sấp; định nghĩa $Y$ tương tự cho B. Các biến $X,Y$ được gọi là *dấu ngẫu nhiên*. Đặt $Z=XY$: $Z=1$ nếu A thắng, $Z=-1$ nếu B thắng. $X,Y$ độc lập khi không biết $Z$, nhưng nếu biết $Z=1$ thì $X=Y$. Vậy chúng phụ thuộc khi điều kiện hóa theo $Z$. ◇

**Ví dụ 3.8.12 (Hai nguyên nhân khiến chuông báo cháy reo).** Giả sử chuông chỉ reo khi có cháy hoặc có người quay bỏng ngô trong lò vi sóng quá lâu, và hai biến cố ấy độc lập. Gọi $X$ là biến chỉ báo có cháy, $Y$ là biến chỉ báo quay bỏng ngô quá lâu, $Z$ là biến chỉ báo chuông reo. Ta có $Z=\max(X,Y)$. Theo giả thiết, $X,Y$ độc lập. Nhưng khi biết chuông đã reo và không ai quay bỏng ngô, ta biết chắc có cháy; vì vậy $X,Y$ phụ thuộc có điều kiện theo $Z$. Ví dụ này có cùng cấu trúc với tình huống “chỉ có hai người bạn từng gọi điện cho tôi” ở Ví dụ 2.5.10. ◇

**Ví dụ 3.8.13 (Đối thủ bí ẩn).** Giả sử bạn chơi hai ván quần vợt với một trong hai người sinh đôi giống hệt nhau. Với người thứ nhất, khả năng thắng thua của bạn ngang nhau; với người thứ hai, bạn có xác suất thắng $3/4$. Bạn không phân biệt được người đang chơi cho đến sau hai ván. Đặt $Z$ là biến chỉ báo đối thủ là người ngang sức; $X,Y$ lần lượt là biến chỉ báo thắng ván một và ván hai. Nếu $Z=1$, $X,Y$ i.i.d. $\operatorname{Bern}(1/2)$; nếu $Z=0$, chúng i.i.d. $\operatorname{Bern}(3/4)$. Vậy chúng độc lập có điều kiện theo $Z$. Nhưng nếu không biết $Z$, chúng phụ thuộc: quan sát $X=1$ khiến ta có cơ sở tin đối thủ là người chơi kém hơn, tức $P(Y=1\mid X=1)>P(Y=1)$. Trận trước giúp suy ra đối thủ là ai, rồi dự đoán trận sau. Ví dụ này có cùng cấu trúc với “đồng xu ngẫu nhiên” ở Ví dụ 2.3.7. ◇

### 3.9 Liên hệ giữa phân phối Nhị thức và Siêu bội

Hai phân phối liên hệ với nhau theo hai cách quan trọng. Ta có thể đi từ Nhị thức sang Siêu bội bằng cách điều kiện hóa, và từ Siêu bội sang Nhị thức bằng cách lấy giới hạn. Trước tiên là một ví dụ gợi ý.

**Ví dụ 3.9.1 (Kiểm định chính xác Fisher, trang PDF 140).** Một nhà khoa học muốn nghiên cứu liệu phụ nữ hay nam giới có nguy cơ mắc một bệnh cao hơn, hay hai nhóm có nguy cơ bằng nhau. Lấy ngẫu nhiên $n$ phụ nữ và $m$ nam giới, kiểm tra bệnh cho từng người (giả sử xét nghiệm chính xác hoàn toàn). Số phụ nữ và nam giới mắc bệnh lần lượt là $X,Y$, độc lập, với $X\sim\operatorname{Bin}(n,p_1)$ và $Y\sim\operatorname{Bin}(m,p_2)$. Các tham số $p_1,p_2$ chưa biết; ta muốn kiểm tra $p_1=p_2$ (gọi là *giả thuyết không* trong thống kê).

Xét bảng $2\times2$: hàng biểu thị tình trạng bệnh, cột biểu thị giới tính; tổng bốn ô là $n+m$. Giả sử quan sát thấy $X+Y=r$. Kiểm định chính xác Fisher điều kiện hóa theo tổng hàng và cột, coi $n,m,r$ cố định, rồi xét xem giá trị $X$ quan sát được có “cực đoan” so với phân phối có điều kiện hay không. Dưới giả thuyết không, hãy tìm PMF có điều kiện của $X$ khi biết $X+Y=r$.

**Lời giải.** Bảng số lượng với $n,m,r$ cố định:

| | Phụ nữ | Nam giới | Tổng |
|---|---:|---:|---:|
| Mắc bệnh | $x$ | $r-x$ | $r$ |
| Không mắc bệnh | $n-x$ | $m-r+x$ | $n+m-r$ |
| Tổng | $n$ | $m$ | $n+m$ |

Theo quy tắc Bayes và tính độc lập của $X,Y$,

$$P(X=x\mid X+Y=r)
=\frac{P(X+Y=r\mid X=x)P(X=x)}{P(X+Y=r)}
=\frac{P(Y=r-x)P(X=x)}{P(X+Y=r)}.$$

Dưới giả thuyết không, đặt $p=p_1=p_2$. Khi ấy $X\sim\operatorname{Bin}(n,p)$ và $Y\sim\operatorname{Bin}(m,p)$ độc lập, nên $X+Y\sim\operatorname{Bin}(n+m,p)$. Vì thế

$$P(X=x\mid X+Y=r)
=\frac{\binom m{r-x}p^{r-x}(1-p)^{m-r+x}
        \binom nx p^x(1-p)^{n-x}}
       {\binom{n+m}r p^r(1-p)^{n+m-r}}
=\frac{\binom nx\binom m{r-x}}{\binom{n+m}r}.$$

Vậy phân phối có điều kiện của $X$ là Siêu bội với tham số $(n,m,r)$.

Để hiểu vì sao phân phối Siêu bội xuất hiện dường như bất ngờ, hãy liên hệ với câu chuyện đánh dấu và bắt lại nai. Khi ấy ta quan tâm số nai đã đánh dấu trong mẫu bắt lại. Ở đây hãy xem phụ nữ như nai đã đánh dấu và nam giới như nai chưa đánh dấu. Thay vì ngẫu nhiên bắt lại $r$ con nai, ta có $X+Y=r$ người mắc bệnh; dưới giả thuyết không, mọi tập gồm $r$ người bệnh đều có khả năng như nhau. Vì thế, khi biết $X+Y=r$, biến $X$ đếm số phụ nữ trong $r$ người bệnh. Đó đúng là số nai đã đánh dấu trong mẫu bắt lại, có phân phối $\operatorname{HGeom}(n,m,r)$.

Một điều thú vị và hữu ích trong thống kê: phân phối có điều kiện của $X$ không phụ thuộc $p$. Trước khi điều kiện hóa, $X\sim\operatorname{Bin}(n,p)$; sau đó $p$ biến mất. Điều này hợp lý vì khi đã biết $X+Y=r$, ta làm việc trực tiếp với quần thể gồm $r$ người mắc và $n+m-r$ người không mắc, không cần quan tâm giá trị $p$ đã tạo ra quần thể ấy. ◇

Ví dụ vừa rồi cũng chứng minh định lý sau.

**Định lý 3.9.2.** Nếu $X\sim\operatorname{Bin}(n,p)$, $Y\sim\operatorname{Bin}(m,p)$ và $X,Y$ độc lập, thì phân phối của $X$ có điều kiện theo $X+Y=r$ là $\operatorname{HGeom}(n,m,r)$.

Theo chiều ngược lại, Nhị thức là trường hợp giới hạn của Siêu bội.

**Định lý 3.9.3.** Nếu $X\sim\operatorname{HGeom}(w,b,n)$ và $N=w+b\to\infty$ trong khi $p=w/(w+b)$ giữ cố định, thì PMF của $X$ hội tụ đến PMF $\operatorname{Bin}(n,p)$.

**Chứng minh.** Đặt $q=1-p$. Lấy giới hạn của PMF Siêu bội; theo Định lý 3.4.5,

$$\begin{aligned}
P(X=k)
&=\frac{\binom wk\binom b{n-k}}{\binom{w+b}n}
=\binom nk\frac{\binom{w+b-n}{w-k}}{\binom{w+b}w}\\
&=\binom nk
\frac{w(w-1)\cdots(w-k+1)\,
      b(b-1)\cdots(b-n+k+1)}
     {(w+b)(w+b-1)\cdots(w+b-n+1)}\\
&=\binom nk
\frac{p(p-1/N)\cdots(p-(k-1)/N)\,
      q(q-1/N)\cdots(q-(n-k-1)/N)}
     {(1-1/N)(1-2/N)\cdots(1-(n-1)/N)}.
\end{aligned}$$

Khi $N\to\infty$, mẫu số tiến đến 1 và phần tích ở tử số tiến đến $p^kq^{n-k}$. Vậy

$$P(X=k)\longrightarrow\binom nk p^kq^{n-k},$$

chính là PMF của $\operatorname{Bin}(n,p)$. □

Câu chuyện Nhị thức và Siêu bội cho trực giác về kết quả này: với bình gồm $w$ bóng trắng và $b$ bóng đen, rút $n$ lần có hoàn lại tạo phân phối Nhị thức, còn rút không hoàn lại tạo phân phối Siêu bội. Khi tổng số bóng rất lớn so với số bóng rút, hai cách rút hầu như tương đương. Trong thực hành, nếu $N=w+b$ lớn so với $n$, ta có thể xấp xỉ PMF $\operatorname{HGeom}(w,b,n)$ bằng PMF $\operatorname{Bin}(n,w/(w+b))$.

Bài toán sinh nhật cho thấy khi rút có hoàn lại, khả năng rút lại ít nhất một bóng có thể khá cao: chẳng hạn rút 1.200 lần từ một triệu bóng thì xác suất có bóng được rút hơn một lần khoảng 51%! Khả năng ấy giảm khi $N$ tăng; ngay cả khi vẫn có vài lần trùng, phép xấp xỉ có thể hợp lý nếu gần như toàn bộ bóng trong mẫu chỉ được rút một lần.

### 3.10 Tóm tắt

Biến ngẫu nhiên là một hàm gán số thực cho mọi kết quả khả dĩ của thí nghiệm. Phân phối của biến $X$ xác định đầy đủ xác suất của các biến cố liên quan đến $X$, chẳng hạn $\{X=3\}$ và $\{1\le X\le5\}$. Phân phối của biến rời rạc có thể được mô tả bằng PMF, CDF hoặc một câu chuyện. PMF là hàm $P(X=x)$; CDF là hàm $P(X\le x)$, với $x\in\mathbb R$. Câu chuyện mô tả một thí nghiệm có thể tạo ra biến ngẫu nhiên cùng phân phối với $X$.

Cần phân biệt biến ngẫu nhiên và phân phối của nó: phân phối là bản thiết kế để tạo biến, nhưng các biến khác nhau có thể cùng phân phối, như nhiều ngôi nhà có thể xây từ cùng một bản thiết kế.

Bốn họ phân phối rời rạc có tên là Bernoulli, Nhị thức, Siêu bội và đều rời rạc. Mỗi họ được xác định thêm bằng các tham số:

- $X\sim\operatorname{Bern}(p)$ là biến chỉ báo thành công của một phép thử Bernoulli có xác suất thành công $p$.
- $X\sim\operatorname{Bin}(n,p)$ đếm thành công trong $n$ phép thử Bernoulli độc lập, cùng xác suất thành công $p$.
- $X\sim\operatorname{HGeom}(w,b,n)$ đếm bóng trắng trong mẫu $n$ bóng rút không hoàn lại từ bình có $w$ bóng trắng và $b$ bóng đen.
- $X\sim\operatorname{DUnif}(C)$ là phần tử chọn đều ngẫu nhiên từ tập hữu hạn $C$.

Hàm của biến ngẫu nhiên vẫn là biến ngẫu nhiên. Nếu biết PMF của $X$, có thể tìm $P(g(X)=k)$ bằng cách diễn đạt $\{g(X)=k\}$ thành biến cố tương đương theo $X$, rồi dùng PMF của $X$.

Hai biến ngẫu nhiên độc lập nếu biết giá trị một biến không cho thông tin về biến kia. Điều này không liên quan tới việc chúng có cùng phân phối hay không. Chương 7 sẽ bàn cách xét các biến phụ thuộc thông qua phân phối chung của chúng.

Đến đây ta đã gặp bốn loại đối tượng cơ bản trong xác suất: phân phối, biến ngẫu nhiên, biến cố và con số. Hình 3.12 cho thấy mối liên hệ giữa chúng. CDF có thể làm bản thiết kế để tạo $X$; từ $X$ sinh ra các biến cố như $\{X\le x\}$. Biết xác suất các biến cố này sẽ xác định lại CDF, khép kín vòng liên hệ. Với biến rời rạc, PMF cũng có thể làm bản thiết kế.

*Hình 3.12 (trang PDF 143).* Bốn loại đối tượng cơ bản: phân phối (bản thiết kế), biến ngẫu nhiên, biến cố và con số. Từ CDF $F$, tạo biến $X$; từ $X$, tạo các biến khác bằng hàm $g(X)$. Các biến cố $\{X\le x\}$, $\{X=x\}$ mô tả $X$. Xác suất của chúng, xét cho mọi $x$, cho ta CDF và (trong trường hợp rời rạc) PMF.

### 3.11 R

#### Các phân phối trong R

Mọi phân phối có tên gặp trong sách đều đã được cài đặt trong R. Mục này giải thích cách làm việc với phân phối Nhị thức và Siêu bội trong R, cũng như cách sinh biến ngẫu nhiên từ một phân phối rời rạc có miền giá trị hữu hạn. Gõ <code>help(distributions)</code> để xem danh sách tiện lợi các phân phối có sẵn; nhiều phân phối khác có trong các gói R có thể nạp thêm.

Nhìn chung, với nhiều phân phối rời rạc có tên, ba hàm bắt đầu bằng <code>d</code>, <code>p</code>, <code>r</code> lần lượt cho PMF, CDF và việc sinh số ngẫu nhiên. Cần lưu ý: hàm bắt đầu bằng <code>p</code> là CDF, không phải PMF.

#### Phân phối Nhị thức

Ba hàm R là <code>dbinom</code>, <code>pbinom</code>, <code>rbinom</code>. Với phân phối Bernoulli, chỉ cần dùng các hàm Nhị thức với $n=1$.

- <code>dbinom</code> là PMF Nhị thức, nhận ba đối số: giá trị $x$ cần tính, rồi hai tham số $n,p$. Chẳng hạn <code>dbinom(3,5,0.2)</code> trả về $P(X=3)$ khi $X\sim\operatorname{Bin}(5,0{,}2)$:

  $$\texttt{dbinom(3,5,0.2)}
  =\binom53(0{,}2)^3(0{,}8)^2=0{,}0512.$$

- <code>pbinom</code> là CDF Nhị thức, cũng nhận $x,n,p$. <code>pbinom(3,5,0.2)</code> là $P(X\le3)$ khi $X\sim\operatorname{Bin}(5,0{,}2)$:

  $$\texttt{pbinom(3,5,0.2)}
  =\sum_{k=0}^3\binom5k(0{,}2)^k(0{,}8)^{5-k}
  \approx0{,}9933.$$

- <code>rbinom</code> sinh các biến Nhị thức. Đối số đầu là số biến cần sinh; hai đối số sau là $n,p$. Vậy <code>rbinom(7,5,0.2)</code> cho bảy giá trị của bảy biến i.i.d. $\operatorname{Bin}(5,0{,}2)$. Khi chạy, tác giả nhận được <code>2 1 0 0 1 0 0</code>, nhưng bạn rất có thể nhận kết quả khác.

Ta cũng có thể tính PMF, CDF trên cả một vectơ giá trị. <code>0:n</code> là cách viết nhanh dãy số nguyên từ 0 đến $n$. Lệnh <code>dbinom(0:5,5,0.2)</code> trả về sáu số $P(X=0),\ldots,P(X=5)$ khi $X\sim\operatorname{Bin}(5,0{,}2)$.

#### Phân phối Siêu bội

Ba hàm là <code>dhyper</code>, <code>phyper</code>, <code>rhyper</code>, tương ứng tính PMF, CDF và sinh biến ngẫu nhiên Siêu bội. Vì phân phối có ba tham số, mỗi hàm nhận bốn đối số. Với <code>dhyper</code>, <code>phyper</code>, đối số đầu là giá trị cần tính và ba đối số sau là tham số. <code>dhyper(k,w,b,n)</code> trả $P(X=k)$, còn <code>phyper(k,w,b,n)</code> trả $P(X\le k)$ khi $X\sim\operatorname{HGeom}(w,b,n)$. Với <code>rhyper</code>, đối số đầu là số biến cần sinh: <code>rhyper(100,w,b,n)</code> sinh 100 biến i.i.d. $\operatorname{HGeom}(w,b,n)$.

#### Phân phối rời rạc có miền giá trị hữu hạn

Có thể dùng lệnh <code>sample</code> để sinh biến từ bất kỳ phân phối rời rạc nào có miền giá trị hữu hạn. Khi mới giới thiệu, ta dùng <code>sample(n,k)</code> hoặc <code>sample(n,k,replace=TRUE)</code> để lấy mẫu $k$ lần từ các số $1,\ldots,n$, không hoàn lại hoặc có hoàn lại. Chẳng hạn, để sinh năm biến i.i.d. $\operatorname{DUnif}(\{1,\ldots,100\})$, dùng <code>sample(100,5,replace=TRUE)</code>.

Thực ra <code>sample</code> linh hoạt hơn nhiều. Muốn lấy mẫu từ $x_1,\ldots,x_n$ với các xác suất $p_1,\ldots,p_n$, ta tạo vectơ <code>x</code> chứa các $x_i$ và vectơ <code>p</code> chứa các $p_i$, rồi truyền cho <code>sample</code>. Ví dụ, muốn sinh 100 biến i.i.d. $X_1,\ldots,X_{100}$ với PMF

$$P(X_j=0)=0{,}25,\quad
P(X_j=1)=0{,}5,\quad
P(X_j=5)=0{,}1,\quad
P(X_j=10)=0{,}15,$$

và bằng 0 ở các giá trị khác, trước tiên dùng hàm <code>c</code> để tạo vectơ miền giá trị và xác suất:

    x <- c(0,1,5,10)
    p <- c(0.25,0.5,0.1,0.15)

Tiếp theo dùng lệnh:

    sample(x,100,prob=p,replace=TRUE)

Các đối số lần lượt là vectơ giá trị cần lấy mẫu, số mẫu cần sinh (ở đây là 100), xác suất tương ứng với mỗi giá trị (nếu bỏ qua thì mặc định bằng nhau), và lựa chọn lấy mẫu có hoàn lại.

### 3.12 Bài tập

#### PMF và CDF

**1.** Mọi người lần lượt đến dự tiệc. Trong khi chờ người khác, họ so sánh ngày sinh. Gọi $X$ là số người cần có để lần đầu xuất hiện hai người trùng ngày sinh: trước khi người thứ $X$ tới, không ai trùng ngày sinh; khi người ấy tới, có một cặp trùng. Tìm PMF của $X$.

**2.** (a) Thực hiện các phép thử Bernoulli độc lập với xác suất thành công $1/2$ cho đến khi có ít nhất một lần thành công. Tìm PMF của số phép thử đã thực hiện. (b) Lặp lại, nhưng dừng khi đã có cả ít nhất một lần thành công và ít nhất một lần thất bại. Tìm PMF của số phép thử.

**3.** Cho biến ngẫu nhiên $X$ có CDF $F$, và $Y=\mu+\sigma X$, trong đó $\mu,\sigma$ là số thực với $\sigma>0$. (Khi đó $Y$ được gọi là phép biến đổi vị trí–tỉ lệ của $X$; khái niệm này sẽ gặp nhiều ở Chương 5 và sau đó.) Tìm CDF của $Y$ theo $F$.

**4.** Cho số nguyên dương $n$ và $F(x)=\lfloor x\rfloor/n$ khi $0\le x\le n$, $F(x)=0$ khi $x<0$, $F(x)=1$ khi $x>n$, với $\lfloor x\rfloor$ là số nguyên lớn nhất không vượt quá $x$. Chứng minh $F$ là CDF và tìm PMF tương ứng.

**5.** (a) Chứng minh $p(n)=(1/2)^{n+1}$ với $n=0,1,2,\ldots$ là PMF hợp lệ của một biến ngẫu nhiên rời rạc. (b) Tìm CDF của biến có PMF ở (a).

**6.** Định luật Benford nói rằng trong rất nhiều bộ dữ liệu thực tế, chữ số đầu tiên xấp xỉ một phân phối cụ thể: khoảng 30% khả năng là 1, 18% là 2, và tổng quát

$$P(D=j)=\log_{10}\left(\frac{j+1}{j}\right),\qquad j\in\{1,2,\ldots,9\},$$

với $D$ là chữ số đầu của một phần tử chọn ngẫu nhiên. Kiểm tra đây là PMF hợp lệ bằng tính chất logarit, không dùng máy tính.

**7.** Bob chơi một trò chơi điện tử có bảy cấp độ. Anh bắt đầu ở cấp 1 và có xác suất $p_1$ đạt cấp 2. Nói chung, khi đã đến cấp $j$, anh có xác suất $p_j$ đạt cấp $j+1$, với $1\le j\le6$. Gọi $X$ là cấp cao nhất anh đạt được. Tìm PMF của $X$ theo $p_1,\ldots,p_6$.

**8.** Có 100 phần thưởng, lần lượt trị giá 1, 2, ..., 100 đô la, đặt riêng vào 100 hộp. Bạn lấy được năm phần thưởng bằng cách chọn ngẫu nhiên lần lượt năm hộp không hoàn lại. Tìm PMF của giá trị phần thưởng đắt nhất bạn nhận được, dưới dạng đơn giản theo các hệ số nhị thức.

**9.** Cho $F_1,F_2$ là CDF, $0<p<1$ và $F(x)=pF_1(x)+(1-p)F_2(x)$ với mọi $x$. (a) Chứng minh trực tiếp $F$ thỏa tính chất của CDF hợp lệ (Định lý 3.6.3). Phân phối do $F$ xác định được gọi là *hỗn hợp* của hai phân phối do $F_1,F_2$ xác định. (b) Tung đồng xu có xác suất ra ngửa $p$. Nếu ra ngửa, sinh biến theo $F_1$; nếu ra sấp, sinh biến theo $F_2$. Chứng minh biến thu được có CDF $F$.

**10.** (a) Có phân phối rời rạc nào với miền giá trị $\{1,2,3,\ldots\}$ mà PMF tại $n$ tỉ lệ với $1/n$ không? Gợi ý: xem phần phụ lục toán học để ôn các tính chất chuỗi. (b) Nếu PMF tại $n$ tỉ lệ với $1/n^2$ thì sao?

**11.** Cho $X$ nhận các giá trị khả dĩ $0,1,2,\ldots$ với CDF $F$. Ở một số nước, người ta dùng hàm $G(x)=P(X<x)$ thay CDF để đặc tả phân phối. Hãy chỉ cách tính $G(x)$ với mọi số thực $x$ nếu biết $F$.

**12.** (a) Cho ví dụ hai biến $X,Y$ sao cho $F_X(x)\le F_Y(x)$ với mọi $x$, và bất đẳng thức nghiêm ở ít nhất một $x$. Vẽ phác hai CDF trên cùng hệ trục, rồi vẽ hai PMF trên một hệ trục khác. (b) Có thể tìm hai PMF khác nhau mà PMF thứ nhất không vượt PMF thứ hai tại mọi điểm và nhỏ hơn hẳn ở ít nhất một điểm không? Hãy tìm $X,Y$ thỏa $P(X=x)\le P(Y=x)$ với mọi $x$, nghiêm ở một số $x$, hoặc chứng minh không thể.

**13.** Cho các biến rời rạc $X,Y,Z$ sao cho $X,Y$ có cùng phân phối có điều kiện theo $Z$: với mọi $a,z$, $P(X=a\mid Z=z)=P(Y=a\mid Z=z)$. Chứng minh $X,Y$ cùng phân phối khi không điều kiện hóa.

**14.** Gọi $X$ là số lần Fred mua hàng trên trang web của một công ty trong một khoảng thời gian nhất định. Giả sử

$$P(X=k)=\frac{e^{-\lambda}\lambda^k}{k!},\qquad k=0,1,2,\ldots.$$

Đây là phân phối Poisson với tham số $\lambda$, sẽ được nghiên cứu kỹ ở các chương sau. (a) Tìm $P(X\ge1)$ và $P(X\ge2)$ mà không cộng chuỗi vô hạn. (b) Công ty chỉ biết những người từng mua hàng ít nhất một lần (người mua cần tạo tài khoản; người chưa mua không có trong cơ sở dữ liệu khách hàng). Dữ liệu số lần mua của những người trong cơ sở dữ liệu vì thế tuân theo phân phối có điều kiện khi đã mua ít nhất một lần. Tìm PMF có điều kiện của $X$ khi biết $X\ge1$. Phân phối này được gọi là Poisson cắt cụt.

#### Các phân phối có tên

**15.** Tìm CDF của $X\sim\operatorname{DUnif}(\{1,2,\ldots,n\})$.

**16.** Cho $X\sim\operatorname{DUnif}(C)$ và $B$ là tập con không rỗng của $C$. Tìm phân phối có điều kiện của $X$ khi biết $X\in B$.

**17.** Một hãng hàng không bán vé vượt số ghế vì dự đoán sẽ có người không đến. Máy bay có 100 ghế, 110 người đã đặt chỗ. Mỗi người đến chuyến bay với xác suất $0{,}9$, độc lập. Tìm xác suất có đủ ghế cho tất cả người đến.

**18.** (a) Trong giải World Series bóng chày, hai đội A và B thi đấu cho đến khi một đội thắng bốn trận. Gọi $p$ là xác suất A thắng một trận, giả sử các trận độc lập. Xác suất A thắng cả loạt là bao nhiêu? (b) Giải thích bằng trực giác xem đáp án (a) có phụ thuộc vào việc hai đội luôn đấu đủ bảy trận, đội thắng đa số là đội vô địch, hay dừng ngay khi một đội thắng bốn trận (như thực tế) hay không.

**19.** Trong một giải cờ vua, có $n$ ván diễn ra độc lập. Mỗi ván kết thúc với một người thắng, xác suất $0{,}4$, hoặc hòa, xác suất $0{,}6$. Tìm PMF của số ván hòa và PMF của số người chơi có ván đấu kết thúc hòa.

**20.** Mỗi vé số có xác suất trúng $p$, độc lập với các vé khác. Một người mua ba vé, hy vọng tăng gấp ba cơ hội có ít nhất một vé trúng. (a) Số vé trúng trong ba vé có phân phối gì? (b) Chứng minh bằng hai cách rằng xác suất có ít nhất một vé trúng là $3p-3p^2+p^3$: dùng nguyên lý bao hàm–loại trừ; rồi xét biến cố đối và dùng PMF của một phân phối có tên. (c) Chứng minh cơ hội không tăng đúng gấp ba so với mua một vé, nhưng xấp xỉ gấp ba khi $p$ nhỏ.

**21.** Cho $X\sim\operatorname{Bin}(n,p)$ và $Y\sim\operatorname{Bin}(m,p)$ độc lập với $X$. Chứng minh $X-Y$ không có phân phối Nhị thức.

**22.** Có hai đồng xu, xác suất ra ngửa lần lượt $p_1,p_2$. Chọn ngẫu nhiên đều một đồng xu, rồi tung đồng xu ấy $n\ge2$ lần. Gọi $X$ là số lần ra ngửa. (a) Tìm PMF của $X$. (b) Nếu $p_1=p_2$ thì $X$ có phân phối gì? (c) Giải thích trực giác vì sao $X$ không có phân phối Nhị thức khi $p_1\ne p_2$ (phân phối của nó được gọi là hỗn hợp của hai phân phối Nhị thức). Có thể giả sử $n$ lớn để dùng cách hiểu tần suất của xác suất.

**23.** Có $n$ người đủ điều kiện bỏ phiếu trong một cuộc bầu cử. Muốn bỏ phiếu phải đăng ký. Các quyết định độc lập. Mỗi người đăng ký với xác suất $p_1$; khi đã đăng ký, họ bỏ phiếu với xác suất $p_2$; khi bỏ phiếu, họ chọn ứng cử viên Kodos với xác suất $p_3$. Phân phối của số phiếu cho Kodos là gì? Hãy cho PMF rút gọn hoàn toàn hoặc tên phân phối cùng các tham số.

**24.** Gọi $X$ là số lần ra ngửa trong 10 lần tung đồng xu công bằng. (a) Tìm PMF có điều kiện của $X$ khi biết hai lần tung đầu đều ra ngửa. (b) Tìm PMF có điều kiện của $X$ khi biết có ít nhất hai lần ra ngửa.

**25.** Alice tung đồng xu công bằng $n$ lần, Bob tung một đồng xu công bằng khác $n+1$ lần, tạo hai biến độc lập $X\sim\operatorname{Bin}(n,1/2)$ và $Y\sim\operatorname{Bin}(n+1,1/2)$. (a) Chứng minh $P(X<Y)=P(n-X<n+1-Y)$. (b) Tính $P(X<Y)$. Gợi ý: dùng (a) và việc $X,Y$ nhận giá trị nguyên.

**26.** Nếu $X\sim\operatorname{HGeom}(w,b,n)$ thì $n-X$ có phân phối gì? Chứng minh ngắn.

**27.** Nhắc lại bài toán ghép cặp de Montmort ở Chương 1: trong bộ $n$ lá bài đánh số từ 1 đến $n$, một lá khớp khi số trên lá trùng vị trí của nó trong bộ bài. Gọi $X$ là số lá khớp. $X$ có phân phối Nhị thức không? Có phân phối Siêu bội không?

**28.** Có $n$ quả trứng, mỗi quả nở thành gà con với xác suất $p$, độc lập. Mỗi gà con sống sót với xác suất $r$, độc lập. Tìm phân phối của số gà con nở và của số gà con sống sót. Hãy cho PMF, tên phân phối và tham số nếu có.

**29.** Thực hiện $n$ thí nghiệm độc lập; mỗi thí nghiệm thành công với xác suất $p$ và thất bại với xác suất $q=1-p$. Chứng minh rằng nếu biết số lần thành công thì mọi dãy kết quả hợp lệ đều có khả năng như nhau.

**30.** Một công ty có $n$ nhân viên nữ và $m$ nhân viên nam đang quyết định thăng chức. (a) Công ty quyết định thăng chức $t$ người, $1\le t\le n+m$, bằng cách chọn ngẫu nhiên đều một tập $t$ nhân viên. Số phụ nữ được thăng chức có phân phối gì? (b) Thay vì ấn định số người, công ty quyết định độc lập cho từng nhân viên, thăng chức với xác suất $p$. Tìm phân phối của số phụ nữ được thăng chức, số phụ nữ không được thăng chức và tổng số nhân viên được thăng chức. (c) Theo cách ở (b), tìm phân phối có điều kiện của số phụ nữ được thăng chức nếu biết có đúng $t$ nhân viên được thăng chức.

**31.** Một nhà thống kê nổi tiếng từng mời một phụ nữ uống trà. Bà nói mình phân biệt được sữa được đổ vào tách trước hay sau trà. Nhà thống kê quyết định thử nghiệm. (a) Bà được đưa sáu tách, biết trước ba tách rót sữa trước và ba tách rót trà trước, thứ tự hoàn toàn ngẫu nhiên. Bà nếm rồi đoán ba tách rót sữa trước. Giả sử bà hoàn toàn không phân biệt được hai cách pha. Tìm xác suất bà đoán đúng ít nhất hai trong ba tách. (b) Bà được đưa một tách, xác suất sữa được rót trước là $1/2$. Gọi $p_1$ là xác suất bà đoán đúng khi sữa được rót trước, $p_2$ là xác suất bà đoán đúng khi trà được rót trước. Bà nói tách này rót sữa trước. Tìm *tỉ số xác suất hậu nghiệm* rằng sữa thực sự được rót trước, dựa trên lời đoán ấy.

**32.** Trong lớp lịch sử của Evan, 10 trong 100 thuật ngữ chính sẽ được chọn ngẫu nhiên vào đề thi cuối kỳ; Evan phải chọn bảy trong mười thuật ngữ đó để định nghĩa. Biết trước dạng đề, Evan cân nhắc nên học bao nhiêu thuật ngữ. (a) Nếu Evan học $s$ thuật ngữ, với $s$ nguyên từ 0 đến 100, gọi $X$ là số thuật ngữ xuất hiện trong đề mà cậu đã học. $X$ có phân phối gì? Cho tên và các tham số theo $s$. (b) Dùng R hoặc phần mềm khác tính xác suất Evan biết ít nhất bảy trong mười thuật ngữ xuất hiện trong đề, nếu cậu học $s=75$ thuật ngữ.

**33.** Một cuốn sách có $n$ lỗi in. Hai người soát lỗi Prue và Frida đọc sách độc lập. Prue phát hiện từng lỗi với xác suất $p_1$, bỏ sót với xác suất $q_1=1-p_1$, độc lập giữa các lỗi; Frida tương tự với $p_2$ và $q_2=1-p_2$. Gọi $X_1$ là số lỗi Prue phát hiện, $X_2$ là số lỗi Frida phát hiện, $X$ là số lỗi được ít nhất một trong hai người phát hiện. (a) Tìm phân phối của $X$. (b) Chỉ ở phần này, giả sử $p_1=p_2$. Tìm phân phối có điều kiện của $X_1$ khi biết $X_1+X_2=t$.

**34.** Một trường có $n$ sinh viên; trong đó số sinh viên chuyên ngành Thống kê là $X\sim\operatorname{Bin}(n,p)$. Lấy mẫu ngẫu nhiên đơn giản cỡ $m$: lấy không hoàn lại sao cho mọi tập con cỡ $m$ đồng khả năng. (a) Dùng luật xác suất toàn phần tìm PMF của số sinh viên chuyên ngành Thống kê trong mẫu; nêu miền giá trị khả dĩ. Có thể để đáp án ở dạng tổng (hoặc rút gọn bằng cách viết hệ số nhị thức qua giai thừa và dùng định lý nhị thức). (b) Suy ra phân phối bằng chứng minh theo câu chuyện và rút gọn hoàn toàn. Gợi ý: sinh viên khai báo chuyên ngành trước hay sau khi rút mẫu có khác gì không?

**35.** A và B lần lượt trả lời các câu đố kiến thức, A trả lời đầu tiên. Mỗi lần A trả lời, xác suất đúng là $p_1$; mỗi lần B trả lời, xác suất đúng là $p_2$. (a) Nếu A trả lời $m$ câu, tìm PMF số câu cô trả lời đúng. (b) Nếu A trả lời $m$ lần và B trả lời $n$ lần, tìm PMF tổng số câu họ trả lời đúng; có thể để dưới dạng tổng. Nêu chính xác khi nào tổng này có phân phối Nhị thức. (c) Nếu người đầu tiên trả lời đúng thắng, không giới hạn trước số câu hỏi, tìm xác suất A thắng.

**36.** Trong một cuộc bầu cử có $n$ cử tri, với $n$ chẵn và lớn, có hai ứng viên A thuộc đảng Unite và B thuộc đảng Untie. Gọi $X$ là số người bầu cho A. Giả sử mỗi cử tri chọn độc lập và đều giữa hai người. (a) Tìm biểu thức chính xác cho xác suất hai ứng viên hòa phiếu. (b) Dùng xấp xỉ Stirling

$$n!\approx\sqrt{2\pi n}\left(\frac ne\right)^n$$

để tìm một xấp xỉ đơn giản cho xác suất hòa phiếu, có dạng $1/\sqrt{cn}$; hãy xác định hằng số $c$.

**37.** Một thông điệp gồm $n$ bit $x_1,\ldots,x_n$ được gửi qua kênh nhiễu. Mỗi bit có thể bị lỗi, biến 0 thành 1 hoặc ngược lại, độc lập giữa các bit; xác suất một bit lỗi là $p$, với $0<p<1/2$. Gọi $y_1,\ldots,y_n$ là thông điệp nhận được: $y_i=x_i$ nếu bit đó không lỗi, $y_i=1-x_i$ nếu lỗi.

Để phát hiện lỗi, bit thứ $n$ dùng kiểm tra chẵn lẻ: $x_n=0$ nếu $x_1+\cdots+x_{n-1}$ chẵn, bằng 1 nếu tổng ấy lẻ. Người nhận kiểm tra $y_n$ có cùng tính chẵn lẻ với $y_1+\cdots+y_{n-1}$ không. Nếu sai, họ biết có ít nhất một lỗi; nếu đúng, họ cho rằng không có lỗi.

(a) Với $n=5,p=0{,}1$, xác suất thông điệp nhận có lỗi nhưng không phát hiện được là bao nhiêu? (b) Viết biểu thức dạng tổng cho xác suất ấy với $n,p$ tổng quát. (c) Tìm biểu thức rút gọn, không chứa tổng nhiều hạng. Gợi ý: đặt

$$a=\sum_{\substack{k\text{ chẵn}\\k\ge0}}\binom nk p^k(1-p)^{n-k},
\qquad
b=\sum_{\substack{k\text{ lẻ}\\k\ge1}}\binom nk p^k(1-p)^{n-k}.$$

Định lý nhị thức cho phép tìm $a+b$ và $a-b$, rồi suy ra $a,b$.

#### Tính độc lập của biến ngẫu nhiên

**38.** (a) Cho ví dụ hai biến ngẫu nhiên phụ thuộc $X,Y$ sao cho $P(X<Y)=1$. (b) Cho ví dụ hai biến độc lập $X,Y$ cũng thỏa $P(X<Y)=1$.

**39.** Cho ví dụ hai biến rời rạc $X,Y$ trên cùng không gian mẫu, có cùng phân phối với miền giá trị $\{1,2,\ldots,10\}$, nhưng biến cố $X=Y$ không bao giờ xảy ra. Nếu $X,Y$ độc lập thì còn xây dựng được ví dụ như vậy không?

**40.** Giả sử hai biến rời rạc $X,Y$ thỏa $P(X=Y)=1$, tức chúng luôn nhận cùng giá trị. (a) PMF của chúng có giống nhau không? (b) Chúng có thể độc lập không?

**41.** Nếu $X,Y,Z$ là các biến ngẫu nhiên sao cho $X$ độc lập với $Y$, và $Y$ độc lập với $Z$, thì $X$ có nhất thiết độc lập với $Z$ không? Gợi ý: nghĩ tới ví dụ đơn giản và cực đoan.

**42.** Chọn ngẫu nhiên đều một ngày trong tuần; mã hóa thứ Hai là 1, thứ Ba là 2, v.v., tạo biến $X\in\{1,\ldots,7\}$. Gọi $Y$ là ngày kế tiếp, cũng mã hóa từ 1 đến 7. $X,Y$ có cùng phân phối không? $P(X<Y)$ bằng bao nhiêu?

**43.** (a) Có thể có hai biến $X,Y$ cùng phân phối mà $P(X<Y)=p$ với $p$ lần lượt bằng $0{,}9$, $0{,}99$, $0{,}9999999999999$ và 1 không? Với mỗi giá trị, hãy cho ví dụ hoặc chứng minh bất khả thi. Gợi ý: làm câu trước. (b) Xét lại khi giả sử thêm $X,Y$ độc lập. Đáp án có thay đổi không?

**44.** Với hai bit $x,y\in\{0,1\}$, định nghĩa $x\oplus y=0$ nếu $x=y$ và bằng 1 nếu $x\ne y$. Đây là phép XOR, hay cộng theo môđun 2. (a) Cho $X\sim\operatorname{Bern}(p)$, $Y\sim\operatorname{Bern}(1/2)$ độc lập. $X\oplus Y$ có phân phối gì? (b) $X\oplus Y$ có độc lập với $X$ không? Với $Y$ không? Xét cả $p=1/2$ và $p\ne1/2$. (c) Cho $X_1,\ldots,X_n$ i.i.d. $\operatorname{Bern}(1/2)$. Với mỗi tập con không rỗng $J$ của $\{1,\ldots,n\}$, đặt $Y_J=\bigoplus_{j\in J}X_j$. Thứ tự thực hiện không ảnh hưởng kết quả vì XOR giao hoán và kết hợp. Chứng minh $Y_J\sim\operatorname{Bern}(1/2)$ và $2^n-1$ biến $Y_J$ độc lập từng đôi nhưng không độc lập đồng thời. Chẳng hạn, có thể mô phỏng 1.023 lần tung xu công bằng độc lập từng đôi bằng chỉ 10 lần tung độc lập. Gợi ý: áp dụng các phần trước với $p=1/2$. Với hai tập $J,K$ khác nhau và không rỗng, tách các $X_i$ thành ba nhóm: chỉ số thuộc $J\cap K$, thuộc $J\setminus K$, và thuộc $K\setminus J$; XOR trong từng nhóm lần lượt là $A,B,C$. Khi đó $Y_J=A\oplus B$, $Y_K=A\oplus C$. Ba nhóm độc lập vì dùng các $X_i$ rời nhau; nhiều nhất một nhóm có thể rỗng. Nếu $J\cap K=\varnothing$ thì $Y_J=B,Y_K=C$; nếu không, tính $P(Y_J=y,Y_K=z)$ bằng cách điều kiện hóa theo $A=1$ hay $A=0$.

#### Bài tập tổng hợp

**45.** Một phương pháp điều trị mới được thử để xem có tốt hơn phương pháp chuẩn không. Cách điều trị hiện tại hiệu quả ở 50% bệnh nhân. Ban đầu người ta tin với xác suất $2/3$ rằng cách mới hiệu quả ở 60% bệnh nhân, và với xác suất $1/3$ rằng nó hiệu quả ở 50%. Trong nghiên cứu thử nghiệm trên 20 bệnh nhân chọn ngẫu nhiên, cách mới hiệu quả với 15 người. (a) Dựa trên thông tin này, xác suất cách mới tốt hơn cách chuẩn là bao nhiêu? (b) Sau đó nghiên cứu thứ hai áp dụng cách mới cho 20 bệnh nhân mới. Biết kết quả nghiên cứu thứ nhất, tìm PMF của số bệnh nhân mới mà cách điều trị có hiệu quả. Có thể viết đáp án theo $p$, với $p$ là đáp án (a).

**46.** Thực hiện các phép thử Bernoulli độc lập, mỗi phép thử thành công với xác suất $1/2$. Một câu hỏi quan trọng là nên làm bao nhiêu phép thử. Trong thống kê đã có nhiều tranh luận về cách phân tích thí nghiệm khi số phép thử phụ thuộc dữ liệu đã thu. Chẳng hạn, nếu theo quy tắc “tiếp tục đến khi số thất bại lớn hơn hai lần số thành công rồi dừng”, tỉ lệ thất bại/thành công tại lúc dừng sẽ lớn hơn $2:1$, thay vì tỉ lệ lý thuyết thật $1:1$; kết luận ngây thơ từ đó có thể rất sai lệch. Tuy nhiên, trạng thái số thất bại lớn hơn gấp đôi số thành công có thể không bao giờ xảy ra. Bài này tính xác suất nó xảy ra.

(a) Hai người A và B cá cược liên tiếp; mỗi người có xác suất thắng mỗi lần là $1/2$. A được 2 đô la mỗi khi thắng và mất 1 đô la khi thua, một trò rất có lợi cho A. Họ được phép vay tiền nên tiếp tục mãi. Gọi $p_k$ là xác suất A, bắt đầu với $k$ đô la, có lúc chạm mốc 0, với mọi $k\ge0$. Giải thích liên hệ với bài toán ban đầu và cách dùng $p_k$ để giải nó. (b) Tìm $p_k$. Gợi ý: như bài toán người đánh bạc phá sản, lập và giải phương trình sai phân. Ta có $p_k\to0$ khi $k\to\infty$; không cần chứng minh, nhưng điều này hợp lý vì trò chơi có lợi cho A. Một chứng minh hình thức có thể dùng luật số lớn ở Chương 10. Đáp án có thể viết đẹp bằng tỉ số vàng. (c) Tìm xác suất từng có số thất bại lớn hơn gấp đôi số thành công trong dãy phép thử $\operatorname{Bern}(1/2)$ ban đầu.

**47.** Một máy photocopy tạo $n$ trang mỗi ngày. Máy có hai khay giấy; mỗi trang được lấy ngẫu nhiên và độc lập từ một trong hai khay. Đầu ngày mỗi khay được nạp $m$ tờ. (a) Gọi $\operatorname{pbinom}(x,n,p)$ là CDF của $\operatorname{Bin}(n,p)$ tại $x$. Viết biểu thức đơn giản theo hàm này cho xác suất cả hai khay đủ giấy trong một ngày, ở trường hợp xác suất nằm nghiêm giữa 0 và 1. Nêu các giá trị $m$ khiến xác suất bằng 0 hoặc 1. Gợi ý: chú ý bất đẳng thức nghiêm hay không vì Nhị thức rời rạc. (b) Dùng máy tính tìm $m$ nhỏ nhất để xác suất cả hai khay đủ giấy ít nhất 95%, với $n=10,100,1000,10000$. Nếu dùng R, có thể định nghĩa hàm $g(m,n)$ là đáp án (a); xét vectơ $g(1:100,100)$, dùng hàm <code>which(v>0.95)</code> tìm chỉ số các phần tử vượt $0{,}95$ và <code>min(w)</code> tìm phần tử nhỏ nhất của vectơ.

*(Trang PDF 154 không có văn bản.)*

## Chương 4. Kỳ vọng

### 4.1 Định nghĩa kỳ vọng

Ở chương trước, ta đã giới thiệu phân phối của biến ngẫu nhiên; nó cho đầy đủ thông tin về xác suất biến rơi vào một tập bất kỳ. Chẳng hạn, có thể nói biến vượt 1.000, bằng 5, hay nằm trong khoảng $[0,7]$ với xác suất bao nhiêu. Nhưng việc xử lý nhiều xác suất có thể cồng kềnh, nên ta thường muốn một con số tóm tắt giá trị “trung bình” của biến.

“Trung bình” có nhiều nghĩa, nhưng thông dụng nhất là *trung bình* của biến ngẫu nhiên, còn gọi là *giá trị kỳ vọng*. Ngoài ra, thống kê thường nghiên cứu sự biến thiên của thế giới, nên cần biết phân phối “phân tán” đến mức nào; điều này sẽ được diễn đạt bằng *phương sai* và *độ lệch chuẩn*. Hai đại lượng ấy được định nghĩa qua giá trị kỳ vọng, nên kỳ vọng hữu ích vượt xa việc chỉ tính trung bình.

Với dãy số $x_1,\ldots,x_n$, cách tính trung bình quen thuộc là cộng chúng rồi chia $n$. Đây là *trung bình cộng*:

$$\bar x=\frac1n\sum_{j=1}^n x_j.$$

Tổng quát hơn, *trung bình có trọng số* của dãy là

$$\operatorname{weighted\mbox{-}mean}(x)=\sum_{j=1}^n x_jp_j,$$

trong đó các trọng số $p_1,\ldots,p_n$ không âm, được ấn định trước và có tổng bằng 1. Trung bình không trọng số $\bar x$ là trường hợp $p_j=1/n$ với mọi $j$.

Định nghĩa kỳ vọng cho biến rời rạc lấy cảm hứng từ trung bình có trọng số, với trọng số chính là xác suất.

**Định nghĩa 4.1.1 (Kỳ vọng của biến ngẫu nhiên rời rạc).** Giá trị kỳ vọng (còn gọi là kỳ vọng hay trung bình) của biến rời rạc $X$ có các giá trị khả dĩ phân biệt $x_1,x_2,\ldots$ được định nghĩa là

$$E(X)=\sum_{j=1}^{\infty}x_jP(X=x_j).$$

Nếu miền giá trị khả dĩ hữu hạn, ta dùng tổng hữu hạn. Cũng có thể viết

$$E(X)=\sum_x xP(X=x),$$

trong đó tổng lấy theo miền giá trị khả dĩ của $X$; nếu $x$ nằm ngoài miền ấy thì $xP(X=x)=0$. Kỳ vọng không xác định nếu $\sum_{j=1}^{\infty}|x_j|P(X=x_j)$ phân kỳ, vì khi đó chuỗi định nghĩa $E(X)$ phân kỳ hoặc giá trị phụ thuộc thứ tự liệt kê các $x_j$.

Nói bằng lời, kỳ vọng là trung bình có trọng số của các giá trị $X$ có thể nhận, với trọng số là xác suất tương ứng. Hãy kiểm tra qua hai ví dụ đơn giản.

1. Nếu $X$ là kết quả gieo một xúc xắc công bằng sáu mặt, các giá trị $1,\ldots,6$ đồng khả năng. Theo trực giác, trung bình là tổng sáu giá trị chia sáu. Đúng vậy:

   $$E(X)=\frac16(1+2+\cdots+6)=3{,}5.$$

   Nhưng $X$ không bao giờ bằng trung bình của nó. Tương tự, số con trung bình trên mỗi hộ gia đình ở một nước có thể là $1{,}8$, không có nghĩa một gia đình điển hình có $1{,}8$ đứa con.

2. Nếu $X\sim\operatorname{Bern}(p)$ và $q=1-p$ thì $E(X)=1p+0q=p$. Giá trị này nằm giữa 0 và 1 tùy khả năng của hai kết quả. Hình 4.1 minh họa trường hợp $p<1/2$ bằng hai viên sỏi cân trên đòn bẩy. Điểm tựa phải đặt tại $p$, tức trọng tâm theo vật lý.

   Theo cách hiểu tần suất, xét nhiều phép thử Bernoulli độc lập có xác suất thành công $p$. Ghi 1 cho thành công và 0 cho thất bại; về lâu dài, tỉ lệ số 1 rất gần $p$. Trung bình của dãy 0 và 1 chính là tỉ lệ số 1.

Kỳ vọng $E(X)$ chỉ phụ thuộc vào phân phối của $X$. Điều này suy ra ngay từ định nghĩa, nhưng rất quan trọng.

*Hình 4.1 (trang PDF 157).* Trọng tâm của hai viên sỏi minh họa $E(X)=p$ khi $X\sim\operatorname{Bern}(p)$; $q,p$ là khối lượng của chúng.

**Mệnh đề 4.1.2.** Nếu hai biến ngẫu nhiên rời rạc $X,Y$ cùng phân phối thì $E(X)=E(Y)$, miễn là một trong hai vế tồn tại.

**Chứng minh.** Để tính $E(X)$ theo định nghĩa, chỉ cần biết PMF của $X$. □

Chiều ngược lại sai: kỳ vọng chỉ tóm tắt phân phối bằng một số, không đủ xác định toàn bộ phân phối. Nó đo vị trí “tâm”, nhưng không cho biết phân phối trải rộng đến đâu hay xác suất biến dương là bao nhiêu. Hình 4.2 cho hai PMF khác nhau nhưng cùng điểm cân bằng, tức cùng kỳ vọng bằng 2.

*Hình 4.2.* Kỳ vọng không quyết định phân phối: các PMF khác nhau có thể cùng điểm cân bằng.

**Lưu ý 4.1.3 (Thay biến ngẫu nhiên bằng kỳ vọng).** Với biến rời rạc $X$, $E(X)$ là một số nếu tồn tại. Một lỗi phổ biến là tự ý thay $X$ bằng $E(X)$. Điều đó sai cả về toán học ($X$ là hàm, $E(X)$ là hằng số) lẫn thống kê (bỏ qua sự biến thiên của $X$), trừ trường hợp suy biến $X$ là hằng số.

**Ký hiệu 4.1.4.** Ta thường viết tắt $E(X)$ thành $EX$ và $E(X^2)$ thành $EX^2$. Vậy $EX^2$ là kỳ vọng của biến $X^2$, không phải bình phương của số $EX$. Nói chung, trừ khi dấu ngoặc chỉ rõ khác đi, phép lấy kỳ vọng thực hiện sau cùng. Chẳng hạn $E(X-3)^2$ được hiểu là $E((X-3)^2)$, chứ không phải $(E(X-3))^2$. Thứ tự phép tính này rất quan trọng.

### 4.2 Tính tuyến tính của kỳ vọng

Tính chất quan trọng nhất của kỳ vọng là tính tuyến tính: kỳ vọng của tổng bằng tổng các kỳ vọng.

**Định lý 4.2.1 (Tính tuyến tính của kỳ vọng).** Với mọi biến ngẫu nhiên $X,Y$ và hằng số $c$,

$$E(X+Y)=E(X)+E(Y),\qquad E(cX)=cE(X).$$

Đẳng thức thứ hai cho phép đưa hằng số ra ngoài kỳ vọng; điều này vừa hợp trực giác vừa dễ kiểm tra từ định nghĩa. Đẳng thức thứ nhất cũng có vẻ hợp lý khi $X,Y$ độc lập. Điều có thể gây ngạc nhiên là nó vẫn đúng khi chúng *phụ thuộc*. Xét trường hợp cực đoan $X=Y$ luôn luôn: khi đó $X+Y=2X$, và hai vế của đẳng thức đều bằng $2E(X)$.

Tính tuyến tính đúng với mọi biến ngẫu nhiên, không riêng biến rời rạc, nhưng chương này chỉ chứng minh cho trường hợp rời rạc. Trước khi chứng minh, hãy nhắc lại cách tính trung bình. Với dãy $(1,1,1,1,1,3,3,5)$, tính trực tiếp:

$$\frac18(1+1+1+1+1+3+3+5)=2.$$

Hoặc gom các giá trị bằng nhau:

$$\frac58\cdot1+\frac28\cdot3+\frac18\cdot5=2.$$

Nhận xét rằng trung bình có thể tính bằng cách chưa gom hoặc đã gom nhóm là đủ để chứng minh tính tuyến tính. Biến $X$ gán một số cho mỗi kết quả $s$ trong không gian mẫu và có thể gán cùng một số cho nhiều kết quả. Trong định nghĩa kỳ vọng, ta gom các kết quả ấy thành một “viên sỏi lớn” có trọng lượng $P(X=x)$ bằng tổng trọng lượng các viên thành phần. Hình 4.3 minh họa khi $X$ nhận các giá trị $\{0,1,2\}$. Vậy định nghĩa kỳ vọng tương ứng với cách tính trung bình đã gom nhóm.

*Hình 4.3 (trang PDF 159).* Bên trái, $X$ gán số cho từng viên sỏi trong không gian mẫu. Bên phải, khi gom theo giá trị $X$, chín viên thành ba viên lớn. Trọng lượng mỗi viên lớn bằng tổng trọng lượng các viên thành phần.

Ưu điểm của định nghĩa này là ta làm việc trực tiếp với phân phối $X$ mà không cần trở lại không gian mẫu. Nhược điểm xuất hiện khi chứng minh định lý như trên: một biến $Y$ khác trên cùng không gian mẫu sẽ tạo cách gom nhóm khác, với trọng lượng $P(Y=y)$ khác, làm việc kết hợp hai tổng $\sum_xxP(X=x)$ và $\sum_yyP(Y=y)$ trở nên khó khăn.

May mắn là có cách tính trung bình tương đương: trung bình có trọng số theo từng viên sỏi riêng lẻ. Nếu $X(s)$ là giá trị $X$ gán cho kết quả $s$, ta có

$$E(X)=\sum_s X(s)P(\{s\}),$$

với $P(\{s\})$ là trọng lượng của viên sỏi $s$. Đây là cách tính chưa gom nhóm. Ta dùng cùng các trọng số $P(\{s\})$ cho mọi biến trên cùng không gian mẫu. Do đó, nếu $Y$ là biến khác,

$$E(Y)=\sum_s Y(s)P(\{s\}),$$

và có thể kết hợp:

$$E(X)+E(Y)
=\sum_sX(s)P(\{s\})+\sum_sY(s)P(\{s\})
=\sum_s(X+Y)(s)P(\{s\})=E(X+Y).$$

Một trực giác khác về tính tuyến tính đến từ mô phỏng. Nếu mô phỏng rất nhiều lần từ phân phối của $X$, biểu đồ tần suất kết quả sẽ rất giống PMF thật. Trung bình cộng các giá trị mô phỏng sẽ rất gần $E(X)$. Luật số lớn, một định lý quan trọng ở Chương 10, mô tả chính xác sự hội tụ này.

Giả sử $X,Y$ tóm tắt một thí nghiệm. Ta thực hiện thí nghiệm $n$ lần với $n$ rất lớn và ghi giá trị $X,Y$ ở từng lần. Mỗi lần cho một giá trị $X$, một giá trị $Y$ và tổng $X+Y$. Trong Hình 4.4, mỗi hàng là một lần thử; ba cột lần lượt ghi $X,Y,X+Y$.

*Hình 4.4 (trang PDF 160).* Minh họa tính tuyến tính của kỳ vọng. Cộng cột cuối tương đương cộng riêng hai cột đầu rồi cộng hai tổng. Vì vậy trung bình cột cuối bằng tổng trung bình hai cột đầu.

Có hai cách tính tổng cột cuối: cộng trực tiếp các số trong cột ấy, hoặc cộng riêng các số trong cột thứ nhất và thứ hai rồi cộng hai tổng. Chia tất cả cho $n$, ta thấy hai quy trình sau tương đương:

- Tính trung bình cộng các số ở cột cuối. Theo luật số lớn, kết quả rất gần $E(X+Y)$.
- Tính trung bình cộng mỗi cột đầu, rồi cộng hai trung bình. Theo luật số lớn, kết quả rất gần $E(X)+E(Y)$.

Vậy tính tuyến tính của kỳ vọng xuất phát từ một tính chất số học đơn giản: ta chỉ đổi thứ tự cộng các số. Lập luận không dùng tính độc lập của $X,Y$. Thực ra ở Hình 4.4, $X,Y$ có vẻ phụ thuộc: $Y$ thường lớn khi $X$ lớn và nhỏ khi $X$ nhỏ (theo thuật ngữ Chương 7, chúng *tương quan dương*). Sự phụ thuộc không ảnh hưởng ở đây: xáo trộn các giá trị được mô phỏng của $Y$ có thể thay đổi hoàn toàn quan hệ phụ thuộc giữa $X,Y$ nhưng không đổi tổng cột.

Tính tuyến tính rất hữu ích khi tính kỳ vọng, thường giúp ta không phải dùng trực tiếp định nghĩa. Hãy dùng nó tìm kỳ vọng của phân phối Nhị thức và Siêu bội.

**Ví dụ 4.2.2 (Kỳ vọng Nhị thức, trang PDF 161).** Với $X\sim\operatorname{Bin}(n,p)$, ta tìm $E(X)$ theo hai cách. Đặt $q=1-p$. Theo định nghĩa,

$$E(X)=\sum_{k=0}^{n}kP(X=k)
=\sum_{k=0}^{n}k\binom nk p^kq^{n-k}.$$

Từ Ví dụ 1.5.2, $k\binom nk=n\binom{n-1}{k-1}$. Do đó

$$\begin{aligned}
E(X)
&=n\sum_{k=1}^{n}\binom{n-1}{k-1}p^kq^{n-k}\\
&=np\sum_{j=0}^{n-1}\binom{n-1}{j}p^jq^{n-1-j}
=np.
\end{aligned}$$

Tổng ở dòng áp chót bằng 1 vì là tổng PMF $\operatorname{Bin}(n-1,p)$, hoặc theo định lý nhị thức. Vậy $E(X)=np$.

Chứng minh này đòi hỏi nhớ đồng nhất thức tổ hợp và biến đổi hệ số nhị thức. Tính tuyến tính cho con đường ngắn hơn nhiều. Viết $X=I_1+\cdots+I_n$ với các $I_j$ độc lập, cùng phân phối $\operatorname{Bern}(p)$ và $E(I_j)=p$. Khi đó

$$E(X)=E(I_1)+\cdots+E(I_n)=np.\quad\Diamond$$

**Ví dụ 4.2.3 (Kỳ vọng Siêu bội).** Cho $X\sim\operatorname{HGeom}(w,b,n)$ là số bóng trắng trong mẫu $n$ bóng rút không hoàn lại từ bình có $w$ bóng trắng và $b$ bóng đen. Như với Nhị thức, viết $X=I_1+\cdots+I_n$, trong đó $I_j=1$ nếu bóng rút ở lượt $j$ màu trắng, bằng 0 nếu không. Theo đối xứng, $I_j\sim\operatorname{Bern}(p)$ với $p=w/(w+b)$: nếu chưa biết các lượt khác, bóng thứ $j$ đồng khả năng là bất cứ bóng nào.

Khác trường hợp Nhị thức, các $I_j$ không độc lập vì rút không hoàn lại: biết một bóng trong mẫu màu trắng sẽ làm giảm khả năng một bóng khác cũng màu trắng. Nhưng tính tuyến tính vẫn đúng với biến phụ thuộc, nên

$$E(X)=\frac{nw}{w+b}.\quad\Diamond$$

Một ứng dụng khác của tính tuyến tính là chứng minh nhanh nhận xét trực giác “biến lớn hơn có kỳ vọng lớn hơn”.

**Mệnh đề 4.2.4 (Tính đơn điệu của kỳ vọng).** Cho $X,Y$ là các biến ngẫu nhiên thỏa $X\ge Y$ với xác suất 1. Khi đó $E(X)\ge E(Y)$; đẳng thức xảy ra khi và chỉ khi $X=Y$ với xác suất 1.

**Chứng minh.** Mệnh đề đúng với mọi biến ngẫu nhiên, nhưng ta chỉ chứng minh cho biến rời rạc vì chương này tập trung vào trường hợp đó. Biến $Z=X-Y$ không âm với xác suất 1, nên $E(Z)\ge0$ vì nó là tổng các số hạng không âm. Theo tính tuyến tính,

$$E(X)-E(Y)=E(X-Y)\ge0.$$

Nếu $E(X)=E(Y)$ thì $E(Z)=0$, kéo theo $P(X=Y)=P(Z=0)=1$: chỉ cần một số hạng dương trong tổng định nghĩa $E(Z)$ là cả tổng dương. □

### 4.3 Phân phối Hình học và Nhị thức âm

Ta giới thiệu hai phân phối rời rạc nổi tiếng nữa, Hình học và Nhị thức âm, rồi tính kỳ vọng của chúng.

**Câu chuyện 4.3.1 (Phân phối Hình học).** Thực hiện các phép thử Bernoulli độc lập, cùng xác suất thành công $p\in(0,1)$, cho đến khi có lần thành công đầu tiên. Gọi $X$ là số lần thất bại trước lần thành công ấy. Khi đó $X$ có phân phối *Hình học* với tham số $p$, ký hiệu $X\sim\operatorname{Geom}(p)$. ◇

Ví dụ, tung đồng xu công bằng đến lần đầu ra ngửa; số lần sấp trước đó có phân phối $\operatorname{Geom}(1/2)$. Để suy ra PMF, hình dung dãy phép thử là một chuỗi số 0 (thất bại) kết thúc bằng 1 (thành công). Mỗi số 0 có xác suất $q=1-p$, số 1 cuối có xác suất $p$, nên xác suất đúng $k$ lần thất bại rồi thành công là $q^kp$.

**Định lý 4.3.2 (PMF Hình học).** Nếu $X\sim\operatorname{Geom}(p)$ thì

$$P(X=k)=q^kp,\qquad k=0,1,2,\ldots,\quad q=1-p.$$

Đây là PMF hợp lệ vì

$$\sum_{k=0}^{\infty}q^kp
=p\sum_{k=0}^{\infty}q^k
=\frac p{1-q}=1.$$

Giống như định lý nhị thức chứng minh PMF Nhị thức hợp lệ, chuỗi hình học chứng minh PMF Hình học hợp lệ. Hình 4.5 vẽ PMF và CDF của $\operatorname{Geom}(0{,}5)$ từ $k=0$ đến 6. Các PMF Hình học đều có dạng tương tự; $p$ càng lớn, PMF giảm về 0 càng nhanh.

*Hình 4.5 (trang PDF 163).* PMF và CDF của $\operatorname{Geom}(0{,}5)$.

**Lưu ý 4.3.3 (Quy ước về phân phối Hình học).** Có nhiều quy ước: một số tài liệu định nghĩa biến Hình học là tổng số phép thử, *kể cả* lần thành công. Trong sách này, Hình học *không tính* lần thành công; phân phối *Lần thành công đầu tiên* thì có tính.

**Định nghĩa 4.3.4 (Phân phối Lần thành công đầu tiên).** Trong dãy phép thử Bernoulli độc lập có xác suất thành công $p$, gọi $Y$ là tổng số phép thử cho đến lần thành công đầu tiên, kể cả lần ấy. Khi đó $Y$ có phân phối Lần thành công đầu tiên với tham số $p$, ký hiệu $Y\sim\operatorname{FS}(p)$.

Dễ chuyển đổi giữa hai phân phối nhưng phải chú ý quy ước. Nếu $Y\sim\operatorname{FS}(p)$ thì $Y-1\sim\operatorname{Geom}(p)$, và $P(Y=k)=P(Y-1=k-1)$. Ngược lại, nếu $X\sim\operatorname{Geom}(p)$ thì $X+1\sim\operatorname{FS}(p)$.

**Ví dụ 4.3.5 (Kỳ vọng Hình học).** Với $X\sim\operatorname{Geom}(p)$ và $q=1-p$,

$$E(X)=\sum_{k=0}^{\infty}kq^kp.$$

Tổng này không hẳn là chuỗi hình học vì mỗi số hạng có thêm $k$. Nhưng $kq^{k-1}$ là đạo hàm của $q^k$ theo $q$, nên bắt đầu từ

$$\sum_{k=0}^{\infty}q^k=\frac1{1-q}.$$

Chuỗi hội tụ vì $0<q<1$. Lấy đạo hàm hai vế theo $q$:

$$\sum_{k=0}^{\infty}kq^{k-1}=\frac1{(1-q)^2}.$$

Nhân hai vế với $pq$ để thu tổng cần tìm:

$$E(X)=\sum_{k=0}^{\infty}kq^kp
=\frac{pq}{(1-q)^2}
=\frac qp.$$

Ở Ví dụ 9.1.8 thuộc Chương 9, ta sẽ có chứng minh bằng câu chuyện dựa trên phân tích bước đầu tiên: điều kiện hóa theo kết quả phép thử thứ nhất. Nếu thành công ngay thì $X=0$; nếu thất bại, ta mất một phép thử rồi trở về đúng trạng thái ban đầu. ◇

**Ví dụ 4.3.6 (Kỳ vọng Lần thành công đầu tiên).** Viết $Y\sim\operatorname{FS}(p)$ thành $Y=X+1$ với $X\sim\operatorname{Geom}(p)$. Khi đó

$$E(Y)=E(X+1)=\frac qp+1=\frac1p.\quad\Diamond$$

Phân phối Nhị thức âm khái quát phân phối Hình học: thay vì đợi một lần thành công, ta đợi một số $r$ lần thành công được ấn định trước.

**Câu chuyện 4.3.7 (Phân phối Nhị thức âm).** Trong dãy phép thử Bernoulli độc lập với xác suất thành công $p$, nếu $X$ là số lần thất bại trước lần thành công thứ $r$ thì $X$ có phân phối *Nhị thức âm* với các tham số $r,p$, ký hiệu $X\sim\operatorname{NBin}(r,p)$. ◇

Cả Nhị thức lẫn Nhị thức âm đều dựa trên các phép thử Bernoulli độc lập, nhưng khác quy tắc dừng và đại lượng đếm: Nhị thức đếm số thành công trong một số phép thử cố định; Nhị thức âm đếm số thất bại trước khi đạt một số lần thành công cố định. Vì vậy, cách suy ra PMF Nhị thức âm cũng giống phần nào cách suy ra PMF Nhị thức.

**Định lý 4.3.8 (PMF Nhị thức âm).** Nếu $X\sim\operatorname{NBin}(r,p)$ thì

$$P(X=n)=\binom{n+r-1}{r-1}p^rq^n,\qquad n=0,1,2,\ldots,\quad q=1-p.$$

**Chứng minh.** Hình dung chuỗi số 0 và 1, trong đó 1 biểu thị thành công. Mỗi chuỗi cụ thể gồm $n$ số 0 và $r$ số 1 có xác suất $p^rq^n$. Vì dừng ngay khi thành công thứ $r$ xảy ra, chuỗi phải kết thúc bằng 1. Trong $n+r-1$ vị trí còn lại, chọn $r-1$ chỗ cho các số 1 trước đó. Vậy xác suất có đúng $n$ thất bại trước thành công thứ $r$ là công thức trên. □

Giống như biến Nhị thức có thể biểu diễn thành tổng các biến Bernoulli i.i.d., biến Nhị thức âm có thể biểu diễn thành tổng các biến Hình học i.i.d.

**Định lý 4.3.9.** Cho $X\sim\operatorname{NBin}(r,p)$ là số lần thất bại trước thành công thứ $r$ trong dãy phép thử Bernoulli độc lập. Có thể viết $X=X_1+\cdots+X_r$, trong đó các $X_i$ i.i.d. $\operatorname{Geom}(p)$.

**Chứng minh.** Đặt $X_1$ là số thất bại trước thành công đầu tiên, $X_2$ là số thất bại giữa thành công thứ nhất và thứ hai; tổng quát, $X_i$ là số thất bại giữa thành công thứ $i-1$ và thứ $i$. Theo câu chuyện Hình học, $X_1\sim\operatorname{Geom}(p)$. Sau thành công đầu tiên, số thất bại bổ sung trước thành công tiếp theo vẫn có phân phối Hình học; các $X_i$ khác cũng vậy. Chúng độc lập vì các phép thử đều độc lập. Cộng chúng lại ta được tổng số thất bại trước thành công thứ $r$, tức $X$. □

Theo tính tuyến tính, ta suy ra kỳ vọng Nhị thức âm mà không cần phép tính mới.

**Ví dụ 4.3.10 (Kỳ vọng Nhị thức âm).** Nếu $X\sim\operatorname{NBin}(r,p)$ thì $X=X_1+\cdots+X_r$ với các $X_i$ i.i.d. $\operatorname{Geom}(p)$, nên

$$E(X)=E(X_1)+\cdots+E(X_r)=r\frac qp.\quad\Diamond$$

Ví dụ tiếp theo là bài toán xác suất nổi tiếng, ứng dụng hai phân phối Hình học và Lần thành công đầu tiên. Bài toán thường nói về sưu tập phiếu giảm giá, nhưng ở đây ta dùng đồ chơi.

**Ví dụ 4.3.11 (Người sưu tập phiếu thưởng).** Có $n$ loại đồ chơi; bạn thu thập từng món với mục tiêu có đủ một bộ. Loại đồ chơi nhận được mỗi lần là ngẫu nhiên, như đồ chơi tặng trong hộp ngũ cốc hoặc suất ăn trẻ em. Giả sử mỗi lần nhận một món, nó đồng khả năng thuộc bất kỳ loại nào trong $n$ loại. Cần trung bình bao nhiêu món để có đủ bộ?

**Lời giải.** Gọi $N$ là tổng số món cần nhận; ta muốn tìm $E(N)$. Viết $N=N_1+\cdots+N_n$, trong đó $N_1$ là số món cần để gặp loại mới đầu tiên (luôn bằng 1), $N_2$ là số món *bổ sung* để gặp loại mới thứ hai, v.v. Hình 4.6 minh họa khi có ba loại.

Theo câu chuyện phân phối FS, $N_2\sim\operatorname{FS}((n-1)/n)$: sau khi đã có loại đầu, lần nhận tiếp theo có xác suất $1/n$ trùng loại cũ (thất bại), xác suất $(n-1)/n$ là loại mới (thành công). Tương tự, $N_3\sim\operatorname{FS}((n-2)/n)$. Nói chung,

$$N_j\sim\operatorname{FS}\left(\frac{n-j+1}{n}\right).$$

*Hình 4.6 (trang PDF 167).* Bài toán sưu tập phiếu thưởng với $n=3$. $N_1$ là số món cần để gặp loại mới đầu tiên, $N_2$ là số món thêm để gặp loại mới thứ hai, $N_3$ là số món thêm để gặp loại mới thứ ba. Tổng số món cần để đủ bộ là $N_1+N_2+N_3$.

Theo tính tuyến tính,

$$\begin{aligned}
E(N)
&=E(N_1)+\cdots+E(N_n)\\
&=1+\frac n{n-1}+\frac n{n-2}+\cdots+n\\
&=n\sum_{j=1}^{n}\frac1j.
\end{aligned}$$

Khi $n$ lớn, giá trị này rất gần $n(\log n+0{,}577)$.

Trước khi rời ví dụ, hãy liên hệ với chứng minh Định lý 4.3.9, biểu diễn Nhị thức âm thành tổng các biến Hình học i.i.d. Cả hai bài toán đều đợi một số lần thành công nhất định, và đều xét các khoảng giữa các lần thành công. Có hai khác biệt:

- Trong Định lý 4.3.9, ta không tính bản thân các lần thành công, nên số thất bại giữa hai lần thành công có phân phối Hình học. Trong bài toán sưu tập, ta tính cả món đồ chơi tạo ra loại mới vì cần đếm tổng số món, nên dùng phân phối Lần thành công đầu tiên.
- Trong Định lý 4.3.9, xác suất thành công ở mọi phép thử không đổi, nên tổng số thất bại là tổng các biến Hình học i.i.d. Trong bài toán sưu tập, xác suất gặp loại mới giảm sau mỗi lần gặp loại mới: càng lúc càng khó tìm loại chưa có. Vì vậy các $N_j$ không cùng phân phối, dù chúng độc lập. ◇

**Lưu ý 4.3.12 (Kỳ vọng của hàm phi tuyến).** Kỳ vọng tuyến tính, nhưng nói chung $E(g(X))\ne g(E(X))$ với hàm $g$ tùy ý. Không được tự ý chuyển $E$ qua hàm $g$ khi $g$ không tuyến tính. Ví dụ sau cho hai giá trị khác nhau rất xa.

**Ví dụ 4.3.13 (Nghịch lý St. Petersburg).** Một người giàu có đề nghị chơi trò sau: bạn tung đồng xu công bằng đến lần đầu ra ngửa. Nếu trò kéo dài một lượt, bạn được 2 đô la; hai lượt được 4 đô la; ba lượt được 8 đô la; nói chung $n$ lượt được $2^n$ đô la. Giá trị công bằng của trò chơi, tức khoản tiền thắng kỳ vọng, là bao nhiêu? Bạn sẵn lòng trả bao nhiêu để chơi một lần?

**Lời giải.** Gọi $X$ là tiền thắng, $N$ là số lượt; $X=2^N$. Biến $X$ bằng 2 với xác suất $1/2$, bằng 4 với xác suất $1/4$, bằng 8 với xác suất $1/8$, v.v. Do đó

$$E(X)=\frac12\cdot2+\frac14\cdot4+\frac18\cdot8+\cdots=\infty.$$

Tiền thắng kỳ vọng là vô hạn! Mặt khác, $N$ là số lần tung đến lần đầu ra ngửa, nên $N\sim\operatorname{FS}(1/2)$ và $E(N)=2$. Vậy $E(2^N)=\infty$ trong khi $2^{E(N)}=4$: không được nhầm $E(g(N))$ với $g(E(N))$ khi $g$ phi tuyến.

Đây thường được xem là nghịch lý: dù tiền thắng kỳ vọng vô hạn, phần lớn mọi người không sẵn lòng trả quá nhiều để chơi, kể cả khi đủ sức chịu mất tiền. Một cách giải thích là lượng tiền ngoài đời hữu hạn. Giả sử nếu trò kéo dài hơn 40 lượt, người giàu bỏ trốn và bạn không nhận gì. Vì $2^{40}\approx1{,}1\times10^{12}$, bạn vẫn có cơ hội nhận hơn một nghìn tỷ đô la; hơn nữa trò kéo dài quá 40 lượt cực kỳ hiếm. Dù vậy,

$$E(X)=\sum_{n=1}^{40}\frac1{2^n}2^n
+\sum_{n=41}^{\infty}\frac1{2^n}0=40.$$

Liệu mức giảm lớn này có phải do khả năng người giàu bỏ trốn? Giả sử thay vào đó tiền thắng được giới hạn ở $2^{40}$: nếu trò quá 40 lượt, bạn vẫn nhận số tiền đó. Khi ấy

$$E(X)=\sum_{n=1}^{40}\frac1{2^n}2^n
+\sum_{n=41}^{\infty}\frac1{2^n}2^{40}=40+1=41,$$

chỉ tăng một đô la so với trường hợp trước. Kỳ vọng vô hạn trong nghịch lý do “đuôi” vô hạn gồm những biến cố cực hiếm nhưng có khoản thưởng cực lớn. Cắt đuôi này ở một điểm nào đó, như hợp lý ngoài đời, làm kỳ vọng giảm mạnh. ◇

### 4.4 Biến chỉ báo và cây cầu cơ bản

Mục này bàn kỹ hơn về biến chỉ báo đã gặp ở chương trước. Chúng là công cụ rất hữu ích để tính kỳ vọng. Nhắc lại, biến chỉ báo $I_A$ (hay $I(A)$) bằng 1 nếu biến cố $A$ xảy ra, bằng 0 nếu không. Vậy $I_A$ là biến Bernoulli, với “thành công” nghĩa là $A$ xảy ra.

**Định lý 4.4.1 (Tính chất biến chỉ báo).** Với các biến cố $A,B$:

1. $(I_A)^k=I_A$ với mọi số nguyên dương $k$.
2. $I_{A^c}=1-I_A$.
3. $I_{A\cap B}=I_AI_B$.
4. $I_{A\cup B}=I_A+I_B-I_AI_B$.

**Chứng minh.** Tính chất 1 vì $0^k=0$, $1^k=1$. Tính chất 2 vì $1-I_A$ bằng 1 đúng khi $A$ không xảy ra. Tính chất 3 vì $I_AI_B$ bằng 1 đúng khi cả hai chỉ báo bằng 1. Tính chất 4 suy ra từ

$$I_{A\cup B}
=1-I_{A^c\cap B^c}
=1-I_{A^c}I_{B^c}
=1-(1-I_A)(1-I_B)
=I_A+I_B-I_AI_B.\quad\Box$$

Biến chỉ báo nối xác suất với kỳ vọng; ta gọi đó là *cây cầu cơ bản*.

**Định lý 4.4.2 (Cây cầu cơ bản giữa xác suất và kỳ vọng).** Có tương ứng một đối một giữa biến cố và biến chỉ báo, và xác suất của biến cố $A$ bằng kỳ vọng chỉ báo của nó:

$$P(A)=E(I_A).$$

**Chứng minh.** Mỗi biến cố $A$ cho một chỉ báo $I_A$. Tương ứng là một đối một vì $A$ xác định duy nhất $I_A$, và ngược lại $A=\{s\in S:I_A(s)=1\}$. Do $I_A\sim\operatorname{Bern}(P(A))$, ta có $E(I_A)=P(A)$. □

Cây cầu cơ bản cho phép biểu diễn mọi xác suất thành kỳ vọng. Ví dụ, nó cho chứng minh ngắn của nguyên lý bao hàm–loại trừ và bất đẳng thức Boole, còn gọi là bất đẳng thức Bonferroni.

**Ví dụ 4.4.3 (Boole, Bonferroni và bao hàm–loại trừ).** Với các biến cố $A_1,\ldots,A_n$,

$$I_{A_1\cup\cdots\cup A_n}\le I_{A_1}+\cdots+I_{A_n}.$$

Nếu vế trái bằng 0 thì rõ ràng; nếu bằng 1, ít nhất một số hạng vế phải bằng 1. Lấy kỳ vọng và dùng tính tuyến tính cùng cây cầu cơ bản:

$$P(A_1\cup\cdots\cup A_n)
\le P(A_1)+\cdots+P(A_n).$$

Đây là bất đẳng thức Boole hay Bonferroni. Với hai biến cố, lấy kỳ vọng hai vế của tính chất 4 ở Định lý 4.4.1 cho nguyên lý bao hàm–loại trừ. Với $n$ biến cố, dùng

$$\begin{aligned}
1-I_{A_1\cup\cdots\cup A_n}
&=I_{A_1^c\cap\cdots\cap A_n^c}\\
&=(1-I_{A_1})\cdots(1-I_{A_n})\\
&=1-\sum_i I_{A_i}
+\sum_{i<j}I_{A_i}I_{A_j}
-\cdots+(-1)^nI_{A_1}\cdots I_{A_n}.
\end{aligned}$$

Lấy kỳ vọng hai vế và dùng cây cầu cơ bản, ta được công thức bao hàm–loại trừ. ◇

Ngược lại, cây cầu cơ bản cũng rất hữu ích trong bài toán kỳ vọng. Ta thường có thể viết một biến rời rạc phức tạp, chưa biết phân phối, thành tổng các biến chỉ báo rất đơn giản. Cây cầu cơ bản cho kỳ vọng của từng chỉ báo; tính tuyến tính cho kỳ vọng biến ban đầu. Ta đã dùng chính cách này khi tìm kỳ vọng Nhị thức và Siêu bội.

Nhận ra bài toán phù hợp và định nghĩa chỉ báo cần luyện tập qua nhiều ví dụ. Nếu biến ngẫu nhiên đếm số “đối tượng” nào đó, hãy đặt một chỉ báo cho *mỗi đối tượng có thể được đếm*. Đối tượng đó có thể là người, địa điểm hoặc vật. Ta sẽ gặp cả ba loại.

Trước tiên, trở lại hai bài toán Chương 1: ghép cặp de Montmort và ngày sinh.

**Ví dụ 4.4.4 (Bài toán ghép cặp, trang PDF 170).** Có bộ $n$ lá bài xáo kỹ, đánh số từ 1 đến $n$. Một lá được gọi là khớp nếu vị trí của nó trong bộ bài trùng số trên lá. Gọi $X$ là số lá khớp; tìm $E(X)$.

**Lời giải.** Trước hết thử xem $X$ có thuộc một phân phối có tên đã học không. Nhị thức và Siêu bội là hai ứng viên vì $X$ là số nguyên từ 0 đến $n$. Nhưng cả hai không có miền giá trị phù hợp: $X$ không thể bằng $n-1$, vì nếu $n-1$ lá khớp thì lá cuối cũng buộc khớp. Dù $X$ không thuộc phân phối có tên đã học, kỳ vọng vẫn dễ tính. Viết $X=I_1+\cdots+I_n$, trong đó $I_j$ bằng 1 nếu lá ở vị trí $j$ khớp, bằng 0 nếu không. Mỗi chỉ báo như “giơ tay” khi lá của mình khớp; đếm số tay giơ lên chính là $X$.

Theo cây cầu cơ bản, $E(I_j)=P(\text{lá thứ }j\text{ khớp})=1/n$ với mọi $j$. Theo tính tuyến tính,

$$E(X)=E(I_1)+\cdots+E(I_n)=n\cdot\frac1n=1.$$

Số lá khớp kỳ vọng là 1, bất kể $n$. Dù các $I_j$ phụ thuộc phức tạp khiến $X$ không phải Nhị thức hay Siêu bội, tính tuyến tính vẫn đúng. ◇

**Ví dụ 4.4.5 (Ngày sinh khác nhau và cặp trùng ngày sinh).** Trong nhóm $n$ người, theo những giả thiết thường dùng về ngày sinh, kỳ vọng có bao nhiêu ngày sinh *khác nhau*, tức bao nhiêu ngày trong năm có ít nhất một người sinh? Kỳ vọng có bao nhiêu *cặp người* trùng ngày sinh?

**Lời giải.** Gọi $X$ là số ngày sinh khác nhau, viết $X=I_1+\cdots+I_{365}$, trong đó $I_j=1$ nếu có người sinh vào ngày thứ $j$, bằng 0 nếu không. Đặt một chỉ báo cho mỗi ngày vì $X$ đếm số ngày được “đại diện”. Theo cây cầu cơ bản,

$$E(I_j)=P(\text{có người sinh ngày }j)
=1-P(\text{không ai sinh ngày }j)
=1-\left(\frac{364}{365}\right)^n.$$

Vậy theo tính tuyến tính,

$$E(X)=365\left[1-\left(\frac{364}{365}\right)^n\right].$$

Tiếp theo, gọi $Y$ là số cặp người trùng ngày sinh. Đánh số người từ 1 đến $n$, rồi xếp $\binom n2$ cặp theo một thứ tự cố định. Viết $Y=J_1+\cdots+J_{\binom n2}$, với $J_i$ là chỉ báo cặp thứ $i$ trùng ngày sinh. Mỗi cặp có xác suất trùng $1/365$, nên

$$E(Y)=\frac{\binom n2}{365}.\quad\Diamond$$

Hai ví dụ còn dùng một dạng đối xứng giúp tính toán gọn hơn: trong mỗi tổng chỉ báo, mọi chỉ báo có cùng kỳ vọng. Ở bài ghép cặp, xác suất lá thứ $j$ khớp không phụ thuộc $j$, nên chỉ cần lấy $n$ lần kỳ vọng của chỉ báo đầu. Những dạng đối xứng khác cũng hữu ích. Hai ví dụ sau cho thấy đối xứng từ các hoán vị đồng khả năng kết hợp với tính tuyến tính và cây cầu cơ bản để giải những bài toán có vẻ khó.

**Ví dụ 4.4.6 (Bài toán Putnam).** Một hoán vị $a_1,\ldots,a_n$ của $1,\ldots,n$ có cực đại địa phương tại vị trí $j$ nếu $a_j>a_{j-1}$ và $a_j>a_{j+1}$ với $2\le j\le n-1$; tại $j=1$ thì cần $a_1>a_2$, tại $j=n$ thì cần $a_n>a_{n-1}$. Ví dụ, dãy $4,2,5,3,6,1$ có ba cực đại địa phương ở vị trí 1, 3, 5. Kỳ thi Putnam năm 2006, một cuộc thi toán nổi tiếng rất khó mà điểm trung vị thường bằng 0, hỏi: với $n\ge2$, số cực đại địa phương trung bình của một hoán vị ngẫu nhiên đều trong $n!$ hoán vị là bao nhiêu?

**Lời giải.** Đặt $I_j=1$ nếu vị trí $j$ là cực đại địa phương, bằng 0 nếu không. Ta cần $E(\sum_{j=1}^n I_j)$. Với $1<j<n$, xác suất $a_j$ lớn nhất trong $a_{j-1},a_j,a_{j+1}$ là $1/3$ vì mọi thứ tự đồng khả năng; do đó $E(I_j)=1/3$. Ở hai đầu, mỗi vị trí chỉ có một hàng xóm, nên kỳ vọng mỗi chỉ báo là $1/2$. Bởi tính tuyến tính,

$$E\left(\sum_{j=1}^nI_j\right)
=2\cdot\frac12+(n-2)\cdot\frac13
=\frac{n+1}{3}.\quad\Diamond$$

Ví dụ tiếp theo giới thiệu phân phối Siêu bội âm và hoàn tất bảng bốn mô hình lấy mẫu: có hoàn lại hoặc không, dừng sau số lượt cố định hoặc sau số lần thành công cố định.

| Quy tắc dừng | Có hoàn lại | Không hoàn lại |
|---|---|---|
| Số lượt cố định | Nhị thức | Siêu bội |
| Số thành công cố định | Nhị thức âm | Siêu bội âm |

**Ví dụ 4.4.7 (Siêu bội âm, trang PDF 173).** Bình có $w$ bóng trắng và $b$ bóng đen, được rút ngẫu nhiên từng quả không hoàn lại. Số bóng đen rút trước khi gặp bất kỳ bóng trắng nào có phân phối *Siêu bội âm*. Chẳng hạn, nếu xáo bộ bài rồi chia lần lượt, số lá được chia trước lá át đầu tiên có phân phối Siêu bội âm với $w=4,b=48$. Tính trực tiếp kỳ vọng từ định nghĩa dẫn tới tổng tích rất phức tạp. Nhưng đáp án đơn giản: $b/(w+1)$.

Chứng minh bằng biến chỉ báo. Đánh số các bóng đen từ 1 đến $b$, và đặt $I_j=1$ nếu bóng đen thứ $j$ được rút trước mọi bóng trắng, bằng 0 nếu không. Khi chỉ xét thứ tự rút bóng đen $j$ và các bóng trắng (bỏ qua những bóng khác), mọi thứ tự đồng khả năng. Biến cố $I_j=1$ nghĩa là bóng đen $j$ đứng đầu danh sách này, nên $P(I_j=1)=1/(w+1)$. Bởi tính tuyến tính,

$$E\left(\sum_{j=1}^{b}I_j\right)
=\sum_{j=1}^{b}E(I_j)
=\frac b{w+1}.$$

**Kiểm tra tính hợp lý:** Đáp án tăng theo $b$, giảm theo $w$, và đúng ở hai trường hợp biên $b=0$ (không rút bóng đen nào) và $w=0$ (rút hết bóng đen trước khi gặp bóng trắng vốn không tồn tại). ◇

Liên quan chặt với biến chỉ báo là cách viết khác cho kỳ vọng của biến $X$ nhận giá trị nguyên không âm: thay vì cộng giá trị $X$ nhân PMF, ta cộng các *xác suất đuôi* $P(X>n)$ theo các số nguyên không âm $n$.

**Định lý 4.4.8 (Kỳ vọng qua hàm sống sót).** Cho $X$ là biến ngẫu nhiên nguyên không âm, có CDF $F$. Đặt $G(x)=1-F(x)=P(X>x)$; $G$ được gọi là *hàm sống sót* của $X$. Khi đó

$$E(X)=\sum_{n=0}^{\infty}G(n).$$

Nghĩa là kỳ vọng bằng tổng hàm sống sót, hay tổng các xác suất đuôi.

**Chứng minh.** Để đơn giản, chỉ xét $X$ bị chặn: có số nguyên không âm $b$ sao cho $X\le b$ luôn luôn. Viết $X=I_1+\cdots+I_b$, với $I_k=I_{\{X\ge k\}}$. Chẳng hạn, nếu $X=7$ thì $I_1,\ldots,I_7$ đều bằng 1, các chỉ báo khác bằng 0. Bởi tính tuyến tính, cây cầu cơ bản và $\{X\ge k\}=\{X>k-1\}$,

$$E(X)=\sum_{k=1}^{b}E(I_k)
=\sum_{k=1}^{b}P(X\ge k)
=\sum_{n=0}^{b-1}P(X>n)
=\sum_{n=0}^{\infty}G(n).\quad\Box$$

**Ví dụ 4.4.9 (Tính lại kỳ vọng Hình học).** Nếu $X\sim\operatorname{Geom}(p)$ và $q=1-p$, thì $\{X>n\}$ nghĩa là $n+1$ phép thử đầu đều thất bại. Theo Định lý 4.4.8,

$$E(X)=\sum_{n=0}^{\infty}P(X>n)
=\sum_{n=0}^{\infty}q^{n+1}
=\frac q{1-q}=\frac qp,$$

đúng như kết quả đã biết. ◇

### 4.5 Quy tắc LOTUS

Nghịch lý St. Petersburg cho thấy $E(g(X))$ nói chung khác $g(E(X))$ khi $g$ phi tuyến. Vậy tính đúng $E(g(X))$ thế nào? Vì $g(X)$ cũng là biến ngẫu nhiên, một cách là tìm phân phối của nó rồi dùng định nghĩa kỳ vọng. Điều có thể gây ngạc nhiên là ta tính được trực tiếp từ phân phối của $X$, không cần tìm phân phối $g(X)$ trước. Đó là quy tắc được gọi là *law of the unconscious statistician* (LOTUS, “định luật của nhà thống kê vô thức”).

**Định lý 4.5.1 (LOTUS).** Nếu $X$ là biến rời rạc và $g:\mathbb R\to\mathbb R$ thì

$$E(g(X))=\sum_x g(x)P(X=x),$$

với tổng lấy trên mọi giá trị khả dĩ của $X$.

Chỉ cần biết PMF $P(X=x)$ của $X$ để tính kỳ vọng $g(X)$; không cần biết PMF của $g(X)$. Tên gọi xuất phát từ việc có vẻ ta chỉ cần thay $x$ bằng $g(x)$ trong công thức $E(X)$ một cách máy móc, gần như “vô thức”. Điều ấy thoạt nghe quá thuận tiện, nhưng LOTUS xác nhận nó đúng.

Trước khi chứng minh tổng quát, xét trường hợp đặc biệt. Cho $X$ nhận $0,1,2,\ldots$ với xác suất $p_0,p_1,p_2,\ldots$. Khi ấy $X^3$ nhận $0^3,1^3,2^3,\ldots$ với cùng dãy xác suất, nên

$$E(X)=\sum_{n=0}^{\infty}np_n,\qquad
E(X^3)=\sum_{n=0}^{\infty}n^3p_n.$$

Để chuyển biểu thức $E(X)$ thành $E(X^3)$, chỉ cần thay $n$ trước $p_n$ bằng $n^3$, giữ nguyên $p_n$. Ví dụ này dễ vì $g(x)=x^3$ là hàm một đối một. Nhưng LOTUS đúng rộng hơn nhiều. Ý chính của chứng minh giống tính tuyến tính: có thể tính kỳ vọng theo từng kết quả mẫu $s$ rồi gom những kết quả có cùng $X(s)=x$. Trong nhóm ấy, $g(X(s))$ luôn bằng $g(x)$. Do đó

$$\begin{aligned}
E(g(X))
&=\sum_s g(X(s))P(\{s\})\\
&=\sum_x\sum_{s:X(s)=x}g(x)P(\{s\})\\
&=\sum_xg(x)\sum_{s:X(s)=x}P(\{s\})\\
&=\sum_xg(x)P(X=x).
\end{aligned}$$

Ở bước cuối, tổng các trọng lượng của các kết quả có $X(s)=x$ chính là $P(X=x)$.

### 4.6 Phương sai

Một ứng dụng quan trọng của LOTUS là tính phương sai. Giống kỳ vọng, phương sai tóm tắt phân phối bằng một số. Kỳ vọng cho biết vị trí trọng tâm, còn phương sai cho biết phân phối trải rộng đến đâu.

**Định nghĩa 4.6.1 (Phương sai và độ lệch chuẩn).** Phương sai của biến ngẫu nhiên $X$ là

$$\operatorname{Var}(X)=E\bigl((X-EX)^2\bigr).$$

Căn bậc hai của phương sai là *độ lệch chuẩn* (SD):

$$\operatorname{SD}(X)=\sqrt{\operatorname{Var}(X)}.$$

Khi viết $E(X-EX)^2$, ta muốn nói kỳ vọng của biến $(X-EX)^2$, không phải $(E(X-EX))^2$, vốn bằng 0 theo tính tuyến tính.

Phương sai đo khoảng cách giữa $X$ và trung bình của nó “trung bình” là bao nhiêu, nhưng lấy trung bình *bình phương* khoảng cách. Nếu chỉ lấy độ lệch trung bình $E(X-EX)$ thì luôn bằng 0: các lệch dương và âm triệt tiêu nhau. Bình phương khiến cả hai phía đều góp vào độ biến thiên. Tuy nhiên, phương sai có đơn vị bình phương: nếu $X$ tính bằng đô la thì phương sai tính bằng đô la bình phương. Lấy căn cho độ lệch chuẩn cùng đơn vị với $X$.

Có thể hỏi sao không dùng $E|X-EX|$: đại lượng này tính cả hai hướng lệch và vẫn giữ đơn vị gốc. Nó ít phổ biến hơn vì hàm trị tuyệt đối không khả vi tại 0, nên không có các tính chất thuận tiện như hàm bình phương. Khoảng cách bình phương còn liên hệ với hình học qua công thức khoảng cách và định lý Pythagoras, từ đó có các diễn giải thống kê.

Công thức tương đương $\operatorname{Var}(X)=E(X^2)-(EX)^2$ thường dễ tính hơn, nên được phát biểu riêng.

**Định lý 4.6.2.** Với mọi biến ngẫu nhiên $X$,

$$\operatorname{Var}(X)=E(X^2)-(EX)^2.$$

**Chứng minh.** Đặt $\mu=EX$, khai triển và dùng tính tuyến tính:

$$\operatorname{Var}(X)
=E((X-\mu)^2)
=E(X^2-2\mu X+\mu^2)
=E(X^2)-2\mu EX+\mu^2
=E(X^2)-\mu^2.\quad\Box$$

Phương sai có các tính chất:

- $\operatorname{Var}(X+c)=\operatorname{Var}(X)$ với mọi hằng số $c$: dịch phân phối làm đổi trọng tâm nhưng không đổi độ trải rộng.
- $\operatorname{Var}(cX)=c^2\operatorname{Var}(X)$.
- Nếu $X,Y$ độc lập, $\operatorname{Var}(X+Y)=\operatorname{Var}(X)+\operatorname{Var}(Y)$. Chương 7 sẽ chứng minh và bàn kỹ. Điều này không đúng nói chung khi $X,Y$ phụ thuộc. Chẳng hạn nếu $X=Y$ luôn luôn và $\operatorname{Var}(X)>0$, thì $\operatorname{Var}(X+Y)=4\operatorname{Var}(X)>2\operatorname{Var}(X)=\operatorname{Var}(X)+\operatorname{Var}(Y)$.
- $\operatorname{Var}(X)\ge0$, bằng 0 khi và chỉ khi $P(X=a)=1$ với một hằng số $a$. Chỉ biến ngẫu nhiên hằng (suy biến) có phương sai bằng 0.

Để chứng minh tính chất cuối, phương sai là kỳ vọng của biến không âm $(X-EX)^2$, nên không âm. Nếu $P(X=a)=1$ thì $E(X)=a$, $E(X^2)=a^2$, nên phương sai bằng 0. Ngược lại, nếu phương sai bằng 0 thì $E((X-EX)^2)=0$, buộc $(X-EX)^2=0$ với xác suất 1, tức $X$ bằng trung bình của nó với xác suất 1.

**Lưu ý 4.6.3 (Phương sai không tuyến tính).** Khác kỳ vọng, phương sai không tuyến tính. Hằng số ra ngoài thành bình phương trong $\operatorname{Var}(cX)=c^2\operatorname{Var}(X)$; phương sai của tổng các biến có thể bằng hoặc khác tổng phương sai.

**Ví dụ 4.6.4 (Phương sai Hình học và Nhị thức âm).** Dùng LOTUS tính phương sai Hình học. Với $X\sim\operatorname{Geom}(p)$, ta đã biết $E(X)=q/p$, $q=1-p$. Theo LOTUS,

$$E(X^2)=\sum_{k=0}^{\infty}k^2P(X=k)
=\sum_{k=1}^{\infty}k^2pq^k.$$

Bắt đầu từ chuỗi hình học và lấy đạo hàm theo $q$:

$$\sum_{k=0}^{\infty}q^k=\frac1{1-q},
\qquad
\sum_{k=1}^{\infty}kq^{k-1}=\frac1{(1-q)^2}.$$

Nhân đẳng thức thứ hai với $q$ rồi lấy đạo hàm lần nữa:

$$\sum_{k=1}^{\infty}kq^k=\frac q{(1-q)^2},
\qquad
\sum_{k=1}^{\infty}k^2q^{k-1}
=\frac{1+q}{(1-q)^3}.$$

Suy ra

$$E(X^2)=pq\frac{1+q}{(1-q)^3}
=\frac{q(1+q)}{p^2},$$

và

$$\operatorname{Var}(X)
=E(X^2)-(EX)^2
=\frac{q(1+q)}{p^2}-\left(\frac qp\right)^2
=\frac q{p^2}.$$

Phân phối Lần thành công đầu tiên có cùng phương sai vì cộng hằng số không đổi phương sai. Biến $\operatorname{NBin}(r,p)$ là tổng $r$ biến $\operatorname{Geom}(p)$ i.i.d. theo Định lý 4.3.9; do phương sai cộng được với biến độc lập, phương sai Nhị thức âm là $rq/p^2$. ◇

LOTUS dùng được cho mọi $E(g(X))$, nhưng thường dẫn tới những tổng phức tạp nên nên xem là phương án cuối. Với phương sai, biến chỉ báo đôi khi giúp tránh LOTUS.

**Ví dụ 4.6.5 (Phương sai Nhị thức).** Tìm phương sai $X\sim\operatorname{Bin}(n,p)$ bằng chỉ báo. Viết $X=I_1+\cdots+I_n$, với $I_j$ báo thành công ở phép thử thứ $j$. Vì $I_j^2=I_j$ và $E(I_j)=p$,

$$\operatorname{Var}(I_j)
=E(I_j^2)-(E(I_j))^2
=p-p^2=p(1-p).$$

Các $I_j$ độc lập, nên cộng phương sai:

$$\operatorname{Var}(X)=\sum_{j=1}^n\operatorname{Var}(I_j)=np(1-p).$$

Một cách khác là tìm $E(X^2)$ qua $E\binom X2$. Nghe có vẻ phức tạp hơn, nhưng $\binom X2$ đếm số *cặp* phép thử đều thành công. Tạo chỉ báo cho mỗi cặp:

$$E\binom X2=\binom n2p^2.$$

Do $\binom X2=X(X-1)/2$, suy ra

$$n(n-1)p^2=E(X(X-1))=E(X^2)-E(X)=E(X^2)-np.$$

Vậy một lần nữa,

$$\operatorname{Var}(X)
=E(X^2)-(EX)^2
=n(n-1)p^2+np-(np)^2
=np(1-p).$$

Bài tập 44 dùng cách này để tìm phương sai Siêu bội. ◇

### 4.7 Phân phối Poisson

Phân phối rời rạc cuối cùng giới thiệu trong chương này là Poisson, rất phổ biến để mô hình hóa dữ liệu đếm. Ta sẽ nêu PMF, trung bình, phương sai rồi bàn kỹ hơn về câu chuyện của nó.

**Định nghĩa 4.7.1 (Phân phối Poisson).** Biến $X$ có phân phối Poisson với tham số $\lambda$ nếu

$$P(X=k)=\frac{e^{-\lambda}\lambda^k}{k!},\qquad k=0,1,2,\ldots.$$

Ký hiệu $X\sim\operatorname{Pois}(\lambda)$. Đây là PMF hợp lệ vì chuỗi Taylor $\sum_{k=0}^{\infty}\lambda^k/k!=e^\lambda$.

**Ví dụ 4.7.2 (Kỳ vọng và phương sai Poisson).** Cho $X\sim\operatorname{Pois}(\lambda)$. Ta sẽ chứng minh cả trung bình và phương sai đều bằng $\lambda$. Với kỳ vọng, bỏ số hạng $k=0$ vì bằng 0, rồi đưa $\lambda$ ra ngoài:

$$\begin{aligned}
E(X)
&=e^{-\lambda}\sum_{k=1}^{\infty}k\frac{\lambda^k}{k!}\\
&=\lambda e^{-\lambda}\sum_{k=1}^{\infty}
\frac{\lambda^{k-1}}{(k-1)!}
=\lambda e^{-\lambda}e^\lambda
=\lambda.
\end{aligned}$$

Để tính phương sai, trước tiên tìm $E(X^2)$ bằng LOTUS:

$$E(X^2)=e^{-\lambda}
\sum_{k=0}^{\infty}k^2\frac{\lambda^k}{k!}.$$

Giống cách tính phương sai Hình học, bắt đầu từ chuỗi quen thuộc, lấy đạo hàm theo $\lambda$ rồi nhân lại với $\lambda$:

$$\sum_{k=0}^{\infty}\frac{\lambda^k}{k!}=e^\lambda,
\qquad
\sum_{k=1}^{\infty}k\frac{\lambda^{k-1}}{k!}=e^\lambda,
\qquad
\sum_{k=1}^{\infty}k\frac{\lambda^k}{k!}=\lambda e^\lambda.$$

Lặp lại:

$$\sum_{k=1}^{\infty}k^2\frac{\lambda^{k-1}}{k!}
=e^\lambda+\lambda e^\lambda
=e^\lambda(1+\lambda),$$

$$\sum_{k=1}^{\infty}k^2\frac{\lambda^k}{k!}
=\lambda e^\lambda(1+\lambda).$$

Vậy $E(X^2)=\lambda(1+\lambda)$ và

$$\operatorname{Var}(X)
=E(X^2)-(EX)^2
=\lambda(1+\lambda)-\lambda^2
=\lambda.\quad\Diamond$$

Hình 4.7 vẽ PMF và CDF của $\operatorname{Pois}(2)$ và $\operatorname{Pois}(5)$ từ $k=0$ đến 10. Trung bình dường như nằm quanh 2 và 5, khớp kết quả trên. PMF của $\operatorname{Pois}(2)$ rất lệch; khi $\lambda$ lớn hơn, độ lệch giảm và PMF gần hình chuông hơn.

Poisson thường dùng khi đếm số lần thành công trong một vùng hoặc khoảng thời gian, có nhiều “phép thử” nhưng mỗi phép thử rất ít khả năng thành công. Ví dụ, các biến sau có thể xấp xỉ Poisson:

- Số email bạn nhận trong một giờ. Rất nhiều người có thể gửi, nhưng một người cụ thể ít khả năng gửi trong giờ ấy. Hoặc chia giờ thành mili giây: có $3{,}6\times10^6$ mili giây trong một giờ, và xác suất nhận email trong một mili giây cụ thể rất nhỏ. *Bản gốc in “giây” tại chỗ này; con số tương ứng là mili giây.*
- Số hạt sô cô la trong một chiếc bánh quy. Chia bánh thành những khối lập phương nhỏ: mỗi khối ít khả năng chứa hạt, nhưng có rất nhiều khối.
- Số động đất trong một năm ở một vùng. Tại một thời điểm và địa điểm cụ thể, xác suất động đất thấp, nhưng suốt năm có rất nhiều thời điểm, địa điểm có thể xảy ra.

*Hình 4.7 (trang PDF 181).* Hàng trên: PMF và CDF $\operatorname{Pois}(2)$. Hàng dưới: PMF và CDF $\operatorname{Pois}(5)$.

Tham số $\lambda$ được hiểu là *tốc độ* xảy ra các biến cố hiếm. Ở ba ví dụ trên, nó có thể lần lượt là 20 email/giờ, 10 hạt/bánh và 2 trận động đất/năm. *Mô hình Poisson* nói rằng trong các ứng dụng tương tự, phân phối số biến cố xảy ra có thể xấp xỉ bằng Poisson.

**Xấp xỉ 4.7.3 (Mô hình Poisson).** Cho các biến cố $A_1,\ldots,A_n$ với $p_j=P(A_j)$, trong đó $n$ lớn, các $p_j$ nhỏ và các biến cố độc lập hoặc chỉ phụ thuộc yếu. Đặt

$$X=\sum_{j=1}^{n}I_{A_j}$$

đếm số biến cố xảy ra. Khi ấy $X$ xấp xỉ $\operatorname{Pois}(\lambda)$ với $\lambda=\sum_{j=1}^{n}p_j$.

Chứng minh chất lượng xấp xỉ này khó, vì cần định nghĩa chính xác “phụ thuộc yếu” và “xấp xỉ tốt”. Một định lý đáng chú ý: nếu các $A_j$ độc lập, $N\sim\operatorname{Pois}(\lambda)$ và $B$ là tập bất kỳ gồm các số nguyên không âm, thì

$$|P(X\in B)-P(N\in B)|
\le\min\left(1,\frac1\lambda\right)
\sum_{j=1}^{n}p_j^2.$$

Đây là chặn trên sai số xấp xỉ không chỉ cho PMF của $X$ mà còn cho xác suất $X$ nằm trong bất kỳ tập nào. Nó cũng làm rõ “$p_j$ nhỏ” nghĩa là gì: ta muốn $\sum_jp_j^2$ rất nhỏ, hoặc ít nhất rất nhỏ so với $\lambda$. Có thể chứng minh bằng kỹ thuật nâng cao gọi là phương pháp Stein–Chen.

Mô hình Poisson còn gọi là *luật biến cố hiếm*. “Hiếm” nghĩa là các $p_j$ nhỏ, chứ không nhất thiết $\lambda$ nhỏ. Trong ví dụ email, xác suất một người cụ thể gửi thư trong giờ đó thấp, nhưng có rất nhiều người có thể gửi.

Những ví dụ trên không có phân phối Poisson chính xác: biến Poisson không bị chặn trên, trong khi chỉ có tối đa $n$ biến cố trong $A_1,\ldots,A_n$ xảy ra, và không thể nhét vô hạn hạt sô cô la vào một chiếc bánh. Dù vậy, Poisson thường xấp xỉ tốt. Điều kiện khá linh hoạt: các phép thử có thể có xác suất thành công khác nhau và không buộc độc lập hoàn toàn, miễn sự phụ thuộc không quá mạnh. Vì vậy Poisson là mô hình phổ biến, hoặc ít nhất là điểm khởi đầu, cho dữ liệu nguyên không âm (*dữ liệu đếm* trong thống kê).

Xấp xỉ Poisson giúp giải gần đúng bài toán ngày sinh ở Chương 1 và nhiều biến thể rất khó giải chính xác.

**Ví dụ 4.7.4 (Trở lại bài toán ngày sinh).** Với $m$ người và các giả thiết thông thường, mỗi cặp có xác suất trùng ngày sinh $1/365$ và có $\binom m2$ cặp. Theo mô hình Poisson, số cặp trùng $X$ xấp xỉ $\operatorname{Pois}(\lambda)$ với $\lambda=\binom m2/365$. Vì vậy

$$P(X\ge1)=1-P(X=0)\approx1-e^{-\lambda}.$$

Với $m=23$, $\lambda=253/365$ và $1-e^{-\lambda}\approx0{,}500002$, khớp kết quả Chương 1 rằng 23 người là đủ cho cơ hội trùng ngày sinh gần 50–50. Dù $m=23$ không quá lớn, đại lượng liên quan thực sự là $\binom m2$, tổng số “phép thử” cho một cặp trùng, nên xấp xỉ vẫn tốt. ◇

**Ví dụ 4.7.5 (Ngày sinh gần nhau).** Muốn có xác suất 50–50 rằng hai người sinh cách nhau tối đa một ngày (cùng ngày hoặc trước/sau một ngày), cần bao nhiêu người? Khác bài toán gốc, đáp án chính xác khó tìm, nhưng mô hình Poisson vẫn dùng được. Mỗi cặp có xác suất ngày sinh cách nhau tối đa một ngày là $3/365$: chọn ngày sinh người đầu, người thứ hai cần sinh hôm ấy, hôm trước hoặc hôm sau. Có $\binom m2$ cặp, nên số cặp phù hợp xấp xỉ $\operatorname{Pois}(\lambda)$ với $\lambda=3\binom m2/365$. Tính tương tự cho thấy cần ít nhất $m=14$. Đây là xấp xỉ nhanh, nhưng hóa ra 14 cũng chính là đáp án chính xác! ◇

### 4.8 Liên hệ giữa Poisson và Nhị thức

Hai phân phối liên hệ chặt chẽ, song song với liên hệ Nhị thức–Siêu bội ở chương trước: từ Poisson sang Nhị thức bằng điều kiện hóa; từ Nhị thức sang Poisson bằng lấy giới hạn.

Các kết quả dựa trên tính chất tổng hai biến Poisson độc lập vẫn là Poisson, giống tổng hai biến Nhị thức độc lập có cùng xác suất thành công vẫn là Nhị thức. Trước mắt ta chứng minh bằng luật xác suất toàn phần; Chương 6 sẽ cho phương pháp nhanh hơn bằng *hàm sinh mômen*. Chương 13 cung cấp thêm trực giác.

**Định lý 4.8.1 (Tổng các biến Poisson độc lập).** Nếu $X\sim\operatorname{Pois}(\lambda_1)$, $Y\sim\operatorname{Pois}(\lambda_2)$ và chúng độc lập, thì $X+Y\sim\operatorname{Pois}(\lambda_1+\lambda_2)$.

**Chứng minh.** Điều kiện hóa theo $X$, dùng luật xác suất toàn phần và tính độc lập:

$$\begin{aligned}
P(X+Y=k)
&=\sum_{j=0}^{k}P(X+Y=k\mid X=j)P(X=j)\\
&=\sum_{j=0}^{k}P(Y=k-j)P(X=j)\\
&=\sum_{j=0}^{k}
\frac{e^{-\lambda_2}\lambda_2^{k-j}}{(k-j)!}
\frac{e^{-\lambda_1}\lambda_1^j}{j!}\\
&=\frac{e^{-(\lambda_1+\lambda_2)}}{k!}
\sum_{j=0}^{k}\binom kj\lambda_1^j\lambda_2^{k-j}\\
&=\frac{e^{-(\lambda_1+\lambda_2)}
(\lambda_1+\lambda_2)^k}{k!}.
\end{aligned}$$

Bước cuối dùng định lý nhị thức. Ta thu được PMF $\operatorname{Pois}(\lambda_1+\lambda_2)$. Theo câu chuyện Poisson, nếu hai loại biến cố độc lập xảy ra với tốc độ $\lambda_1,\lambda_2$, thì tổng tốc độ là $\lambda_1+\lambda_2$. □

**Định lý 4.8.2 (Poisson có điều kiện theo tổng).** Nếu $X\sim\operatorname{Pois}(\lambda_1)$, $Y\sim\operatorname{Pois}(\lambda_2)$ độc lập, thì phân phối có điều kiện của $X$ khi biết $X+Y=n$ là $\operatorname{Bin}(n,\lambda_1/(\lambda_1+\lambda_2))$.

**Chứng minh (bắt đầu).** Như chứng minh tương ứng cho Nhị thức và Siêu bội, dùng quy tắc Bayes:

$$P(X=k\mid X+Y=n)
=\frac{P(X+Y=n\mid X=k)P(X=k)}{P(X+Y=n)}
=\frac{P(Y=n-k)P(X=k)}{P(X+Y=n)}.$$

Thay các PMF của $X,Y,X+Y$ (biến cuối có phân phối $\operatorname{Pois}(\lambda_1+\lambda_2)$):

$$\begin{aligned}
P(X=k\mid X+Y=n)
&=\frac{
\left(e^{-\lambda_2}\lambda_2^{n-k}/(n-k)!\right)
\left(e^{-\lambda_1}\lambda_1^k/k!\right)}
{e^{-(\lambda_1+\lambda_2)}(\lambda_1+\lambda_2)^n/n!}\\
&=\binom nk\frac{\lambda_1^k\lambda_2^{n-k}}
{(\lambda_1+\lambda_2)^n}\\
&=\binom nk
\left(\frac{\lambda_1}{\lambda_1+\lambda_2}\right)^k
\left(\frac{\lambda_2}{\lambda_1+\lambda_2}\right)^{n-k}.
\end{aligned}$$

Đây đúng là PMF $\operatorname{Bin}(n,\lambda_1/(\lambda_1+\lambda_2))$. □

Ngược lại, nếu cho $n\to\infty$, $p\to0$ trong $\operatorname{Bin}(n,p)$ mà giữ $np$ cố định, ta thu được Poisson. Đây là cơ sở cho phép xấp xỉ Poisson đối với Nhị thức.

**Định lý 4.8.3 (Xấp xỉ Poisson cho Nhị thức).** Nếu $X\sim\operatorname{Bin}(n,p)$, $n\to\infty$, $p\to0$ và $\lambda=np$ giữ cố định, thì PMF của $X$ hội tụ đến PMF $\operatorname{Pois}(\lambda)$. Tổng quát hơn, kết luận vẫn đúng nếu $np\to\lambda$.

Đây là trường hợp riêng của mô hình Poisson khi các biến cố $A_j$ độc lập và có cùng xác suất, nên tổng chỉ báo có phân phối Nhị thức. Trong trường hợp này, có thể chứng minh xấp xỉ bằng cách lấy giới hạn PMF.

**Chứng minh.** Xét $\lambda=np$ cố định. Với $0\le k\le n$,

$$\begin{aligned}
P(X=k)
&=\binom nk p^k(1-p)^{n-k}\\
&=\frac{\lambda^k}{k!}
\frac{n(n-1)\cdots(n-k+1)}{n^k}
\left(1-\frac\lambda n\right)^n
\left(1-\frac\lambda n\right)^{-k}.
\end{aligned}$$

Khi $n\to\infty$ với $k$ cố định, ba thừa số sau lần lượt tiến đến $1,e^{-\lambda},1$; giới hạn giữa là công thức lãi kép ở phụ lục toán học. Vậy

$$P(X=k)\longrightarrow
\frac{e^{-\lambda}\lambda^k}{k!},$$

PMF của $\operatorname{Pois}(\lambda)$. □

Nếu $n$ lớn, $p$ nhỏ và $np$ ở mức vừa phải, có thể xấp xỉ PMF $\operatorname{Bin}(n,p)$ bằng PMF $\operatorname{Pois}(np)$. Điều quan trọng nhất là $p$ nhỏ. Thực ra chặn sai số sau mô hình Poisson cho biết trong trường hợp này sai số xấp xỉ $P(X\in B)$ bằng $P(N\in B)$, với $N\sim\operatorname{Pois}(np)$, không vượt quá $\min(p,np^2)$.

**Ví dụ 4.8.4 (Khách truy cập trang web).** Chủ một trang web nghiên cứu phân phối số khách truy cập. Mỗi ngày, một triệu người độc lập quyết định có ghé trang hay không; mỗi người có xác suất $p=2\times10^{-6}$ ghé. Hãy xấp xỉ xác suất có ít nhất ba khách trong một ngày.

**Lời giải.** Gọi $X\sim\operatorname{Bin}(n,p)$ là số khách, $n=10^6$. Tính chính xác có thể gặp khó khăn số học vì $n$ rất lớn, $p$ rất nhỏ. Nhưng $np=2$ vừa phải, nên $\operatorname{Pois}(2)$ là xấp xỉ tốt:

$$P(X\ge3)=1-P(X<3)
\approx1-e^{-2}-2e^{-2}-\frac{2^2}{2!}e^{-2}
=1-5e^{-2}\approx0{,}3233.$$

Xấp xỉ này hóa ra cực kỳ chính xác. ◇

### 4.9 *Dùng xác suất và kỳ vọng để chứng minh sự tồn tại

Một điều đẹp và đáng ngạc nhiên: có thể dùng xác suất và kỳ vọng để chứng minh tồn tại những đối tượng có tính chất mong muốn. Kỹ thuật này gọi là *phương pháp xác suất*, dựa trên hai ý đơn giản nhưng mạnh. Giả sử muốn chứng minh có một đối tượng trong một tập hợp sở hữu tính chất nào đó. Thoạt nhìn không liên quan xác suất; ta có thể kiểm tra từng đối tượng đến khi tìm thấy.

Phương pháp xác suất thay cách kiểm tra tỉ mỉ bằng chọn ngẫu nhiên: lấy một đối tượng ngẫu nhiên và chứng minh xác suất nó có tính chất cần tìm là dương. Không cần tính chính xác xác suất, chỉ cần chứng minh nó lớn hơn 0. Khi đó chắc chắn có đối tượng sở hữu tính chất, dù ta chưa biết xây dựng cụ thể.

Tương tự, nếu mỗi đối tượng có một điểm số và ta muốn chứng minh có đối tượng có điểm “tốt”, vượt một ngưỡng, hãy chọn đối tượng ngẫu nhiên và gọi điểm của nó là $X$. Phải có đối tượng đạt ít nhất $E(X)$: không thể tất cả đều dưới trung bình. Nếu $E(X)$ đã là điểm tốt thì tồn tại đối tượng tốt. Hai ý được phát biểu:

- **Nguyên lý khả năng:** Nếu biến cố $A$ là “đối tượng chọn ngẫu nhiên có tính chất cần tìm” và $P(A)>0$, thì tồn tại đối tượng có tính chất ấy.
- **Nguyên lý điểm tốt:** Nếu $X$ là điểm đối tượng chọn ngẫu nhiên và $E(X)\ge c$, thì tồn tại đối tượng đạt ít nhất $c$.

Nguyên lý khả năng đúng theo phản đảo: nếu không có đối tượng nào sở hữu tính chất thì xác suất chọn được đối tượng như vậy bằng 0. Tương tự, nếu mọi điểm đều dưới $c$ thì trung bình có trọng số cũng dưới $c$. Phương pháp xác suất chỉ bảo đảm tồn tại, không chỉ cách tìm đối tượng.

**Ví dụ 4.9.1.** Có 100 người được phân vào 15 ủy ban, mỗi ủy ban 20 người, mỗi người tham gia ba ủy ban. Chứng minh tồn tại hai ủy ban có ít nhất ba thành viên chung.

**Lời giải.** Liệt kê mọi cách phân công rồi đếm giao của mọi cặp ủy ban là không thực tế. Ta chọn ngẫu nhiên hai ủy ban bất kỳ và gọi $X$ là số người thuộc cả hai. Viết $X=I_1+\cdots+I_{100}$, với $I_j=1$ nếu người thứ $j$ thuộc cả hai. Theo đối xứng, $E(X)=100E(I_1)$.

Theo cây cầu cơ bản, $E(I_1)$ là xác suất người thứ nhất, gọi là Bob, thuộc cả hai ủy ban được chọn. Xem ba ủy ban của Bob như ba con nai được đánh dấu trong quần thể 15 con; hai ủy ban chọn ngẫu nhiên là mẫu hai con không hoàn lại. Theo PMF $\operatorname{HGeom}(3,12,2)$,

$$E(I_1)=P(\text{cả hai ủy ban đều có Bob})
=\frac{\binom32\binom{12}0}{\binom{15}2}
=\frac1{35}.$$

Do đó $E(X)=100/35=20/7$, hơi dưới ngưỡng điểm tốt 3. Nhưng vẫn đủ: nguyên lý điểm tốt cho cặp ủy ban có ít nhất $20/7$ người chung; số người là số nguyên nên phải ít nhất 3. ◇

#### 4.9.1 *Truyền thông qua kênh nhiễu

Phương pháp xác suất còn có ứng dụng lớn trong lý thuyết thông tin, ngành nghiên cứu cách truyền tin đáng tin cậy qua kênh nhiễu. Ai cũng có thể gặp nhiễu khi gọi điện, khiến lời nói bị nghe sai. Giả sử thông điệp là vectơ nhị phân $x\in\{0,1\}^k$ và ta muốn dùng mã để tăng khả năng truyền thành công.

**Định nghĩa 4.9.2 (Mã và tốc độ).** Với các số nguyên dương $k,n$, *mã* là hàm $c$ gán cho mỗi thông điệp đầu vào $x\in\{0,1\}^k$ một *từ mã* $c(x)\in\{0,1\}^n$. Tốc độ mã là $k/n$, số bit đầu vào trên mỗi bit đầu ra. Sau khi gửi $c(x)$, bộ giải mã nhận thông điệp có thể đã hỏng và cố khôi phục $x$.

Một mã hiển nhiên là lặp lại thông điệp $m$ lần, với $m$ lẻ. Đây là *mã lặp*. Người nhận lấy kết quả đa số cho từng bit; chẳng hạn giải bit đầu của $x$ thành 1 nếu bit ấy được nhận là 1 nhiều hơn 0. Nhưng mã có thể rất kém hiệu quả: để giảm mạnh xác suất lỗi, có thể cần lặp nhiều lần, làm tốc độ $1/m$ rất thấp.

Claude Shannon, người khai sinh lý thuyết thông tin, chứng minh điều kỳ diệu: ngay cả kênh rất nhiễu vẫn có mã cho truyền tin rất đáng tin cậy với tốc độ không tiến về 0 khi ta đòi xác suất lỗi ngày càng nhỏ. Chứng minh của ông còn bất ngờ hơn: xét hiệu quả của một mã hoàn toàn ngẫu nhiên. Richard Hamming, đồng nghiệp của Shannon tại Bell Labs, kể:

> Can đảm cũng là phẩm chất của những người làm được việc lớn. Shannon là ví dụ. Có một thời gian ông đến chỗ làm khoảng 10 giờ sáng, chơi cờ đến khoảng 2 giờ chiều rồi về nhà.
>
> Điều quan trọng là cách ông chơi. Khi bị tấn công, ông hầu như không phòng thủ mà phản công. Cách chơi ấy nhanh chóng tạo bàn cờ rối rắm, nhiều quân liên hệ nhau. Ông dừng suy nghĩ đôi chút rồi tiến hậu, nói: “Tôi chẳng sợ gì cả.” Mãi sau tôi mới hiểu tất nhiên đó là lý do ông chứng minh được sự tồn tại của các phương pháp mã hóa tốt. Ngoài Shannon, ai nghĩ đến việc lấy trung bình trên mọi mã ngẫu nhiên mà mong trung bình gần lý tưởng? Tôi học cách tự nói như thế khi mắc kẹt, và đôi khi cách tiếp cận của ông giúp tôi đạt kết quả đáng kể. [16]

Ta sẽ chứng minh một phiên bản kết quả của Shannon cho kênh mà mỗi bit truyền đi bị đảo từ 0 sang 1 hoặc ngược lại với xác suất $p$, độc lập. Trước hết cần hai định nghĩa.

**Định nghĩa 4.9.3 (Khoảng cách Hamming).** Với hai vectơ nhị phân $v,w$ cùng độ dài, khoảng cách Hamming $d(v,w)$ là số vị trí chúng khác nhau:

$$d(v,w)=\sum_i|v_i-w_i|.$$

**Định nghĩa 4.9.4 (Hàm entropy nhị phân).** Với $0<p<1$, hàm entropy nhị phân là

$$H(p)=-p\log_2p-(1-p)\log_2(1-p),$$

và đặt $H(0)=H(1)=0$.

Trong lý thuyết thông tin, $H(p)$ đo lượng thông tin thu được khi quan sát biến $\operatorname{Bern}(p)$. $H(1/2)=1$ nghĩa là tung xu công bằng cho 1 bit thông tin; $H(1)=0$ nghĩa là nếu xu luôn ra ngửa thì nghe thông báo kết quả không cho thông tin mới.

Xét kênh đảo mỗi bit với xác suất $p$, độc lập. Trực giác có thể cho rằng $p$ càng nhỏ càng tốt; thực tế $p=1/2$ là trường hợp tệ nhất, gọi là *kênh vô dụng*: đầu ra độc lập với đầu vào, không thể truyền thông tin. Tương tự, khi quyết định xem phim, bạn muốn nghe người luôn bất đồng với mình hay người chỉ đồng ý với bạn một nửa số lần? Ta sẽ chứng minh khi $0<p<1/2$, có thể truyền rất đáng tin cậy với tốc độ gần $1-H(p)$.

**Định lý 4.9.5 (Shannon).** Trên kênh đảo từng bit độc lập với xác suất $0<p<1/2$, với mọi $\varepsilon>0$, tồn tại mã có tốc độ ít nhất $1-H(p)-\varepsilon$ và xác suất giải mã lỗi nhỏ hơn $\varepsilon$.

**Chứng minh (bắt đầu).** Có thể giả sử $1-H(p)-\varepsilon>0$, vì nếu không thì không có ràng buộc tốc độ. Chọn số nguyên dương $n$ lớn (theo những điều kiện sẽ nêu) và đặt

$$k=\left\lceil n(1-H(p)-\varepsilon)\right\rceil+1.$$

Dùng hàm trần vì $k$ phải nguyên. Chọn $p'\in(p,1/2)$ sao cho $|H(p')-H(p)|<\varepsilon/2$, làm được vì $H$ liên tục.

Xét một mã ngẫu nhiên $C$. Với mỗi thông điệp đầu vào $x\in\{0,1\}^k$, chọn độc lập $C(x)$ đều ngẫu nhiên trong $\{0,1\}^n$. Có thể xem $C(x)$ là vectơ gồm $n$ biến $\operatorname{Bern}(1/2)$ i.i.d. Tốc độ $k/n$ vượt $1-H(p)-\varepsilon$ theo định nghĩa; giờ xét khả năng giải mã.

Cho $x$ là thông điệp đầu vào, $C(x)$ là từ mã và $Y\in\{0,1\}^n$ là thông điệp nhận. Tạm coi $x$ cố định. $C(x)$ ngẫu nhiên vì mã được chọn ngẫu nhiên; $Y$ ngẫu nhiên vì cả mã lẫn nhiễu. Ta hy vọng $C(x)$ gần $Y$ theo khoảng cách Hamming, còn mọi $C(z)$ với $z\ne x$ đều xa $Y$. Quy tắc giải mã:

> Nếu tồn tại duy nhất $z\in\{0,1\}^k$ sao cho $d(C(z),Y)\le np'$, giải mã $Y$ thành $z$; nếu không, báo giải mã thất bại.

Sẽ chứng minh với $n$ đủ lớn, xác suất không khôi phục được $x$ nhỏ hơn $\varepsilon$. Có hai khả năng lỗi: (a) $d(C(x),Y)>np'$; hoặc (b) có “kẻ mạo danh” $z\ne x$ với $d(C(z),Y)\le np'$.

Lưu ý $d(C(x),Y)$ là biến ngẫu nhiên, nên $d(C(x),Y)>np'$ là biến cố. Với (a), đặt $B_i$ là chỉ báo bit thứ $i$ bị đảo. Khi ấy

$$d(C(x),Y)=B_1+\cdots+B_n\sim\operatorname{Bin}(n,p).$$

Theo luật số lớn (Chương 10), khi $n$ tăng, $d(C(x),Y)/n$ tiến rất gần kỳ vọng $p$ nên rất ít khả năng vượt $p'$:

$$P(d(C(x),Y)>np')
=P\left(\frac{B_1+\cdots+B_n}{n}>p'\right)\longrightarrow0.$$

Chọn $n$ đủ lớn để xác suất này nhỏ hơn $\varepsilon/4$. Với (b), $d(C(z),Y)\sim\operatorname{Bin}(n,1/2)$ khi $z\ne x$: các bit của $C(z)$ độc lập, cùng phân phối $\operatorname{Bern}(1/2)$ và độc lập với $Y$ (có thể kiểm tra kỹ bằng cách điều kiện hóa theo $Y$ rồi dùng luật xác suất toàn phần). Gọi $B\sim\operatorname{Bin}(n,1/2)$. Theo bất đẳng thức Boole,

$$P(\exists z\ne x:d(C(z),Y)\le np')
\le(2^k-1)P(B\le np').$$

Để gọn ký hiệu, giả sử $np'$ nguyên. Có thể chặn tổng $m$ số hạng bằng $m$ lần số hạng lớn nhất; cũng có thể chặn $\binom nj\le r^{-j}(1-r)^{-(n-j)}$ với bất kỳ $r\in(0,1)$. Kết hợp hai chặn thô ấy,

$$\begin{aligned}
P(B\le np')
&=2^{-n}\sum_{j=0}^{np'}\binom nj\\
&\le\frac{np'+1}{2^n}\binom n{np'}\\
&\le(np'+1)2^{nH(p')-n},
\end{aligned}$$

vì $(p')^{-np'}(1-p')^{-n(1-p')}=2^{nH(p')}$. Do đó

$$\begin{aligned}
2^kP(B\le np')
&\le (np'+1)\,2^{n(1-H(p)-\varepsilon)+2+n(H(p)+\varepsilon/2)-n}\\
&=4(np'+1)2^{-n\varepsilon/2}\longrightarrow0.
\end{aligned}$$

Vậy có thể chọn $n$ sao cho xác suất có một $z\ne x$ đủ gần $Y$ nhỏ hơn $\varepsilon/4$.

Giả sử $k,n$ đã được chọn như trên. Gọi $F(c,x)$ là biến cố giải mã thất bại khi dùng mã $c$ với thông điệp $x$. Từ hai loại lỗi, với mã ngẫu nhiên $C$ và mọi $x$ cố định,

$$P(F(C,x))<\varepsilon/2.$$

Điều này cho biết với mỗi $x$ có một mã $c$ hoạt động tốt, nhưng ta cần *một mã dùng tốt cho mọi $x$*. Chọn thông điệp đầu vào ngẫu nhiên đều $X\in\{0,1\}^k$, độc lập với $C$. Theo luật xác suất toàn phần,

$$P(F(C,X))
=\sum_xP(F(C,x))P(X=x)
<\varepsilon/2.$$

Điều kiện hóa theo $C$ lần nữa:

$$\sum_cP(F(c,X))P(C=c)
=P(F(C,X))<\varepsilon/2.$$

Vì thế có mã $c$ sao cho xác suất lỗi trung bình trên thông điệp ngẫu nhiên $X$ nhỏ hơn $\varepsilon/2$. Cuối cùng, bỏ đi 50% thông điệp có xác suất lỗi lớn nhất đối với mã $c$. Mọi thông điệp còn lại có xác suất lỗi nhỏ hơn $\varepsilon$; nếu không, hơn nửa thông điệp sẽ có xác suất lỗi hơn gấp đôi trung bình. Đánh nhãn lại $2^{k-1}$ thông điệp còn lại bằng vectơ trong $\{0,1\}^{k-1}$, ta được mã $c':\{0,1\}^{k-1}\to\{0,1\}^n$ có tốc độ

$$\frac{k-1}{n}\ge1-H(p)-\varepsilon$$

và xác suất lỗi dưới $\varepsilon$ đối với *mọi* thông điệp đầu vào. □

Định lý trên cũng có chiều đảo: nếu đòi tốc độ ít nhất $1-H(p)+\varepsilon$ thì không thể tìm mã có xác suất lỗi nhỏ tùy ý. Vì vậy $1-H(p)$ được gọi là *dung lượng* của kênh. Shannon còn có kết quả tương tự cho những kênh tổng quát hơn. Chúng cho giới hạn lý thuyết về điều có thể đạt, nhưng không chỉ rõ nên dùng mã nào. Suốt nhiều thập kỷ sau, người ta phát triển các mã cụ thể vừa gần giới hạn Shannon vừa mã hóa, giải mã hiệu quả.

### 4.10 Tóm tắt

Kỳ vọng của biến rời rạc $X$ là

$$E(X)=\sum_xxP(X=x).$$

Cách tính tương đương, chưa gom nhóm:

$$E(X)=\sum_sX(s)P(\{s\}),$$

với tổng lấy trên các kết quả mẫu. Kỳ vọng tóm tắt trọng tâm phân phối bằng một số. Phương sai tóm tắt độ trải rộng:

$$\operatorname{Var}(X)
=E((X-EX)^2)
=E(X^2)-(EX)^2.$$

Căn bậc hai phương sai là độ lệch chuẩn.

Kỳ vọng tuyến tính:

$$E(cX)=cE(X),\qquad E(X+Y)=E(X)+E(Y),$$

bất kể $X,Y$ có độc lập hay không. Phương sai không tuyến tính: $\operatorname{Var}(cX)=c^2\operatorname{Var}(X)$ và nhìn chung $\operatorname{Var}(X+Y)\ne\operatorname{Var}(X)+\operatorname{Var}(Y)$; trường hợp quan trọng có đẳng thức là $X,Y$ độc lập.

Chiến lược rất quan trọng để tính kỳ vọng của biến rời rạc là biểu diễn nó thành tổng các biến chỉ báo, rồi dùng tính tuyến tính và cây cầu cơ bản. Các chỉ báo không cần độc lập. Ba bước:

1. Viết $X$ thành tổng các chỉ báo. Hãy xem $X$ đang đếm gì; chẳng hạn nếu $X$ đếm cực đại địa phương thì đặt một chỉ báo cho mỗi vị trí có thể là cực đại.
2. Dùng cây cầu cơ bản tính kỳ vọng mỗi chỉ báo; tận dụng đối xứng nếu có.
3. Cộng các kỳ vọng chỉ báo nhờ tính tuyến tính.

LOTUS là công cụ khác: $E(g(X))=\sum_xg(x)P(X=x)$, chỉ cần PMF của $X$. Nếu $g$ phi tuyến, hoán đổi $E$ và $g$ là sai nghiêm trọng.

Ba phân phối rời rạc mới là Hình học, Nhị thức âm và Poisson. Biến $\operatorname{Geom}(p)$ đếm thất bại trước thành công đầu trong dãy phép thử Bernoulli độc lập với xác suất thành công $p$; $\operatorname{NBin}(r,p)$ đếm thất bại trước thành công thứ $r$. Phân phối Lần thành công đầu tiên cũng được giới thiệu: đó là Hình học được cộng thêm 1 để tính cả lần thành công.

Poisson thường xấp xỉ số lần thành công khi có nhiều phép thử độc lập hoặc phụ thuộc yếu, mỗi phép thử ít khả năng thành công. Trong câu chuyện Nhị thức, mọi phép thử có cùng xác suất $p$; ở xấp xỉ Poisson, mỗi phép thử có thể có xác suất nhỏ $p_j$ khác nhau.

Poisson, Nhị thức và Siêu bội liên hệ qua điều kiện hóa và giới hạn, như Hình 4.8. Những chương sau sẽ thêm phân phối mới vào “cây gia đình” này. Hình 4.9 mở rộng sơ đồ của chương trước về bốn loại đối tượng: phân phối, biến ngẫu nhiên, biến cố và con số.

*Hình 4.8 (trang PDF 194).* Quan hệ giữa Poisson, Nhị thức và Siêu bội: điều kiện hóa đưa Poisson tới Nhị thức, Nhị thức tới Siêu bội; lấy giới hạn theo chiều ngược lại.

*Hình 4.9.* Từ biến $X$, các hàm cho biến khác như $X^2,X^3,g(X)$; LOTUS cho các kỳ vọng $E(X),E(X^2),E(X^3),E(g(X))$. Trung bình, phương sai và độ lệch chuẩn biểu thị vị trí trung bình và độ trải rộng của phân phối $X$; chúng chỉ phụ thuộc CDF $F$, không phụ thuộc trực tiếp bản thân phép gán $X$.

### 4.11 R

#### Hình học, Nhị thức âm và Poisson

Ba hàm R cho phân phối Hình học là <code>dgeom</code>, <code>pgeom</code>, <code>rgeom</code>, tương ứng PMF, CDF và sinh số ngẫu nhiên. Hai hàm đầu nhận giá trị cần tính rồi tham số $p$; hàm thứ ba nhận số biến cần sinh rồi $p$.

Ví dụ, để tính $P(X=3)$ và $P(X\le3)$ với $X\sim\operatorname{Geom}(0{,}5)$, lần lượt dùng <code>dgeom(3,0.5)</code>, <code>pgeom(3,0.5)</code>. Để sinh 100 biến i.i.d. $\operatorname{Geom}(0{,}8)$, dùng <code>rgeom(100,0.8)</code>. Muốn sinh 100 biến i.i.d. $\operatorname{FS}(0{,}8)$ thì cộng 1: <code>rgeom(100,0.8)+1</code>.

Với Nhị thức âm có <code>dnbinom</code>, <code>pnbinom</code>, <code>rnbinom</code>, mỗi hàm nhận ba đối số. Chẳng hạn, PMF $\operatorname{NBin}(5,0{,}5)$ tại 3 là <code>dnbinom(3,5,0.5)</code>.

Với Poisson có <code>dpois</code>, <code>ppois</code>, <code>rpois</code>, mỗi hàm nhận hai đối số. CDF $\operatorname{Pois}(10)$ tại 2 là <code>ppois(2,10)</code>.

#### Mô phỏng bài toán ghép cặp

Tiếp Ví dụ 4.4.4, dùng mô phỏng tính số lá khớp kỳ vọng. Đặt $n$ là số lá, lặp thí nghiệm $10^4$ lần:

    n <- 100
    r <- replicate(10^4,sum(sample(n)==(1:n)))

Vectơ <code>r</code> chứa số lá khớp ở mỗi lần mô phỏng. Thay vì xác suất có ít nhất một lá khớp như Chương 1, giờ cần trung bình số lá khớp. Dùng <code>mean(r)</code>, tương đương <code>sum(r)/length(r)</code>. Kết quả rất gần 1, xác nhận phép tính bằng chỉ báo ở Ví dụ 4.4.4. Dù chọn $n$ nào, <code>mean(r)</code> vẫn rất gần 1.

#### Mô phỏng số ngày sinh khác nhau

Tính số ngày sinh khác nhau kỳ vọng trong nhóm $k$ người bằng mô phỏng. Chọn $k=20$, nhưng có thể chọn giá trị khác:

    k <- 20
    r <- replicate(10^4,{bdays <- sample(365,k,replace=TRUE);
    length(unique(bdays))})

Lệnh <code>replicate</code> lặp biểu thức trong ngoặc nhọn $10^4$ lần. Mỗi lần lấy mẫu $k$ ngày sinh có hoàn lại từ 1 đến 365 và lưu ở <code>bdays</code>. <code>unique(bdays)</code> bỏ ngày trùng; <code>length(unique(bdays))</code> đếm số ngày còn lại. Hai lệnh trong ngoặc nhọn được ngăn bằng dấu chấm phẩy.

Giờ <code>r</code> chứa số ngày sinh khác nhau ở mỗi lần mô phỏng. Trung bình là <code>mean(r)</code>; so với giá trị lý thuyết ở Ví dụ 4.4.5:

    mean(r)
    365*(1-(364/365)^k)

Khi tác giả chạy, cả hai đều xấp xỉ $19{,}5$.

### 4.12 Bài tập

#### Kỳ vọng và phương sai

**1.** Bobo, con amip ở Chương 2, hiện sống một mình trong ao. Sau một phút, Bobo chết, tách thành hai amip, hoặc giữ nguyên, ba khả năng đồng xác suất. Tìm kỳ vọng và phương sai số amip trong ao sau một phút.

**2.** Trong lịch Gregory, một năm có 365 ngày (năm thường) hoặc 366 ngày (năm nhuận). Chọn ngẫu nhiên một năm với xác suất năm thường $3/4$, năm nhuận $1/4$. Tìm trung bình và phương sai số ngày của năm được chọn.

**3.** (a) Gieo một xúc xắc công bằng; tìm kỳ vọng kết quả. (b) Gieo bốn xúc xắc công bằng; tìm kỳ vọng tổng kết quả.

**4.** Gieo xúc xắc công bằng; bạn được chọn dừng sau một, hai hoặc ba lần gieo, dựa trên các kết quả đã thấy. Bạn nhận số đô la bằng kết quả lần gieo cuối. Chiến lược tối ưu để tối đa kỳ vọng tiền thắng là gì? Kỳ vọng tiền thắng theo chiến lược đó bằng bao nhiêu? Gợi ý: trước hết xét phiên bản chỉ được gieo tối đa hai lần; với những kết quả nào ở lần đầu nên gieo tiếp?

**5.** Tìm trung bình và phương sai của biến đều rời rạc trên $\{1,2,\ldots,n\}$. Gợi ý: xem phụ lục toán học về các công thức tổng.

**6.** Hai đội đấu tối đa bảy trận, dừng khi một đội thắng bốn trận. Mỗi trận có một đội thắng, đội kia thua. Giả sử hai đội có cơ hội thắng mỗi trận như nhau và các trận độc lập. Tìm trung bình và phương sai số trận được chơi.

**7.** Một thị trấn nhỏ có 100 gia đình: 30 gia đình có một con, 50 gia đình có hai con và 20 gia đình có ba con. *Thứ tự sinh* của một đứa trẻ là 1 nếu là con đầu, 2 nếu là con thứ hai, 3 nếu là con thứ ba. (a) Chọn ngẫu nhiên đều một gia đình, rồi chọn ngẫu nhiên đều một đứa trẻ trong gia đình đó. Tìm PMF, trung bình và phương sai thứ tự sinh của đứa trẻ. (b) Chọn ngẫu nhiên đều một đứa trẻ trong toàn thị trấn. Tìm PMF, trung bình và phương sai thứ tự sinh.

**8.** Một nước có bốn vùng Bắc, Đông, Nam, Tây với dân số lần lượt 3, 4, 5, 8 triệu. Vùng Bắc có bốn thành phố, Đông có ba, Nam có hai và Tây có một. Mỗi người sống trong đúng một thành phố. (a) Quy mô thành phố trung bình của cả nước là bao nhiêu? Đây là trung bình cộng dân số các thành phố, cũng là kỳ vọng dân số của thành phố chọn đều ngẫu nhiên. Gợi ý: đặt tên cho các thành phố. (b) Chứng minh không thể tính phương sai dân số của thành phố chọn ngẫu nhiên nếu thiếu thông tin về cách dân cư mỗi vùng phân bố giữa các thành phố. (c) Chọn ngẫu nhiên đều một vùng rồi chọn ngẫu nhiên đều một thành phố trong vùng ấy. Kỳ vọng dân số thành phố được chọn là bao nhiêu? Gợi ý: trước tiên tìm PMF dân số thành phố để sắp xếp phép tính. (d) Giải thích trực giác vì sao đáp án (c) lớn hơn (a).

**9.** Xét tình huống giản lược từ chương trình *Ai là triệu phú?*, nơi mỗi câu hỏi có bốn đáp án. Fred đã trả lời đúng chín câu và đang ở câu thứ mười. Anh không biết đáp án câu mười hoặc mười một. Anh có một quyền trợ giúp dùng ở một trong hai câu, giúp giảm bốn lựa chọn xuống còn hai. Các phương án:

(a) Dừng và nhận 16.000 đô la.

(b) Dùng trợ giúp ở câu mười rồi trả lời. Nếu sai, rời chương trình với 1.000 đô la; nếu đúng, sang câu mười một. Sau đó nhận 32.000 đô la nếu câu mười một sai, 64.000 đô la nếu đúng.

(c) Như (b), nhưng không dùng trợ giúp ở câu mười mà dùng ở câu mười một nếu qua được câu mười.

Tìm kỳ vọng tiền nhận theo từng phương án. Phương án nào có kỳ vọng cao nhất? Phương án nào có phương sai thấp nhất?

**10.** Xét nghịch lý St. Petersburg ở Ví dụ 4.3.13, nhưng nếu trò kéo dài $n$ lượt thì bạn nhận $n$ đô la thay vì $2^n$. Giá trị công bằng của trò là bao nhiêu? Nếu tiền thưởng là $n^2$ đô la thì sao?

**11.** Martin nghe một chiến lược cá cược hấp dẫn: cược 1 đô la rằng đồng xu công bằng ra ngửa. Nếu đúng thì dừng. Nếu ra sấp, tăng gấp đôi tiền cược ở lần tung tiếp, tức 2 đô la cho ngửa. Nếu đúng thì dừng; nếu không lại tăng gấp đôi thành 4 đô la, v.v., luôn dừng ngay sau lần thắng. Mỗi cược riêng là công bằng, có lợi nhuận ròng kỳ vọng bằng 0. Vì

$$1+2+2^2+\cdots+2^n=2^{n+1}-1,$$

sau lần thắng người chơi sẽ hơn ban đầu 1 đô la và có thể rời bàn. Martin thử chiến lược, nhưng chỉ có 31 đô la, nên có thể phá sản trước khi thắng. Trung bình Martin thắng bao nhiêu tiền?

**12.** Cho biến rời rạc $X$ có miền giá trị $\{-n,-n+1,\ldots,0,\ldots,n-1,n\}$ với $n$ nguyên dương. Giả sử PMF đối xứng: $P(X=-k)=P(X=k)$ với mọi $k$ nguyên. Tìm $E(X)$.

**13.** Có thể có hai biến rời rạc $X,Y$ sao cho $E(X)>100E(Y)$ nhưng $Y>X$ với xác suất ít nhất $0{,}99$ không?

**14.** Cho $X$ có PMF

$$P(X=k)=\frac{cp^k}{k},\qquad k=1,2,\ldots,$$

với $0<p<1$ và hằng số chuẩn hóa $c=-1/\log(1-p)$ theo chuỗi Taylor

$$-\log(1-p)=p+\frac{p^2}{2}+\frac{p^3}{3}+\cdots.$$

Đây là phân phối *Logarit*, thường được dùng trong sinh thái học. Tìm trung bình và phương sai của $X$.

**15.** Người chơi A chọn một số nguyên ngẫu nhiên từ 1 đến 100, với xác suất chọn $j$ là $p_j$. Người chơi B đoán số A đã chọn và nhận số đô la bằng chính số ấy nếu đoán đúng, bằng 0 nếu sai. (a) Giả sử B biết các $p_j$. Chiến lược tối ưu để tối đa tiền thắng kỳ vọng của B là gì? (b) Chứng minh nếu cả hai chọn $j$ với xác suất tỉ lệ $1/j$ thì không ai có động cơ đổi chiến lược khi chiến lược đối phương cố định. Theo thuật ngữ lý thuyết trò chơi, đây là một *cân bằng Nash*. (c) Tìm tiền thắng kỳ vọng của B theo chiến lược (b), biểu diễn dưới dạng tổng các hạng đơn giản và xấp xỉ số. Giá trị này có phụ thuộc chiến lược của A không?

**16.** Trưởng khoa Đại học Blotchville khoe quy mô lớp trung bình là 20. Nhưng đa số sinh viên lại học trong những lớp rất lớn, giảng đường chật chỗ ngồi và kẹo dẻo Haribo. Bài này giải thích nghịch lý đó. Giả sử mỗi sinh viên chỉ học một môn mỗi học kỳ. (a) Có 16 lớp thảo luận, mỗi lớp 10 sinh viên, và hai lớp giảng lớn, mỗi lớp 100 sinh viên. Tìm trung bình quy mô lớp theo góc nhìn trưởng khoa (trung bình đơn giản theo lớp) và theo góc nhìn sinh viên (trung bình quy mô lớp mà sinh viên trải nghiệm, như khi khảo sát sinh viên). Giải thích sự khác nhau. (b) Chứng minh ngắn rằng với mọi tập quy mô lớp, trung bình theo trưởng khoa nhỏ hơn nghiêm ngặt trung bình theo sinh viên, trừ khi mọi lớp cùng quy mô. Gợi ý: liên hệ tính không âm của phương sai.

#### Các phân phối có tên

**17.** Một cặp vợ chồng sinh con đến khi có ít nhất một trai và một gái rồi dừng. Giả sử không sinh đôi, các lần sinh độc lập với xác suất bé trai $1/2$, và họ đủ khả năng sinh con mãi. Kỳ vọng số con là bao nhiêu?

**18.** Tung đồng xu liên tiếp đến lần đầu ra ngửa. Gọi $X$ là tổng số lần tung, kể cả lần ngửa, và $p$ là xác suất ngửa, nên $X\sim\operatorname{FS}(p)$. Tìm CDF của $X$ và phác đồ thị khi $p=1/2$.

**19.** Cho $X\sim\operatorname{Bin}(100,0{,}9)$. Trong mỗi phần, hãy dựng ví dụ chứng minh có thể hoặc giải thích rõ vì sao bất khả thi. $Y$ nằm trên cùng không gian xác suất với $X$; hai biến không nhất thiết độc lập. (a) Có thể có $Y\sim\operatorname{Pois}(0{,}01)$ và $P(X\ge Y)=1$ không? (b) Có thể có $Y\sim\operatorname{Bin}(100,0{,}5)$ và $P(X\ge Y)=1$ không? (c) Có thể có $Y\sim\operatorname{Bin}(100,0{,}5)$ và $P(X\le Y)=1$ không?

**20.** Alice tung xu công bằng $n$ lần, Bob tung đồng xu công bằng khác $n+1$ lần, tạo hai biến độc lập $X\sim\operatorname{Bin}(n,1/2)$ và $Y\sim\operatorname{Bin}(n+1,1/2)$. (a) Đặt $V=\min(X,Y)$, $W=\max(X,Y)$. Nếu $X=Y$ thì $V=W=X=Y$. Tìm $E(V)+E(W)$. (b) Chứng minh $P(X<Y)=P(n-X<n+1-Y)$. (c) Tính $P(X<Y)$. Gợi ý: dùng (b) và việc $X,Y$ nguyên.

**21.** Mưa rơi trung bình 20 giọt trên mỗi inch vuông mỗi phút. Phân phối nào hợp lý để mô hình số giọt rơi trên vùng diện tích 5 inch vuông trong $t$ phút? Vì sao? Theo phân phối đã chọn, tính xác suất vùng ấy không nhận giọt nào trong khoảng ba giây.

**22.** Alice và Bob vừa gặp nhau và băn khoăn có bạn chung không. Mỗi người có 50 bạn trong số 1.000 người khác sống cùng thị trấn. Họ nghĩ khó trùng bạn vì mỗi người chỉ kết bạn với 5% dân số. Giả sử 50 bạn của Alice là mẫu ngẫu nhiên đều từ 1.000 người, tương tự Bob, và biết bạn của Alice không cho thông tin về bạn của Bob. (a) Tính kỳ vọng số bạn chung. (b) Gọi $X$ là số bạn chung; tìm PMF của $X$. (c) $X$ thuộc một phân phối quan trọng đã học không? Nếu có, phân phối nào?

**23.** Cho $X\sim\operatorname{Bin}(n,p)$ và $Y\sim\operatorname{NBin}(r,p)$. Dùng câu chuyện về dãy phép thử Bernoulli chứng minh $P(X<r)=P(Y>n-r)$.

**24.** Calvin và Hobbes đấu nhiều trận, Calvin thắng từng trận với xác suất $p$, độc lập. Luật thắng là dẫn đối thủ hai trận: người đầu tiên có nhiều hơn đối thủ hai trận là người thắng chung cuộc. Tìm kỳ vọng số trận đấu. Gợi ý: nhóm hai trận đầu thành một cặp, hai trận sau thành một cặp, v.v.

**25.** Nick và Penny thực hiện các dãy phép thử Bernoulli độc lập với nhau. Cụ thể, Nick tung đồng xu nickel có xác suất ngửa $p_1$, Penny tung đồng xu penny có xác suất ngửa $p_2$. Gọi $X_1,X_2,\ldots$ là kết quả của Nick, $Y_1,Y_2,\ldots$ là kết quả của Penny, với $X_i\sim\operatorname{Bern}(p_1)$ và $Y_j\sim\operatorname{Bern}(p_2)$. (a) Tìm phân phối và kỳ vọng của thời điểm đầu tiên họ cùng thành công, tức $n$ nhỏ nhất sao cho $X_n=Y_n=1$. Gợi ý: định nghĩa dãy phép thử Bernoulli mới và dùng câu chuyện Hình học. (b) Tìm kỳ vọng thời gian đến khi ít nhất một người thành công, tính cả lần thành công. Gợi ý tương tự. (c) Khi $p_1=p_2$, tìm xác suất những lần thành công đầu tiên của họ xảy ra đồng thời, rồi suy ra xác suất Nick thành công trước Penny.

**26.** Cho hai biến $X,Y\sim\operatorname{Pois}(\lambda)$ và $T=X+Y$. Giả sử $X,Y$ không độc lập, mà $X=Y$. Hãy chứng minh hoặc bác bỏ khẳng định $T\sim\operatorname{Pois}(2\lambda)$.

**27.** (a) Dùng LOTUS chứng minh rằng với $X\sim\operatorname{Pois}(\lambda)$ và hàm $g$ bất kỳ,

$$E(Xg(X))=\lambda E(g(X+1)).$$

Đây gọi là đồng nhất thức Stein–Chen cho Poisson. (b) Dùng đồng nhất thức ấy và một ít đại số để tìm mômen bậc ba $E(X^3)$, quy phép tính về việc $X$ có trung bình và phương sai đều bằng $\lambda$.

**28.** Trong dữ liệu đếm, giá trị 0 đôi khi xuất hiện nhiều hơn hẳn mức mà mô hình Poisson giải thích được. Có thể tăng $P(X=0)$ của $X\sim\operatorname{Pois}(\lambda)$ bằng cách giảm $\lambda$, nhưng điều đó cũng buộc trung bình và phương sai giảm vì cả hai bằng $\lambda$. *Poisson tăng cường số 0* là một biến thể cho phép xử lý nhiều số 0.

Biến $X$ có phân phối ấy với tham số $p,\lambda$ được tạo như sau: tung đồng xu có xác suất ngửa $p$. Nếu ngửa thì $X=0$; nếu sấp thì $X\sim\operatorname{Pois}(\lambda)$. Khi $X=0$, có hai khả năng: xu ngửa (số 0 *cấu trúc*) hoặc xu sấp nhưng biến Poisson tình cờ bằng 0. Chẳng hạn, $X$ là số bánh mì kẹp gà một người ăn trong một tuần. Người ăn chay chắc chắn có $X=0$ (số 0 cấu trúc), còn người ăn gà vẫn có thể tình cờ không ăn chiếc nào tuần đó.

(a) Tìm PMF của $X$. (b) Giải thích vì sao $X$ cùng phân phối với $(1-I)Y$, với $I\sim\operatorname{Bern}(p)$ độc lập với $Y\sim\operatorname{Pois}(\lambda)$. (c) Tìm trung bình $X$ bằng hai cách: trực tiếp qua PMF và qua biểu diễn ở (b). Với cách sau có thể dùng tính chất (chứng minh ở Chương 7): nếu $Z,W$ độc lập thì $E(ZW)=E(Z)E(W)$. (d) Tìm phương sai của $X$.

**29.** Một phân phối rời rạc có *tính không nhớ* nếu, với biến $X$ mang phân phối ấy, $P(X\ge j+k\mid X\ge j)=P(X\ge k)$ cho mọi số nguyên không âm $j,k$. (a) Nếu CDF là $F$ và PMF tại $i$ là $p_i=P(X=i)$, hãy biểu diễn $P(X\ge j+k)$ theo $F(j),F(k),p_j,p_k$. (b) Nêu một phân phối rời rạc có tính không nhớ và giải thích bằng lời hoặc bằng phép tính.

#### Biến chỉ báo

**30.** Đặt ngẫu nhiên $k$ quả bóng phân biệt vào $n$ hộp phân biệt, mọi khả năng đồng xác suất. Tìm kỳ vọng số hộp rỗng.

**31.** Một nhóm 50 người so sánh ngày sinh; giả sử ngày sinh độc lập, không có 29 tháng 2, v.v. Tìm kỳ vọng số cặp người trùng ngày sinh và kỳ vọng số ngày trong năm có ít nhất hai người của nhóm sinh.

**32.** Một nhóm $n\ge4$ người so sánh ngày sinh dưới các giả thiết thông thường. Gọi $I_{ij}$ là chỉ báo người $i,j$ trùng ngày sinh, với $i<j$. $I_{12}$ có độc lập với $I_{34}$ không? Với $I_{13}$ không? Toàn bộ các $I_{ij}$ có độc lập không?

**33.** Phân ngẫu nhiên 20 túi kẹo dẻo Haribo cho 20 sinh viên. Mỗi túi đến tay một sinh viên ngẫu nhiên, độc lập giữa các túi. Tìm trung bình tổng số túi ba sinh viên đầu nhận và trung bình số sinh viên nhận ít nhất một túi.

**34.** Mỗi người trong $n\ge2$ người ghi tên mình lên một phiếu, không ai trùng tên. Xáo phiếu trong mũ rồi mỗi người rút một phiếu, đều ngẫu nhiên ở từng bước và không hoàn lại. Tìm trung bình số người rút đúng tên mình.

**35.** Hai nhà nghiên cứu độc lập chọn mẫu ngẫu nhiên đơn giản từ quần thể cỡ $N$, kích thước mẫu lần lượt $m,n$; mỗi người rút không hoàn lại và mọi mẫu đúng cỡ đều đồng khả năng. Tìm kỳ vọng số phần tử chung của hai mẫu.

**36.** Trong $n$ lần tung đồng xu công bằng độc lập, kỳ vọng số lần xuất hiện liên tiếp mẫu HTH là bao nhiêu? Cho phép các lần xuất hiện chồng nhau; ví dụ HTHTH chứa hai lần xuất hiện chồng nhau.

**37.** Có bộ bài 52 lá đã xáo kỹ. Trung bình có bao nhiêu cặp lá kề nhau đều màu đỏ?

**38.** Có $n$ loại đồ chơi, mỗi lần thu thập một món đều ngẫu nhiên đều giữa $n$ loại. Kỳ vọng số loại khác nhau sau khi nhận đúng $t$ món là bao nhiêu? Giả sử chắc chắn nhận đủ $t$ món dù bộ sưu tập hoàn chỉnh sớm hơn.

**39.** Tòa nhà có $n$ tầng, đánh số $1,\ldots,n$. Ở tầng một, $k$ người vào thang máy đang trống và đi lên. Mỗi người quyết định độc lập muốn đến tầng nào trong $2,\ldots,n$ và bấm nút nếu chưa ai bấm. (a) Nếu các tầng có xác suất được chọn bằng nhau, tìm kỳ vọng số lần thang dừng ở các tầng $2,\ldots,n$. (b) Tổng quát hóa khi xác suất đến tầng $j$ là $p_j$; có thể để đáp án dạng tổng hữu hạn.

**40.** Có 100 dây giày trong hộp. Mỗi bước, chọn ngẫu nhiên hai đầu dây chưa buộc và buộc chúng với nhau. Kết quả là một dây dài hơn nếu hai đầu thuộc hai đoạn khác nhau, hoặc một vòng nếu chúng thuộc cùng đoạn. Tìm kỳ vọng số bước cho đến khi mọi dây đều thành vòng, và kỳ vọng số vòng cuối cùng. Đây là bài phỏng vấn nổi tiếng; có thể để đáp án thứ hai dạng tổng. Gợi ý: mỗi bước đặt chỉ báo có tạo vòng hay không; số đầu tự do giảm hai sau mỗi bước.

**41.** Chứng minh với mọi biến cố $A_1,\ldots,A_n$,

$$P(A_1\cap\cdots\cap A_n)
\ge\sum_{j=1}^{n}P(A_j)-n+1.$$

Gợi ý: Trước hết chứng minh bất đẳng thức tương tự cho các biến chỉ báo, bằng cách xét ý nghĩa khi $I_{A_1\cap\cdots\cap A_n}$ bằng 1 hoặc 0.

**42.** Có bộ bài 52 lá đã xáo kỹ. Bạn lật lần lượt từng lá, không hoàn lại. Kỳ vọng số lá không phải át xuất hiện trước lá át đầu tiên là bao nhiêu? Kỳ vọng số lá không phải át giữa lá át đầu và lá át thứ hai là bao nhiêu?

**43.** Bạn được kiểm tra “khả năng ngoại cảm”; giả sử bạn không có khả năng ấy. Một bộ bài chuẩn được xáo rồi chia úp từng lá. Ngay sau khi mỗi lá được chia, bạn gọi tên một lá bất kỳ để đoán. Gọi $X$ là số lần đoán đúng. (Xem Diaconis [6] để biết thêm về thống kê của phép kiểm tra ngoại cảm.)

(a) Giả sử bạn không được biết dự đoán của mình đúng hay sai. Chứng minh dù dùng chiến lược nào, kỳ vọng $X$ không đổi; tìm giá trị đó. Phương sai có thể khác nhiều giữa các chiến lược: chẳng hạn, luôn nói “át bích” cho phương sai 0. Gợi ý: biến chỉ báo.

(b) Giờ bạn được báo ngay sau mỗi lần đoán rằng đúng hay sai, nhưng không thấy lá bài. Dùng chiến lược: cứ gọi tên một lá cụ thể, chẳng hạn át bích, đến khi được báo đúng. Sau đó chuyển sang tên lá khác, chẳng hạn hai bích, và tiếp tục lặp lại cho tới khi đúng hoặc hết bài. Tính kỳ vọng $X$ và chứng minh nó rất gần $e-1$. Gợi ý: biến chỉ báo.

(c) Giờ có phản hồi đầy đủ: sau mỗi lần đoán, lá bài được lật cho thấy. Gọi chiến lược “ngớ ngẩn” nếu vẫn cho phép đoán một lá đã lật, chẳng hạn đoán át bích sau khi át bích đã xuất hiện. Chứng minh mọi chiến lược không ngớ ngẩn đều cho cùng kỳ vọng $X$; tìm giá trị ấy. Gợi ý: biến chỉ báo.

**44.** Cho $X\sim\operatorname{HGeom}(w,b,n)$. (a) Tìm $E\binom X2$ bằng suy luận, không tính toán phức tạp. (b) Dùng (a) tìm phương sai $X$. Kết quả cần là

$$\operatorname{Var}(X)=\frac{N-n}{N-1}npq,$$

với $N=w+b$, $p=w/N$, $q=1-p$.

**45.** Có $n$ phần thưởng trị giá lần lượt 1, 2, ..., $n$ đô la. Bạn chọn ngẫu nhiên $k$ phần thưởng không hoàn lại. Kỳ vọng tổng giá trị là bao nhiêu? Gợi ý: viết tổng dưới dạng $a_1I_1+\cdots+a_nI_n$, với $a_j$ là hằng số và $I_j$ là chỉ báo.

**46.** Chọn độc lập mười dây cung ngẫu nhiên của một đường tròn. Để tạo một dây, chọn độc lập hai điểm đều ngẫu nhiên trên đường tròn. Theo trực giác, “đều” nghĩa là không ưu tiên góc nào; chính xác, xác suất một cung tỉ lệ với độ dài của cung. Trung bình có bao nhiêu cặp dây cắt nhau? Gợi ý: với hai dây ngẫu nhiên, có thể tương đương chọn bốn điểm ngẫu nhiên độc lập trên đường tròn rồi ghép cặp ngẫu nhiên.

**47.** Một bảng băm lưu số điện thoại của $k$ người; số của mỗi người được lưu ở một vị trí đều ngẫu nhiên trong các vị trí đánh số $1,\ldots,n$ (xem Bài tập 25 Chương 1). Tìm kỳ vọng số vị trí không có số điện thoại, có đúng một số, và có hơn một số. Ba số kỳ vọng ấy có cộng thành $n$ không?

**48.** Tung đồng xu có xác suất ngửa $p$ tổng cộng $n$ lần. Dãy kết quả được chia thành các *đoạn liên tiếp cùng mặt*; ví dụ dãy HHHTTHTTT H (bỏ khoảng trắng) chia thành HHH, TT, H, TTT, H, có năm đoạn. Tìm kỳ vọng số đoạn. Gợi ý: trước tiên tìm kỳ vọng số lần tung, trừ lần đầu, có kết quả khác lần ngay trước.

**49.** Một quần thể có $N$ người, đánh số từ 1 đến $N$. Gọi $y_j$ là giá trị một đặc điểm bằng số của người thứ $j$, và trung bình quần thể là

$$\bar y=\frac1N\sum_{j=1}^{N}y_j.$$

Nếu $y_j$ là chiều cao thì $\bar y$ là chiều cao trung bình; nếu $y_j=1$ khi người ấy có một niềm tin nhất định và bằng 0 nếu không, thì $\bar y$ là tỉ lệ người có niềm tin ấy. Ở đây các $y_j$ được coi là hằng số, không phải biến ngẫu nhiên.

Một nhà nghiên cứu muốn biết $\bar y$ nhưng không thể đo mọi người. Họ lấy mẫu ngẫu nhiên cỡ $n$, chọn từng người đều ngẫu nhiên, không hoàn lại. Gọi $W_j$ là giá trị đặc điểm của người thứ $j$ trong mẫu. Dù các $y_j$ cố định, $W_j$ là biến ngẫu nhiên vì cách chọn mẫu ngẫu nhiên. Ước lượng tự nhiên là

$$\bar W=\frac1n\sum_{j=1}^{n}W_j.$$

Chứng minh $E(\bar W)=\bar y$ bằng hai cách: (a) tính trực tiếp $E(W_j)$ bằng đối xứng; (b) biểu diễn

$$\bar W=\frac1n\sum_{j=1}^{N}I_jy_j,$$

với $I_j$ là chỉ báo người thứ $j$ được chọn, rồi dùng tính tuyến tính và cây cầu cơ bản.

**50.** Xét thuật toán *sắp xếp nổi bọt* để đưa danh sách $n$ số phân biệt về thứ tự tăng. Ban đầu mọi thứ tự đều đồng khả năng. Thuật toán so sánh vị trí 1 và 2, đổi chỗ nếu cần; tiếp đến so sánh các số mới ở vị trí 2 và 3, đổi chỗ nếu cần; tiếp tục đến hết danh sách. Gọi đó là một *lượt quét*. Sau lượt đầu, số lớn nhất ở cuối, nên lượt thứ hai (nếu cần) chỉ xét $n-1$ vị trí đầu. Lượt thứ ba chỉ xét $n-2$ vị trí đầu, v.v. Dừng khi đã làm $n-1$ lượt hoặc một lượt không có đổi chỗ. Chẳng hạn, từ 53241 có bốn lượt quét, tổng 10 phép so sánh:

    53241 → 35241 → 32541 → 32451 → 32415
    32415 → 23415 → 23415 → 23145
    23145 → 23145 → 21345
    21345 → 12345

(a) Một *nghịch thế* là một cặp số sai thứ tự: 12345 không có nghịch thế, còn 53241 có tám. Tìm kỳ vọng số nghịch thế ban đầu.

(b) Chứng minh kỳ vọng số phép so sánh nằm giữa $\frac12\binom n2$ và $\binom n2$. Gợi ý: để tìm một chặn, xét số phép so sánh khi thực hiện đủ $n-1$ lượt; chặn kia dùng (a).

**51.** Một cầu thủ bóng rổ liên tục tập ném phạt. Các lần ném độc lập, xác suất trúng $p$. (a) Trong $n$ lần ném, kỳ vọng có bao nhiêu chuỗi bảy lần trúng liên tiếp? Một chuỗi chín lần trúng liên tiếp được tính là ba chuỗi bảy. (b) Cầu thủ ném đến khi lần đầu đạt bảy quả trúng liên tiếp. Gọi $X$ là số lần ném. Chứng minh $E(X)\le7/p^7$. Gợi ý: xét bảy lần đầu thành một khối, rồi bảy lần tiếp theo, v.v.

**52.** Bình có bóng đỏ, xanh lá và xanh lam. Rút ngẫu nhiên có hoàn lại: ghi màu rồi thả bóng trở lại. Xác suất rút ba màu lần lượt là $r,g,b$, với $r+g+b=1$. (a) Tìm kỳ vọng số bóng rút trước bóng đỏ đầu tiên, không tính bóng đỏ ấy. (b) Tìm kỳ vọng số màu khác nhau nhận được trước bóng đỏ đầu tiên. (c) Tìm xác suất ít nhất hai trong $n$ bóng rút là đỏ, khi biết ít nhất một bóng đỏ.

**53.** Các ứng viên $C_1,C_2,\ldots$ được phỏng vấn lần lượt; người phỏng vấn so sánh và cập nhật bảng xếp hạng từ tốt nhất đến kém nhất. Giả sử có vô hạn ứng viên khả dụng; với mọi $n$, các ứng viên $C_1,\ldots,C_n$ đồng khả năng xuất hiện theo mọi thứ tự; không có hòa hạng. Gọi $X$ là chỉ số ứng viên đầu tiên tốt hơn ứng viên đầu $C_1$. Nếu $C_2,C_3$ kém $C_1$ nhưng $C_4$ tốt hơn, thì $X=4$. Vì mọi $4!$ thứ tự của bốn ứng viên đầu đồng khả năng, $C_1$ cũng có thể là người tốt nhất trong bốn người đầu, khi đó $X>4$. Tìm $E(X)$, thời gian chờ trung bình để gặp người tốt hơn $C_1$. Gợi ý: tìm $P(X>n)$ bằng cách xét vị trí xếp hạng của $C_1$ trong $n$ ứng viên đầu, rồi dùng Định lý 4.4.8.

**54.** Mọi người lần lượt đến bữa tiệc và so sánh ngày sinh. Gọi $X$ là số người cần có đến khi lần đầu xuất hiện một cặp trùng ngày sinh. Giả sử 365 ngày đồng khả năng. Theo bài toán ngày sinh ở Chương 1, 23 người cho xác suất trùng 50,7%; với 22 người, xác suất dưới 50%. Điều này liên quan trung vị của $X$; bài tập sẽ tìm thêm kỳ vọng và so với 23.

(a) *Trung vị* của biến $Y$ là giá trị $m$ sao cho $P(Y\le m)\ge1/2$ và $P(Y\ge m)\ge1/2$. Đây cũng là trung vị của phân phối $Y$, hoàn toàn do CDF xác định. Mọi phân phối đều có trung vị, nhưng có thể không duy nhất. Chứng minh 23 là trung vị duy nhất của $X$.

(b) Chứng minh $X=I_1+\cdots+I_{366}$, trong đó $I_j$ là chỉ báo của biến cố $X\ge j$. Từ đó biểu diễn $E(X)$ theo các $p_j$ được định nghĩa bởi $p_1=p_2=1$ và, với $3\le j\le366$,

$$p_j=\left(1-\frac1{365}\right)
\left(1-\frac2{365}\right)\cdots
\left(1-\frac{j-2}{365}\right).$$

(c) Tính $E(X)$ bằng số. Trong R, lệnh <code>cumprod(1-(0:364)/365)</code> tạo vectơ $(p_2,\ldots,p_{366})$.

(d) Tìm phương sai $X$ theo các $p_j$, rồi tính bằng số. Gợi ý: $I_i^2$ và $I_iI_j$ khi $i<j$ bằng gì? Dùng điều đó để rút gọn

$$X^2=I_1^2+\cdots+I_{366}^2
+2\sum_{j=2}^{366}\sum_{i=1}^{j-1}I_iI_j.$$

*Lưu ý.* Bài toán ngày sinh còn ứng dụng trong tin học, chẳng hạn *tấn công ngày sinh* trong mật mã học. Nếu một năm có $n$ ngày và $n$ lớn, có thể chứng minh $E(X)\approx\sqrt{\pi n/2}$. Trong tập 1 của *The Art of Computer Programming*, Don Knuth đưa xấp xỉ tốt hơn:

$$E(X)\approx\sqrt{\frac{\pi n}{2}}
+\frac23+\sqrt{\frac{\pi}{288n}}.$$

**55.** Một khu rừng có $N$ con nai sừng tấm. Bắt ngẫu nhiên đơn giản $n$ con để đánh dấu, nghĩa là mọi tập $\binom Nn$ con đều đồng khả năng, rồi thả về và lấy mẫu mới. Phương pháp *bắt–đánh dấu–bắt lại* này được dùng rộng rãi trong sinh thái học. Nếu mẫu mới cũng có kích thước cố định và ngẫu nhiên đơn giản, số nai đánh dấu trong mẫu có phân phối Siêu bội.

Ở đây, thay vì kích thước mẫu cố định, bắt lại từng con không hoàn lại đến khi có $m$ con đã đánh dấu, với $m$ định trước và $1\le m\le n\le N$. Ưu điểm là tránh mẫu có quá ít nai đánh dấu, thậm chí bằng 0; nhược điểm là không biết trước kích thước mẫu.

(a) Tìm PMF của số nai *chưa* đánh dấu trong mẫu mới (gọi là $X$) và PMF của tổng số nai trong mẫu mới (gọi là $Y$).

(b) Dùng đối xứng, tính tuyến tính và biến chỉ báo tìm $EY$. Gợi ý: có thể giả sử tiếp tục bắt sau khi đã có $m$ con đánh dấu cho đến khi bắt hết $N$ con; hãy giải thích ngắn vì sao. Viết $X=X_1+\cdots+X_m$, trong đó $X_1$ là số nai chưa đánh dấu trước nai đánh dấu đầu tiên, $X_2$ là số nai chưa đánh dấu giữa nai đánh dấu thứ nhất và thứ hai, v.v. Tìm $EX_j$ bằng cách đặt chỉ báo tương ứng cho mỗi con chưa đánh dấu trong quần thể.

(c) Giả sử $m,n,N$ khiến $EY$ là số nguyên. Nếu lấy mẫu cố định cỡ $EY$ thay vì dừng khi có đúng $m$ con đánh dấu, kỳ vọng số nai đánh dấu trong mẫu là bao nhiêu? Với $n<N$, nó nhỏ hơn, bằng hay lớn hơn $m$?

#### LOTUS

**56.** Với $X\sim\operatorname{Pois}(\lambda)$, tìm $E(X!)$, tức giai thừa trung bình của $X$, nếu hữu hạn.

**57.** Với $X\sim\operatorname{Pois}(\lambda)$, tìm $E(2^X)$ nếu hữu hạn.

**58.** Với $X\sim\operatorname{Geom}(p)$, tìm $E(2^X)$ và $E(2^{-X})$ nếu hữu hạn. Với mỗi kỳ vọng, nêu rõ những giá trị $p$ khiến nó hữu hạn.

**59.** Cho $X\sim\operatorname{Geom}(p)$ và $t$ là hằng số. Tìm $E(e^{tX})$ theo $t$. Đây là *hàm sinh mômen*; Chương 6 sẽ nói nó hữu ích thế nào.

**60.** Số cá trong một hồ là biến $\operatorname{Pois}(\lambda)$. Lo hồ không có con nào, một nhà thống kê thả thêm một con. Gọi $Y$ là số cá sau đó, tức $Y=1+X$ với $X\sim\operatorname{Pois}(\lambda)$. (a) Tìm $E(Y^2)$. (b) Tìm $E(1/Y)$.

**61.** Cho $X\sim\operatorname{Pois}(\lambda)$, với $\lambda$ cố định nhưng chưa biết. Đặt $\theta=e^{-3\lambda}$ và muốn ước lượng $\theta$ từ dữ liệu quan sát $X$. Ước lượng viên là một hàm $g(X)$. *Độ chệch* của $g(X)$ là $E(g(X))-\theta$; ước lượng viên *không chệch* khi độ chệch bằng 0.

(a) Để ước lượng $\lambda$, chính $X$ là ước lượng viên không chệch. Tính độ chệch của $T=e^{-3X}$. Nó có không chệch khi ước lượng $\theta$ không?

(b) Chứng minh $g(X)=(-2)^X$ là ước lượng viên không chệch của $\theta$. Thực ra đây là ước lượng viên không chệch duy nhất cho $\theta$.

(c) Giải thích trực giác vì sao $g(X)$ vẫn là lựa chọn ngớ ngẩn. Tìm ước lượng viên $h(X)$ cho $\theta$ luôn tốt ít nhất bằng $g(X)$ và đôi khi tốt hơn hẳn, nghĩa là

$$|h(X)-\theta|\le|g(X)-\theta|,$$

với bất đẳng thức nghiêm trong một số trường hợp.

#### Xấp xỉ Poisson

**62.** Các lớp luật thường xếp chỗ cố định để thuận tiện cho phương pháp Socrates. Có 100 sinh viên luật năm thứ nhất, mỗi người học hai môn Luật bồi thường thiệt hại và Luật hợp đồng. Hai môn học cùng một giảng đường 100 ghế; chỗ ngồi ở mỗi môn được phân ngẫu nhiên đều và độc lập. (a) Tìm xác suất không ai ngồi cùng ghế ở hai môn, chính xác dưới dạng tổng. (b) Tìm xấp xỉ đơn giản nhưng chính xác cho xác suất ấy. (c) Tìm xấp xỉ đơn giản nhưng chính xác cho xác suất có ít nhất hai sinh viên ngồi cùng ghế ở cả hai môn.

**63.** Một nhóm $n\ge2$ người chơi “Ông già Noel bí mật”: mỗi người bỏ phiếu ghi tên mình vào mũ, rút ngẫu nhiên không hoàn lại một tên rồi mua quà cho người ấy. Họ quên khả năng rút đúng tên mình; một số người có thể phải tự mua quà cho mình (dù cũng có người thích tự chọn quà). (a) Tìm kỳ vọng số người rút đúng tên mình. (b) Tìm kỳ vọng số cặp người $A,B$ sao cho A rút tên B và B rút tên A; $A\ne B$ và không phân biệt thứ tự cặp. (c) Khi $n$ lớn, phân phối xấp xỉ của $X$ là gì? Nêu tham số. $P(X=0)$ tiến tới đâu khi $n\to\infty$?

**64.** Khảo sát một thành phố một triệu người. Lấy mẫu 1.000 người bằng cách chọn ngẫu nhiên đều có hoàn lại. Tìm xấp xỉ đơn giản, chính xác cho xác suất ít nhất một người được chọn hơn một lần (Bài tập 24 Chương 1 hỏi kết quả chính xác). Gợi ý: dùng chỉ báo, nhưng không nên tạo một chỉ báo cho từng người trong một triệu người vì phép tính sẽ rối. Có thể dùng $999\approx1000$.

**65.** Mười triệu người tham gia xổ số; mỗi người có xác suất trúng một phần mười triệu, độc lập. (a) Tìm xấp xỉ đơn giản, tốt cho PMF của số người trúng. (b) Chúc mừng, bạn trúng số! Tuy nhiên có thể có người trúng khác. Giả sử số người trúng ngoài bạn là $W\sim\operatorname{Pois}(1)$; nếu nhiều người trúng thì giải được trao ngẫu nhiên đều cho một người. Tìm xác suất bạn nhận giải, rút gọn.

**66.** Dùng xấp xỉ Poisson khảo sát các kiểu trùng hợp sau, theo các giả thiết quen thuộc của bài toán ngày sinh: 365 ngày đồng khả năng.

(a) Cần bao nhiêu người để có 50% khả năng ít nhất một người trùng ngày sinh với *bạn*?

(b) Cần bao nhiêu người để có 50% khả năng hai người vừa sinh cùng ngày vừa sinh cùng giờ, chẳng hạn cùng trong khoảng 14–15 giờ?

(c) Chỉ $1/24$ số cặp sinh cùng ngày cũng sinh cùng giờ; vì sao đáp án (b) không xấp xỉ $24\cdot23$? Giải thích bằng trực giác và tìm xấp xỉ đơn giản cho hệ số cần nhân vào số người để chuyển từ xác suất trùng ngày sinh $p$ sang xác suất trùng cả ngày lẫn giờ sinh $p$.

(d) Với 100 người, xác suất có ba người cùng ngày sinh là 64% (theo R với <code>pbirthday(100,classes=365,coincident=3)</code>). Hãy cho hai xấp xỉ Poisson: một dùng chỉ báo cho mỗi bộ ba người, một dùng chỉ báo cho mỗi ngày trong năm. Cách nào chính xác hơn?

**67.** Một giải cờ vua có 100 người chơi. Ở vòng đầu, họ được ghép cặp ngẫu nhiên để đấu 50 ván. Vòng hai lại ghép cặp ngẫu nhiên, độc lập với vòng đầu. Ở cả hai vòng, mọi cách ghép cặp đều đồng khả năng. Gọi $X$ là số người gặp cùng đối thủ trong cả hai vòng. (a) Tìm $E(X)$. (b) Giải thích vì sao $X$ không xấp xỉ Poisson. (c) Tìm xấp xỉ tốt cho $P(X=0)$ và $P(X=2)$ bằng cách xét số ván ở vòng hai tái hiện đúng cặp đấu ở vòng một.

#### *Chứng minh sự tồn tại

**68.** Mỗi người trong 111 người nêu năm bộ phim yêu thích từ danh sách 11 phim. (a) Alice và Bob là hai người trong số đó. Chỉ ở phần này, giả sử năm phim của Alice là tập ngẫu nhiên đều trong các tập năm phim, tương tự và độc lập với Bob. Tìm kỳ vọng số phim chung trong hai danh sách. (b) Chứng minh có hai phim được ít nhất 21 người cùng liệt kê là yêu thích.

**69.** Chu vi một đường tròn được tô mực đỏ và xanh lam, trong đó $2/3$ chiều dài là đỏ, $1/3$ là xanh. Chứng minh dù cách tô phức tạp đến đâu, có thể nội tiếp một hình vuông sao cho ít nhất ba trong bốn đỉnh chạm màu đỏ.

**70.** Một trăm sinh viên làm bài thi tám câu; mỗi câu có ít nhất 65 người trả lời đúng. Chứng minh có hai sinh viên mà khi gộp kết quả của họ, cả tám câu đều được ít nhất một người trả lời đúng.

**71.** Cho mười điểm được đánh dấu trên mặt phẳng và mười đồng xu hình tròn cùng bán kính. Chứng minh có thể đặt các đồng xu trên mặt phẳng, không chồng lên nhau, để che cả mười điểm. Gợi ý: xét cách lát mặt phẳng dạng tổ ong bằng các hình lục giác. Có thể dùng sự kiện hình học: diện tích đường tròn nội tiếp hình lục giác bằng $\pi/(2\sqrt3)>0{,}9$ lần diện tích lục giác.

**72.** Gọi $S$ là tập các chuỗi nhị phân độ dài $n$. Gọi $S$ là *đầy đủ bậc $k$* nếu với mọi chỉ số $1\le i_1<\cdots<i_k\le n$ và mọi chuỗi nhị phân $b_1\cdots b_k$ độ dài $k$, có chuỗi $s_1\cdots s_n\in S$ sao cho $s_{i_1}\cdots s_{i_k}=b_1\cdots b_k$. Chẳng hạn, với $n=3$, tập $S=\{001,010,011,100,101,110\}$ đầy đủ bậc 2 vì mọi mẫu nhị phân độ dài 2 đều xuất hiện ở bất kỳ hai vị trí nào. Chứng minh nếu

$$\binom nk\,2^k(1-2^{-k})^m<1,$$

thì tồn tại tập đầy đủ bậc $k$ có không quá $m$ phần tử.

#### Bài tập tổng hợp

**73.** Một tin tặc đoán ngẫu nhiên mật khẩu để vào một trang web. Có $m$ mật khẩu khả dĩ. (a) Nếu đoán đều ngẫu nhiên có hoàn lại, trung bình cần bao nhiêu lần đến khi đúng, tính cả lần đúng? (b) Nếu đoán ngẫu nhiên không hoàn lại thì sao? Gợi ý: dùng đối xứng để tìm PMF số lần đoán. (c) Chứng minh đáp án (a) lớn hơn (b), trừ trường hợp suy biến $m=1$, và giải thích trực giác. (d) Nếu trang khóa tài khoản sau $n$ lần đoán sai, nên tin tặc đoán được nhiều nhất $n$ lần, hãy tìm PMF số lần đoán thực hiện cho cả trường hợp có và không hoàn lại.

**74.** Tung xúc xắc công bằng 20 mặt đến khi người chơi quyết định dừng; họ nhận số đô la bằng giá trị ở lần gieo cuối. Người chơi quyết định trước rằng sẽ gieo đến khi ra ít nhất $m$, với $m$ nguyên cố định từ 1 đến 20. (a) Kỳ vọng số lần gieo là bao nhiêu? Hãy rút gọn. (b) Kỳ vọng căn bậc hai của số lần gieo là bao nhiêu? Có thể để dạng tổng.

**75.** Chia 360 người thành 120 đội, mỗi đội ba người; không xét thứ tự đội hay thứ tự trong đội. (a) Có bao nhiêu cách chia? (b) Nhóm gồm 180 cặp vợ chồng. Chọn đều ngẫu nhiên một cách chia. Kỳ vọng số đội có một cặp vợ chồng là bao nhiêu?

**76.** Người đánh bạc de Méré hỏi Pascal: dễ có ít nhất một lần ra mặt sáu trong bốn lần gieo một xúc xắc, hay dễ có ít nhất một lần cả hai xúc xắc đều ra sáu trong 24 lần gieo một cặp xúc xắc? Tiếp tục mẫu hình ấy, giả sử gieo đồng thời $n$ xúc xắc công bằng tổng cộng $4\cdot6^{n-1}$ lần. (a) Kỳ vọng số lần “tất cả đều sáu” là bao nhiêu? (b) Với $n$ lớn, tìm xấp xỉ đơn giản, chính xác cho xác suất có ít nhất một lần “tất cả đều sáu”, biểu diễn theo $e$ nhưng không theo $n$. (c) de Méré thấy gieo lại nhiều xúc xắc phiền phức. Sau lần gieo đầu bình thường, ở mỗi lần tiếp theo ông giữ nguyên cấu hình cũ với xác suất $6/7$ và gieo lại với xác suất $1/7$. Chẳng hạn, với $n=3$, nếu lần thứ bảy là $(3,1,4)$ thì lần thứ tám giữ kết quả ấy với xác suất $6/7$, còn với xác suất $1/7$ cho kết quả ngẫu nhiên mới. Kỳ vọng số lần “tất cả đều sáu” giữ nguyên, tăng hay giảm so với (a)? Giải thích ngắn và rõ.

**77.** Năm người vừa trúng giải 100 đô la và quyết định chia số tiền ấy theo đơn vị đô la nguyên. Ví dụ, người thứ nhất nhận 50 đô và người thứ hai 10 đô khác cách chia ngược lại. (a) Có bao nhiêu cách chia nếu mỗi người nhận ít nhất 10 đô? (b) Chọn ngẫu nhiên đều trong các cách chia ở (a). Kỳ vọng số tiền người thứ nhất nhận là bao nhiêu? (c) Gọi $A_j$ là biến cố người thứ $j$ nhận nhiều hơn người thứ nhất, với $2\le j\le5$. $A_2,A_3$ có độc lập không?

**78.** Máy nghe nhạc của Joe có 500 bài hát khác nhau, thuộc 50 album, mỗi album 10 bài. Anh nghe 11 bài được chọn ngẫu nhiên độc lập, mọi bài đồng khả năng nên có thể lặp. (a) Tìm PMF số bài trong 11 bài đến từ album yêu thích của anh. (b) Xác suất có ít nhất hai bài trong 11 bài thuộc cùng album là bao nhiêu? (c) Một cặp bài được gọi là khớp nếu cùng album. Nếu bài thứ nhất, thứ ba và thứ bảy cùng album thì tạo ba cặp khớp. Trung bình có bao nhiêu cặp khớp trong 11 bài?

**79.** Mỗi ngày xổ số Mass Cash ở Massachusetts chọn ngẫu nhiên không hoàn lại năm số từ 1 đến 35. (a) Khi chơi, tìm xác suất đoán đúng chính xác ba số nếu biết đã đoán đúng ít nhất một số. (b) Cho biểu thức chính xác cho kỳ vọng số ngày cần để mọi kết quả xổ số trong $\binom{35}5$ khả năng đều đã từng xuất hiện. (c) Xấp xỉ xác suất sau 50 ngày, mọi số từ 1 đến 35 đều đã được chọn ít nhất một lần.

**80.** Thượng viện Hoa Kỳ có 100 thượng nghị sĩ, mỗi bang trong 50 bang có hai người. Có $d$ người thuộc Đảng Dân chủ. Chọn ngẫu nhiên đều một ủy ban gồm $c$ thượng nghị sĩ. (a) Tìm kỳ vọng số thành viên Dân chủ trong ủy ban. (b) Tìm kỳ vọng số bang có ít nhất một đại diện trong ủy ban. (c) Tìm kỳ vọng số bang có cả hai thượng nghị sĩ trong ủy ban.

**81.** Một trường có $g$ môn tốt và $b$ môn tệ, với $g,b$ nguyên dương. Alice thử ngẫu nhiên từng môn không hoàn lại đến khi gặp môn tốt. (a) Tìm kỳ vọng số môn tệ cô đã thử trước môn tốt đầu tiên, dưới dạng đơn giản theo $g,b$. (b) Đáp án (a) nhỏ hơn, bằng hay lớn hơn $b/g$? Giải thích bằng tính chất phân phối Hình học.

**82.** Kiểm định tổng thứ hạng Wilcoxon được dùng rộng rãi để đánh giá hai nhóm quan sát có cùng phân phối không. Nhóm 1 gồm các biến i.i.d. $X_1,\ldots,X_m$ có CDF $F$; nhóm 2 gồm các biến i.i.d. $Y_1,\ldots,Y_n$ có CDF $G$; tất cả độc lập. Giả sử xác suất hai quan sát bằng nhau là 0, như với phân phối liên tục.

Sau khi quan sát $m+n$ giá trị, xếp chúng tăng dần và cho thứ hạng từ 1 đến $m+n$: nhỏ nhất hạng 1, tiếp theo hạng 2, v.v. Gọi $R_j$ là thứ hạng của $X_j$ trong toàn bộ quan sát, và $R=\sum_{j=1}^{m}R_j$ là tổng hạng nhóm 1. Trực giác: $R$ rất lớn gợi ý nhóm 1 thường có giá trị lớn hơn nhóm 2; $R$ rất nhỏ gợi ý ngược lại. Muốn biết “rất lớn” hay “rất nhỏ” chính xác, cần nghiên cứu phân phối $R$.

(a) Giả thuyết không là $F=G$. Chứng minh khi nó đúng, $E(R)=m(m+n+1)/2$.

(b) *Lực kiểm định* đo mức hiệu quả nhận ra giả thuyết không sai. Để nghiên cứu lực của Wilcoxon, xét $F,G$ bất kỳ. Đặt $p=P(X_1>Y_1)$. Tìm $E(R)$ theo $m,n,p$. Gợi ý: viết $R_j$ thành tổng chỉ báo $X_j$ lớn hơn các biến khác.

**83.** Nhà vật lý Richard Feynman của Caltech và hai biên tập viên của *The Feynman Lectures on Physics*, Michael Gottlieb và Ralph Leighton, đặt bài toán chọn món ở nhà hàng. Bạn định ăn $m$ bữa tại một nhà hàng chưa từng tới; mỗi bữa gọi một món. Thực đơn có $n\ge m$ món. Nếu đã thử tất cả, bạn sẽ xếp hạng chúng từ 1 (ít thích nhất) đến $n$ (thích nhất). Nếu biết món thích nhất, bạn sẵn lòng luôn gọi món ấy vì không bao giờ chán.

Trước khi ăn, thứ hạng hoàn toàn chưa biết. Sau khi thử vài món, bạn xếp hạng được chúng với nhau, nhưng không biết so với các món chưa thử. Vậy phải cân bằng giữa *khám phá* (thử món mới) và *tận dụng* (gọi món thích nhất đã biết).

Chiến lược tự nhiên có hai giai đoạn: trong $k$ bữa đầu, mỗi lần thử một món mới; trong $m-k$ bữa sau, luôn gọi món ngon nhất đã thử. Mục tiêu là tối đa kỳ vọng tổng thứ hạng *thật* của các món đã ăn, tính theo thứ hạng 1 đến $n$ nếu bạn thử đủ mọi món. Chứng minh lựa chọn tối ưu là

$$k=\sqrt{2(m+1)}-1,$$

hoặc làm tròn lên hay xuống thành số nguyên nếu cần. Thực hiện theo các bước:

(a) Gọi $X$ là thứ hạng món ngon nhất tìm được trong giai đoạn khám phá. Tìm kỳ vọng tổng thứ hạng các món đã ăn theo $E(X)$.

(b) Tìm PMF của $X$ dưới dạng đơn giản dùng hệ số nhị thức.

(c) Chứng minh $E(X)=k(n+1)/(k+1)$. Gợi ý: dùng Ví dụ 1.5.2 về đội trưởng và Bài tập 18 Chương 1 về đồng nhất thức gậy khúc côn cầu.

(d) Dùng giải tích tìm $k$ tối ưu.

*(Trang PDF 212 không có văn bản.)*

## Chương 5. Biến ngẫu nhiên liên tục

Đến đây ta đã làm việc với biến ngẫu nhiên rời rạc, có thể liệt kê các giá trị khả dĩ. Chương này bàn về biến ngẫu nhiên liên tục, có thể nhận mọi giá trị thực trong một khoảng, kể cả khoảng dài vô hạn như $(0,\infty)$ hoặc toàn trục số. Trước tiên, ta xét tính chất tổng quát. Sau đó giới thiệu ba phân phối liên tục nổi tiếng: Đều, Chuẩn và Mũ. Chúng vừa có câu chuyện quan trọng riêng, vừa là thành phần để xây dựng nhiều phân phối hữu ích khác.

### 5.1 Hàm mật độ xác suất

*Hình 5.1 (trang PDF 213).* Biến rời rạc và liên tục: bên trái, CDF của biến rời rạc nhảy tại từng điểm thuộc miền giá trị khả dĩ; bên phải, CDF của biến liên tục tăng trơn.

Với biến rời rạc, CDF nhảy ở mọi điểm thuộc miền giá trị khả dĩ và nằm ngang ở nơi khác. Ngược lại, với biến liên tục, CDF tăng trơn; Hình 5.1 so sánh hai loại.

**Định nghĩa 5.1.1 (Biến ngẫu nhiên liên tục).** Một biến ngẫu nhiên có *phân phối liên tục* nếu CDF của nó khả vi. Ta cũng cho phép các điểm đầu mút (hoặc hữu hạn điểm) mà CDF liên tục nhưng không khả vi, miễn là nó khả vi ở mọi nơi khác. Biến mang phân phối liên tục được gọi là biến ngẫu nhiên liên tục.

Với biến rời rạc, CDF khó thao tác vì có bước nhảy; đạo hàm gần như vô dụng vì không xác định tại bước nhảy và bằng 0 ở các nơi khác. Với biến liên tục, CDF thường thuận tiện và đạo hàm của nó rất hữu ích, gọi là *hàm mật độ xác suất*.

**Định nghĩa 5.1.2 (Hàm mật độ xác suất).** Với biến liên tục $X$ có CDF $F$, hàm mật độ xác suất (PDF) của $X$ là đạo hàm $f(x)=F'(x)$. Miền giá trị khả dĩ của $X$ và phân phối của nó là tập các $x$ mà $f(x)>0$.

Một khác biệt quan trọng: nếu $X$ liên tục thì $P(X=x)=0$ với mọi $x$. Xác suất ấy bằng độ cao bước nhảy CDF tại $x$, mà CDF của $X$ không có bước nhảy. PMF của biến liên tục sẽ bằng 0 khắp nơi, nên ta dùng PDF.

PDF tương tự PMF ở nhiều mặt, nhưng có khác biệt mấu chốt: $f(x)$ *không phải* xác suất và có thể lớn hơn 1. Muốn có xác suất, phải lấy tích phân PDF. Định lý cơ bản của giải tích cho cách đi từ PDF trở lại CDF.

**Mệnh đề 5.1.3 (Từ PDF sang CDF).** Nếu $X$ liên tục có PDF $f$, thì

$$F(x)=\int_{-\infty}^{x}f(t)\,dt.$$

**Chứng minh.** Theo định nghĩa, $F$ là nguyên hàm của $f$. Theo định lý cơ bản của giải tích,

$$\int_{-\infty}^{x}f(t)\,dt
=F(x)-F(-\infty)=F(x).\quad\Box$$

Kết quả này tương tự cách tính CDF rời rạc bằng cách cộng PMF tại các giá trị không vượt $x$. Ở đây ta tích phân PDF đến $x$, nên CDF là diện tích tích lũy dưới đường mật độ. Có thể chuyển qua lại giữa PDF và CDF bằng tích phân, đạo hàm; vì vậy cả hai chứa đầy đủ thông tin phân phối liên tục.

Vì PDF xác định phân phối, ta có thể dùng nó tìm xác suất $X$ rơi trong khoảng $(a,b)$. Một tính chất tiện lợi: đưa các đầu mút vào hay bỏ đi không đổi xác suất vì mỗi đầu mút có xác suất 0:

$$P(a<X<b)=P(a<X\le b)=P(a\le X<b)=P(a\le X\le b).$$

**Lưu ý 5.1.4 (Có hay không có đầu mút).** Với biến liên tục, ta có thể thoải mái đưa đầu mút vào hoặc bỏ đi. Với biến rời rạc thì phải thận trọng.

Theo định nghĩa CDF và định lý cơ bản của giải tích,

$$P(a<X\le b)=F(b)-F(a)=\int_a^b f(x)\,dx.$$

Vậy để tính xác suất $X$ trong $(a,b]$ (hay ba biến thể khác về đầu mút), chỉ cần tích phân PDF từ $a$ đến $b$. Tổng quát hơn, với vùng $A\subseteq\mathbb R$,

$$P(X\in A)=\int_A f(x)\,dx.$$

Tóm lại: **muốn có xác suất, tích phân PDF trên vùng thích hợp**.

PMF hợp lệ không âm và có tổng 1; PDF hợp lệ không âm và có tích phân 1.

**Định lý 5.1.5 (PDF hợp lệ).** PDF $f$ của biến liên tục phải thỏa $f(x)\ge0$ và

$$\int_{-\infty}^{\infty}f(x)\,dx=1.$$

**Chứng minh.** Xác suất không âm. Nếu $f(x_0)<0$, tích phân trên vùng nhỏ quanh $x_0$ sẽ cho xác suất âm. Hoặc xem $f(x_0)$ là độ dốc CDF: nếu âm thì CDF giảm tại đó, điều không được phép. Tích phân trên toàn trục là xác suất $X$ nhận một giá trị thực nào đó, bằng 1. □

Ngược lại, mọi hàm $f$ thỏa hai điều kiện đều là PDF của một biến ngẫu nhiên. Tích phân nó theo Mệnh đề 5.1.3 cho hàm $F$ thỏa tính chất CDF; sau đó có thể dùng một phiên bản của *Tính phổ quát của phân phối Đều*, khái niệm chính ở Mục 5.3, để tạo biến có CDF $F$.

Sau đây là hai ví dụ PDF cụ thể của phân phối Logistic và Rayleigh. Ta chưa bàn câu chuyện của chúng; chúng giúp làm quen với PDF.

**Ví dụ 5.1.6 (Logistic).** Phân phối Logistic có CDF

$$F(x)=\frac{e^x}{1+e^x},\qquad x\in\mathbb R.$$

Lấy đạo hàm cho PDF

$$f(x)=\frac{e^x}{(1+e^x)^2},\qquad x\in\mathbb R.$$

Với $X\sim\operatorname{Logistic}$,

$$P(-2<X<2)=\int_{-2}^{2}\frac{e^x}{(1+e^x)^2}\,dx
=F(2)-F(-2)\approx0{,}76.$$

Tích phân dễ tính vì đã biết $F$ là nguyên hàm. Nếu chưa biết, đặt $u=1+e^x$, $du=e^x\,dx$:

$$\int_{-2}^{2}\frac{e^x}{(1+e^x)^2}\,dx
=\int_{1+e^{-2}}^{1+e^2}\frac1{u^2}\,du
=\left[-\frac1u\right]_{1+e^{-2}}^{1+e^2}
\approx0{,}76.$$

Hình 5.2 vẽ PDF bên trái, CDF bên phải. Trên PDF, $P(-2<X<2)$ là diện tích tô bóng; trên CDF là độ cao ngoặc đánh dấu. Có thể kiểm tra các tính chất PDF và CDF hợp lệ.

*Hình 5.2 (trang PDF 216).* PDF và CDF Logistic; xác suất $P(-2<X<2)$ được biểu diễn bằng diện tích dưới PDF và độ cao đánh dấu trên CDF. ◇

**Ví dụ 5.1.7 (Rayleigh).** Phân phối Rayleigh có CDF

$$F(x)=1-e^{-x^2/2},\qquad x>0.$$

Lấy đạo hàm cho PDF $f(x)=xe^{-x^2/2}$ khi $x>0$. Với $x\le0$, cả CDF và PDF đều bằng 0. Nếu $X\sim\operatorname{Rayleigh}$, để tìm $P(X>2)$ ta tích phân PDF từ 2 đến vô cực. Có thể đặt $u=-x^2/2$, nhưng CDF đã có dạng thuận tiện:

$$P(X>2)=\int_2^\infty xe^{-x^2/2}\,dx
=1-F(2)\approx0{,}14.$$

Hình 5.3 vẽ PDF và CDF Rayleigh. Một lần nữa, xác suất được biểu diễn bằng diện tích tô bóng dưới PDF và độ cao trên CDF. ◇

*Hình 5.3 (trang PDF 217).* PDF và CDF Rayleigh; $P(X>2)$ là diện tích dưới PDF từ 2 trở đi, cũng là chiều cao được đánh dấu trên CDF.

Dù độ cao PDF tại $x$ không phải xác suất, nó liên hệ chặt với xác suất rơi trong một khoảng rất nhỏ quanh $x$.

**Trực giác 5.1.8.** Cho $F,f$ lần lượt là CDF và PDF của biến liên tục $X$. Như đã nói, $f(x)$ không phải xác suất: có thể $f(3)>1$, trong khi $P(X=3)=0$. Nhưng xét xác suất $X$ *rất gần* 3 giúp giải thích $f(3)$. Khoảng rất nhỏ độ dài $\varepsilon$ và tâm 3 có xác suất xấp xỉ $f(3)\varepsilon$:

$$P(3-\varepsilon/2<X<3+\varepsilon/2)
=\int_{3-\varepsilon/2}^{3+\varepsilon/2}f(x)\,dx
\approx f(3)\varepsilon,$$

vì trên khoảng nhỏ đó $f$ gần như hằng bằng $f(3)$. Tổng quát, có thể hiểu $f(x)\,dx$ là xác suất $X$ nằm trong khoảng vô cùng nhỏ độ dài $dx$ quanh $x$.

Trong ứng dụng, $X$ thường có đơn vị đo như độ dài, thời gian, diện tích hoặc khối lượng. Kiểm tra đơn vị giúp biết đáp án có hợp lý không. Giả sử $X$ là độ dài tính bằng xăng ti mét (cm). Khi ấy $f(x)=dF(x)/dx$ có đơn vị xác suất trên mỗi cm, giải thích tên *mật độ xác suất*. Xác suất không có đơn vị, nên $f(x)$ có đơn vị cm$^{-1}$. Muốn thu lại xác suất phải nhân với một độ dài; trong tích phân như $\int_0^5 f(x)\,dx$, vai trò đó thuộc về $dx$ thường bị xem nhẹ. ◇

Định nghĩa kỳ vọng cho biến liên tục giống biến rời rạc: thay tổng bằng tích phân và PMF bằng PDF.

**Định nghĩa 5.1.9 (Kỳ vọng biến liên tục).** Với biến liên tục $X$ có PDF $f$,

$$E(X)=\int_{-\infty}^{\infty}x f(x)\,dx.$$

Như trường hợp rời rạc, kỳ vọng có thể tồn tại hoặc không. Để khỏi lặp đi lặp lại cụm “nếu tồn tại”, ta thường hiểu ngầm điều đó khi chưa chứng minh kỳ vọng tồn tại.

Tích phân viết trên toàn trục, nhưng nếu miền giá trị khả dĩ nhỏ hơn thì chỉ cần tích phân trên miền ấy. Đơn vị cũng hợp lý: nếu $X$ đo bằng cm thì $xf(x)\,dx$ có đơn vị cm $\cdot$ cm$^{-1}\cdot$ cm = cm, nên $E(X)$ cũng là cm.

Kỳ vọng vẫn được hiểu là trọng tâm. Hình 5.4 dùng PDF Rayleigh minh họa: kỳ vọng là điểm cân bằng của PDF, như trường hợp PMF rời rạc. Tính tuyến tính vẫn đúng với biến liên tục (xem Ví dụ 7.2.4). LOTUS cũng đúng khi thay tổng và PMF bằng tích phân và PDF:

**Định lý 5.1.10 (LOTUS cho biến liên tục).** Nếu $X$ có PDF $f$ và $g:\mathbb R\to\mathbb R$, thì

$$E(g(X))=\int_{-\infty}^{\infty}g(x)f(x)\,dx.$$

Ta đã có đủ công cụ để nghiên cứu các phân phối có tên trong chương này, bắt đầu bằng phân phối Đều.

*Hình 5.4 (trang PDF 219).* Kỳ vọng của biến liên tục là điểm cân bằng của PDF.

### 5.2 Phân phối Đều

Theo trực giác, biến Đều trên khoảng $(a,b)$ là một số hoàn toàn ngẫu nhiên giữa $a$ và $b$. Ta diễn đạt “hoàn toàn ngẫu nhiên” bằng cách yêu cầu PDF không đổi trên khoảng.

**Định nghĩa 5.2.1 (Phân phối Đều).** Biến liên tục $U$ có phân phối Đều trên $(a,b)$ nếu PDF là

$$f(x)=
\begin{cases}
\dfrac1{b-a},&a<x<b,\\
0,&\text{ngoài khoảng ấy}.
\end{cases}$$

Ký hiệu $U\sim\operatorname{Unif}(a,b)$. Đây là PDF hợp lệ vì diện tích dưới đường mật độ là diện tích hình chữ nhật rộng $b-a$, cao $1/(b-a)$. CDF là diện tích tích lũy:

$$F(x)=
\begin{cases}
0,&x\le a,\\
\dfrac{x-a}{b-a},&a<x<b,\\
1,&x\ge b.
\end{cases}$$

Phân phối thường dùng nhất là $\operatorname{Unif}(0,1)$, còn gọi là *Đều chuẩn*. Trên $0<x<1$, PDF bằng 1 và CDF bằng $x$. Hình 5.5 vẽ hai hàm này. Với $\operatorname{Unif}(a,b)$ tổng quát, PDF hằng trên $(a,b)$, CDF tăng tuyến tính từ 0 đến 1 khi $x$ đi từ $a$ đến $b$.

*Hình 5.5 (trang PDF 220).* PDF và CDF của $\operatorname{Unif}(0,1)$.

Với phân phối Đều, xác suất tỉ lệ với độ dài.

**Mệnh đề 5.2.2.** Nếu $U\sim\operatorname{Unif}(a,b)$ và $(c,d)\subseteq(a,b)$ có độ dài $\ell=d-c$, thì $P(c<U<d)$ tỉ lệ với $\ell$. Khoảng dài gấp đôi có xác suất gấp đôi; các khoảng bằng nhau có xác suất bằng nhau.

**Chứng minh.** PDF hằng $1/(b-a)$ trên $(a,b)$, nên diện tích dưới PDF từ $c$ đến $d$ là $\ell/(b-a)$, một hằng số nhân $\ell$. □

Đây là tính chất rất riêng của phân phối Đều; với phân phối khác, có những khoảng bằng độ dài nhưng khác xác suất. Ngay cả sau khi điều kiện hóa rằng biến Đều nằm trong một khoảng con, phân phối trong khoảng con vẫn Đều.

**Mệnh đề 5.2.3.** Nếu $U\sim\operatorname{Unif}(a,b)$ và $(c,d)\subseteq(a,b)$, thì phân phối có điều kiện của $U$ khi biết $U\in(c,d)$ là $\operatorname{Unif}(c,d)$.

**Chứng minh.** Với $c<u<d$,

$$P(U\le u\mid U\in(c,d))
=\frac{P(U\in(c,u])}{P(U\in(c,d))}
=\frac{u-c}{d-c}.$$

CDF có điều kiện bằng 0 khi $u\le c$ và bằng 1 khi $u\ge d$, nên đúng là CDF Đều trên $(c,d)$. □

**Ví dụ 5.2.4.** Với $U\sim\operatorname{Unif}(0,1)$, miền giá trị có độ dài 1 nên xác suất bằng độ dài: $P(U\in(0,0{,}3))=0{,}3$, và các khoảng $(0{,}3,0{,}6)$, $(0{,}4,0{,}7)$ hay bất kỳ khoảng con độ dài $0{,}3$ cũng vậy.

Giả sử biết $U\in(0{,}4,0{,}7)$. Phân phối có điều kiện là $\operatorname{Unif}(0{,}4,0{,}7)$, nên xác suất có điều kiện $U\in(0{,}4,0{,}6)$ bằng $2/3$: độ dài khoảng đầu bằng $2/3$ độ dài khoảng điều kiện. Xác suất có điều kiện $U\in(0,0{,}6)$ cũng bằng $2/3$, vì các điểm bên trái $0{,}4$ bị loại sau khi điều kiện hóa. ◇

Tiếp theo, suy ra trung bình và phương sai của $U\sim\operatorname{Unif}(a,b)$. Kỳ vọng có trực giác rõ: PDF hằng nên điểm cân bằng là trung điểm. Định nghĩa cho đúng kết quả:

$$E(U)=\int_a^b x\frac1{b-a}\,dx
=\frac{b^2-a^2}{2(b-a)}
=\frac{a+b}{2}.$$

Để tính phương sai, dùng LOTUS:

$$E(U^2)=\int_a^b x^2\frac1{b-a}\,dx
=\frac{b^3-a^3}{3(b-a)}.$$

Vậy

$$\operatorname{Var}(U)
=\frac{b^3-a^3}{3(b-a)}
-\left(\frac{a+b}{2}\right)^2
=\frac{(b-a)^2}{12},$$

sau khi tách $b^3-a^3=(b-a)(a^2+ab+b^2)$ và rút gọn.

Cách tính trên không quá khó, nhưng có cách dễ hơn dùng *biến đổi vị trí–tỉ lệ*. Dịch và nhân tỉ lệ một biến Đều lại cho biến Đều: nếu $X\sim\operatorname{Unif}(1,2)$ thì $X+5\sim\operatorname{Unif}(6,7)$, $2X\sim\operatorname{Unif}(2,4)$ và $2X+5\sim\operatorname{Unif}(7,9)$. Dịch là thay đổi vị trí, nhân là thay đổi tỉ lệ.

**Định nghĩa 5.2.5 (Biến đổi vị trí–tỉ lệ).** Nếu $X$ là biến ngẫu nhiên, $Y=\sigma X+\mu$ với các hằng $\sigma>0,\mu$, thì $Y$ là biến đổi vị trí–tỉ lệ của $X$. $\mu$ điều khiển vị trí, $\sigma$ điều khiển tỉ lệ.

**Lưu ý 5.2.6.** Nếu $X\sim\operatorname{Unif}(a,b)$ và $Y=cX+d$ với $c>0$, tính Đều được giữ: $Y\sim\operatorname{Unif}(ca+d,cb+d)$. Nếu $Y$ là biến đổi phi tuyến của $X$, nói chung $Y$ không Đều. Chẳng hạn, với $0\le a<b$, biến $Y=X^2$ có miền giá trị $(a^2,b^2)$ nhưng không Đều trên đó. Chương 8 nghiên cứu kỹ các phép biến đổi biến ngẫu nhiên.

Khi nghiên cứu họ Đều, chiến lược hữu ích là bắt đầu bằng phân phối đơn giản nhất rồi dùng biến đổi vị trí–tỉ lệ cho trường hợp tổng quát. Với $U\sim\operatorname{Unif}(0,1)$, PDF bằng 1 trên $(0,1)$, nên

$$E(U)=\int_0^1x\,dx=\frac12,\qquad
E(U^2)=\int_0^1x^2\,dx=\frac13,\qquad
\operatorname{Var}(U)=\frac13-\frac14=\frac1{12}.$$

Để chuyển sang $\operatorname{Unif}(a,b)$, nhân $U$ với $b-a$ rồi cộng $a$:

$$\widetilde U=a+(b-a)U\sim\operatorname{Unif}(a,b).$$

Tính tuyến tính của kỳ vọng cho

$$E(\widetilde U)=a+(b-a)E(U)
=a+\frac{b-a}{2}
=\frac{a+b}{2}.$$

Cộng hằng không đổi phương sai, nhân hằng đưa ra bình phương, nên

$$\operatorname{Var}(\widetilde U)
=(b-a)^2\operatorname{Var}(U)
=\frac{(b-a)^2}{12}.$$

Hai kết quả khớp phép tính trực tiếp. Phương pháp vị trí–tỉ lệ dùng được cho mọi họ phân phối mà việc dịch, nhân một biến trong họ lại cho biến cùng họ. Nó không dùng được cho các họ rời rạc với miền giá trị cố định: nếu $X\sim\operatorname{Bin}(n,p)$, thì $X+4$ không thể nhận $0,1,2,3$, còn $2X$ chỉ nhận số chẵn. Cả hai không còn là biến Nhị thức, vốn phải có khả năng nhận mọi số nguyên từ 0 đến một chặn trên.

**Lưu ý 5.2.7 (Cẩn thận với “ma thuật cảm ứng”).** Khi dùng biến đổi vị trí–tỉ lệ, hãy dịch và nhân *biến ngẫu nhiên*, không phải PDF của nó. Nhầm hai đối tượng là lỗi “ma thuật cảm ứng” (Lưu ý 3.7.7) và sẽ cho PDF không hợp lệ. Ví dụ, nếu $U\sim\operatorname{Unif}(0,1)$ thì PDF $f$ bằng 1 trên $(0,1)$, bằng 0 ở nơi khác. Biến $3U+1\sim\operatorname{Unif}(1,4)$, nhưng hàm $3f+1$ bằng 4 trên $(0,1)$ và bằng 1 ở nơi khác; nó không phải PDF hợp lệ vì tích phân không bằng 1.

### 5.3 Tính phổ quát của phân phối Đều

Phân phối Đều có tính chất đáng chú ý: từ một biến $\operatorname{Unif}(0,1)$, ta xây dựng được biến mang bất kỳ phân phối liên tục mong muốn. Ngược lại, từ biến có phân phối liên tục bất kỳ, ta tạo được biến $\operatorname{Unif}(0,1)$. Vì vậy phân phối Đều là điểm xuất phát phổ quát. Tính chất này còn mang nhiều tên: *biến đổi tích phân xác suất*, *lấy mẫu bằng biến đổi nghịch đảo*, *biến đổi phân vị*, và thậm chí *định lý cơ bản của mô phỏng*.

Để chứng minh đơn giản, trước mắt ta giả sử CDF mong muốn có hàm nghịch đảo. Tổng quát hơn, những ý tương tự cho phép mô phỏng biến với bất kỳ CDF hợp lệ nào theo Định lý 3.6.3 bằng một hàm của biến $\operatorname{Unif}(0,1)$.

**Định lý 5.3.1 (Tính phổ quát của phân phối Đều).** Cho CDF $F$ liên tục và tăng nghiêm ngặt trên miền giá trị khả dĩ của phân phối. Khi ấy hàm nghịch đảo $F^{-1}:(0,1)\to\mathbb R$ tồn tại và:

1. Nếu $U\sim\operatorname{Unif}(0,1)$ và $X=F^{-1}(U)$ thì $X$ có CDF $F$.
2. Nếu $X$ có CDF $F$ thì $F(X)\sim\operatorname{Unif}(0,1)$.

Phần một nói rằng từ $U$ và $F$ ta tạo biến có CDF $F$ bằng cách thế $U$ vào *hàm phân vị* $F^{-1}$. Vì hàm của biến ngẫu nhiên vẫn là biến ngẫu nhiên, $F^{-1}(U)$ là biến; định lý xác định CDF của nó. Phần hai đi chiều ngược: $F(X)$ là biến nhận giá trị giữa 0 và 1, và phân phối của nó là Đều trên $(0,1)$.

**Lưu ý 5.3.2.** Thế $X$ vào chính CDF $F$ của nó thoạt nhìn có vẻ tự tham chiếu, nhưng $F$ chỉ là một hàm như các hàm khác. Dễ nhầm ký hiệu: $F(x)=P(X\le x)$, song viết “$F(X)=P(X\le X)=1$” là sai. Trước tiên phải tìm biểu thức hàm $F$ theo đối số thực $x$, rồi thay $x$ bằng biến $X$. Ví dụ, nếu $F(x)=1-e^{-x}$ với $x>0$, thì $F(X)=1-e^{-X}$.

Hiểu phát biểu định lý là phần khó; chứng minh mỗi chiều chỉ vài dòng.

**Chứng minh.** 1. Nếu $U\sim\operatorname{Unif}(0,1)$ và $X=F^{-1}(U)$, thì với mọi $x$ thực,

$$P(X\le x)=P(F^{-1}(U)\le x)
=P(U\le F(x))=F(x),$$

vì $P(U\le u)=u$ với $u\in(0,1)$.

2. Cho $X$ có CDF $F$, đặt $Y=F(X)$. Vì $Y\in(0,1)$, $P(Y\le y)=0$ khi $y\le0$, bằng 1 khi $y\ge1$. Với $0<y<1$,

$$P(Y\le y)=P(F(X)\le y)
=P(X\le F^{-1}(y))
=F(F^{-1}(y))=y.$$

Vậy $Y$ có CDF $\operatorname{Unif}(0,1)$. □

Để hiểu hàm phân vị và tính phổ quát sâu hơn, xét ví dụ quen thuộc: *phân vị điểm thi*.

**Ví dụ 5.3.3 (Phân vị).** Rất nhiều sinh viên làm một bài thi chấm từ 0 đến 100. Gọi $X$ là điểm của một sinh viên ngẫu nhiên. Để dễ xử lý, xấp xỉ phân phối điểm rời rạc bằng phân phối liên tục có CDF $F$ tăng nghiêm ngặt trên $(0,100)$. Thực tế chỉ có hữu hạn sinh viên và điểm số, nhưng xấp xỉ liên tục có thể tốt.

Giả sử điểm trung vị là 60: một nửa sinh viên cao hơn 60, một nửa thấp hơn. Dùng phân phối liên tục giúp khỏi xét người đúng bằng 60. Khi đó $F(60)=1/2$, hay $F^{-1}(1/2)=60$.

Nếu Fred được 72 điểm, phân vị của cậu là tỉ lệ sinh viên dưới 72 điểm: $F(72)$, nằm trong $(1/2,1)$ vì 72 trên trung vị. Tổng quát, điểm $x$ ứng với phân vị $F(x)$. Ngược lại, $F^{-1}(0{,}95)$ là điểm ứng với phân vị $0{,}95$. $F$ biến điểm thành phân vị; $F^{-1}$ biến phân vị thành điểm.

Giờ $F(X)$ có diễn giải tự nhiên: phân vị của một sinh viên chọn ngẫu nhiên. Phân phối điểm thi có thể rất khác Đều; không có lý do để 10% điểm nằm từ 70 đến 80 chỉ vì khoảng ấy chiếm 10% thang điểm. Nhưng phân phối *phân vị* là Đều: $F(X)\sim\operatorname{Unif}(0,1)$. Chẳng hạn, 50% sinh viên có phân vị ít nhất $0{,}5$; 10% nằm ở mỗi khoảng phân vị $(0,0{,}1)$, $(0{,}1,0{,}2)$, v.v. Điều này cũng rõ từ định nghĩa phân vị. ◇

Áp dụng tính phổ quát cho hai phân phối đã gặp: Logistic và Rayleigh.

**Ví dụ 5.3.4 (Tạo Logistic từ biến Đều).** CDF Logistic là $F(x)=e^x/(1+e^x)$ với $x\in\mathbb R$. Nếu có $U\sim\operatorname{Unif}(0,1)$ và muốn sinh biến Logistic, phần một định lý cho $F^{-1}(U)\sim\operatorname{Logistic}$. Giải phương trình CDF được

$$F^{-1}(u)=\log\frac{u}{1-u},\qquad
F^{-1}(U)=\log\frac{U}{1-U}.$$

Có thể kiểm tra trực tiếp CDF:

$$\begin{aligned}
P\left(\log\frac U{1-U}\le x\right)
&=P\left(\frac U{1-U}\le e^x\right)\\
&=P(U\le e^x(1-U))\\
&=P\left(U\le\frac{e^x}{1+e^x}\right)\\
&=\frac{e^x}{1+e^x}.
\end{aligned}$$

Để trực quan, tác giả mô phỏng một triệu giá trị $\operatorname{Unif}(0,1)$ rồi biến đổi từng giá trị $u$ thành $\log(u/(1-u))$. Hình 5.6 đặt biểu đồ tần suất các giá trị $U$ cạnh PDF Đều; bên dưới đặt biểu đồ giá trị biến đổi cạnh PDF Logistic. Biểu đồ thứ hai rất giống PDF Logistic, đúng như định lý.

*Hình 5.6 (trang PDF 226).* Hàng trên: biểu đồ một triệu giá trị $U\sim\operatorname{Unif}(0,1)$ và PDF Đều. Hàng dưới: biểu đồ một triệu giá trị $\log(U/(1-U))$ và PDF Logistic.

Ngược lại, nếu $X\sim\operatorname{Logistic}$ thì

$$F(X)=\frac{e^X}{1+e^X}\sim\operatorname{Unif}(0,1).\quad\Diamond$$

**Ví dụ 5.3.5 (Tạo Rayleigh từ biến Đều).** CDF Rayleigh là $F(x)=1-e^{-x^2/2}$ với $x>0$. Hàm phân vị là

$$F^{-1}(u)=\sqrt{-2\log(1-u)}.$$

Do đó nếu $U\sim\operatorname{Unif}(0,1)$,

$$\sqrt{-2\log(1-U)}\sim\operatorname{Rayleigh}.$$

Tác giả lại sinh một triệu giá trị Đều và biến đổi chúng. Hình 5.7 cho thấy biểu đồ các giá trị $\sqrt{-2\log(1-U)}$ rất giống PDF Rayleigh, như định lý dự đoán.

*Hình 5.7 (trang PDF 227).* Hàng trên: biểu đồ một triệu giá trị Đều và PDF Đều. Hàng dưới: biểu đồ một triệu giá trị $\sqrt{-2\log(1-U)}$ và PDF Rayleigh.

Ngược lại, nếu $X\sim\operatorname{Rayleigh}$ thì $F(X)=1-e^{-X^2/2}\sim\operatorname{Unif}(0,1)$. ◇

Tính phổ quát áp dụng tới đâu với biến *rời rạc*? CDF rời rạc có bước nhảy và đoạn ngang nên không có $F^{-1}$ theo nghĩa thông thường. Nhưng phần một vẫn đúng theo nghĩa: từ một biến Đều, ta tạo được biến với bất kỳ phân phối rời rạc mong muốn. Thay vì dùng CDF không khả nghịch, làm trực tiếp với PMF thuận tiện hơn.

Giả sử muốn từ $U\sim\operatorname{Unif}(0,1)$ tạo biến $X$ có PMF $p_j=P(X=j)$ với $j=0,1,\ldots,n$. Như Hình 5.8, chia khoảng $(0,1)$ thành các đoạn có độ dài $p_0,p_1,\ldots,p_n$. Vì tổng PMF bằng 1, các đoạn lấp đầy chính xác khoảng đơn vị. Định nghĩa $X=j$ nếu $U$ rơi vào đoạn độ dài $p_j$. Với biến Đều, xác suất bằng độ dài, nên $P(X=j)=p_j$ như yêu cầu.

*Hình 5.8 (trang PDF 228).* Cho PMF, chia khoảng $(0,1)$ thành các đoạn có độ dài đúng bằng các giá trị PMF.

Cách này cũng đúng khi biến rời rạc nhận vô hạn giá trị như Poisson: chia $(0,1)$ thành vô hạn đoạn, tổng độ dài vẫn là 1. Vậy mọi hàm thỏa tính chất PMF ở Định lý 3.2.7 đều thực sự là PMF của một biến ngẫu nhiên, như đã hứa ở Chương 3.

Phần hai của tính phổ quát *không* đúng cho biến rời rạc. Hàm của biến rời rạc vẫn rời rạc, nên $F(X)$ không thể Đều liên tục. Ví dụ, nếu $X\sim\operatorname{Bern}(p)$ thì $F(X)$ chỉ nhận hai giá trị $F(0)=1-p$ và $F(1)=1$.

Kết luận: dùng biến Đều $U$ để sinh biến liên tục bằng cách thế vào CDF nghịch đảo; để sinh biến rời rạc, chia khoảng đơn vị theo các xác suất PMF. Tính phổ quát rất hữu ích trong mô phỏng khi phần mềm sinh được biến Đều nhưng chưa hỗ trợ phân phối cần dùng; mức thuận tiện còn phụ thuộc việc tính CDF nghịch đảo có dễ hay không.

Theo cách ví phân phối là bản thiết kế, biến ngẫu nhiên là ngôi nhà, cái đẹp của tính phổ quát là: bản thiết kế Đều rất đơn giản, dễ xây nhà; rồi có quy tắc đơn giản để sửa “ngôi nhà Đều” thành ngôi nhà theo bất kỳ bản thiết kế khác, dù phức tạp đến đâu.

### 5.4 Phân phối Chuẩn

Phân phối Chuẩn là phân phối liên tục nổi tiếng có PDF hình chuông. Nó rất phổ biến trong thống kê nhờ *định lý giới hạn trung tâm*: dưới những giả thiết khá yếu, tổng của nhiều biến ngẫu nhiên i.i.d. có phân phối xấp xỉ Chuẩn, bất kể phân phối riêng của từng biến. Ta có thể bắt đầu từ những biến độc lập thuộc hầu như bất kỳ phân phối rời rạc hoặc liên tục nào; khi cộng nhiều biến, phân phối của tổng trông gần Chuẩn.

Định lý giới hạn trung tâm sẽ học ở Chương 10. Trước mắt ta giới thiệu PDF, CDF, kỳ vọng và phương sai Chuẩn. Lại dùng chiến lược vị trí–tỉ lệ: bắt đầu bằng *Chuẩn tắc*, có tâm 0 và phương sai 1, rồi dịch và nhân để được mọi phân phối Chuẩn khác.

**Định nghĩa 5.4.1 (Phân phối Chuẩn tắc).** Biến liên tục $Z$ có phân phối Chuẩn tắc nếu PDF $\varphi$ là

$$\varphi(z)=\frac1{\sqrt{2\pi}}e^{-z^2/2},
\qquad -\infty<z<\infty.$$

Ký hiệu $Z\sim N(0,1)$ vì sẽ chứng minh trung bình của $Z$ là 0 và phương sai là 1. Hằng $1/\sqrt{2\pi}$ có thể gây ngạc nhiên: vì sao xuất hiện $\pi$ ở hàm có $e$ dù chẳng thấy hình tròn? Nó chính xác là hằng cần để tích phân PDF bằng 1, gọi là *hằng số chuẩn hóa*.

CDF Chuẩn tắc $\Phi$ là diện tích tích lũy:

$$\Phi(z)=\int_{-\infty}^{z}\varphi(t)\,dt
=\int_{-\infty}^{z}\frac1{\sqrt{2\pi}}e^{-t^2/2}\,dt.$$

Nhiều người khó chịu khi lần đầu gặp $\Phi$ vì nó được để dưới dạng tích phân. Nhưng không có lựa chọn đóng đơn giản: nguyên hàm của $\varphi$ không thể biểu diễn bằng tổng hữu hạn các hàm quen thuộc như đa thức, hàm mũ. Dù không có công thức dạng đóng, $\Phi$ vẫn là hàm xác định rõ: nhập $z$, nhận diện tích dưới PDF từ $-\infty$ đến $z$.

**Ký hiệu 5.4.2.** PDF và CDF Chuẩn tắc được dành hẳn chữ Hy Lạp: theo quy ước, $\varphi$ là PDF, $\Phi$ là CDF. Ta thường dùng $Z$ cho biến Chuẩn tắc.

Hình 5.9 vẽ hai hàm: PDF hình chuông đối xứng quanh 0; CDF hình chữ S. Chúng tương tự PDF và CDF Logistic, nhưng PDF Chuẩn tiến về 0 nhanh hơn nhiều: gần như toàn bộ diện tích dưới $\varphi$ nằm giữa $-3$ và 3, trong khi với Logistic phải nhìn đến khoảng $-5$ đến 5.

*Hình 5.9 (trang PDF 230).* PDF Chuẩn tắc $\varphi$ bên trái và CDF $\Phi$ bên phải.

Có ba tính chất đối xứng quan trọng:

1. **Đối xứng PDF:** $\varphi(z)=\varphi(-z)$, nên $\varphi$ là hàm chẵn.
2. **Đối xứng diện tích đuôi:** Diện tích bên trái $-2$ bằng diện tích bên phải 2. Tổng quát, $\Phi(z)=1-\Phi(-z)$. Nhìn hình thấy rõ; đại số dùng phép đặt $u=-t$ và tổng diện tích 1:

   $$\Phi(-z)=\int_{-\infty}^{-z}\varphi(t)\,dt
   =\int_z^\infty\varphi(u)\,du
   =1-\Phi(z).$$

3. **Đối xứng $Z$ và $-Z$:** Nếu $Z\sim N(0,1)$ thì $-Z\sim N(0,1)$. CDF của $-Z$ là

   $$P(-Z\le z)=P(Z\ge-z)
   =1-\Phi(-z)=\Phi(z).$$

Cần chứng minh ba điều để xử lý phân phối Chuẩn tổng quát: $\varphi$ là PDF hợp lệ, $E(Z)=0$, $\operatorname{Var}(Z)=1$.

Để xác nhận $\varphi$, ta chứng minh tổng diện tích dưới $e^{-z^2/2}$ bằng $\sqrt{2\pi}$. Không tìm được nguyên hàm trực tiếp dưới dạng đóng, nhưng có mẹo cho tích phân xác định: *viết tích phân hai lần*, rồi chuyển sang tọa độ cực. Nếu đặt

$$I=\int_{-\infty}^{\infty}e^{-z^2/2}\,dz,$$

thì

$$\begin{aligned}
I^2
&=\left(\int_{-\infty}^{\infty}e^{-x^2/2}\,dx\right)
  \left(\int_{-\infty}^{\infty}e^{-y^2/2}\,dy\right)\\
&=\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}
e^{-(x^2+y^2)/2}\,dx\,dy\\
&=\int_0^{2\pi}\int_0^\infty e^{-r^2/2}r\,dr\,d\theta.
\end{aligned}$$

Ở dòng đầu, $z$ chỉ là biến tích phân nên được đổi tên thành $x,y$. Thừa số $r$ khi chuyển tọa độ là định thức Jacobi (Phụ lục A.7.2) và cũng giúp giải tích phân: đặt $u=r^2/2$, $du=r\,dr$. Do đó

$$I^2=\int_0^{2\pi}\left(\int_0^\infty e^{-u}\,du\right)d\theta
=\int_0^{2\pi}1\,d\theta=2\pi,$$

nên $I=\sqrt{2\pi}$ như cần chứng minh.

Theo đối xứng PDF, trọng tâm Chuẩn tắc phải là 0. Trong định nghĩa,

$$E(Z)=\frac1{\sqrt{2\pi}}
\int_{-\infty}^{\infty}ze^{-z^2/2}\,dz=0,$$

vì $ze^{-z^2/2}$ là hàm lẻ: diện tích có dấu ở hai phía 0 triệt tiêu. Lập luận tương tự cho $E(Z^n)=0$ với mọi số nguyên dương lẻ $n$.

*Lưu ý kỹ thuật:* Không thể chỉ lấy “$\infty-\infty$”; cần biết diện tích tuyệt đối một phía hữu hạn. Ở đây đúng vì $e^{-z^2/2}$ giảm rất nhanh, nhanh hơn mức tăng đa thức $z^n$.

Tính trung bình dễ, còn phương sai đòi thêm một bước. Theo LOTUS, $EZ=0$ và tính chẵn của $z^2e^{-z^2/2}$,

$$\operatorname{Var}(Z)=E(Z^2)
=\frac2{\sqrt{2\pi}}\int_0^\infty z^2e^{-z^2/2}\,dz.$$

Tích phân từng phần với $u=z$, $dv=ze^{-z^2/2}\,dz$, nên $du=dz$, $v=-e^{-z^2/2}$:

$$\begin{aligned}
\operatorname{Var}(Z)
&=\frac2{\sqrt{2\pi}}
\left(\left[-ze^{-z^2/2}\right]_0^\infty
+\int_0^\infty e^{-z^2/2}\,dz\right)\\
&=\frac2{\sqrt{2\pi}}
\left(0+\frac{\sqrt{2\pi}}2\right)=1.
\end{aligned}$$

Số hạng biên bằng 0 vì hàm mũ giảm nhanh hơn $z$ tăng. Tích phân còn lại là nửa tổng diện tích $\sqrt{2\pi}$. Vậy Chuẩn tắc có trung bình 0, phương sai 1.

Phân phối Chuẩn tổng quát có hai tham số $\mu,\sigma^2$, chính là trung bình và phương sai. Từ $Z\sim N(0,1)$, dịch và nhân cho mọi trung bình, phương sai mong muốn.

**Định nghĩa 5.4.3 (Phân phối Chuẩn).** Nếu $Z\sim N(0,1)$, thì

$$X=\mu+\sigma Z\sim N(\mu,\sigma^2),$$

nghĩa là $X$ Chuẩn với trung bình $\mu$, phương sai $\sigma^2$. Thật vậy,

$$E(\mu+\sigma Z)=\mu,\qquad
\operatorname{Var}(\mu+\sigma Z)
=\sigma^2\operatorname{Var}(Z)=\sigma^2.$$

Ta nhân $Z$ với *độ lệch chuẩn* $\sigma$, không phải $\sigma^2$; nếu nhân với $\sigma^2$ thì đơn vị sai và phương sai thành $\sigma^4$.

Đi chiều ngược từ $X$ về $Z$ gọi là *chuẩn hóa*:

$$\frac{X-\mu}{\sigma}\sim N(0,1).$$

Dùng chuẩn hóa, ta tìm CDF và PDF tổng quát theo hai hàm Chuẩn tắc.

**Định lý 5.4.4 (CDF và PDF Chuẩn).** Với $X\sim N(\mu,\sigma^2)$,

$$F(x)=\Phi\left(\frac{x-\mu}{\sigma}\right),
\qquad
f(x)=\frac1{\sigma}
\varphi\left(\frac{x-\mu}{\sigma}\right).$$

**Chứng minh.** Chuẩn hóa trong định nghĩa CDF:

$$F(x)=P(X\le x)
=P\left(\frac{X-\mu}{\sigma}
\le\frac{x-\mu}{\sigma}\right)
=\Phi\left(\frac{x-\mu}{\sigma}\right).$$

Lấy đạo hàm và dùng quy tắc dây chuyền cho PDF. Viết tường minh,

$$f(x)=\frac1{\sqrt{2\pi}\sigma}
\exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right).\quad\Box$$

Ba mốc quan trọng là xác suất nằm trong một, hai, ba độ lệch chuẩn quanh trung bình.

**Định lý 5.4.5 (Quy tắc 68–95–99,7%).** Nếu $X\sim N(\mu,\sigma^2)$ thì

$$P(|X-\mu|<\sigma)\approx0{,}68,\quad
P(|X-\mu|<2\sigma)\approx0{,}95,\quad
P(|X-\mu|<3\sigma)\approx0{,}997.$$

Quy tắc cho xấp xỉ nhanh xác suất Chuẩn. Sau chuẩn hóa,

$$P(|Z|<1)\approx0{,}68,\quad
P(|Z|<2)\approx0{,}95,\quad
P(|Z|<3)\approx0{,}997.$$

*Chú thích:* Quy tắc nói khoảng 95% giá trị nằm trong $\pm2$ độ lệch chuẩn. Mốc chính xác hơn là $\pm1{,}96$ độ lệch chuẩn. Vì thế 1,96 xuất hiện thường xuyên trong khoảng tin cậy 95%: lấy ước lượng rồi thêm biên 1,96 độ lệch chuẩn mỗi phía.

**Ví dụ 5.4.6 (bắt đầu).** Cho $X\sim N(-1,4)$. Tính $P(|X|<3)$ chính xác theo $\Phi$ và xấp xỉ. Biến cố $|X|<3$ là $-3<X<3$. Chuẩn hóa bằng $Z=(X+1)/2$:

$$P(-3<X<3)
=P\left(\frac{-3-(-1)}2<Z<
\frac{3-(-1)}2\right)
=P(-1<Z<2).$$

Đáp án chính xác là $\Phi(2)-\Phi(-1)$. Quy tắc 68–95–99,7% cho $P(-1<Z<1)\approx0{,}68$ và $P(-2<Z<2)\approx0{,}95$. Mở rộng từ $\pm1$ đến $\pm2$ thêm khoảng $0{,}27$ diện tích; do đối xứng, mỗi phía thêm $0{,}135$. Vậy

$$P(-1<Z<2)\approx0{,}68+\frac{0{,}27}{2}=0{,}815,$$

khá gần giá trị đúng $\Phi(2)-\Phi(-1)\approx0{,}8186$. ◇

### 5.5 Phân phối Mũ

Phân phối Mũ là tương ứng liên tục của phân phối Hình học. Biến Hình học đếm số thất bại trước thành công đầu tiên trong dãy thử Bernoulli; với phân phối Mũ, ta chờ thành công trong *thời gian liên tục*, các lần thành công đến với tốc độ $\lambda$ lần trên mỗi đơn vị thời gian. Trong khoảng dài $t$, số thành công trung bình là $\lambda t$, nhưng số thực tế ngẫu nhiên. Biến Mũ biểu thị thời gian chờ đến lần thành công đầu.

**Định nghĩa 5.5.1 (Phân phối Mũ).** Biến liên tục $X$ có phân phối Mũ với tham số $\lambda$ nếu PDF là

$$f(x)=\lambda e^{-\lambda x},\qquad x>0.$$

Ký hiệu $X\sim\operatorname{Expo}(\lambda)$. CDF tương ứng là $F(x)=1-e^{-\lambda x}$ khi $x>0$. PDF và CDF $\operatorname{Expo}(1)$ được vẽ ở Hình 5.10; chúng tương tự PMF và CDF Hình học ở Chương 4. Bài tập 45 khảo sát cách Hình học tiến đến Mũ khi phép thử Bernoulli diễn ra ngày càng nhanh nhưng xác suất thành công mỗi lần ngày càng nhỏ.

Các phân phối Đều và Chuẩn liên hệ bằng phép dịch và nhân tỉ lệ. Phân phối Mũ luôn có miền giá trị $(0,\infty)$, nên dịch sẽ đổi đầu trái; nhưng phép nhân tỉ lệ hoạt động tốt. Nếu $X\sim\operatorname{Expo}(1)$ thì

$$Y=\frac X\lambda\sim\operatorname{Expo}(\lambda),$$

vì với $y>0$,

$$P(Y\le y)=P(X\le\lambda y)=1-e^{-\lambda y}.$$

Ngược lại, nếu $Y\sim\operatorname{Expo}(\lambda)$ thì $\lambda Y\sim\operatorname{Expo}(1)$.

*Hình 5.10 (trang PDF 236).* PDF và CDF của $\operatorname{Expo}(1)$.

Vậy có thể tính trung bình và phương sai bằng trường hợp đơn giản $X\sim\operatorname{Expo}(1)$. Tích phân từng phần cho

$$E(X)=\int_0^\infty xe^{-x}\,dx=1,\qquad
E(X^2)=\int_0^\infty x^2e^{-x}\,dx=2,$$

và $\operatorname{Var}(X)=2-1^2=1$. Chương sau sẽ giới thiệu hàm sinh mômen để tìm các kết quả ấy mà không cần tích phân. Với $Y=X/\lambda$,

$$E(Y)=\frac1\lambda,\qquad
\operatorname{Var}(Y)=\frac1{\lambda^2}.$$

Tốc độ đến $\lambda$ càng lớn thì thời gian chờ trung bình càng ngắn.

Phân phối Mũ có tính chất đặc biệt gọi là *không nhớ*: dù đã chờ nhiều giờ hay nhiều ngày mà chưa thành công, thành công cũng không vì thế mà sắp đến hơn. Xét về thời gian còn phải chờ, như thể bạn chỉ mới bắt đầu đợi 10 giây trước.

**Định nghĩa 5.5.2 (Tính không nhớ).** Một phân phối có tính không nhớ nếu biến $X$ mang phân phối ấy thỏa

$$P(X\ge s+t\mid X\ge s)=P(X\ge t)$$

với mọi $s,t>0$. Ở đây $s$ là thời gian đã chờ; sau khi chờ $s$ phút, xác suất còn phải chờ thêm ít nhất $t$ phút bằng xác suất ngay từ đầu phải chờ ít nhất $t$ phút. Nói cách khác, khi biết $X\ge s$, thời gian chờ thêm $X-s$ vẫn phân phối $\operatorname{Expo}(\lambda)$. Đặc biệt,

$$E(X\mid X\ge s)=s+E(X)=s+\frac1\lambda.$$

Kỳ vọng có điều kiện sẽ được giải thích kỹ ở Chương 9; ở đây $E(X\mid A)$ là kỳ vọng $X$ khi biết biến cố $A$, tính bằng cách thay PMF hoặc PDF thường bằng PMF hoặc PDF có điều kiện trong định nghĩa kỳ vọng.

Kiểm tra trực tiếp tính không nhớ bằng xác suất có điều kiện, với $X\sim\operatorname{Expo}(\lambda)$:

$$P(X\ge s+t\mid X\ge s)
=\frac{P(X\ge s+t)}{P(X\ge s)}
=\frac{e^{-\lambda(s+t)}}{e^{-\lambda s}}
=e^{-\lambda t}
=P(X\ge t).$$

Nếu thời gian đến xe buýt phân phối Mũ, sau khi bạn chờ 30 phút, xe cũng chưa vì thế mà “sắp đến”; phân phối quên nửa giờ ấy và thời gian còn lại như khi bạn vừa đến bến. Nếu tuổi thọ một máy phân phối Mũ, sau khi đã chạy lâu mà chưa hỏng, nó vẫn như mới theo nghĩa xác suất: không có hiệu ứng hao mòn làm nó dễ hỏng sớm hơn. Nếu tuổi thọ con người là Mũ, người đã sống đến 80 tuổi sẽ có phân phối thời gian sống còn lại giống trẻ sơ sinh!

Rõ ràng tính không nhớ không mô tả tốt tuổi thọ người hoặc máy. Vậy tại sao phân phối Mũ quan trọng?

1. Một số hiện tượng vật lý, như phân rã phóng xạ, thực sự có tính không nhớ, nên Mũ là mô hình hữu ích.
2. Mũ liên hệ chặt với các phân phối có tên khác. Mục tiếp theo nối Mũ với Poisson qua cùng một câu chuyện; các chương sau còn nhiều liên hệ.
3. Mũ là thành phần xây các phân phối linh hoạt hơn như Weibull (Bài tập 25 Chương 6), cho phép hiệu ứng hao mòn, hoặc hiệu ứng “sống sót của kẻ thích nghi” khi sống càng lâu thì càng bền. Muốn hiểu chúng, trước hết phải hiểu Mũ.

Tính không nhớ là tính chất rất riêng: không có phân phối liên tục nào khác trên $(0,\infty)$ có nó.

**Định lý 5.5.3.** Nếu $X$ là biến liên tục dương có tính không nhớ thì $X$ có phân phối Mũ.

**Chứng minh.** Gọi $F$ là CDF của $X$ và $G(x)=P(X>x)=1-F(x)$ là hàm sống sót. Ta sẽ chứng minh $G(x)=e^{-\lambda x}$ với một $\lambda$. Tính không nhớ cho

$$G(s+t)=G(s)G(t),\qquad s,t>0.$$

Lấy đạo hàm theo $s$ (CDF liên tục trong nghĩa đang dùng nên $G$ khả vi):

$$G'(s+t)=G'(s)G(t).$$

Cho $s=0$, $G'(t)=G'(0)G(t)$. Đặt $c=G'(0)$, $y=G(t)$, ta được phương trình vi phân tách biến $dy/dt=cy$ (xem Phụ lục A.5). Nghiệm tổng quát $G(t)=Ke^{ct}$; điều kiện $G(0)=P(X>0)=1$ cho $K=1$. Đặt $\lambda=-c$, ta có $G(t)=e^{-\lambda t}$. Vì $G$ giảm, $c<0$ nên $\lambda>0$. Vậy $X$ có phân phối Mũ. □

Vì câu chuyện Hình học và Mũ tương tự, bạn có thể đoán Hình học cũng không nhớ. Đúng vậy: khi chờ lần đầu ra ngửa, dù vừa có 10 lần sấp liên tiếp, số lần tung còn cần không đổi phân phối. Đồng xu không “nợ” mặt ngửa và cũng không cố tình ra sấp mãi. Hình học là phân phối rời rạc duy nhất trên $\{0,1,\ldots\}$ có tính không nhớ; Mũ là phân phối liên tục duy nhất trên $(0,\infty)$ có tính ấy.

**Ví dụ 5.5.4 (Blissville và Blotchville).** Fred sống ở Blissville, nơi xe buýt luôn đến đúng giờ, cách nhau đúng 10 phút. Bị mất đồng hồ, Fred đến bến vào một thời điểm đều ngẫu nhiên trong ngày; giả sử xe chạy 24 giờ mỗi ngày và thời điểm Fred đến độc lập với lịch xe.

(a) Thời gian Fred chờ chuyến tiếp theo có phân phối gì? Trung bình anh chờ bao lâu?

(b) Nếu đã chờ sáu phút mà xe chưa đến, xác suất phải chờ thêm ít nhất ba phút là bao nhiêu?

(c) Fred chuyển tới Blotchville, nơi xe đến thất thường hơn. Sau mỗi lần một xe đến, thời gian đến xe kế tiếp có phân phối Mũ với trung bình 10 phút. Fred đến bến vào thời điểm ngẫu nhiên, không biết xe trước đến bao lâu rồi. Thời gian chờ xe kế tiếp của anh có phân phối gì và trung bình bao lâu?

(d) Fred than phiền giao thông Blotchville tệ hơn. Bạn anh nói: “Đừng than nữa! Anh đến vào một thời điểm đều ngẫu nhiên giữa hai chuyến xe. Khoảng cách trung bình giữa hai xe là 10 phút; vì anh có khả năng đến như nhau ở mọi thời điểm trong khoảng ấy, trung bình anh chỉ phải chờ năm phút.” Fred không đồng ý, cả theo kinh nghiệm lẫn đáp án (c) mà anh giải lúc chờ xe. Hãy chỉ ra sai lầm của người bạn.

**Lời giải.** (a) Thời gian chờ Đều trên $(0,10)$, trung bình năm phút.

(b) Gọi $T$ là thời gian chờ. Khi biết $T>6$,

$$P(T\ge9\mid T>6)
=\frac{P(T\ge9)}{P(T>6)}
=\frac{1/10}{4/10}
=\frac14.$$

Thời gian chờ ở Blissville không có tính không nhớ: sau khi đợi sáu phút, cơ hội còn phải đợi ít nhất ba phút là $1/4$, trong khi người vừa tới bến có xác suất $P(T\ge3)=7/10$.

(c) Theo tính không nhớ, thời gian chờ còn lại là $\operatorname{Expo}(1/10)$, trung bình 10 phút, bất kể Fred đến lúc nào và chuyến trước đã đi bao lâu.

(d) Bạn Fred phạm lỗi ở Lưu ý 4.1.3: thay biến ngẫu nhiên (khoảng thời gian giữa xe) bằng kỳ vọng 10 phút, bỏ qua sự biến thiên. Trung bình các khoảng là 10 phút, nhưng Fred *không* đồng khả năng rơi vào mọi khoảng: anh dễ đến trong khoảng dài hơn khoảng ngắn. Nếu một khoảng dài 50 phút và khoảng khác dài 5 phút, Fred có khả năng đến trong khoảng 50 phút cao gấp 10 lần.

Hiện tượng ấy gọi là *thiên lệch theo độ dài*. Nó gặp trong nhiều tình huống: hỏi ngẫu nhiên các bà mẹ họ có bao nhiêu con cho phân phối khác hỏi ngẫu nhiên người dân họ có bao nhiêu anh chị em, kể cả bản thân. Hỏi sinh viên sĩ số lớp họ rồi lấy trung bình có thể cao hơn nhiều so với lấy danh sách các lớp và trung bình sĩ số, gọi là *nghịch lý sĩ số lớp*. Các bài tập tiếp tục câu chuyện Fred; xem thêm MacKay [18]. ◇

### 5.6 Quá trình Poisson

Phân phối Mũ liên hệ chặt với Poisson, như việc cùng dùng tham số $\lambda$ gợi ý. Hai phân phối được nối bởi câu chuyện *quá trình Poisson*: một chuỗi các lần xuất hiện ở những thời điểm khác nhau, sao cho số lần xuất hiện trong một khoảng thời gian có phân phối Poisson. Chương 13 nghiên cứu kỹ; ta đã có đủ công cụ cho định nghĩa và tính chất cơ bản.

**Định nghĩa 5.6.1 (Quá trình Poisson, bắt đầu).** Một quá trình các lần xuất hiện trong thời gian liên tục là quá trình Poisson tốc độ $\lambda$ nếu hai điều kiện đúng:

1. Số lần xuất hiện trong khoảng thời gian dài $t$ có phân phối $\operatorname{Pois}(\lambda t)$.
2. Số lần xuất hiện trong các khoảng thời gian rời nhau độc lập. Ví dụ, số lần trong $(0,10)$, $[10,12)$ và $[15,\infty)$ độc lập.

Hình 5.11 phác một quá trình Poisson; mỗi dấu nhân đánh dấu một lần xuất hiện.

*Hình 5.11 (trang PDF 241).* Quá trình Poisson với các thời điểm xuất hiện $T_1,T_2,\ldots$.

Ví dụ, giả sử các lần xuất hiện là email đến hộp thư theo quá trình Poisson tốc độ $\lambda$. Trong một giờ có bao nhiêu email? Theo định nghĩa, số email có phân phối $\operatorname{Pois}(\lambda)$. Đây là biến nguyên không âm, nên dùng phân phối rời rạc.

Đảo câu hỏi: từ một thời điểm mốc, phải chờ bao lâu đến email đầu tiên? Thời gian chờ là số thực dương, nên dùng phân phối liên tục trên $(0,\infty)$. Gọi $T_1$ là thời gian ấy và $N_t$ là số email đã đến tính đến thời điểm $t$. Mấu chốt:

$$\{T_1>t\}=\{N_t=0\}.$$

Đây là *tính hai mặt số đếm–thời điểm*: biến rời rạc $N_t$ đếm số lần, biến liên tục $T_1$ đánh dấu thời điểm đến đầu. Hai biến cố bằng nhau có cùng xác suất. Vì $N_t\sim\operatorname{Pois}(\lambda t)$,

$$P(T_1>t)=P(N_t=0)
=\frac{e^{-\lambda t}(\lambda t)^0}{0!}
=e^{-\lambda t}.$$

Do đó $P(T_1\le t)=1-e^{-\lambda t}$, tức $T_1\sim\operatorname{Expo}(\lambda)$. Thời gian đến lần xuất hiện đầu trong quá trình Poisson tốc độ $\lambda$ là biến Mũ cùng tham số.

Thế còn $T_2-T_1$, thời gian giữa lần thứ nhất và thứ hai? Các khoảng rời nhau độc lập, nên khi lần đầu đã đến, quá khứ không ảnh hưởng tương lai. Vì vậy $T_2-T_1$ độc lập với $T_1$ và cũng phân phối $\operatorname{Expo}(\lambda)$. Tương tự, $T_3-T_2$ độc lập với hai khoảng trước và có cùng phân phối. Suy ra mọi khoảng giữa các lần đến đều i.i.d. $\operatorname{Expo}(\lambda)$.

Tóm lại, trong quá trình Poisson tốc độ $\lambda$:

- Số lần đến trong khoảng dài 1 có phân phối $\operatorname{Pois}(\lambda)$.
- Các thời gian giữa những lần đến là biến i.i.d. $\operatorname{Expo}(\lambda)$.

Quá trình Poisson nối phân phối rời rạc với liên tục; ký hiệu $\lambda$ dùng chung là hợp lý vì nó là tốc độ xuất hiện trong cùng quá trình.

**Lưu ý 5.6.2.** Tổng thời gian đến lần xuất hiện thứ hai $T_2=T_1+(T_2-T_1)$ là tổng hai biến $\operatorname{Expo}(\lambda)$ độc lập. Nó không còn Mũ mà có phân phối Gamma, sẽ giới thiệu ở Chương 8.

Câu chuyện quá trình Poisson cho trực giác rằng giá trị nhỏ nhất của các biến Mũ độc lập vẫn là Mũ.

**Ví dụ 5.6.3 (Giá trị nhỏ nhất của các biến Mũ độc lập).** Cho $X_1,\ldots,X_n$ độc lập với $X_j\sim\operatorname{Expo}(\lambda_j)$. Đặt $L=\min(X_1,\ldots,X_n)$. Chứng minh $L\sim\operatorname{Expo}(\lambda_1+\cdots+\lambda_n)$ và giải thích trực giác.

**Lời giải.** Tìm hàm sống sót:

$$\begin{aligned}
P(L>t)
&=P(X_1>t,\ldots,X_n>t)\\
&=P(X_1>t)\cdots P(X_n>t)\\
&=e^{-\lambda_1t}\cdots e^{-\lambda_nt}
=e^{-(\lambda_1+\cdots+\lambda_n)t}.
\end{aligned}$$

Biến cố giá trị nhỏ nhất vượt $t$ nghĩa là *mọi* $X_j$ đều vượt $t$; dòng thứ hai dùng độc lập. Hàm sống sót cuối đúng của biến Mũ tốc độ tổng. Theo trực giác, $\lambda_j$ là tốc độ của $n$ quá trình Poisson độc lập, chẳng hạn thời gian chờ xe màu xanh lá, xanh lam, v.v. Biến $L$ chờ xe thuộc *bất kỳ* màu nào trong các màu ấy, nên tốc độ tổng là tổng các tốc độ. ◇

### 5.7 Tính đối xứng của các biến liên tục i.i.d.

Các biến liên tục độc lập cùng phân phối có tính đối xứng quan trọng: mọi thứ hạng đều đồng khả năng.

**Mệnh đề 5.7.1.** Nếu $X_1,\ldots,X_n$ i.i.d. từ phân phối liên tục, thì với mọi hoán vị $a_1,\ldots,a_n$ của $1,\ldots,n$,

$$P(X_{a_1}<\cdots<X_{a_n})=\frac1{n!}.$$

**Chứng minh.** Gọi $F$ là CDF chung. Theo đối xứng, mọi thứ tự đồng khả năng. Chẳng hạn, $P(X_3<X_2<X_1)=P(X_1<X_2<X_3)$ vì hai biểu thức cùng dạng $P(A<B<C)$ với $A,B,C$ i.i.d. từ $F$.

Với $i\ne j$, xác suất $X_i=X_j$ bằng 0 vì chúng độc lập và liên tục. Theo bất đẳng thức Boole, xác suất có ít nhất một cặp hòa cũng bằng 0:

$$P\left(\bigcup_{i\ne j}\{X_i=X_j\}\right)
\le\sum_{i\ne j}P(X_i=X_j)=0.$$

Vậy các giá trị phân biệt với xác suất 1, và mỗi trong $n!$ thứ tự có xác suất $1/n!$. □

**Lưu ý 5.7.2.** Mệnh đề có thể sai khi các biến phụ thuộc. Nếu $X_1=X_2$ luôn luôn thì cả $P(X_1<X_2)$ lẫn $P(X_2<X_1)$ đều bằng 0. Với những biến phụ thuộc khác, hai xác suất ấy còn có thể khác nhau (xem Bài tập 42 Chương 3).

Nếu $X,Y$ i.i.d. liên tục thì $P(X<Y)=P(Y<X)=1/2$, vì đối xứng và xác suất hòa bằng 0. Nếu i.i.d. rời rạc, hai xác suất vẫn bằng nhau nhưng mỗi cái nhỏ hơn $1/2$ do có thể hòa.

Thứ hạng của các số phân biệt được tính từ nhỏ nhất hạng 1, kế đến hạng 2, v.v. Chẳng hạn, dãy $3{,}14;2{,}72;1{,}41;1{,}62$ có thứ hạng $4,3,1,2$. Mệnh đề nói thứ hạng của $X_1,\ldots,X_n$ i.i.d. liên tục là một hoán vị đều ngẫu nhiên của $1,\ldots,n$.

Ví dụ sau dùng tính đối xứng cùng chỉ báo trong bài toán *kỷ lục*, như lượng mưa cao kỷ lục hay thành tích nhảy cao.

**Ví dụ 5.7.3 (Kỷ lục).** Các vận động viên lần lượt nhảy cao. Gọi $X_j$ là độ cao của người thứ $j$, các $X_j$ i.i.d. liên tục. Người thứ $j$ lập kỷ lục nếu $X_j$ cao hơn mọi $X_1,\ldots,X_{j-1}$.

(a) Biến cố “người thứ 110 lập kỷ lục” có độc lập với “người thứ 111 lập kỷ lục” không?

(b) Tìm kỳ vọng số kỷ lục trong $n$ người đầu. Khi $n\to\infty$ thì sao?

(c) *Kỷ lục kép* tại $j$ xảy ra nếu cả người thứ $j-1$ và $j$ đều lập kỷ lục. Tìm kỳ vọng số kỷ lục kép trong $n$ người đầu. Khi $n\to\infty$ thì sao?

**Lời giải.** (a) Gọi $I_j$ là chỉ báo người thứ $j$ lập kỷ lục. Theo đối xứng, $P(I_j=1)=1/j$, vì trong $j$ lượt đầu, mỗi lượt đều đồng khả năng cao nhất. Cả lượt 110 và 111 lập kỷ lục đúng khi trong 111 lượt đầu, cao nhất ở vị trí 111 và cao nhì ở vị trí 110; 109 lượt còn lại xếp tùy ý. Vì vậy

$$P(I_{110}=1,I_{111}=1)
=\frac{109!}{111!}
=\frac1{110\cdot111}
=P(I_{110}=1)P(I_{111}=1).$$

Hai biến cố độc lập. Trực giác: biết người 111 lập kỷ lục không cho thông tin về thứ tự *bên trong* 110 kết quả trước.

(b) Theo tính tuyến tính, kỳ vọng số kỷ lục là $\sum_{j=1}^{n}1/j$, tiến tới vô hạn khi $n\to\infty$ vì chuỗi điều hòa phân kỳ.

(c) Gọi $J_j$ là chỉ báo kỷ lục kép tại $j$, $2\le j\le n$. Từ lập luận (a), $P(J_j=1)=1/[j(j-1)]$. Kỳ vọng số kỷ lục kép:

$$
\sum_{j=2}^{n}\frac1{j(j-1)}
=\sum_{j=2}^{n}\left(\frac1{j-1}-\frac1j\right)
=1-\frac1n.
$$

Vậy kỳ vọng số kỷ lục thông thường tăng không giới hạn, còn kỳ vọng số kỷ lục kép tiến tới 1. ◇

### 5.8 Tóm tắt

Biến liên tục có thể nhận mọi giá trị trong một khoảng, dù xác suất bằng đúng một giá trị cụ thể luôn bằng 0. CDF khả vi và đạo hàm là PDF. Xác suất là *diện tích* dưới PDF, không phải giá trị PDF tại một điểm. Muốn tính xác suất phải tích phân.

| Khái niệm | Biến rời rạc | Biến liên tục |
|---|---|---|
| CDF | $F(x)=P(X\le x)$ | $F(x)=P(X\le x)$ |
| PMF/PDF | $P(X=x)$ là độ cao bước nhảy CDF tại $x$; PMF không âm, tổng bằng 1 | $f(x)=F'(x)$; PDF không âm, tích phân trên toàn trục bằng 1 |
| Xác suất trong tập | Cộng PMF trên tập | Tích phân PDF trên vùng |
| Kỳ vọng | $E(X)=\sum_xxP(X=x)$ | $E(X)=\int_{-\infty}^{\infty}xf(x)\,dx$ |
| LOTUS | $E(g(X))=\sum_xg(x)P(X=x)$ | $E(g(X))=\int_{-\infty}^{\infty}g(x)f(x)\,dx$ |

Ba phân phối liên tục quan trọng là Đều, Chuẩn và Mũ. Biến $\operatorname{Unif}(a,b)$ là số “hoàn toàn ngẫu nhiên” trong $(a,b)$, với xác suất tỉ lệ độ dài. Tính phổ quát của Đều cho cách tạo biến theo phân phối khác từ $\operatorname{Unif}(0,1)$; nếu thế một biến liên tục vào CDF của chính nó, kết quả là $\operatorname{Unif}(0,1)$.

Biến $N(\mu,\sigma^2)$ có PDF hình chuông đối xứng quanh $\mu$, với $\sigma$ kiểm soát độ trải rộng. Trung bình là $\mu$, độ lệch chuẩn là $\sigma$. Quy tắc 68–95–99,7% cho các mốc xác suất nằm trong một, hai, ba độ lệch chuẩn quanh trung bình.

Biến $\operatorname{Expo}(\lambda)$ là thời gian chờ thành công đầu trong thời gian liên tục, tương ứng biến Hình học đếm thất bại trước thành công đầu trong thời gian rời rạc; $\lambda$ là tốc độ xuất hiện. Mũ có tính không nhớ: sau khi chờ một thời gian chưa thành công, phân phối thời gian còn phải chờ vẫn như ban đầu. Đây là phân phối liên tục dương duy nhất có tính ấy.

Quá trình Poisson là chuỗi lần đến trong thời gian liên tục: số lần đến trong khoảng có độ dài cố định phân phối Poisson, và các khoảng rời nhau độc lập. Thời gian giữa các lần đến trong quá trình tốc độ $\lambda$ là các biến i.i.d. $\operatorname{Expo}(\lambda)$.

Chiến lược vị trí–tỉ lệ: nếu dịch và nhân không đưa biến ra khỏi họ phân phối đang xét, ta bắt đầu từ thành viên đơn giản nhất rồi biến đổi cho trường hợp tổng quát:

- Đều: $U\sim\operatorname{Unif}(0,1)$ cho $a+(b-a)U\sim\operatorname{Unif}(a,b)$.
- Chuẩn: $Z\sim N(0,1)$ cho $\mu+\sigma Z\sim N(\mu,\sigma^2)$.
- Mũ: $X\sim\operatorname{Expo}(1)$ cho $X/\lambda\sim\operatorname{Expo}(\lambda)$. Không dịch vì sẽ làm miền giá trị không còn $(0,\infty)$.

Trong sơ đồ liên hệ các phân phối, Mũ là giới hạn liên tục của Hình học; Poisson và Mũ nối nhau qua quá trình Poisson. Trên bản đồ bốn loại đối tượng nền tảng, PDF được thêm làm bản thiết kế cho biến liên tục, song song PMF cho biến rời rạc (Hình 5.12).

### 5.9 R

Mục này giới thiệu các phân phối liên tục trong R, cách vẽ đồ thị cơ bản, mô phỏng tính phổ quát của Đều và thời điểm đến trong quá trình Poisson.
