---
title: "Workshop"
date: 2026-07-22
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploying MalScanAI on AWS with ECS Fargate

#### What this workshop covers

MalScanAI first ran locally with Docker Compose. When we moved it to AWS, we kept the same two-container layout: a **Streamlit** container for the web interface and a **URL Engine** container for URL analysis. Both containers run inside one ECS Fargate task and communicate through `127.0.0.1`.

This workshop follows the configuration that our team completed in the AWS Console. It is organized into three parts:

1. [Project overview](5.1-Project-Overview/)
2. [Deployment architecture](5.2-Architecture/)
3. [Configuration steps](5.3-Configuration/)

There is no separate results chapter. At the end of each configuration step, the final screenshot shows that the resource was created or reached a state such as `Available`, `Active`, `Running`, `Healthy`, `Issued`, or `Deployed`.

{{% notice note %}}
Domain names, resource IDs, and several values in the screenshots belong to our lab environment. Use your own resource names and never copy secret values from screenshots.
{{% /notice %}}
