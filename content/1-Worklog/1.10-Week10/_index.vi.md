---
title: "Nhật ký công việc tuần 10"
date: 2026-11-16
weight: 10
chapter: false
pre: "<b>1.10.</b>"
---

**Thời gian** — 16–21/11/2026.

## Mục tiêu

Tiếp nối tuần 9, tuần này tập trung sửa các luồng OCR, gợi ý bữa ăn và bản đồ cơ sở y tế, đồng thời hoàn thiện xác thực OTP và tích hợp tóm tắt tiền khám vào quy trình đặt lịch.

## Công việc theo ngày

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ Hai | - **Gọi mô hình cho chatbot.** Tìm hiểu `Converse` để gửi hội thoại theo cấu trúc `messages`, `ConverseStream` để nhận phản hồi từng phần và `InvokeModel` cho trường hợp cần định dạng đầu vào riêng của mô hình. Khi đánh giá phương án tích hợp, các thông tin cần kiểm tra gồm `modelId`, Region, quyền IAM và loại dữ liệu mà mô hình hỗ trợ. | 16/11/2026 | 16/11/2026 | [Bedrock Runtime API](https://docs.aws.amazon.com/bedrock/latest/userguide/conversation-inference.html) |
| Thứ Ba | - Sửa lỗi đăng ký OTP liên quan đến trạng thái tài khoản, cập nhật luồng gửi mã qua Gmail SMTP và chuyển cấu hình SMS sang SpeedSMS.<br>- Thêm `pytest-cov` vào bộ phụ thuộc kiểm thử.<br>- Đưa các mô hình OpenRouter vào cấu hình dự phòng cho các tính năng AI (`015ffc0`). | 17/11/2026 | 17/11/2026 | `8b4fd5a`, `015ffc0`, `a76d732` |
| Thứ Tư | - Cập nhật luồng OCR để mô hình thị giác nhận cả ảnh toàn đơn và vùng chữ rõ.<br>- Ảnh toàn đơn giữ ngữ cảnh bố cục, còn ảnh cắt hỗ trợ đọc tên thuốc và hàm lượng.<br>- **Đọc bảng giá suy luận.** Đối với mô hình văn bản tính tiền theo token, cần tra riêng đơn giá token đầu vào và đầu ra theo mô hình, Region và chế độ sử dụng. Với luồng RAG, đầu vào còn có thể gồm lịch sử hội thoại và các đoạn tài liệu truy xuất được. Với OCR, cần xem cách tính riêng cho ảnh của mô hình được chọn. | 18/11/2026 | 18/11/2026 | `d239a92` · [Amazon Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/) |
| Thứ Năm | - Chỉnh thực đơn ba món, tách món mặn dùng riêng khỏi món tráng miệng và cập nhật bộ lọc liên quan đến gout và chất béo.<br>- Sửa trường hợp OCR đọc sai Banitase và bổ sung dọn ảnh cắt tạm.<br>- Thêm mô hình mặc định cho luồng dinh dưỡng để môi trường CI có cấu hình dự phòng (`fd6b991`). | 19/11/2026 | 19/11/2026 | `8a4cd9d`, `03bd37a` |
| Thứ Sáu | - Tách các route từ `app.py` thành năm mô-đun theo chức năng, giữ URL và tên endpoint hiện có.<br>- Tích hợp Groq cho tác vụ văn bản và giữ cấu hình mô hình thị giác riêng cho OCR.<br>- Đưa nút Lịch hẹn của tôi vào giao diện cơ sở y tế và thêm nhãn trợ năng cho các trường của biểu mẫu đặt lịch (`14abf71`, `731e869`).<br>- **Lập cách ước tính cho dự án.** Ví dụ, 1.000 lượt gọi với trung bình 1.200 token đầu vào và 300 token đầu ra tương ứng 1,2 triệu token đầu vào và 0,3 triệu token đầu ra. Nhân mỗi phần với đơn giá tương ứng rồi cộng lại để ước tính chi phí văn bản. Nếu dùng thêm Knowledge Bases hoặc Guardrails, cần dự toán riêng theo cách tính của từng tính năng. Các con số trên là giả định minh họa. | 20/11/2026 | 20/11/2026 | `61bdac6`, `00c06b6`, `4b09a1b` · [Amazon Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/) |
| Thứ Bảy | - Cập nhật chính sách CSP để bản đồ tải được tài nguyên từ ArcGIS và CDN bản đồ.<br>- Tham dự AWS Student Community Day và ghi lại các ý chính về bảo mật mạng nhiều lớp. | 21/11/2026 | 21/11/2026 | `3a5f359` · [Báo cáo Event 6](../../4-eventparticipated/4.6-event6/) |

## Kết quả đạt được tuần 10

- **Amazon Bedrock API và chi phí.** Phân biệt cách gửi hội thoại với `Converse`, nhận phản hồi từng phần với `ConverseStream` và gọi mô hình theo định dạng riêng với `InvokeModel`. Xác định các thông tin cần kiểm tra khi tích hợp gồm mã mô hình, Region, quyền IAM và loại đầu vào. Lập ví dụ dự toán 1.000 lượt gọi từ đơn giá token đầu vào và đầu ra. Đây là kết quả khảo sát tài liệu và bảng giá.
- **Xác thực OTP và kiểm thử.** Sửa lỗi trạng thái tài khoản khi đăng ký bằng OTP, cập nhật gửi mã qua Gmail SMTP và cấu hình SpeedSMS. Bổ sung `pytest-cov` vào bộ phụ thuộc kiểm thử.
- **OCR đơn thuốc.** Cập nhật yêu cầu gửi cho mô hình thị giác để có cả ảnh toàn đơn và vùng chữ rõ. Ảnh toàn đơn giữ ngữ cảnh bố cục, còn ảnh cắt hỗ trợ đọc tên thuốc và hàm lượng. Sửa trường hợp đọc sai Banitase và dọn ảnh cắt tạm sau xử lý.
- **Gợi ý bữa ăn.** Chỉnh cách tạo thực đơn ba món, phân biệt món mặn dùng riêng với món tráng miệng, cập nhật bộ lọc liên quan đến gout và chất béo. Bổ sung cấu hình mô hình mặc định cho luồng dinh dưỡng trong CI.
- **Tổ chức backend và cấu hình AI.** Tách các route từ `app.py` thành năm mô-đun theo chức năng, giữ URL và tên endpoint hiện có. Thêm Groq cho tác vụ văn bản và dùng cấu hình mô hình thị giác riêng cho OCR ảnh.
- **Cơ sở y tế và đặt lịch.** Đưa nút Lịch hẹn của tôi vào trang cơ sở y tế, thêm nhãn trợ năng cho các trường đặt lịch và cập nhật CSP để bản đồ tải được tài nguyên từ ArcGIS và CDN bản đồ.
- **Bài học từ AWS Student Community Day.** Ghi lại cách phân vùng hệ thống, giới hạn luồng kết nối cần thiết và kiểm tra lại kết nối sau khi thay đổi cấu hình. [Báo cáo Event 6](../../4-eventparticipated/4.6-event6/)
