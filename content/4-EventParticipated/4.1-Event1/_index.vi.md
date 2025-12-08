---
title: "Event 1"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# WORKSHOP AI/ML/GENAI TRÊN AWS

### Thông Tin Sự Kiện

**Thời gian:** Thứ Bảy, ngày 15 tháng 11 năm 2025, 8:30 – 12:00  
**Địa điểm:** Văn phòng AWS Vietnam  
**Vai trò:** Người tham dự

### Mục Đích Của Sự Kiện

Workshop được thiết kế để cung cấp trải nghiệm thực hành với các dịch vụ AI/ML của AWS, tập trung vào Amazon SageMaker cho các quy trình machine learning truyền thống và Amazon Bedrock cho các ứng dụng generative AI. Sự kiện nhằm giúp người tham dự hiểu cách triển khai thực tế các giải pháp AI/ML trên AWS và khám phá các khả năng mới nhất trong generative AI.

### Tổng Quan Chương Trình

#### 8:30 – 9:00 | Chào Mừng & Giới Thiệu

- Đăng ký người tham dự và cơ hội networking
- Tổng quan workshop và trình bày mục tiêu học tập
- Hoạt động phá băng để thúc đẩy hợp tác
- Tổng quan về hệ sinh thái AI/ML tại Việt Nam

#### 9:00 – 10:30 | Tổng Quan Dịch Vụ AI/ML trên AWS

**Amazon SageMaker – Nền Tảng ML Toàn Diện**

- **Chuẩn Bị Dữ Liệu và Gán Nhãn:** Hiểu cách chuẩn bị dataset cho machine learning, bao gồm làm sạch dữ liệu, feature engineering, và khả năng gán nhãn tự động
- **Huấn Luyện, Tinh Chỉnh và Triển Khai Mô Hình:** Khám phá hạ tầng training của SageMaker, hyperparameter tuning, và các tùy chọn triển khai mô hình bao gồm real-time và batch inference
- **Khả Năng MLOps Tích Hợp:** Tìm hiểu về các tính năng MLOps tích hợp sẵn của SageMaker cho versioning mô hình, monitoring, và các pipeline retraining tự động

**Demo Trực Tiếp: SageMaker Studio Walkthrough**

Phần trình diễn giới thiệu môi trường phát triển thống nhất cho machine learning, bao gồm:
- Tích hợp Jupyter notebook cho phát triển tương tác
- Theo dõi thử nghiệm và đăng ký mô hình
- Visual workflow builder cho các pipeline MLOps
- Tích hợp với các dịch vụ AWS khác cho xử lý dữ liệu

#### 10:30 – 10:45 | Giải Lao

Phiên networking với đồ uống và thảo luận không chính thức về các use case AI/ML.

#### 10:45 – 12:00 | Generative AI với Amazon Bedrock

**Foundation Models: Claude, Llama, Titan – Hướng Dẫn So Sánh & Lựa Chọn**

- Hiểu về các foundation model khác nhau có sẵn trên Bedrock
- So sánh khả năng, use case và đặc điểm hiệu suất của các mô hình
- Best practices để lựa chọn mô hình phù hợp cho nhu cầu kinh doanh cụ thể
- Cân nhắc về chi phí và chiến lược tối ưu hóa

**Prompt Engineering: Kỹ Thuật, Chain-of-Thought Reasoning, Few-shot Learning**

- **Nguyên Tắc Cơ Bản Prompt Engineering:** Học cách tạo prompt hiệu quả để có được output mong muốn từ language models
- **Chain-of-Thought Reasoning:** Hiểu cách hướng dẫn mô hình qua quy trình lý luận từng bước cho giải quyết vấn đề phức tạp
- **Few-shot Learning:** Kỹ thuật cung cấp ví dụ để cải thiện hiệu suất mô hình trên các tác vụ cụ thể mà không cần fine-tuning

**Retrieval-Augmented Generation (RAG): Kiến Trúc & Tích Hợp Knowledge Base**

- **Tổng Quan Kiến Trúc RAG:** Hiểu cách RAG kết hợp việc truy xuất thông tin liên quan với khả năng generative
- **Tích Hợp Knowledge Base:** Học cách kết nối Bedrock với vector databases và knowledge bases (Amazon OpenSearch, Amazon Kendra)
- **Pattern Triển Khai:** Best practices để xây dựng ứng dụng RAG cung cấp phản hồi chính xác, có ngữ cảnh

**Bedrock Agents: Quy Trình Đa Bước và Tích Hợp Công Cụ**

- **Kiến Trúc Agent:** Hiểu cách Bedrock Agents có thể điều phối các quy trình đa bước phức tạp
- **Tích Hợp Công Cụ:** Học cách kết nối agents với external APIs, databases và các dịch vụ AWS
- **Thiết Kế Quy Trình:** Pattern để thiết kế ứng dụng dựa trên agent có thể xử lý các yêu cầu phức tạp của người dùng

**Guardrails: An Toàn và Lọc Nội Dung**

- **An Toàn Nội Dung:** Hiểu về Bedrock Guardrails để lọc nội dung có hại hoặc không phù hợp
- **Chính Sách Tùy Chỉnh:** Học cách cấu hình bộ lọc nội dung tùy chỉnh dựa trên yêu cầu kinh doanh
- **Tuân Thủ và Quản Trị:** Best practices để đảm bảo ứng dụng AI đáp ứng các tiêu chuẩn quy định và đạo đức

