---
title: "Create the Application Load Balancer"
date: 2026-07-22
weight: 12
chapter: false
pre: " <b> 5.3.12. </b> "
---

# Create the Application Load Balancer for Streamlit

The ALB accepts requests from CloudFront and forwards valid traffic to the Streamlit container on port `8501`.

## 1. Configure the basic settings

Go to **EC2 → Load Balancers**, choose **Create load balancer → Application Load Balancer**, and configure:

- **Name:** `malscanai-alb`
- **Scheme:** `Internet-facing`
- **IP address type:** `IPv4`

![ALB basic settings](alb-basic-settings.png)

The ALB is Internet-facing because CloudFront uses its DNS name as a custom origin.

## 2. Select the VPC and public subnets

Under Network mapping, select:

- **VPC:** `malscanai-vpc`
- **Availability Zones:** `ap-southeast-1a` and `ap-southeast-1b`
- **Subnets:** the two public subnets

![ALB network mapping](alb-network.png)

Subnets in different Availability Zones give the ALB a multi-AZ setup instead of depending on one zone.

## 3. Select the security group and listener

Select:

```text
malscanai-alb-sg
```

![Select the ALB security group](alb-security-group-select.png)

Create the listener:

- **Protocol:** HTTP
- **Port:** `80`
- **Default action:** Forward to `malscanai-streamlit-tg`

![ALB listener configuration](alb-listener.png)

Users connect to CloudFront through HTTPS. In the current setup, CloudFront connects to the ALB through HTTP. URL Engine port `5000` is not added to the listener.

## 4. Review and create the ALB

Review the subnets, security group, listener, and Target Group, then choose **Create load balancer**.

![Review the ALB](alb-review.png)

Wait until the state becomes `Active`.

![Created ALB](alb-created.png)

## 5. Check ALB attributes

Open the **Attributes** tab and review the idle timeout and connection settings.

![ALB attributes](alb-attributes.png)

Streamlit uses long-lived connections and WebSocket. If the interface disconnects during processing, the idle timeout is one of the first settings the team checks.
