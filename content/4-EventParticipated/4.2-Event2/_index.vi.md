---
title: "Event 2"
date: 2026-05-30
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Báo cáo tổng kết: “AWS Student Builder Group: Build Voice Agents at Scale”

### Mục tiêu sự kiện
* Hiểu về kiến trúc của các AI Voice Agents trên nền tảng đám mây.
* Tìm hiểu cách sử dụng Amazon Bedrock AgentCore cho các tính năng AI tạo sinh (Generative AI).
* Khám phá các thực tiễn tốt nhất (best practices) để triển khai và mở rộng quy mô ứng dụng AI đàm thoại trên AWS.
* Thảo luận về các case study thực tế khi tích hợp AI vào quy trình làm việc tự động hóa.

### Diễn giả & Điều phối
* **Kiệt Trần** – AI Developer / Diễn giả khách mời
* **Danh Hoàng Hiếu Nghị** – Điều phối (Host) / AWS Student Builder Group tại HUFLIT

---

### Nội dung nổi bật

#### 1. Giới thiệu về Amazon Bedrock AgentCore
* **Tính năng:** Cách Bedrock AgentCore đơn giản hóa việc tạo các ứng dụng AI bằng cách tự động quản lý các lệnh gọi API, cửa sổ ngữ cảnh (context windows) và lịch sử trò chuyện.
* **Foundation Models:** Tiêu chí lựa chọn các mô hình ngôn ngữ lớn (LLMs) phù hợp cho các luồng công việc chuyển đổi giọng nói thành văn bản (voice-to-text) và văn bản thành giọng nói (text-to-voice).

#### 2. Thiết kế kiến trúc Voice Agent
* **Luồng dữ liệu (Data Flow):** Quá trình thu thập đầu vào giọng nói, chuyển biên, xử lý ý định (intent) bằng LLM và tổng hợp giọng nói đầu ra.
* **Tích hợp Serverless:** Sử dụng AWS Lambda và API Gateway để tạo ra các tương tác phản hồi nhanh, độ trễ thấp cho Voice Agent.

#### 3. Mở rộng quy mô và Thực tiễn vận hành
* **Hiệu suất:** Chiến lược xử lý các yêu cầu đồng thời cao (high-concurrency) và tối ưu hóa độ trễ trong xử lý giọng nói theo thời gian thực.
* **Bảo mật:** Cách bảo mật prompt, quản lý quyền IAM cho Bedrock và đảm bảo quyền riêng tư dữ liệu trong môi trường đám mây.

---

### Bài học rút ra
* **Tư duy AI:** Chuyển đổi từ các chatbot dựa trên quy tắc (rule-based) truyền thống sang các AI agent có khả năng nhận thức ngữ cảnh động nhờ Foundation Models.
* **Kiến trúc:** Nắm vững sự tích hợp giữa các dịch vụ AI (Amazon Bedrock) và điện toán Serverless (Lambda) để xây dựng các giải pháp có khả năng mở rộng cao.
* **Hiệu quả:** Tận dụng các dịch vụ được quản lý (managed services) cho phép builder tập trung vào logic nghiệp vụ và "tính cách" của agent thay vì phải lo lắng về hạ tầng bên dưới.

### Ứng dụng vào công việc
* **Tích hợp AI:** Khám phá việc áp dụng Bedrock và AI tạo sinh vào quy trình phân tích mối đe dọa hoặc SOC (ví dụ: sử dụng AI agent để tóm tắt log bảo mật và điều tra hành vi mã độc).
* **Điện toán Serverless:** Đưa vào quy chuẩn việc sử dụng AWS Lambda để kích hoạt các tác vụ tự động, hướng sự kiện (event-driven).
* **Đổi mới:** Thử nghiệm phát triển các công cụ nội bộ sử dụng AI agent nhằm tăng tốc độ truy xuất thông tin và truy vấn hệ thống trên môi trường đám mây.

---

### Trải nghiệm sự kiện
Sự kiện đã cung cấp một cái nhìn sâu sắc và thực tế về lĩnh vực Generative AI đang phát triển nhanh chóng trên AWS.

**Học hỏi từ các chuyên gia trong ngành**
* Diễn giả đã chia sẻ các **thực tiễn tốt nhất** trong việc xây dựng và mở rộng AI agent, giúp các khái niệm phức tạp về Bedrock trở nên vô cùng dễ hiểu.
* Các bản demo thực tế đã làm rõ cách các foundation models tương tác với các API bên ngoài để thực thi các tác vụ tự động.

**Tiếp cận kỹ thuật thực tiễn**
* Hình dung rõ ràng **luồng dữ liệu** của các hệ thống AI đàm thoại theo thời gian thực.
* Thu được kiến thức về cách vượt qua các thách thức về độ trễ và quản lý trạng thái (state-management) trong các ứng dụng dựa trên giọng nói.

**Kết nối và thảo luận**
* Phần Q&A đã làm nổi bật những cạm bẫy phổ biến mà các developer thường gặp khi bắt đầu làm việc với Generative AI.
* Việc tương tác với cộng đồng HUFLIT Builder đã mang lại động lực và những góc nhìn mới mẻ về công nghệ đám mây.

#### Hình ảnh sự kiện
![Hình ảnh sự kiện](image-1.png)

> **Đánh giá chung:** Sự kiện đã kết nối thành công khoảng cách giữa lý thuyết AI và kỹ thuật đám mây thực tế, trang bị cho tôi kiến thức nền tảng để bắt đầu tích hợp Amazon Bedrock vào các dự án vận hành và bảo mật trong tương lai.