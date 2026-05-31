---
title: "Week 4 Worklog"
date: 2026-05-31
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---


### Week 4 Objectives:
* Master core security mechanisms and optimize data flow for Amazon S3, establishing a secure storage foundation.
* Grasp the mechanics of Containerization utilizing Docker through localized deployment testing to bypass environmental capacity limits.
* Refactor and advance the "Serverless Malware Scanner" project: Launch the Web App locally, expand the Document Analysis Model, and establish a miniature MLOps framework.
* Systematize and containerize all machine learning models (PE & Document) into standalone environments as a strategic fallback plan.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Completed theoretical training (Videos 103 - 109) reinforcing AWS system design principles.<br>- Researched Containerization architecture, distinguishing between traditional virtual machines and container structures. | 25/05/2026 | 25/05/2026 | AWS Video Series |
| 3 | - Implemented advanced security configurations for Amazon S3 (Lab: S3 Security Best Practices).<br>- Enforced server-side encryption (SSE-S3) and HTTPS transit via customized S3 Bucket Policies.<br>- Activated Block Public Access (BPA) at the bucket level to mitigate unintended data exposure. | 26/05/2026 | 26/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Configured S3 VPC Endpoints to route traffic privately and securely, optimizing internal network flows.<br>- Successfully installed and initialized Docker Desktop on the local development environment. | 27/05/2026 | 27/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Executed the Docker web application containerization lab.<br>- Scripted the `Dockerfile`, executed the build process (`docker build`), and ran localized tests (`docker run`) to circumvent immediate cloud costs.<br>- Successfully authenticated and pushed the generated Docker Image to the public Docker Hub registry. | 28/05/2026 | 28/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - Resumed group project development: Finalized the Document Model supporting Word, Excel, PDF, and HTML analysis.<br>- Implemented concurrent batch upload functionalities within the Web App interface.<br>- Successfully containerized the PE Model (XGBoost, 2568 features, SHAP/Defender integration) into a stable, localized Docker environment. | 29/05/2026 | 29/05/2026 | Team Project |
| 7 | - Developed MLOps capabilities (Continuous Training): Engineered a pipeline to cross-reference Document Model predictions against the VirusTotal API.<br>- Automated the extraction of false predictions into a local SQLite database for future training.<br>- Programmed threshold-based auto-training triggers, integrated A/B testing protocols, Model Registry version control, and fallback retention logic. | 30/05/2026 | 31/05/2026 | Team Project |

### Week 4 Achievements:
* **Cloud Security Mindset (S3):** Demonstrated practical application of multi-layered storage security leveraging Bucket Policies, mandatory encryption, and private VPC routing.
* **Container Architecture (Docker):** Acquired proficiency in deployment automation using Docker, equipping the project to overcome deployment size limitations on cloud infrastructure.
* **ML Architecture & Data Pipelines:** Finalized a miniature MLOps lifecycle encompassing automated data ingestion, ground-truth cross-validation (via VirusTotal), and intelligent model retraining capabilities.
* **Risk Mitigation:** Secured project continuity by successfully packaging the entire PE and Document analytical engine into a localized Container version, ensuring deployment readiness.