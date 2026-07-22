---
title: "Create Amazon EFS"
date: 2026-07-22
weight: 6
chapter: false
pre: " <b> 5.3.6. </b> "
---

# Create shared storage for `/app/data`

The Fargate filesystem is temporary and disappears when a task is replaced. MalScanAI stores models, data, and SQLite files under `/app/data`, so the team uses Amazon EFS as shared persistent storage.

## 1. Create the EFS file system

In **Amazon EFS**, choose **Create file system → Customize** and configure:

- **Name:** `malscanai-efs`
- **File system type:** `Regional`
- **Automatic backups:** Enabled
- **Encryption at rest:** Enabled
- **Performance mode:** `General Purpose`
- **Throughput mode:** `Elastic`

![General EFS settings](efs-settings.png)

![Performance and lifecycle settings](efs-performance.png)

Regional storage avoids depending on a single Availability Zone. General Purpose suits normal application file access, while Elastic throughput does not require the team to estimate throughput in advance.

## 2. Configure network access

Under Network access, select:

- **VPC:** `malscanai-vpc`
- **Mount target:** a subnet in the VPC
- **Security Group:** `malscanai-efs-sg`

![EFS network access](efs-network.png)

The EFS security group allows NFS port `2049` only from the ECS security group. Other sources cannot mount the file system.

Review the settings and choose **Create**.

![Review EFS](efs-review.png)

![Created EFS file system](efs-created.png)

## 3. Create an EFS Access Point

In the new file system, open **Access points → Create access point**. Configure a root directory and POSIX user that match the user running inside the container.

![EFS Access Point configuration](access-point-settings.png)

The Access Point ensures that the task mounts the intended directory with consistent POSIX permissions instead of allowing each container to create different ownership settings.

![Created Access Point](access-point-created.png)

Save the **File system ID** and **Access point ID** for the ECS Task Definition. The volume will be mounted at `/app/data`.
