---
title: "Event 3"
date: "2025-09-11"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# WORKSHOP AWS WELL-ARCHITECTED SECURITY PILLAR

### Thông Tin Sự Kiện

**Thời gian:** Thứ Bảy, ngày 29 tháng 11 năm 2025, 8:30 – 12:00  
**Địa điểm:** Văn phòng AWS Vietnam  
**Vai trò:** Người tham dự

### Mục Đích Của Sự Kiện

Workshop buổi sáng này cung cấp cái nhìn chuyên sâu toàn diện về AWS Well-Architected Security Pillar, bao gồm tất cả năm domain bảo mật: Identity & Access Management, Detection, Infrastructure Protection, Data Protection, và Incident Response.

Phiên workshop được thiết kế để trang bị cho người tham dự kiến thức thực tế về việc triển khai các best practices bảo mật trong môi trường AWS, với các ví dụ thực tế từ doanh nghiệp Việt Nam.

### Tổng Quan Chương Trình

#### 8:30 – 8:50 | Khai mạc & Nền tảng Security

**Security Pillar trong Well-Architected Framework**

- Vai trò của Security Pillar trong Well-Architected Framework
- Nguyên tắc cốt lõi: Least Privilege – Zero Trust – Defense in Depth
- AWS Shared Responsibility Model
- Các mối đe dọa bảo mật cloud hàng đầu tại Việt Nam

#### Pillar 1 — Identity & Access Management

**8:50 – 9:30 | Kiến trúc IAM hiện đại**

- IAM cơ bản: Users, Roles, Policies – tránh long-term credentials
- IAM Identity Center: SSO, permission sets
- SCP & Permission Boundaries cho môi trường multi-account
- MFA, credential rotation, Access Analyzer
- Mini Demo: Validate IAM Policy + simulate access

#### Pillar 2 — Detection

**9:30 – 9:55 | Detection & Continuous Monitoring**

- CloudTrail (org-level), GuardDuty, Security Hub
- Logging tại mọi tầng: VPC Flow Logs, ALB/S3 logs
- Alerting & automation với EventBridge
- Detection-as-Code (infrastructure + rules)

#### 9:55 – 10:10 | Giải lao

#### Pillar 3 — Infrastructure Protection

**10:10 – 10:40 | Network & Workload Security**

- VPC segmentation, private vs public placement
- Security Groups vs NACLs: mô hình áp dụng
- WAF + Shield + Network Firewall
- Workload protection: EC2, ECS/EKS security basics

#### Pillar 4 — Data Protection

**10:40 – 11:10 | Encryption, Keys & Secrets**

- KMS: key policies, grants, rotation
- Encryption at-rest & in-transit: S3, EBS, RDS, DynamoDB
- Secrets Manager & Parameter Store — rotation patterns
- Data classification & access guardrails

#### Pillar 5 — Incident Response

**11:10 – 11:40 | IR Playbook & Automation**

- IR lifecycle theo AWS framework
- Playbooks:
  - Compromised IAM key
  - S3 public exposure
  - EC2 malware detection
- Snapshot, isolation, evidence collection
- Auto-response với Lambda/Step Functions

#### 11:40 – 12:00 | Tổng kết & Q&A

- Tóm tắt 5 security pillars
- Common pitfalls & thực tế doanh nghiệp Việt Nam
- Roadmap học security (Security Specialty, SA Pro certifications)

### Những Gì Tôi Học Được

- **Least Privilege là nền tảng** – luôn bắt đầu với quyền tối thiểu và mở rộng khi cần
- **Kiến trúc Zero Trust** không giả định tin cậy ngầm định, ngay cả trong mạng nội bộ
- **Defense in Depth** yêu cầu kiểm soát bảo mật ở nhiều lớp
- **Khả năng detection** phải được tự động hóa và liên tục
- **Incident response playbooks** cần được tài liệu hóa và kiểm tra thường xuyên

### Ứng Dụng Vào Công Việc

- **Triển khai IAM Access Analyzer** trong các dự án hiện tại
- **Thiết lập GuardDuty và Security Hub** cho giám sát bảo mật tập trung
- **Tạo incident response playbooks** cho các kịch bản phổ biến
- **Review và siết chặt Security Group rules** theo nguyên tắc least privilege
- **Bật encryption** cho tất cả data stores (S3, RDS, DynamoDB)

### Trải Nghiệm Cá Nhân

Workshop này cực kỳ giá trị để hiểu toàn diện về bảo mật AWS:

- Các demo thực tế giúp các khái niệm trừu tượng trở nên cụ thể
- Học về các pitfalls bảo mật phổ biến tại doanh nghiệp Việt Nam rất bổ ích
- Các incident response playbooks cung cấp templates có thể áp dụng ngay
- Hiểu mối quan hệ giữa cả năm pillars giúp thiết kế kiến trúc bảo mật toàn diện

### Bài Học Rút Ra

- **Bảo mật là hành trình liên tục**, không phải đích đến
- **Tự động hóa là chìa khóa** để duy trì bảo mật ở quy mô lớn
- **Well-Architected Security Pillar** cung cấp framework toàn diện cho cloud security
- **Review và cải thiện bảo mật định kỳ** là thiết yếu
- **AWS cung cấp các công cụ native mạnh mẽ** cho từng domain bảo mật

### Một Số Hình Ảnh

![Security Workshop 1](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event5/1.jpg)
![Security Workshop 2](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event5/2.jpg)
![Security Workshop 3](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event5/3.jpg)
![Security Workshop 4](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event5/4.jpg)
![Security Workshop 5](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event5/5.jpg)
