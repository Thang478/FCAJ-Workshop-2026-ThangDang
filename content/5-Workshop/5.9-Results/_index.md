---
title: "Results and demo video"
date: 2026-07-22
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

# Deployment results and demo video

After completing the configuration steps, MalScanAI is deployed on Amazon ECS Fargate and users access the application through the configured domain name.

The final workshop video will demonstrate:

- Accessing MalScanAI through the HTTPS domain.
- Verifying the Streamlit interface.
- Scanning a sample URL or file.
- Following the processing flow and reviewing the returned result.
- Checking the ECS service, task, and target group status.
- Accessing the Application Load Balancer directly to confirm that an invalid request receives a `403` response.



### 🖥️ Detailed Features of MalScanAI Web Interface (SOC Platform Edition)

The system is designed with a 3-tier Role-Based Access Control (Guest, User, Admin) and features a **Multi-language (i18n)** interface for an optimal user experience. Higher tiers inherit all functionalities from the previous levels and gain additional administrative privileges.

#### 1. Guest (Unregistered User)
*   **Resource Protection (Rate Limiter):** Limited file upload size (Max 200MB/file), batch size, and daily scan quotas to prevent system spam. Scan history is not saved.
*   **URL Phishing Scanner:** Analyzes suspicious links using AI combined with Open-Source Intelligence (OSINT) extraction.
*   **File Scanner (PE & Document):** Supports single or batch file analysis. Cross-references results with VirusTotal.
*   **Secure ZIP Extraction:** Capable of detecting password-protected ZIP files (a common evasion technique used by hackers) and provides a form to enter the password for safe extraction and deep structural scanning.
*   **Advanced PE Scanner:** 
    *   Automatically detects Win32/Win64 software architectures.
    *   **Dual-Model AI Integration:** Equipped with a standard analysis model (V1) and a specialized **Evasion-resilient model (V2)**. The system allows users to flexibly activate Model V2 to uncover sophisticated, stealthy malware, enhancing detection rates.
    *   Directly detects malformed/modified files (High Entropy, suspected packing/encryption) and requires user confirmation before allowing deep AI analysis.
*   **Delivered Results:** Real-time risk reports directly on the screen. Utilizes Explainable AI (XAI) via SHAP to provide transparency on the AI's decision-making process.

#### 2. Registered User
*   **Inheritance:** Includes all Guest scanning features.
*   **Account Security:** Passwords are securely hashed using one-way encryption (Bcrypt).
*   **Upgraded Quotas:** File size and batch scanning limits are expanded up to 3 times compared to Guests (supports drag-and-drop for hundreds of files for batch scanning).
*   **Customization:** Option to toggle VirusTotal cross-referencing on/off to speed up local analysis.
*   **History Management:** Automatically stores the complete history of scanned URLs and files, along with a personal statistics overview.
*   **Delivered Results:** Access to a personal Dashboard. Instantly review past scan details without re-analyzing, thanks to the ultra-fast **Hash Cache System**.

#### 3. Administrator (MLOps & SOC Privileges)
*   **Inheritance:** Includes all User features and storage capabilities.
*   **SOC Dashboard Landing Page:** Real-time, comprehensive system monitoring:
    *   *Storage Status:* Monitors actual cloud disk space. (e.g., 🖥️ **Server Status** 📊 *Used: 0.0 GB / 8589934592.0 GB*).
    *   *Hash Cache Database Statistics:* Displays total scans (URL, PE), Phishing/Malware detection rates (%), user count, and system acceleration performance (Cache Hit Rate).
    *   *AI Modules Status:* Monitors the operational state (Production Active) and performance metrics (F1 Score, Accuracy) of all 6 AI cores (WORD, EXCEL, PDF, HTML, PE Win32, PE Win64).
    *   *Analytics Charts:* Visualizes file status distribution and centrally manages System Error Logs securely hidden on the EFS (Elastic File System).
*   **User & Cost Management:** Manages roles (Promote to Admin/User). Upon user deletion, the system triggers **Garbage Collection**—automatically scanning the EFS to wipe orphaned physical files previously uploaded by that user (if no cross-references exist), optimizing AWS storage costs.
*   **AI Lifecycle Management (MLOps):** Controls the end-to-end pipeline: *Data Ingestion → Training → Staging → Production*.
    *   *Data Ingestion:* Deploys the automated "PE Hunter" to scan Data Lakes (MalwareBazaar) and collect new samples when the AI mispredicts. Supports manual file uploads and visual tracking of sample collection progress.
    *   *Model Training:* Automatically cleans duplicate data (preventing overfitting). Supports combining the base dataset with newly collected data or applying Incremental Learning to generate superior models.
    *   *Staging Test:* Provides a testing environment for new models (supporting batch testing) before deploying them to production.
    *   *Model History (Versioning):* Manages model states (Production, Staging, Trash). Allows restoring models from the trash or deleting them permanently.
*   **Delivered Results:** Ultimate control at a SOC Platform standard, enabling Admins to operate, collect data, and continuously Retrain AI directly via the Web Application without modifying the source code.

## Demo video

<!-- Paste your Google Drive file ID into YOUR_GOOGLE_DRIVE_FILE_ID below. Make sure the video on Drive is set to "Anyone with the link can view" -->
<iframe src="https://drive.google.com/file/d/1AKdMJN-z_w3wlmlskxMsq_m7E3x4hzEj/preview" width="100%" height="480" allow="autoplay" style="border: none;"></iframe>
