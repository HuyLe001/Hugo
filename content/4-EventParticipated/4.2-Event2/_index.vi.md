---
title: "Event 2"
date: "2025-09-11"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# WORKSHOP DEVOPS TRÊN AWS

### Thông Tin Sự Kiện

**Thời gian:** Thứ Hai, ngày 17 tháng 11 năm 2025, 8:30 – 17:00  
**Địa điểm:** Văn phòng AWS Vietnam  
**Vai trò:** Người tham dự

### Mục Đích Của Sự Kiện

Workshop được thiết kế để cung cấp kiến thức toàn diện và trải nghiệm thực hành với các dịch vụ DevOps của AWS, bao gồm CI/CD pipelines, Infrastructure as Code, container services, và monitoring & observability. Sự kiện nhằm giúp người tham dự hiểu về văn hóa DevOps, nguyên tắc và best practices đồng thời khám phá cách triển khai thực tế các quy trình DevOps trên AWS.

### Tổng Quan Chương Trình

#### Phiên Buổi Sáng (8:30 – 12:00)

**8:30 – 9:00 | Chào Mừng & Tư Duy DevOps**

- Tóm tắt phiên AI/ML từ workshop trước
- **Văn Hóa và Nguyên Tắc DevOps:** Hiểu về sự chuyển đổi văn hóa từ IT truyền thống sang DevOps, nhấn mạnh hợp tác, tự động hóa và cải tiến liên tục
- **Lợi Ích và Chỉ Số Chính:**
  - **DORA Metrics:** Tần suất triển khai, thời gian lead time cho thay đổi, mean time to recovery (MTTR), tỷ lệ thất bại thay đổi
  - **MTTR (Mean Time To Recovery):** Đo lường tốc độ phục hồi từ lỗi của các team
  - **Tần Suất Triển Khai:** Theo dõi tần suất các team deploy code lên production
- Thảo luận về cách các thực hành DevOps cải thiện việc giao hàng phần mềm và hiệu suất vận hành

**9:00 – 10:30 | Dịch Vụ DevOps AWS – CI/CD Pipeline**

**Source Control: AWS CodeCommit, Chiến Lược Git**

- **AWS CodeCommit:** Dịch vụ source control được quản lý hoàn toàn, repositories Git an toàn
- **Chiến Lược Git:**
  - **GitFlow:** Feature branches, develop, release branches workflow
  - **Trunk-based Development:** Tập trung vào main branch, feature branches ngắn hạn
- Best practices cho branching strategies dựa trên quy mô team và yêu cầu dự án

**Build & Test: Cấu Hình CodeBuild, Testing Pipelines**

- **AWS CodeBuild:** Dịch vụ build được quản lý hoàn toàn, compile source code, chạy tests và tạo software packages sẵn sàng deploy
- **Cấu Hình Build:** Buildspec files, environment variables và build artifacts
- **Testing Pipelines:** Unit tests, integration tests và thực thi test tự động
- Tích hợp với testing frameworks và công cụ chất lượng code

**Deployment: CodeDeploy với Blue/Green, Canary và Rolling Updates**

- **AWS CodeDeploy:** Triển khai ứng dụng tự động đến EC2, Lambda hoặc on-premises servers
- **Blue/Green Deployment:** Triển khai zero-downtime bằng cách chạy hai môi trường production giống hệt nhau
- **Canary Deployment:** Rollout dần dần đến một phần trăm nhỏ người dùng trước khi triển khai đầy đủ
- **Rolling Updates:** Triển khai tăng dần qua các instances với khả năng rollback tự động
- Chọn chiến lược triển khai phù hợp dựa trên yêu cầu ứng dụng

**Orchestration: Tự Động Hóa CodePipeline**

- **AWS CodePipeline:** Dịch vụ continuous delivery được quản lý hoàn toàn để tự động hóa release pipelines
- **Pipeline Stages:** Source, Build, Test, Deploy và Approval stages
- **Tích Hợp:** Kết nối CodeCommit, CodeBuild, CodeDeploy và các dịch vụ AWS khác
- **Tự Động Hóa:** Automated triggers, thực thi song song và visualization pipeline

**Demo: Full CI/CD Pipeline Walkthrough**

Phần trình diễn giới thiệu pipeline CI/CD hoàn chỉnh:
- Thiết lập CodeCommit repository
- Cấu hình CodeBuild cho automated builds và tests
- Tạo CodeDeploy application với Blue/Green deployment
- Xây dựng CodePipeline để điều phối toàn bộ workflow
- Test pipeline với code changes và quan sát automated deployment

**10:30 – 10:45 | Giải Lao**

Networking và đồ uống.

