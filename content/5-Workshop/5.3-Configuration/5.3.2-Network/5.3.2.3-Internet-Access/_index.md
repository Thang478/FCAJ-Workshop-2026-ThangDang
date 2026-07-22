---
title: "Create Internet Connectivity"
date: 2026-07-22
weight: 3
chapter: false
pre: " <b> 5.3.2.3. </b> "
---

# Provide Internet access for both network layers

The public subnets use an Internet Gateway. The private subnet does not route directly to the Internet Gateway; the team uses a NAT Gateway so that the ECS task can only initiate outbound connections.

## 1. Create the Internet Gateway

Go to **VPC → Internet gateways**, choose **Create internet gateway**, and enter:

```text
Name tag: malscanai-igw
```

![Create the Internet Gateway](internet-gateway-create.png)

After creation, choose **Actions → Attach to a VPC**, select `malscanai-vpc`, and confirm.

![Select the VPC](internet-gateway-attach.png)

![Internet Gateway attached to the VPC](internet-gateway-attached.png)

The Internet Gateway only provides a gateway for the VPC. A public subnet still needs a route table entry that points to this gateway.

## 2. Allocate an Elastic IP

Go to **Elastic IP addresses**, choose **Allocate Elastic IP address**, and keep the default network border group for the Singapore Region.

![Allocate an Elastic IP](elastic-ip.png)

The Elastic IP is assigned to the NAT Gateway so that its public address remains stable while the gateway exists.

## 3. Create the NAT Gateway

Go to **NAT gateways**, choose **Create NAT gateway**, and configure:

- **Name:** `malscanai-nat-gateway`
- **Subnet:** one public subnet; the team used Public Subnet 1
- **Connectivity type:** `Public`
- **Elastic IP allocation ID:** the allocated Elastic IP

![NAT Gateway configuration](nat-gateway-create.png)

Choose **Create NAT gateway** and wait until its state becomes `Available`.

![Available NAT Gateway](nat-gateway-created.png)

The ECS task needs outbound connectivity to pull images, send logs, and call VirusTotal, MalwareBazaar, ipinfo.io, or microlink.io when VPC endpoints do not cover every service. The NAT Gateway does not allow the Internet to initiate a connection to the private task.

{{% notice warning %}}
A NAT Gateway is charged by running time and processed data. The team deletes it and releases the Elastic IP after the demonstration when it is no longer required.
{{% /notice %}}
