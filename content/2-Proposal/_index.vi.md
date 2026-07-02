---
title: "Bản đề xuất"
date: 2026-06-30
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# MalScan AI — Nền Tảng Phát Hiện Mã Độc Cộng Đồng Tích Hợp AI

---

## 1. Tóm tắt điều hành

MalScan AI là một nền tảng phát hiện mã độc hướng cộng đồng, hoạt động theo mô hình tương tự VirusTotal thu nhỏ. Hệ thống cho phép người dùng quét file thực thi PE (exe/dll), tài liệu Office (Word/Excel/PDF/HTML) và URL đáng ngờ để phát hiện mã độc bằng các mô hình Machine Learning (XGBoost, CNN). Đồng thời, hệ thống tích hợp vòng đời quản lý mô hình (MLOps) hoàn chỉnh cho phép Admin tự huấn luyện lại và triển khai mô hình mới mà không cần dừng hệ thống. Toàn bộ được triển khai trên AWS ECS Fargate với kiến trúc Container hóa, bảo vệ nhiều lớp (CloudFront + WAF + ALB) và lưu trữ bền vững qua Amazon EFS.

---

## 2. Tuyên bố vấn đề

*Vấn đề hiện tại*

Các công cụ phát hiện mã độc hiện tại thường yêu cầu cài đặt phức tạp hoặc phụ thuộc hoàn toàn vào dịch vụ đám mây bên thứ ba như VirusTotal (giới hạn rate, không có khả năng tùy chỉnh mô hình). Bên cạnh đó, các đội SOC nội bộ thiếu công cụ tích hợp để vừa phân tích mã độc vừa quản lý vòng đời mô hình AI theo thời gian.

*Giải pháp*

MalScan AI cung cấp một cổng giao tiếp duy nhất qua giao diện Streamlit web app, hỗ trợ:
- Quét PE file với 2568 đặc trưng EMBER 2024 (XGBoost + SHAP explanation)
- Quét tài liệu Office/PDF/HTML với mô hình được huấn luyện từ CIC-Trap4Phish 2025
- Quét URL với mô hình CNN 3-nhánh kết hợp OSINT (IP, WHOIS, SSL, Screenshot)
- Cơ chế Hash Cache kiểu VirusTotal: file/URL đã quét trả kết quả tức thì không chạy lại AI
- MLOps Dashboard: thu thập data → làm sạch → huấn luyện → staging test → production deploy

---

## 3. Kiến trúc giải pháp

Hệ thống triển khai theo kiến trúc Container hóa trên AWS ECS Fargate, bao gồm hai container chạy song song trong cùng một Fargate Task:

- **Container 1 (Streamlit — Port 8501)**: Giao diện người dùng, PE Scanner, Document Scanner, URL Scanner, Model Management
- **Container 2 (Flask API — Port 5000)**: Xử lý riêng TensorFlow URL model (tách biệt để tránh xung đột thư viện numpy)

![MalScan AI Architecture](/images/2-Proposal/architecture.png)

*Luồng dữ liệu chính:*

1. User gửi HTTPS Request → CloudFront (Global CDN)
2. CloudFront → AWS WAF (lọc DDoS, SQL Injection, XSS)
3. WAF → Internet Gateway → VPC
4. IGW → Application Load Balancer (Public Subnet, port 443→8501)
5. ALB → AWS Fargate Task (Private Subnet, port 8501)
6. Fargate ↔ Amazon EFS (đọc/ghi ML models + SQLite database)
7. Fargate → NAT Gateway → Internet (gọi External APIs)
8. NAT → ECR (pull Docker image qua ECR VPC Endpoint)
9. NAT → VirusTotal, MalwareBazaar, IP Geolocation, microlink.io
10. Fargate → CloudWatch VPC Endpoint → CloudWatch (logs & metrics)
11. AWS IAM ECS Task Role → cấp quyền cho Fargate

*Dịch vụ AWS sử dụng:*

| Dịch vụ | Vai trò |
|---|---|
| Amazon ECS Fargate | Chạy 2 container không cần quản lý server |
| Application Load Balancer | Điều phối traffic vào Private Subnet |
| AWS WAF + CloudFront | Bảo vệ biên, chống DDoS Layer 7 |
| Amazon ECR | Lưu trữ Docker Image |
| Amazon EFS | Lưu trữ bền vững: ML models + SQLite |
| Amazon VPC | Cô lập mạng: Public/Private Subnet, NAT Gateway, VPC Endpoints |
| Amazon CloudWatch | Thu thập log và metrics |
| AWS IAM | Kiểm soát quyền ECS Task Role |

---

## 4. Triển khai kỹ thuật

*Các giai đoạn triển khai:*

**Tháng 1 — Nghiên cứu & Phát triển Mô hình:**
- Huấn luyện PE model (XGBoost, 2568 EMBER features, Win32/Win64)
- Huấn luyện Document model (Word/Excel/PDF/HTML từ CIC-Trap4Phish 2025)
- Tích hợp URL Scanner với CNN 3-nhánh + OSINT engine
- Xây dựng Model Lifecycle Management (data collection → training → staging → production)
- Đóng gói toàn bộ thành Docker Image (2 container)

