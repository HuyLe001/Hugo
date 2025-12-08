---
title: "Worklog Tuần 11"
date: "2025-09-11"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

{{% notice warning %}}  
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.  
{{% /notice %}}

## Mục tiêu tuần 11

• Xây dựng hands-on projects sử dụng các services đã học trong 10 tuần  
• Thực hành kết hợp nhiều AWS services trong ứng dụng thực tế  
• Củng cố hiểu biết thông qua practical implementation  
• Tạo portfolio-ready projects với documentation

---

## Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|:---:|:-----|:----------:|:---------------:|:-------------------|
| Thứ Hai | - Thiết kế và lập kế hoạch Project 1: Simple Blog Application<br>- Thiết lập architecture (EC2 + RDS + S3)<br>- Tạo VPC và security configurations | 17/11/2025 | 17/11/2025 | [Video 39](https://www.youtube.com/watch?v=b6es98paBIw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=39)<br>[Video 127](https://www.youtube.com/watch?v=8254BfjSBhk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=127)<br>[Video 128](https://www.youtube.com/watch?v=q9vy2k-ucKg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=128) |
| Thứ Ba | - Triển khai Project 1 backend và database<br>- Deploy application trên EC2<br>- Cấu hình RDS cho blog posts storage | 18/11/2025 | 18/11/2025 | [Video 129](https://www.youtube.com/watch?v=HyJtLNU1HgQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=129)<br>[Video 130](https://www.youtube.com/watch?v=4yoBRMOsKJ4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=130)<br>Review Week 2-4 materials |
| Thứ Tư | - Thiết kế và build Project 2: Serverless To-Do API<br>- Tạo API Gateway + Lambda + DynamoDB<br>- Triển khai CRUD operations | 19/11/2025 | 19/11/2025 | [Video 58](https://www.youtube.com/watch?v=BLBB1fcPyYA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=58)<br>[Video 59](https://www.youtube.com/watch?v=5rJWHz4VK3k&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=59)<br>[Video 60](https://www.youtube.com/watch?v=jqAYsKS2Fwk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=60) |
| Thứ Năm | - Build Project 3: Automated Image Processing<br>- S3 upload triggers Lambda<br>- Xử lý images và lưu metadata vào DynamoDB | 20/11/2025 | 20/11/2025 | [Video 61](https://www.youtube.com/watch?v=MFEjP5s3bYE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=61)<br>[Video 62](https://www.youtube.com/watch?v=_VxmPZjEWFs&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=62)<br>[Video 63](https://www.youtube.com/watch?v=p5hcAUK-AZg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=63) |
| Thứ Sáu | - Tạo CI/CD pipeline cho một project<br>- Document tất cả projects với architecture diagrams<br>- Clean up resources và review tuần | 21/11/2025 | 21/11/2025 | [Video 64](https://www.youtube.com/watch?v=wrCVzKmZ5hM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=64)<br>[Video 65](https://www.youtube.com/watch?v=qOYh9XQiDAA&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=65)<br>Review Week 8 CI/CD notes |

---

## Kết quả đạt được tuần 11

• Xây dựng Project 1 (Blog Application): 3-tier architecture với S3 static frontend, EC2 Node.js backend, RDS MySQL database, và Application Load Balancer.  
• Xây dựng Project 2 (Serverless To-Do API): Complete CRUD operations sử dụng API Gateway, 5 Lambda functions, và DynamoDB với API key authentication.  
• Xây dựng Project 3 (Automated Image Processing): S3 upload trigger, Lambda với Pillow library cho thumbnail generation, DynamoDB cho metadata storage.  
• Triển khai CI/CD pipeline cho To-Do API với CodeCommit, CodeBuild, và automated Lambda deployment.  
• Tạo comprehensive documentation với architecture diagrams, setup instructions, API documentation, và cost estimates cho tất cả projects.  
• Đạt được practical experience tích hợp nhiều AWS services và troubleshooting distributed systems trong real-world scenarios.  
• Áp dụng tất cả kiến thức từ Week 1-10 vào working projects chứng minh AWS skills cho portfolio.  
• Học được importance of testing từng component riêng biệt trước integration để giảm debugging time.


