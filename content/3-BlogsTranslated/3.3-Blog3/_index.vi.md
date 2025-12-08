---
title: "Hướng dẫn Amazon DocumentDB Serverless dành cho Nhà phát triển Game"
date: "2025-09-11"
weight: 2
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Thông tin dưới đây chỉ mang tính chất tham khảo. Vui lòng **không sao chép nguyên văn** cho báo cáo của riêng bạn, bao gồm cả cảnh báo này.
{{% /notice %}}

# HƯỚNG DẪN AMAZON DOCUMENTDB SERVERLESS DÀNH CHO NHÀ PHÁT TRIỂN GAME

**Bài viết gốc**: [Game developer's guide to Amazon DocumentDB Serverless](https://aws.amazon.com/vi/blogs/gametech/game-developers-guide-to-amazon-documentdb-serverless/)

**Tác giả gốc**: Jackie Jiang, Douglas Bonser, và Matthew Nimmo

**Ngày xuất bản**: 18 NOV 2025

**Người dịch**: Diệp Huy

**Ngày dịch**: 02 DEC 2025

---

## GIỚI THIỆU

Hôm nay, chúng ta sẽ khám phá cách Amazon DocumentDB Serverless giúp các nhà phát triển game đơn giản hóa hoạt động, xử lý lưu lượng truy cập không thể dự đoán và tối ưu hóa chi phí.

---

## AMAZON DOCUMENTDB SERVERLESS LÀ GÌ

Amazon DocumentDB Serverless là một cấu hình theo yêu cầu, tự động mở rộng (on-demand, auto scaling) cho Amazon DocumentDB (tương thích với MongoDB). Nó tự động mở rộng quy mô dung lượng lên hoặc xuống theo từng mức tăng nhỏ dựa trên nhu cầu của ứng dụng của bạn. Nó loại bỏ nhu cầu phải cung cấp, mở rộng và quản lý các database instance theo cách thủ công, đồng thời xác minh rằng bạn chỉ trả tiền cho các tài nguyên mà bạn thực sự tiêu thụ.

---

## TẠI SAO CÁC STUDIO GAME NÊN QUAN TÂM

Đối với các studio game quản lý dữ liệu người chơi, bảng xếp hạng và trạng thái game, việc quản lý cơ sở dữ liệu có thể là một vấn đề vận hành đáng kể. Amazon DocumentDB Serverless cung cấp một giải pháp hấp dẫn đặc biệt phù hợp với các khối lượng công việc động (dynamic workloads) phổ biến trong các ứng dụng game.

- **Tính linh hoạt ngày ra mắt**: Không còn phải đoán mò về kích thước instance cần thiết cho ngày ra mắt. Amazon DocumentDB Serverless tự động mở rộng quy mô để xử lý các đợt tăng đột biến người chơi, sau đó thu nhỏ lại trong các giai đoạn yên tĩnh.

- **Tối ưu hóa chi phí**: Đối với các game theo mùa hoặc những game có giờ cao điểm rõ rệt, bạn chỉ phải trả tiền cho việc sử dụng thực tế. Khi người chơi châu Âu của bạn đang ngủ và người chơi Mỹ chưa đăng nhập, bạn không lãng phí tiền cho dung lượng cơ sở dữ liệu nhàn rỗi.

- **Hiệu quả môi trường phát triển**: Đang thử nghiệm các tính năng mới hoặc chạy môi trường QA? Amazon DocumentDB Serverless hoàn hảo cho các khối lượng công việc phát triển nơi việc sử dụng cơ sở dữ liệu không đều đặn, nhưng hiệu suất cao vẫn rất quan trọng.

---

## CÁC TÌNH HUỐNG GAME THỰC TẾ

Sau đây là một số tình huống game mà Amazon DocumentDB Serverless có thể hỗ trợ:

### Live service games

- **Ví dụ**: Trong một sự kiện chung kết mùa trong game battle royale, số lượng người chơi có thể tăng từ 50.000 lên 500.000 trong vài phút. Amazon DocumentDB Serverless tự động mở rộng để xử lý hàng triệu lần kiểm tra kho đồ đồng thời và ghi kết quả trận đấu.

- **Quản lý reset hàng ngày**: Khi tất cả người chơi đồng thời nhận phần thưởng hàng ngày vào thời điểm reset, cơ sở dữ liệu xử lý mượt mà đợt tăng đột biến mà không cần cung cấp trước.

- **Sự kiện đặc biệt**: Trong một sự kiện rơi vật phẩm hiếm, cơ sở dữ liệu có thể xử lý hàng nghìn cập nhật kho đồ đồng thời và giao dịch marketplace.

### MMO đa nền tảng

- **Ví dụ**: Một MMO ra mắt raid boss mới vào các thời điểm khác nhau trên các khu vực. Khi các server châu Á đạt đỉnh, sau đó châu Âu, rồi châu Mỹ, dung lượng cơ sở dữ liệu theo làn sóng hoạt động của người chơi trên toàn cầu.

- **Dữ liệu hệ thống guild**: Quản lý các cấu trúc guild phức tạp, quyền hạn và kho đồ chia sẻ yêu cầu cập nhật và đọc thường xuyên.

- **Hệ thống giao dịch**: Xử lý các giao dịch auction house và giao dịch giữa người chơi với người chơi với hiệu suất ổn định bất kể hoạt động thị trường.

### Game mobile với sự phát triển không thể dự đoán

- **Ví dụ**: Một game mobile thông thường đột nhiên viral trên TikTok, phát triển từ 10.000 lên 1.000.000 người dùng hoạt động hàng ngày trong 48 giờ. Amazon DocumentDB Serverless tự động thích ứng mà không cần can thiệp của nhà phát triển.

- **Tính năng xã hội**: Quản lý danh sách bạn bè, hệ thống tặng quà và các tương tác xã hội có thể tăng đột biến trong các sự kiện khuyến mãi.

- **Tiến trình season pass**: Theo dõi và cập nhật tiến trình battle pass của hàng triệu người chơi đồng thời.

---

## HIỂU VỀ CÁC ĐƠN VỊ DUNG LƯỢNG AMAZON DOCUMENTDB

Khi một đợt tăng đột biến người chơi tấn công các game server của bạn, Amazon DocumentDB Serverless tự động phát hiện tải tăng và mở rộng sức mạnh tính toán và bộ nhớ. Nó đo lường việc sử dụng bằng các đơn vị dung lượng Amazon DocumentDB (DCU - DocumentDB Capacity Units). Mỗi DCU là sự kết hợp của khoảng 2 gibibyte (GiB) bộ nhớ, CPU tương ứng và mạng.

Mỗi writer hoặc reader của Amazon DocumentDB Serverless có dung lượng của chúng được đo bằng DCU. Nó được biểu diễn dưới dạng một số dấu phẩy động điều chỉnh lên hoặc xuống với việc mở rộng quy mô. Dung lượng này được cập nhật mỗi giây. Chúng tôi khuyến nghị thiết lập dung lượng tối thiểu để cho phép mỗi writer hoặc reader giữ working set của ứng dụng trong buffer pool. Điều này ngăn nội dung của buffer bị loại bỏ trong thời gian nhàn rỗi.

Trước khi thêm các instance Amazon DocumentDB Serverless vào một cluster, cluster phải có tham số ServerlessV2ScalingConfiguration được đặt. Tham số này xác định phạm vi dung lượng instance serverless với hai giá trị, MinCapacity và MaxCapacity, với phạm vi dung lượng từ 0.5256 DCU. Trong một cuộc đột kích guild lớn hoặc giải đấu, cơ sở dữ liệu của bạn có thể cần 64 DCU để xử lý tải. Trong giờ thấp điểm, nó có thể thu nhỏ xuống 0.5 DCU.

Amazon DocumentDB Serverless liên tục giám sát CPU, bộ nhớ và mức sử dụng mạng (gọi chung là tải - load) cho mỗi serverless writer hoặc reader. Điều này bao gồm cả các hoạt động cơ sở dữ liệu ứng dụng, và các tác vụ cơ sở dữ liệu nền và quản trị. Khi đạt giới hạn dung lượng hoặc phát sinh vấn đề về hiệu suất, Amazon DocumentDB Serverless tự động mở rộng quy mô để duy trì hiệu suất tối ưu. Các mức tăng mở rộng bắt đầu nhỏ đến 0.5 DCU, với dung lượng hiện tại lớn hơn cho phép các mức tăng lớn hơn và mở rộng nhanh hơn.

Khi các writer hoặc reader của Amazon DocumentDB Serverless nhàn rỗi, các instance có thể thu nhỏ xuống trạng thái nhàn rỗi là 0.5 DCU nếu MinCapacity được đặt thành 0.5. Trong trạng thái này, các tài nguyên tính toán không đủ cho hầu hết các khối lượng công việc sản xuất, nhưng các instance vẫn sẵn sàng để nhanh chóng mở rộng quy mô. Khi thoát khỏi trạng thái nhàn rỗi, các instance mở rộng trực tiếp lên ít nhất 1.02.5 DCU (hoặc MaxCapacity, nếu thấp hơn). Để cho phép thu nhỏ xuống 0.5 DCU, dung lượng instance bị giới hạn bất cứ khi nào MinCapacity là 1.0 DCU hoặc ít hơn.

Các khoản phí cho dung lượng Amazon DocumentDB Serverless được đo theo DCU giờ. Bằng cách tính phí cho mỗi lần sử dụng DCU, thay vì duy trì các instance dung lượng cao cho thời gian cao điểm, các cơ sở dữ liệu serverless điều chỉnh chi phí của chúng theo hoạt động thực tế của người chơi. Điều này giải phóng nhóm phát triển của bạn để tập trung vào việc xây dựng các tính năng game thay vì dự báo và quản lý cơ sở hạ tầng.

---

## YÊU CẦU VÀ CÁC CÂN NHẮC

Amazon DocumentDB Serverless yêu cầu các cluster đang chạy phiên bản engine 5.0.0 và nó không được hỗ trợ trong các phiên bản engine cũ hơn. Mặc dù một số tính năng Amazon DocumentDB tương thích với Amazon DocumentDB Serverless, chúng có thể gây ra các vấn đề về hiệu suất hoặc lỗi hết bộ nhớ (out-of-memory errors) nếu phạm vi dung lượng của bạn không đủ cho yêu cầu bộ nhớ của khối lượng công việc của bạn.

Các tính năng yêu cầu cài đặt MinCapacity hoặc MaxCapacity cao hơn bao gồm Performance Insights và tạo instance serverless trên các cluster có khối lượng dữ liệu lớn (bao gồm trong quá trình khôi phục cluster). Nếu bạn gặp lỗi Out-of-memory do cấu hình sai dung lượng, hãy đọc Avoiding out-of-memory errors để biết thêm thông tin. Các instance Amazon DocumentDB Serverless không hỗ trợ global clusters.

---

## DI CHUYỂN SANG SERVERLESS

Mỗi cluster Amazon DocumentDB có thể sử dụng dung lượng serverless, dung lượng được cung cấp (provisioned capacity), hoặc cả hai trong cấu hình hỗn hợp. Ví dụ: kết hợp một writer được cung cấp lớn với các reader serverless để có thông lượng ghi cao hơn, hoặc sử dụng một writer serverless với các reader được cung cấp khi ghi có thể thay đổi nhưng đọc ổn định. Cũng có thể cấu hình một cluster chỉ sử dụng serverless, bằng cách tạo một cluster serverless mới hoặc chuyển đổi dung lượng được cung cấp hiện có.

Để di chuyển sang Amazon DocumentDB Serverless, trước tiên hãy nâng cấp cluster lên phiên bản engine được hỗ trợ 5.0.0. Cấu hình mở rộng quy mô bằng cách thêm các instance serverless và tùy chọn thực hiện thao tác failover để biến một instance serverless thành cluster writer. Sau đó, bạn có thể tùy chọn chuyển đổi các instance được cung cấp sang serverless hoặc loại bỏ chúng.

Di chuyển từ MongoDB yêu cầu AWS Database Migration Service (AWS DMS) cho các di chuyển trực tuyến, thời gian ngừng hoạt động tối thiểu, hoặc các công cụ MongoDB gốc cho dump và restore ngoại tuyến. Xem lại Migrating to Amazon DocumentDB Serverless để biết hướng dẫn từng bước chi tiết và các phương pháp hay nhất.

Sau khi di chuyển, hãy làm theo Amazon DocumentDB best practices bằng cách tối ưu hóa các chỉ mục, giám sát các số liệu hiệu suất chính, thực thi kiểm soát bảo mật và chi phí. Hãy chắc chắn điều chỉnh các khối lượng công việc của bạn để xác nhận độ tin cậy, hiệu quả và khả năng mở rộng.

---

## GIÁM SÁT SỬ DỤNG SERVERLESS

Amazon DocumentDB Serverless cung cấp giám sát chi tiết thông qua các số liệu Amazon CloudWatch cập nhật mỗi giây để cung cấp cái nhìn sâu sắc thời gian thực về việc mở rộng quy mô instance và việc sử dụng tài nguyên. Thông thường, hầu hết việc mở rộng quy mô cho các instance Amazon DocumentDB Serverless đều do việc sử dụng bộ nhớ và hoạt động CPU gây ra. Ngoài ra, bạn có thể sử dụng Performance Insights để giám sát hiệu suất của các instance Amazon DocumentDB Serverless.

Amazon DocumentDB Serverless cung cấp bốn số liệu giám sát quan trọng để giúp bạn theo dõi hiệu suất và tối ưu hóa phân bổ tài nguyên:

1. **ServerlessDatabaseCapacity**: Đo lường dung lượng hiện tại của mỗi instance trong DCU, phản ánh CPU, bộ nhớ và tài nguyên mạng. Ở cấp độ cluster, nó tính trung bình dung lượng trên tất cả các instance serverless.

2. **DCUUtilization**: Đo lường phần trăm dung lượng cơ sở dữ liệu hiện tại được sử dụng so với dung lượng tối đa được cấu hình. Nếu nó gần 100%, instance đã mở rộng đến giới hạn của nó, và người dùng nên xem xét việc tăng DCU tối đa hoặc thêm nhiều instance reader hơn để cân bằng khối lượng công việc.

3. **CPUUtilization**: Biểu diễn phần trăm CPU hiện đang được sử dụng so với dung lượng CPU có sẵn theo cài đặt DCU tối đa của cluster. Nó giám sát việc sử dụng CPU liên tục và kích hoạt tự động mở rộng quy mô khi việc sử dụng luôn cao.

4. **FreeableMemory**: Biểu diễn lượng bộ nhớ không sử dụng có sẵn khi instance được mở rộng đến dung lượng tối đa của nó, tăng khoảng 2 GiB cho mỗi DCU dưới dung lượng tối đa.

---

## TÓM TẮT

Amazon DocumentDB Serverless cung cấp tính đàn hồi hợp lý mà các nhà phát triển game cần bằng cách loại bỏ việc đoán mò kích thước trước, xử lý các đợt tăng đột biến sự kiện và điều chỉnh chi phí với hoạt động người chơi hiện tại. Bằng cách tự động mở rộng quy mô dung lượng cơ sở dữ liệu dựa trên nhu cầu thực tế, Amazon DocumentDB Serverless cung cấp cho các nhà phát triển game một cách để tập trung vào việc tạo ra trải nghiệm người chơi hấp dẫn, trong khi AWS xử lý sự phức tạp của cơ sở hạ tầng cơ sở dữ liệu.

Liên hệ với AWS for Games specialist để biết chúng tôi có thể giúp đẩy nhanh doanh nghiệp của bạn như thế nào.

---

## TÀI LIỆU THAM KHẢO THÊM

- [Amazon DocumentDB Serverless is now available](https://aws.amazon.com/blogs/aws/amazon-documentdb-serverless-is-now-available/)
- [Using Amazon DocumentDB Serverless](https://docs.aws.amazon.com/documentdb/latest/developerguide/docdb-serverless.html)
- [JSON database solutions in AWS: Amazon DocumentDB (with MongoDB compatibility)](https://aws.amazon.com/blogs/database/json-database-solutions-in-aws-amazon-documentdb-with-mongodb-compatibility/)
- [Game Developer's Guide to Amazon DocumentDB Part 1: An Overview](https://aws.amazon.com/blogs/gametech/game-developers-guide-to-amazon-documentdb-part-1-an-overview/)
- [Choosing the scaling capacity range for a DocumentDB serverless cluster](https://docs.aws.amazon.com/documentdb/latest/developerguide/docdb-serverless-scaling-config.html#docdb-serverless-scaling-capacity-choosing)

---

![Jackie Jiang](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2024/07/24/Jackie-Jiang.png)

**Jackie Jiang**

Jackie Jiang là Principal Solutions Architect tại AWS. Jackie làm việc với các khách hàng game doanh nghiệp để hỗ trợ sự đổi mới của họ trên đám mây. Cô tận dụng hơn 20 năm kinh nghiệm xuyên ngành để giúp khách hàng của mình biến tầm nhìn thành hiện thực một cách đáng tin cậy, có thể mở rộng và tiết kiệm chi phí.

![Douglas Bonser](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/Douglas-Bonser.png)

**Douglas Bonser**

Douglas Bonser là Senior DocumentDB Specialist Solutions Architect. Ông mang đến hơn 30 năm làm việc rộng rãi với các công nghệ cơ sở dữ liệu NoSQL và quan hệ. Douglas thích giúp khách hàng giải quyết vấn đề và hiện đại hóa ứng dụng của họ bằng cách sử dụng công nghệ cơ sở dữ liệu NoSQL.

![Matthew Nimmo](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/06/Matthew-Nimmo.png)

**Matthew Nimmo**

Matthew Nimmo là Solutions Architect cho Game Tech tại AWS. Là cả một chuyên gia công nghệ và game thủ nhiệt tình, ông giúp các studio game tận dụng công nghệ đám mây để giải quyết các thách thức phức tạp và tạo ra trải nghiệm người chơi tốt hơn.
