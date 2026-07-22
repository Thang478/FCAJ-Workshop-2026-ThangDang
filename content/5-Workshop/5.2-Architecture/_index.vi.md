---
title: "Kiến trúc triển khai"
date: 2026-07-22
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# Kiến trúc MalScanAI trên AWS

![Kiến trúc MalScanAI](malscanai-architecture.jpg)

Nhóm chia luồng thành hai phần: đường đi của request người dùng và các kết nối phục vụ vận hành container.

#### Luồng truy cập chính

1. Người dùng truy cập `https://malscanai.sadc.io.vn`.
2. Route 53 phân giải tên miền đến CloudFront.
3. CloudFront nhận request HTTPS, áp dụng lớp bảo vệ WAF và chuyển request hợp lệ đến ALB.
4. ALB nằm ở public subnet, nhận traffic và forward đến port `8501` của ECS task.
5. Container Streamlit gọi container URL Engine qua `http://127.0.0.1:5000/api/analyze`.

#### Luồng dữ liệu và vận hành

- ECS kéo hai Docker image từ ECR khi task khởi động.
- VirusTotal API key được lấy từ Secrets Manager thông qua task execution role.
- EFS được mount vào `/app/data` để hai container dùng chung model, dữ liệu và SQLite.
- Log của container được gửi đến CloudWatch Logs.
- Request đến các API bên ngoài đi từ private subnet qua NAT Gateway rồi ra Internet Gateway.

{{% notice note %}}
Sơ đồ có thể hiện ECR Endpoint và CloudWatch Endpoint như hướng tăng cường kết nối riêng tư. Bộ ảnh cấu hình của workshop này bám theo môi trường nhóm đã dựng, trong đó private subnet vẫn có đường outbound qua NAT Gateway. Vì vậy, workshop không tách thêm một bước tạo hai endpoint này.
{{% /notice %}}

Điểm nhóm chú ý nhất là ALB không phải địa chỉ truy cập chính. CloudFront gửi thêm một custom header, còn listener của ALB chỉ forward khi header đúng. Request đi thẳng đến DNS của ALB sẽ nhận fixed response `403`.
