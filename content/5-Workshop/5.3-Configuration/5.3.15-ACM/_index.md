---
title: "Create the ACM Certificate"
date: 2026-07-22
weight: 15
chapter: false
pre: " <b> 5.3.15. </b> "
---

# Create the HTTPS certificate for CloudFront

CloudFront only lists ACM certificates created in **US East (N. Virginia) – `us-east-1`**. The team changes the Region to `us-east-1` before requesting the certificate.

## 1. Request a public certificate

In **AWS Certificate Manager**, choose **Request certificate → Request a public certificate**.

![Start the certificate request](certificate-start.png)

## 2. Enter the domain and validation method

Enter:

```text
malscanai.sadc.io.vn
```

Select:

```text
Validation method: DNS validation
```

![Certificate domain configuration](certificate-domain.png)

DNS validation was selected because Route 53 manages the domain. The validation CNAME can be created automatically, and ACM can renew the certificate while the record remains in place.

## 3. Create the validation CNAME in Route 53

After the request, choose **Create records in Route 53** so that ACM adds the validation CNAME to the Hosted Zone.

![Create the DNS validation record](dns-validation-records.png)

## 4. Wait for certificate issuance

Wait until the status changes from `Pending validation` to `Issued`.

![Issued certificate](certificate-issued.png)

This certificate will be selected as the CloudFront custom SSL certificate.

{{% notice warning %}}
A certificate created in `ap-southeast-1` will not appear in CloudFront. Verify that the current Region is `us-east-1` before requesting it.
{{% /notice %}}
