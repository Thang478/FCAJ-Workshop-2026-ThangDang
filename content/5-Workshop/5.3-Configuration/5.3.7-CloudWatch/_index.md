---
title: "Create the CloudWatch Log Group"
date: 2026-07-22
weight: 7
chapter: false
pre: " <b> 5.3.7. </b> "
---

# Create a log destination for both containers

The team creates the Log Group before the Task Definition so that the same group name is used consistently by Streamlit and the URL Engine.

## 1. Create the Log Group

Go to **CloudWatch → Logs → Log groups**, choose **Create log group**, and enter:

```text
/ecs/malscanai
```

![Create the CloudWatch Log Group](log-group-create.png)

The `/ecs/malscanai` name identifies ECS logs and groups both project containers together. Each container still receives a separate log stream through its stream prefix.

Choose **Create** and confirm that the group appears in the list.

![Created Log Group](log-group-created.png)

## 2. Check Log Streams after ECS starts

When the ECS Service creates a task, Streamlit and the URL Engine send stdout and stderr through the `awslogs` driver.

![Application Log Streams](log-streams.png)

The logs are used to troubleshoot container startup, EFS mounting, health checks, and external API calls. API keys, custom header values, and user file contents must not be written to logs.

{{% notice note %}}
For a student environment, a retention period of 7 to 30 days is usually enough and avoids retaining logs indefinitely.
{{% /notice %}}
