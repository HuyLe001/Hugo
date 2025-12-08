---
title: "Proposal"
date: "2025-11-11"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice warning %}}

{{% /notice %}}

# CloudRead – Online Ebook Reading Platform  
## Giải pháp đọc và quản lý sách trực tuyến trên nền tảng Java + AWS  

### 1. Tóm tắt điều hành  
**CloudRead** là dự án học thuật của nhóm 5 sinh viên Công nghệ thông tin, hướng đến việc phát triển một nền tảng đọc và quản lý sách điện tử (ebook) chạy trên **hạ tầng AWS**.  
Người dùng có thể đăng ký tài khoản, tìm kiếm và đọc ebook trực tuyến qua trình đọc PDF tích hợp, đồng thời nhận email thông báo hoặc hỗ trợ khôi phục mật khẩu qua **Amazon SES**.  
Hệ thống được phát triển bằng **Spring Boot (Java 17)** cho backend, **HTML/CSS/JavaScript (Vanilla JS)** cho frontend, và triển khai trên **AWS** với các dịch vụ **EC2, RDS, S3, CloudFront, SES, IAM, CloudWatch và CodePipeline**.  
Mục tiêu của dự án là xây dựng một nền tảng đọc sách số ổn định, chi phí thấp, dễ mở rộng và mang tính học thuật cao.  

---

### 2. Tuyên bố vấn đề  

*Vấn đề hiện tại*  
Phần lớn các nền tảng ebook miễn phí như **nhasachmienphi.com** chỉ cho phép người dùng tải về hoặc đọc trực tiếp, thiếu các tính năng cơ bản như phân quyền, thống kê truy cập, hoặc đánh giá nội dung.  
Ngoài ra, nhiều nền tảng thương mại có chi phí triển khai và vận hành cao, không phù hợp với quy mô sinh viên hoặc dự án học thuật.  

*Giải pháp*  
CloudRead được thiết kế như một nền tảng học tập – trình diễn công nghệ giúp:  
- Lưu trữ và phân phối ebook qua **Amazon S3 + CloudFront (Signed URL)**.  

- Quản lý người dùng, sách và đánh giá qua **Amazon RDS MySQL**.  
- Triển khai backend Spring Boot trực tiếp trên **Amazon EC2**.  
- Phát hành giao diện frontend tĩnh qua **S3 + CloudFront**.  
- Gửi email xác nhận, hỗ trợ người dùng qua **Amazon SES (SMTP)**.  
- Tự động hóa quá trình build & deploy bằng **AWS CodePipeline → CodeBuild → CodeDeploy**.  
- Giám sát log, hiệu năng và chi phí qua **Amazon CloudWatch**.  

*Lợi ích & ROI*  
- Giúp sinh viên thực hành đầy đủ quy trình phát triển và triển khai ứng dụng cloud thực tế.  
- Dễ vận hành, có thể chạy 24/7 trên AWS với chi phí thấp.  
- Củng cố kiến thức về hệ thống phân tán, bảo mật, DevOps và tối ưu hạ tầng.  
- Sản phẩm có thể mở rộng thêm tính năng học tập, chia sẻ và phân loại sách trong tương lai.  

---

### 3. Kiến trúc giải pháp  

CloudRead sử dụng mô hình **3 lớp kết hợp các dịch vụ AWS**.  
Người dùng truy cập website thông qua **Route 53**, được phân phối nội dung tĩnh qua **CloudFront** lấy từ **S3 (Frontend Bucket)**.  
Khi người dùng đăng nhập, tìm kiếm hoặc mở sách, yêu cầu được gửi đến **EC2 (Spring Boot Backend)**. EC2 truy cập cơ sở dữ liệu **RDS MySQL** trong private subnet để lấy thông tin người dùng, sách và đánh giá, đồng thời truy xuất file từ **S3 private bucket**.  
Khi cần thông báo hoặc hỗ trợ, hệ thống gửi email qua **Amazon SES**.  
Toàn bộ mã nguồn backend được build và triển khai tự động thông qua **CodePipeline → CodeBuild → CodeDeploy**, và được giám sát qua **CloudWatch**.  

