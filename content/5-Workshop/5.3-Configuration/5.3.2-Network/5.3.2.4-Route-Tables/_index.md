---
title: "Configure the Route Tables"
date: 2026-07-22
weight: 4
chapter: false
pre: " <b> 5.3.2.4. </b> "
---

# Separate public and private traffic with route tables

The team created two route tables. The public route table sends traffic to the Internet Gateway, while the private route table sends outbound traffic to the NAT Gateway.

## 1. Create the Public Route Table

Go to **VPC → Route tables**, choose **Create route table**, and configure:

- **Name:** `malscan-public-rt`
- **VPC:** `malscanai-vpc`

![Create the Public Route Table](public-route-table-create.png)

Open **Subnet associations → Edit subnet associations** and select:

- `malscanai-subnet-public-1`
- `malscanai-subnet-public-2`

![Associate the public subnets](public-subnet-associations.png)

In the **Routes** tab, choose **Edit routes → Add route**:

```text
Destination: 0.0.0.0/0
Target: Internet Gateway – malscanai-igw
```

![Add the default route to the Internet Gateway](public-default-route.png)

![Completed Public Route Table](public-route-table-complete.png)

This route gives both public subnets a direct path to the Internet Gateway, which is required by the public ALB and NAT Gateway.

## 2. Create the Private Route Table

Create a second route table:

- **Name:** `malscan-private-rt`
- **VPC:** `malscanai-vpc`

![Create the Private Route Table](private-route-table-create.png)

Under **Subnet associations**, select only `malscanai-subnet-private-1`.

![Associate the private subnet](private-subnet-association.png)

Add the default route:

```text
Destination: 0.0.0.0/0
Target: NAT Gateway – malscanai-nat-gateway
```

![Add the route to the NAT Gateway](private-default-route.png)

![Completed Private Route Table](private-route-table-complete.png)

The ECS task can now initiate outbound connections from the private subnet, but there is no direct Internet route into the task. User traffic follows CloudFront → ALB → ECS.
