---
title: "Nhật ký công việc tuần 10"
date: 2026-11-16
weight: 10
chapter: false
pre: "<b>1.10.</b> "
---

### Mục tiêu tuần 10:

- Chuyển chatbot từ Gemini sang Groq cho tác vụ văn bản và khảo sát OpenRouter cùng Amazon Bedrock.
- Làm lại luồng OCR đơn thuốc để mô hình thị giác xử lý ảnh toàn đơn và vùng chữ rõ.
- Tích hợp OTP đăng ký qua Gmail SMTP và SpeedSMS.
- Hoàn thiện bản đồ Cơ sở y tế và kết nối tóm tắt tiền khám với tính năng đặt lịch.
- Cập nhật bộ lọc thực đơn và củng cố kiểm thử ngoại tuyến trên CI.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Đồng bộ màn hình đo lại OCR, trích xuất ngày sinh và tuổi rồi đưa vào dữ liệu số hóa đơn thuốc.</li><li>Rà soát kiểm thử ngoại tuyến và đồng bộ phiên bản FastAPI, Starlette theo tệp khóa phụ thuộc trong CI.</li><li>Đọc tài liệu Amazon Bedrock Runtime và so sánh ba cách gọi mô hình. Converse nhận dữ liệu hội thoại, ConverseStream trả kết quả theo luồng và InvokeModel nhận định dạng đầu vào riêng của mô hình.</li></ul> | 16/11/2026 | 16/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical)<br>[Amazon Bedrock Runtime](https://docs.aws.amazon.com/bedrock/latest/userguide/conversation-inference.html) |
| 3 | <ul><li>Tích hợp cập nhật OTP đăng ký từ nhánh nhóm, gồm sửa lỗi trạng thái tài khoản, gửi mã qua Gmail SMTP và chuyển cấu hình SMS sang SpeedSMS.</li><li>Đồng bộ cấu hình các mô hình OpenRouter và bổ sung pytest-cov vào bộ phụ thuộc kiểm thử từ các thay đổi của nhóm.</li><li>Chỉnh giao diện đăng nhập và cập nhật quy tắc tránh trùng nguyên liệu ở món phụ.</li><li>Tìm hiểu luồng Google OAuth 2.0, gồm bước chuyển sang Google và nhận phản hồi qua địa chỉ callback. Xem cách backend gửi mã OTP qua Gmail SMTP.</li></ul> | 17/11/2026 | 17/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 4 | <ul><li>Làm lại bước chuẩn bị ảnh OCR để gửi đồng thời ảnh toàn đơn và vùng chữ rõ cho mô hình thị giác. Ảnh toàn đơn giữ bố cục, ảnh cắt giúp đọc tên thuốc và hàm lượng.</li><li>Tham khảo cách tính chi phí Bedrock, tách token của chatbot (gồm lịch sử hội thoại và đoạn tài liệu RAG) khỏi chi phí xử lý ảnh đơn thuốc.</li></ul> | 18/11/2026 | 18/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical)<br>[Amazon Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/) |
| 5 | <ul><li>Hiệu chỉnh ca OCR đọc sai tên thuốc và bổ sung bước xóa ảnh cắt tạm sau khi xử lý.</li><li>Chỉnh cách ghép thực đơn ba món, tách món mặn dùng riêng khỏi món tráng miệng và cập nhật quy tắc lọc dinh dưỡng.</li><li>Thêm cấu hình mô hình mặc định cho luồng dinh dưỡng khi chạy kiểm thử ngoại tuyến trên CI.</li></ul> | 19/11/2026 | 19/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 6 | <ul><li>Chuyển tác vụ văn bản của chatbot từ Gemini sang Groq trên bản tích hợp của nhóm. Giữ cấu hình mô hình thị giác riêng cho luồng đọc ảnh đơn thuốc.</li><li>Đồng bộ thay đổi tách route Flask từ app.py thành năm mô-đun, giữ nguyên URL và tên endpoint hiện có.</li><li>Tích hợp luồng đặt lịch vào trang Cơ sở y tế, đưa nút <strong>Lịch hẹn của tôi</strong> vào giao diện, bổ sung nhãn trợ năng cho biểu mẫu và chuyển bản tóm tắt tiền khám sang bước đặt hẹn.</li><li>Tính thử lượng token cho 1.000 lượt gọi chatbot. Với giả định mỗi lượt dùng 1.200 token đầu vào và 300 token đầu ra, tổng lần lượt là 1,2 triệu và 300.000 token.</li><li>Tham khảo các tiêu chí chọn mô hình qua Groq API, gồm loại đầu vào hỗ trợ, giới hạn lượt gọi và cấu hình cho chatbot văn bản hoặc OCR ảnh.</li></ul> | 20/11/2026 | 20/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical)<br>[Amazon Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/) |
| 7 | <ul><li>Hoàn thiện cấu hình tải bản đồ Cơ sở y tế bằng cách cập nhật Content Security Policy (CSP) để cho phép nguồn tài nguyên ArcGIS và CDN ô bản đồ.</li><li>Bổ sung chế độ hỏi đáp nhanh cho các câu hỏi thông tin.</li><li>Tham dự AWS Student Community Day và ghi lại các nội dung về phân vùng mạng, kiểm tra kết nối và bảo mật nhiều lớp.</li></ul> | 21/11/2026 | 21/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical)<br>[Báo cáo Event 6](../../4-eventparticipated/4.6-event6/) |

### Kết quả đạt được tuần 10:

- Chatbot dùng Groq cho tác vụ văn bản và luồng OCR có cấu hình mô hình thị giác riêng. Đã khảo sát OpenRouter, các cách gọi Bedrock Runtime và lập ví dụ ước tính token.
- Luồng OCR gửi được ảnh toàn đơn cùng vùng chữ rõ, trích xuất thêm ngày sinh và tuổi, xử lý một ca đọc sai tên thuốc và dọn ảnh cắt tạm.
- Tích hợp OTP đăng ký với Gmail SMTP và SpeedSMS. Bản tích hợp có cập nhật xử lý trạng thái tài khoản khi đăng ký.
- Hoàn thiện bản đồ Cơ sở y tế với cấu hình CSP cho ArcGIS và CDN. Luồng đặt lịch nhận bản tóm tắt tiền khám, có mục Lịch hẹn của tôi và nhãn trợ năng trên biểu mẫu.
- Cập nhật cách ghép thực đơn ba món, quy tắc lọc dinh dưỡng và cấu hình dự phòng cho kiểm thử ngoại tuyến.
- Đồng bộ các cập nhật của nhóm gồm năm mô-đun route Flask và pytest-cov. Cập nhật FastAPI và Starlette trong CI theo tệp khóa phụ thuộc.
- Ghi lại nội dung về phân vùng mạng và kiểm tra kết nối sau AWS Student Community Day. [Báo cáo Event 6](../../4-eventparticipated/4.6-event6/)
