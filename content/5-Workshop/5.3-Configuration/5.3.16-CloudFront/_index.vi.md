---
title: "Tạo CloudFront Distribution"
date: 2026-07-22
weight: 16
chapter: false
pre: " <b> 5.3.16. </b> "
---

# Đặt CloudFront và WAF phía trước ALB

CloudFront là điểm truy cập public của MalScanAI. Người dùng kết nối HTTPS đến CloudFront, sau đó CloudFront chuyển request hợp lệ về ALB.

## 1. Bắt đầu tạo Distribution

Tại **CloudFront → Distributions**, chọn **Create distribution**. Nếu giao diện hiển thị lựa chọn plan, nhóm chọn gói phù hợp môi trường demo và không bật tính năng trả phí chưa cần dùng.

![Chọn CloudFront plan](cloudfront-plan.png)

![Bắt đầu tạo Distribution](cloudfront-start.png)

## 2. Chọn ALB làm Origin

Ở phần Origin:

- **Origin domain:** DNS của `malscanai-alb`
- **Origin type:** Custom origin / ALB
- **Origin protocol:** HTTP theo cấu hình hiện tại

![Chọn ALB làm Origin](cloudfront-origin.png)

CloudFront không gọi trực tiếp ECS task. ALB tiếp tục chịu trách nhiệm health check và phân phối request đến target đang Healthy.

## 3. Cấu hình Cache Behavior

Streamlit là ứng dụng động nên nhóm không dùng cache như website tĩnh. Cấu hình chính gồm:

- **Viewer protocol policy:** Redirect HTTP to HTTPS
- **Allowed methods:** cho phép các method ứng dụng cần
- Chuyển tiếp cookie, query string và header cần thiết cho phiên Streamlit

![Cấu hình Cache Behavior](cloudfront-settings.png)

![Allowed HTTP methods](cloudfront-methods.png)

Nếu cache HTML hoặc session không đúng, người dùng có thể nhận nội dung cũ hoặc WebSocket hoạt động không ổn định. Vì vậy nhóm ưu tiên behavior dành cho ứng dụng động.

## 4. Cấu hình WAF

Tại phần bảo vệ, nhóm giữ lớp WAF phù hợp với gói đang chọn và không thêm rule nâng cao ngoài phạm vi đồ án.

![Cấu hình WAF](cloudfront-waf.png)

WAF giúp lọc request trước khi traffic đến ALB. Phần chặn truy cập trực tiếp ALB ở bước sau giúp người dùng không dễ bỏ qua lớp này.

## 5. Review và tạo Distribution

Kiểm tra Origin, behavior và WAF, sau đó chọn **Create distribution**.

![Review CloudFront](cloudfront-review.png)

![CloudFront Distribution đã tạo](cloudfront-created.png)

## 6. Gắn domain và certificate

Thêm alternate domain name:

```text
malscanai.sadc.io.vn
```

![Thêm Alternate Domain Name](alternate-domain.png)

Chọn certificate ACM đã `Issued` trong `us-east-1`.

![Chọn ACM certificate](certificate-selected.png)

## 7. Tạo Alias Record trong Route 53

Khi Distribution đã `Deployed`, quay lại Route 53 và tạo Alias A record:

```text
Record name: malscanai
Route traffic to: CloudFront Distribution
```

![Tạo Alias đến CloudFront](route53-alias.png)

Domain `malscanai.sadc.io.vn` lúc này phân giải đến CloudFront thay vì trỏ thẳng vào ALB.
