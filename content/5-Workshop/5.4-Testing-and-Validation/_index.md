---
title: "Testing and validation"
date: 2026-07-24
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# End-to-end validation after deployment

After the ECS service completed its deployment, the team validated both the Internet-facing access path and the health of the components behind the load balancer. Functional testing is demonstrated in the video, so this chapter focuses on technical evidence from AWS.

## 1. Access the application through HTTPS

Users access the application at `https://malscanai.sadc.io.vn`. The browser confirms a secure HTTPS connection and loads the Streamlit interface successfully.

![MalScanAI available through HTTPS](domain-https.png)

## 2. Validate the ECS service

The ECS service is `Active`, with one desired task, one running task, no pending task, and a successful current deployment.

![Running ECS service](ecs-service-running.png)

## 3. Validate the target group

The target group uses target type `IP`, HTTP, and port `8501`. At validation time, the target is `Healthy` and no target is `Unhealthy`.

![Healthy target group](target-group-healthy.png)

## 4. Validate direct-ALB protection

Opening the Application Load Balancer DNS name directly over HTTP returns `Access denied`. This confirms that only requests carrying the CloudFront origin header match the forwarding rule. Direct requests reach the default action and receive a `403` response.

![Direct ALB access denied](direct-alb-403.png)

## 5. Test-result summary

| Test | Expected result | Actual result |
|---|---|---|
| HTTPS domain | The MalScanAI interface loads | Passed |
| ECS service | `1 Running`, `0 Pending`, successful deployment | Passed |
| Target group | `1 Healthy`, `0 Unhealthy` | Passed |
| Direct ALB access | Rejected with a `403` response | Passed |
| Scanning functions | URL, PE, and document scans return results | Demonstrated in the video |
| Application logs | Both containers send logs to CloudWatch | Passed; see chapter 5.6 |

{{% notice note %}}
Only safe sample files and URLs are used during validation. API keys, passwords, custom-header values, and personal data must not appear in workshop screenshots.
{{% /notice %}}

