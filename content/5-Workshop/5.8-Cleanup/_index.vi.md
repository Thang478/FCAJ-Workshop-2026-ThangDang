---
title: "Dọn dẹp tài nguyên AWS"
date: 2026-07-24
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

# Clean-up sau khi hoàn thành workshop

Các tài nguyên Fargate, NAT Gateway và Application Load Balancer tạo phần lớn chi phí cố định theo tháng. Vì vậy, sau khi hoàn tất demo và lưu đủ bằng chứng, nhóm cần xóa tài nguyên theo thứ tự phụ thuộc bên dưới.

{{% notice danger %}}
Xóa Amazon EFS sẽ xóa vĩnh viễn database, tài khoản, lịch sử và dữ liệu ứng dụng trong `/app/data`. Hãy sao lưu dữ liệu cần giữ trước khi tiếp tục.
{{% /notice %}}

## 1. Chuẩn bị trước khi xóa

- Tải xuống hoặc sao lưu dữ liệu cần giữ từ `/app/data`, đặc biệt là `malscan.db`.
- Lưu video demo, ảnh cấu hình, ảnh testing và bản AWS Pricing Calculator.
- Kiểm tra tài nguyên có đang được dùng bởi project khác hay không.
- Ghi lại domain, resource name và ARN cần cho báo cáo.

## 2. Gỡ bản ghi truy cập ứng dụng

Tại **Route 53 → Hosted zones**, mở hosted zone đang quản lý tên miền và xóa riêng record của:

```text
malscanai.sadc.io.vn
```

Không xóa toàn bộ hosted zone `sadc.io.vn` nếu còn subdomain hoặc hệ thống khác sử dụng.

## 3. Xóa AWS User Notifications và CloudWatch Alarm

1. Vào **AWS User Notifications → Notification configurations**.
2. Xóa configuration `malscanai-alarm-email` và delivery channel không còn dùng.
3. Vào **CloudWatch → Alarms**.
4. Chọn `malscanai-unhealthy-target-alarm` và chọn **Delete**.

Alarm và notification không phải khoản chi phí chính, nhưng xóa chúng giúp môi trường không còn gửi sự kiện từ tài nguyên cũ.

## 4. Disable và xóa CloudFront Distribution

1. Vào **CloudFront → Distributions → malscanai-cloudfront**.
2. Chọn **Disable**.
3. Chờ trạng thái thay đổi được deploy hoàn tất.
4. Chọn distribution và **Delete**.
5. Kiểm tra Flat-Rate Plan không còn gắn với distribution đã xóa.

CloudFront yêu cầu distribution được disable trước khi xóa.

## 5. Xóa ECS Service

1. Vào **ECS → Clusters → malscanai-cluster → Services**.
2. Chọn `malscanai-service`.
3. Chọn **Delete service** và xác nhận force delete nếu Console yêu cầu.
4. Chờ task chuyển sang `Stopped` và network interface của task được giải phóng.

Có thể giảm desired count về `0` trước để quan sát task dừng, nhưng xóa service bằng Console cũng dừng các task thuộc service.

## 6. Xóa Application Load Balancer và Target Group

Sau khi ECS Service không còn target đang chạy:

1. Vào **EC2 → Load Balancers** và xóa `malscanai-alb`.
2. Chờ Load Balancer bị xóa.
3. Vào **EC2 → Target Groups** và xóa `malscanai-streamlit-tg`.

ALB là tài nguyên tính phí theo giờ, nên cần ưu tiên xóa ngay sau ECS Service.

## 7. Xóa ECS Cluster và Task Definition cũ

1. Vào **ECS → Clusters** và xóa cluster khi không còn service hoặc task.
2. Vào **ECS → Task definitions → malscanai-task**.
3. Deregister các revision không còn cần thiết.

Task Definition không tạo chi phí khi chỉ được lưu, nhưng dọn revision giúp tránh triển khai nhầm phiên bản cũ.

## 8. Xóa EFS

1. Xác nhận không còn ECS task đang mount EFS.
2. Vào **EFS → Access points** và xóa `malscanai-data-ap`.
3. Mở file system `malscanai-efs` và kiểm tra các mount target.
4. Xóa mount target hoặc dùng thao tác xóa file system trên Console để Console xử lý các mount target liên quan.
5. Xóa file system và xác nhận đúng file system ID.

