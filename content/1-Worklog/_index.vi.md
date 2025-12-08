---
title: "Nhật ký công việc"
date: "2025-12-01"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

{{% notice warning %}}  
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.  
{{% /notice %}}

**Tuần 1:** [Giới thiệu & Thiết lập Môi trường](1.1-week1/)  
Hiểu mô hình Cloud computing, vùng (Region), và Availability Zones. Tạo và cấu hình tài khoản AWS. Giới thiệu Free Tier, quản lý chi phí, và bật cảnh báo Budget. Làm quen với AWS Management Console và AWS CLI.

**Tuần 2:** [Compute & Networking Cơ Bản](1.2-week2/)  
Dịch vụ: EC2, Elastic IP, Auto Scaling, VPC cơ bản. Các thành phần mạng: Subnet, Route Table, Security Group, NACL. Thực hành: Triển khai một web server trên EC2, truy cập từ internet.

**Tuần 3:** [Lưu Trữ & Cơ Sở Dữ Liệu](1.3-week3/)  
Dịch vụ: S3, EBS, EFS, RDS. Phân biệt block / object / file storage. Thực hành: Tạo bucket S3, bật versioning & lifecycle, kết nối ứng dụng với RDS.

**Tuần 4:** [IAM & Bảo Mật Cơ Bản](1.4-week4/)  
Dịch vụ: IAM Users, Groups, Roles, Policies, MFA. Best practices bảo mật tài khoản AWS. Thực hành: Tạo user theo nguyên tắc least privilege, kiểm tra quyền thực tế.

**Tuần 5:** [Giám Sát & Tự Động Hóa Cơ Bản](1.5-week5/)  
Dịch vụ: CloudWatch, CloudTrail, SNS, EventBridge. Giới thiệu Infrastructure as Code (IaC) – CloudFormation căn bản. Thực hành: Tạo Stack EC2 + S3 bằng CloudFormation.

**Tuần 6:** [Tổng Kết Foundation + Mini Project](1.6-week6/)  
Ôn tập toàn bộ các dịch vụ: EC2, S3, RDS, IAM, CloudWatch. Triển khai mini project: Website tĩnh hoặc web app nhỏ sử dụng S3 + EC2 + RDS. Kết quả: Có một project nền tảng & kiến thức vững trước khi vào track chuyên sâu.

**Tuần 7:** [DevOps & Automation](1.7-week7/)  
CI/CD với CodeCommit, CodeBuild, CodeDeploy, CodePipeline. IaC nâng cao: CloudFormation, AWS CDK, Terraform (tùy chọn). Container: ECS, ECR, EKS. Thực hành: Tự động build & deploy web app bằng CodePipeline.

**Tuần 8:** [Container & Orchestration](1.8-week8/)  
Tìm hiểu sâu các dịch vụ container: ECS, EKS, Fargate. Container networking và service discovery. Thực hành: Triển khai ứng dụng containerized với ECS và EKS.

**Tuần 9:** [Security & Compliance](1.9-week9/)  
Kiến trúc Zero Trust. Quản lý khóa với AWS KMS, Secrets Manager. Bảo mật dữ liệu S3, logging và encryption. Thực hành: Thiết lập quy trình bảo mật IAM + KMS + CloudTrail.

**Tuần 10:** [Serverless & Ứng Dụng Hiện Đại](1.10-week10/)  
Dịch vụ Serverless: Lambda, API Gateway, DynamoDB, AppSync. Xây dựng kiến trúc event-driven. Thực hành: Dự án mini – API Serverless hoặc ứng dụng real-time.

**Tuần 11:** [Phát Triển Dự Án Cuối Kỳ](1.11-week11/)  
Thiết kế kiến trúc hoàn chỉnh (từ front-end → backend → database). Áp dụng CI/CD, bảo mật, monitoring, và cost optimization. Kết quả: Hoàn thành một dự án thực tế đủ để thêm vào portfolio CV.

**Tuần 12:** [Showcase Dự Án & Chuẩn Bị Nghề Nghiệp](1.12-week12/)  
Viết blog post / tech talk chia sẻ kinh nghiệm dự án. Ôn tập và luyện thi AWS Certified Cloud Practitioner. Chuẩn bị CV, hồ sơ LinkedIn, và kỹ năng phỏng vấn cloud. Tham gia demo day / showcase của FCJ để trình bày sản phẩm cuối cùng.
