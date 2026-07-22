---
title: "Configure Route 53"
date: 2026-07-22
weight: 14
chapter: false
pre: " <b> 5.3.14. </b> "
---

# Manage project DNS with Route 53

The team uses the root domain `sadc.io.vn` and reserves `malscanai.sadc.io.vn` for the application.

## 1. Create a Public Hosted Zone

Go to **Route 53 → Hosted zones**, choose **Create hosted zone**, and configure:

- **Domain name:** `sadc.io.vn`
- **Type:** `Public hosted zone`

![Create the Public Hosted Zone](hosted-zone-create.png)

A Public Hosted Zone is used because the domain must resolve from the Internet. A Private Hosted Zone would only resolve inside a VPC.

## 2. Update the nameservers

Route 53 creates NS and SOA records after the hosted zone is created.

![Created Hosted Zone](hosted-zone-created.png)

If the domain is registered with another provider, copy the four nameservers from the NS record and update them at that provider. DNS delegation can take time to propagate.

The Alias record for `malscanai.sadc.io.vn` is not created yet. It will be added after the CloudFront Distribution exists so that the correct target is available.
