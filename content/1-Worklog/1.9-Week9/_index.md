---
title: "Week 9 Worklog"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

{{% notice warning %}}  
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.  
{{% /notice %}}

## Week 9 Objectives

• Learn about AWS workflow orchestration with Step Functions  
• Understand event-driven architecture with EventBridge  
• Practice advanced Lambda integration patterns  
• Explore container orchestration concepts

---

## Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
|:---:|:-----|:----------:|:---------------:|:-------------------|
| Monday | - Introduction to AWS Step Functions<br>- Learn about workflow orchestration<br>- Understand state machines and workflows | 03/11/2025 | 03/11/2025 | [Video 48](https://www.youtube.com/watch?v=Eg-AeKi-kfU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=48)<br>[Video 49](https://www.youtube.com/watch?v=qN0aq6VLqAU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=49)<br>[Video 50](https://www.youtube.com/watch?v=fMGw40i1ukw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=50) |
| Tuesday | - Create Step Functions workflows<br>- Practice coordinating multiple Lambda functions<br>- Learn about error handling in workflows | 04/11/2025 | 04/11/2025 | [Video 51](https://www.youtube.com/watch?v=uFBb8BnSGm4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=51)<br>[Video 52](https://www.youtube.com/watch?v=rKZBjKq-A9g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=52)<br>[Video 53](https://www.youtube.com/watch?v=sQBLpJvFP1M&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=53) |
| Wednesday | - Introduction to Amazon EventBridge<br>- Learn about event-driven architecture<br>- Understand event routing and patterns | 05/11/2025 | 05/11/2025 | [Video 75](https://www.youtube.com/watch?v=aIazn-nCagY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=75)<br>[Video 76](https://www.youtube.com/watch?v=qdqkPxgAi3s&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=76)<br>[Video 77](https://www.youtube.com/watch?v=YZx7lZaGMJw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=77) |
| Thursday | - Practice EventBridge with Lambda integration<br>- Create event rules and targets<br>- Build event-driven workflows | 06/11/2025 | 06/11/2025 | [Video 78](https://www.youtube.com/watch?v=G_9EpfKxXNM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=78)<br>[Video 79](https://www.youtube.com/watch?v=VrzejJBWDLE&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=79)<br>[Video 54](https://www.youtube.com/watch?v=pB0CjiR3YLM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=54) |
| Friday | - Build integrated workflow project<br>- Combine Step Functions + EventBridge + Lambda<br>- Review week's learnings | 07/11/2025 | 07/11/2025 | [Video 124](https://www.youtube.com/watch?v=SVRVnGU63qg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=124)<br>[Video 125](https://www.youtube.com/watch?v=rHh8LFzmWXg&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=125)<br>[Video 126](https://www.youtube.com/watch?v=2LmRXbhVjNI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=126) |

---

## Week 9 Achievements

• Learned AWS Step Functions for workflow orchestration using state machines and Amazon States Language (JSON).  
• Created workflows with different state types: Task, Choice, Wait, Parallel, Map, Pass, Succeed/Fail.  
• Implemented error handling and retry logic in Step Functions for robust workflow management.  
• Learned Amazon EventBridge for event-driven architecture including event rules, patterns, and routing.  
• Built event-driven applications routing S3 events to Lambda functions via EventBridge triggers.  
• Created integrated project combining EventBridge, Step Functions, and Lambda for complex multi-step data processing.  
• Practiced basic encryption with KMS (Key Management Service) for securing Lambda environment variables and S3 objects.  
• Learned to use Secrets Manager to store database credentials and API keys securely instead of hardcoding in Lambda.  
• Understood when to use Step Functions for long-running workflows vs direct Lambda invocation.  
• Practiced creating event patterns and scheduled events for automated task execution.
