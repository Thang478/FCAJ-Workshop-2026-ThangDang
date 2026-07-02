---
title: "Nhật ký công việc Tuần 8"
date: 2026-06-28
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---


### Mục tiêu Tuần 8:
* Tích hợp toàn diện các phân hệ lõi (PE Scanner, Document Scanner, URL Scanner) vào chung một cấu trúc dự án.
* Đóng gói ứng dụng lên môi trường cô lập bằng Docker và Docker Compose.
* Xử lý triệt để các sự cố xung đột thư viện (Dependency Conflicts) phát sinh khi gộp chung các mô hình Machine Learning và Deep Learning.
* Tái cấu trúc ứng dụng từ Monolithic sang Multi-container để đảm bảo tính ổn định.

### Các công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - **Tích hợp Source Code:** Tiến hành nối gộp hai phân hệ lõi của đồ án là PE Scanner (XGBoost) và URL Phishing Scanner (TensorFlow) vào chung một thư mục dự án. | 22/06/2026 | 22/06/2026 | Source code nội bộ |
| 3 | - **Kiểm thử Local & Viết Dockerfile:** Khởi tạo file `Dockerfile` và `docker-compose.yml` để đóng gói toàn bộ hệ thống nguyên khối (Monolithic). Ánh xạ volumes và port 8501. | 23/06/2026 | 23/06/2026 | Docker Documentation |
| 4 | - **Phát hiện lỗi nghiêm trọng:** Khi chạy `docker compose build`, hệ thống bị sập do tranh chấp phiên bản `numpy` giữa TensorFlow và XGBoost/SHAP.<br>- Mô hình PE không thể tải được chỉ số cấu hình (`base_score`). | 24/06/2026 | 24/06/2026 | StackOverflow / GitHub Issues |
| 5 | - **Gỡ lỗi (Debugging):** Áp dụng chiến lược "Khóa phiên bản" (Pinning Version) trong `requirements.txt`.<br>- Thử nghiệm chuyển sang sử dụng `tensorflow-cpu` để giảm thiểu dung lượng Image và rủi ro tràn RAM trên Docker. | 25/06/2026 | 25/06/2026 | TensorFlow Docs |
| 6 | - **Thay đổi Kiến trúc:** Dù đã thử nhiều cách, việc ép chung 2 framework vào một không gian nhớ vẫn không ổn định. Quyết định "đập đi xây lại", phân tách hệ thống thành các container độc lập. | 26/06/2026 | 26/06/2026 | AWS Microservices Architecture |
| 7 | - **Triển khai Multi-Container:** Tách dự án thành 2 container chạy song song:<br>&emsp;+ *Container 1 (Port 8501):* Chạy Streamlit chứa PE Scanner & Document Scanner.<br>&emsp;+ *Container 2 (Port 5000):* Chạy Flask API chuyên xử lý TensorFlow URL model. | 27/06/2026 | 28/06/2026 | Docker Compose Docs |

### Thành tựu Tuần 8:
* **Làm chủ quy trình Troubleshooting:** Nâng cao kỹ năng đọc log lỗi của trình quản lý gói (pip), phân tích nguyên nhân gốc rễ (Root-cause) của sự kiện xung đột thư viện lõi (Dependency Hell) giữa các nền tảng AI khác nhau.
* **Tư duy thiết kế hệ thống (System Design):** Thay vì cố chấp vá lỗi trên một kiến trúc nguyên khối (Monolithic) chắp vá, đã mạnh dạn áp dụng tư duy phân tán. Việc tách riêng engine xử lý URL (TensorFlow) thành một API Backend độc lập giúp triệt tiêu hoàn toàn lỗi xung đột `numpy`.
* **Container hóa thành công (Dockerization):** Hoàn thiện file `docker-compose.yml` chạy song song 2 services (Streamlit và Flask) giao tiếp mượt mà với nhau qua mạng nội bộ ảo của Docker. Sẵn sàng cho việc đẩy (push) Image lên Amazon ECR ở các tuần tiếp theo.