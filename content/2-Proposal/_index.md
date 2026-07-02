---
title: "Proposal"
date: 2026-06-30
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# MalScan AI — Community-Based AI Malware Detection Platform

---

## 1. Executive Summary

MalScan AI is a community-oriented malware detection platform inspired by VirusTotal. It allows users to scan PE executable files (exe/dll), Office documents (Word/Excel/PDF/HTML), and suspicious URLs using Machine Learning models (XGBoost, CNN). The platform also integrates a complete Model Lifecycle Management (MLOps) system, enabling admins to retrain and deploy new models without system downtime. The entire system is deployed on AWS ECS Fargate with a containerized architecture, multi-layer security (CloudFront + WAF + ALB), and persistent storage via Amazon EFS.

---

## 2. Problem Statement

*Current Problem*

Existing malware detection tools often require complex installation or rely entirely on third-party cloud services like VirusTotal (rate-limited, no model customization). Additionally, internal SOC teams lack integrated tools to both analyze malware and manage the AI model lifecycle over time.

*Solution*

MalScan AI provides a single entry point through a Streamlit web interface, supporting:
- PE file scanning with 2568 EMBER 2024 features (XGBoost + SHAP explanation)
- Office/PDF/HTML document scanning with models trained on CIC-Trap4Phish 2025
- URL scanning with a 3-branch CNN model combined with OSINT (IP, WHOIS, SSL, Screenshot)
- VirusTotal-style Hash Cache: previously scanned files/URLs return instant results without re-running AI
- MLOps Dashboard: data collection → cleaning → training → staging test → production deploy

---

## 3. Solution Architecture

The system is deployed using a containerized architecture on AWS ECS Fargate, with two containers running in parallel within the same Fargate Task:

- **Container 1 (Streamlit — Port 8501)**: User interface, PE Scanner, Document Scanner, URL Scanner, Model Management
- **Container 2 (Flask API — Port 5000)**: Dedicated TensorFlow URL model handler (isolated to avoid numpy library conflicts)

![MalScan AI Architecture](/images/2-Proposal/architecture.png)

*Main Data Flow:*

1. User sends HTTPS Request → CloudFront (Global CDN)
2. CloudFront → AWS WAF (filters DDoS, SQL Injection, XSS)
3. WAF → Internet Gateway → VPC
4. IGW → Application Load Balancer (Public Subnet, port 443→8501)
5. ALB → AWS Fargate Task (Private Subnet, port 8501)
6. Fargate ↔ Amazon EFS (read/write ML models + SQLite database)
7. Fargate → NAT Gateway → Internet (calls External APIs)
8. NAT → ECR (pull Docker image via ECR VPC Endpoint)
9. NAT → VirusTotal, MalwareBazaar, IP Geolocation, microlink.io
10. Fargate → CloudWatch VPC Endpoint → CloudWatch (logs & metrics)
11. AWS IAM ECS Task Role → grants permissions to Fargate

*AWS Services Used:*

| Service | Role |
|---|---|
| Amazon ECS Fargate | Run 2 containers without server management |
| Application Load Balancer | Route traffic into Private Subnet |
| AWS WAF + CloudFront | Edge protection, Layer 7 DDoS mitigation |
| Amazon ECR | Docker Image registry |
| Amazon EFS | Persistent storage: ML models + SQLite |
| Amazon VPC | Network isolation: Public/Private Subnet, NAT Gateway, VPC Endpoints |
| Amazon CloudWatch | Log and metrics collection |
| AWS IAM | ECS Task Role permission control |

---

## 4. Technical Implementation

*Deployment Phases:*

**Month 1 — Research & Model Development:**
- Train PE model (XGBoost, 2568 EMBER features, Win32/Win64)
- Train Document model (Word/Excel/PDF/HTML from CIC-Trap4Phish 2025)
- Integrate URL Scanner with 3-branch CNN + OSINT engine
- Build Model Lifecycle Management (data collection → training → staging → production)
- Package everything into Docker Images (2 containers)

