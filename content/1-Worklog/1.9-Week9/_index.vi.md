---
title: "Worklog Tuần 9"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

{{% notice warning %}}  
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.  
{{% /notice %}}

## Mục tiêu tuần 9

• Học về AWS workflow orchestration với Step Functions  
• Hiểu event-driven architecture với EventBridge  
• Thực hành advanced Lambda integration patterns  
• Khám phá container orchestration concepts

---

## Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|:---:|:-----|:----------:|:---------------:|:-------------------|
| Thứ Hai | - Giới thiệu về AWS Step Functions<br>- Học về workflow orchestration<br>- Hiểu state machines và workflows | 03/11/2025 | 03/11/2025 | [Video 48](https://www.youtube.com/watch?v=Eg-AeKi-kfU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=48)<br>[Video 49](https://www.youtube.com/watch?v=qN0aq6VLqAU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=49)<br>[Video 50](https://www.youtube.com/watch?v=fMGw40i1ukw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=50) |
| Thứ Ba | - Tạo Step Functions workflows<br>- Thực hành phối hợp nhiều Lambda functions<br>- Học về error handling trong workflows | 04/11/2025 | 04/11/2025 | [Video 51](https://www.youtube.com/watch?v=uFBb8BnSGm4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=51)<br>[Video 52](https://www.youtube.com/watch?v=rKZBjKq-A9g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=52)<br>[Video 53](https://www.youtube.com/watch?v=sQBLpJvFP1M&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=53) |
| Thứ Tư | - Giới thiệu về Amazon EventBridge<br>- Học về event-driven architecture<br>- Hiểu event routing và patterns | 05/11/2025 | 05/11/2025 | [Video 75](https://www.youtube.com/watch?v=aIazn-nCagY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=75)<br>[Video 76](https://www.youtube.com/watch?v=qdqkPxgAi3s&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=76)<br>[Video 77](https://www.youtube.com/watch?v=YZx7lZaGMJw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=77) |
| Thứ Năm | - Thực hành EventBridge với Lambda integration<br>- Tạo event rules và targets<br>- Build event-driven workflows | 06/11/2025 | 06/11/2025 | [Video 78](https://www.youtube.com/watch?v=G_9EpfKxXNM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=78)<br>[Video 79](https://www.youtube.com/watch?v=VrzejJBWDLE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=79)<br>[Video 54](https://www.youtube.com/watch?v=pB0CjiR3YLM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=54) |
| Thứ Sáu | - Build integrated workflow project<br>- Kết hợp Step Functions + EventBridge + Lambda<br>- Ôn tập learnings của tuần | 07/11/2025 | 07/11/2025 | [Video 124](https://www.youtube.com/watch?v=SVRVnGU63qg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=124)<br>[Video 125](https://www.youtube.com/watch?v=rHh8LFzmWXg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=125)<br>[Video 126](https://www.youtube.com/watch?v=2LmRXbhVjNI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=126) |

---

## Kết quả đạt được tuần 9

• Học AWS Step Functions cho workflow orchestration sử dụng state machines và Amazon States Language (JSON).  
• Tạo workflows với các state types khác nhau: Task, Choice, Wait, Parallel, Map, Pass, Succeed/Fail.  
• Triển khai error handling và retry logic trong Step Functions cho quản lý workflow mạnh mẽ.  
• Học Amazon EventBridge cho event-driven architecture bao gồm event rules, patterns và routing.  
• Build event-driven applications routing S3 events đến Lambda functions qua EventBridge triggers.  
• Tạo integrated project kết hợp EventBridge, Step Functions và Lambda cho xử lý dữ liệu multi-step phức tạp.  
• Thực hành encryption cơ bản với KMS (Key Management Service) để bảo mật Lambda environment variables và S3 objects.  
• Học sử dụng Secrets Manager để lưu trữ database credentials và API keys an toàn thay vì hardcoding trong Lambda.  
• Hiểu khi nào dùng Step Functions cho long-running workflows vs direct Lambda invocation.  
• Thực hành tạo event patterns và scheduled events cho automated task execution.


