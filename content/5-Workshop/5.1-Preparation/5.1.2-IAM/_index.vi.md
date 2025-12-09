---
title: "Tạo IAM Role"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 5.1.2 </b> "
---

# Tạo IAM Role cho EC2

EC2 cần quyền truy cập vào S3 để lấy code/ảnh, và quyền gọi API của Rekognition và Textract. Thay vì lưu Access Key trong code, ta sẽ dùng IAM Role gán cho EC2.

## Các bước thực hiện

1. Truy cập **IAM Dashboard**.
2. Chọn **Roles** -> **Create role**.
3. Tại bước **Trusted entity type**, chọn **AWS service**.
4. Tại **Use case**, chọn **EC2**.
5. Nhấn **Next**.

![IAM Step 1](/images/2-Proposal/iam-1.png)

1. Tại bước **Add permissions**, tìm và chọn các Policy sau:
    - `AmazonS3FullAccess` (Hoặc policy giới hạn chỉ bucket của pj).
    - `AmazonRekognitionFullAccess`.
    - `AmazonTextractFullAccess`.
    - `AmazonSSMManagedInstanceCore` (Để remote vào EC2 qua Session Manager nếu cần).
2. Nhấn **Next**.
3. Đặt tên Role là `Auction-EC2-Role`.
4. Xem lại và nhấn **Create role**.

![IAM Step 2](/images/2-Proposal/iam-2.png)