**Demo Trực Tiếp: Xây Dựng Chatbot Generative AI bằng Bedrock**

Phần trình diễn hướng dẫn tạo ứng dụng chatbot hoàn chỉnh:
- Thiết lập foundation model Bedrock
- Triển khai RAG với tích hợp knowledge base
- Cấu hình Bedrock Agents cho cuộc hội thoại đa lượt
- Thêm Guardrails cho an toàn nội dung
- Triển khai ứng dụng chatbot

### Nội Dung Nổi Bật

- **Nền Tảng ML Toàn Diện:** SageMaker cung cấp giải pháp end-to-end hoàn chỉnh cho machine learning, từ chuẩn bị dữ liệu đến triển khai và giám sát mô hình
- **Khả Năng Generative AI:** Amazon Bedrock cung cấp quyền truy cập vào nhiều foundation models, giúp dễ dàng thử nghiệm và chọn mô hình phù hợp cho từng use case
- **Kiến Trúc RAG:** Pattern RAG cho phép xây dựng ứng dụng AI có thể truy cập và sử dụng knowledge base cụ thể, cải thiện độ chính xác và tính liên quan
- **MLOps Sẵn Sàng Production:** Khả năng MLOps tích hợp của SageMaker đơn giản hóa quy trình triển khai và duy trì mô hình ML trong production
- **An Toàn Là Ưu Tiên:** Bedrock Guardrails đảm bảo các ứng dụng generative AI an toàn, tuân thủ và phù hợp với giá trị kinh doanh

### Những Gì Tôi Học Được

- SageMaker Studio cung cấp giao diện thống nhất cho toàn bộ vòng đời ML, cải thiện đáng kể năng suất của developer
- Lựa chọn foundation model là quan trọng và phụ thuộc vào use case cụ thể, yêu cầu hiệu suất và ràng buộc chi phí
- Prompt engineering là kỹ năng quan trọng có thể cải thiện đáng kể output của mô hình mà không cần fine-tuning
- Kiến trúc RAG là cần thiết để xây dựng ứng dụng AI cần truy cập thông tin cụ thể, cập nhật
- Bedrock Agents cho phép xây dựng ứng dụng AI tinh vi có thể xử lý các quy trình đa bước phức tạp
- An toàn nội dung phải được xem xét ngay từ đầu khi xây dựng ứng dụng generative AI

### Ứng Dụng Vào Công Việc

- **Thử Nghiệm SageMaker:** Thiết lập SageMaker Studio để khám phá phát triển mô hình ML cho các dự án phân tích dữ liệu
- **Xây Dựng Ứng Dụng RAG:** Triển khai kiến trúc RAG sử dụng Bedrock và knowledge bases cho hệ thống tài liệu nội bộ và Q&A
- **Thực Hành Prompt Engineering:** Phát triển kỹ năng prompt engineering bằng cách tạo templates và best practices cho các use case phổ biến
- **Tích Hợp MLOps:** Áp dụng khả năng MLOps của SageMaker để tự động hóa các pipeline training và triển khai mô hình
- **Triển Khai An Toàn:** Tích hợp Bedrock Guardrails vào bất kỳ ứng dụng generative AI nào để đảm bảo an toàn nội dung

### Trải Nghiệm Cá Nhân

Workshop này cung cấp giới thiệu thực hành tuyệt vời về các dịch vụ AI/ML của AWS:

- Demo SageMaker Studio đặc biệt ấn tượng, cho thấy cách một nền tảng thống nhất có thể tối ưu hóa toàn bộ quy trình ML
- Tìm hiểu về kiến trúc RAG rất mở mang tầm mắt, vì nó chứng minh cách xây dựng ứng dụng AI có thể tận dụng knowledge base cụ thể
- Trình diễn Bedrock Agents cho thấy tiềm năng xây dựng ứng dụng AI tinh vi có thể xử lý các quy trình phức tạp
- Tập trung thực tế vào prompt engineering cung cấp các kỹ năng có thể áp dụng ngay cho làm việc với language models
- Hiểu về Guardrails giúp tôi đánh giá cao tầm quan trọng của an toàn và tuân thủ trong ứng dụng AI

### Bài Học Rút Ra

- **Bắt Đầu Từ Use Case:** Luôn bắt đầu bằng cách xác định vấn đề kinh doanh cụ thể trước khi chọn giải pháp AI/ML
- **Foundation Models Mạnh Mẽ:** Các foundation model được pre-train có thể giải quyết nhiều vấn đề mà không cần training tùy chỉnh
- **RAG Là Cần Thiết:** Đối với ứng dụng yêu cầu kiến thức cụ thể, kiến trúc RAG là cách tiếp cận đúng đắn
- **MLOps Quan Trọng:** Thực hành MLOps đúng đắn là quan trọng để duy trì mô hình ML trong production
- **An Toàn Không Thể Bỏ Qua:** Lọc nội dung và biện pháp an toàn phải được tích hợp ngay từ đầu
- **Học Liên Tục:** Hệ sinh thái AI/ML phát triển nhanh chóng, yêu cầu học tập và thử nghiệm liên tục

## Một Số Hình Ảnh

![Hình ảnh sự kiện 1](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event3/1.jpg)

![Hình ảnh sự kiện 2](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event3/2.jpg)

![Hình ảnh sự kiện 3](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event3/3.jpg)

![Hình ảnh sự kiện 4](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event3/4.jpg)

![Hình ảnh sự kiện 4](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event3/5.jpg)