Không thể xóa EFS khi mount target hoặc tài nguyên phụ thuộc vẫn còn hoạt động.

## 9. Xóa ECR images và repositories

Vào **ECR → Private repositories** và xử lý hai repository:

```text
malscanai-streamlit
malscanai-url-engine
```

- Xóa các image tag không còn cần thiết.
- Chọn **Delete repository** và chọn force deletion nếu repository vẫn còn image.

Nếu muốn giữ khả năng phục hồi hệ thống, có thể giữ image cần thiết và chỉ xóa các tag cũ. ECR tiếp tục tính phí theo dung lượng còn lưu.

## 10. Xóa Secrets Manager secret

1. Vào **Secrets Manager → Secrets**.
2. Chọn `malscanai/virustotal-api-key`.
3. Chọn **Delete secret**.
4. Đặt recovery window phù hợp và xác nhận schedule deletion.

Không ghi secret value vào báo cáo hoặc ảnh clean-up.

## 11. Xóa CloudWatch Logs

1. Vào **CloudWatch → Log groups**.
2. Chọn `/ecs/malscanai`.
3. Xóa Log Group sau khi đã lưu các log cần cho báo cáo.

Nếu chưa muốn xóa ngay, đặt retention 7 ngày để log tự hết hạn thay vì giữ vô thời hạn.

## 12. Xóa NAT Gateway và giải phóng Elastic IP

1. Vào **VPC → NAT gateways**.
2. Chọn NAT Gateway của MalScanAI và chọn **Delete NAT gateway**.
3. Chờ trạng thái chuyển sang `Deleted`.
4. Vào **EC2 → Elastic IP addresses**.
5. Chọn Elastic IP đã dùng cho NAT Gateway và chọn **Release Elastic IP address**.

{{% notice warning %}}
Xóa NAT Gateway chỉ disassociate Elastic IP; địa chỉ không tự được release. Nếu quên release, Public IPv4 vẫn có thể tiếp tục phát sinh phí.
{{% /notice %}}

## 13. Xóa các tài nguyên mạng còn lại

Sau khi ALB, ECS task, EFS mount target và NAT Gateway đã được xóa:

1. Xóa các route tùy chỉnh trỏ đến NAT Gateway nếu còn tồn tại.
2. Xóa custom route tables và subnet associations.
3. Xóa private subnet và public subnet.
4. Xóa các Security Group của ALB, ECS và EFS.
5. Detach Internet Gateway khỏi VPC rồi xóa Internet Gateway.
6. Xóa `malscanai-vpc`.

Nếu Security Group hoặc subnet chưa xóa được, kiểm tra network interface còn sót từ ALB, ECS, EFS hoặc NAT Gateway.

## 14. Xử lý ACM và Route 53

- ACM public certificate không phát sinh phí riêng, nhưng có thể xóa nếu certificate chỉ dành cho MalScanAI và không còn được CloudFront sử dụng.
- Chỉ xóa hosted zone khi toàn bộ domain không còn được sử dụng. Đối với domain dùng chung, chỉ xóa record của MalScanAI.

## 15. Kiểm tra cuối cùng

Kiểm tra các trang sau sau khi clean-up:

- **Billing and Cost Management → Cost Explorer**
- **EC2 → Elastic IP addresses**
- **VPC → NAT gateways**
- **EC2 → Load Balancers**
- **ECS → Clusters**
- **EFS → File systems**
- **ECR → Repositories**
- **CloudWatch → Log groups**

Bảng xác nhận:

| Tài nguyên | Trạng thái sau clean-up |
|---|---|
| ECS Service và task | Đã xóa hoặc `Stopped` |
| ALB và Target Group | Không còn |
| NAT Gateway | `Deleted` |
| Elastic IP | Đã release |
| EFS | Đã xóa sau khi backup |
| ECR | Đã xóa hoặc chỉ giữ image chủ động |
| CloudWatch Log Group | Đã xóa hoặc retention ngắn |
| Secret | Đã schedule deletion |
| Route 53 record | Record MalScanAI đã xóa |

{{% notice note %}}
Billing và Cost Explorer có thể cập nhật chậm. Sau khi xóa tài nguyên, tiếp tục kiểm tra chi phí trong những ngày tiếp theo để chắc chắn không còn tài nguyên tính phí ngoài dự kiến.
{{% /notice %}}
