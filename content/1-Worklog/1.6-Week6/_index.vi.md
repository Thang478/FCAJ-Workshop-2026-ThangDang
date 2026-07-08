---
title: "Worklog Tuần 6"
date: 2026-06-14
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu Tuần 6:
* Nắm vững cơ chế bảo mật dữ liệu tại chỗ (Data at Rest) thông qua dịch vụ quản lý khóa AWS Key Management Service (KMS).
* Thiết lập hệ thống kiểm toán, truy vết nhật ký API bảo mật bằng AWS CloudTrail và truy vấn dữ liệu lớn phi máy chủ bằng Amazon Athena.
* Tối ưu hóa mã nguồn Web App MLOps: xử lý tệp nén ZIP mã hóa, tối ưu bộ nhớ giao diện (Smart Cache) và hoàn thiện luồng tự động cách ly (Sandbox).
* Phác thảo sơ đồ kiến trúc hệ thống và kiểm thử ổn định phiên bản Docker cuối cùng trước khi triển khai thực tế.

### Các công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu lý thuyết Bảo mật Đám mây: Phân biệt CMK (Customer Managed Keys) và AWS Managed Keys trong KMS.<br>- Tìm hiểu kiến trúc ghi log sự kiện tập trung với CloudTrail và Athena. | 08/06/2026 | 08/06/2026 | AWS Video Series |
| 3 | - Thực hành Lab: *AWS Key Management Service (KMS)*.<br>- Khởi tạo khóa đối xứng (Symmetric Key), thiết lập IAM Policy (Least Privilege) và ép buộc mã hóa SSE-KMS mặc định cho bucket Amazon S3. | 09/06/2026 | 09/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Thực hành Lab: *CloudTrail & Amazon Athena*.<br>- Kích hoạt Data Events trên S3. Viết truy vấn SQL trên giao diện Athena để truy vết sự kiện `PutObject` và kiểm chứng mã lỗi `AccessDenied` khi thiếu quyền giải mã. | 10/06/2026 | 10/06/2026 | [AWS Cloud Journey](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Đồ án nhóm: Nâng cấp Web App. Tích hợp thư viện `pyzipper` hỗ trợ phân tích hàng loạt mẫu mã độc nằm trong file nén ZIP bảo vệ bằng mật khẩu (AES/ZipCrypto). | 11/06/2026 | 11/06/2026 | Đồ án nhóm |
| 6 | - Tái cấu trúc giao diện Streamlit: Triển khai cơ chế *Smart Cache* để tối ưu hạn mức API VirusTotal.<br>- Xây dựng phân hệ Sandbox tự động cách ly vật lý các file AI nhận diện sai lệch. Fix lỗi định dạng đường dẫn (`os.path.normpath`). | 12/06/2026 | 13/06/2026 | Đồ án nhóm |
| 7 | - Phác thảo thiết kế Sơ đồ Kiến trúc Hệ thống (Architecture Diagram) bằng Draw.io.<br>- Build lại Image Docker, kiểm thử toàn diện luồng người dùng và dọn dẹp các tài nguyên AWS (Schedule Key Deletion, Empty S3) để tối ưu chi phí. | 14/06/2026 | 14/06/2026 | Đồ án nhóm |

### Thành tựu Tuần 6:
* **Bảo mật Dữ liệu (AWS KMS):** Làm chủ quy trình cấp phát, phân quyền và thiết lập vòng đời tự hủy cho các khóa mã hóa bảo vệ kho lưu trữ dữ liệu S3.
* **Kiểm toán & Truy vết Hệ thống (Digital Forensics):** Có khả năng thiết lập "hộp đen" hệ thống, sử dụng SQL qua Amazon Athena để rà soát hàng ngàn dòng nhật ký truy cập từ CloudTrail nhằm phát hiện hành vi trái phép.



* **Nâng cấp Hệ thống MLOps:** Hoàn thiện luồng kỹ thuật (UX/UI) cho SOC Analyst với tính năng quét batch file ZIP, bộ nhớ đệm thông minh tự dọn dẹp và vòng lặp thu thập dữ liệu (Feedback Loop) hoàn toàn tự động.
* **DevOps & Architecture:** Đóng gói thành công khối mã nguồn nâng cao vào Container cô lập. Sẵn sàng cho việc đẩy Image lên Amazon ECR ở giai đoạn tiếp theo.