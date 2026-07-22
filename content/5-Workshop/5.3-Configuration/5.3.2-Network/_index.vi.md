---
title: "Cấu hình mạng"
date: 2026-07-22
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

# Cấu hình mạng cho MalScanAI

Nhóm tạo một VPC riêng để tách hệ thống MalScanAI khỏi default VPC. Kiến trúc mạng được chia thành lớp public dành cho ALB và NAT Gateway, còn ECS Fargate được đặt trong private subnet.

| Thành phần | Cấu hình |
|---|---|
| VPC | `malscanai-vpc` – `10.3.0.0/16` |
| Public subnet 1 | `10.3.1.0/24` – `ap-southeast-1a` |
| Public subnet 2 | `10.3.2.0/24` – `ap-southeast-1b` |
| Private subnet 1 | `10.3.3.0/24` – `ap-southeast-1a` |

Hai public subnet được đặt ở hai Availability Zone để ALB có thể hoạt động đúng mô hình multi-AZ. ECS task không nhận public IP; lưu lượng đi vào task phải qua ALB, còn lưu lượng đi ra Internet sẽ qua NAT Gateway.

## Trình tự thực hiện

1. [Tạo VPC và bật DNS](5.3.2.1-VPC/)
2. [Tạo các subnet](5.3.2.2-Subnets/)
3. [Tạo Internet Gateway, Elastic IP và NAT Gateway](5.3.2.3-Internet-Access/)
4. [Cấu hình public và private route table](5.3.2.4-Route-Tables/)

{{% notice note %}}
Bản triển khai của nhóm sử dụng một private subnet và một NAT Gateway để phù hợp phạm vi đồ án. Khi triển khai production, nên bổ sung private subnet và NAT Gateway theo từng Availability Zone để giảm phụ thuộc vào một vùng.
{{% /notice %}}
