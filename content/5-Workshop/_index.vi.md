---
title: "Triển khai hệ thống"
date: "2025-09-11"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


# Triển khai hệ thống trên AWS

#### Tổng quan

Trong workshop này, bạn sẽ học cách triển khai một hệ thống hoàn chỉnh trên AWS sử dụng nhiều dịch vụ bao gồm VPC, RDS, ElastiCache, S3, EC2, Load Balancer, CloudFront, Route 53 và GitLab CI/CD.

#### Kiến trúc

Hệ thống tuân theo kiến trúc đa tầng với các lớp riêng biệt cho networking, database, compute, distribution và tự động hóa triển khai.

#### Nội dung

1. [Chuẩn bị](5.1-Preparation/)
2. [Database & Storage](5.2-Database-Storage/)
3. [Compute](5.3-Compute/)
4. [Distribution](5.4-Distribution/)
5. [CI/CD](5.5-Deploy/)
6. [Dọn dẹp tài nguyên](5.6-CleanUp/)