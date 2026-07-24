---
title: "Workshop"
date: 2026-07-22
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai MalScanAI trên AWS bằng ECS Fargate

#### Nhóm mình làm gì trong workshop này?

MalScanAI ban đầu chạy trên máy cá nhân bằng Docker Compose. Khi đưa hệ thống lên AWS, nhóm mình giữ nguyên cách tách ứng dụng thành hai container: một container chạy giao diện **Streamlit** và một container chạy **URL Engine**. Hai container được đặt chung trong một ECS Fargate Task để có thể gọi nhau qua địa chỉ `127.0.0.1`.

Workshop này ghi lại đúng quá trình nhóm đã cấu hình trên AWS Console. Nội dung workshop được chia thành chín phần:

1. [Tổng quan dự án](5.1-Project-Overview/)
2. [Kiến trúc triển khai](5.2-Architecture/)
3. [Các bước cấu hình](5.3-Configuration/)
4. [Kiểm thử và xác thực](5.4-Testing-and-Validation/)
5. [Giám sát và cảnh báo](5.5-Monitoring-and-Alerts/)
6. [Chi phí và tối ưu](5.6-Cost-and-Optimization/)
7. [Bảo mật và giới hạn](5.7-Security-and-Limitations/)
8. [Dọn dẹp](5.8-Cleanup/)
9. [Kết quả và video demo](5.9-Results/)

Sau mỗi bước cấu hình, ảnh cuối phần cho thấy tài nguyên đã được tạo hoặc chuyển sang trạng thái như `Available`, `Active`, `Running`, `Healthy`, `Issued` hay `Deployed`. Phần cuối workshop được dành riêng cho video demo hoạt động của hệ thống sau khi triển khai.

{{% notice note %}}
Tên miền, ID tài nguyên và một số giá trị trong ảnh thuộc môi trường nhóm đã dựng. Khi làm lại, bạn nên dùng tên tài nguyên của riêng mình và không sao chép các giá trị bí mật.
{{% /notice %}}

📺 [Click here to watch the MalScanAI Demo Video](https://drive.google.com/file/d/1H0fn-DJBwUtcIOCNBVlZHzQekS9tQYFk/view?usp=drivesdk)