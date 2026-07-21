---
title: "Blog 3"
date: 2024-07-08
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# UNDERSTANDING AND IMPLEMENTING IAM ROLES INSTEAD OF ACCESS KEYS ON EC2

Configuring Access Keys and Secret Access Keys (Long-term Credentials) directly on EC2 instances is common in educational labs for the sake of convenience. However, according to AWS security best practices, the safest and most optimal solution for production environments is using IAM Roles (Instance Profiles) to grant permissions automatically and much more securely.

Key points to know:

*Eliminating Long-term Credentials: Instead of storing static credentials on the server (via the `aws configure` command), attaching an IAM Role to an EC2 instance allows applications to retrieve temporary credentials, drastically minimizing the risk of key or source code leaks.
*AWS STS (Security Token Service): Acts as the engine that automatically issues Temporary Credentials (including an Access Key ID, Secret Access Key, and Session Token). Because they have a short Time-To-Live (TTL) and expire automatically, the blast radius is significantly reduced if the credentials are ever compromised.
*Instance Metadata Service v2 (IMDSv2): This is the communication channel for the AWS SDK and applications on EC2 to retrieve Temporary Credentials. AWS automatically manages and rotates these credentials without any developer intervention.
*Protection against SSRF Attacks: IMDSv2 provides a robust defense layer against Server-Side Request Forgery vulnerabilities through a mandatory two-step authentication mechanism: sending an HTTP PUT request to retrieve a Session Token, and then using an HTTP GET with the Token in the Header to call the metadata API.
* Complete Automation: When using an IAM Role, tools like the AWS SDK and AWS CLI automatically detect and utilize the temporary credentials, ensuring a smooth and highly secure application development workflow.

### Architecture Diagram

![IAM Role and IMDSv2 Workflow Diagram](blog3.png)

### References
* AWS Security Blog: [Practical steps to minimize key exposure using AWS Security Services](https://aws.amazon.com/blogs/security/practical-steps-to-minimize-key-exposure-using-aws-security-services/)
* AWS Security Blog: [Defense in depth against open firewalls, reverse proxies, and SSRF vulnerabilities with enhancements to the EC2 Instance Metadata Service](https://aws.amazon.com/blogs/security/defense-in-depth-open-firewalls-reverse-proxies-ssrf-vulnerabilities-ec2-instance-metadata-service/)
* AWS IAM User Guide: [Temporary security credentials in IAM (AWS STS)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html)
* AWS IAM User Guide: [Use temporary credentials with AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_use-resources.html)