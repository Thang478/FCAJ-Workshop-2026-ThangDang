---
title: "Security and system limitations"
date: 2026-07-24
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

# Security-layer summary

Security controls were configured throughout the deployment process. This chapter summarizes the final state and records limitations that must be presented accurately.

## 1. Implemented controls

| Layer | Actual configuration |
|---|---|
| DNS and TLS | Route 53 maps the domain to CloudFront; users connect through HTTPS |
| Edge | The CloudFront Free Plan is placed in front of the ALB |
| AWS WAF | Core protections and rate limiting are enabled in Monitor mode |
| Origin protection | CloudFront sends a custom origin header; the ALB default action returns `403` |
| ECS networking | The task runs in a private subnet without a public IP |
| Security group | Port 8501 accepts traffic only from the ALB security group |
| URL Engine | Port 5000 is not public; Streamlit calls it through `127.0.0.1` |
| EFS | NFS port 2049 accepts traffic only from the ECS security group |
| Secrets | The VirusTotal API key is stored in Secrets Manager instead of the image |
| IAM | The ECS task execution role is separated from the task role |
| Logging | Both containers send stdout and stderr to `/ecs/malscanai` |

## 2. WAF Monitor mode

CloudFront Security shows Core protections and Rate limiting enabled in **Monitor mode**. This mode records requests and security trends but does not block requests under the monitored rules.

![WAF operating in Monitor mode](waf-monitor-mode.png)

The team selected Monitor mode because a managed rule had blocked a legitimate Streamlit upload request. This preserves upload functionality for the workshop but is not the strongest production configuration.

## 3. Validate ALB protection

Direct ALB access returns `403`, while the HTTPS CloudFront domain remains available. This demonstrates that the custom-header rule and default fixed response operate as intended.

![Direct ALB access blocked](direct-alb-403.png)

## 4. Current limitations

### One ECS task and SQLite

The system keeps `desired count = 1` because the SQLite database is stored on EFS. Multiple tasks writing to one SQLite file can cause locking contention. Therefore, the current version does not enable ECS Service Auto Scaling or horizontal scale-out.

### WAF is not blocking in production mode

Monitor mode observes traffic only. Before production use, WAF logs should be reviewed, a precise exception should be created for the upload endpoint, and suitable rules should be moved to Block mode.

### The URL Engine uses the Flask development server

CloudWatch logs show that the URL Engine uses the Flask development server and produces a library-version warning while loading the model. A future version should use Gunicorn or another production WSGI server and align the training and inference library versions.

### High availability is incomplete

The ALB and CloudFront protect the access layer, but the application has one task and one SQLite database. ECS can replace a failed task, but a brief interruption can occur during replacement.

## 5. Improvement roadmap

- Move SQLite to Amazon RDS or DynamoDB before increasing the task count.
- Run at least two tasks across Availability Zones after the data layer supports scale-out.
- Create a precise WAF exception for Streamlit uploads instead of leaving all relevant rules in Monitor mode.
- Use a production WSGI server and eliminate model-version warnings.
- Add periodic backup for EFS data.
- Review IAM policies regularly and reduce permissions according to the principle of least privilege.

