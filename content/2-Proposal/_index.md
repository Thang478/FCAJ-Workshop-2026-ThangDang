---
title: "Project Proposal"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# MalScan AI — AI-Integrated Community Malware Detection Platform

---

## 1. Executive Summary

MalScan AI is a community-driven malware detection platform operating on a miniature VirusTotal model. The system allows users to scan executable PE files (exe/dll), Office documents (Word/Excel/PDF/HTML), and suspicious URLs to detect malware using Machine Learning models (XGBoost, CNN). Concurrently, the system integrates a complete Model Lifecycle Management (MLOps) pipeline, allowing Admins to retrain and deploy new models seamlessly without system downtime. The entire platform is deployed on AWS ECS Fargate using a containerized architecture, featuring multi-layer protection (Route 53 + CloudFront + WAF + ALB) and persistent storage via Amazon EFS.

---

## 2. Problem Statement

*Current Issues*

Existing malware detection tools often require complex installations or rely entirely on third-party cloud services like VirusTotal (which have rate limits and lack model customization capabilities). Furthermore, internal SOC teams lack integrated tools to simultaneously analyze malware and manage the AI model lifecycle over time.

*Our Solution*

MalScan AI provides a single unified gateway via a Streamlit web app interface, supporting:
- Scanning PE files using 2568 static features extracted directly from PE files based on the EMBER 2024 dataset (XGBoost + SHAP explanation).
- Scanning Office/PDF/HTML documents with a model trained on the CIC-Trap4Phish 2025 dataset.
- Scanning URLs using a 3-branch CNN model combined with OSINT (IP, WHOIS, SSL, Screenshot).
- VirusTotal-style Hash Cache mechanism: previously scanned files/URLs return instant results without re-running AI inference.
- MLOps Dashboard: data collection → data cleaning → training → staging test → production deployment.

---

## 3. Solution Architecture

The system is deployed using a containerized architecture on AWS ECS Fargate, consisting of two containers running in parallel within a single Fargate Task:

- **Container 1 (Streamlit — Port 8501)**: User Interface, PE Scanner, Document Scanner, URL Scanner, Model Management.
- **Container 2 (Flask API — Port 5000)**: Exclusively handles the TensorFlow URL model (isolated to prevent numpy library conflicts).

![MalScan AI Architecture](<SƠ ĐỒ 4.drawio (10).png>)

*Main Data Flow:*

1. **(1) HTTPS Request:** Users access the system via a custom domain, resolved by Amazon Route 53, which routes traffic to CloudFront (integrated with AWS WAF to filter DDoS, SQL Injection, and XSS at the Edge).
2. **(2) Route valid traffic:** CloudFront routes valid traffic through the Internet Gateway to enter the VPC.
3. **(3) Forward port 443→8501:** The Internet Gateway forwards traffic to the Application Load Balancer in the Public Subnet.
4. **(4) Streamlit App (port 8501):** The ALB balances and forwards requests to the AWS Fargate Task located in the Private Subnet.
5. **(5) Read/Write models & SQLite:** The Fargate Task reads/writes ML models and the database on Amazon EFS.
6. **(6) Outbound traffic:** Outbound traffic from the Fargate Task is routed to the NAT Gateway.
7. **(7) Pull Docker image:** The system pulls images via the ECR Endpoint (Private link).
8. **(8) External API calls:** The NAT Gateway makes calls to External APIs (VirusTotal, MalwareBazaar, IP Geolocation, microlink.io).
9. **(9) Logs & Metrics:** The Fargate Task sends logs and metrics via the CloudWatch Endpoint.
10. **(10) Grant ECS permissions:** AWS IAM grants execution permissions (ECS Task Role) to the Fargate Task.
11. **(11) Fetch API Keys:** The Fargate Task retrieves security keys securely through AWS Secrets Manager.

*AWS Services Utilized:*

| Service | Role |
|---|---|
| Amazon Route 53 | Domain Name System (DNS) resolution and reliable user traffic routing |
| Amazon ECS Fargate | Runs 2 containers without server management |
| Application Load Balancer | Distributes incoming traffic into the Private Subnet |
| AWS WAF + CloudFront | Edge protection, content delivery, and Layer 7 DDoS mitigation |
| Amazon ECR | Stores Docker Images |
| Amazon EFS | Persistent storage: ML models + SQLite database |
| Amazon VPC | Network isolation: Public/Private Subnets, NAT Gateway, VPC Endpoints |
| Amazon CloudWatch | Collects logs and metrics |
| AWS Secrets Manager | Securely manages API Keys and credentials |
| AWS IAM | Controls ECS Task Role permissions |

---

## 4. Technical Implementation

*Implementation Phases:*

**Month 1 — Model Research & Development:**
- Train PE model (XGBoost, 2568 static features from the EMBER dataset, supporting Win32/Win64).
- Train Document model (Word/Excel/PDF/HTML from CIC-Trap4Phish 2025).
- Integrate URL Scanner with 3-branch CNN + OSINT engine (Achieved 97% accuracy on a 500,000 sample dataset).
- Build Model Lifecycle Management (data collection → training → staging → production).
- Package everything into Docker Images (2 containers).

