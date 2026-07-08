---
title: "Week 8 Worklog"
date: 2026-06-28
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:
* Comprehensive integration of core modules (PE Scanner, Document Scanner, URL Scanner) into a unified project structure.
* Package the application into an isolated environment using Docker and Docker Compose.
* Completely resolve dependency conflicts arising from merging Machine Learning and Deep Learning models into the same environment.
* Refactor the application architecture from Monolithic to Multi-container to ensure system stability.

### Tasks Completed This Week:
| Day | Task | Start Date | Completion Date | References |
| --- | --- | --- | --- | --- |
| 2 | - **Source Code Integration:** Merged the two core modules of the project, PE Scanner (XGBoost) and URL Phishing Scanner (TensorFlow), into a single project directory. | 22/06/2026 | 22/06/2026 | Internal source code |
| 3 | - **Local Testing & Writing Dockerfile:** Initialized the `Dockerfile` and `docker-compose.yml` to package the entire monolithic system. Mapped volumes and exposed port 8501. | 23/06/2026 | 23/06/2026 | Docker Documentation |
| 4 | - **Critical Error Detection:** When running `docker compose build`, the system crashed due to a `numpy` version conflict between TensorFlow and XGBoost/SHAP.<br>- The PE model failed to load the configuration metric (`base_score`). | 24/06/2026 | 24/06/2026 | StackOverflow / GitHub Issues |
| 5 | - **Debugging:** Applied the "Pinning Version" strategy in `requirements.txt`.<br>- Experimented with switching to `tensorflow-cpu` to reduce Image size and mitigate RAM overflow risks on Docker. | 25/06/2026 | 25/06/2026 | TensorFlow Docs |
| 6 | - **Architecture Modification:** Despite trying multiple methods, forcing 2 frameworks into the same memory space remained unstable. Decided to "tear down and rebuild," splitting the system into independent containers. | 26/06/2026 | 26/06/2026 | AWS Microservices Architecture |
| 7 | - **Multi-Container Deployment:** Split the project into 2 parallel containers:<br>&emsp;+ *Container 1 (Port 8501):* Runs Streamlit containing the PE Scanner & Document Scanner.<br>&emsp;+ *Container 2 (Port 5000):* Runs a Flask API dedicated to processing the TensorFlow URL model. | 27/06/2026 | 28/06/2026 | Docker Compose Docs |

### Week 8 Achievements:
* **Mastering Troubleshooting Process:** Enhanced skills in reading package manager (pip) error logs and analyzing the root cause of core dependency conflicts (Dependency Hell) between different AI platforms.
* **System Design Mindset:** Instead of stubbornly patching errors on a patchwork Monolithic architecture, boldly adopted a distributed mindset. Separating the URL processing engine (TensorFlow) into an independent Backend API completely eliminated the `numpy` conflict.
* **Successful Dockerization:** Completed the `docker-compose.yml` file, running 2 parallel services (Streamlit and Flask) that communicate smoothly via Docker's virtual internal network. The system is now ready for the Image push to Amazon ECR in the upcoming weeks.