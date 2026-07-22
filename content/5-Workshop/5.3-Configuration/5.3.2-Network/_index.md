---
title: "Network Configuration"
date: 2026-07-22
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

# Configure the MalScanAI network

The team created a dedicated VPC instead of using the default VPC. The public layer contains the Application Load Balancer and NAT Gateway, while the ECS Fargate task runs in a private subnet.

| Component | Configuration |
|---|---|
| VPC | `malscanai-vpc` – `10.3.0.0/16` |
| Public subnet 1 | `10.3.1.0/24` – `ap-southeast-1a` |
| Public subnet 2 | `10.3.2.0/24` – `ap-southeast-1b` |
| Private subnet 1 | `10.3.3.0/24` – `ap-southeast-1a` |

The two public subnets are placed in different Availability Zones so that the ALB can use a multi-AZ configuration. The ECS task does not receive a public IP. Incoming traffic reaches it through the ALB, while outbound Internet traffic uses the NAT Gateway.

## Configuration order

1. [Create the VPC and enable DNS](5.3.2.1-VPC/)
2. [Create the subnets](5.3.2.2-Subnets/)
3. [Create the Internet Gateway, Elastic IP, and NAT Gateway](5.3.2.3-Internet-Access/)
4. [Configure the public and private route tables](5.3.2.4-Route-Tables/)

{{% notice note %}}
The student deployment uses one private subnet and one NAT Gateway to keep the project within scope. A production deployment should add a private subnet and NAT Gateway in each Availability Zone.
{{% /notice %}}
