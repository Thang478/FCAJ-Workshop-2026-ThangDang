---
title: "Worklog Tuần 3"
date: 2026-05-24
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---


### Mục tiêu tuần 3:
* Làm chủ các khái niệm cốt lõi về tính toán của AWS (Cấu hình Amazon EC2, AMI, các loại ổ cứng và vòng đời máy ảo) thông qua Module 03.
* Xây dựng hệ thống bảo vệ dữ liệu tự động, hướng sự kiện sử dụng kết hợp AWS Backup, CloudFormation, Amazon SNS và AWS Lambda.
* Thiết lập mô hình mạng doanh nghiệp có khả năng mở rộng quy mô bằng cách sử dụng AWS Transit Gateway làm bộ định tuyến trung tâm thay thế cho VPC Peering.
* Phối hợp với đồng đội để thống nhất đề tài dự án thực tập và phân chia phân khúc công việc kỹ thuật ban đầu.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Hoàn thành khóa đào tạo lý thuyết chuyên sâu của Module 03 (Video từ 72 đến 80).<br>- Nghiên cứu chi tiết về Instance Types, Amazon Machine Images (AMI), và sự khác biệt về kiến trúc lưu trữ giữa EBS và Instance Store.<br>- Phân tích kịch bản khởi tạo máy ảo (User Data) và các tính năng của siêu dữ liệu (Metadata). | 18/05/2026 | 18/05/2026 | Chuỗi Video AWS |
| 3 | - Bắt đầu triển khai bài thực hành sao lưu hệ thống "Data Protection with AWS Backup".<br>- Khởi tạo thủ công S3 bucket mang tên `thang-aws-backup-lab-2026`, điều chỉnh quyền truy cập công khai và áp dụng cấu hình JSON Bucket Policy (`s3:GetObject`).<br>- Tải lên các file tài nguyên hạ tầng tĩnh (`backup-lab.yaml`, `lambda_function.zip`). | 19/05/2026 | 19/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Triển khai tự động hóa hạ tầng thông qua dịch vụ AWS CloudFormation.<br>- Thực hiện chỉnh sửa trực tiếp tệp cấu hình mẫu `backup-lab.yaml`, thay đổi loại InstanceType sang dòng máy `t3.micro` để đảm bảo tính tương thích và cấp phát thành công.<br>- Khởi tạo thành công VPC, nhóm bảo mật, và máy chủ ứng dụng web mục tiêu. | 20/05/2026 | 20/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Thiết lập két sắt lưu trữ chuyên dụng `BACKUP-LAB-VAULT` và lập cấu hình kế hoạch sao lưu tổng thể `BACKUP-LAB`.<br>- Áp dụng quy tắc vòng đời (Lifecycle) tự động xóa bỏ các điểm phục hồi cũ sau thời hạn 7 ngày.<br>- Sử dụng AWS CloudShell thực thi lệnh CLI liên kết các sự kiện hoạt động của Vault (`BACKUP_JOB_COMPLETED`, `RESTORE_JOB_COMPLETED`) tới Amazon SNS. | 21/05/2026 | 21/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - Kích hoạt phiên sao lưu theo yêu cầu (On-demand Backup) dựa trên Instance ID của máy chủ EC2.<br>- Kiểm tra luồng tự động hóa hệ thống: xác thực hàm AWS Lambda tự động gọi API chạy bài test khôi phục dữ liệu (Restore Test).<br>- Phân tích logs ứng dụng tại CloudWatch Log Groups, nhận email thông báo thời gian thực và dọn dẹp sạch toàn bộ tài nguyên. | 22/05/2026 | 22/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 7 / CN | - Triển khai bài thực hành mạng nâng cao: "Centralized Network Management with AWS Transit Gateway".<br>- Khởi tạo Transit Gateway đóng vai trò bộ định tuyến đám mây (Cloud Router) và cấu hình TGW Attachments để kết nối 4 VPC độc lập.<br>- Cấu hình TGW Route Tables và cập nhật bảng định tuyến nội bộ của các VPC (định tuyến `172.16.0.0/16` và `0.0.0.0/0`) để ping kiểm tra kết nối thành công.<br>- Họp nhóm với để phân chia công việc dự án. | 23/05/2026 | 24/05/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:
* **Năng lực hạ tầng chuyên sâu:** Nắm vững cơ chế ảo hóa của EC2, kiến trúc ổ đĩa lưu trữ tạm thời và lưu trữ vĩnh viễn (EBS), cùng kỹ thuật cấu hình kịch bản tự động hóa bootstrap hệ thống.
* **Thực chứng Hạ tầng dạng mã (IaC):** Làm chủ cách thức CloudFormation biên dịch tài nguyên mạng an toàn, đảm bảo cấp phát thành công thông qua cấu hình `t3.micro`.
* **Chu trình Bảo vệ dữ liệu tự động:** Thiết lập thành công chuỗi cung ứng dữ liệu hướng sự kiện phi máy chủ (Serverless), kích hoạt thông báo tự động qua Amazon SNS và tự động gọi mã nguồn AWS Lambda để thẩm định tính toàn vẹn của dữ liệu sau khôi phục.
* **Kiến thức mạng đám mây nâng cao:** Nắm vững chiến thuật xây dựng mạng lưới doanh nghiệp theo mô hình Hub-and-Spoke. Quản lý thành công luồng giao tiếp phức tạp giữa nhiều VPC thông qua AWS Transit Gateway.
* **Quản trị dự án nhóm:** Thống nhất chặt chẽ lộ trình phân bổ công việc kỹ thuật cụ thể với đồng đội nhằm đảm bảo các mốc thời gian quan trọng của dự án thực tập.