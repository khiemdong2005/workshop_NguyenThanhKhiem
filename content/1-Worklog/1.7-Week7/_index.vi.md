---
title: "Nhật ký công việc tuần 7"
date: 2026-10-26
weight: 7
chapter: false
pre: "<b>1.7.</b> "
---

### Mục tiêu tuần 7:

- Dựng bản web đầu tiên và tích hợp chatbot nhận văn bản, ảnh và tài liệu tra cứu.
- Sửa luồng gửi ảnh và phát triển phần đọc đơn thuốc.
- Tìm hiểu PaddleOCR, TrOCR và cách gửi ảnh qua API để chọn hướng đọc đơn thuốc phù hợp với dự án.
- Rà đề xuất, dự toán chi phí và sơ đồ kiến trúc AWS.
- Tham gia AWS First Cloud AI Journey Community Day.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Đưa bản nền đầu tiên của ứng dụng lên repo. Bản này có giao diện web, hồ sơ sức khỏe điện tử (EHR), OCR đơn thuốc và sàng lọc triệu chứng.</li><li>Dùng Flask để xử lý yêu cầu và tách giao diện, phần hướng dẫn mô hình và logic sàng lọc thành các tệp riêng.</li><li>Tổ chức lại README của dự án.</li></ul> | 26/10/2026 | 26/10/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/bcde09c8f6a54244178c6bbb0b09d631b3c88a6a) |
| 3 | <ul><li>Bỏ bớt chức năng thừa rồi mở web chạy thử.</li><li>Cho chatbot nhận cả câu hỏi và ảnh bằng Gemini Vision. Nạp tài liệu y khoa để chatbot tìm nội dung liên quan trước khi trả lời (RAG) và thêm ảnh tham chiếu.</li><li>Thêm hai lớp kiểm tra phản hồi và cập nhật phần Việt–Anh cho luồng chatbot qua Flask và FastAPI.</li></ul> | 27/10/2026 | 27/10/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/474f6e62efc39933d3efde62f07a2b7e1c879abc) |
| 4 | <ul><li>Sửa nút đính kèm trong chat để người dùng mở được trình chọn ảnh.</li><li>Sửa luồng tiếp nhận ảnh da liễu, chuyển sang Gemini 3.1 Flash-Lite và thêm mô hình dự phòng.</li><li>Kiểm tra cách chạy FastAPI và xem API bằng Swagger, rồi rà nơi lưu thông tin tài khoản.</li><li>So sánh cách dùng PaddleOCR hoặc TrOCR để đọc chữ trên đơn với cách gửi ảnh cho mô hình qua API.</li><li>Dùng gợi ý từ UI/UX Pro Max để rà icon, đổi sang SVG phù hợp với giao diện y tế, dọn phần hiển thị chat và thêm mục theo dõi lịch dùng thuốc.</li></ul> | 28/10/2026 | 28/10/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/3ff6ec2aa3f2ea54cec086854d16bd2338c5cba6) |
| 5 | <ul><li>Bỏ đường dẫn tuyệt đối trong cấu hình và chuyển sang tìm .env từ thư mục gốc của dự án.</li><li>Thử luồng Hybrid OCR cho đơn thuốc: chỉnh ảnh trước, đọc chữ bằng OCR rồi đưa nội dung sang Gemini để phân tích.</li><li>Nối kết quả trích xuất với màn hình đơn thuốc, tinh gọn cách hiển thị và xử lý lỗi chuyển tab.</li><li>Đọc thêm tài liệu Amazon Comprehend Medical và ghi lại giới hạn với dữ liệu tiếng Việt.</li></ul> | 29/10/2026 | 29/10/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/5dbd223863df779f72717589e7074e27251c3d14)<br>[AWS Comprehend Medical](https://docs.aws.amazon.com/comprehend-medical/latest/dev/) |
| 6 | <ul><li>Thử nền tối rồi chuyển sang nền sáng với ảnh bệnh viện. Chỉnh thanh điều hướng và ba khung nội dung trên trang chính.</li><li>Rà lại các thành phần cần thể hiện trên sơ đồ AWS và đối chiếu với những phần đang có trong ứng dụng.</li><li>Cập nhật chỉ mục để chatbot tra cứu bộ tài liệu y khoa mới hơn.</li></ul> | 30/10/2026 | 30/10/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/cb34ab66e5765c7b1f2c507d891c4748774125eb) |
| 7 | <ul><li>Rà tiêu chí proposal và workshop, tập trung vào kiến trúc, demo và phần trình bày. Xem lại cách mô tả mô hình đọc đơn thuốc trong đề xuất.</li><li>Vẽ lại sơ đồ kiến trúc AWS theo khung 16:9 để trình chiếu, rồi xuất tệp SVG và PNG.</li><li>Tham gia AWS First Cloud AI Journey Community Day, nghe chia sẻ và giao lưu với cộng đồng FCAJ.</li></ul> | 31/10/2026 | 31/10/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/baa06e19ac20c41ca75a74bfecca16cf1b338561) |

### Kết quả đạt được tuần 7:

- Có bản web đầu tiên trên repo với các phần hồ sơ, đọc đơn thuốc và sàng lọc triệu chứng ở mức ban đầu.
- Nối được Gemini Vision với chatbot và dùng RAG để tìm tài liệu liên quan. Đến cuối tuần đã cập nhật chỉ mục vector.
- Sửa được nút mở trình chọn ảnh trong chat.
- Thử hướng Hybrid OCR để tách phần đọc chữ khỏi phần AI phân tích. PaddleOCR, TrOCR và Amazon Comprehend Medical nằm trong phần tìm hiểu.
- Chỉnh giao diện sang nền sáng và bố trí lại thanh điều hướng, các khung nội dung.
- Cập nhật proposal kèm dự toán chi phí AWS và xuất sơ đồ kiến trúc 16:9 dưới dạng SVG và PNG.
- Tham gia FCAJ Community Day ngày 31/10 và trao đổi với các thành viên.
