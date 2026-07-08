---
title: "Worklog Tuần 7"
date: 2026-06-21
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu Tuần 7:
* Triển khai hệ thống xác thực người dùng an toàn thông qua Amazon Cognito (User Pools & Identity Pools).
* Làm chủ kỹ năng giám sát hệ thống Serverless bằng Amazon CloudWatch và phân tích hiệu năng/điểm nghẽn bằng AWS X-Ray.
* Chuẩn hóa các chính sách phân quyền IAM cho môi trường Docker MLOps.
* Hoàn thiện sơ đồ kiến trúc hệ thống (Architecture Diagram) cho nền tảng SOC Malware.

### Các công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu lý thuyết quản lý định danh: Phân tích luồng JWT Token, cấu hình User Pool và cơ chế xác thực OAuth 2.0. | 15/06/2026 | 15/06/2026 | AWS Documentation |
| 3 | - Thực hành Lab: *Xác thực người dùng với Amazon Cognito*.<br>- Khởi tạo User Pool, thiết lập chính sách mật khẩu mạnh và ánh xạ credential API (`ClientID`, `ClientSecret`). | 16/06/2026 | 16/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Thực hành Lab: *Giám sát ứng dụng Serverless (CloudWatch & X-Ray)*.<br>- Cấu hình log cho Lambda, tạo Custom Metrics và thiết lập CloudWatch Alarms tích hợp SNS để cảnh báo lỗi. | 17/06/2026 | 17/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Thực hành Lab: *AWS X-Ray*.<br>- Tích hợp thư viện `aws_xray_sdk` vào Lambda, thiết lập Service Map và phân tích các điểm nghẽn độ trễ khi thực thi hàm. | 18/06/2026 | 18/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 6 | - Đồ án nhóm: Thắt chặt chính sách phân quyền IAM. Tối ưu hóa các chính sách theo nguyên tắc đặc quyền tối thiểu cho Docker containers. | 19/06/2026 | 20/06/2026 | Đồ án nhóm |
| 7 | - Đồ án nhóm: Thiết kế kiến trúc. Liên tục tinh chỉnh sơ đồ kiến trúc hệ thống trên Draw.io để đạt chuẩn hóa thiết kế đám mây. | 21/06/2026 | 21/06/2026 | Đồ án nhóm |

### Thành tựu Tuần 7:
* **Quản lý Định danh (Amazon Cognito):** Xây dựng thành công luồng xác thực an toàn, bảo vệ các API endpoint và quản lý phiên người dùng hiệu quả.
* **Giám sát & Gỡ lỗi Serverless:** Có khả năng thực hiện phân tích nguyên nhân gốc rễ (Root-cause analysis) trong hệ thống phân tán. Thành thạo việc tạo cảnh báo tự động qua Email (SNS) và sử dụng X-Ray Service Map để phát hiện các điểm nghẽn hiệu năng.
* **Thiết kế Kiến trúc:** Xây dựng bản đồ luồng dữ liệu phức tạp cho nền tảng SOC, đảm bảo kiến trúc có khả năng mở rộng và bảo mật cao trước khi triển khai trên Cloud.
* **Bảo mật DevOps:** Cấu trúc lại các IAM Roles và chính sách bảo mật, đảm bảo nền tảng MLOps dựa trên Docker hoạt động đúng nguyên tắc đặc quyền tối thiểu (Least Privilege).