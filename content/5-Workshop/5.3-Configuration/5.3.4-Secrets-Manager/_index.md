---
title: "Store the VirusTotal API Key"
date: 2026-07-22
weight: 4
chapter: false
pre: " <b> 5.3.4. </b> "
---

# Store the API key in AWS Secrets Manager

MalScanAI uses the VirusTotal API for hash lookups. The team does not place the API key in the source code, Dockerfile, or image environment because those locations can be exposed when the code or image is shared.

## 1. Select the secret type

In **AWS Secrets Manager**, choose **Store a new secret** and configure:

- **Secret type:** `Other type of secret`
- **Secret value:** Plaintext or key/value
- **Encryption key:** `aws/secretsmanager`

![Select the secret type](secret-type.png)

The workshop screenshot uses a placeholder. The real API key must not be shown.

## 2. Name the secret

Use:

```text
malscanai/virustotal-api-key
```

![Name the secret](secret-name.png)

The `malscanai/` prefix groups the secret with the project and makes it easier to limit IAM permissions to the exact resource.

## 3. Select the key replacement method

Automatic rotation is not enabled.

![Rotation configuration](secret-rotation.png)

VirusTotal is an external service and does not automatically rotate its API key through Secrets Manager. When a new key is required, the team creates a new secret version and redeploys the ECS task.

## 4. Review and store the secret

Review the name, encryption key, and rotation settings, then choose **Store**.

![Review the secret](secret-review.png)

![Created secret](secret-created.png)

The secret ARN is later used by the IAM policy and Task Definition. Account IDs and unnecessary ARN details should be hidden in public screenshots.

{{% notice warning %}}
If a real API key has appeared in a screenshot, commit, or log, revoke it and create a new key. Redacting the screenshot after exposure is not sufficient.
{{% /notice %}}
