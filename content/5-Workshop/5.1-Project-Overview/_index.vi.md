---
title: "Tổng quan dự án"
date: 2026-07-22
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# MalScanAI là gì?

MalScanAI là ứng dụng hỗ trợ kiểm tra tệp và URL có dấu hiệu độc hại. Giao diện chính được viết bằng Streamlit, còn phần phân tích URL được tách thành một Flask API riêng. Ở môi trường local, nhóm chạy hai dịch vụ bằng Docker Compose. Khi chuyển lên AWS, mục tiêu của nhóm là giữ cách hoạt động cũ nhưng thay phần vận hành bằng các dịch vụ managed của AWS.

Trong phạm vi workshop này, hệ thống được triển khai theo mô hình **ECS Service chạy trên Fargate**. Dữ liệu dùng chung, model và SQLite được đặt trên Amazon EFS. Docker image được lưu trong Amazon ECR. Lưu lượng từ người dùng đi qua Route 53, CloudFront và Application Load Balancer trước khi đến container Streamlit.

Một số API bên ngoài mà ứng dụng sử dụng gồm VirusTotal, MalwareBazaar, dịch vụ tra cứu vị trí IP và dịch vụ chụp ảnh website. Fargate task nằm trong private subnet nên các kết nối đi ra ngoài được chuyển qua NAT Gateway.

#### Mục tiêu triển khai

- Không mở trực tiếp container Streamlit ra Internet.
- Chỉ cho ALB gửi traffic đến ECS trên port `8501`.
- Chỉ cho ECS truy cập EFS qua NFS port `2049`.
- Lấy VirusTotal API key từ Secrets Manager thay vì ghi thẳng trong image.
- Đưa log của hai container lên CloudWatch.
- Dùng CloudFront và custom header để hạn chế truy cập thẳng vào ALB.

Đây là bản triển khai phục vụ đồ án và demo. Nhóm ưu tiên luồng dễ kiểm tra, có phân lớp mạng và hạn chế quyền truy cập giữa các thành phần.
