---
title: "Week 3 Worklog"
date: 2026-05-24
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---


### Week 3 Objectives:
* Master AWS Compute core concepts (Amazon EC2 configurations, AMIs, storage options, and lifecycle features) through Module 03.
* Implement an automated, event-driven data protection infrastructure using AWS Backup, CloudFormation, Amazon SNS, and AWS Lambda.
* Architect a scalable multi-VPC environment using AWS Transit Gateway as a centralized cloud router to overcome VPC Peering limitations.
* Coordinate with teammate to finalize the capstone project topic and delineate initial technical responsibilities.

### Tasks carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Completed Module 03 theoretical training (Videos 72-80).<br>- Studied EC2 Instance Types, Amazon Machine Images (AMI), and storage architecture differences (EBS vs. Instance Store).<br>- Analyzed EC2 bootstrap scripts (User Data) and instance metadata capabilities. | 18/05/2026 | 18/05/2026 | AWS Video Series |
| 3 | - Initiated the "Data Protection with AWS Backup" lab framework.<br>- Provisioned an S3 bucket named `thang-aws-backup-lab-2026` with explicit public permissions and a custom JSON Bucket Policy (`s3:GetObject`).<br>- Uploaded static architecture deployment templates (`backup-lab.yaml`, `lambda_function.zip`). | 19/05/2026 | 19/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Deployed core infrastructure utilizing AWS CloudFormation.<br>- Refactored the `backup-lab.yaml` template file to explicitly enforce the `t3.micro` instance type to ensure provisioning compatibility.<br>- Successfully built the target VPC environment, security groups, and the active web application server instance. | 20/05/2026 | 20/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Constructed an AWS Backup Vault named `BACKUP-LAB-VAULT` and mapped out an automated Backup Plan (`BACKUP-LAB`).<br>- Implemented a 7-day automated lifecycle retention policy for recovery points.<br>- Executed CLI configurations inside AWS CloudShell to link vault notification event hooks (`BACKUP_JOB_COMPLETED`, `RESTORE_JOB_COMPLETED`) directly to the Amazon SNS topic. | 21/05/2026 | 21/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - Triggered an On-demand Backup for the production EC2 instance.<br>- Monitored the serverless pipeline: successfully verified automated AWS Lambda execution initializing the Restore Test.<br>- Evaluated application logs inside Amazon CloudWatch Log Groups, received real-time email reports, and executed a complete environment cleanup (S3, CloudFormation, SNS). | 22/05/2026 | 22/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 7 | - Executed the advanced network architecture workshop: "Centralized Network Management with AWS Transit Gateway".<br>- Built a centralized Transit Gateway acting as a cloud router and connected 4 independent VPCs via TGW Attachments.<br>- Configured TGW Route Tables and updated individual VPC Route Tables (`172.16.0.0/16` and `0.0.0.0/0`) to successfully route traffic and perform cross-VPC ping tests.<br>- Held a project synchronization meeting to align on workload distribution. | 23/05/2026 | 24/05/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 3 Achievements:
* **Deep Compute Competency:** Acquired advanced operational knowledge of EC2 virtualization, storage mechanics (ephemeral vs. persistent), and infrastructure bootstrapping.
* **Infrastructure as Code (IaC):** Mastered CloudFormation syntax for deploying nested infrastructure safely while maintaining strict compliance with budget frameworks (`t3.micro` migration).
* **Automated Data Protection:** Successfully engineered an event-driven data lifecycle workflow utilizing AWS Backup, automated notifications via Amazon SNS, and scriptless validation checks through AWS Lambda.
* **Cloud Routing Proficiency:** Gained clear tactical insight into building Hub-and-Spoke enterprise networks. Successfully managed complex traffic routing between multiple VPCs using AWS Transit Gateway.
* **Team Governance:** Established clear task alignment and timeline milestones with teammate regarding the upcoming project implementation phase.