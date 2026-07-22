---
title: "Create the Subnets"
date: 2026-07-22
weight: 2
chapter: false
pre: " <b> 5.3.2.2. </b> "
---

# Divide the VPC into public and private subnets

Go to **VPC → Subnets**, choose **Create subnet**, and select `malscanai-vpc`. The team created three subnets in the same configuration process.

## 1. Create Public Subnet 1

Configure:

- **Subnet name:** `malscanai-subnet-public-1`
- **Availability Zone:** `ap-southeast-1a`
- **IPv4 VPC CIDR block:** `10.3.0.0/16`
- **IPv4 subnet CIDR block:** `10.3.1.0/24`

![Public Subnet 1 configuration](public-subnet-1.png)

This subnet is used by the ALB and can host the NAT Gateway. The `10.3.1.0/24` range was reserved for the first public layer.

## 2. Create Public Subnet 2

Choose **Add new subnet** and configure:

- **Subnet name:** `malscanai-subnet-public-2`
- **Availability Zone:** `ap-southeast-1b`
- **IPv4 VPC CIDR block:** `10.3.0.0/16`
- **IPv4 subnet CIDR block:** `10.3.2.0/24`

![Public Subnet 2 configuration](public-subnet-2.png)

Public Subnet 2 is in a different Availability Zone from Public Subnet 1. An ALB requires subnets in at least two Availability Zones, so both public subnets were not placed in the same zone.

## 3. Create Private Subnet 1

Choose **Add new subnet** again and configure:

- **Subnet name:** `malscanai-subnet-private-1`
- **Availability Zone:** `ap-southeast-1a`
- **IPv4 VPC CIDR block:** `10.3.0.0/16`
- **IPv4 subnet CIDR block:** `10.3.3.0/24`

![Private Subnet 1 configuration](private-subnet-1.png)

The ECS Fargate task runs in this subnet so that it cannot be reached directly from the Internet. Application traffic is accepted only from the ALB security group.

After checking that the CIDR ranges do not overlap, choose **Create subnet**.

![Created subnets](subnets-created.png)

## 4. Enable automatic public IPv4 assignment

Select `malscanai-subnet-public-1`, choose **Actions → Edit subnet settings**, enable **Enable auto-assign public IPv4 address**, and save the change.

![Enable public IPv4 for Public Subnet 1](public-ip-subnet-1.png)

Repeat the same step for `malscanai-subnet-public-2`.

![Enable public IPv4 for Public Subnet 2](public-ip-subnet-2.png)

Do not enable this setting for the private subnet. A subnet does not become public because of its name. It becomes public after its route table contains a `0.0.0.0/0` route to an Internet Gateway.
