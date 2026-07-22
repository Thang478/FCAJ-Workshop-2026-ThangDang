---
title: "Tạo ECR và đẩy Docker image"
date: 2026-07-22
weight: 8
chapter: false
pre: " <b> 5.3.8. </b> "
---

# Lưu hai Docker image trong Amazon ECR

Dự án có hai container độc lập nên nhóm tạo hai private repository. Việc tách repository giúp mỗi service có lịch sử tag và vòng đời image riêng.

## 1. Tạo repository cho Streamlit

Tại **Amazon ECR → Private registry → Repositories**, chọn **Create repository**:

- **Visibility:** `Private`
- **Repository name:** `malscanai-streamlit`
- **Image tag mutability:** giữ theo cấu hình nhóm sử dụng
- **Scan on push:** bật nếu phù hợp với tài khoản

![Tạo repository Streamlit](repository-streamlit.png)

## 2. Tạo repository cho URL Engine

Lặp lại thao tác với tên:

```text
malscanai-url-engine
```

![Tạo repository URL Engine](repository-url-engine.png)

![Hai repository đã tạo](repositories-created.png)

## 3. Kiểm tra image local

Trước khi push, nhóm kiểm tra image đã build:

![Docker image local](local-docker-images.png)

## 4. Đăng nhập ECR, tag và push image

Thay `<ACCOUNT_ID>` bằng AWS Account ID của môi trường triển khai:

```powershell
aws ecr get-login-password --region ap-southeast-1 |
  docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com

docker tag malscanai-streamlit:latest <ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com/malscanai-streamlit:v1
docker tag malscanai-url-engine:latest <ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com/malscanai-url-engine:v1

docker push <ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com/malscanai-streamlit:v1
docker push <ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com/malscanai-url-engine:v1
```

![Push hai image lên ECR](push-images.png)

## 5. Kiểm tra image trên ECR

Mở từng repository và kiểm tra tag `v1` đã xuất hiện.

![Streamlit image trên ECR](streamlit-image-in-ecr.png)

![URL Engine image trên ECR](url-engine-image-in-ecr.png)

Nhóm dùng tag phiên bản như `v1`, `v2`, `v3` thay vì chỉ dùng `latest`. Khi cập nhật ứng dụng, Task Definition sẽ trỏ đến tag mới, giúp quay lại phiên bản cũ dễ hơn khi deployment gặp lỗi.
