---
title: "Week 2 Worklog"
date: 2026-05-17
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu Tuần 2 (Week 2 Objectives)

* **Lý thuyết:** Tiếp cận kiến thức nền tảng vững chắc về mạng trong điện toán đám mây thông qua dịch vụ Amazon Virtual Private Cloud (VPC).
* **Thực hành:** Triển khai thực tế mô hình kết nối bảo mật AWS Site-to-Site VPN, kết nối an toàn giữa hai vùng mạng độc lập.
* **Kỹ năng nâng cao:** Rèn luyện tư duy phân tích log và xử lý sự cố (Troubleshooting) hệ thống mạng thực tế trên hệ điều hành đời mới.

---

### Các công việc đã thực hiện (Tasks Carried Out)

| Giai đoạn | Nội dung chi tiết công việc thực hiện | Trạng thái | Tư liệu tham khảo |
| :--- | :--- | :--- | :--- |
| **Nghiên cứu & Học tập** | - Xem chuỗi video hướng dẫn AWS (2025 - 2026) từ cơ bản đến phần VPC Lab 2-1.<br>- Nghiên cứu lý thuyết cốt lõi: Subnets, Route Tables, Internet Gateway (IGW), NAT Gateway, Security Groups (SG), và Network ACLs (NACLs). | **Hoàn thành** | AWS Study Group - Blog / Youtube |
| **Thực hành Căn bản** | - Thực hiện bài Lab: **Kiến thức cơ bản về mạng với Amazon Virtual Private Cloud (VPC)**.<br>- Tự tay cấu hình phân đoạn mạng đa tầng (Public Subnet cho máy chủ ngoại mạng, Private Subnet cho cơ sở dữ liệu nội bộ). | **Hoàn thành** | AWS Study Group - Workshop |
| **Thực hành Nâng cao** | - Triển khai kiến trúc **AWS Site-to-Site VPN** kết nối mạng Main office (VPC ASG) và Branch office (VPC ASG VPN).<br>- Khởi tạo Virtual Private Gateway (VGW), Customer Gateway (CGW) và thiết lập cấu hình định tuyến Static Routing. | **Hoàn thành** | AWS Study Group - Workshop |
| **Xử lý sự cố (Troubleshooting)** | - Di cư cấu hình từ OpenSwan cũ sang **Libreswan** để tương thích với hệ điều hành **Amazon Linux 2023**.<br>- Tiến hành fix liên hoàn lỗi cú pháp file cấu hình, lỗi thụt lề, lỗi ký tự ẩn Windows (`CRLF`) bằng công cụ `dos2unix`. | **Hoàn thành** | AWS Health / Kỹ sư hỗ trợ |
| **Dọn dẹp & Tối ưu** | - Thực hiện quy trình phá hủy và giải phóng tài nguyên (Resource Clean-up) nghiêm ngặt để tránh phát sinh chi phí ngầm (Terminate EC2, Release Elastic IP, Delete NAT Gateway, Clear CloudWatch Flow Logs & Reachability Analyzer). | **Hoàn thành** | AWS Console |

---

### Kết quả đạt được (Week 2 Achievements)

* **Xây dựng hệ thống mạng hoàn chỉnh:** Làm chủ giao diện và cách thức liên kết các thành phần mạng trong VPC. Hiểu rõ cơ chế hoạt động phối hợp giữa Tường lửa cấp Subnet (NACL - Stateless) và Tường lửa cấp Instance (Security Group - Stateful).
* **Đào thông đường hầm VPN:** Vượt qua chốt chặn cấu hình phức tạp để đưa trạng thái hệ thống từ `Loaded 0` lên **`Total IPsec connections: loaded 2`**. 
* **Kết nối nội bộ thành công:** Thực hiện lệnh `ping` kiểm tra gói tin chạy thông suốt giữa máy chủ Private và Customer Gateway bằng IP nội bộ thông qua đường hầm mã hóa IPsec bảo mật.
* **Xử lý sự cố thực tế:** Thành thạo các câu lệnh quản trị mạng nâng cao trên Linux để kiểm tra và ép hệ thống nạp cấu hình như:
  ```bash
  sudo systemctl status ipsec
  sudo ipsec status
  sudo dos2unix /etc/ipsec.d/aws.conf
