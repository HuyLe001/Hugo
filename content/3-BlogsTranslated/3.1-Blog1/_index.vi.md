---
title: "Xác thực cho Game Mobile"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Thông tin dưới đây chỉ mang tính chất tham khảo. Vui lòng không sao chép nguyên văn cho báo cáo của riêng bạn, bao gồm cả cảnh báo này.
{{% /notice %}}

# XÁC THỰC CHO GAME MOBILE

**Bài viết gốc**: [Authentication for Mobile Games](https://aws.amazon.com/vi/blogs/gametech/authentication-for-mobile-games/)

**Tác giả gốc**: Carl Prescott

**Ngày xuất bản**: 04 OCT 2023

**Người dịch**: Diệp Huy

**Ngày dịch**: 02 DEC 2025

---

## GIỚI THIỆU

Xác thực người dùng và ủy quyền là một khía cạnh quan trọng của hầu như bất kỳ ứng dụng nào. Đối với game mobile nói riêng, quản lý xác thực và ủy quyền cho người chơi của bạn có thể đặt ra những thách thức độc đáo. Một số thách thức này liên quan đến việc sử dụng thiết bị di động. Những thách thức khác liên quan đến việc bảo mật nhiều hệ thống backend mà một game mobile hiện đại có thể tương tác, như máy chủ game, mạng xã hội và nhà cung cấp thanh toán.

Bài viết blog này tìm cách xác định một số thách thức đó cũng như cung cấp một số cách tiếp cận và thực hành tốt khi giải quyết chúng.

---

## XÁC THỰC VÀ ÚY QUYỀN

Trước tiên, giải thích ngắn gọn về sự khác biệt giữa xác thực (authentication) và ủy quyền (authorization).

**Xác thực (Authentication)** (thường được viết tắt là AuthN) là hành động xác nhận danh tính của người dùng hoặc hệ thống. Ví dụ: đăng nhập bằng tên người dùng và mật khẩu, quét dấu vân tay hoặc sử dụng nhận dạng khuôn mặt.

**Ủy quyền (Authorization)** (hoặc AuthZ) là quá trình xác định các quyền mà người dùng hoặc hệ thống gắn liền với một danh tính đã xác thực có, và liệu các hành động mà họ thực hiện có nên được cho phép hay từ chối.

---

## CÁC THÁCH THỨC XÁC THỰC GAME MOBILE

Một số thách thức phổ biến mà chúng tôi thấy khi triển khai xác thực và ủy quyền trong game mobile bao gồm:

### Hỗ trợ người dùng ẩn danh

Game mobile thường cho phép người chơi ẩn danh hoặc chưa xác thực chơi mà không cần tạo tài khoản. Do đó, game cần theo dõi và kiểm soát quyền truy cập của người chơi chưa xác thực cũng như liên kết họ với tài khoản đã xác thực nếu người chơi sau đó tạo tài khoản.

### Tạo quy trình đăng ký đơn giản

Việc điền form hoặc nhập nhiều thông tin người dùng trên màn hình cảm ứng di động có thể tạo sự cản trở cho người chơi mới, khiến họ cảm thấy phiền toái và bỏ cuộc hoàn toàn.

### Xác thực ngoại tuyến

Thiết bị di động có thể không luôn có kết nối Internet. Trong trường hợp này, cần thực hiện một cách tiếp cận để hỗ trợ xác thực hoặc ủy quyền cục bộ.

### Caching (lưu trữ tạm) thông tin xác thực

Cần chú ý đến thông tin xác thực được lưu trữ cục bộ để đảm bảo không thể bị truy cập trái phép. Những thông tin xác thực này có thể được sử dụng để thực hiện các hành động không được phép, ví dụ, truy cập trực tiếp vào API mà game sử dụng.

### Thao túng client (client tampering)

Các tệp nhị phân bị sửa đổi có thể được hacker hoặc cheater sử dụng để lấy thông tin xác thực bảo mật và thực hiện các hành động không mong muốn đối với game backend, hoặc tự cấp cho mình vàng hoặc kinh nghiệm trong game mà không được phép.

### Mã hóa lỗi thời hoặc không an toàn

Nhiều thiết bị di động chạy hệ điều hành đã lỗi thời mà không còn nhận các bản cập nhật bảo mật. Điều này có thể dẫn đến việc sử dụng mật mã (cryptography) yếu hoặc các vấn đề bảo mật khác.

### Lưu lượng người chơi tăng đột biến hoặc không thể dự đoán

Ra mắt game, sự kiện trong game, khuyến mãi trong các cửa hàng game mobile, hoặc thậm chí hoạt động trên mạng xã hội có thể dẫn đến sự gia tăng đáng kể trong ngắn hạn về lưu lượng truy cập, có thể tạm thời làm quá tải các dịch vụ xác thực.

---

Xác thực và ủy quyền có thể là một chủ đề phức tạp. Có những hậu quả nghiêm trọng nếu chúng không được triển khai đúng cách, vì vậy có thể nên sử dụng dịch vụ Identity-as-a-Service (IDaaS) của bên thứ ba để đảm nhiệm chức năng chính. Một số cân nhắc trong lĩnh vực này được khám phá trong phần tiếp theo.

---

## ĐIỀU CẦN TÌM KIẾM TRONG MỘT GIẢI PHÁP XÁC THỰC

### Bảo mật

Về cơ bản, một hệ thống xác thực sẽ cung cấp bảo mật cho tài khoản của người chơi. Một giải pháp phải hỗ trợ các cơ chế mã hóa hiện đại, cả cho dữ liệu ở trạng thái nghỉ (at rest) và trong quá trình truyền (in transit). HTTPS là bắt buộc, và bạn nên kiểm tra phiên bản TLS (bạn không nên sử dụng bất kỳ thứ gì thấp hơn TLS v1.2). iOS có App Transport Security ngăn chặn mọi kết nối ra ngoài sử dụng bất kỳ thứ gì thấp hơn TLS v1.2. Android có khả năng tương tự nhưng điều này có thể bị ghi đè.

Tìm hiểu cách dữ liệu người chơi của bạn được lưu trữ trong hệ thống xác thực - mật khẩu không nên được lưu trữ trực tiếp, và bất kỳ giá trị hash nào cũng nên được salted và hashed.

### Trải nghiệm người dùng

Một hệ thống xác thực nên cung cấp trải nghiệm người dùng tốt, cả cho nhà phát triển và người chơi. Việc đăng ký, đăng nhập và đặt lại mật khẩu nên dễ dàng. Tích hợp đăng nhập xã hội, cho các nền tảng như Facebook, Twitter, Apple ID hoặc các nền tảng khác, có thể làm cho quy trình đăng ký và đăng nhập đơn giản hơn cho người chơi cũng là điều cần xem xét.

### Khả năng mở rộng

Hệ thống nên có khả năng mở rộng để đáp ứng các yêu cầu đỉnh điểm. Nếu bạn có một đợt ra mắt thành công, hoặc một sự kiện nào đó thu hút nhiều người dùng (hiện có hoặc mới) đến game của bạn, bạn cần tự tin rằng hệ thống xác thực có thể mở rộng để đáp ứng nhu cầu đăng nhập và đăng ký.

Đối với các dịch vụ được lưu trữ, hãy tìm kiếm quota/giới hạn API, và đối với các hệ thống tại chỗ (on premises), hãy xem xét cách cơ sở hạ tầng sẽ cần được định kích thước để đáp ứng nhu cầu đỉnh điểm. Lập kế hoạch cho các đỉnh điểm vượt quá các mẫu lưu lượng bình thường của bạn. Ví dụ: nếu game của bạn được liệt kê tự nhiên trong bảng xếp hạng New Games hoặc Most Downloaded của Google Play hoặc Apple App Store, điều này có thể dẫn đến lưu lượng người chơi bổ sung đáng kể.

### Hỗ trợ đa nền tảng

Nếu bạn cần hỗ trợ đa nền tảng, hãy tìm kiếm các hệ thống hỗ trợ chức năng cross-platform cho phép người chơi sử dụng cùng một tài khoản trên các thiết bị khác nhau. Điều này bao gồm việc xem xét các SDK nào có sẵn cho các nền tảng như iOS và Android, và cho các ngôn ngữ lập trình như C# và JavaScript.

### Luồng xác thực (Authentication flows)

Bạn cũng sẽ cần suy nghĩ về các luồng xác thực mà bạn muốn sử dụng. Bạn có cần sử dụng các luồng OAuth/OpenID như authentication code hoặc device grant không? Bạn có muốn triển khai luồng không cần mật khẩu (passwordless), chẳng hạn như dấu vân tay hoặc nhận dạng khuôn mặt không?

### Tùy chỉnh

Xem xét các tùy chọn tùy chỉnh của hệ thống. Bạn có thể muốn xây dựng trang đăng ký hoặc đăng nhập tùy chỉnh, hoặc sử dụng trang được xây dựng sẵn do hệ thống cung cấp. Nó nên tích hợp với các hệ thống khác lưu giữ dữ liệu người chơi có liên quan và bạn nên xem xét các tùy chọn nào có sẵn nếu bạn cần tùy chỉnh luồng xác thực hoặc giao diện.

### Phân tích và báo cáo

Kiểm tra khả năng phân tích và báo cáo để xem bạn có thể có được cái nhìn sâu sắc gì từ hành vi người chơi. Bạn có thể xem lại các mẫu đăng nhập, xác định hoạt động đáng ngờ và sử dụng thông tin này để cải thiện bảo mật game của bạn không?

### Mô hình chi phí

Đảm bảo bạn hiểu mô hình chi phí và chọn phương án phù hợp nhất cho khối lượng dự kiến của bạn. Có các tùy chọn cho phép bạn trả tiền cho những gì bạn sử dụng (ví dụ: cho mỗi yêu cầu đăng nhập/đăng xuất, hoặc theo số lượng tài khoản được tạo), và các hệ thống khác yêu cầu đầu tư trước. Mỗi tùy chọn đều có ưu và nhược điểm của nó. Phương án phù hợp nhất sẽ phụ thuộc vào ngân sách, khối lượng dự kiến và khẩu vị rủi ro của bạn.

### Tuân thủ (Compliance)

Nếu bạn có yêu cầu tuân thủ để tuân theo, chẳng hạn như bảo vệ dữ liệu hoặc xác minh độ tuổi, hãy đảm bảo hệ thống xác thực tuân thủ, hoặc cho phép bạn xây dựng giải pháp tuân thủ với việc triển khai đúng đắn.

---

## CÁC THỰC HÀNH TỐT

Một số thực hành tốt chính khác cần tuân theo khi lập kế hoạch cho cách tiếp cận xác thực và ủy quyền của bạn cho game mobile:

### Sử dụng cơ chế bảo vệ do cửa hàng ứng dụng cung cấp

Google cung cấp **Play Integrity API** và Apple cung cấp **DeviceCheck**, cả hai bạn đều có thể sử dụng để đảm bảo người chơi đang sử dụng tệp nhị phân game chính hãng, chưa bị sửa đổi để truy cập tài nguyên máy chủ backend của bạn.

### Tận dụng phần tử bảo mật phần cứng của thiết bị

Để lưu trữ cục bộ bất kỳ bí mật mật mã hoặc thông tin xác thực được lưu trong bộ nhớ cache, hãy tận dụng phần tử bảo mật phần cứng (hardware secure element) của thiết bị. Đối với Android, bạn nên sử dụng **Keystore**, và đối với iOS, bạn nên sử dụng **Keychain**.

### Xác thực định kỳ với dịch vụ backend

Đảm bảo bạn xác thực định kỳ với các dịch vụ backend của mình. Đôi khi bạn có thể cần tin tưởng thông tin xác thực được lưu trong cache (ví dụ: khi người dùng không có kết nối internet), nhưng bạn nên tránh tin tưởng xác thực chỉ cục bộ trong thời gian dài.

### Xem xét xác thực hai yếu tố (2FA)

Xem xét việc sử dụng xác thực hai yếu tố (2FA) cho các hành động yêu cầu mức độ ủy quyền cao hơn, chẳng hạn như mua hàng trong ứng dụng hoặc thay đổi dữ liệu người dùng. Điều này có thể liên quan đến việc gửi mã đến email hoặc số điện thoại đã biết để người dùng nhập trong game. Ngoài ra, bạn có thể triển khai step-up auth bằng cách sử dụng chức năng sinh trắc học của thiết bị, chẳng hạn như dấu vân tay hoặc face ID.

### Sử dụng external user agents cho OAuth 2.0

Các yêu cầu OAuth 2.0 nên được thực hiện thông qua external user agents, chẳng hạn như trình duyệt của thiết bị, thay vì trực tiếp từ game client. Điều này ngăn ứng dụng host (hoặc bất kỳ ứng dụng đã sửa đổi nào) có thể sao chép hoặc trích xuất thông tin xác thực người dùng và cookie, và giảm nhu cầu người dùng phải xác thực riêng trong mỗi ứng dụng họ sử dụng.

### Không lưu trữ PII trong authentication token

Đừng lưu trữ bất kỳ Thông tin nhận dạng cá nhân (PII - Personally Identifiable Information) nào trong các token xác thực. Token được ký nhưng không nhất thiết được mã hóa, vì vậy chúng có thể dễ dàng đọc được. Bao gồm PII bên trong một token có thể dẫn đến dữ liệu nhạy cảm bị lộ vô tình.

---

## LUỒNG XÁC THỰC MẪU

![Example authentication flow](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2023/09/29/mobileauth-1.png)

**Hình 1**: Luồng xác thực mẫu.

Hình 1 minh họa một luồng xác thực cấp cao. Các bước liên quan như sau:

1. Người dùng ứng dụng di động xác thực với nhà cung cấp danh tính (identity provider) đã chọn của họ (chẳng hạn như Google, Apple, Facebook hoặc các nhà cung cấp khác) và nhận lại một token.

2. Token này được gửi đến dịch vụ identity, dịch vụ này kiểm tra xem chúng có đáng tin cậy hay không, và nếu có, một token được trả về cho ứng dụng có thể được sử dụng để đăng nhập người dùng vào ứng dụng.

3. Tùy chọn, token sau đó được sử dụng để ủy quyền cho ứng dụng thực hiện các cuộc gọi đến các dịch vụ backend.

---

## KẾT LUẬN

Tóm lại, chúng tôi đã thảo luận về sự khác biệt giữa xác thực (hành động xác nhận danh tính) và ủy quyền (cung cấp quyền truy cập vào tài nguyên). Chúng tôi cũng đã khám phá các thách thức chính của xác thực game mobile, những gì cần tìm kiếm trong giải pháp xác thực của bên thứ ba và một số thực hành tốt.

Trong bài viết blog tiếp theo trong loạt bài này, chúng tôi sẽ xem xét cách bạn có thể sử dụng các dịch vụ AWS, chẳng hạn như Amazon Cognito, để xây dựng xác thực vào game mobile của bạn.

Để biết thêm thông tin, hãy xem các tài nguyên sau:

- AWS Well Architected Framework Games Industry Lens [identity and access management section](https://docs.aws.amazon.com/wellarchitected/latest/games-industry-lens/games-sec-bp-iam.html)
- [Guidance for Custom Game Backend Hosting on AWS](https://aws.amazon.com/solutions/guidance/custom-game-backend-hosting-on-aws/?did=sl_card&trk=sl_card)
- [Using Amazon Cognito to authenticate players for a game backend service](https://aws.amazon.com/blogs/gametech/using-amazon-cognito-to-authenticate-players-for-a-game-backend-service/)

---

**Tác giả blog:**
- Carl Prescott  AWS Games Solutions Architect
- James Thompson  AWS Senior Solutions Architect

---

![Carl Prescott](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2024/09/26/Carl-Prescott.jpg)

**Carl Prescott**

Carl Prescott là Solutions Architect tập trung vào các khách hàng và use case trong lĩnh vực gaming tại AWS. Anh bắt đầu chơi game trên máy Commodore Plus/4 từ rất nhiều năm trước và gần như chưa bao giờ thực sự dừng lại. Carl mang niềm đam mê của mình với ngành công nghiệp này vào vai trò của mình, nơi anh giúp các nhà phát triển game Build, Run và Grow game của họ trên cloud bằng cách sử dụng nhiều dịch vụ đa dạng mà AWS cung cấp.
