---
title: "System Configuration"
date: 2026-07-22
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

# MalScanAI configuration order

The team configures the system from the network layer to the application layer. Each section records the values used, the AWS Console actions, and the reason for the selected configuration. Screenshots at the end of each step confirm that a resource was created or saved; they are not a separate results chapter.

1. [Prepare the environment](5.3.1-Preparation/)
2. [Configure the network](5.3.2-Network/)
3. [Create the security groups](5.3.3-Security-Groups/)
4. [Store the VirusTotal API key](5.3.4-Secrets-Manager/)
5. [Create the IAM roles](5.3.5-IAM-Roles/)
6. [Create Amazon EFS](5.3.6-EFS/)
7. [Create the CloudWatch Log Group](5.3.7-CloudWatch/)
8. [Create ECR repositories and push images](5.3.8-ECR/)
9. [Create the ECS Cluster](5.3.9-ECS-Cluster/)
10. [Create the ECS Task Definition](5.3.10-Task-Definition/)
11. [Create the Target Group](5.3.11-Target-Group/)
12. [Create the Application Load Balancer](5.3.12-ALB/)
13. [Create the ECS Service](5.3.13-ECS-Service/)
14. [Configure Route 53](5.3.14-Route53/)
15. [Create the ACM certificate](5.3.15-ACM/)
16. [Create the CloudFront Distribution](5.3.16-CloudFront/)
17. [Restrict direct ALB access](5.3.17-Protect-ALB/)

{{% notice warning %}}
NAT Gateway, EFS, ALB, Fargate, CloudFront, and WAF can generate charges. Check Billing and delete resources that are no longer needed after the demonstration.
{{% /notice %}}
