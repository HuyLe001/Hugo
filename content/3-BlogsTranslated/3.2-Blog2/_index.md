---
title: "Making SaaS Products Accessible in AWS Marketplace"
date: "2025-09-11"
weight: 3
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice warning %}}
 **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# MAKING SAAS PRODUCTS ACCESSIBLE IN AWS MARKETPLACE

**Original Article:** [Making SaaS products accessible in AWS Marketplace](https://aws.amazon.com/vi/blogs/awsmarketplace/making-saas-products-accessible-in-aws-marketplace/)

**Original Authors:** Len Gomes and Ricardo Oriol

**Publication Date:** 04 JUN 2025

---

AWS Marketplace sellers offering software-as-a-service (SaaS) solutions frequently seek guidance on understanding the options and best practices for granting buyers access to their software solutions. To address these questions, we explain the three main available access options that can help sellers effectively design and build access mechanisms to their SaaS solutions listed in AWS Marketplace.

When AWS Marketplace sellers list SaaS products in AWS Marketplace, they need to make several key decisions that affect how buyers interact with their solutions. These decisions go beyond pricing and billing integration to include how customers will access their product. This post explores the three main access options for SaaS solutions in AWS Marketplace to help sellers make an informed decision that aligns with their product's architecture and customer needs. Sellers have the flexibility to implement any combination of these access options: They can choose to support one, two, or all three access modes.

---

## USE THE SELLER'S WEBSITE WITH AWS MARKETPLACE SERVERLESS INTEGRATION

When using the seller's website as the main access point for an AWS Marketplace software as a service (SaaS) offering, the integration process can be streamlined with the AWS Marketplace serverless SaaS integration solution. This approach lets the seller keep the existing website infrastructurewhere customers register, sign in, and get supportwhile taking advantage of AWS Marketplace automated deployment capabilities.

The AWS Quick Start deployment sets up core functions including customer registration handling, access management, entitlement updates, and usage metering. The seller maintains full control over their customer experience and user interface. The serverless integration architecture reduces the development work needed for AWS Marketplace integration by handling much of the infrastructure setup through automated workflows. While the seller's website remains the public endpoint for customer interactions, the serverless backend manages the AWS Marketplace connection points, security implementations, and subscription lifecycle events. This approach combines the control of the existing web presence with AWS serverless architecture, helping the seller get to market faster while maintaining direct customer relationships.

---

## WORKSHOP RESOURCES

A workshop is available to help sellers implement Quick Start at Integrate your SaaS with the Serverless SaaS Integration reference. This hands-on workshop guides you through:

- Deploying the serverless integration solution
- Configuring Amazon Simple Notification Service (Amazon SNS) notifications
- Setting up registration URLs
- Testing buyer subscription flow
- Managing entitlements and metering

---

## USE QUICK LAUNCH

Quick Launch changes complex manual configuration into a streamlined, automated experience, changing how sellers make their SaaS products accessible to buyers in AWS Marketplace. Quick Launch uses preconfigured AWS CloudFormation templates validated by both the software provider and AWS to provide secure and standardized deployments while reducing technical complexity for customers. The automation handles tasks such as AWS Identity and Access Management (IAM) role configuration, security group management, and cross-account permissions, which means customers can focus on using the product rather than managing infrastructure.

---

## HOW IT WORKS

To implement Quick Launch successfully, sellers must have a seller account and a separate test buyer account to properly validate the Quick Launch experience. The seller's SaaS product must be listed in AWS Marketplace with Limited or Public visibility status to enable Quick Launch configuration.

---

## IMPLEMENTATION STEPS

To configure Quick Launch the seller must:

1. Open the product in the AWS Marketplace Management Portal and choose the Fulfillment options tab
2. Enable Quick Launch configuration and enter the sign-in or registration URL
3. Create an AWS CloudFormation template following AWS Well-Architected Framework principles
4. Configure AWS CloudFormation template details such as title, description, Amazon Simple Storage Service (Amazon S3) URL for the template, and required IAM permissions to deploy the template. Refer to IAM policies required for the seller account for the full list of policies.
5. (Optional) Add instructions and documentation links for manual configuration
6. Specify the product access URL for post-deployment to launch the product
7. (Optional) Provide a comma-separated list of AWS allowlisted accounts to test with Limited visibility
8. Submit for AWS Marketplace review
9. Update visibility to Public after approval

---

## WORKSHOP RESOURCES

A workshop is available to help sellers implement Quick Launch: Enable SaaS Quick Launch. This hands-on workshop guides sellers through:

- Template creation
- Security configuration
- Testing procedures
- Template development best practices
- Deployment validation

---

## USE AWS PRIVATELINK

AWS sellers can deliver their SaaS through Amazon Virtual Private Cloud (Amazon VPC) using AWS PrivateLink to configure their products as VPC endpoint services. AWS Marketplace supports AWS PrivateLink, a highly available and scalable AWS technology that allows sellers to use the Amazon network to provide buyers access to SaaS products in a provider and consumer model. Through a VPC endpoint, a private connection between the buyer's VPC and the seller's product is created without requiring access over the internet or through a NAT device, a virtual private network (VPN) connection, or AWS Direct Connect. This connection method increases security to buyers because they access the seller's service through the Amazon private network rather than through the internet.

The following diagram is the architecture for the solution using AWS PrivateLink.

![Architecture diagram showing ISV provider account with VPC endpoint service and Network Load Balancer connecting to customer consumer account with VPC endpoint through AWS PrivateLink.](https://d2908q01vomqb2.cloudfront.net/761f22b2c1593d0bb87e0b606f990ba4974706de/2025/05/19/Screenshot-2025-05-19-at-14.40.40.png)

**Figure 1:** Independent software vendor (ISV) Account as provider and Customer Account as consumer

An interface endpoint is the entry point for traffic destined to a PrivateLink powered service such as an AWS Marketplace product. PrivateLink deploys elastic network interfaces in the client VPC with unique IP addresses from the client's subnet. This architectural design provides complete network isolation and eliminates IP overlapping by default. PrivateLink can thus be used to bring a service into a VPC. Security groups can be associated with these endpoint network interfaces to increase security. AWS PrivateLink connects the interface endpoint to a Network Load Balancer used as a front-end in the provider's VPC.

---

## IMPLEMENTATION STEPS FOR SELLERS

To configure a SaaS product to be available through an Amazon VPC endpoint sellers must:

1. Have a SaaS product listing in Limited or Public visibility.

2. Request a certificate from AWS Certificate Manager (ACM) for a user-friendly DNS name.
   - Before ACM issues a certificate, it validates that the seller owns or controls the domain names in the certificate request.
   - AWS recommends that sellers provide a private DNS name that buyers can use when they create their VPC endpoints.

3. Create a Network Load Balancer in the region where the product is deployed. AWS recommends multiple availability zones.

4. Create a VPC endpoint service and associate the Network Load Balancer to the endpoint service.

5. Verify that you can access the service through the Network Load Balancer.

6. Submit your PrivateLink enabled product to the AWS Marketplace Seller Operations team by emailing the following information:
   - The endpoint and the AWS account used to create it. The endpoint looks similar to this: \com.amazonaws.vpce.us-east-1.vpce-svc-0daa010345a21646\
   - The user-friendly DNS name. This is the DNS name that AWS Marketplace buyers use to access the seller's product.
   - The AWS account used to request certificates and the private DNS name that buyers will use to access the VPC endpoint.

7. Delegate the subdomain of the user-friendly DNS name, such as \pi.vpce.example.com\, to the name servers provided by the AWS Marketplace Seller Operations team. In the seller's DNS system, they must create a name server (NS) resource record to point this subdomain to the Amazon Route 53 name servers provided by the AWS Marketplace Seller Operations team so that DNS names (such as \pce-0ac6c347a78c90f8.api.vpce.example.com\) are publicly resolvable.

The AWS Marketplace Seller Operations team verifies the seller's company's identity and the DNS name used for the service being registered (such as \pi.vpce.example.com\). After verification, the DNS name overrides the default base endpoint DNS name.

When AWS Marketplace buyers subscribe to a PrivateLink enabled product and create a VPC endpoint, the service is shown under Your AWS Marketplace Services in AWS Console. The AWS Marketplace Seller Operations team uses the user-friendly DNS name for ease of discovery of the service when creating the VPC endpoint. The endpoints are shown as network interfaces in the subnets. Local IP addresses and Region and zonal DNS names are assigned to the endpoints.

With the launch of native cross-Region connectivity for AWS PrivateLink, service providers can now share and create access through VPC endpoint services across different Regions. This helps service providers offer SaaS solutions privately to a global audience from a single Region. Consumers can use interface endpoints to connect to cross-Region enabled services, the same as they would to services in the same Region. Cross-Region connectivity over PrivateLink is simple, secure, and customizable to fit a variety of use cases. In this Networking & Content Delivery Blog post released in December 2024, Introducing Cross-Region Connectivity for AWS PrivateLink, my colleagues introduce cross-Region connectivity for AWS PrivateLink, including steps to set it up.

---

## CONCLUSION

AWS Marketplace offers SaaS sellers three primary flexible options for granting buyers access to their solutions: Whether choosing the flexibility of a seller's website, the streamlined automation of Quick Launch, or the enhanced security of AWS PrivateLink, sellers can strategically design their product access mechanism to optimize customer experience and marketplace integration. By carefully evaluating their product's technical requirements, security considerations, and growth objectives, SaaS providers can take advantage of multiple access options concurrently or start with a single method to effectively expand their reach, streamline customer onboarding, and create seamless software delivery experiences within AWS Marketplace.

For more information, refer to the AWS Marketplace Seller Guide documentation.

---

## ABOUT THE AUTHORS

![Len Gomes](https://d2908q01vomqb2.cloudfront.net/761f22b2c1593d0bb87e0b606f990ba4974706de/2024/12/17/Len.jpg)

**Len Gomes** is a Partner Solutions Architect working with top software companies (ISV's) that partner with AWS across EMEA. He helps partners architect, optimize, and deliver cloud-based solutions that drive business value for customers while ensuring technical excellence and AWS best practices. Len has a passion for networking, hybrid and edge services and solutions. In his free time, he enjoys playing and watching football, outdoor activities, and barbecuing. He is skilled at grilling and considers himself a barbecue pit-master.

![Ricardo Oriol](https://d2908q01vomqb2.cloudfront.net/761f22b2c1593d0bb87e0b606f990ba4974706de/2025/05/27/roriol.jpg)

**Ricardo Oriol** is a Partner Solutions Architect at AWS, where he works with Partners across EMEA to deliver impactful, scalable solutions for Customers. In his role, Ricardo helps Partners discover and develop innovative cloud capabilities that drive business transformation. With a passion for cloud architecture and enabling growth through AWS, Ricardo is dedicated to empowering Customers through Partners at scale. Outside of work, he enjoys exploring emerging technologies, reading, and staying active through outdoor sports.
