---
title: "Worklog Tuần 5"
date: 2026-06-07
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu Tuần 5:
* Nắm vững tư duy thiết kế Kiến trúc hướng sự kiện (Event-Driven Architecture) trên hạ tầng AWS.
* Xây dựng hệ thống Serverless Backend tự động hóa hoàn toàn với Amazon S3, AWS Lambda và Amazon DynamoDB.
* Thiết lập cổng kết nối API Gateway để giao tiếp an toàn giữa Web App và các dịch vụ đám mây.
* Tích hợp các phân hệ đồ án vào ứng dụng Web thống nhất, đóng gói Docker và thực hiện kiểm thử trên môi trường Container cục bộ.

### Các công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu kiến trúc hướng sự kiện (Event-Driven Architecture) thông qua video bài giảng: *Module 07-Lab39-8 - LEDA*. <br>- Hiểu cơ chế trigger bất đồng bộ giữa các dịch vụ. | 01/06/2026 | 01/06/2026 | AWS Video Series |
| 3 | - Thực hành Lab: *Serverless Backend with Lambda, S3, and DynamoDB*.<br>- Cấu hình S3 Event Notifications để tự động trigger Lambda xử lý file. | 02/06/2026 | 02/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Thực hành Lab: *Building Serverless APIs*.<br>- Khởi tạo REST API trên Amazon API Gateway, định nghĩa các Resource và Method (POST, GET, DELETE). | 03/06/2026 | 03/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Cấu hình Lambda Proxy Integration và CORS để cho phép Web App tương tác với Backend.<br>- Kiểm thử luồng API thành công qua Postman (HTTP 200 OK). | 04/06/2026 | 04/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 6 | - Đồ án nhóm: Hợp nhất các module phân tích PE và Document vào một giao diện Web App duy nhất.<br>- Triển khai luồng giao tiếp giữa Frontend và Backend thông qua API Gateway. | 05/06/2026 | 06/06/2026 | Đồ án nhóm |
| 7 | - Container hóa toàn bộ hệ thống Web App bằng Docker.<br>- Tiến hành build container, gỡ lỗi kết nối và kiểm thử tính ổn định trong môi trường cô lập. | 07/06/2026 | 07/06/2026 | Đồ án nhóm |

### Thành tựu Tuần 5:
* **Kiến trúc Serverless (Backend):** Làm chủ luồng dữ liệu tự động từ S3 trigger Lambda ghi log vào DynamoDB, hiểu rõ cơ chế vận hành không máy chủ. 

[Image of AWS Serverless architecture]

* **Cổng giao tiếp API (API Gateway):** Thiết lập hệ thống API công khai, nắm vững kỹ thuật về Proxy Integration, xử lý CORS và triển khai phiên bản (Deploy API Stage).
* **Vận hành Container (Docker):** Đóng gói thành công ứng dụng Web App phức tạp vào môi trường Docker, đảm bảo tính nhất quán giữa môi trường phát triển và kiểm thử.
* **Hệ thống hóa đồ án:** Định hình khung cấu trúc của Web App, sẵn sàng cho giai đoạn kết nối thực tế với hạ tầng AWS trong tuần tới.