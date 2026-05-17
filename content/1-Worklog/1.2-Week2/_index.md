---
title: "Week 2 Worklog"
date: 2026-05-17
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives

* **Theory:** Acquire a solid foundational understanding of cloud networking concepts utilizing Amazon Virtual Private Cloud (VPC).
* **Hands-on Practice:** Implement a real-world AWS Site-to-Site VPN architecture to securely bridge two isolated network environments.
* **Advanced Skills:** Develop a strong mindset for log analysis and infrastructure troubleshooting on modern cloud operating systems.

---

### Tasks Carried Out

| Phase | Detailed Tasks Performed | Status | Reference Material |
| :--- | :--- | :--- | :--- |
| **Research & Learning** | - Reviewed AWS tutorial video series (2025 - 2026) from scratch up to VPC Lab 2-1.<br>- Studied core concepts: Subnets, Route Tables, Internet Gateways (IGW), NAT Gateways, Security Groups (SG), and Network ACLs (NACLs). | **Completed** | AWS Study Group - Blog / YouTube |
| **Basic Practice** | - Conducted the workshop: **AWS Networking Fundamentals**.<br>- Manually configured multi-tier network segmentation (Public Subnet for public-facing servers, Private Subnet for internal databases). | **Completed** | AWS Study Group - Workshop |
| **Advanced Practice** | - Deployed an **AWS Site-to-Site VPN** architecture connecting Main Office (VPC ASG) and Branch Office (VPC ASG VPN).<br>- Initialized Virtual Private Gateway (VGW), Customer Gateway (CGW), and configured Static Routing. | **Completed** | AWS Study Group - Workshop |
| **Troubleshooting** | - Migrated configuration from legacy OpenSwan to **Libreswan** to ensure compatibility with **Amazon Linux 2023**.<br>- Debugged sequential syntax errors, indentation issues, and hidden Windows CRLF characters using the `dos2unix` utility. | **Completed** | AWS Health / Support Engineer |
| **Cleanup & Optimization** | - Executed a strict resource decommissioning process to eliminate hidden charges (Terminated EC2 instances, released Elastic IPs, deleted NAT Gateways, cleared CloudWatch Flow Logs & Reachability Analyzer paths). | **Completed** | AWS Console |

---

### Week 2 Achievements

* **Robust Network Infrastructure Construction:** Mastered the VPC management console and structural dependencies. Deeply understood the cooperative defense-in-depth mechanics between Subnet-level firewalls (NACL - Stateless) and Instance-level firewalls (Security Group - Stateful).
* **Successful VPN Tunnel Establishment:** Successfully resolved persistent syntax issues, shifting the system state from `Loaded 0` to **`Total IPsec connections: loaded 2`**.
* **Internal Connectivity Verified:** Confirmed secure end-to-end communication by successfully executing `ping` commands between the Private EC2 instance and the Customer Gateway using internal IPs over the encrypted IPsec tunnel.
* **Real-World Troubleshooting Expertise:** Acquired hands-on proficiency with advanced Linux networking commands to inspect and force-load configuration files:
  ```bash
  sudo systemctl status ipsec
  sudo ipsec status
  sudo dos2unix /etc/ipsec.d/aws.conf
