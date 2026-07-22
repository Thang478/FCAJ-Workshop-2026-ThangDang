---
title: "Create the ECS Cluster"
date: 2026-07-22
weight: 9
chapter: false
pre: " <b> 5.3.9. </b> "
---

# Create the ECS cluster for tasks and services

Go to **Amazon ECS → Clusters**, choose **Create cluster**, and configure:

- **Cluster name:** `malscanai-cluster`
- **Infrastructure:** `AWS Fargate (serverless)`
- **Container Insights:** enable when detailed CPU, memory, and task metrics are required

![ECS Cluster configuration](cluster-create.png)

Fargate was selected because the team does not need to create, patch, or manage EC2 container instances. The project can focus on containers, task definitions, and networking instead of server administration.

Choose **Create** and confirm that the cluster appears without any services or tasks.

![Created ECS Cluster](cluster-created.png)

The cluster is a logical ECS management boundary. CPU and memory are provisioned only when the service runs Fargate tasks.
