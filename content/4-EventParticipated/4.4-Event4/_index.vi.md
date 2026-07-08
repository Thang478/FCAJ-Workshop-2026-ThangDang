---
title: "Event 4"
date: 2026-06-06
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

# Báo cáo tổng kết: “AWS Student Builder Group - Kiro Spec-Driven Development”

### Mục tiêu sự kiện
* Nắm bắt khái niệm và phương pháp luận của Spec-Driven Development (Phát triển theo hướng đặc tả).
* Tìm hiểu tổng quan vai trò của nền tảng Kiro trong quá trình hỗ trợ kỹ nghệ phần mềm với AI (AI-assisted software engineering).
* Khám phá quy trình chuyển đổi từ Yêu cầu thô sang Đặc tả (Specifications), Thiết kế hệ thống và Kế hoạch triển khai.
* Cải thiện tư duy cộng tác và đưa ra quyết định kiến trúc tốt hơn để tận dụng AI hiệu quả.

### Diễn giả & Điều phối
* **Quang Tịnh Trương** – Diễn giả chính
* **Kiệt Trần** – Diễn giả khách mời
* **Danh Hoàng Hiếu Nghị** – Điều phối (Host) / AWS Student Builder Group tại HUFLIT

---

### Nội dung nổi bật

#### 1. Giới thiệu về Spec-Driven Development (SDD)
* **Tư duy Specification-first:** Chuyển dịch từ việc vội vàng viết code hoặc để AI sinh mã rời rạc sang việc tập trung xác định rõ ràng cấu trúc, ràng buộc và luồng dữ liệu ngay từ đầu.
* **Tầm quan trọng:** Giải quyết tình trạng AI bị "ảo giác" (hallucination), giúp tạo ra những đoạn code đáng tin cậy và dễ bảo trì hơn nhờ có ngữ cảnh tổng thể.

#### 2. Kiro và AI-Assisted Engineering
* **Vai trò của Kiro:** Đóng vai trò định hình và chuẩn hóa các yêu cầu thành bản đặc tả kỹ thuật, hướng dẫn các AI coding assistant tạo ra mã nguồn tuân thủ đúng quy chuẩn kiến trúc.
* **Sức mạnh của Markdown (.md):** Khả năng đọc hiểu, tóm tắt và tự động hóa khởi tạo các file đặc tả hệ thống dưới định dạng Markdown, giúp lưu trữ minh bạch và đồng bộ dễ dàng cùng source code.

#### 3. Triển khai kiến trúc thực tế (Chia sẻ từ khách mời)
* **AgentCore Runtime Deployment Pattern:** Diễn giả Kiệt Trần chia sẻ thêm về mô hình triển khai AI Voice Agents, nhấn mạnh việc đóng gói pipeline thành các Container và sử dụng cơ chế MicroVM để cô lập các phiên làm việc (Session isolation).
* **Network & Security:** Cách ứng dụng TURN servers và thiết lập NAT Gateway trong VPC để đảm bảo kết nối WebRTC bảo mật, tốc độ cao.

---

### Bài học rút ra
* **Tư duy thiết kế:** Code sinh ra từ AI chỉ thực sự an toàn và có giá trị khi nó được dẫn dắt bởi một bản thiết kế kiến trúc chuẩn mực.
* **Quản trị rủi ro AI:** Không nên phó mặc hoàn toàn logic nghiệp vụ cho AI. Kỹ sư cần là người nắm giữ bản đặc tả cốt lõi của hệ thống.
* **Kiến trúc triển khai:** Nắm bắt được cách phân tách hệ thống (Container-Session isolation) để vận hành các mô hình AI an toàn trên môi trường Cloud.

### Ứng dụng vào công việc
* **Cấu trúc dự án:** Áp dụng phương pháp spec-first để viết tài liệu API, vẽ sơ đồ luồng giao tiếp mạng và thiết lập các module bảo mật trước khi code hệ thống nhận diện mã độc.
* **Tối ưu Prompting:** Yêu cầu AI phản biện, thiết lập bảo mật (WAF, VPC) và xuất ra định dạng Markdown rõ ràng trước khi tạo các file cấu hình hạ tầng.
* **Vận dụng hạ tầng:** Áp dụng mô hình cô lập Container và định tuyến qua NAT Gateway (học từ pattern của Voice Agent) vào việc thiết lập môi trường an toàn cho hệ thống xử lý phân tích file PE độc hại.

---

### Trải nghiệm sự kiện
Sự kiện trực tuyến đã mang đến một góc nhìn thực tế về cách kiểm soát AI trong lập trình hiện đại thông qua phương pháp định hướng đặc tả.

**Tiếp cận nền tảng ở mức tổng quan**
* Do không có quá nhiều câu hỏi đi sâu vào kỹ thuật phức tạp, phần chia sẻ về Kiro mang tính chất giới thiệu bề mặt, giúp người nghe dễ dàng hình dung concept và tư duy nền tảng của Spec-Driven Development. Bù lại, phần chia sẻ ngắn của khách mời về mô hình triển khai AgentCore lại đem đến hàm lượng kiến trúc mạng rất thực chiến.

**Giá trị kết nối và Thảo luận Q&A**
* Dù số lượng câu hỏi ít, nhưng điểm nhấn của phần Q&A là màn so sánh trực tiếp rất sắc sảo: Kiro đóng vai trò như một kiến trúc sư (tập trung vào file `.md` và bối cảnh tổng thể), trong khi các công cụ như GitHub Copilot Pro thiên về vai trò trợ lý gõ code cục bộ.

**Thay đổi tư duy làm việc với AI**
* Buổi chia sẻ đã xóa bỏ thói quen lạm dụng AI để sinh code "mì ăn liền". Thay vào đó là tư duy biến yêu cầu thành các file thiết kế hệ thống rõ ràng, minh bạch hóa quy trình phát triển phần mềm.

#### Hình ảnh sự kiện
![Hình ảnh sự kiện](image.png)
> **Đánh giá chung:** Một sự kiện thực chiến, đánh đúng vào xu hướng phát triển phần mềm hiện đại. Kiến thức về Spec-Driven Development cùng với các pattern triển khai kiến trúc là nền tảng vô cùng hữu ích để áp dụng ngay vào việc chuẩn hóa tài liệu và thiết lập topology mạng cho đồ án tốt nghiệp hiện tại.