**10:45 – 12:00 | Infrastructure as Code (IaC)**

**AWS CloudFormation: Templates, Stacks và Drift Detection**

- **CloudFormation Templates:** Templates JSON/YAML để định nghĩa AWS resources
- **Stacks:** Tập hợp các AWS resources được quản lý như một đơn vị
- **Drift Detection:** Xác định các thay đổi được thực hiện bên ngoài CloudFormation
- **Stack Updates:** Cập nhật infrastructure với change sets và khả năng rollback
- **Best Practices:** Tổ chức template, parameterization và nested stacks

**AWS CDK (Cloud Development Kit): Constructs, Patterns Tái Sử Dụng và Hỗ Trợ Ngôn Ngữ**

- **AWS CDK:** Định nghĩa cloud infrastructure sử dụng các ngôn ngữ lập trình quen thuộc (TypeScript, Python, Java, C#, Go)
- **Constructs:** Các cloud components tái sử dụng, từ low-level resources đến high-level patterns
- **Patterns Tái Sử Dụng:** Giải pháp pre-built cho các use case phổ biến (VPC, ECS clusters, serverless applications)
- **Hỗ Trợ Ngôn Ngữ:** TypeScript, Python, Java, C#, Go và JavaScript
- **Lợi Ích:** Type safety, IDE support và dễ test hơn so với CloudFormation templates

**Demo: Triển Khai với CloudFormation và CDK**

Phần trình diễn so sánh cả hai cách tiếp cận:
- CloudFormation: Triển khai VPC và EC2 instance sử dụng YAML template
- CDK: Cùng infrastructure sử dụng TypeScript với CDK constructs
- Làm nổi bật sự khác biệt trong cách tiếp cận, khả năng bảo trì và developer experience

**Thảo Luận: Lựa Chọn Giữa Các Công Cụ IaC**

- Khi nào sử dụng CloudFormation vs CDK
- Cân nhắc: chuyên môn team, độ phức tạp dự án và yêu cầu bảo trì
- Cách tiếp cận hybrid: Sử dụng cả hai công cụ cho các phần khác nhau của infrastructure

**Giải Lao Trưa (12:00 – 13:00)**

Giải lao trưa tự túc.

#### Phiên Buổi Chiều (13:00 – 17:00)

**13:00 – 14:30 | Container Services trên AWS**

**Docker Cơ Bản: Microservices và Containerization**

- **Khái Niệm Containerization:** Hiểu về containers, images và lợi ích của containerization
- **Kiến Trúc Microservices:** Chia nhỏ monolithic applications thành các services nhỏ hơn, độc lập
- **Docker Cơ Bản:** Dockerfile, image building, container lifecycle
- **Lợi Ích:** Portability, consistency và resource efficiency

**Amazon ECR: Lưu Trữ Image, Scanning, Lifecycle Policies**

- **Amazon ECR:** Docker container registry được quản lý hoàn toàn
- **Lưu Trữ Image:** Lưu trữ an toàn, có thể mở rộng cho Docker images
- **Image Scanning:** Quét lỗ hổng tự động cho container images
- **Lifecycle Policies:** Tự động hóa cleanup và retention policies cho images
- **Tích Hợp:** Tích hợp liền mạch với ECS, EKS và các dịch vụ AWS khác

**Amazon ECS & EKS: Chiến Lược Triển Khai, Scaling và Orchestration**

- **Amazon ECS:** Dịch vụ container orchestration được quản lý hoàn toàn
  - **Task Definitions:** Đặc tả container, yêu cầu tài nguyên và networking
  - **Services:** Long-running tasks với load balancing và auto-scaling
  - **Chiến Lược Triển Khai:** Rolling updates, Blue/Green deployments
  - **Scaling:** Auto-scaling dựa trên CPU, memory hoặc custom metrics
- **Amazon EKS:** Dịch vụ Kubernetes được quản lý
  - **Khái Niệm Kubernetes:** Pods, Services, Deployments và Namespaces
  - **Tính Năng EKS:** Managed control plane, node groups và add-ons
  - **Chiến Lược Triển Khai:** Rolling updates, Canary deployments với Istio/App Mesh
  - **Scaling:** Cluster autoscaler và horizontal pod autoscaler

**AWS App Runner: Triển Khai Container Đơn Giản**

- **App Runner:** Dịch vụ được quản lý hoàn toàn để build và chạy ứng dụng containerized
- **Triển Khai Đơn Giản:** Deploy từ source code hoặc container image
- **Auto-scaling:** Tự động scaling dựa trên traffic
- **Use Cases:** Web applications, APIs và microservices
- **So Sánh:** Khi nào sử dụng App Runner vs ECS vs EKS

**Demo & Case Study: So Sánh Triển Khai Microservices**

Phần trình diễn so sánh các tùy chọn triển khai container khác nhau:
- Triển khai web application đơn giản với App Runner
- Cùng ứng dụng với ECS Fargate
- So sánh độ phức tạp setup, chi phí và operational overhead
- Case study: Chọn dịch vụ container phù hợp cho các scenario khác nhau

**14:30 – 14:45 | Giải Lao**

Networking và đồ uống.

**14:45 – 16:00 | Monitoring & Observability**

**CloudWatch: Metrics, Logs, Alarms và Dashboards**

- **CloudWatch Metrics:** Thu thập và theo dõi metrics từ AWS services và custom applications
- **CloudWatch Logs:** Centralized logging, log groups và log streams
- **CloudWatch Alarms:** Hành động tự động dựa trên metric thresholds
- **CloudWatch Dashboards:** Dashboards có thể tùy chỉnh để visualize metrics và logs
- **Best Practices:** Quy ước đặt tên metric, log retention và cấu hình alarm

**AWS X-Ray: Distributed Tracing và Performance Insights**

- **AWS X-Ray:** Dịch vụ phân tích và debug distributed applications
- **Distributed Tracing:** End-to-end request tracing qua microservices
- **Service Map:** Biểu diễn trực quan kiến trúc ứng dụng và dependencies
- **Performance Insights:** Xác định bottlenecks và vấn đề hiệu suất
- **Tích Hợp:** Tích hợp X-Ray SDK với applications và AWS services

**Demo: Thiết Lập Full-Stack Observability**

Phần trình diễn cho thấy:
- Thiết lập CloudWatch metrics và logs cho ứng dụng
- Tạo CloudWatch dashboards để monitoring
- Cấu hình CloudWatch alarms để alerting
- Bật X-Ray tracing cho distributed tracing
- Xem service maps và trace analysis

**Best Practices: Alerting, Dashboards và Quy Trình On-Call**

- **Chiến Lược Alerting:** Thiết lập alerts có ý nghĩa, tránh alert fatigue
- **Thiết Kế Dashboard:** Tạo dashboards hiệu quả cho các đối tượng khác nhau (developers, operations, management)
- **Quy Trình On-Call:** Thủ tục phản ứng sự cố, escalation paths và runbooks
- **SLO/SLI:** Service Level Objectives và Indicators để đo lường độ tin cậy

**16:00 – 16:45 | DevOps Best Practices & Case Studies**

**Chiến Lược Triển Khai: Feature Flags, A/B Testing**

- **Feature Flags:** Rollout tính năng dần dần, canary releases và rollback tức thì
- **A/B Testing:** So sánh các phiên bản khác nhau để tối ưu trải nghiệm người dùng
- **Công Cụ:** AWS AppConfig, tích hợp LaunchDarkly
- **Best Practices:** Quản lý feature flags và chiến lược testing

**Automated Testing và Tích Hợp CI/CD**

- **Testing Pyramid:** Unit tests, integration tests và end-to-end tests
- **Test Automation:** Thực thi test tự động trong CI/CD pipelines
- **Quality Gates:** Chặn deployments dựa trên kết quả test
- **Test Coverage:** Đo lường và cải thiện test coverage

**Quản Lý Sự Cố và Postmortems**

- **Phản Ứng Sự Cố:** Thủ tục phát hiện, phản ứng và phục hồi
- **Postmortems:** Học hỏi từ sự cố, ghi lại root causes
- **Văn Hóa Không Đổ Lỗi:** Tập trung vào cải thiện hệ thống thay vì đổ lỗi cá nhân
- **Công Cụ:** Công cụ quản lý sự cố và kênh giao tiếp

**Case Studies: Chuyển Đổi DevOps của Startups và Doanh Nghiệp**

- **Case Study Startup:** Scaling nhanh với thực hành DevOps, tối ưu chi phí
- **Case Study Doanh Nghiệp:** Migration quy mô lớn sang DevOps, chuyển đổi văn hóa
- **Bài Học:** Thách thức và giải pháp phổ biến
- **ROI:** Đo lường tác động của việc áp dụng DevOps

**16:45 – 17:00 | Q&A & Tổng Kết**

- **Lộ Trình Nghề Nghiệp DevOps:** Tiến trình nghề nghiệp trong DevOps, kỹ năng cần thiết
- **Lộ Trình Chứng Chỉ AWS:** Các chứng chỉ AWS liên quan cho DevOps engineers
  - AWS Certified DevOps Engineer – Professional
  - AWS Certified Solutions Architect
  - AWS Certified SysOps Administrator
- **Bước Tiếp Theo:** Tài nguyên để tiếp tục học tập và thực hành
- **Kết Luận:** Tóm tắt các điểm chính và action items

### Nội Dung Nổi Bật

- **CI/CD Pipeline:** AWS CodePipeline cung cấp giải pháp hoàn chỉnh để tự động hóa software delivery từ source đến production
- **Infrastructure as Code:** Cả CloudFormation và CDK đều cung cấp cách mạnh mẽ để quản lý infrastructure, với CDK cung cấp developer experience tốt hơn
- **Container Services:** AWS cung cấp nhiều tùy chọn container (ECS, EKS, App Runner) cho các use case và mức độ phức tạp khác nhau
- **Observability:** CloudWatch và X-Ray cùng nhau cung cấp khả năng monitoring và tracing toàn diện
- **Văn Hóa DevOps:** Thành công yêu cầu thay đổi văn hóa, không chỉ công cụ và công nghệ
- **Best Practices:** Feature flags, automated testing và incident management là cần thiết cho DevOps hiện đại

### Những Gì Tôi Học Được

- **DevOps Là Văn Hóa Trước:** Công cụ quan trọng, nhưng chuyển đổi văn hóa là nền tảng của thành công DevOps
- **Tự Động Hóa CI/CD:** Tự động hóa toàn bộ software delivery pipeline cải thiện đáng kể tốc độ và độ tin cậy
- **Lợi Ích IaC:** Infrastructure as Code cho phép version control, repeatability và thay đổi infrastructure nhanh hơn
- **Chiến Lược Container:** Chọn dịch vụ container phù hợp phụ thuộc vào độ phức tạp, chuyên môn team và yêu cầu vận hành
- **Observability Quan Trọng:** Monitoring và tracing toàn diện là cần thiết để duy trì hệ thống đáng tin cậy
- **Cải Tiến Liên Tục:** DevOps là về học tập và cải tiến liên tục, không phải triển khai một lần

### Ứng Dụng Vào Công Việc

- **Triển Khai CI/CD:** Thiết lập CodePipeline cho automated deployments trong các dự án hiện tại
- **Áp Dụng IaC:** Bắt đầu sử dụng CloudFormation hoặc CDK để quản lý infrastructure
- **Migration Container:** Đánh giá cơ hội containerization cho các ứng dụng hiện có
- **Cải Thiện Monitoring:** Nâng cao CloudWatch dashboards và alarms để có visibility tốt hơn
- **Thực Hành DevOps:** Áp dụng nguyên tắc và thực hành DevOps trong công việc hàng ngày
- **Quản Lý Sự Cố:** Thiết lập thủ tục phản ứng sự cố và thực hành postmortem

### Trải Nghiệm Cá Nhân

Workshop DevOps cả ngày này toàn diện và rất thực tế:

- Demo CI/CD pipeline đặc biệt có giá trị, cho thấy cách tự động hóa toàn bộ quy trình software delivery
- Tìm hiểu về các công cụ IaC khác nhau giúp tôi hiểu khi nào sử dụng CloudFormation vs CDK
- So sánh container services cung cấp hướng dẫn rõ ràng về chọn dịch vụ phù hợp cho các scenario khác nhau
- Phiên observability nhấn mạnh tầm quan trọng của monitoring và tracing để duy trì hệ thống đáng tin cậy
- Các case studies cung cấp insight thực tế về chuyển đổi DevOps
- Thảo luận về lộ trình nghề nghiệp rất động viên và cung cấp hướng rõ ràng cho phát triển chuyên môn

### Bài Học Rút Ra

- **Bắt Đầu Nhỏ:** Bắt đầu với tự động hóa CI/CD cơ bản và dần dần mở rộng thực hành DevOps
- **Văn Hóa Quan Trọng:** Thành công DevOps yêu cầu hợp tác team và thay đổi văn hóa
- **Chọn Công Cụ Đúng:** Chọn công cụ dựa trên chuyên môn team và yêu cầu dự án
- **Monitor Mọi Thứ:** Observability toàn diện là cần thiết cho hệ thống đáng tin cậy
- **Học Liên Tục:** Thực hành DevOps phát triển nhanh chóng, yêu cầu học tập liên tục
- **Đo Lường Thành Công:** Sử dụng DORA metrics để theo dõi cải thiện DevOps và ROI

### Một Số Hình Ảnh

![Hình ảnh sự kiện 1](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event4/1.jpg)

![Hình ảnh sự kiện 2](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event4/2.jpg)

![Hình ảnh sự kiện 3](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event4/3.jpg)

![Hình ảnh sự kiện 4](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event4/4.jpg)