**Month 2 — AWS Infrastructure Deployment:**
- Set up VPC (Public/Private Subnet, NAT Gateway, VPC Endpoints)
- Push Docker Images to Amazon ECR
- Configure ECS Task Definition with EFS volume mount
- Set up ALB and Target Group
- Configure IAM Task Role following Least Privilege principle

**Month 3 — Security, Testing & Documentation:**
- Configure WAF Rules and CloudFront distribution
- End-to-end system testing (log/metric via CloudWatch)
- Build Hash Cache database (SQLAlchemy + SQLite on EFS)
- Deploy community registration/login system
- Write bilingual Workshop report and clean up resources

*Technical Requirements:*
- **ML & App**: Python 3.12, XGBoost 3.3, TensorFlow 2.20, Streamlit, Flask, SHAP, scikit-learn
- **Cloud**: AWS VPC, ECS Fargate, ALB, WAF, CloudFront, EFS, ECR, CloudWatch, IAM
- **DevOps**: Docker, docker-compose (2 services), SQLAlchemy + SQLite

---

## 5. Roadmap & Milestones

| Milestone | Timeline | Deliverable |
|---|---|---|
| PE Model complete | Week 2 | Accuracy >97.5%, SHAP explanation |
| Document Model complete | Week 3 | 4 file types, F1 >93% |
| URL Scanner integrated | Week 5 | CNN + OSINT + Screenshot |
| Docker build successful | Week 6 | 2 containers running stably |
| MLOps Dashboard | Week 7 | Full Train/Stage/Deploy pipeline |
| AWS Infrastructure | Week 9 | VPC, ECS, EFS, ALB live |
| Security Layer | Week 10 | WAF + CloudFront active |
| Hash Cache + Auth | Week 11 | Community features live |
| Workshop Report | Week 12 | Bilingual, full screenshots |

---

## 6. Budget Estimate

*Estimated Infrastructure Cost (AWS Pricing Calculator):*

| Service | Cost/month |
|---|---|
| AWS Fargate (0.5 vCPU, 2GB RAM, 24/7) | ~$20 |
| Application Load Balancer | ~$16 |
| NAT Gateway | ~$32 |
| Amazon EFS (10GB) | ~$3 |
| AWS WAF + CloudFront | ~$5 |
| Amazon ECR (5GB) | ~$0.5 |
| **Total Estimate** | **~$76.5/month** |

*Cost Optimization Strategy:*
- Scale ECS Task to 0 when no traffic (saves ~$20 Fargate)
- VPC Endpoints for ECR and CloudWatch (reduce NAT Gateway load)
- Set AWS Budget Alert at $100 for early warning
- With $200 AWS credits: system can operate stably for ~2.5 months

---

## 7. Risk Assessment

| Risk | Impact | Probability | Mitigation Strategy |
|---|---|---|---|
| Evasion Attack on PE model | High | Medium | Anti-evasion V2 model + VirusTotal cross-check |
| numpy/tensorflow library conflict | High | Occurred | Separate 2 independent containers (resolved) |
| Budget overrun (NAT Gateway) | Medium | High | VPC Endpoints + AWS Budget Alert |
| URL Scanner False Positive | Medium | Medium | Combine AI score + OSINT for composite result |
| API Key leakage | Critical | Low | Store via ECS environment variables, never hardcode |
| SQLite lock on EFS | Low | Low | connect_args timeout=30 + single Fargate task |

---

## 8. Expected Outcomes

*Technical Results:*
- PE Scanner: Accuracy >97.5% with SHAP explanation per prediction
- Document Scanner: F1 Score >93% across 4 file types (Word/Excel/PDF/HTML)
- URL Scanner: Phishing detection with 3-branch CNN + multi-source OSINT
- Hash Cache: Significantly reduced response time for previously scanned files/URLs
- MLOps: Complete model lifecycle from data collection to production deploy

*Long-term Value:*
- Community system: More users → fuller cache → lighter server load
- Scalable architecture: Add new scanners by simply adding containers/modules
- MLOps platform: Admin can continuously improve models from real-world feedback
- Future development: Integrate Amazon Cognito, DynamoDB, S3 for enterprise scale