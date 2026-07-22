---
title: "Tạo ECS Service"
date: 2026-07-22
weight: 13
chapter: false
pre: " <b> 5.3.13. </b> "
---

# Chạy Task Definition dưới dạng ECS Service

ECS Service giữ số lượng task theo cấu hình, thay task bị lỗi và đăng ký task vào Target Group.

## 1. Bắt đầu tạo Service

Mở cluster `malscanai-cluster` và chọn **Create service**.

![Bắt đầu tạo ECS Service](service-start.png)

## 2. Chọn Task Definition và số lượng task

Cấu hình:

- **Compute options:** Launch type
- **Launch type:** `Fargate`
- **Task definition family:** `malscanai-task`
- **Revision:** revision mới nhất đã kiểm tra
- **Service name:** `malscanai-service`
- **Desired tasks:** `1`

![Cấu hình cơ bản của Service](service-basic.png)

Nhóm dùng một task để phù hợp môi trường đồ án. ECS Service vẫn có khả năng tạo lại task nếu task hiện tại dừng.

## 3. Cấu hình deployment

Giữ rolling deployment để khi cập nhật revision, ECS tạo task mới và chuyển traffic trước khi dừng task cũ trong giới hạn cấu hình.

![Cấu hình deployment](service-deployment.png)

## 4. Cấu hình network cho task

Chọn:

- **VPC:** `malscanai-vpc`
- **Subnet:** `malscanai-subnet-private-1`
- **Security Group:** `malscanai-ecs-sg`
- **Public IP:** `Turned off`

![Network của ECS Service](ervice-network.png)

Task nằm trong private subnet và không nhận public IP. Lưu lượng vào task chỉ được phép từ ALB trên port `8501`; lưu lượng đi ra ngoài sử dụng NAT Gateway.

## 5. Gắn ALB và Target Group

Ở phần Load balancing:

- **Load balancer type:** Application Load Balancer
- **Container:** `malscanai-streamlit:8501`
- **Listener:** listener của `malscanai-alb`
- **Target Group:** `malscanai-streamlit-tg`

![Gắn ALB và Target Group](service-load-balancer.png)

Chỉ container Streamlit được gắn vào Target Group. URL Engine tiếp tục là backend nội bộ trong task.

## 6. Review và tạo Service

Kiểm tra Task Definition revision, subnet, Security Group và Target Group, sau đó chọn **Create service**.

![Review ECS Service](service-review.png)

![ECS Service đã tạo](service-created.png)

Sau vài phút, task chuyển sang `Running` và target chuyển sang `Healthy`.

![Target ở trạng thái Healthy](target-healthy.png)

Nếu target `Unhealthy`, nhóm kiểm tra lần lượt: CloudWatch log, health check path, port `8501`, inbound rule của ECS Security Group và lỗi mount EFS.
