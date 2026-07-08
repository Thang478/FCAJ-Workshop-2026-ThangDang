---
title: "Week 9 Worklog"
date: 2026-07-05
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:
* Develop the Authentication module and Role-Based Access Control (RBAC).
* Configure Data Segregation to ensure absolute privacy for the scanning history and cache of each user.
* Build an Admin Dashboard integrated with visual statistical charts.
* Package, standardize technical documentation, and hand over the source code to the team responsible for Cloud infrastructure deployment.
* Restructure and finalize the overall System Architecture Topology.

### Tasks Completed During the Week:
| Day | Task | Start Date | End Date | References |
| --- | --- | --- | --- | --- |
| 2 | - **Auth Development & Data Segregation:** Coded the Register/Login functionalities. Established database routing logic to completely isolate the scanning history (URL, Document, PE files) and temporary cache of each user, ensuring users cannot view each other's data. | 29/06/2026 | 29/06/2026 | Web Authentication Best Practices, Data Isolation |
| 3 | - **Admin Dashboard Implementation:** Designed a module specifically for Administrators. Added privileges allowing the Admin to view the overall data of the entire system and integrated visual charting libraries (Statistical Charts) to track usage traffic and malware analysis results. | 30/06/2026 | 30/06/2026 | Data Visualization, RBAC Models |
| 4 | - **Bug Fixing & Security Optimization:** Detected and resolved logic bugs related to password validation and Password Hashing. Patched Session Leakage vulnerabilities when switching between User and Admin accounts. | 01/07/2026 | 01/07/2026 | OWASP Authentication Cheat Sheet |
| 5 | - **Integration Testing on Docker:** Relaunched the Multi-container system using `docker-compose`. Executed multi-threaded login testing scenarios and cross-data queries to ensure the authorization mechanism operates stably without memory conflicts. | 02/07/2026 | 02/07/2026 | Docker Compose Workflow |
| 6 | - **Source Code Packaging & Handover:** Standardized the directory structure and removed redundant configuration files. Handed over the clean, stable source code to the members responsible for pushing to AWS (ECR, ECS Fargate). | 03/07/2026 | 03/07/2026 | Git / GitHub Collaboration |
| 7 | - **Network Architecture Finalization & Review:** Collaborated with the team to review and redraw the detailed Infrastructure Architecture Diagram (Multi-AZ, ALB, VPC Endpoints, NAT Gateway, EFS, and AWS WAF). Supported the AWS team in resolving initial bottlenecks regarding container connection routing. | 04/07/2026 | 05/07/2026 | Internal Team, AWS Architecture Diagrams |

### Week 9 Achievements:
* **Enforcing the Principle of Least Privilege:** Successfully applied the RBAC model and Data Segregation, thoroughly solving the user data privacy issue while maintaining the centralized monitoring and statistical capabilities of the Admin.
* **Core Web Features Finalization:** Cleanly resolved logic bugs in the account management module, making the application highly reliable and ready to serve multiple concurrent test users.
* **Teamwork & Delivery:** Successfully handed over the optimized and rigorously tested source code on the Docker virtualized environment, paving the way for a smooth deployment to the cloud infrastructure.
* **System Design Standardization:** Finalized the detailed architectural topology diagram, providing a solid foundation for calculating the cost estimate (AWS Calculator) and establishing the theoretical basis for network infrastructure in the final report.