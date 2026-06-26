---
title: "Blog 1"
date: 2026-06-26
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# TỐI ƯU CHI PHÍ VÀ ĐƠN GIẢN HÓA KIẾN TRÚC MẠNG VỚI "NATIVE ATTACHMENT" TRONG AWS NETWORK FIREWALL

Việc thiết lập vị trí tường lửa (Firewall) trong kiến trúc đám mây nhiều VPC nhằm đảm bảo an toàn và khả năng phục hồi ở cấp độ kiến trúc (architecture-level resilience) luôn là một thách thức lớn về mặt thiết kế. Giải pháp sử dụng tính năng "Native Attachment" của AWS Network Firewall tích hợp với Transit Gateway giúp giải quyết triệt để bài toán này bằng cách tối ưu hóa cấu trúc liên kết mạng.

Các điểm chính cần nắm:

* Tính năng Native Attachment cho phép gắn trực tiếp AWS Network Firewall vào AWS Transit Gateway dưới dạng một "Network Function".
* Tự động hóa hạ tầng: AWS tự động triển khai tường lửa vào một VPC do chính họ quản lý (AWS Managed VPC), loại bỏ hoàn toàn yêu cầu phải tự thiết kế và duy trì "Inspection VPC" cùng hệ thống Route Table phức tạp.
* Tối ưu chi phí tài nguyên: Cắt giảm hoàn toàn chi phí duy trì các tài nguyên đi kèm như Subnet, NAT Gateway và Route Table trung gian.
* Quản lý chi phí linh hoạt (Flexible cost allocation): Sử dụng Transit Gateway metering policies để tính toán và phân bổ chính xác chi phí tường lửa cho từng dự án dựa trên lưu lượng thực tế phát sinh.
* Đơn giản hóa luồng mạng: Traffic từ các Spoke VPC được đẩy thẳng đến Transit Gateway, tự động chuyển xuyên qua Network Firewall để rà soát mã độc/xâm nhập, sau đó trả về và định tuyến ra Internet qua Egress VPC.

Kiến trúc này là một "best practice" đặc biệt hữu ích khi tổ chức muốn ưu tiên hướng Cloud-native, giảm thiểu tối đa gánh nặng quản lý hạ tầng ngầm, tối ưu ngân sách vận hành và duy trì khả năng mở rộng quy mô linh hoạt.

### Sơ đồ kiến trúc

![Kiến trúc Transit Gateway-attached Network Firewall](updated-figure-2.png)
*(Nguồn: AWS Security Blog - Cấu trúc luồng dữ liệu khi sử dụng Native Attachment. Lưu ý: Bạn cần chèn đúng đường dẫn file ảnh của bạn vào thư mục /images)*

### Nguồn tham khảo
* Bài viết chi tiết từ AWS Security Blog: [Why and how to migrate to a Transit Gateway-attached AWS Network Firewall](https://aws.amazon.com/blogs/security/why-and-how-to-migrate-to-a-transit-gateway-attached-aws-network-firewall/)

