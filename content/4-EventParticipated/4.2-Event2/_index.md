---
title: "Event 2"
date: "2025-09-11"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
 **Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report, including this warning.
{{% /notice %}}

# DEVOPS ON AWS WORKSHOP

### Event Information

**Date & Time:** Monday, November 17, 2025, 8:30 AM – 5:00 PM  
**Location:** AWS Vietnam Office  
**Role:** Attendee

### Event Purpose

The workshop was designed to provide comprehensive knowledge and hands-on experience with AWS DevOps services, covering CI/CD pipelines, Infrastructure as Code, container services, and monitoring & observability. The event aimed to help participants understand DevOps culture, principles, and best practices while exploring practical implementation of DevOps workflows on AWS.

### Agenda Overview

#### Morning Session (8:30 AM – 12:00 PM)

**8:30 – 9:00 AM | Welcome & DevOps Mindset**

- Recap of AI/ML session from previous workshop
- **DevOps Culture and Principles:** Understanding the cultural shift from traditional IT to DevOps, emphasizing collaboration, automation, and continuous improvement
- **Benefits and Key Metrics:**
  - **DORA Metrics:** Deployment frequency, lead time for changes, mean time to recovery (MTTR), change failure rate
  - **MTTR (Mean Time To Recovery):** Measuring how quickly teams can recover from failures
  - **Deployment Frequency:** Tracking how often teams deploy code to production
- Discussion on how DevOps practices improve software delivery and operational performance

**9:00 – 10:30 AM | AWS DevOps Services – CI/CD Pipeline**

**Source Control: AWS CodeCommit, Git Strategies**

- **AWS CodeCommit:** Fully managed source control service, secure Git repositories
- **Git Strategies:**
  - **GitFlow:** Feature branches, develop, release branches workflow
  - **Trunk-based Development:** Main branch focused, short-lived feature branches
- Best practices for branching strategies based on team size and project requirements

**Build & Test: CodeBuild Configuration, Testing Pipelines**

- **AWS CodeBuild:** Fully managed build service that compiles source code, runs tests, and produces ready-to-deploy software packages
- **Build Configuration:** Buildspec files, environment variables, and build artifacts
- **Testing Pipelines:** Unit tests, integration tests, and automated test execution
- Integration with testing frameworks and code quality tools

**Deployment: CodeDeploy with Blue/Green, Canary, and Rolling Updates**

- **AWS CodeDeploy:** Automated application deployments to EC2, Lambda, or on-premises servers
- **Blue/Green Deployment:** Zero-downtime deployment by running two identical production environments
- **Canary Deployment:** Gradual rollout to a small percentage of users before full deployment
- **Rolling Updates:** Incremental deployment across instances with automatic rollback capabilities
- Choosing the right deployment strategy based on application requirements

**Orchestration: CodePipeline Automation**

- **AWS CodePipeline:** Fully managed continuous delivery service for automating release pipelines
- **Pipeline Stages:** Source, Build, Test, Deploy, and Approval stages
- **Integration:** Connecting CodeCommit, CodeBuild, CodeDeploy, and other AWS services
- **Automation:** Automated triggers, parallel execution, and pipeline visualization

**Demo: Full CI/CD Pipeline Walkthrough**

The demonstration showcased a complete CI/CD pipeline:
- Setting up CodeCommit repository
- Configuring CodeBuild for automated builds and tests
- Creating CodeDeploy application with Blue/Green deployment
- Building CodePipeline to orchestrate the entire workflow
- Testing the pipeline with code changes and observing automated deployment

**10:30 – 10:45 AM | Break**

Networking and refreshments.

**10:45 AM – 12:00 PM | Infrastructure as Code (IaC)**

**AWS CloudFormation: Templates, Stacks, and Drift Detection**

- **CloudFormation Templates:** JSON/YAML templates for defining AWS resources
- **Stacks:** Collections of AWS resources managed as a single unit
- **Drift Detection:** Identifying changes made outside of CloudFormation
- **Stack Updates:** Updating infrastructure with change sets and rollback capabilities
- **Best Practices:** Template organization, parameterization, and nested stacks

**AWS CDK (Cloud Development Kit): Constructs, Reusable Patterns, and Language Support**

