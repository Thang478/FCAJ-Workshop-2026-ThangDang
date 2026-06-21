---
title: "Week 7 Work Log"
date: 2026-06-21
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:
* Implement robust User Authentication using Amazon Cognito (User Pools & Identity Pools).
* Master Serverless Observability by monitoring applications with Amazon CloudWatch and analyzing performance/bottlenecks with AWS X-Ray.
* Standardize internal IAM security policies for the MLOps Docker environment.
* Finalize the System Architecture Diagram for the SOC Malware platform.

### Tasks Completed During the Week:
| Day | Tasks | Start Date | Completion Date | References |
| --- | --- | --- | --- | --- |
| 2 | - Studied Identity Management theory: Analyzed JWT Token workflows, User Pool/Identity Pool configurations, and OAuth 2.0 integration. | 15/06/2026 | 15/06/2026 | AWS Documentation |
| 3 | - Practice Lab: *User Authentication with Amazon Cognito*.<br>- Provisioned User Pools, enforced strict password policies, and mapped API credentials (`ClientID`, `ClientSecret`). | 16/06/2026 | 16/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Practice Lab: *Serverless Observability (CloudWatch & X-Ray)*.<br>- Configured Lambda logging, created Custom Metrics, and set up SNS-integrated CloudWatch Alarms for error tracking. | 17/06/2026 | 17/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Practice Lab: *AWS X-Ray*.<br>- Instrumented Lambda functions with `aws_xray_sdk`, mapped service dependencies, and analyzed execution latency bottlenecks. | 18/06/2026 | 18/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 6 | - Group Project: Hardened IAM configurations. Refined least-privilege policies for Docker containers and service-to-service communication. | 19/06/2026 | 20/06/2026 | Group Project |
| 7 | - Group Project: Architecture Modeling. Iteratively refined the System Architecture Diagram in Draw.io to align with cloud-native standards. | 21/06/2026 | 21/06/2026 | Group Project |

### Week 7 Achievements:
* **Identity Management (Amazon Cognito):** Proficient in building secure authentication flows, protecting API endpoints, and managing secure user session tokens.
* **Serverless Monitoring & Debugging:** Developed the ability to perform root-cause analysis in distributed systems. Skilled in setting up automated alerts (SNS) and identifying performance bottlenecks using X-Ray Service Maps.
* **Architecture Design:** Successfully mapped the complex data flow of the SOC platform, ensuring a scalable and secure design ready for cloud-native deployment.
* **DevOps Security:** Solidified IAM roles and security policies, ensuring the Docker-based MLOps platform operates under the principle of Least Privilege.