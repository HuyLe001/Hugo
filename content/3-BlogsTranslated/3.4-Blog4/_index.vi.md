---
title: "Theo dõi Tình trạng Máy chủ với Máy chủ Amazon GameLift"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Thông tin dưới đây chỉ mang tính chất tham khảo. Vui lòng **không sao chép nguyên văn** cho báo cáo của riêng bạn, bao gồm cả cảnh báo này.
{{% /notice %}}

# THEO DÕI TÌNH TRẠNG MÁY CHỦ VỚI MÁY CHỦ AMAZON GAMELIFT

**Bài viết gốc**: [Monitoring server health with Amazon GameLift Servers](https://aws.amazon.com/vi/blogs/gametech/monitoring-server-health-with-amazon-gamelift-servers/)

**Tác giả gốc**: Brian Schuster - Principal Engineer, AWS GameLift

**Ngày xuất bản**: 20 NOV 2025

**Người dịch**: Diệp Huy

**Ngày dịch**: 02 DEC 2025

---

## GIỚI THIỆU

Vận hành một game multiplayer thành công đồng nghĩa với việc liên tục cân bằng giữa hiệu suất, khả năng mở rộng và trải nghiệm người chơi. Khi cơ sở người chơi của bạn phát triển, những thách thức mới sẽ xuất hiện. Nguyên nhân có thể là bất kỳ vấn đề nào trong số nhiều vấn đề khác nhau. Có thể đó là một vấn đề trong code máy chủ của bạn. Có thể có rò rỉ bộ nhớ (memory leak), logic không hiệu quả hoặc lỗi chỉ xuất hiện trong những điều kiện cụ thể.

Ngoài ra, việc tối ưu hóa độ trễ (latency) bằng cách sử dụng Amazon GameLift Servers thông qua việc đặt dung lượng một cách chiến lược trên các Region, xác minh người chơi kết nối với các máy chủ gần họ nhất cũng rất quan trọng. Tuy nhiên, ngay cả khi đã tối ưu hóa độ trễ, bạn vẫn có thể nhận được khiếu nại từ người chơi về hiệu suất kém hoặc gameplay giảm chất lượng từ một nhóm người chơi nhất định.

Chúng tôi đã đề cập trước đó về cách chẩn đoán và giải quyết các vấn đề mạng rộng hơn, nhưng các số liệu độ trễ đơn thuần sẽ không cung cấp cho bạn toàn bộ bức tranh. Bạn cần khả năng hiển thị sâu hơn về những gì đang xảy ra trên các game server của mình.

Đây là nơi mà các số liệu telemetry của Amazon GameLift Servers có thể giúp ích.

---

## VƯỢT QUA ĐỘ TRỄ: KHẢ NĂNG QUAN SÁT PHÍA MÁY CHỦ

Khi sử dụng Amazon GameLift Servers với telemetry được bật, các game server của bạn sẽ thu thập nhiều loại số liệu chi tiếtbao gồm mức sử dụng tài nguyên (như CPU, bộ nhớ và mạng), các số liệu đặc thù cho game (như tick rate) và các số liệu tùy chỉnh mà bạn xác định. Các số liệu này được thu thập với các chiều (dimensions) và mức độ tổng hợp khác nhau, do đó bạn có thể phân tích hiệu suất ở cấp độ process, container, host và toàn bộ fleet.

Các số liệu sẽ chuyển vào kho số liệu (metrics warehouse) mà bạn lựa chọn và có thể được hiển thị bằng các công cụ và dịch vụ ưa thích của bạn.

Chúng tôi sẽ trình diễn bằng cách sử dụng Amazon Managed Grafana với các dashboard được xây dựng sẵn. Việc thiết lập được sắp xếp hợp lý và có thể hoàn thành trong vòng chưa đầy một giờ.

Sức mạnh thực sự không chỉ nằm ở bản thân các số liệu, mà còn ở cách các dashboard giúp bạn nhanh chóng xác định và chẩn đoán các vấn đề.

---

## KHẮC PHỤC SỰ CỐ MÁY CHỦ GAME BỊ CRASH

Hãy bắt đầu với một tình huống phổ biến: Các phiên game đang bị crash. Người chơi đang bị ngắt kết nối giữa trận đấu và bạn cần tìm hiểu tại sao.

Nếu bạn chưa thiết lập dashboard giám sát, hãy làm theo tài liệu Configure Amazon Grafanachỉ mất vài phút để cung cấp các dashboard được xây dựng sẵn cho fleet của bạn. Lưu ý rằng chúng tôi đang làm theo các bước C++ SDK được liên kết từ tài liệu Implementation, hãy điều chỉnh cho tùy chọn triển khai mà bạn đã chọn.

Sau khi cấu hình xong, hãy mở Amazon Managed Grafana từ AWS Management Console và điều hướng đến dashboard EC2 Fleet Overview. Hình 1 cho thấy một sự kiện crash trong biểu đồ Game Server Crashes, trong khi phần Crashed Game Sessions hiển thị chi tiết về phiên game cụ thể đã bị crash. Cả instance và phiên game đã bị crash đều được liên kết một cách thuận tiện để cho phép điều tra sâu hơn.

![Fleet Overview dashboard displaying game session crash information.](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/SH-Image-1.png)

**Hình 1**: Dashboard EC2 Fleet Overview hiển thị phiên game bị crash.

Chọn instance bị ảnh hưởng bằng cách nhấp vào nó. Biểu đồ bộ nhớ (Hình 2) minh họa câu chuyện: việc sử dụng bộ nhớ tăng đột ngột, sau đó giảm khi process bị crash. Đây là dấu hiệu của rò rỉ bộ nhớ (memory leak). Nhìn vào phân tích cấp session, bạn có thể thấy rằng một phiên game có mức sử dụng bộ nhớ cao hơn đáng kể.

![Instance Performance dashboard showing memory leak.](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/SH-Image-2.png)

**Hình 2**: Dashboard Instance Performance hiển thị rò rỉ bộ nhớ.

Nhấp vào phiên game bị crash đưa chúng ta đến dashboard Server Performance (Hình 3), dashboard này hiển thị mức tiêu thụ của phiên game cho đến thời điểm bị crash. Dashboard minh họa rằng phiên game bị crash chính là phiên chịu trách nhiệm cho rò rỉ bộ nhớ.

![Server Performance dashboard showing memory leak.](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/SH-Image-3.png)

**Hình 3**: Dashboard Server Performance hiển thị rò rỉ bộ nhớ.

Mỗi biểu đồ đều bao gồm các tooltip hữu ích giải thích những gì cần tìm kiếm và cách diễn giải dữ liệu. Trong trường hợp này, bước tiếp theo rất rõ ràng: điều tra các log của phiên game bị crash để xác định điều gì đã kích hoạt rò rỉ. Điều này có thể giúp bạn xác định xem đó có phải là một chế độ game cụ thể hay có thể là từ hành động của một người chơi cụ thể. Các số liệu giúp bạn chỉ ra đúng các log cần kiểm tra.

---

## KHẮC PHỤC SỰ CỐ SỬ DỤNG CPU CAO

Hãy xem xét một tình huống khác: Người chơi đang báo cáo gameplay bị giật lag, nhưng không có crash. Vấn đề có thể liên quan đến CPU.

Chuyển sang dashboard EC2 Instances Overview trong Amazon Managed Grafana. Hình 4 hiển thị 20 instance EC2 hàng đầu theo mức tiêu thụ CPU. Hầu hết các instance dao động khoảng 2-3% mức sử dụng CPU, nhưng một vài instance đang hiển thị ở mức 20-30% hoặc cao hơn.

![EC2 Instances Overview dashboard.](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/SH-Image-4.png)

**Hình 4**: Dashboard EC2 Instances Overview.

Chọn một trong các instance có CPU cao. Dashboard sẽ phân tích mức sử dụng CPU theo phiên game (Hình 5) và ngay lập tức chỉ ra session nào đang tiêu thụ nhiều tài nguyên nhất. Sau đó, bạn có thể tham khảo các log của phiên game cho session cụ thể đó, tập trung vào giai đoạn có mức sử dụng CPU cao.

![Instance Performance dashboard showing top CPU consuming game sessions.](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/SH-Image-5.png)

**Hình 5**: Dashboard Instance Performance hiển thị các phiên game tiêu thụ CPU hàng đầu.

Có thể bạn phát hiện ra rằng CPU cao có liên quan đến các tình huống chiến đấu căng thẳng, hoặc có thể có lỗi tìm đường (pathfinding) gây ra các phép tính quá mức. Mặc dù các số liệu đơn thuần không cho bạn biết chính xác điều gì đã sai, nhưng chúng cho bạn biết chính xác nơi cần tìm kiếm.

---

## HỖ TRỢ CONTAINER

Nếu bạn đang chạy Amazon GameLift Servers Fleet của mình với container thay vì các instance EC2, thì cách tiếp cận khắc phục sự cố tương tự vẫn áp dụng. Hình 6 cho thấy dashboard Container Fleet Overview, hiển thị các task hàng đầu theo mức tiêu thụ CPU hoặc bộ nhớ.

![Container Fleet Overview dashboard.](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/SH-Image-6.png)

**Hình 6**: Dashboard Container Fleet Overview.

Nhấp vào một task cụ thể, và dashboard Container Performance sẽ phân tích các số liệu theo từng container riêng lẻ trong task đó (Hình 7). Bạn có thể xem liệu container game server (Container1 trong trường hợp này) có đang tiêu thụ tài nguyên như mong đợi hay không, hoặc liệu một sidecar container có đang gây ra vấn đề hay không. Độ chi tiết này giúp bạn cô lập các vấn đề một cách nhanh chóng, cho dù bạn đang chạy trên EC2 hay container.

![Container Performance dashboard.](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/SH-Image-7.png)

**Hình 7**: Dashboard Container Performance.

---

## CÁC BƯỚC TIẾP THEO

Trong khi các số liệu tích hợp sẵn bao gồm hiệu suất phần cứng và các số liệu game chung (như tick rate và crashes), bạn có thể mở rộng giám sát hơn nữa. Các chỉ báo sức khỏe đặc thù cho game có thể được thu thập bằng cách sử dụng custom metrics như được mô tả trong tài liệu Custom metrics.

Hãy xem xét việc theo dõi các số liệu như:

- **Combat balance**: Thời gian trung bình để tiêu diệt (time-to-kill) hoặc sát thương mỗi giây (damage-per-second) trên các loại vũ khí để phát hiện xem một bản vá cân bằng gần đây có làm cho một số vũ khí trở nên quá mạnh hay không.

- **Progression blockers**: Tỷ lệ thành công cho các nhiệm vụ quan trọng hoặc các cuộc chiến với boss để xác định xem có lỗi nào đang ngăn người chơi tiến triển hay không.

- **Economy health**: Tỷ lệ lạm phát tiền tệ hoặc các mẫu thu thập vật phẩm để phát hiện các lỗi khai thác trước khi chúng làm mất ổn định nền kinh tế trong game của bạn.

- **AI pathfinding duration**: Thời gian dành cho việc tính toán đường đi của NPC để phát hiện xem các tình huống phức tạp có đang gây ra vấn đề hiệu suất hay không.

Sau khi bạn đã thiết lập các số liệu tùy chỉnh phù hợp với game của mình, hãy thiết lập cảnh báo (alerts) trong Amazon Managed Grafana cho cả ngưỡng hệ thống và ngưỡng đặc thù cho game. Thêm cảnh báo cho việc sử dụng bộ nhớ trên 90%, sử dụng CPU duy trì trên 85%, tăng các session bị crash, hoặc các bất thường khác trong các số liệu tùy chỉnh của bạn (chẳng hạn như tăng đột ngột các lần thử đánh boss thất bại). Khi một cảnh báo kích hoạt, bạn có thể nhấp trực tiếp vào dashboard liên quan và bắt đầu điều traphát hiện các lỗi hồi quy trước khi chúng xuất hiện trên mạng xã hội.

---

## KẾT LUẬN

Tối ưu hóa độ trễ có thể kết nối người chơi đến đúng vị trí, nhưng khả năng quan sát phía máy chủ (server-side observability) xác nhận rằng họ có trải nghiệm mượt mà khi họ đã vào game. Các số liệu telemetry của Amazon GameLift Servers, cùng với các dashboard được xây dựng sẵn, cung cấp khả năng hiển thị cần thiết để nhanh chóng chẩn đoán các crash, các điểm nghẽn hiệu suất và các vấn đề về tài nguyênmà không bị chìm ngập trong các số liệu thô.

Lần sau khi một người chơi phàn nàn về trải nghiệm bị lỗi, bạn sẽ biết chính xác nơi cần tìm kiếm, và với cảnh báo chủ động, bạn sẽ phát hiện vấn đề trước khi họ nhận thấy.

Liên hệ với AWS Representative để biết chúng tôi có thể giúp đẩy nhanh doanh nghiệp của bạn như thế nào.

---

## TÀI LIỆU THAM KHẢO THÊM

- [Getting started with Amazon GameLift Servers](https://aws.amazon.com/gamelift/servers/getting-started/)
- [Setting up alerts in Amazon Managed Grafana](https://docs.aws.amazon.com/grafana/latest/userguide/alerts-overview.html)
- [Available Amazon GameLift Servers dashboards and metrics](https://docs.aws.amazon.com/gameliftservers/latest/developerguide/gamelift-servers-metrics-dashboards.html)

---

![Brian Schuster](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/01/28/Brian-Schuster.jpg)

**Brian Schuster**

Brian Schuster là Principal Engineer tại AWS cho Amazon GameLift, nơi ông làm việc để định hình hướng đi kỹ thuật của dịch vụ. Ông có sự tập trung sâu sắc vào việc thúc đẩy cải tiến trong các lĩnh vực về tính khả dụng (availability) và khả năng mở rộng (scalability) để hỗ trợ các yêu cầu khắt khe nhất của các game quy mô lớn.
