---
title: "Cost estimation and optimization"
date: 2026-07-24
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Monthly operating-cost estimate

The team uses AWS Pricing Calculator to estimate the cost of running MalScanAI continuously for one month in **Asia Pacific (Singapore)**. The estimate excludes taxes, account-specific credits, Free Tier benefits, and changes in actual traffic.

![MalScanAI AWS Pricing Calculator estimate](cost-estimate-final.png)

## 1. Calculation assumptions

| Component | Assumption |
|---|---|
| Runtime | 730 hours/month |
| ECS Fargate | 1 task, Linux x86, 2 vCPU, 4 GB RAM, 21 GB ephemeral storage |
| Application Load Balancer | 1 ALB |
| Amazon VPC | 1 NAT Gateway, 10 GB processed/month, 3 public IPv4 addresses |
| Amazon EFS | Regional Standard, 10 GB stored, 10 GB read and 2 GB written/month |
| Amazon ECR | 10 GB of images/month |
| CloudWatch | Application logs, metrics, and one alarm |
| Secrets Manager | 1 secret for 30 days |
| CloudFront | One Free Flat-Rate Plan |

## 2. Estimate result

| Service | Displayed monthly cost |
|---|---:|
| AWS Fargate | USD 90.07 |
| Amazon VPC | USD 54.61 |
| Elastic Load Balancing | USD 18.63 |
| Amazon EFS | USD 4.14 |
| Amazon ECR | USD 1.00 |
| Amazon CloudWatch | USD 0.71 |
| AWS Secrets Manager | USD 0.41 |
| Amazon CloudFront | USD 0.00 |
| **Calculator total** | **USD 169.56/month** |
| **12-month estimate** | **USD 2,034.72** |

The service rows are rounded by the Calculator interface, so manually adding the displayed rows can differ by a few cents from the system total.

## 3. Cost observation

Fargate, VPC, and the ALB account for approximately 96% of the estimate. These resources continue to incur time-based charges even when the website receives little traffic. The current architecture prioritizes network isolation, HTTPS, health checks, and stable operations over the lowest possible cost for a demonstration site.

## 4. Optimizations already applied

- Run one ECS task because the current application uses SQLite on EFS.
- Use the CloudFront Free Flat-Rate Plan for the workshop distribution.
- Keep a short CloudWatch Logs retention period; seven days is proposed for the demo environment.
- Store only one required secret in Secrets Manager.
- Do not add a separate pay-as-you-go WAF estimate because WAF is included in the CloudFront plan.
- Keep ECR storage small and retain only images required for rollback.

## 5. Further optimization opportunities

- Right-size Fargate CPU and memory after load testing, followed by full regression testing.
- Create an ECR lifecycle policy that retains only a limited number of recent versions.
- Delete the NAT Gateway, ALB, and ECS service immediately after the demo environment is no longer needed.
- Review Billing and Cost Explorer for resources running outside the planned period.
- For a scheduled environment, reduce the ECS desired count to `0` outside the required window; the website will be unavailable while the task is stopped.
- In a future design, evaluate an architecture that does not depend on a NAT Gateway or that better matches low, event-driven traffic.

{{% notice warning %}}
AWS Pricing Calculator provides an estimate only. Actual charges depend on requests, uploaded file size, NAT Gateway traffic, logs, taxes, and the pricing policy at the time of use.
{{% /notice %}}

