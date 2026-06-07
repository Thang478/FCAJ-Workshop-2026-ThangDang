---
title: "Worklog Week 5"
date: 2026-06-07
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:
* Master the design mindset of Event-Driven Architecture on AWS.
* Build a fully automated Serverless Backend system using Amazon S3, AWS Lambda, and Amazon DynamoDB.
* Configure API Gateway as a secure interface between the Web Application and cloud services.
* Integrate project modules into a unified Web Application, package with Docker, and perform comprehensive testing in a containerized environment.

### Weekly Implementation Log:
| Day | Task | Start Date | End Date | References |
| --- | --- | --- | --- | --- |
| Mon | - Researched Event-Driven Architecture through video tutorials: *Module 07-Lab39-8 - LEDA*. <br>- Understood asynchronous trigger mechanisms between services. | 01/06/2026 | 01/06/2026 | AWS Video Series |
| Tue | - Completed Lab: *Serverless Backend with Lambda, S3, and DynamoDB*.<br>- Configured S3 Event Notifications to automatically trigger Lambda for file processing. | 02/06/2026 | 02/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| Wed | - Completed Lab: *Building Serverless APIs*.<br>- Initialized REST API on Amazon API Gateway, defined Resources and Methods (POST, GET, DELETE). | 03/06/2026 | 03/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| Thu | - Configured Lambda Proxy Integration and CORS to enable Web App-to-Backend communication.<br>- Verified API flow using Postman (HTTP 200 OK). | 04/06/2026 | 04/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| Fri | - Group Project: Integrated PE and Document analysis modules into a unified Web Application interface.<br>- Implemented communication flow between Frontend and Backend via API Gateway. | 05/06/2026 | 06/06/2026 | Team Project |
| Sat | - Containerized the entire Web Application using Docker.<br>- Performed container building, connection debugging, and stability testing in an isolated environment. | 07/06/2026 | 07/06/2026 | Team Project |

### Weekly Achievements:
* **Serverless Backend Architecture:** Successfully mastered the automated data flow from S3 trigger to Lambda processing and DynamoDB storage, gaining deep insight into serverless operations. 

[Image of AWS Serverless architecture]

* **API Gateway Connectivity:** Established a secure public API interface, gaining proficiency in Proxy Integration, CORS handling, and API Stage deployment.
* **Container Operations (Docker):** Successfully packaged a complex multi-page Web App into a Docker environment, ensuring environment consistency between development and testing.
* **System Integration:** Solidified the core architectural framework of the project, ready for real-world integration with the AWS cloud infrastructure in the coming week.