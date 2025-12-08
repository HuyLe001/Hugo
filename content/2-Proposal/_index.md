---
title: "Proposal"
date: "2025-11-11"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice warning %}}

{{% /notice %}}

# CloudRead – Online Ebook Reading Platform  
## Online Book Reading and Management Solution on Java + AWS Platform  

### 1. Executive Summary  
**CloudRead** is an academic project by a team of 5 Information Technology students, aimed at developing an electronic book (ebook) reading and management platform running on **AWS infrastructure**.  
Users can register accounts, search for and read ebooks online through an integrated PDF reader, while receiving email notifications or password recovery support via **Amazon SES**.  
The system is developed using **Spring Boot (Java 17)** for the backend, **HTML/CSS/JavaScript (Vanilla JS)** for the frontend, and deployed on **AWS** with services including **EC2, RDS, S3, CloudFront, SES, IAM, CloudWatch, and CodePipeline**.  
The project's goal is to build a stable, low-cost, scalable digital book reading platform with high academic value.  

---

### 2. Problem Statement  

*Current Problem*  
Most free ebook platforms like **nhasachmienphi.com** only allow users to download or read directly, lacking basic features such as user roles, access statistics, or content ratings.  
Additionally, many commercial platforms have high deployment and operating costs, unsuitable for student-scale or academic projects.  

*Solution*  
CloudRead is designed as a learning platform – a technology demonstration that helps:  
- Store and distribute ebooks via **Amazon S3 + CloudFront (Signed URL)**.  

- Manage users, books, and reviews via **Amazon RDS MySQL**.  
- Deploy Spring Boot backend directly on **Amazon EC2**.  
- Publish static frontend interface via **S3 + CloudFront**.  
- Send confirmation emails and user support via **Amazon SES (SMTP)**.  
- Automate build & deploy processes using **AWS CodePipeline → CodeBuild → CodeDeploy**.  
- Monitor logs, performance, and costs via **Amazon CloudWatch**.  

*Benefits & ROI*  
- Helps students practice the complete development and deployment process of real cloud applications.  
- Easy to operate, can run 24/7 on AWS with low costs.  
- Strengthens knowledge of distributed systems, security, DevOps, and infrastructure optimization.  
- The product can be expanded with additional learning, sharing, and book categorization features in the future.  

---

### 3. Solution Architecture  

CloudRead uses a **3-tier model combined with AWS services**.  
Users access the website through **Route 53**, receiving static content distributed via **CloudFront** from **S3 (Frontend Bucket)**.  
When users log in, search, or open books, requests are sent to **EC2 (Spring Boot Backend)**. EC2 accesses the **RDS MySQL** database in a private subnet to retrieve user, book, and review information, while also accessing files from **S3 private bucket**.  
When notifications or support are needed, the system sends emails via **Amazon SES**.  
The entire backend source code is built and deployed automatically through **CodePipeline → CodeBuild → CodeDeploy**, and monitored via **CloudWatch**.  

*Main AWS Services:*  
- **Amazon EC2**: runs Spring Boot backend.  
- **Amazon RDS (MySQL)**: stores user, book, and review data.  
- **Amazon S3 + CloudFront**: stores and distributes web content and book files.  
- **Amazon SES**: sends confirmation and user support emails.  
- **Amazon IAM**: manages access permissions between EC2, S3, and SES.  
- **Amazon CodePipeline/CodeBuild/CodeDeploy**: automates deployment.  
- **Amazon CloudWatch**: monitors logs, performance, and cost alerts.  

---

### 4. Technical Implementation  

*Implementation Phases*  
1. **Local Development (1–2 weeks)**: design database, write APIs for user and book management, create PDF reading interface using HTML/JS.  
2. **AWS Setup (2 weeks)**: create EC2, RDS, S3, CloudFront, SES and configure secure IAM Roles.  
3. **CI/CD Integration (1 week)**: set up CodePipeline – CodeBuild – CodeDeploy to automatically build and update the application.  
4. **Testing & Demo (1 week)**: test book reading, review, email sending, login/registration, and content management features.  

*Technical Requirements*  
- Java 17 + Spring Boot  
- MySQL (local → RDS)  
- HTML/CSS/JavaScript (Vanilla JS + PDF.js)  
- AWS SDK for Java (S3 + SES)  
- GitHub, CodePipeline/CodeBuild/CodeDeploy  
- Postman, CloudWatch  

---

### 5. Roadmap & Milestones  

- **Month 1**: Design database, write APIs and basic interface.  
- **Month 2**: Configure AWS RDS, S3, CloudFront, SES.  
- **Month 3**: Integrate CI/CD, test and present CloudRead demo version.  

---

### 6. Budget Estimate  

The operating cost of the CloudRead system is estimated at approximately **$15–17 USD/month**, including EC2 (~$6.5 USD), RDS (~$7 USD), S3 and CloudFront (~$0.7 USD), SES (~$0.15 USD), CI/CD (~$1 USD), and CloudWatch (~$0.1 USD).  
When leveraging **AWS Free Tier** and **AWS Student Credit ($100)**, the actual cost is nearly **$0 USD/month** during the initial phase.  

---

### 7. Risk Assessment  

Main risks include AWS service connectivity loss, data breaches, and exceeding free tier limits.  
Preventive measures include:  
- Set up **private bucket + Signed URL** for book files.  
- Configure **Billing Alarm** to monitor costs.  
- Verify SES domain to ensure stable email delivery.  
- Create periodic snapshots for EC2 and RDS.  
If the pipeline fails, the team can **manually rollback** to a stable version.  

*Contingency Solutions:*  
- Keep a local running version for offline demos.  
- Monitor logs using CloudWatch and regularly control costs.  

---

### 8. Expected Results  

Upon completion, **CloudRead** will be a complete online ebook reading and management platform, deployed on AWS.  
The project helps the team master full-stack and basic DevOps skills: development, deployment, monitoring, and cloud system cost optimization.  
In the long term, CloudRead can be expanded with community features, book recommendations, device synchronization, and user authentication via **Amazon Cognito**.  

---
