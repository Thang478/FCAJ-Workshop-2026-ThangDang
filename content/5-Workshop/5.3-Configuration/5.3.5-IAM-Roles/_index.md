---
title: "Create IAM Roles for ECS"
date: 2026-07-22
weight: 5
chapter: false
pre: " <b> 5.3.5. </b> "
---

# Separate the Execution Role and Task Role

The team created two IAM roles. The ECS agent uses the Execution Role when starting a task, while the application code inside the containers uses the Task Role.

## 1. Create the ECS Task Execution Role

Go to **IAM → Roles** and choose **Create role**:

- **Trusted entity type:** `AWS service`
- **Service or use case:** `Elastic Container Service`
- **Use case:** `Elastic Container Service Task`

![Select the trusted entity](execution-role-trusted-entity.png)

Attach the managed policy:

```text
AmazonECSTaskExecutionRolePolicy
```

Name the role:

```text
malscanai-ecs-task-execution-role
```

The managed policy allows ECS to pull images from ECR and send container logs to CloudWatch.

## 2. Allow the Execution Role to read the VirusTotal secret

In the new role, choose **Add permissions → Create inline policy** and add:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "secretsmanager:GetSecretValue",
      "Resource": "arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:malscanai/virustotal-api-key-*"
    }
  ]
}
```

![Inline policy for the secret](secret-policy-redacted.png)

The `Resource` is limited to the required secret instead of `*`. ECS needs this permission because the secret is injected when the task starts.

![Created Execution Role](execution-role-created.png)

## 3. Create the ECS Task Role

Create a second role with the same ECS Task trusted entity and name it:

```text
malscanai-ecs-task-role
```

![Created Task Role](task-role-created.png)

The current application does not call additional AWS APIs through an SDK, so the Task Role does not require broad permissions. If S3 or another AWS service is added later, application permissions will be attached to this role instead of the Execution Role.

![Verify attached permissions](secret-policy-attached.png)

Separating the roles makes the permission model easier to review and prevents the application from using permissions that belong to the ECS agent.