**Tháng 2 — Triển khai Hạ tầng AWS:**
- Thiết lập VPC (Public/Private Subnet, NAT Gateway, VPC Endpoints)
- Đẩy Docker Image lên Amazon ECR
- Cấu hình ECS Task Definition với EFS volume mount
- Thiết lập ALB và Target Group
- Cấu hình IAM Task Role theo nguyên tắc Least Privilege

**Tháng 3 — Bảo mật, Kiểm thử & Tài liệu:**
- Cấu hình WAF Rules và CloudFront distribution
- Kiểm thử hệ thống end-to-end (log/metric trên CloudWatch)
- Xây dựng Hash Cache database (SQLAlchemy + SQLite trên EFS)
- Triển khai hệ thống đăng ký/đăng nhập cộng đồng
- Viết Workshop report song ngữ và dọn dẹp tài nguyên

*Yêu cầu kỹ thuật:*
- **ML & App**: Python 3.12, XGBoost 3.3, TensorFlow 2.20, Streamlit, Flask, SHAP, scikit-learn
- **Cloud**: AWS VPC, ECS Fargate, ALB, WAF, CloudFront, EFS, ECR, CloudWatch, IAM
- **DevOps**: Docker, docker-compose (2 service), SQLAlchemy + SQLite

---

## 5. Lộ trình & Mốc triển khai

| Mốc | Thời gian | Kết quả |
|---|---|---|
| PE Model hoàn thiện | Tuần 2 | Accuracy >97.5%, SHAP explanation |
| Document Model hoàn thiện | Tuần 3 | 4 loại file, F1 >93% |
| URL Scanner tích hợp | Tuần 5 | CNN + OSINT + Screenshot |
| Docker build thành công | Tuần 6 | 2 container chạy ổn định |
| MLOps Dashboard | Tuần 7 | Train/Stage/Deploy hoàn chỉnh |
| AWS Infrastructure | Tuần 9 | VPC, ECS, EFS, ALB live |
| Security Layer | Tuần 10 | WAF + CloudFront active |
| Hash Cache + Auth | Tuần 11 | Community features live |
| Workshop Report | Tuần 12 | Song ngữ, đầy đủ screenshot |

---

## 6. Ước tính ngân sách

*Chi phí hạ tầng ước tính (AWS Pricing Calculator):*

| Dịch vụ | Chi phí/tháng |
|---|---|
| AWS Fargate (0.5 vCPU, 2GB RAM, 24/7) | ~$20 |
| Application Load Balancer | ~$16 |
| NAT Gateway | ~$32 |
| Amazon EFS (10GB) | ~$3 |
| AWS WAF + CloudFront | ~$5 |
| Amazon ECR (5GB) | ~$0.5 |
| **Tổng ước tính** | **~$76.5/tháng** |

*Chiến lược tối ưu chi phí:*
- ECS Task scale về 0 khi không có traffic (tiết kiệm ~$20 Fargate)
- VPC Endpoints cho ECR và CloudWatch (giảm tải NAT Gateway)
- Sử dụng AWS Budget Alert ở mức $100 để cảnh báo sớm
- Với $200 AWS credits: hệ thống có thể vận hành ổn định ~2.5 tháng

---

## 7. Đánh giá rủi ro

| Rủi ro | Mức độ ảnh hưởng | Xác suất | Chiến lược giảm thiểu |
|---|---|---|---|
| Evasion Attack vào PE model | Cao | Trung bình | Mô hình V2 chống evasion + đối chiếu VirusTotal |
| Xung đột thư viện numpy/tensorflow | Cao | Đã xảy ra | Tách 2 container độc lập (đã giải quyết) |
| Vượt ngân sách (NAT Gateway) | Trung bình | Cao | VPC Endpoints + AWS Budget Alert |
| False Positive URL Scanner | Trung bình | Trung bình | Kết hợp AI score + OSINT để đưa ra kết quả tổng hợp |
| Rò rỉ API Keys | Nghiêm trọng | Thấp | Lưu qua biến môi trường ECS, không hardcode trong Docker |
| SQLite lock trên EFS | Thấp | Thấp | connect_args timeout=30 + single Fargate task |

---

## 8. Kết quả kỳ vọng

*Kết quả kỹ thuật:*
- PE Scanner: Độ chính xác >97.5% với SHAP explanation cho từng dự đoán
- Document Scanner: F1 Score >93% trên 4 loại file (Word/Excel/PDF/HTML)
- URL Scanner: Phát hiện phishing với CNN 3-nhánh + OSINT đa nguồn
- Hash Cache: Giảm thiểu đáng kể thời gian phản hồi cho file/URL đã quét
- MLOps: Vòng đời mô hình hoàn chỉnh từ data collection đến production deploy

*Giá trị dài hạn:*
- Hệ thống cộng đồng: Càng nhiều người dùng → cache càng đầy → server càng nhẹ
- Kiến trúc có thể mở rộng: Thêm scanner mới chỉ cần thêm container/module
- Nền tảng MLOps: Admin có thể cải thiện model liên tục từ feedback thực tế
- Hướng phát triển tương lai: Tích hợp Amazon Cognito, DynamoDB, S3 cho enterprise scale