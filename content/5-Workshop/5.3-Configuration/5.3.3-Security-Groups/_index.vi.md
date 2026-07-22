---
title: "Tạo Security Group"
date: 2026-07-22
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

# Tách Security Group theo từng lớp

Nhóm tạo ba Security Group riêng cho ALB, ECS và EFS. Cách này giúp rule thể hiện rõ luồng kết nối và tránh mở một Security Group quá rộng cho toàn bộ hệ thống.

## 1. Security Group của ALB

Tại **VPC → Security groups**, chọn **Create security group** và cấu hình:

- **Name:** `malscanai-alb-sg`
- **VPC:** `malscanai-vpc`
- **Inbound HTTP 80:** nguồn `0.0.0.0/0`
- **Inbound HTTPS 443:** nguồn `0.0.0.0/0`
- **Outbound:** giữ mặc định

![Security Group của ALB](alb-security-group.png)

ALB là origin public của CloudFront nên cần nhận kết nối từ Internet. Ở bước cuối, nhóm dùng custom header và listener rule để request gọi thẳng ALB bị trả về `403`.

## 2. Security Group của ECS

Tạo Security Group thứ hai:

- **Name:** `malscanai-ecs-sg`
- **Inbound type:** Custom TCP
- **Port:** `8501`
- **Source:** `malscanai-alb-sg`
- **Outbound:** cho phép kết nối đi ra

![Security Group của ECS](ecs-security-group.png)

Nguồn của port `8501` là Security Group ALB, không phải `0.0.0.0/0`. Nhờ vậy, dù private IP của task thay đổi khi ECS triển khai task mới, rule vẫn đúng. Port `5000` không cần mở vì Streamlit gọi URL Engine qua `127.0.0.1` trong cùng task.

## 3. Security Group của EFS

Tạo Security Group thứ ba:

- **Name:** `malscanai-efs-sg`
- **Inbound type:** NFS
- **Port:** `2049`
- **Source:** `malscanai-ecs-sg`

![Security Group của EFS](efs-security-group.png)

EFS chỉ nhận NFS từ ECS task. Nhóm không mở port `2049` cho toàn VPC hoặc Internet vì chỉ container của MalScanAI cần mount file system.
