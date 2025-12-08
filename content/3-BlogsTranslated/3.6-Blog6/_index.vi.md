---
title: "Wicked Saints Studios Tích hợp TikTok vào World Reborn sử dụng AWS"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 3.6. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Thông tin dưới đây chỉ mang tính chất tham khảo. Vui lòng **không sao chép nguyên văn** cho báo cáo của riêng bạn, bao gồm cả cảnh báo này.
{{% /notice %}}

# WICKED SAINTS STUDIOS TÍCH HỢP TIKTOK VÀO WORLD REBORN SỬ DỤNG AWS

**Bài viết gốc**: [Wicked Saints Studios integrates TikTok within World Reborn using AWS](https://aws.amazon.com/vi/blogs/gametech/wicked-saints-studios-integrates-tiktok-within-world-reborn-using-aws/)

**Tác giả gốc**: Matthew Nimmo

**Ngày xuất bản**: 11 NOV 2025

**Người dịch**: Diệp Huy

**Ngày dịch**: 02 DEC 2025

---

## GIỚI THIỆU

Đối mặt với việc tích hợp chức năng TikTok vào game mobile mới của họ, World Reborn, Wicked Saints Studios gặp phải một tình thế khó xử. Các giải pháp thị trường hiện có hoặc là quá đắt, tốn thời gian để triển khai, hoặc hoàn toàn thiếu tích hợp TikTok. Để đáp ứng thời hạn gấp rút của mình, đồng thời duy trì hiệu quả chi phí, studio đã phát triển một giải pháp sáng tạo bằng cách xây dựng dựa trên hướng dẫn hiện có của [Amazon Web Services (AWS)](https://aws.amazon.com/).

---

## BỐI CẢNH TÍCH HỢP TIKTOK TRONG NGÀNH GAME

TikTok đã cách mạng hóa việc chia sẻ nội dung game thông qua định dạng video ngắn. Các chiến lược marketing hiện nay đang nhấn mạnh vào nội dung hậu trường chân thực, điều này phù hợp với phong cách của TikTok. Do đó, các studio đang triển khai chức năng "Share to TikTok" trực tiếp cho các thành tích và chiến thắng.

---

## TRIỂN KHAI CỦA WICKED SAINTS

Wicked Saints, được thành lập vào năm 2021 như một công ty game mobile khởi nghiệp, đang chuẩn bị cho đợt ra mắt chính thức của World Reborn vào năm tới. Gần đây, họ đã sử dụng [Guidance for Custom Game Backend Hosting on AWS](https://aws.amazon.com/solutions/guidance/custom-game-backend-hosting-on-aws/) để khởi động giải pháp backend của họ cho xác thực người dùng. Giải pháp này cung cấp một framework đã được thử nghiệm thực tế, sẵn sàng sử dụng, tích hợp liền mạch vào cơ sở hạ tầng backend hiện có của họ.

Guidance for Custom Game Backend Hosting on AWS cung cấp một framework toàn diện để xây dựng các game backend có khả năng mở rộng. Nó cung cấp chuyên môn trong quản lý người chơi, xác thực, triển khai toàn cầu và hoạt động live service. Giải pháp nhấn mạnh vào việc xây dựng các hệ thống có thể xử lý mọi thứ từ game mobile bình thường đến trải nghiệm multiplayer quy mô lớn. Nó tập trung vào quản lý người chơi, kiến trúc có khả năng mở rộng và phạm vi toàn cầu. Wicked Saints đã mở rộng giải pháp này để bao gồm tích hợp TikTok.

---

## CÁC THÁCH THỨC GẶP PHẢI TRONG QUÁ TRÌNH TÍCH HỢP

Wicked Saints gặp phải một số thách thức trong quá trình tích hợp TikTok:

1. **Deep link encoding và giới hạn kích thước state**: Nhóm phải giữ state tối thiểu và được ký để hoạt động trong các ràng buộc của TikTok.

2. **Redirect allowlist mismatches**: Đảm bảo đồng bộ hóa giữa cài đặt ứng dụng TikTok và hostname runtime đòi hỏi cấu hình cẩn thận.

3. **Thời gian phê duyệt kéo dài**: Việc có được quyền truy cập API production từ TikTok liên quan đến một quy trình phê duyệt dài.

4. **Tối ưu hóa trải nghiệm người dùng**: Duy trì trải nghiệm người dùng sạch sẽ và liền mạch, đồng thời tuân thủ các hướng dẫn của TikTok tỏ ra khó khăn.

---

## TỔNG QUAN KIẾN TRÚC

![Wicked Saints Studios Architecture](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/06/WS-Image-1.png)

**Hình 1**: Kiến trúc tổng quan.

Hướng dẫn kiến trúc cấp cao của Wicked Saints:

- Người chơi kết nối thông qua [Amazon Route 53](https://aws.amazon.com/route53/), đi qua [Amazon CloudFront](https://aws.amazon.com/cloudfront/) và đến [Amazon API Gateway](https://aws.amazon.com/api-gateway/).

- Để bảo vệ chống lại các cuộc tấn công độc hại, [AWS WAF](https://aws.amazon.com/waf/) được sử dụng để bảo vệ API Gateway.

- Từ đó, người chơi có thể làm mới access token, đăng nhập bằng Google và hiện tại đăng nhập bằng TikTok thông qua [AWS Lambda](https://aws.amazon.com/lambda/).

- Tất cả secrets (ví dụ: thông tin xác thực ứng dụng TikTok) được lưu trữ trong [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) và tất cả metadata liên quan đến mục đích đăng nhập được lưu trữ trong [Amazon DocumentDB](https://aws.amazon.com/documentdb/).

- [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) lưu trữ bất kỳ nội dung game nào có tính chất tĩnh, chẳng hạn như tài sản nghệ thuật.

---

## ÁNH XẠ FRAMEWORK AWS SANG PROVIDER TIKTOK

Wicked Saints bắt đầu từ luồng mẫu Google Play được cung cấp trong Guidance for Custom Game Backend Hosting on AWS và sao chép mẫu đó. Token exchange trong backend là cần thiết vì lý do bảo mật từ TikTok, vì họ sử dụng OAuth để người dùng có thể được xác thực đúng cách với TikTok.

Trong khi các tùy chọn đăng nhập khác đã có phương tiện sẵn có, Wicked Saints phải tạo mẫu đăng nhập tùy chỉnh của riêng họ cho TikTok bằng HTTP, sao chép các ví dụ hiện có trong hướng dẫn AWS. Là một phần của quá trình token exchange này, Wicked Saints cần giữ mọi thứ an toàn bằng cách mã hóa token. Token được mã hóa này được lưu trữ trong Secrets Manager, và khóa được mã hóa được giữ trong Amazon DocumentDB.

Tất cả các use case được thể hiện bởi các tính năng đăng nhập hiện có do hướng dẫn giải pháp tiêu chuẩn cung cấp đều được phản ánh với phần mở rộng TikTok mới được ánh xạ này. Các tình huống này bao gồm liên kết với tài khoản hiện có, đăng nhập vào tài khoản hiện có và tạo tài khoản mới và liên kết với provider.

---

## TRIỂN KHAI OAUTH FLOW

Tất cả các phần code sau đây mô tả cách Wicked Saints thực hiện tích hợp TikTok của họ. Code không nhằm mục đích quy định, mà để được điều chỉnh để tạo tích hợp TikTok với các game mobile của riêng bạn.

Phần code đầu tiên minh họa cách Wicked Saints xây dựng token exchange. Đầu tiên có một server endpoint \GET /tiktok/login?redirectUrl={redirectUrl}\ được gọi bởi client. \PlayerId\ và \IsLinking\ là những thứ Wicked Saints đặt ra để theo dõi xem có người dùng hiện có hay không đang đăng nhập qua TikTok.

Đây không phải là yêu cầu với TikTok, mà là một cách để xem liệu người dùng gọi endpoint đăng nhập TikTok đã đăng nhập vào World Reborn chưa. Nếu đúng như vậy, giải pháp liên kết tài khoản người chơi của họ với tài khoản TikTok của họ. Wicked Saints nhận user id từ user claims, nếu chúng tồn tại. Player chỉ tồn tại nếu user đã đăng nhập vào game.

\\\csharp
public IActionResult Login([FromQuery] string redirectUrl)
{
    var callbackUrl = \$"{enter your callback url here}";
    var playerId = User.FindFirstValue(ClaimTypes.NameIdentifier);
    var url = tikTokService.RequestAccessToken(callbackUrl, redirectUrl, playerId);
    return Redirect(url);
}
\\\

Khi chuyển hướng xảy ra, có một callback endpoint được gọi. Endpoint này được thiết kế để xác thực. Wicked Saints xác thực state, sau đó chuyển hướng lại client đến \RedirectURL\ với code. Xem ví dụ sau:

\\\csharp
public IActionResult Callback([FromQuery] string code, [FromQuery] string state)
{
    if (string.IsNullOrEmpty(code)) return BadRequest("No code provided");
    if (string.IsNullOrEmpty(state)) return BadRequest("No state provided");
    var oAuthState = AuthorizerService.GetOAuthState(state);
    if (oAuthState == null) return BadRequest("Invalid state provided");
    return Redirect(\$"{oAuthState.RedirectUrl}?code={code}&state={Uri.EscapeDataString(state)}");
}
\\\

Sau khi xác thực thành công, Wicked Saints trao đổi code lấy tokens. Với một lần gọi server endpoint khác \GET /tiktok/exchange?code=...&state=...\, Wicked Saints có thể truy xuất access_token, refresh_token và TikTok user ID. Từ đó, Wicked Saints tiến hành chính xác như cách được mô tả trong ví dụ Google Play được cung cấp trong Guidance for Custom Game Backend Hosting on AWS.

\\\csharp
public async Task<IActionResult> Exchange([FromQuery] string code, [FromQuery] string state)
{
    if (string.IsNullOrEmpty(code)) return BadRequest("No code provided");
    if (string.IsNullOrEmpty(state)) return BadRequest("No state provided");
    var oAuthState = AuthorizerService.GetOAuthState(state);
    if (oAuthState == null) return BadRequest("Invalid state provided");
    var callbackUrl = \$"{enter your same callback url here}";
    var accessToken = await tikTokService.GetAccessToken(callbackUrl, code);
    if (accessToken == null) return BadRequest("Failed to get access token from TikTok");
    var tikTokUserId = accessToken.UserId;
    if (string.IsNullOrEmpty(tikTokUserId)) return BadRequest("TikTok user ID missing from token");
    // proceed with same login flow :) 
}
\\\

Sau đó, Wicked Saints xác định linking dựa trên logic sau:

- Nếu linking đang xảy ra và player có JSON Web Token (JWT); đính kèm TikTok user id vào player đó (điều này cũng bảo vệ chống lại các tài khoản đã được liên kết).
- Nếu TikTok ID đã tồn tại thì đi đến đăng nhập; nếu không, thì tạo một player mới và liên kết các tài khoản (tài khoản game và TikTok).

Cuối cùng, Wicked Saints phát hành game JWT.

Wicked Saints cũng xây dựng một số maintenance endpoints. Một để làm mới hoặc sử dụng lại các token hiện có. Một khác là ngắt kết nối hoặc thu hồi provider token và bỏ liên kết identity. Cuối cùng, họ xây dựng một endpoint xử lý các luồng chuyển giao token trực tiếp.

---

## TÍCH HỢP CLIENT (UNITY)

Để đồng bộ với phần còn lại của các endpoint dựa trên REST của họ, Wicked Saints đã triển khai cách tiếp cận REST-first:

- Mở system browser (hoặc in-app web view) đến game backend TikTok Login endpoint.
- TikTok trả về một callback URL được chỉ định (TikTok callback endpoint), sau đó server chuyển hướng lại đến ứng dụng với code và state.
- Client gọi TikTok exchange endpoint truyền code và state để nhận game JWT.

**LƯU Ý**: TikTok yêu cầu bạn đăng ký redirect URI trong cấu hình ứng dụng; sau khi đồng ý, người dùng được gửi trở lại URI đó. Giữ các chuyển hướng của bạn trong allowlist trong \TikTok Login Kit\.

Trong tương lai, Wicked Saints sẽ mở rộng AWS Mobile SDK for Unity để hỗ trợ tích hợp TikTok mới. Mặc dù Wicked Saints đã đi theo lộ trình tích hợp \est api\, bạn có thể mở rộng Guidance for Custom Game Backend Hosting on AWS gaming backend với AWS Mobile SDK for Unity để hỗ trợ tích hợp TikTok mới của bạn.

Ví dụ, bạn có thể sử dụng một cái gì đó như sau:

\\\csharp
public class AWSGameSDKClient : MonoBehaviour {
    public void LoginWithTikTok(string redirectUrl, bool mobile, Action<LoginRequestData> callback)
        => StartTikTokSignIn(redirectUrl, mobile, callback);

    public void LinkTikTokToCurrentUser(string redirectUrl, bool mobile, Action<LoginRequestData> callback)
    {
        StartTikTokSignIn(redirectUrl, mobile, callback);
    }

    public void StartTikTokSignIn(string redirectUrl, bool mobile, Action<LoginRequestData> callback)
    {
        if (this.loginEndpoint == null) { this.LoginErrorCallback?.Invoke("Login endpoint not defined"); return; }
        this.LoginCallback = callback;
        var url = \$"{this.loginEndpoint}tiktok?redirectUrl={UnityWebRequest.EscapeURL(redirectUrl)}";
        Application.OpenURL(url);
    }

    void OnEnable()
    {
        Application.deepLinkActivated += OnDeepLinkActivated;
        if (!string.IsNullOrEmpty(Application.absoluteURL)) OnDeepLinkActivated(Application.absoluteURL);
    }

    private void OnDeepLinkActivated(string url)
    {
        var uri = new System.Uri(url);
        var q = ParseQuery(uri.Query);
        if (!q.ContainsKey("code") || !q.ContainsKey("state")) return;
        StartCoroutine(this.CallRestApiGetForLogin(
            this.loginEndpoint,
            "tiktok/exchange",
            this.SdkLoginCallback,
            new Dictionary<string,string> { { "code", q["code"] }, { "state", q["state"] } }
        ));
    }
}
\\\

---

## SỬ DỤNG TIKTOK API CHO QUY TRÌNH LÀM VIỆC CỦA CREATOR

Sau khi người chơi xác thực thành công thông qua TikTok Login Kit, Wicked Saints có thể cung cấp cho người chơi một cách để chia sẻ nội dung trực tiếp từ game, hoặc ứng dụng đồng hành, lên tài khoản TikTok của họ. Tích hợp này yêu cầu các quyền cụ thể và tuân theo các quy trình đã được thiết lập.

### Điều kiện tiên quyết

Trước khi triển khai xuất bản nội dung TikTok, hãy xác minh các yêu cầu sau được đáp ứng:

**Phê duyệt ứng dụng nhà phát triển**
- Ứng dụng nhà phát triển TikTok của bạn phải được xem xét và phê duyệt để truy cập Content Posting API
- Gửi tài liệu cần thiết và các use case cho TikTok để xem xét

**Yêu cầu ủy quyền người dùng**
- Người chơi phải cấp các quyền cụ thể thông qua OAuth consent
- Các scope bắt buộc bao gồm:
  - \ideo.upload\: Để tải lên nội dung video
  - \ideo.publish\: Để xuất bản nội dung lên TikTok

**Triển khai xác thực**
- Triển khai luồng xác thực TikTok OAuth v2
- Quản lý và lưu trữ đúng cách user access token
- Xử lý làm mới và hết hạn token

### Quy trình xuất bản nội dung

**Tùy chọn 1: Deferred publishing workflow**

Với quy trình này, người chơi có thể tải lên nội dung trước và hoàn thành quá trình đăng bài sau trong TikTok:

- **Khởi tạo upload**
  - Tạo một phiên upload với TikTok API
  - Lấy các token và endpoint upload cần thiết

- **Chuyển nội dung video**
  - Một trong hai:
    - Tải lên dữ liệu video trực tiếp thông qua API endpoint
  - Hoặc:
    - Cung cấp URL cho TikTok để pull nội dung (yêu cầu xác minh domain)

- **Hoàn thành của người dùng**
  - Người chơi nhận thông báo TikTok
  - Sau đó họ có thể chỉnh sửa và hoàn thành bài đăng trong ứng dụng TikTok
  - Cung cấp quyền truy cập đầy đủ vào các tính năng chỉnh sửa gốc của TikTok

**Tùy chọn 2: Direct publishing workflow**

Quy trình này cho phép đăng nội dung ngay lập tức từ trong ứng dụng của bạn:

- **Chuẩn bị giao diện xuất bản**
  - Query \creator_info\ API endpoint
  - Truy xuất thông tin hồ sơ TikTok của người dùng
  - Xây dựng giao diện xuất bản phù hợp dựa trên loại tài khoản TikTok của người dùng

- **Khởi tạo post**
  - Tạo phiên post mới
  - Đặt các tham số post ban đầu
  - Chuẩn bị metadata nội dung

- **Xuất và xuất bản**
  - Tải lên nội dung video
  - Gửi post để xuất bản ngay lập tức

---

## TẠI SAO CHỌN AWS CUSTOM GAMING BACKEND CHO TÍCH HỢP

Wicked Saints chọn giải pháp Guidance for Custom Game Backend Hosting on AWS làm điểm khởi đầu của họ vì một số lý do chính:

1. **Linh hoạt theo thiết kế**: Framework identity layer là provider-agnostic, cho phép bổ sung nhanh TikTok mà không cần định hình lại client hoặc backend.

2. **Scaffolding sẵn sàng production**: API Gateway với Lambda, vòng đời token, Secrets Manager, CDK stack và các biện pháp bảo vệ bảo mật cung cấp các khối xây dựng đã được chứng minh.

3. **Khả năng mở rộng**: Kiến trúc serverless, hướng sự kiện, với các kho dữ liệu tự động mở rộng, duy trì ngân sách độ trễ trong quá trình phát triển.

4. **Khả năng quan sát và quản trị tích hợp sẵn**: Distributed tracing, structured log, metrics và CDK-based tagging và phân bổ chi phí đơn giản hóa hoạt động trên các tài khoản development, staging và production.

5. **Thời gian tạo giá trị nhanh hơn**: AWS Quick Starts (các kiến trúc tham chiếu tự động hợp lý hóa việc triển khai các khối lượng công việc chính trên AWS Cloud) và các thành phần mẫu cho phép thiết lập nhanh một luồng identity hoạt động, với tích hợp nhanh các .NET minimal API và data model.

6. **Thân thiện với engine**: Các mẫu Unity và REST endpoint sạch xác minh khả năng tương thích với các Unity REST client hiện có, với tùy chọn mở rộng SDK sau cho các helper TikTok.

7. **Bảo mật đáng tin cậy**: Tận dụng các mẫu đã được thử nghiệm thực tế từ các kiến trúc sư AWS giảm rủi ro trong một lĩnh vực quan trọng.

8. **Tập trung vào trải nghiệm người chơi**: Nhóm có thể tập trung vào việc tạo ra các tính năng liên quan đến TikTok hấp dẫn thay vì xây dựng cơ sở hạ tầng xác thực cơ bản.

9. **Giảm thời gian phát triển và rủi ro**: Tận dụng tính chất mở rộng của framework và các mẫu bảo mật đã được chứng minh đẩy nhanh quá trình phát triển.

---

## TÓM TẮT

Wicked Saints đã tích hợp thành công TikTok vào game của họ bằng cách sử dụng Guidance for Custom Game Backend Hosting on AWS. Bằng cách tận dụng framework này và bổ sung vào đó, họ đã có thể triển khai một hệ thống xác thực mạnh mẽ, có khả năng mở rộng, tích hợp liền mạch OAuth flow của TikTok. Mặc dù đối mặt với những thách thức, chẳng hạn như giới hạn deep link encoding và quy trình phê duyệt, nhóm đã có thể tập trung vào việc tạo ra trải nghiệm người chơi hấp dẫn thay vì xây dựng cơ sở hạ tầng xác thực từ đầu.

Giải pháp AWS đã cung cấp một nền tảng linh hoạt, sẵn sàng production, cung cấp cho Wicked Saints một cách để triển khai nhanh tích hợp TikTok của họ, đồng thời duy trì bảo mật và khả năng mở rộng. Case study này chứng minh cách các studio game có thể tận dụng các giải pháp dựa trên cloud để hợp lý hóa tích hợp mạng xã hội và tập trung vào các tính năng gameplay cốt lõi.

Liên hệ với [AWS Representative](https://aws.amazon.com/contact-us/) để tìm hiểu cách chúng tôi có thể giúp đẩy nhanh doanh nghiệp của bạn.

---

## TÀI LIỆU THAM KHẢO THÊM

- [Harmony Games Deploys a Fully Custom Game Backend Utilizing AWS Cloud Development Kit (AWS CDK)](https://aws.amazon.com/blogs/gametech/harmony-games-deploys-a-fully-custom-game-backend-utilizing-aws-cloud-development-kit-aws-cdk/?refid=88cbb1f8-d68e-4966-a75e-e04a1754ebd1)
- [Playable Worlds Scales MMO Gaming with Unity and AWS](https://aws.amazon.com/solutions/case-studies/playable-worlds-unity/)
- [Using latency-based routing with Amazon CloudFront for a multi-Region active-active architecture](https://aws.amazon.com/blogs/networking-and-content-delivery/latency-based-routing-leveraging-amazon-cloudfront-for-a-multi-region-active-active-architecture/)

---

![Matthew Nimmo](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/06/Matthew-Nimmo.png)

**Matthew Nimmo**

Matthew Nimmo là Solutions Architect cho Game Tech tại AWS. Là cả một chuyên gia công nghệ và game thủ nhiệt tình, ông giúp các studio game tận dụng công nghệ đám mây để giải quyết các thách thức phức tạp và tạo ra trải nghiệm người chơi tốt hơn.
