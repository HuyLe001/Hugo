---
title: "Dọn dẹp tài nguyên"
date: "2025-12-09"
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Dọn dẹp tài nguyên

Chúc mừng bạn đã hoàn thành workshop!

Để tránh phát sinh chi phí, vui lòng xóa tất cả tài nguyên đã tạo trong workshop này.

#### Các bước dọn dẹp:

1. Xóa CloudFront distribution
2. Xóa Route 53 records
3. Xóa Application Load Balancer
4. Terminate EC2 instances
5. Xóa RDS database
6. Xóa ElastiCache cluster
7. Làm rỗng và xóa S3 buckets
8. Xóa VPC và các tài nguyên liên quan
9. Xóa IAM roles (nếu không cần)

{{% notice warning %}}
Đảm bảo xóa tài nguyên theo đúng thứ tự để tránh lỗi phụ thuộc.
{{% /notice %}}
