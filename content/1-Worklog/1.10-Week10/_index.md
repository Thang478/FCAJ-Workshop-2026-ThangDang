---
title: "Week 10 Worklog"
date: 2026-07-12
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:
* Optimize and finalize the AWS Architecture Topology diagram based on in-depth feedback from experts.
* Perform cost estimation and Cloud FinOps optimization using the AWS Pricing Calculator.
* Aggregate community contributions and edit an in-depth technical blog post.
* Prepare all Proposal documentation for the upcoming Workshop and presentation scripts for the team.

### Tasks Completed During the Week:
| Day | Task | Start Date | End Date | References |
| --- | --- | --- | --- | --- |
| 2 | - **AWS Architecture Refinement:** Received feedback and adjusted the draw.io diagram: (1) Re-routed the connection from CloudFront directly into the Internet Gateway (IGW); (2) Redrew the AWS Fargate Task block accurately; (3) Removed icons for External Services and renamed them as self-developed services to avoid confusion. | 06/07/2026 | 06/07/2026 | AWS Architecture Icons, Admin Feedback |
| 3-4 | - **Cost Calculation & FinOps:** Detailed cost calculations for 7 services (Fargate, ALB, EFS, VPC, CloudFront, WAF, Secrets Manager) in the Singapore Region (AP-Southeast-1). Optimized the NAT Gateway configuration, finalizing the estimated cost at ~$103/month. Exported the detailed PDF estimate. | 07/07/2026 | 08/07/2026 | AWS Pricing Calculator |
| 5-6 | - **Community Blog Editing & Aggregation:** Reviewed and aggregated a technical article previously published on the AWS Study Group VN (on June 23) regarding *"Cost Optimization and Network Architecture with AWS Network Firewall & Transit Gateway."* Systematized the content for inclusion in the FCAJ community competency evaluation portfolio. | 09/07/2026 | 10/07/2026 | AWS Security Blog |
| 7 | - **Workshop Documentation Prep:** Drafted a complete 8-part Proposal. Prepared a bilingual (Vietnamese/English) architecture description and drafted presentation scripts to align the team's content. Monitored the team's AWS deployment progress. | 11/07/2026 | 12/07/2026 | FCAJ Workshop Guidelines |

### Week 10 Achievements:
* **Production-Ready Architecture:** Completely resolved routing logic errors (CloudFront -> IGW) and finalized the detailed AWS diagram, successfully defending the rationale for using ALB and EFS to the experts.
* **Financial Optimization:** Successfully adjusted the network configuration, bringing the total cost estimate down to ~$103/month, ensuring an optimal operational budget for the project.
* **Community Contribution:** Acknowledged and systematized research capabilities through an in-depth article on AWS Security (Transit Gateway Native Attachment), affirming a flexible security architecture mindset (Flexible cost allocation).