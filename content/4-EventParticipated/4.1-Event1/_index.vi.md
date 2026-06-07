---
title: "Event 1"
date: 2026-06-06
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---



# Bài thu hoạch “AWS First Cloud Journey / Community Day”

### Mục Đích Của Sự Kiện
* Định hướng kỹ năng công nghệ cốt lõi cho các lập trình viên trẻ (builders) trong kỷ nguyên AI.
* Cập nhật các kiến trúc Cloud Native thực tế trên AWS (Serverless, Containerization, GraphRAG, NIDS).
* Hướng dẫn thiết kế kiến trúc hệ thống mạng cho Game Multiplayer.
* Chia sẻ kinh nghiệm thực chiến về vận hành hệ thống và phát triển sự nghiệp.

### Danh Sách Diễn Giả
* **Slavik Dimitrovich** - Đại diện AWS (Phiên chia sẻ định hướng chiến lược qua Video)
* **Nguyễn Quốc Bảo** - Game Developer / Cloud Builder
* **Bảo Huỳnh** - Junior Cloud Native Developer tại Endava / Founder of ITea Lab
* **Việt Phát** - AI/ML Builder
* **Lê Hoàng Gia Đại** - Security Builder (Team AWS G3)
* **Trần Trung Vinh** - System Administrator tại Central Retail Group (Chia sẻ kinh nghiệm thực chiến)

---

### Nội Dung Nổi Bật

#### 1. Định hướng chiến lược trong kỷ nguyên AI (Video Keynote)
* **Hình thức:** Phiên chia sẻ định hướng qua video ghi hình sẵn từ chuyên gia AWS.
* **Nội dung:** Bác Slavik Dimitrovich phân tích lộ trình kỹ năng cho builders trẻ trong 5 năm tới, cách thu hẹp khoảng cách giữa năng lực kỹ thuật và kỳ vọng của doanh nghiệp, cũng như chiến lược xây dựng giải pháp AI hiệu quả tại khu vực ASEAN.

#### 2. Kiến trúc Game Multiplayer trên Cloud (Nguyễn Quốc Bảo)
* **Lựa chọn kiến trúc:** Phân tích UDP, WebSocket và HTTP Polling.
* **Godot Integration:** Kết nối Godot 4 với AWS WebSockets, sử dụng Lambda xử lý JSON và DynamoDB lưu trữ trạng thái game.

#### 3. Công nghệ Containerization (Bảo Huỳnh)
* So sánh Virtualization vs Containerization.
* Demo trực tiếp quy trình đóng gói ứng dụng (Containerize) lên môi trường Docker.

#### 4. Ứng dụng AI/ML và Bảo mật (Việt Phát & Lê Hoàng Gia Đại)
* **GraphRAG:** Kết hợp Amazon Bedrock với Amazon Neptune để nâng cao độ chính xác cho AI.
* **NIDS:** Xây dựng hệ thống phát hiện xâm nhập bằng cách tích hợp AWS WAF và Machine Learning.

#### 5. Hành trình thực chiến (Trần Trung Vinh)
* **Vận hành:** Cách xử lý High Traffic và đảm bảo High Availability khi gặp sự cố phần cứng (triết lý ưu tiên dịch vụ lõi).
* **Sự nghiệp:** Chiến lược "đọc vị" doanh nghiệp qua LinkedIn và lộ trình phát triển từ Helpdesk lên Senior Sysadmin.

---

### Những Gì Học Được

* **Tư duy thiết kế:** Luôn bắt đầu từ Business-first approach và tư duy "hy sinh râu ria để giữ lấy phần lõi" trong vận hành.
* **Kiến trúc:** Nắm vững cách lựa chọn công nghệ (VM vs Containers vs Serverless) và giao thức mạng dựa trên đặc thù bài toán.
* **Chiến lược:** Đo lường ROI trước khi hiện đại hóa hệ thống và xây dựng networking bền vững qua LinkedIn.

### Ứng Dụng Vào Công Việc
* Áp dụng Docker cho môi trường dev/deploy để chuẩn hóa hệ thống.
* Thử nghiệm AWS Lambda/DynamoDB cho các logic backend đơn giản.
* Tối ưu profile LinkedIn và tìm hiểu kỹ tech-stack của công ty trước khi apply.

---

### Trải nghiệm trong event
Sự kiện cung cấp cái nhìn toàn diện từ kỹ thuật chuyên sâu (Docker, AI, Security) đến tư duy vận hành thực tế. 

**Học hỏi từ diễn giả chuyên môn**
* Các kiến thức về best practices trong thiết kế kiến trúc game, container hóa và bảo mật mạng được chia sẻ rất thực tế.
* Những đúc kết từ anh Trung Vinh về việc "giữ lấy phần lõi" khi hệ thống gặp sự cố là bài học thực tế quý giá nhất.

**Trải nghiệm kỹ thuật**
* Hình dung rõ ràng data flow của hệ thống real-time khi kết nối Godot với hạ tầng AWS Serverless.
* Hiểu cách AWS WAF kết hợp với Machine Learning tạo ra lá chắn bảo mật chủ động.

**Kết nối và trao đổi**
* Sự kiện giúp tôi thấy được sự khác biệt giữa năng lực hiện tại và yêu cầu từ thị trường, từ đó có lộ trình học tập tập trung hơn vào các giải pháp Cloud Native.

#### Bài học rút ra
* Việc lựa chọn kiến trúc phải luôn dựa trên đặc thù bài toán thay vì chạy theo xu hướng.
* High Availability và khả năng ứng biến khi phần cứng gặp sự cố quan trọng hơn việc xây dựng một hệ thống hoàn hảo nhưng thiếu tính dự phòng.
* Luôn cập nhật kỹ năng cốt lõi để không bị tụt hậu trước sự phát triển của Generative AI.

#### Hình ảnh sự kiện
![alt text](image.png)

> **Tổng kết:** Sự kiện giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team công nghệ.