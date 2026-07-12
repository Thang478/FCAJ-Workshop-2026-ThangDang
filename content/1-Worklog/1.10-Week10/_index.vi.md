---
title: "Worklog Tuần 10"
date: 2026-07-12
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu Tuần 10:
* Tối ưu hóa và hoàn thiện sơ đồ kiến trúc hạ tầng AWS (Architecture Topology) dựa trên các góp ý chuyên sâu từ chuyên gia.
* Thực hiện dự toán và tối ưu hóa chi phí đám mây (Cloud FinOps) thông qua AWS Pricing Calculator.
* Tổng hợp các đóng góp cộng đồng (Community Contribution) và biên tập lại bài viết kỹ thuật chuyên sâu.
* Chuẩn bị toàn bộ hồ sơ, tài liệu Proposal cho buổi Workshop và kịch bản trình bày cho nhóm.

### Các công việc thực hiện trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - **Nâng cấp & Sửa lỗi Kiến trúc AWS:** Nhận feedback và điều chỉnh sơ đồ draw.io: (1) Nắn lại luồng kết nối từ CloudFront đi thẳng vào Internet Gateway (IGW); (2) Vẽ lại khối AWS Fargate Task cho chuẩn xác; (3) Xóa icon của các External Services và đổi tên thành các dịch vụ tự phát triển để tránh nhầm lẫn. | 06/07/2026 | 06/07/2026 | AWS Architecture Icons, Admin Feedback |
| 3-4 | - **Tính toán & Tối ưu Chi phí (FinOps):** Tính toán chi tiết 7 dịch vụ (Fargate, ALB, EFS, VPC, CloudFront, WAF, Secrets Manager) tại Region Singapore (AP-Southeast-1). Tối ưu lại NAT Gateway và chốt tổng chi phí ước tính ở mức ~$103/tháng. Xuất file PDF dự toán chi tiết. | 07/07/2026 | 08/07/2026 | AWS Pricing Calculator |
| 5-6 | - **Biên tập & Tổng hợp Blog Cộng đồng:** Rà soát và tổng hợp lại bài viết kỹ thuật đã đăng trên AWS Study Group VN (ngày 23/06) về chủ đề *"Tối ưu chi phí và kiến trúc mạng với AWS Network Firewall & Transit Gateway"*. Hệ thống hóa nội dung bài viết để đưa vào danh mục đánh giá năng lực cộng đồng của FCAJ. | 09/07/2026 | 10/07/2026 | AWS Security Blog |
| 7 | - **Chuẩn bị Tài liệu Workshop:** Viết bản Proposal hoàn chỉnh gồm 8 phần. Chuẩn bị bản mô tả kiến trúc song ngữ Việt/Anh và soạn thảo các kịch bản trình bày để nhóm thống nhất nội dung. Theo dõi tiến độ deploy lên AWS của nhóm. | 11/07/2026 | 12/07/2026 | FCAJ Workshop Guidelines |

### Thành tựu Tuần 10:
* **Kiến trúc đạt chuẩn thực chiến:** Khắc phục triệt để các lỗi sai về luồng định tuyến (CloudFront -> IGW) và hoàn thiện sơ đồ AWS chi tiết, trực tiếp giải trình thành công lý do sử dụng ALB và EFS trước chuyên gia.
* **Tối ưu hóa tài chính:** Điều chỉnh thành công cấu hình mạng, đưa tổng dự toán chi phí (Cost estimate) về mức ~$103/tháng, đảm bảo ngân sách vận hành tối ưu cho dự án.
* **Lan tỏa giá trị cộng đồng:** Ghi nhận và hệ thống hóa thành công năng lực nghiên cứu thông qua bài viết chuyên sâu về AWS Security (tính năng Native Attachment của Transit Gateway), khẳng định tư duy kiến trúc bảo mật linh hoạt (Flexible cost allocation).