*Các dịch vụ AWS chính:*  
- **Amazon EC2**: chạy backend Spring Boot.  
- **Amazon RDS (MySQL)**: lưu trữ dữ liệu người dùng, sách, đánh giá.  
- **Amazon S3 + CloudFront**: lưu trữ và phân phối nội dung web và file sách.  
- **Amazon SES**: gửi email xác nhận, hỗ trợ người dùng.  
- **Amazon IAM**: quản lý quyền truy cập giữa EC2, S3, và SES.  
- **Amazon CodePipeline/CodeBuild/CodeDeploy**: tự động hóa triển khai.  
- **Amazon CloudWatch**: theo dõi log, hiệu năng và cảnh báo chi phí.  

---

### 4. Triển khai kỹ thuật  

*Các giai đoạn triển khai*  
1. **Phát triển cục bộ (1–2 tuần)**: thiết kế cơ sở dữ liệu, viết API cho người dùng và quản lý sách, tạo giao diện đọc PDF bằng HTML/JS.  
2. **Thiết lập AWS (2 tuần)**: tạo EC2, RDS, S3, CloudFront, SES và cấu hình IAM Role bảo mật.  
3. **Tích hợp CI/CD (1 tuần)**: thiết lập CodePipeline – CodeBuild – CodeDeploy để tự động build và cập nhật ứng dụng.  
4. **Kiểm thử & demo (1 tuần)**: kiểm tra các chức năng đọc sách, đánh giá, gửi email, đăng nhập/đăng ký và quản lý nội dung.  

*Yêu cầu kỹ thuật*  
- Java 17 + Spring Boot  
- MySQL (local → RDS)  
- HTML/CSS/JavaScript (Vanilla JS + PDF.js)  
- AWS SDK for Java (S3 + SES)  
- GitHub, CodePipeline/CodeBuild/CodeDeploy  
- Postman, CloudWatch  

---

### 5. Lộ trình & Mốc triển khai  

- **Tháng 1**: Thiết kế database, viết API và giao diện cơ bản.  
- **Tháng 2**: Cấu hình AWS RDS, S3, CloudFront, SES.  
- **Tháng 3**: Tích hợp CI/CD, kiểm thử và trình diễn bản demo CloudRead.  

---

### 6. Ước tính ngân sách  

Chi phí vận hành hệ thống CloudRead ước tính khoảng **15–17 USD/tháng**, bao gồm EC2 (~6.5 USD), RDS (~7 USD), S3 và CloudFront (~0.7 USD), SES (~0.15 USD), CI/CD (~1 USD) và CloudWatch (~0.1 USD).  
Khi tận dụng **AWS Free Tier** và **AWS Student Credit ($100)**, chi phí thực tế gần như bằng **0 USD/tháng** trong giai đoạn đầu.  

---

### 7. Đánh giá rủi ro  

Các rủi ro chính bao gồm mất kết nối dịch vụ AWS, rò rỉ dữ liệu và vượt mức chi phí miễn phí.  
Giải pháp phòng ngừa gồm:  
- Thiết lập **bucket private + Signed URL** cho file sách.  
- Cấu hình **Billing Alarm** theo dõi chi phí.  
- Xác thực domain SES để đảm bảo gửi mail ổn định.  
- Tạo snapshot định kỳ cho EC2 và RDS.  
Nếu pipeline bị lỗi, nhóm có thể **rollback thủ công** sang bản ổn định.  

*Giải pháp dự phòng:*  
- Giữ bản chạy local để demo khi offline.  
- Theo dõi log bằng CloudWatch và kiểm soát chi phí thường xuyên.  

---

### 8. Kết quả kỳ vọng  

Khi hoàn thành, **CloudRead** sẽ là một nền tảng đọc và quản lý ebook trực tuyến hoàn chỉnh, triển khai thật trên AWS.  
Dự án giúp nhóm nắm vững kỹ năng full-stack và DevOps cơ bản: phát triển, triển khai, giám sát và tối ưu chi phí hệ thống cloud.  
Về lâu dài, CloudRead có thể mở rộng thêm tính năng cộng đồng, gợi ý sách, đồng bộ thiết bị và xác thực người dùng qua **Amazon Cognito**.  

---
