---
title: "Kết quả và video demo"
date: 2026-07-22
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---


Sau khi hoàn thành các bước cấu hình, hệ thống MalScanAI được triển khai trên Amazon ECS Fargate và người dùng truy cập ứng dụng thông qua tên miền đã cấu hình.

Video demo cuối workshop sẽ tập trung vào các nội dung sau:

- Truy cập MalScanAI qua tên miền HTTPS.
- Kiểm tra giao diện Streamlit.
- Thực hiện quét URL hoặc tệp tin mẫu.
- Theo dõi quá trình xử lý và kết quả trả về.




### 🖥️ Mô tả chi tiết chức năng Giao diện Web MalScanAI (Phiên bản SOC Platform)

Hệ thống được thiết kế phân quyền theo 3 cấp độ (Guest, User, Admin) với giao diện **Đa ngôn ngữ (i18n)**, hỗ trợ chuyển đổi linh hoạt để tối ưu trải nghiệm người dùng. Cấp độ sau sẽ kế thừa toàn bộ tính năng của cấp độ trước và được mở rộng thêm các đặc quyền quản trị.

#### 1. Khách vãng lai (Guest)
*   **Bảo vệ tài nguyên (Rate Limiter):** Bị giới hạn dung lượng tải lên (Max 200MB/file), số lượng file và số lượt quét tối đa trong ngày để chống Spam. Không lưu lại lịch sử.
*   **Quét URL Phishing:** Phân tích đường link đáng ngờ bằng AI kết hợp trích xuất thông tin tình báo mạng (OSINT).
*   **Quét Tệp tin (PE & Document):** Hỗ trợ phân tích file đơn hoặc nhiều file cùng lúc. Đối chiếu chéo với VirusTotal.
*   **Xử lý tệp nén bảo mật (Secure ZIP Extraction):** Hệ thống có khả năng nhận diện file ZIP bị khóa mật khẩu (kỹ thuật hacker thường dùng để lách phần mềm diệt virus), cung cấp Form yêu cầu nhập mật khẩu để giải nén và quét sâu cấu trúc bên trong.
*   **Bảo vệ hệ thống (PE Scanner tiên tiến):** 
    *   Tự động nhận diện kiến trúc phần mềm Win32/Win64. 
    *   **Tích hợp Mô hình AI kép (Dual-Model):** Trang bị mô hình phân tích tiêu chuẩn (V1) và một **mô hình chuyên dụng chống né tránh (Evasion-resilient - V2)**. Hệ thống cho phép linh hoạt kích hoạt Model V2 để bóc trần các mã độc ẩn mình tinh vi, giúp nâng cao tỷ lệ phát hiện.
    *   Trực tiếp phát hiện các file bị dị dạng/chỉnh sửa (Độ hỗn loạn Entropy cao, nghi ngờ nén/mã hóa) và yêu cầu người dùng xác nhận trước khi cho phép AI phân tích sâu.
*   **Kết quả nhận được:** Xem trực tiếp báo cáo rủi ro ngay trên màn hình. Sử dụng công nghệ giải thích XAI (SHAP) để minh bạch hóa lý do AI đưa ra quyết định.

#### 2. Người dùng đăng nhập (User)
*   **Kế thừa:** Toàn bộ tính năng quét của Khách.
*   **Bảo mật tài khoản:** Mật khẩu được mã hóa an toàn một chiều (Bcrypt).
*   **Nâng hạn mức:** Giới hạn dung lượng và số lượng quét được mở rộng gấp 3 lần so với Khách (Cho phép kéo thả hàng trăm file để quét hàng loạt).
*   **Tùy biến:** Tích hợp tính năng bật/tắt đối chiếu VirusTotal để tăng tốc độ phân tích cục bộ.
*   **Quản lý lịch sử:** Tự động lưu trữ toàn bộ lịch sử URL và tệp tin đã quét, kèm bảng thống kê tổng quan cá nhân.
*   **Kết quả nhận được:** Sở hữu Bảng điều khiển (Dashboard) cá nhân. Xem lại chi tiết các lần quét cũ ngay lập tức mà không cần phân tích lại nhờ cơ sở dữ liệu **Hash Cache System** siêu tốc.

#### 3. Quản trị viên (Admin - Đặc quyền MLOps & SOC)
*   **Kế thừa:** Toàn bộ tính năng và lịch sử lưu trữ của User.
*   **Tổng trạm Giám sát (SOC Dashboard Landing Page):** Theo dõi toàn cảnh hệ thống theo thời gian thực:
    *   *Trạng thái lưu trữ:* Giám sát tài nguyên không gian đĩa thực tế trên Đám mây. (VD: 🖥️ **Trạng Thái Máy Chủ** 📊 *Đã dùng: 0.0 GB / 8589934592.0 GB*).
    *   *Thống kê Hash Cache Database:* Hiển thị tổng lượt quét (URL, PE), tỷ lệ phát hiện Phishing/Malware (%), số lượng User và hiệu suất tăng tốc hệ thống (Cache Hit Rate).
    *   *Hiện trạng AI Modules:* Giám sát trạng thái hoạt động (Production Active) và chỉ số hiệu năng (F1 Score, Accuracy) của toàn bộ 6 lõi AI (WORD, EXCEL, PDF, HTML, PE Win32, PE Win64).
    *   *Biểu đồ phân tích:* Trực quan hóa phân bố trạng thái file và quản lý tập trung lịch sử lỗi hệ thống (System Error Logs) được ẩn an toàn trên EFS.
*   **Quản trị Người dùng & Tối ưu Chi phí:** Phân quyền (Nâng cấp Admin/User). Khi xóa tài khoản người dùng, hệ thống kích hoạt **Garbage Collection** — tự động dò quét trên EFS để dọn sạch sẽ các file vật lý rác mà User đó từng tải lên (nếu không còn tham chiếu chéo), giúp tối ưu hóa chi phí lưu trữ AWS.
*   **Quản trị Vòng đời AI (MLOps Management):** Kiểm soát khép kín quy trình: *Thu thập Data → Training → Staging → Production*.
    *   *Thu thập Dữ liệu (Data Ingestion):* Triển khai "Thợ săn tự động" (PE Hunter) càn quét Data Lake (MalwareBazaar) để thu thập mẫu mới khi AI dự đoán sai. Hỗ trợ nạp file thủ công và theo dõi trực quan tiến độ gom mẫu.
    *   *Huấn luyện Mô hình (Training):* Tự động dọn dẹp dữ liệu trùng lặp (chống học vẹt). Hỗ trợ huấn luyện kết hợp Dataset gốc với dữ liệu mới, hoặc học tăng cường (Incremental Learning) để sinh ra model ưu việt hơn.
    *   *Kiểm thử (Staging Test):* Cung cấp môi trường thử nghiệm model mới (hỗ trợ test hàng loạt) trước khi đưa ra thực tế.
    *   *Quản lý Phiên bản (Model History):* Quản lý trạng thái model (Production, Staging, Trash). Cho phép khôi phục model từ thùng rác hoặc xóa vĩnh viễn.
*   **Kết quả nhận được:** Quyền kiểm soát tối cao chuẩn SOC Platform, cho phép Admin vận hành, thu thập dữ liệu và liên tục cải tiến trí tuệ nhân tạo (Retrain AI) trực tiếp trên Web mà không cần can thiệp mã nguồn.

## Video demo


<iframe src="https://drive.google.com/file/d/1AKdMJN-z_w3wlmlskxMsq_m7E3x4hzEj/preview" width="100%" height="480" allow="autoplay" style="border: none;"></iframe>
