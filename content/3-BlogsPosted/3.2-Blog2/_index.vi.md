---
title: "Blog 2"
date: 2026-07-08
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Sản xuất Linh hoạt với AWS và SoftServe:

Giải pháp sản xuất linh hoạt của SoftServe tận dụng mạnh mẽ hệ sinh thái AWS để đáp ứng nhu cầu cá nhân hóa sản phẩm tự động mà không cần can thiệp cài đặt lại phần cứng. Dưới đây là các mô hình và dịch vụ cốt lõi đã làm nên thành công của hệ thống này.

Các điểm chính cần nắm:

* Tạo mẫu bằng GenAI (Design): Sử dụng Amazon Nova Canvas (qua Amazon Bedrock) để tự động sinh ra bản thiết kế từ yêu cầu văn bản của khách hàng.
* Điều phối thông minh (Orchestration): Amazon Bedrock Agents đóng vai trò là "bộ não", tự động suy luận và ra quyết định điều khiển robot mà không cần lập trình cố định (hard-code).
* Xử lý luồng tự động (Serverless): AWS Lambda tự động xử lý/đổi đuôi file ảnh; AWS Step Functions và Amazon SQS quản lý trạng thái máy và hàng đợi đơn hàng liền mạch.
* Kiểm định bằng AI (Vision QA): Mô hình ngôn ngữ hình ảnh Amazon Nova VLM tự động đối chiếu ảnh chụp thành phẩm với bản gốc để nghiệm thu chất lượng (Đạt/Lỗi).
* Kết nối IoT Đám mây - Biên (Cloud-to-Edge): AWS IoT Core kết nối đám mây với robot độ trễ thấp; AWS IoT Greengrass xử lý tại biên (edge) giúp duy trì hoạt động ngay cả khi mạng chập chờn.
* Bảo mật và Giám sát: Bảo mật giao tiếp bằng Mutual TLS và giám sát toàn bộ chỉ số hệ thống, độ trễ robot theo thời gian thực qua Amazon CloudWatch.

Sự kết hợp giữa AI, tự động hóa Serverless và IoT tại biên giúp kiến trúc AWS này đạt hiệu suất gần 100%, mở ra hướng đi mới cho việc sản xuất các lô hàng tùy biến ngắn hạn.

### Sơ đồ kiến trúc

![Sơ đồ hệ thống triển khai](diagram2.png)


### Nguồn tham khảo
Bài viết chi tiết từ Aws blog Physical-AI:[Flexible Manufacturing with AWS and SoftServe: How Simulation-First Robotics Reaches Production Faster]
https://aws.amazon.com/blogs/physical-ai/flexible-manufacturing-with-aws-and-softserve-how-simulation-first-robotics-reaches-production-faster/