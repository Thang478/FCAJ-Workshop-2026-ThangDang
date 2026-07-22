---
title: "Create the ECS Task Definition"
date: 2026-07-22
weight: 10
chapter: false
pre: " <b> 5.3.10. </b> "
---

# Define both containers in one ECS task

The Task Definition describes how ECS runs Streamlit and the URL Engine, including images, ports, CPU, memory, secrets, logs, and the EFS volume.

## 1. Configure task infrastructure

Go to **Amazon ECS → Task definitions**, choose **Create new task definition**, and configure:

- **Task definition family:** `malscanai-task`
- **Launch type:** `AWS Fargate`
- **Operating system/Architecture:** `Linux/X86_64`
- **Network mode:** `awsvpc`
- **CPU:** `2 vCPU`
- **Memory:** `4 GB`
- **Task role:** `malscanai-ecs-task-role`
- **Task execution role:** `malscanai-ecs-task-execution-role`

![Task infrastructure configuration](task-infrastructure.png)

`awsvpc` is required for Fargate. Each task receives an ENI and a private IP in the subnet selected by the ECS Service.

## 2. Add the Streamlit container

Configure the interface container:

- **Name:** `malscanai-streamlit`
- **Image URI:** ECR image tagged `v1`
- **Essential container:** Yes
- **Container port:** `8501`
- **Protocol:** TCP
- **App protocol:** HTTP
- **Memory hard limit:** `3 GB`
- **Memory soft limit:** `1 GB`

![Streamlit container configuration](streamlit-container.png)

Port `8501` is declared because the ALB forwards application traffic to Streamlit. More memory is assigned to this container because it also processes files and reads models.

## 3. Configure Streamlit environment variables, secret, and logs

Add:

```text
FLASK_API_URL=http://127.0.0.1:5000/api/analyze
PYTHONUNBUFFERED=1
VT_API_KEY=ValueFrom Secrets Manager
```

Configure logs:

```text
awslogs-group=/ecs/malscanai
awslogs-region=ap-southeast-1
awslogs-stream-prefix=streamlit
```

![Streamlit environment, secret, and logs](streamlit-environment-logging.png)

`VT_API_KEY` uses ValueFrom, so the real value is not stored in the Task Definition. `PYTHONUNBUFFERED=1` sends Python output to CloudWatch without buffering.

## 4. Add the URL Engine container

Configure the backend container:

- **Name:** `malscanai-url-engine`
- **Image URI:** ECR image tagged `v1`
- **Essential container:** Yes
- **Container port:** `5000`
- **CPU reservation:** about `1 vCPU`
- **Memory hard/soft limit:** about `1 GB`
- **Environment:** `PYTHONUNBUFFERED=1`

![URL Engine container configuration](url-engine-container.png)

Both containers run in the same task, so Streamlit calls the Flask API through `127.0.0.1:5000`. Port `5000` is not exposed through the ALB or to the Internet.

## 5. Define the EFS volume

Under **Volumes**, add the EFS volume and select:

- The created file system
- The created Access Point
- Transit encryption: Enabled
- Container mount path: `/app/data`

![EFS volume configuration](efs-volume.png)

EFS keeps models, data, and SQLite files when ECS replaces a task. Only `/app/data` is mounted so that the volume does not overwrite application code from the image.

## 6. Create the Task Definition

Review the image URIs, roles, ports, secret, logs, and volume, then choose **Create**.

![Created Task Definition](task-definition-created.png)

When an image or container setting changes, the team creates a new revision instead of modifying an old revision.
