---
title: "Week 6 Work Log"
date: 2026-06-14
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:
* Master Data at Rest security mechanisms through AWS Key Management Service (KMS).
* Set up a comprehensive auditing system and API security logging using AWS CloudTrail, and perform serverless big data queries using Amazon Athena.
* Optimize the MLOps Web App source code: handle encrypted ZIP files, optimize UI memory allocation (Smart Cache), and perfect the automated quarantine pipeline (Sandbox).
* Draft the system architecture diagram and conduct stability testing on the final Docker version prior to actual deployment.

### Tasks Completed During the Week:
| Day | Tasks | Start Date | Completion Date | References |
| --- | --- | --- | --- | --- |
| 2 | - Studied Cloud Security theory: Differentiated between CMK (Customer Managed Keys) and AWS Managed Keys in KMS.<br>- Explored centralized event logging architecture using CloudTrail and Athena. | 08/06/2026 | 08/06/2026 | AWS Video Series |
| 3 | - Practice Lab: *AWS Key Management Service (KMS)*.<br>- Provisioned a Symmetric Key, configured IAM Policies (Least Privilege), and enforced default SSE-KMS encryption for Amazon S3 buckets. | 09/06/2026 | 09/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Practice Lab: *CloudTrail & Amazon Athena*.<br>- Enabled Data Events for S3. Authored SQL queries on the Athena console to trace `PutObject` events and verified `AccessDenied` errors for unauthorized decryption attempts. | 10/06/2026 | 10/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Group Project: Upgraded the Web App. Integrated the `pyzipper` library to support batch analysis of malware samples inside password-protected ZIP files (AES/ZipCrypto). | 11/06/2026 | 11/06/2026 | Group Project |
| 6 | - Group Project: Restructured the Streamlit UI. Implemented a *Smart Cache* mechanism to optimize VirusTotal API quotas.<br>- Built a Sandbox module to physically and automatically isolate files misclassified by AI. Fixed cross-platform path formatting bugs (`os.path.normpath`). | 12/06/2026 | 13/06/2026 | Group Project |
| 7 | - Group Project: Drafted the System Architecture Diagram using Draw.io.<br>- Rebuilt the Docker Image, conducted comprehensive user flow testing, and cleaned up AWS resources (Schedule Key Deletion, Empty S3) to optimize costs. | 14/06/2026 | 14/06/2026 | Group Project |

### Week 6 Achievements:
* **Data Security (AWS KMS):** Mastered the lifecycle of cryptographic keys, including provisioning, access control, and scheduled deletion, to protect S3 data repositories.
* **System Auditing & Digital Forensics:** Capable of setting up a system "black box". Proficient in using SQL via Amazon Athena to investigate thousands of access logs from CloudTrail to detect unauthorized behaviors.



* **MLOps System Upgrade:** Completed the technical workflow (UX/UI) for SOC Analysts, featuring batch ZIP scanning, a smart self-cleaning cache, and a fully automated Feedback Loop for data collection.
* **DevOps & Architecture:** Successfully containerized the advanced source code into an isolated environment. The project is now fully prepared to push the Docker Image to Amazon ECR in the upcoming phase.