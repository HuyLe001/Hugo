---
title: "Worklog Tuần 4"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

{{% notice warning %}}  
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.  
{{% /notice %}}

## Mục tiêu tuần 4

• Thực hành với các dịch vụ lưu trữ và hệ thống file  
• Có kinh nghiệm thực tế với databases (RDS)  
• Tìm hiểu về giám sát bảo mật và các khái niệm compliance cơ bản  
• Xây dựng project nhỏ tích hợp nhiều dịch vụ AWS

---

## Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|:---:|:-----|:----------:|:---------------:|:-------------------|
| Thứ Hai | - Ôn tập các khái niệm storage từ các tuần trước<br>- Tìm hiểu về EFS (Elastic File System)<br>- Hiểu sự khác biệt giữa EBS, EFS và S3 | 29/09/2025 | 29/09/2025 | [Video 17](https://www.youtube.com/watch?v=kkcdRBRnxl4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=17)<br>[Video 18](https://www.youtube.com/watch?v=aPQynt3CfYc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=18)<br>[Video 19](https://www.youtube.com/watch?v=NoF8eEIEA6M&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=19) |
| Thứ Ba | - Thực hành với RDS (Relational Database Service)<br>- Thử tạo database MySQL/PostgreSQL đơn giản<br>- Tìm hiểu về database backups và snapshots | 30/09/2025 | 30/09/2025 | [Video 38](https://www.youtube.com/watch?v=nSRrWRBSphc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=38)<br>[Video 46](https://www.youtube.com/watch?v=Oo2UpjL-exE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=46)<br>[Video 47](https://www.youtube.com/watch?v=EQ-5P6U7Ph4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=47) |
| Thứ Tư | - Tiếp tục thực hành SNS và SQS<br>- Thử gửi notifications với SNS<br>- Hiểu về message queuing với SQS | 01/10/2025 | 01/10/2025 | [Video 91](https://www.youtube.com/watch?v=9Cd_dAUCh9o&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=91)<br>[Video 92](https://www.youtube.com/watch?v=iw0qEi-PiOc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=92)<br>[Video 93](https://www.youtube.com/watch?v=pJEhAwGyu9g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=93) |
| Thứ Năm | - Tìm hiểu về CloudTrail cho auditing<br>- Hiểu các best practices về bảo mật AWS<br>- Làm quen với các khái niệm compliance cơ bản | 02/10/2025 | 02/10/2025 | [Video 96](https://www.youtube.com/watch?v=5RxYavHbgVE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=96)<br>[Video 97](https://www.youtube.com/watch?v=TicCP8LfNPU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=97)<br>[Video 98](https://www.youtube.com/watch?v=HcLBLpYHtCw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=98) |
| Thứ Sáu | - Làm việc trên project nhỏ tích hợp EC2, RDS và S3<br>- Thực hành kết nối web server với database<br>- Ôn tập và ghi chép những gì đã học trong tháng | 03/10/2025 | 03/10/2025 | Thực hành và ôn tập<br>Video trước làm tham khảo |

---

## Kết quả đạt được tuần 4

• Học về EFS (Elastic File System) và sự khác biệt giữa EBS (block storage), EFS (file storage) và S3 (object storage).  
• Tạo RDS database instance đầu tiên (MySQL), thực hành database snapshots và backups.  
• Kết nối thành công EC2 với RDS database sau khi khắc phục vấn đề cấu hình security group.  
• Thực hành SNS (Simple Notification Service) cho email notifications và SQS (Simple Queue Service) cho message queuing.  
• Học CloudTrail để theo dõi AWS API calls và mục đích security auditing.  
• Xây dựng project tích hợp kết hợp EC2 web server, RDS MySQL database và S3 cho static files.  
• Cải thiện kỹ năng debugging cho các vấn đề kết nối và cấu hình security group.  
• Bắt đầu ghi nhật ký khắc phục sự cố và học được tầm quan trọng của việc đặt tên tài nguyên có tổ chức.


