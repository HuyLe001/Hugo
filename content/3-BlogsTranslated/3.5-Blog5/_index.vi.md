---
title: "Tăng cường Truy vấn Mô hình Nền tảng thông qua Tích hợp Amazon Bedrock-Amazon Alexa"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 3.5. </b> "
---

{{% notice warning %}}
 **Lưu ý:** Thông tin dưới đây chỉ mang tính chất tham khảo. Vui lòng **không sao chép nguyên văn** cho báo cáo của riêng bạn, bao gồm cả cảnh báo này.
{{% /notice %}}

# TĂNG CƯỜNG TRUY VẤN MÔ HÌNH NỀN TẢNG THÔNG QUA TÍCH HỢP AMAZON BEDROCK-AMAZON ALEXA

**Bài viết gốc**: [Strengthen foundation model queries through Amazon Bedrock-Amazon Alexa integration](https://aws.amazon.com/vi/blogs/publicsector/strengthen-foundation-model-queries-through-amazon-bedrock-amazon-alexa-integration/)

**Tác giả gốc**: Cristiano Scandura và Gabriel Martini

**Ngày xuất bản**: 17 JAN 2025

**Người dịch**: Diệp Huy

**Ngày dịch**: 02 DEC 2025

---

## GIỚI THIỆU

Ngày nay, trí tuệ nhân tạo tạo sinh (generative AI) là trung tâm của nhiều quyết định và công nghệ mà các doanh nghiệp trên toàn cầu đang triển khai. Yếu tố then chốt để đảm bảo trí tuệ nhân tạo tạo sinh hoạt động hiệu quả phụ thuộc vào các mô hình nền tảng (FMs) lưu trữ dữ liệu. Để đảm bảo rằng các FM đó đang truy xuất dữ liệu chính xác, [Amazon Web Services (AWS)](https://aws.amazon.com/) đã phát triển một giải pháp thông qua [Amazon Bedrock](https://aws.amazon.com/bedrock/) để tạo SQL nhằm trả lời các câu hỏi của người dùng về dữ liệu. Giải pháp được phát triển để hỗ trợ [Viện Liên bang São Paulo](https://spo.ifsp.edu.br/) (IFSP) và đã tối ưu hóa việc ra quyết định của họ.

Trí tuệ nhân tạo tạo sinh dựa trên các FM lớn, được huấn luyện trên lượng dữ liệu khổng lồ và có khả năng tạo ra văn bản, hình ảnh, âm thanh, mã code và nhiều hơn nữa. Tuy nhiên, dữ liệu này có thể đã lỗi thời hoặc thiếu ngữ cảnh, và các mô hình này gặp khó khăn trong việc xử lý dữ liệu có cấu trúc và tạo ra các câu trả lời xác định hơn. Khó khăn này có thể dẫn đến hiện tượng ảo giác (hallucinations), khi mô hình tạo ra đầu ra không dựa trên dữ liệu đầu vào hoặc kiến thức thực tế. Ví dụ, khi cố gắng tính tổng các giá trị trong một bảng, mô hình có thể tạo ra các con số ngẫu nhiên hoặc không nhất quán thay vì thực hiện các phép tính một cách chính xác.

Việc không thể diễn giải đúng cấu trúc của hàng, cột và ô, cũng như các mối quan hệ phức tạp giữa chúng, có thể dẫn đến lỗi trong việc xác định giá trị lớn nhất, nhỏ nhất và các phép toán toán học khác. Vấn đề ảo giác và không chính xác đặc biệt nghiêm trọng khi xử lý dữ liệu nhạy cảm, chẳng hạn như thông tin tài chính, y tế hoặc khoa học, nơi mà độ chính xác là thiết yếu, ảnh hưởng đến độ tin cậy của ứng dụng sử dụng trí tuệ nhân tạo tạo sinh.

Một cách để giải quyết vấn đề ảo giác khi trả lời các câu hỏi trong ngữ cảnh dữ liệu có cấu trúc là sử dụng các mô hình để tạo truy vấn SQL. Thay vì cố gắng trực tiếp diễn giải các bảng và thực hiện các phép toán toán học, một mô hình được huấn luyện có thể được sử dụng để tạo truy vấn SQL dựa trên ngôn ngữ tự nhiên.

[Anthropic](https://www.anthropic.com/) đã tạo ra Claude 3, một trợ lý AI có khả năng diễn giải các cửa sổ ngữ cảnh lớn. Sử dụng các kỹ thuật kỹ thuật prompt (prompt engineering), mô hình có thể kết hợp hiểu biết ngôn ngữ tự nhiên với kiến thức chuyên môn về SQL và cấu trúc cơ sở dữ liệu. Để hỗ trợ người dùng, Anthropic có một thư viện các prompt cho các trường hợp sử dụng khác nhau, bao gồm [prompt SQL sorcerer](https://docs.anthropic.com/en/prompt-library/sql-sorcerer) để tạo truy vấn SQL. Với các prompt này, người dùng có thể tạo mã SQL bằng ngôn ngữ tự nhiên, điều phối việc thực thi truy vấn bằng các dịch vụ cơ sở dữ liệu và tạo ra một phản hồi thân thiện với người dùng. Sơ đồ sau đây cho thấy kiến trúc cấp cao của giải pháp.

![Kiến trúc giải pháp tích hợp Alexa với Amazon Bedrock](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2025/01/17/FM_queries_Bedrock_Alexa_figure1.png)

**Hình 1**: Kiến trúc của giải pháp tích hợp Alexa với Amazon Bedrock.

Các thành phần chính là Amazon S3 bucket, AWS Lambda, Amazon Athena, Amazon Bedrock, AWS Glue và Amazon EventBridge.

Trong giải pháp này, người dùng có thể đặt câu hỏi về dữ liệu thông qua Alexa bằng cách sử dụng một skill. [Alexa Skills Kit](https://developer.amazon.com/pt-BR/alexa/alexa-skills-kit) là một framework phát triển phần mềm bạn có thể sử dụng để tạo nội dung, được gọi là skills. Giải pháp cũng sử dụng [Amazon Bedrock](https://aws.amazon.com/bedrock/), một dịch vụ được quản lý hoàn toàn cung cấp một số tùy chọn FM hiệu suất cao từ các công ty AI hàng đầu như AI21 Labs, Anthropic, Cohere, Meta, Mistral AI, Stability AI và Amazon, thông qua một API duy nhất. Amazon Bedrock cũng có một tập hợp rộng các tài nguyên cần thiết như knowledge bases, agents và guardrails để tạo các ứng dụng trí tuệ nhân tạo tạo sinh với tính an toàn, riêng tư và trách nhiệm.

---

## LUỒNG KIẾN TRÚC

Luồng của kiến trúc tuân theo các bước sau:

1. Quá trình bắt đầu với người dùng đặt câu hỏi bằng ngôn ngữ tự nhiên thông qua Alexa. Các câu hỏi này được chuyển tiếp đến một hàm [AWS Lambda](https://aws.amazon.com/lambda/). Hàm sẽ tương tác với LLM của Anthropic, cụ thể là mô hình Claude 3 Haiku, thông qua các lệnh gọi API Amazon Bedrock

2. Claude 3 Haiku nhận cấu trúc cơ sở dữ liệu làm ngữ cảnh, chẳng hạn như mô tả các bảng và trường, thông qua câu hỏi của người dùng. Dựa trên câu hỏi và cấu trúc cơ sở dữ liệu, mô hình tạo mã SQL. Truy vấn SQL được tạo sau đó được thực thi trong [Amazon Athena](https://aws.amazon.com/athena/), truy xuất dữ liệu từ các tệp ".csv" có cấu trúc được lưu trữ trong [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/). Athena sử dụng metadata từ data catalog được quản lý bởi [AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/catalog-and-crawler.html)

3. Dữ liệu được trả về sau khi thực thi truy vấn SQL được sử dụng làm ngữ cảnh trong một lệnh gọi API Amazon Bedrock mới cho Claude 3 Haiku để tạo một phản hồi văn bản, giải thích dữ liệu truy vấn theo cách tự nhiên và dễ hiểu. Phản hồi này sau đó được trả về bởi hàm Lambda cho Alexa, chuyển đổi nó thành âm thanh và phản hồi cho người dùng

4. Để giữ cho giải pháp được cập nhật trong trường hợp có thay đổi cấu trúc trong cơ sở dữ liệu, có một quy tắc được tạo trong [Amazon EventBridge](https://aws.amazon.com/eventbridge/) được kích hoạt mỗi khi dữ liệu được cập nhật trong Amazon S3 và sẽ kích hoạt một hàm Lambda cập nhật các data catalog trong AWS Glue bằng cách thực thi AWS Glue crawler và cập nhật các tệp ngữ cảnh của giải pháp

Giải pháp này nảy sinh từ nhu cầu của IFSP, hiện có hơn 50.000 sinh viên, để tối ưu hóa việc ra quyết định cho các nhà quản lý hành chính trong một môi trường ngày càng năng động đòi hỏi các quyết định ngân sách và giáo dục nhanh chóng dựa trên một lượng lớn dữ liệu. IFSP đã làm việc để phát triển skill Alexa với sự hợp tác của AWS, do đó cho phép tương tác ngôn ngữ tự nhiên với một tập hợp phức tạp [dữ liệu hiện có trong Nền tảng Nilo Peçanha](https://www.gov.br/mec/pt-br/pnp). Điều này cung cấp cho ban lãnh đạo cao nhất một phương tiện truy cập dữ liệu và các chỉ số giáo dục để hỗ trợ việc ra quyết định với sự liên kết đúng đắn của tổ chức với các yêu cầu chiến lược và xã hội của nó.

"Tương tác ngôn ngữ tự nhiên với dữ liệu từ Nền tảng Nilo Peçanha là một sự phát triển cần thiết để hợp lý hóa việc ra quyết định chiến lược, dựa trên dữ liệu và đổi mới thông qua việc tích hợp các công cụ trí tuệ nhân tạo tạo sinh của AWS vào cuộc sống hàng ngày của các nhà quản lý tổ chức của chúng tôi," Bruno Luz, phó hiệu trưởng về kế hoạch và phát triển tổ chức tại IFSP cho biết.

---

## TRIỂN KHAI VÀ KỸ THUẬT PROMPT

Dữ liệu được nhập và lưu trữ trong một kiến trúc data lake serverless trên AWS, sử dụng Amazon S3 làm lớp lưu trữ và AWS Glue và Amazon Athena để phân loại và truy vấn dữ liệu. Các prompt khác nhau đã được thử nghiệm trên Claude 3 Haiku, sử dụng các kỹ thuật như [zero-shot](https://www.promptingguide.ai/techniques/zeroshot) và [few-shot](https://www.promptingguide.ai/techniques/fewshot). Prompt sau đây đáp ứng tốt nhất trường hợp sử dụng này:

\\\
Human:
Transform this natural language question into a query for AWS Athena. Respond only with the SQL query in a single line. In the query, the table name and column names should be in quotes. ONLY the table name should have '"AwsDataCatalog"."s3".'. Do not generate queries related to any database alterations, only generate query questions. Assume that the database has the following tables and columns:

Table: TaxaEvasao

- Id (integer pk)
- Description (varchar)
- Quantity (number)

<others tables...>

For questions related to Dropout Rate, table TaxaEvasao, consider that the calculation of the dropout rate is the sum of the numero_de_matriculas column divided by the sum of the matriculas_numero_de_evadidos column. Additionally, the number must be in decimal format, and Athena will present a decimal if both sums have a CAST to decimal. For example, to list the dropout rates for 2022, the correct query would be:

SELECT instituicao, sum(numero_de_matriculas) as MAT, sum(matriculas_numero_de_evadidos) as EVD, CAST ((sum(numero_de_matriculas)) AS decimal(10,2))/CAST ((sum(matriculas_numero_de_evadidos)) AS decimal(10,2)) FROM "AwsDataCatalog"."s3"."TaxaEvasao" WHERE "ano" = 2022 GROUP BY instituicao ORDER BY "instituicao" DESC;

<other queries tables samples...>

Identify the query generated in your response and place it between the <query></query> tags
\\\

Thông qua prompt này và theo câu hỏi của người dùng, Claude 3 Haiku phản hồi với mã SQL. Ví dụ, đối với câu hỏi "List the top 3 institutes with more student-teacher ratio for the year 2022", kết quả là:

\\\sql
SELECT instituicao_nome, rap
FROM "AwsDataCatalog"."s3"."RelacaoAlunoProfessorRAP"
WHERE ano = 2021 ORDER BY rap DESC LIMIT 3;
\\\

Sau khi truy vấn được thực hiện trong data lake, phản hồi cuối cùng cho người dùng được tạo động bằng cách sử dụng LLM. Ảnh chụp màn hình sau đây cho thấy kết quả được trả về.

![Ví dụ về câu hỏi và câu trả lời trong kiểm thử trên bảng điều khiển nhà phát triển Alexa](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2025/01/17/FM_queries_Bedrock_Alexa_figure2.png)

**Hình 2**: Ví dụ về câu hỏi và câu trả lời trong kiểm thử trên bảng điều khiển nhà phát triển Alexa.

Bạn có thể tải xuống mã nguồn cho giải pháp này và chạy phiên bản skill Alexa của riêng bạn bằng cách truy cập ví dụ đã được xuất bản trong [kho lưu trữ GitHub mẫu AWS chính thức](https://github.com/aws-samples/alexa-and-bedrock-integration).

"Việc sử dụng AI với AWS cho phép các khu vực CNTT đóng vai trò đổi mới, mở ra cánh cửa cho việc sử dụng các công nghệ mới để phát triển tổ chức theo hướng các môi trường được chuẩn bị tốt hơn và nhanh nhẹn hơn với chi phí phải chăng và tương thích với độ phức tạp công nghệ liên quan," Leonardo Menzani Silva, giám đốc CNTT tại IFSP cho biết.

---

## BẢO MẬT, QUYỀN RIÊNG TƯ VÀ BẢO VỆ

Điều quan trọng cần nhấn mạnh là giải pháp cung cấp bảo mật tài nguyên. Dữ liệu được mã hóa khi lưu trữ và khi truyền tải, cả bởi Amazon Bedrock và trong việc tích hợp Alexa với hàm Lambda. Trong giải pháp này, chúng tôi đã bật mã hóa dữ liệu trong các S3 bucket theo mặc định bằng cách sử dụng các khóa có thể được tạo và quản lý trong [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/).

Amazon Bedrock không chia sẻ dữ liệu của bạn với các nhà cung cấp mô hình và không sử dụng nó để huấn luyện lại các mô hình công khai, có nghĩa là dịch vụ duy trì tính bảo mật của dữ liệu. Khi bạn điều chỉnh FM của mình, nó dựa trên một bản sao riêng tư của mô hình đó. Amazon Bedrock tuân thủ các tiêu chuẩn quốc tế, bao gồm ISO, SOC, CSA STAR Level 2 và GDPR, và đủ điều kiện cho HIPAA.

Sơ đồ sau đây cho thấy cách quyền truy cập vào các dịch vụ và tài nguyên hoạt động bằng cách sử dụng các vai trò và chính sách được tạo và duy trì với [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/).

![Sơ đồ kiến trúc của quyền truy cập vào các dịch vụ và tài nguyên](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2025/01/17/FM_queries_Bedrock_Alexa_figure3.png)

**Hình 3**: Sơ đồ kiến trúc của quyền truy cập vào các dịch vụ và tài nguyên.

Để skill Alexa có thể gọi một hàm Lambda, nó cần cấu hình Amazon Resource Name (ARN) của hàm Lambda trong bảng điều khiển phát triển skill. Ngược lại, nó cần tạo một chính sách dựa trên tài nguyên với ID của skill được liên kết với hàm Lambda cho phép nó được gọi bởi skill.

Ngoài ra, bạn cần tạo các chính sách dựa trên tài nguyên để hàm Lambda, khi được gọi, có thể truy cập các dịch vụ Amazon Bedrock, Athena và AWS Glue catalog. Mặc dù hàm không truy cập trực tiếp vào AWS Glue, nhưng chính sách được liên kết với nó cho phép nó, thông qua Athena, truy cập các tài nguyên được lưu trữ trong Amazon S3 và khóa mã hóa dữ liệu được lưu trữ trong AWS KMS.

Giải pháp không giải quyết vấn đề ủy quyền truy cập dữ liệu vì dữ liệu là công khai. Nếu bạn cần hạn chế quyền truy cập của người dùng vào dữ liệu, bạn có thể sử dụng [chức năng liên kết tài khoản của Alexa Skills Kit](https://developer.amazon.com/en-US/docs/alexa/account-linking/add-account-linking.html).

---

## CHI PHÍ

Giải pháp này sử dụng thanh toán Amazon Bedrock On-Demand, cho phép sử dụng FM mà không cần cam kết dựa trên thời gian. Các mô hình tạo văn bản được tính phí theo input tokens được xử lý và output tokens được tạo ra.

Một token bao gồm một vài ký tự và đề cập đến đơn vị văn bản cơ bản mà một mô hình học để hiểu prompt. Đối với Claude, [một token đại diện cho khoảng 3.5 ký tự trong tiếng Anh](https://docs.anthropic.com/en/docs/glossary), mặc dù số lượng chính xác có thể thay đổi tùy thuộc vào ngôn ngữ được sử dụng. Tokens thường được ẩn khi tương tác với các mô hình ngôn ngữ ở cấp độ "văn bản", nhưng chúng trở nên có liên quan khi kiểm tra các đầu vào và đầu ra chính xác của một mô hình ngôn ngữ.

Trong ước tính chi phí với IFSP, 1.000 lệnh gọi hàng tháng đã được quy định. Để giảm chi phí, quá trình xử lý đầu tiên, nơi truy vấn SQL được tạo, đã sử dụng LLM Claude 3 Haiku với input prompt sử dụng khoảng 6.000 tokens và tạo ra một output với khoảng 400 tokens, chi phí khoảng 1,50 USD. Trong phần thứ hai, nơi phản hồi cuối cùng được tạo, chúng tôi đã sử dụng LLM Claude 3 Sonnet để có một phản hồi phù hợp hơn. Kết quả là 400 tokens làm input và khoảng 150 tokens làm output, chi phí khoảng 1,20 USD.

Để biết thông tin chi tiết về giá, vui lòng tham khảo [trang Giá Amazon Bedrock](https://aws.amazon.com/bedrock/pricing/).

---

## KẾT LUẬN

Việc tích hợp trí tuệ nhân tạo tạo sinh với Alexa để phân tích dữ liệu, sử dụng các mô hình tiên tiến như Claude 3 của Anthropic trên Amazon Bedrock, đơn giản hóa tương tác với dữ liệu phức tạp, chuyển đổi các truy vấn ngôn ngữ tự nhiên và trả về các phản hồi chính xác. Giải pháp này, được minh họa bằng thành công tại Viện Liên bang São Paulo, chứng minh hiệu quả của phương pháp tiếp cận, làm cho phân tích dữ liệu dễ tiếp cận hơn. Để tìm hiểu thêm, hãy liên hệ với nhóm tài khoản AWS của bạn hoặc [nhóm AWS Public Sector](https://aws.amazon.com/government-education/contact/).

---

## TÀI LIỆU THAM KHẢO THÊM

- [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
- [Alexa Skills Kit Documentation](https://developer.amazon.com/en-US/docs/alexa/ask-overviews/what-is-the-alexa-skills-kit.html)
- [AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/catalog-and-crawler.html)
- [Amazon Athena User Guide](https://docs.aws.amazon.com/athena/)
- [Anthropic Claude Prompt Library](https://docs.anthropic.com/en/prompt-library/sql-sorcerer)
- [AWS Sample GitHub Repository - Alexa and Bedrock Integration](https://github.com/aws-samples/alexa-and-bedrock-integration)

---

![Cristiano Scandura](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2024/12/13/Cristiano_Scandura.jpg)

**Cristiano Scandura**

Cristiano đã làm việc trong ngành CNTT từ năm 1998. Anh ấy tham gia Amazon Web Services (AWS) vào năm 2018, nơi anh ấy làm việc trên các dự án cho các khách hàng doanh nghiệp. Hiện tại, anh ấy chuyên về các dự án trí tuệ nhân tạo tạo sinh (generative AI), AI và machine learning (ML) cho AWS Worldwide Public Sector.

![Gabriel Martini](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2024/12/13/Gabriel_Martini.jpg)

**Gabriel Martini**

Gabriel có kinh nghiệm trong kỹ thuật phần mềm, kiến trúc giải pháp và khoa học dữ liệu. Anh ấy đã làm việc trong CNTT từ năm 2014 và tham gia Amazon Web Services (AWS) vào năm 2017. Tại AWS, anh ấy đã làm việc như một solutions architect cho các khách hàng lớn và trên các sáng kiến nghiên cứu dữ liệu mở. Hiện tại anh ấy làm việc như một AI specialist solutions architect tập trung vào các lĩnh vực như generative AI, machine learning operations (MLOps) và computer vision.