- **AWS CDK:** Define cloud infrastructure using familiar programming languages (TypeScript, Python, Java, C#, Go)
- **Constructs:** Reusable cloud components, from low-level resources to high-level patterns
- **Reusable Patterns:** Pre-built solutions for common use cases (VPC, ECS clusters, serverless applications)
- **Language Support:** TypeScript, Python, Java, C#, Go, and JavaScript
- **Benefits:** Type safety, IDE support, and easier testing compared to CloudFormation templates

**Demo: Deploying with CloudFormation and CDK**

The demonstration compared both approaches:
- CloudFormation: Deploying a VPC and EC2 instance using YAML template
- CDK: Same infrastructure using TypeScript with CDK constructs
- Highlighting the differences in approach, maintainability, and developer experience

**Discussion: Choosing between IaC Tools**

- When to use CloudFormation vs CDK
- Considerations: team expertise, project complexity, and maintenance requirements
- Hybrid approaches: Using both tools together for different parts of infrastructure

**Lunch Break (12:00 – 1:00 PM)**

Self-arranged lunch break.

#### Afternoon Session (1:00 – 5:00 PM)

**1:00 – 2:30 PM | Container Services on AWS**

**Docker Fundamentals: Microservices and Containerization**

- **Containerization Concepts:** Understanding containers, images, and containerization benefits
- **Microservices Architecture:** Breaking monolithic applications into smaller, independent services
- **Docker Basics:** Dockerfile, image building, container lifecycle
- **Benefits:** Portability, consistency, and resource efficiency

**Amazon ECR: Image Storage, Scanning, Lifecycle Policies**

- **Amazon ECR:** Fully managed Docker container registry
- **Image Storage:** Secure, scalable storage for Docker images
- **Image Scanning:** Automated vulnerability scanning for container images
- **Lifecycle Policies:** Automating image cleanup and retention policies
- **Integration:** Seamless integration with ECS, EKS, and other AWS services

**Amazon ECS & EKS: Deployment Strategies, Scaling, and Orchestration**

- **Amazon ECS:** Fully managed container orchestration service
  - **Task Definitions:** Container specifications, resource requirements, and networking
  - **Services:** Long-running tasks with load balancing and auto-scaling
  - **Deployment Strategies:** Rolling updates, Blue/Green deployments
  - **Scaling:** Auto-scaling based on CPU, memory, or custom metrics
- **Amazon EKS:** Managed Kubernetes service
  - **Kubernetes Concepts:** Pods, Services, Deployments, and Namespaces
  - **EKS Features:** Managed control plane, node groups, and add-ons
  - **Deployment Strategies:** Rolling updates, Canary deployments with Istio/App Mesh
  - **Scaling:** Cluster autoscaler and horizontal pod autoscaler

**AWS App Runner: Simplified Container Deployment**

- **App Runner:** Fully managed service for building and running containerized applications
- **Simplified Deployment:** Deploy from source code or container image
- **Auto-scaling:** Automatic scaling based on traffic
- **Use Cases:** Web applications, APIs, and microservices
- **Comparison:** When to use App Runner vs ECS vs EKS

**Demo & Case Study: Microservices Deployment Comparison**

The demonstration compared different container deployment options:
- Deploying a simple web application with App Runner
- Same application with ECS Fargate
- Comparison of setup complexity, cost, and operational overhead
- Case study: Choosing the right container service for different scenarios

**2:30 – 2:45 PM | Break**

Networking and refreshments.

**2:45 – 4:00 PM | Monitoring & Observability**

**CloudWatch: Metrics, Logs, Alarms, and Dashboards**

- **CloudWatch Metrics:** Collecting and tracking metrics from AWS services and custom applications
- **CloudWatch Logs:** Centralized logging, log groups, and log streams
- **CloudWatch Alarms:** Automated actions based on metric thresholds
- **CloudWatch Dashboards:** Customizable dashboards for visualizing metrics and logs
- **Best Practices:** Metric naming conventions, log retention, and alarm configuration

**AWS X-Ray: Distributed Tracing and Performance Insights**

- **AWS X-Ray:** Service for analyzing and debugging distributed applications
- **Distributed Tracing:** End-to-end request tracing across microservices
- **Service Map:** Visual representation of application architecture and dependencies
- **Performance Insights:** Identifying bottlenecks and performance issues
- **Integration:** X-Ray SDK integration with applications and AWS services

**Demo: Full-Stack Observability Setup**

The demonstration showed:
- Setting up CloudWatch metrics and logs for an application
- Creating CloudWatch dashboards for monitoring
- Configuring CloudWatch alarms for alerting
- Enabling X-Ray tracing for distributed tracing
- Viewing service maps and trace analysis

**Best Practices: Alerting, Dashboards, and On-Call Processes**

- **Alerting Strategy:** Setting up meaningful alerts, avoiding alert fatigue
- **Dashboard Design:** Creating effective dashboards for different audiences (developers, operations, management)
- **On-Call Processes:** Incident response procedures, escalation paths, and runbooks
- **SLO/SLI:** Service Level Objectives and Indicators for measuring reliability

**4:00 – 4:45 PM | DevOps Best Practices & Case Studies**

**Deployment Strategies: Feature Flags, A/B Testing**

- **Feature Flags:** Gradual feature rollouts, canary releases, and instant rollbacks
- **A/B Testing:** Comparing different versions to optimize user experience
- **Tools:** AWS AppConfig, LaunchDarkly integration
- **Best Practices:** Feature flag management and testing strategies

**Automated Testing and CI/CD Integration**

- **Testing Pyramid:** Unit tests, integration tests, and end-to-end tests
- **Test Automation:** Automated test execution in CI/CD pipelines
- **Quality Gates:** Blocking deployments based on test results
- **Test Coverage:** Measuring and improving test coverage

**Incident Management and Postmortems**

- **Incident Response:** Detection, response, and recovery procedures
- **Postmortems:** Learning from incidents, documenting root causes
- **Blameless Culture:** Focusing on system improvements rather than individual blame
- **Tools:** Incident management tools and communication channels

**Case Studies: Startups and Enterprise DevOps Transformations**

- **Startup Case Study:** Rapid scaling with DevOps practices, cost optimization
- **Enterprise Case Study:** Large-scale migration to DevOps, cultural transformation
- **Lessons Learned:** Common challenges and solutions
- **ROI:** Measuring the impact of DevOps adoption

**4:45 – 5:00 PM | Q&A & Wrap-up**

- **DevOps Career Pathways:** Career progression in DevOps, required skills
- **AWS Certification Roadmap:** Relevant AWS certifications for DevOps engineers
  - AWS Certified DevOps Engineer – Professional
  - AWS Certified Solutions Architect
  - AWS Certified SysOps Administrator
- **Next Steps:** Resources for continued learning and practice
- **Closing Remarks:** Summary of key takeaways and action items

### Key Highlights

- **CI/CD Pipeline:** AWS CodePipeline provides a complete solution for automating software delivery from source to production
- **Infrastructure as Code:** Both CloudFormation and CDK offer powerful ways to manage infrastructure, with CDK providing better developer experience
- **Container Services:** AWS offers multiple container options (ECS, EKS, App Runner) for different use cases and complexity levels
- **Observability:** CloudWatch and X-Ray together provide comprehensive monitoring and tracing capabilities
- **DevOps Culture:** Success requires cultural change, not just tools and technology
- **Best Practices:** Feature flags, automated testing, and incident management are essential for modern DevOps

### Key Learnings

- **DevOps is Culture First:** Tools are important, but cultural transformation is the foundation of DevOps success
- **CI/CD Automation:** Automating the entire software delivery pipeline significantly improves speed and reliability
- **IaC Benefits:** Infrastructure as Code enables version control, repeatability, and faster infrastructure changes
- **Container Strategy:** Choosing the right container service depends on complexity, team expertise, and operational requirements
- **Observability is Critical:** Comprehensive monitoring and tracing are essential for maintaining reliable systems
- **Continuous Improvement:** DevOps is about continuous learning and improvement, not a one-time implementation

### Application to My Work

- **Implement CI/CD:** Set up CodePipeline for automated deployments in current projects
- **Adopt IaC:** Start using CloudFormation or CDK for infrastructure management
- **Container Migration:** Evaluate containerization opportunities for existing applications
- **Improve Monitoring:** Enhance CloudWatch dashboards and alarms for better visibility
- **Practice DevOps:** Apply DevOps principles and practices in daily work
- **Incident Management:** Establish incident response procedures and postmortem practices

### Personal Experience

This full-day DevOps workshop was comprehensive and highly practical:

- The CI/CD pipeline demonstration was particularly valuable, showing how to automate the entire software delivery process
- Learning about different IaC tools helped me understand when to use CloudFormation vs CDK
- The container services comparison provided clear guidance on choosing the right service for different scenarios
- The observability session emphasized the importance of monitoring and tracing for maintaining reliable systems
- The case studies provided real-world insights into DevOps transformations
- The career pathway discussion was motivating and provided clear direction for professional development

### Takeaways

- **Start Small:** Begin with basic CI/CD automation and gradually expand DevOps practices
- **Culture Matters:** DevOps success requires team collaboration and cultural change
- **Choose the Right Tools:** Select tools based on team expertise and project requirements
- **Monitor Everything:** Comprehensive observability is essential for reliable systems
- **Learn Continuously:** DevOps practices evolve rapidly, requiring continuous learning
- **Measure Success:** Use DORA metrics to track DevOps improvements and ROI

### Event Photos

![Event Photo 1](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event4/1.jpg)

![Event Photo 2](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event4/2.jpg)

![Event Photo 3](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event4/3.jpg)

![Event Photo 4](https://aws-fcj-report-a0ff3d.gitlab.io/images/Event4/4.jpg)
