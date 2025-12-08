---
title: "Translated Blogs"
date: "2025-09-11"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# TRANSLATED BLOGS

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please do not copy verbatim for your own report, including this warning.
{{% /notice %}}

---

This section lists and introduces the AWS blogs that have been translated from English to Vietnamese as part of the FCJ internship program.

---

### [Blog 1 - Authentication for Mobile Games](3.1-Blog1/)

This blog explores the critical challenges of implementing authentication and authorization systems for mobile games. You will learn about common obstacles such as supporting anonymous users, creating frictionless sign-up processes, handling offline authentication, and protecting against client tampering. The article provides comprehensive guidance on what to look for in an authentication solution, including security requirements (TLS v1.2+, encrypted storage), user experience considerations, scalability needs, and best practices like utilizing app store protection mechanisms (Play Integrity API, DeviceCheck) and following OAuth 2.0 security standards.

---

### [Blog 2 - Making SaaS Products Accessible in AWS Marketplace](3.2-Blog2/)

This comprehensive guide explains the three main access options for SaaS sellers in AWS Marketplace. You will discover how to use the seller's website with AWS Marketplace serverless integration, Quick Launch implementation using pre-configured CloudFormation templates, and AWS PrivateLink configuration for enhanced security. Each option includes detailed implementation steps, workshop resources, and architectural diagrams showing how ISV provider accounts connect to customer consumer accounts through various access methods.

---

### [Blog 3 - Game Developer's Guide to Amazon DocumentDB Serverless](3.3-Blog3/)

This blog introduces how Amazon DocumentDB Serverless helps game developers handle unpredictable player traffic while optimizing costs. You will learn about DocumentDB Capacity Units (DCUs), automatic scaling mechanisms that adjust from 0.5 to 256 DCUs based on actual demand, and real gaming scenarios including live service games with season finale events, cross-platform MMOs with global raid boss launches, and mobile games that go viral on TikTok. It covers migration strategies from MongoDB, CloudWatch monitoring metrics, and best practices for ensuring reliability and scalability.

---

### [Blog 4 - Monitoring Server Health with Amazon GameLift Servers](3.4-Blog4/)

This technical guide demonstrates how to use Amazon GameLift Servers telemetry metrics with Amazon Managed Grafana dashboards to diagnose game server issues. You will learn how to troubleshoot game server crashes by analyzing memory usage patterns, identify which specific game sessions are consuming excessive resources, and investigate high CPU usage that causes stuttering gameplay. The article walks through seven pre-built Grafana dashboards and explains how to implement custom metrics for game-specific health indicators like combat balance, progression blockers, and economy health.

---

### [Blog 5 - Strengthen Foundation Model Queries Through Amazon Bedrock-Amazon Alexa Integration](3.5-Blog5/)

This blog presents a solution developed for the Federal Institute of São Paulo (IFSP) to generate SQL queries from natural language questions using Amazon Bedrock and Alexa. You will learn how Claude 3 Haiku model addresses the hallucination problem when dealing with structured data by generating SQL code instead of directly interpreting tables. The article details the complete architecture including Alexa Skills Kit, AWS Lambda, Amazon Athena, AWS Glue Data Catalog, and Amazon EventBridge. It covers prompt engineering techniques, security implementation with IAM roles and policies, and data encryption using AWS KMS.

---

### [Blog 6 - Wicked Saints Studios Integrates TikTok Within World Reborn Using AWS](3.6-Blog6/)

This case study shows how Wicked Saints Studios built a TikTok authentication integration for their mobile game World Reborn using the Guidance for Custom Game Backend Hosting on AWS. You will learn how they overcame challenges including deep link encoding, redirect allowlist mismatches, and extended TikTok API approval times. The article presents the complete OAuth flow implementation with C# code examples for server endpoints, Unity client integration using deep links and REST APIs, and security measures including token encryption in AWS Secrets Manager and metadata storage in Amazon DocumentDB.
