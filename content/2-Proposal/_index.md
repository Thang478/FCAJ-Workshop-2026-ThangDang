---
title: "Proposal"
date: 2026-06-30
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# MalScan AI — AI-Integrated Community Malware Detection Platform

---

## 1. Executive Summary

MalScan AI is a community-driven malware detection platform, operating on a model similar to a miniature VirusTotal. The system allows users to scan suspicious Portable Executable (PE) files (exe/dll), Office documents (Word/Excel/PDF/HTML), and URLs to detect malware using Machine Learning models (XGBoost, CNN). Concurrently, the system integrates a complete Machine Learning Operations (MLOps) lifecycle, enabling the Admin to retrain and deploy new models without system downtime. The entire platform is deployed on AWS ECS Fargate with a Containerized architecture, multi-layer protection (CloudFront + WAF + ALB), and persistent storage via Amazon EFS.

---

## 2. Problem Statement

*Current Issues*

Existing malware detection tools often require complex installations or rely entirely on third-party cloud services like VirusTotal (which has rate limits and lacks model customization capabilities). Furthermore, internal Security Operations Center (SOC) teams lack integrated tools to simultaneously perform malware analysis and manage the AI model lifecycle over time.

*The Solution*

MalScan AI provides a single communication portal via a Streamlit web app, featuring:
- PE file scanning using 2568 static features extracted directly from PE files based on the EMBER 2024 dataset (XGBoost + SHAP explanation).
- Office/PDF/HTML document scanning with a model trained on the CIC-Trap4Phish 2025 dataset.
- URL scanning utilizing a 3-branch CNN model combined with an OSINT engine (IP, WHOIS, SSL, Screenshot).
- A VirusTotal-style Hash Cache mechanism: previously scanned files/URLs return immediate results without re-running the AI models.
- MLOps Dashboard: data collection → data cleaning → training → staging test → production deploy.

---

## 3. Solution Architecture

The system is deployed using a Containerized architecture on AWS ECS Fargate, comprising two containers running in parallel within the same Fargate Task:

- **Container 1 (Streamlit — Port 8501)**: User Interface, PE Scanner, Document Scanner, URL Scanner, Model Management.
- **Container 2 (Flask API — Port 5000)**: Dedicated processing for the TensorFlow URL model (isolated to prevent `numpy` library conflicts).

![MalScan AI Architecture](<SƠ ĐỒ 4.drawio (8).png>)

*Main Data Flow:*

1. **(1) HTTPS Request:** User sends a request to CloudFront (integrated with AWS WAF to filter DDoS, SQL Injection, and XSS at the Edge).
2. **(2) Route valid traffic:** CloudFront routes valid traffic through the Internet Gateway into the VPC.
3. **(3) Forward port 443→8501:** The Internet Gateway forwards traffic to the Application Load Balancer in the Public Subnet.
4. **(4) Streamlit App (port 8501):** The ALB routes the request to the AWS Fargate Task located in the Private Subnet.
5. **(5) Read/Write models & SQLite:** The Fargate Task reads/writes ML models and the database on Amazon EFS.
6. **(6) Outbound traffic:** Outbound traffic from the Fargate Task is directed to the NAT Gateway.
7. **(7) Pull Docker image:** The system pulls the image securely via the ECR Endpoint (Private link).
8. **(8) External API calls:** The NAT Gateway calls External APIs (VirusTotal, MalwareBazaar, IP Geolocation, microlink.io).
9. **(9) Logs & Metrics:** The Fargate Task sends logs and metrics via the CloudWatch Endpoint.
10. **(10) Grant ECS permissions:** AWS IAM grants execution permissions (ECS Task Role) to the Fargate Task.
11. **(11) Fetch API Keys:** The Fargate Task retrieves secure keys via AWS Secrets Manager.

*AWS Services Utilized:*

| Service | Role |
|---|---|
| Amazon ECS Fargate | Runs 2 containers without server management overhead |
| Application Load Balancer | Routes traffic into the Private Subnet |
| AWS WAF + CloudFront | Edge protection, Layer 7 DDoS mitigation |
| Amazon ECR | Docker Image repository |
| Amazon EFS | Persistent storage: ML models + SQLite database |
| Amazon VPC | Network isolation: Public/Private Subnets, NAT Gateway, VPC Endpoints |
| Amazon CloudWatch | Log and metric collection |
| AWS Secrets Manager | Securely manages API Keys and credentials |
| AWS IAM | Controls ECS Task Role permissions |

---

## 4. Technical Implementation

*Deployment Phases:*

**Month 1 — Research & Model Development:**
- Train the PE model (XGBoost, 2568 static features from the EMBER dataset, supporting Win32/Win64).
- Train the Document model (Word/Excel/PDF/HTML using CIC-Trap4Phish 2025).
- Integrate the URL Scanner with a 3-branch CNN + OSINT engine (Achieving 97% accuracy on a dataset of 500,000 samples).
- Build the Model Lifecycle Management pipeline (data collection → training → staging → production).
- Package everything into a Docker Image (2 containers).

