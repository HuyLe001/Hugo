---
title: "Worklog Tuần 7"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

{{% notice warning %}}  
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.  
{{% /notice %}}

## Mục tiêu tuần 7

• Học về containerization và Docker basics  
• Hiểu sự khác biệt giữa containers và serverless  
• Làm quen với Amazon ECS (Elastic Container Service)  
• Thực hành deploy containerized applications trên AWS

---

## Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|:---:|:-----|:----------:|:---------------:|:-------------------|
| Thứ Hai | - Giới thiệu về containers và Docker<br>- Học containers là gì và tại sao chúng hữu ích<br>- Hiểu Docker basics và thuật ngữ | 20/10/2025 | 20/10/2025 | [Video 112](https://www.youtube.com/watch?v=lRbXC9UXqdo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=112)<br>[Video 113](https://www.youtube.com/watch?v=Yr6oD4btfZg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=113)<br>[Video 114](https://www.youtube.com/watch?v=X5PI5rJHIGM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=114) |
| Thứ Ba | - Học về Docker images và containers<br>- Thử tạo Dockerfile đơn giản<br>- Giới thiệu về ECR (Elastic Container Registry) | 21/10/2025 | 21/10/2025 | [Video 115](https://www.youtube.com/watch?v=ZIQ2uvgLUVQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=115)<br>[Video 116](https://www.youtube.com/watch?v=bsbQQZ3wDzY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=116)<br>[Video 117](https://www.youtube.com/watch?v=Yi60WeqqNWw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=117) |
| Thứ Tư | - Giới thiệu về Amazon ECS<br>- Học về ECS task definitions và services<br>- Hiểu ECS clusters và container orchestration | 22/10/2025 | 22/10/2025 | [Video 118](https://www.youtube.com/watch?v=8klJUbKLLu8&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=118)<br>[Video 119](https://www.youtube.com/watch?v=qDCTqoSZ5Dw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=119)<br>[Video 120](https://www.youtube.com/watch?v=Ipql97gmQjk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=120) |
| Thứ Năm | - Thực hành deploy container lên ECS<br>- Học về ECS Fargate (serverless containers)<br>- Cấu hình container networking và load balancing | 23/10/2025 | 23/10/2025 | [Video 121](https://www.youtube.com/watch?v=B3R87qxarWk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=121)<br>[Video 122](https://www.youtube.com/watch?v=PaEv0YFVVhI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=122)<br>[Video 123](https://www.youtube.com/watch?v=mW1Gxu8AT8c&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=123) |
| Thứ Sáu | - Build và deploy containerized web application đơn giản<br>- So sánh containers vs serverless architecture<br>- Ghi chép learnings và use cases | 24/10/2025 | 24/10/2025 | Thực hành và ôn tập<br>Build container project |

---

## Kết quả đạt được tuần 7

• Học các khái niệm containerization và Docker basics (images, containers, Dockerfile syntax).  
• Tạo Dockerfile đầu tiên và build Docker images locally với layer management đúng cách.  
• Push Docker images lên ECR (Elastic Container Registry) sau khi cấu hình authentication.  
• Giới thiệu về ECS - hiểu clusters, task definitions, tasks và services architecture.  
• Deploy containerized web application sử dụng ECS Fargate với Application Load Balancer configuration.  
• So sánh containers vs serverless architecture và học các use cases phù hợp cho mỗi approach.  
• Thực hành tạo containerized Node.js application đơn giản từ scratch đến deployment.  
• Cải thiện hiểu biết về container orchestration và khi nào nên dùng containers thay vì EC2 truyền thống.