**Month 2 — AWS Infrastructure Deployment:**
- Setup VPC (Public/Private Subnets, NAT Gateway, VPC Endpoints).
- Push Docker Images to Amazon ECR.
- Configure ECS Task Definition with EFS volume mounts.
- Setup ALB and Target Groups.
- Configure IAM Task Role based on the Least Privilege principle.

**Month 3 — Security, Testing & Documentation:**
- Configure WAF Rules and CloudFront distribution.
- Setup AWS Secrets Manager to secure API Keys.
- Perform end-to-end system testing (logs/metrics on CloudWatch).
- Build Hash Cache database (SQLAlchemy + SQLite on EFS).
- Implement community registration/login system.
- Write bilingual Workshop report and clean up resources.

*Technical Requirements:*
- **ML & App**: Python 3.12, XGBoost 3.3, TensorFlow 2.20, Streamlit, Flask, SHAP, scikit-learn.
- **Cloud**: AWS VPC, ECS Fargate, ALB, WAF, CloudFront, EFS, ECR, CloudWatch, Secrets Manager, IAM.
- **DevOps**: Docker, docker-compose (2 services), SQLAlchemy + SQLite.

---

## 5. Roadmap & Milestones

| Milestone | Timeline | Outcome |
|---|---|---|
| PE Model Completed | Week 2 | Accuracy >97.5%, SHAP explanation |
| Document Model Completed | Week 3 | 4 file types, F1 >93% |
| URL Scanner Integrated | Week 5 | 97% accuracy on 500k samples |
| Docker Build Successful | Week 6 | 2 stable running containers |
| MLOps Dashboard | Week 7 | Complete Train/Stage/Deploy flow |
| AWS Infrastructure | Week 9 | VPC, ECS, EFS, ALB, Secrets Manager live |
| Security Layer | Week 10 | WAF + CloudFront active |
| Hash Cache + Auth | Week 11 | Community features live |
| Workshop Report | Week 12 | Bilingual, complete screenshots |

---

## 6. Budget Estimate

*Estimated infrastructure costs via AWS Pricing Calculator (Region: Asia Pacific - Singapore):*

| Service | Cost/Month |
|---|---|
| AWS Fargate (Linux, x86, 8GB RAM, 20GB Storage, 1 task/day) | $35.38 |
| Application Load Balancer (1 ALB) | $18.63 |
| Amazon VPC (1 NAT Gateway, 2 VPC Endpoints) | $85.67 |
| Amazon EFS (10GB Storage) | $4.14 |
| AWS WAF ($8.02) + Amazon CloudFront ($1.36) | $9.38 |
| AWS Secrets Manager (Managing 3 secrets) | $0.90 |
| Amazon Route 53 (1 Hosted Zone) | $0.50 |
| **Total Estimated Cost** | **$154.60/month** |

*Cost Optimization Strategy:*
- Established VPC Endpoints architecture for ECR and CloudWatch to minimize traffic routed through the NAT Gateway.
- Total projected cost for 12 months of operation is $1,855.20 (Upfront cost: $0.00).
- Utilized AWS Budget Alerts for early warnings in case of unexpected cost spikes.

---

## 7. Risk Assessment

| Risk | Impact | Probability | Mitigation Strategy |
|---|---|---|---|
| Evasion Attack on PE model | High | Medium | V2 Model against evasion + VirusTotal cross-referencing |
| numpy/tensorflow library conflict | High | Occurred | Separated into 2 independent containers (Resolved) |
| Budget overrun (NAT Gateway) | Medium | High | VPC Endpoints + AWS Budget Alerts |
| False Positive on URL Scanner | Medium | Medium | Combine AI score + OSINT for a comprehensive result |
| API Keys Leakage | Critical | Low | Transition to centralized management using AWS Secrets Manager |
| SQLite lock on EFS | Low | Low | `connect_args timeout=30` + single Fargate task |

---

## 8. Expected Outcomes

*Technical Outcomes:*
- **PE Scanner:** Accuracy >97.5% based on static features extracted from PE files, providing clear SHAP explanations for each prediction to ensure AI transparency.
- **Document Scanner:** F1 Score >93% across 4 document formats (Word/Excel/PDF/HTML).
- **URL Scanner:** Achieved 97% accuracy on a 500,000 sample dataset by combining a 3-branch CNN model and multi-source OSINT.
- **Hash Cache:** Significantly reduced response time for previously analyzed files/URLs.
- **MLOps:** Closed the model lifecycle loop from data collection to production deployment.

*Long-term Values:*
- Community system: More users → fuller cache → lighter server load.
- Scalable architecture: Adding new scanners only requires adding corresponding containers/modules.
- MLOps Platform: Admins can continuously improve models based on real-world feedback.
- Future roadmap: Integrate Amazon Cognito, DynamoDB, and S3 for Enterprise-scale operations.