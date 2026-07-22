---
title: "Cấu hình Route Table"
date: 2026-07-22
weight: 4
chapter: false
pre: " <b> 5.3.2.4. </b> "
---

# Phân luồng public và private bằng Route Table

Nhóm tạo hai route table riêng. Public route table đưa lưu lượng ra Internet Gateway, còn private route table đưa lưu lượng đi ra NAT Gateway.

## 1. Tạo Public Route Table

Tại **VPC → Route tables**, chọn **Create route table** và nhập:

- **Name:** `malscan-public-rt`
- **VPC:** `malscanai-vpc`

![Tạo Public Route Table](public-route-table-create.png)

Mở tab **Subnet associations → Edit subnet associations**, chọn:

- `malscanai-subnet-public-1`
- `malscanai-subnet-public-2`

![Gắn hai public subnet](public-subnet-associations.png)

Trong tab **Routes**, chọn **Edit routes → Add route**:

```text
Destination: 0.0.0.0/0
Target: Internet Gateway – malscanai-igw
```

![Thêm default route đến Internet Gateway](public-default-route.png)

![Public Route Table hoàn tất](public-route-table-complete.png)

Route này làm cho hai subnet có đường trực tiếp đến Internet Gateway, phù hợp với ALB và NAT Gateway nằm ở lớp public.

## 2. Tạo Private Route Table

Tạo route table thứ hai:

- **Name:** `malscan-private-rt`
- **VPC:** `malscanai-vpc`

![Tạo Private Route Table](private-route-table-create.png)

Trong **Subnet associations**, chỉ chọn `malscanai-subnet-private-1`.

![Gắn private subnet](private-subnet-association.png)

Thêm default route:

```text
Destination: 0.0.0.0/0
Target: NAT Gateway – malscanai-nat-gateway
```

![Thêm route đến NAT Gateway](private-default-route.png)

![Private Route Table hoàn tất](private-route-table-complete.png)

Sau cấu hình này, ECS task trong private subnet có thể mở kết nối đi ra ngoài nhưng không có đường từ Internet đi trực tiếp vào task. Lưu lượng người dùng phải đi theo hướng CloudFront → ALB → ECS.
