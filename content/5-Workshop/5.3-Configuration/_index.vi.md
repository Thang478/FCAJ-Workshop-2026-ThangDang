---
title: "Cấu hình hệ thống"
date: 2026-07-22
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

# Trình tự cấu hình MalScanAI

Nhóm triển khai theo thứ tự từ lớp mạng đến lớp ứng dụng. Mỗi phần trình bày thông số đã sử dụng, thao tác trên AWS Console và lý do nhóm chọn cấu hình đó. Ảnh ở cuối từng bước dùng để xác nhận tài nguyên đã được tạo hoặc lưu cấu hình thành công, không phải một chương kết quả riêng.

1. [Chuẩn bị môi trường](5.3.1-Preparation/)
2. [Cấu hình mạng](5.3.2-Network/)
3. [Tạo Security Group](5.3.3-Security-Groups/)
4. [Lưu VirusTotal API key](5.3.4-Secrets-Manager/)
5. [Tạo IAM Role](5.3.5-IAM-Roles/)
6. [Tạo Amazon EFS](5.3.6-EFS/)
7. [Tạo CloudWatch Log Group](5.3.7-CloudWatch/)
8. [Tạo ECR và đẩy image](5.3.8-ECR/)
9. [Tạo ECS Cluster](5.3.9-ECS-Cluster/)
10. [Tạo ECS Task Definition](5.3.10-Task-Definition/)
11. [Tạo Target Group](5.3.11-Target-Group/)
12. [Tạo Application Load Balancer](5.3.12-ALB/)
13. [Tạo ECS Service](5.3.13-ECS-Service/)
14. [Cấu hình Route 53](5.3.14-Route53/)
15. [Tạo chứng chỉ ACM](5.3.15-ACM/)
16. [Tạo CloudFront Distribution](5.3.16-CloudFront/)
17. [Hạn chế truy cập trực tiếp ALB](5.3.17-Protect-ALB/)

{{% notice warning %}}
NAT Gateway, EFS, ALB, Fargate, CloudFront và WAF có thể phát sinh chi phí. Nhóm cần kiểm tra Billing và xóa tài nguyên không còn dùng sau buổi demo.
{{% /notice %}}
