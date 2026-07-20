---
title: "Worklog Tuần 12"
date: 2026-07-26
weight: 11
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu Tuần 12:
* Kiểm thử nghiệm thu (UAT) hệ thống MalScan AI trên môi trường Live AWS chính thức.
* Quay và dựng Video Demo (3-5 phút) giới thiệu tổng quan kiến trúc và tính năng của hệ thống.
* Đóng gói toàn bộ tài nguyên (Source Code, URL Workshop, Video Demo) và nộp lên FCAJ Portal.
* Chuẩn bị hồ sơ, đánh giá tổng kết và hoàn thành các điều kiện cần thiết để xin cấp mộc xác nhận thực tập.

### Các công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2-3 | - **Kiểm thử UAT (Live Environment):** Thực hiện test end-to-end trên domain chính thức. Bắn tải thử nghiệm các mẫu file PE độc hại, tài liệu phishing và URL để xác nhận CloudFront/WAF lọc đúng traffic và mô hình ML trên Fargate trả về kết quả chính xác. Kiểm tra cơ chế Hash Cache (SQLite trên EFS). | 20/07/2026 | 21/07/2026 | Software Testing (UAT) Checklists |
| 4-5 | - **Sản xuất Video Demo:** Xây dựng kịch bản demo trực quan. Tiến hành quay lại màn hình thao tác quét mã độc, kết hợp giải thích luồng định tuyến kiến trúc AWS (Topology 12 bước). Dựng video (3-5 phút) và upload lên nền tảng lưu trữ. | 22/07/2026 | 23/07/2026 | OBS Studio, Video Editing Tools |
| 6 | - **Nộp hồ sơ FCAJ Portal:** Đóng gói hoàn chỉnh dự án. Truy cập FCAJ Portal để điền form nghiệm thu cuối kỳ. Cung cấp đầy đủ các liên kết: URL Public của Website Workshop, URL GitHub Repository (chứa source code MalScan AI) và link Video Demo. | 24/07/2026 | 24/07/2026 | FCAJ Submission Portal |
| 7 | - **Hoàn thiện thủ tục nhận mộc:** Tổng hợp báo cáo cá nhân và kết quả nghiệm thu dự án. Đối chiếu với các tiêu chí đánh giá của đơn vị thực tập, tiến hành xin chữ ký xác nhận của Mentor/Admin FCAJ và chuẩn bị sẵn sàng hồ sơ cứng để nhận mộc xác nhận từ AWS phục vụ nộp về trường. | 25/07/2026 | 26/07/2026 | Quy định thực tập HUTECH, Nội bộ nhóm |

### Thành tựu Tuần 12:
* **Nghiệm thu Hệ thống Thành công:** Hệ thống MalScan AI vận hành trơn tru trên môi trường AWS thực tế, vượt qua tất cả các kịch bản kiểm thử khắc nghiệt nhất (Live UAT).
* **Hoàn tất Yêu cầu Thực tập (Bootcamp):** Submit thành công toàn bộ hồ sơ chất lượng cao lên FCAJ Portal đúng thời hạn, khép lại chương trình thực tập Bootcamp một cách xuất sắc.
* **Hoàn thiện Thủ tục Hành chính:** Chuẩn bị đầy đủ và hợp lệ toàn bộ hồ sơ, báo cáo, minh chứng năng lực để đáp ứng các điều kiện khắt khe nhất cho việc nhận mộc đánh giá thực tập từ doanh nghiệp.