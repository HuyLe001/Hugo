---
title: "Làm cho các Sản phẩm SaaS dễ Tiếp cận trong AWS Marketplace"
date: "2025-09-11"
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Thông tin dưới đây chỉ mang tính chất tham khảo. Vui lòng không sao chép nguyên văn cho báo cáo của riêng bạn, bao gồm cả cảnh báo này.
{{% /notice %}}

# LÀM CHO CÁC SẢN PHẨM SAAS DỄ TIẾP CẬN TRONG AWS MARKETPLACE

**Bài viết gốc**: [Making SaaS products accessible in AWS Marketplace](https://aws.amazon.com/vi/blogs/awsmarketplace/making-saas-products-accessible-in-aws-marketplace/)

**Tác giả gốc**: Len Gomes và Ricardo Oriol

**Ngày xuất bản**: 04 JUN 2025

**Người dịch**: Diệp Huy

**Ngày dịch**: 02 DEC 2025

---

## GIỚI THIỆU

Các nhà bán hàng trên [AWS Marketplace](https://aws.amazon.com/marketplace/) cung cấp các giải pháp [phần mềm dưới dạng dịch vụ (SaaS)](https://aws.amazon.com/saas/) thường tìm kiếm hướng dẫn về các tùy chọn và thực tiễn tốt nhất để cấp quyền truy cập cho người mua vào giải pháp phần mềm của họ. Để giải đáp các câu hỏi này, chúng tôi sẽ giải thích ba tùy chọn truy cập chính hiện có, giúp các nhà bán hàng thiết kế và xây dựng cơ chế truy cập cho các giải pháp SaaS của họ được liệt kê trong AWS Marketplace một cách hiệu quả.

Khi [các nhà bán hàng trên AWS Marketplace](https://docs.aws.amazon.com/marketplace/latest/userguide/user-guide-for-sellers.html) liệt kê các sản phẩm SaaS trên AWS Marketplace, họ cần đưa ra một số quyết định quan trọng ảnh hưởng đến cách người mua tương tác với giải pháp của họ. Những quyết định này không chỉ dừng lại ở việc tích hợp định giá và thanh toán mà còn bao gồm cách khách hàng sẽ truy cập sản phẩm. Bài viết này sẽ khám phá ba tùy chọn truy cập chính cho các giải pháp SaaS trong AWS Marketplace, giúp các nhà bán hàng đưa ra quyết định phù hợp với kiến trúc sản phẩm và nhu cầu khách hàng của họ. Các nhà bán hàng có thể linh hoạt triển khai bất kỳ kết hợp nào của các tùy chọn truy cập này: Họ có thể chọn hỗ trợ một, hai hoặc cả ba chế độ truy cập.

---

## SỬ DỤNG WEBSITE CỦA NHÀ BÁN HÀNG VỚI TÍCH HỢP SERVERLESS AWS MARKETPLACE

Khi sử dụng website của nhà bán hàng làm điểm truy cập chính cho sản phẩm [phần mềm dưới dạng dịch vụ (SaaS)](https://aws.amazon.com/saas/) trên AWS Marketplace, quá trình tích hợp có thể được đơn giản hóa với [giải pháp tích hợp SaaS serverless của AWS Marketplace](https://docs.aws.amazon.com/marketplace/latest/userguide/deploy-serverless-saas.html). Phương pháp này cho phép nhà bán hàng giữ nguyên cơ sở hạ tầng website hiện cónơi khách hàng đăng ký, đăng nhập và nhận hỗ trợtrong khi tận dụng khả năng triển khai tự động của AWS Marketplace.

Việc triển khai [AWS Quick Start](https://aws.amazon.com/solutions/) thiết lập các chức năng cốt lõi bao gồm xử lý đăng ký khách hàng, quản lý quyền truy cập, cập nhật quyền lợi và đo lường mức sử dụng. Nhà bán hàng vẫn kiểm soát hoàn toàn trải nghiệm khách hàng và giao diện người dùng của họ. Kiến trúc tích hợp serverless giảm thiểu công việc phát triển cần thiết cho tích hợp AWS Marketplace bằng cách xử lý phần lớn thiết lập hạ tầng thông qua các luồng công việc tự động. Trong khi website của nhà bán hàng vẫn là điểm cuối công khai để tương tác với khách hàng, backend serverless sẽ quản lý các điểm kết nối AWS Marketplace, triển khai bảo mật và các sự kiện vòng đời đăng ký. Phương pháp này kết hợp khả năng kiểm soát của website hiện có với kiến trúc serverless của AWS, giúp nhà bán hàng ra thị trường nhanh hơn trong khi vẫn duy trì mối quan hệ trực tiếp với khách hàng.

Một workshop có sẵn để giúp các nhà bán hàng triển khai Quick Start tại [Tích hợp SaaS của bạn với tài liệu tham khảo tích hợp SaaS Serverless](https://catalog.workshops.aws/mpseller/saas/integration-with-quickstart). Workshop thực hành này hướng dẫn bạn qua:

- Triển khai giải pháp tích hợp serverless
- Cấu hình thông báo [Amazon Simple Notification Service (Amazon SNS)](https://aws.amazon.com/sns/)
- Thiết lập URL đăng ký
- Kiểm tra luồng đăng ký của người mua
- Quản lý quyền lợi và đo lường

---

## SỬ DỤNG QUICK LAUNCH

[Quick Launch](https://docs.aws.amazon.com/marketplace/latest/buyerguide/saas-quick-launch.html) biến cấu hình thủ công phức tạp thành trải nghiệm tự động được tối ưu hóa, thay đổi cách các nhà bán hàng làm cho sản phẩm SaaS của họ dễ tiếp cận với người mua trong AWS Marketplace. Quick Launch sử dụng các mẫu [AWS CloudFormation](https://aws.amazon.com/cloudformation/) được cấu hình sẵn, được xác thực bởi cả nhà cung cấp phần mềm và AWS để cung cấp các triển khai an toàn và chuẩn hóa trong khi giảm độ phức tạp kỹ thuật cho khách hàng. Tự động hóa xử lý các tác vụ như cấu hình vai trò [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/), quản lý nhóm bảo mật và quyền cross-account, có nghĩa là khách hàng có thể tập trung vào việc sử dụng sản phẩm thay vì quản lý hạ tầng.

Để triển khai Quick Launch thành công, các nhà bán hàng phải có [tài khoản nhà bán hàng](https://docs.aws.amazon.com/marketplace/latest/userguide/seller-registration-process.html) và một tài khoản người mua thử nghiệm riêng biệt để xác thực đúng trải nghiệm Quick Launch. [Sản phẩm SaaS của nhà bán hàng phải được liệt kê](https://docs.aws.amazon.com/marketplace/latest/userguide/saas-create-product.html) trong AWS Marketplace với trạng thái hiển thị [Limited hoặc Public](https://docs.aws.amazon.com/marketplace/latest/userguide/saas-product-lifecycle.html) để kích hoạt cấu hình Quick Launch.

Để cấu hình Quick Launch, nhà bán hàng phải:

1. Mở sản phẩm trong [AWS Marketplace Management Portal](https://aws.amazon.com/marketplace/management/) và chọn tab Fulfillment options
2. Kích hoạt cấu hình Quick Launch và nhập URL đăng nhập hoặc đăng ký
3. Tạo mẫu AWS CloudFormation tuân theo các nguyên tắc [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc)
4. Cấu hình chi tiết mẫu AWS CloudFormation như tiêu đề, mô tả, URL [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) cho mẫu và các quyền IAM cần thiết để triển khai mẫu. Tham khảo [các chính sách IAM cần thiết cho tài khoản nhà bán hàng](https://catalog.workshops.aws/mpseller/en-US/saas/quick-launch-integration#prerequisites) để biết danh sách đầy đủ các chính sách
5. (Tùy chọn) Thêm hướng dẫn và liên kết tài liệu cho cấu hình thủ công
6. Chỉ định URL truy cập sản phẩm cho việc khởi chạy sau triển khai
7. (Tùy chọn) Cung cấp danh sách phân tách bằng dấu phẩy các tài khoản AWS trong danh sách cho phép để thử nghiệm với khả năng hiển thị Limited
8. Gửi để AWS Marketplace xem xét
9. Cập nhật khả năng hiển thị thành Public sau khi được phê duyệt

Một workshop có sẵn để giúp các nhà bán hàng triển khai Quick Launch: [Kích hoạt SaaS Quick Launch](https://catalog.workshops.aws/mpseller/en-US/saas/quick-launch-integration). Workshop thực hành này hướng dẫn các nhà bán hàng qua:

- Tạo mẫu
- Cấu hình bảo mật
- Quy trình thử nghiệm
- Thực tiễn tốt nhất phát triển mẫu
- Xác thực triển khai

---

## SỬ DỤNG AWS PRIVATELINK

Các nhà bán hàng trên AWS có thể cung cấp SaaS của họ thông qua [Amazon Virtual Private Cloud (Amazon VPC)](https://aws.amazon.com/vpc/) bằng cách [sử dụng AWS PrivateLink để cấu hình sản phẩm của họ làm dịch vụ VPC endpoint](https://docs.aws.amazon.com/marketplace/latest/userguide/privatelink.html). AWS Marketplace hỗ trợ AWS PrivateLink, một công nghệ AWS có khả năng mở rộng và độ khả dụng cao, cho phép các nhà bán hàng sử dụng mạng Amazon để cung cấp cho người mua quyền truy cập vào các sản phẩm SaaS theo mô hình nhà cung cấp và người tiêu dùng. Thông qua [VPC endpoint](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-endpoints.html), một kết nối riêng tư giữa VPC của người mua và sản phẩm của nhà bán hàng được tạo ra mà không cần truy cập qua internet hoặc thông qua thiết bị NAT, kết nối mạng riêng ảo (VPN) hoặc [AWS Direct Connect](https://aws.amazon.com/directconnect/). Phương pháp kết nối này tăng cường bảo mật cho người mua vì họ truy cập dịch vụ của nhà bán hàng thông qua mạng riêng tư của Amazon thay vì thông qua internet.

Sơ đồ sau đây là kiến trúc cho giải pháp sử dụng AWS PrivateLink.

![Kiến trúc AWS PrivateLink](https://d2908q01vomqb2.cloudfront.net/761f22b2c1593d0bb87e0b606f990ba4974706de/2025/05/19/Screenshot-2025-05-19-at-14.40.40.png)

**Hình 1**: Tài khoản nhà cung cấp phần mềm độc lập (ISV) làm nhà cung cấp và Tài khoản khách hàng làm người tiêu dùng.

Interface endpoint là điểm vào cho lưu lượng truy cập hướng đến dịch vụ được hỗ trợ bởi PrivateLink như sản phẩm AWS Marketplace. PrivateLink triển khai các giao diện mạng elastic trong VPC của khách hàng với các địa chỉ IP duy nhất từ subnet của khách hàng. Thiết kế kiến trúc này cung cấp sự cô lập mạng hoàn toàn và loại bỏ việc chồng chéo IP theo mặc định. Do đó, PrivateLink có thể được sử dụng để đưa một dịch vụ vào VPC. Các nhóm bảo mật có thể được liên kết với các giao diện mạng endpoint này để tăng cường bảo mật. AWS PrivateLink kết nối interface endpoint với Network Load Balancer được sử dụng làm front-end trong VPC của nhà cung cấp.

Để cấu hình sản phẩm SaaS khả dụng thông qua Amazon VPC endpoint, các nhà bán hàng phải:

1. Có danh sách sản phẩm SaaS ở trạng thái hiển thị Limited hoặc Public
2. Yêu cầu chứng chỉ từ [AWS Certificate Manager (ACM)](https://aws.amazon.com/acm/) cho tên DNS thân thiện với người dùng
   - Trước khi ACM cấp chứng chỉ, nó sẽ xác thực rằng nhà bán hàng sở hữu hoặc kiểm soát các tên miền trong yêu cầu chứng chỉ
   - AWS khuyến nghị các nhà bán hàng cung cấp tên DNS riêng tư mà người mua có thể sử dụng khi họ tạo VPC endpoint của họ
3. Tạo [Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancer-getting-started.html) trong [khu vực](https://docs.aws.amazon.com/glossary/latest/reference/glos-chap.html#region) nơi sản phẩm được triển khai. AWS khuyến nghị nhiều [vùng khả dụng](http://docs.aws.amazon.com/elasticloadbalancing/latest/classic/enable-disable-az.html)
4. Tạo [dịch vụ VPC endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/create-endpoint-service.html) và liên kết Network Load Balancer với dịch vụ endpoint
5. Xác minh rằng bạn có thể truy cập dịch vụ thông qua Network Load Balancer
6. Gửi sản phẩm được kích hoạt PrivateLink của bạn cho nhóm [AWS Marketplace Seller Operations](https://aws.amazon.com/marketplace/management/contact-us/) bằng cách gửi email các thông tin sau:
   - Endpoint và tài khoản AWS được sử dụng để tạo nó. Endpoint trông tương tự như thế này: com.amazonaws.vpce.us-east-1.vpce-svc-0daa010345a21646
   - Tên DNS thân thiện với người dùng. Đây là tên DNS mà người mua AWS Marketplace sử dụng để truy cập sản phẩm của nhà bán hàng
   - Tài khoản AWS được sử dụng để yêu cầu chứng chỉ và tên DNS riêng tư mà người mua sẽ sử dụng để truy cập VPC endpoint
7. Ủy quyền subdomain của tên DNS thân thiện với người dùng, chẳng hạn như api.vpce.example.com, cho các máy chủ tên được cung cấp bởi nhóm AWS Marketplace Seller Operations. Trong hệ thống DNS của nhà bán hàng, họ phải tạo một bản ghi tài nguyên name server (NS) để trỏ subdomain này đến các máy chủ tên Amazon Route 53 được cung cấp bởi nhóm AWS Marketplace Seller Operations để các tên DNS (chẳng hạn như vpce-0ac6c347a78c90f8.api.vpce.example.com) có thể phân giải công khai

Nhóm AWS Marketplace Seller Operations xác minh danh tính công ty của nhà bán hàng và tên DNS được sử dụng cho dịch vụ đang được đăng ký (chẳng hạn như api.vpce.example.com). Sau khi xác minh, tên DNS sẽ ghi đè tên DNS endpoint cơ sở mặc định.

Khi người mua AWS Marketplace đăng ký sản phẩm được kích hoạt PrivateLink và [tạo VPC endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/privatelink-access-saas.html#create-interface-endpoint-partner-service), dịch vụ sẽ được hiển thị trong Your AWS Marketplace Services trong AWS Console. Nhóm AWS Marketplace Seller Operations sử dụng tên DNS thân thiện với người dùng để dễ dàng khám phá dịch vụ khi tạo VPC endpoint. Các endpoint được hiển thị dưới dạng giao diện mạng trong các subnet. Địa chỉ IP cục bộ và tên DNS theo khu vực và vùng được gán cho các endpoint.

Với [sự ra mắt của kết nối cross-Region gốc cho AWS PrivateLink](https://aws.amazon.com/about-aws/whats-new/2024/11/aws-privatelink-across-region-connectivity/), các nhà cung cấp dịch vụ giờ đây có thể chia sẻ và tạo quyền truy cập thông qua các dịch vụ VPC endpoint trên các khu vực khác nhau. Điều này giúp các nhà cung cấp dịch vụ cung cấp các giải pháp SaaS một cách riêng tư cho đối tượng toàn cầu từ một khu vực duy nhất. Người tiêu dùng có thể sử dụng interface endpoint để kết nối với các dịch vụ được kích hoạt cross-Region, giống như cách họ kết nối với các dịch vụ trong cùng một khu vực. Kết nối cross-Region qua PrivateLink đơn giản, an toàn và có thể tùy chỉnh để phù hợp với nhiều trường hợp sử dụng khác nhau. Trong bài đăng Blog Networking & Content Delivery này được phát hành vào tháng 12 năm 2024, [Giới thiệu kết nối Cross-Region cho AWS PrivateLink](https://aws.amazon.com/blogs/networking-and-content-delivery/introducing-cross-region-connectivity-for-aws-privatelink/), các đồng nghiệp của tôi giới thiệu kết nối cross-Region cho AWS PrivateLink, bao gồm các bước để thiết lập nó.

---

## KẾT LUẬN

AWS Marketplace cung cấp cho các nhà bán hàng SaaS ba tùy chọn linh hoạt chính để cấp quyền truy cập cho người mua vào các giải pháp của họ: Cho dù chọn tính linh hoạt của website nhà bán hàng, tự động hóa được tối ưu hóa của Quick Launch hay bảo mật nâng cao của AWS PrivateLink, các nhà bán hàng có thể thiết kế chiến lược cơ chế truy cập sản phẩm của họ để tối ưu hóa trải nghiệm khách hàng và tích hợp marketplace. Bằng cách đánh giá cẩn thận các yêu cầu kỹ thuật của sản phẩm, các cân nhắc về bảo mật và mục tiêu tăng trưởng, các nhà cung cấp SaaS có thể tận dụng nhiều tùy chọn truy cập đồng thời hoặc bắt đầu với một phương pháp duy nhất để mở rộng phạm vi tiếp cận một cách hiệu quả, tối ưu hóa quá trình onboarding khách hàng và tạo trải nghiệm cung cấp phần mềm liền mạch trong AWS Marketplace.

Để biết thêm thông tin, hãy tham khảo [tài liệu Hướng dẫn nhà bán hàng AWS Marketplace](https://docs.aws.amazon.com/marketplace/latest/userguide/privatelink.html).

---

## TÀI LIỆU THAM KHẢO THÊM

- [AWS Marketplace Seller Guide](https://docs.aws.amazon.com/marketplace/latest/userguide/privatelink.html)
- [Integrate your SaaS with the Serverless SaaS Integration reference](https://catalog.workshops.aws/mpseller/saas/integration-with-quickstart)
- [Enable SaaS Quick Launch workshop](https://catalog.workshops.aws/mpseller/en-US/saas/quick-launch-integration)
- [Introducing Cross-Region Connectivity for AWS PrivateLink](https://aws.amazon.com/blogs/networking-and-content-delivery/introducing-cross-region-connectivity-for-aws-privatelink/)

---

![Len Gomes](https://d2908q01vomqb2.cloudfront.net/761f22b2c1593d0bb87e0b606f990ba4974706de/2024/12/17/Len.jpg)

**Len Gomes**

Len Gomes là Partner Solutions Architect làm việc với các công ty phần mềm hàng đầu (ISV) hợp tác với AWS trên khắp EMEA. Anh ấy giúp các đối tác thiết kế kiến trúc, tối ưu hóa và cung cấp các giải pháp dựa trên đám mây mang lại giá trị kinh doanh cho khách hàng trong khi đảm bảo sự xuất sắc kỹ thuật và các thực tiễn tốt nhất của AWS. Len có đam mê với mạng, các dịch vụ và giải pháp hybrid và edge. Trong thời gian rảnh, anh ấy thích chơi và xem bóng đá, các hoạt động ngoài trời và nướng BBQ. Anh ấy rất giỏi trong việc nướng và tự coi mình là một bậc thầy BBQ.

![Ricardo Oriol](https://d2908q01vomqb2.cloudfront.net/761f22b2c1593d0bb87e0b606f990ba4974706de/2025/05/27/roriol.jpg)

**Ricardo Oriol**

Ricardo Oriol là Partner Solutions Architect tại AWS, nơi anh ấy làm việc với các Đối tác trên khắp EMEA để cung cấp các giải pháp có tác động và có khả năng mở rộng cho Khách hàng. Trong vai trò của mình, Ricardo giúp các Đối tác khám phá và phát triển các khả năng đám mây đổi mới thúc đẩy chuyển đổi kinh doanh. Với niềm đam mê về kiến trúc đám mây và thúc đẩy tăng trưởng thông qua AWS, Ricardo tận tâm trao quyền cho Khách hàng thông qua Đối tác ở quy mô lớn. Ngoài công việc, anh ấy thích khám phá các công nghệ mới nổi, đọc sách và duy trì hoạt động thông qua các môn thể thao ngoài trời.
