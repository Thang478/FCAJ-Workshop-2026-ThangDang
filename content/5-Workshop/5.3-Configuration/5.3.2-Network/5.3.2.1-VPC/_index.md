---
title: "Create the VPC and Enable DNS"
date: 2026-07-22
weight: 1
chapter: false
pre: " <b> 5.3.2.1. </b> "
---

# Create a dedicated VPC

## 1. Define the VPC

Go to **VPC → Your VPCs**, choose **Create VPC**, and select **VPC only**. Configure:

- **Name tag:** `malscanai-vpc`
- **IPv4 CIDR:** `10.3.0.0/16`
- **IPv6 CIDR:** not used
- **Tenancy:** `Default`

![VPC configuration](vpc-settings.png)

The `/16` range leaves enough address space for several `/24` subnets without redesigning the VPC later. The team used the private range `10.3.0.0/16`, which did not overlap with the lab network.

Review the values and choose **Create VPC**.

![Created VPC](vpc-created.png)

## 2. Enable VPC DNS

From the VPC details page, choose **Actions → Edit VPC settings** and enable:

- **Enable DNS resolution**
- **Enable DNS hostnames**

![Enable DNS resolution and hostnames](dns-settings.png)

Choose **Save changes** and confirm that both settings are enabled.

![DNS settings enabled](dns-enabled.png)

DNS was enabled at the beginning because the ALB, ECS, ECR, and AWS endpoints are accessed through domain names. Without DNS, a task may start but fail to resolve service endpoints later.
