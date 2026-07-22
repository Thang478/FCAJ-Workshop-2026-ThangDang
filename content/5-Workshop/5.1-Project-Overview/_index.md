---
title: "Project Overview"
date: 2026-07-22
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# What is MalScanAI?

MalScanAI is an application that helps inspect files and URLs for malicious indicators. The main interface is built with Streamlit, while URL analysis is separated into a Flask API. In our local environment, both services were started with Docker Compose. On AWS, our goal was to keep the same application behavior and replace the local runtime with managed AWS services.

In this workshop, the system is deployed as an **ECS Service on Fargate**. Shared data, models, and the SQLite database are stored on Amazon EFS. Docker images are stored in Amazon ECR. User traffic passes through Route 53, CloudFront, and an Application Load Balancer before reaching the Streamlit container.

The application also calls external services such as VirusTotal, MalwareBazaar, IP geolocation, and webpage screenshot APIs. Because the Fargate task is placed in a private subnet, outbound requests use a NAT Gateway.

#### Deployment goals

- Do not expose the Streamlit container directly to the Internet.
- Allow only the ALB to reach ECS on port `8501`.
- Allow only ECS to reach EFS over NFS port `2049`.
- Read the VirusTotal API key from Secrets Manager instead of baking it into an image.
- Send logs from both containers to CloudWatch.
- Use CloudFront and a custom origin header to reduce direct access to the ALB.

This deployment is intended for a student project and demonstration environment. We focused on a flow that is easy to verify, separates network layers, and limits access between components.