**Month 2 — AWS Infrastructure Deployment:**
- Set up the VPC (Public/Private Subnets, NAT Gateway, VPC Endpoints).
- Push the Docker Image to Amazon ECR.
- Configure the ECS Task Definition with EFS volume mounts.
- Set up the ALB and Target Group.
- Configure the IAM Task Role following the Least Privilege principle.

**Month 3 — Security, Testing & Documentation:**
- Configure WAF Rules and the CloudFront distribution.
- Set up AWS Secrets Manager to secure API Keys.
- Perform end-to-end system testing (monitoring logs/metrics on CloudWatch).
- Build the Hash Cache database (SQLAlchemy + SQLite on EFS).
- Implement the community registration/login system.
- Write the bilingual Workshop report and clean up resources.

*Technical Requirements:*
- **ML & App**: Python 3.12, XGBoost 3.3, TensorFlow 2.20, Streamlit, Flask, SHAP, scikit-learn.
- **Cloud**: AWS VPC, ECS Fargate, ALB, WAF, CloudFront, EFS, ECR, CloudWatch, Secrets Manager, IAM.
- **DevOps**: Docker, docker-compose (2 services), SQLAlchemy + SQLite.

---

## 5. Roadmap & Milestones

| Milestone | Timeframe | Outcome |
|---|---|---|
| PE Model finalized | Week 2 | Accuracy >97.5%, SHAP explanation integrated |
| Document Model finalized | Week 3 | 4 file types supported, F1 Score >93% |
| URL Scanner integrated | Week 5 | 97% accuracy on 500k samples |
| Docker build successful | Week 6 | 2 containers running stably |
| MLOps Dashboard | Week 7 | Train/Stage/Deploy pipeline completed |
| AWS Infrastructure | Week 9 | VPC, ECS, EFS, ALB, Secrets Manager live |
| Security Layer | Week 10 | WAF + CloudFront active |
| Hash Cache + Auth | Week 11 | Community features live |
| Workshop Report | Week 12 | Bilingual report, comprehensive screenshots |

---

## 6. Budget Estimation

*Estimated infrastructure costs based on the AWS Pricing Calculator (Region: Asia Pacific - Singapore):*

| Service | Cost/Month |
|---|---|
| AWS Fargate (Linux, x86, 8GB RAM, 20GB Storage, 1 task/day) | $35.38 |
| Application Load Balancer (1 ALB) | $18.63 |
| Amazon VPC (1 NAT Gateway, 2 VPC Endpoints) | $85.67 |
| Amazon EFS (10GB Storage) | $4.14 |
| AWS WAF ($8.02) + Amazon CloudFront ($1.36) | $9.38 |
| AWS Secrets Manager (Managing 3 secrets) | $0.90 |
| **Total Estimated Cost** | **$154.10/month** |

*Cost Optimization Strategy:*
- Establish a VPC Endpoints architecture for ECR and CloudWatch to maximally reduce the traffic routed through the NAT Gateway.
- The projected total cost for 12 months of operation is $1,849.20 (with $0.00 Upfront cost).
- Utilize AWS Budget Alerts to provide early warnings in case of anomalous cost spikes.

---

## 7. Risk Assessment

| Risk | Impact | Probability | Mitigation Strategy |
|---|---|---|---|
| Evasion Attack on the PE model | High | Medium | V2 model anti-evasion + VirusTotal cross-referencing |
| numpy/tensorflow library conflict | High | Occurred | Separate into 2 independent containers (Resolved) |
| Budget overrun (NAT Gateway) | Medium | High | VPC Endpoints + AWS Budget Alerts |
| URL Scanner False Positives | Medium | Medium | Combine AI scoring with OSINT for an aggregated result |
| API Key Leakage | Critical | Low | Transition to centralized management using AWS Secrets Manager |
| SQLite lock on EFS | Low | Low | Implement `connect_args timeout=30` + single Fargate task |

---

## 8. Expected Outcomes

*Technical Outcomes:*
- **PE Scanner:** Accuracy >97.5% based on static features extracted from PE files, providing clear SHAP explanations for each prediction to ensure AI decision transparency.
- **Document Scanner:** F1 Score >93% across 4 document formats (Word/Excel/PDF/HTML).
- **URL Scanner:** Achieves 97% accuracy on a dataset of 500,000 samples by combining a 3-branch CNN model with multi-source OSINT.
- **Hash Cache:** Significantly reduces response times for files/URLs previously analyzed by the system.
- **MLOps:** Closes the model management lifecycle from data collection to real-world production deployment.

*Long-term Value:*
- Community System: More users → fuller cache → reduced server load.
- Scalable Architecture: Adding a new scanner simply requires adding the corresponding container/module.
- MLOps Platform: Admins can continuously improve models based on real-world feedback.
- Future Development: Integration with Amazon Cognito, DynamoDB, and S3 for Enterprise scale.