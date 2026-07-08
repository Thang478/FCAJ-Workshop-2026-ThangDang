---
title: "Worklog Tuần 9"
date: 2026-07-05
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu Tuần 9:
* Phát triển phân hệ Quản lý tài khoản (Authentication) và Phân quyền truy cập (Role-Based Access Control - RBAC).
* Cấu hình phân lập dữ liệu (Data Segregation) đảm bảo tính riêng tư tuyệt đối cho lịch sử và bộ nhớ đệm (cache) của từng người dùng.
* Xây dựng Bảng điều khiển quản trị (Admin Dashboard) với các biểu đồ thống kê trực quan.
* Đóng gói, chuẩn hóa tài liệu kỹ thuật và bàn giao mã nguồn cho nhóm phụ trách triển khai hạ tầng Cloud.
* Tái cấu trúc và hoàn thiện sơ đồ kiến trúc hạ tầng tổng thể (Architecture Topology).

### Các công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - **Phát triển Auth & Phân lập dữ liệu (Data Segregation):** Code chức năng Đăng ký/Đăng nhập. Thiết lập logic định tuyến cơ sở dữ liệu để cô lập hoàn toàn lịch sử quét (URL, Document, file PE) và bộ nhớ tạm (cache) của mỗi user, đảm bảo các user không thể nhìn thấy dữ liệu của nhau. | 29/06/2026 | 29/06/2026 | Web Authentication Best Practices, Data Isolation |
| 3 | - **Xây dựng Admin Dashboard:** Thiết kế phân hệ dành riêng cho quản trị viên (Admin). Bổ sung đặc quyền cho phép Admin xem được dữ liệu tổng thể của toàn hệ thống và tích hợp các thư viện vẽ biểu đồ trực quan (Statistical Charts) để thống kê lưu lượng sử dụng và kết quả phân tích mã độc. | 30/06/2026 | 30/06/2026 | Data Visualization, RBAC Models |
| 4 | - **Fix Bug & Tối ưu bảo mật:** Phát hiện và xử lý các lỗi logic liên quan đến kiểm tra mật khẩu, băm mật khẩu (Password Hashing) và vá lỗ hổng rò rỉ phiên làm việc (Session Leakage) khi chuyển đổi qua lại giữa tài khoản User và Admin. | 01/07/2026 | 01/07/2026 | OWASP Authentication Cheat Sheet |
| 5 | - **Kiểm thử Tích hợp trên Docker:** Khởi chạy lại hệ thống Multi-container bằng `docker-compose`. Thực hiện các kịch bản test đăng nhập nhiều luồng, truy vấn dữ liệu chéo để đảm bảo cơ chế phân quyền hoạt động ổn định và không xảy ra xung đột bộ nhớ. | 02/07/2026 | 02/07/2026 | Docker Compose Workflow |
| 6 | - **Đóng gói & Bàn giao Source Code:** Chuẩn hóa cấu trúc thư mục, loại bỏ các file cấu hình rác. Tiến hành bàn giao toàn bộ mã nguồn sạch, ổn định cho các thành viên phụ trách đẩy lên AWS (ECR, ECS Fargate). | 03/07/2026 | 03/07/2026 | Git / GitHub Collaboration |
| 7 | - **Hoàn thiện Kiến trúc Mạng & Đánh giá:** Phối hợp cùng nhóm rà soát và vẽ lại Sơ đồ kiến trúc hạ tầng chi tiết (Multi-AZ, ALB, VPC Endpoints, NAT Gateway, EFS và AWS WAF). Hỗ trợ nhóm AWS xử lý các vướng mắc ban đầu về luồng kết nối container. | 04/07/2026 | 05/07/2026 | Nội bộ nhóm, AWS Architecture Diagrams |

### Thành tựu Tuần 9:
* **Đảm bảo Nguyên tắc Đặc quyền tối thiểu (Least Privilege):** Áp dụng thành công mô hình RBAC và Data Segregation, giải quyết triệt để bài toán quyền riêng tư dữ liệu người dùng song song với việc duy trì khả năng giám sát, thống kê tập trung của Admin.
* **Hoàn thiện tính năng Core Web:** Xử lý sạch các bug logic của phân hệ quản lý tài khoản, giúp ứng dụng sẵn sàng phục vụ nhiều người dùng thử nghiệm cùng lúc với độ tin cậy cao.
* **Tinh thần làm việc nhóm và đóng gói (Teamwork & Delivery):** Bàn giao thành công bộ mã nguồn đã được tối ưu hóa và kiểm thử kỹ càng trên môi trường Docker ảo hóa, tạo tiền đề mượt mà cho việc đưa hệ thống lên hạ tầng đám mây.
* **Chuẩn hóa thiết kế hệ thống:** Hoàn thiện sơ đồ kiến trúc topology chi tiết, làm cơ sở vững chắc để tính toán bảng dự toán chi phí (AWS Calculator) và thiết lập cơ sở lý luận kiến trúc hạ tầng mạng cho quyển báo cáo.