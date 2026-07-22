---
title: "Environment Preparation"
date: 2026-07-22
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

# Prepare the environment

Before creating AWS resources, the team verified the selected Region, the AWS account used by the CLI, and the two application images. These checks reduce the risk of deploying resources to the wrong Region or pushing images to the wrong account.

## 1. Select the deployment Region

From the AWS Console navigation bar, select:

```text
Asia Pacific (Singapore) – ap-southeast-1
```

![Select the Singapore Region](select-region.png)

Singapore was selected because it is close to Vietnam. The main MalScanAI resources are kept in the same Region for simpler management. The CloudFront certificate is the exception and will be requested in `us-east-1`.

## 2. Verify the AWS CLI identity

Run the following command on the local computer:

```powershell
aws sts get-caller-identity
```

The output confirms that the CLI is using the intended AWS account. Account IDs, user IDs, and ARNs should be hidden before screenshots are published.

## 3. Verify the Docker images

The source code was tested with Docker Compose before deployment. Check the local images with:

```powershell
docker compose images
```

![Local Docker images](docker-images.png)

The deployment uses two images:

- `malscanai-streamlit`: the Streamlit interface on port `8501`.
- `malscanai-url-engine`: the Flask URL-analysis API on port `5000`.

If the application does not run correctly on the local computer, the team fixes it before pushing the images to ECR. This keeps application errors separate from AWS infrastructure errors.
