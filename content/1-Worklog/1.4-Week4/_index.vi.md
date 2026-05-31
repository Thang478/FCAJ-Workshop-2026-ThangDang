---
title: "Nhật ký công việc Tuần 4"
date: 2026-05-31
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---


### Mục tiêu Tuần 4:
* Nắm vững các cơ chế bảo mật cốt lõi và tối ưu hóa luồng dữ liệu cho kho lưu trữ Amazon S3, chuẩn bị nền tảng lưu trữ an toàn cho đồ án.
* Hiểu rõ cơ chế đóng gói ứng dụng (Containerization) với Docker thông qua việc thực hành triển khai cục bộ (Local), vượt qua giới hạn dung lượng môi trường.
* Tái cấu trúc và phát triển nâng cao đồ án "Serverless Malware Scanner": Triển khai Web App cục bộ, mở rộng mô hình phân tích tài liệu (Document Model) và xây dựng nền tảng MLOps thu nhỏ.
* Hệ thống hóa toàn bộ các mô hình học máy (PE & Document) thành một container độc lập làm phương án dự phòng.

### Các công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Hoàn thành chuỗi video lý thuyết (103 - 109) củng cố kiến thức thiết kế hệ thống AWS.<br>- Nghiên cứu lý thuyết về kiến trúc Containerization, hình dung sự khác biệt giữa cấu trúc máy chủ ảo truyền thống và Container. | 25/05/2026 | 25/05/2026 | AWS Video Series |
| 3 | - Thực hành cấu hình bảo mật chuyên sâu cho Amazon S3 (Lab: S3 Security Best Practices).<br>- Thiết lập S3 Bucket Policy ép buộc mã hóa dữ liệu (SSE-S3) và giao thức HTTPS.<br>- Kích hoạt Block Public Access (BPA) để ngăn chặn truy cập dữ liệu trái phép. | 26/05/2026 | 26/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Tích hợp S3 VPC Endpoint để định tuyến truy cập nội bộ (private network) an toàn và tối ưu.<br>- Hoàn tất cài đặt Docker Desktop trên môi trường phát triển cục bộ (Local). | 27/05/2026 | 27/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Thực hành Lab: Đóng gói ứng dụng web với Docker.<br>- Xây dựng kịch bản `Dockerfile`, thực thi quy trình đóng gói (`docker build`) và khởi chạy (`docker run`) trực tiếp trên Local để tối ưu chi phí.<br>- Đăng nhập và đẩy (push) thành công Docker Image lên kho lưu trữ đám mây Docker Hub. | 28/05/2026 | 28/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - Quay lại phát triển đồ án nhóm: Xây dựng hoàn thiện Document Model hỗ trợ xử lý Word, Excel, PDF, HTML.<br>- Triển khai thành công tính năng tải lên hàng loạt (Batch Upload) đa luồng trên giao diện Web App.<br>- Đóng gói thành công PE Model (XGBoost, 2568 features, tích hợp SHAP/Defender) thành một Docker Container độc lập chạy ổn định trên Local. | 29/05/2026 | 29/05/2026 | Đồ án nhóm |
| 7 | - Phát triển tính năng MLOps (Continuous Training): Thiết lập hệ thống tự động đối chiếu dự đoán của Document Model với API VirusTotal.<br>- Tự động trích xuất các file bị dự đoán sai vào cơ sở dữ liệu SQLite cục bộ (Data Collection).<br>- Lập trình kịch bản tự động huấn luyện (Auto-train) khi dữ liệu đạt ngưỡng, kèm tính năng A/B Testing, quản lý vòng đời mô hình (Model Registry) và sao lưu dự phòng. | 30/05/2026 | 31/05/2026 | Đồ án nhóm |

### Thành tựu Tuần 4:
* **Tư duy Bảo mật Đám mây (S3):** Hiểu rõ cách triển khai mô hình bảo mật nhiều lớp cho kho lưu trữ dữ liệu thông qua cơ chế Policy, mã hóa và định tuyến nội bộ.
* **Kiến trúc Container (Docker):** Nắm bắt thành thạo quy trình tự động hóa môi trường triển khai bằng Docker, sẵn sàng khắc phục các rào cản về dung lượng khi đưa dự án lên hạ tầng đám mây.
* **Kiến trúc ML & Pipeline Dữ liệu:** Hoàn thiện vòng lặp MLOps thu nhỏ từ khâu thu thập dữ liệu tự động, đánh giá chéo qua Ground Truth (VirusTotal), đến khả năng kích hoạt tái huấn luyện (Retrain) thông minh.
* **Dự phòng rủi ro:** Đóng gói thành công toàn bộ hệ thống PE và Document Models thành phiên bản Container cục bộ, bảo đảm tính liên tục và sẵn sàng triển khai của dự án.