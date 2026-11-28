---
title: "Nhật ký công việc tuần 9"
date: 2026-11-09
weight: 9
chapter: false
pre: "<b>1.9.</b> "
---

### Mục tiêu tuần 9:

- Chạy thử ứng dụng bằng Flask và Docker Compose, kiểm tra lỗi truy cập trên môi trường cục bộ.
- Xây dựng mục Dinh dưỡng và dùng pytest để kiểm tra bộ lọc món ăn khi chọn nhiều bệnh nền.
- Chuẩn hóa công thức từ ViFoodRec và Wikibooks bằng Python, xuất danh mục JSON và kiểm tra ảnh món ăn.
- Đánh giá khả năng tìm tài liệu tiếng Anh trong ChromaDB từ câu hỏi tiếng Việt và kiểm tra câu trả lời của Gemini.
- Rà soát luồng đọc đơn thuốc và cải thiện giao diện bản đồ Cơ sở y tế dùng Google Maps.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Khởi chạy bản web tuần trước bằng Flask trên môi trường local và kiểm tra khả năng truy cập qua trình duyệt. Máy chủ Flask báo đã khởi động, nhưng trình duyệt không tải được giao diện.</li><li>Thay đổi cổng lắng nghe của Flask và thử truy cập lại để kiểm tra khả năng xung đột cổng. Lỗi truy cập vẫn xảy ra trên cổng mới.</li></ul> | 09/11/2026 | 09/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 3 | <ul><li>Phương án ban đầu chưa triển khai được, nên tôi bổ sung ý tưởng Dinh dưỡng và đưa mục này lên giao diện thay cho màn hình hồ sơ cũ.</li><li>Dựng phần nhập bệnh nền, gợi ý món và theo dõi thói quen. Rà lại để bỏ các nút và phần hiển thị còn sót của màn hình cũ.</li></ul> | 10/11/2026 | 10/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 4 | <ul><li>Nhập bảng công thức ViFoodRec và dùng script Python để thu thập thêm dữ liệu từ Wikibooks. Lọc các dòng không phù hợp, tách nguyên liệu và cách nấu, rồi xuất dữ liệu JSON cho danh mục món.</li><li>Rà soát các ảnh món ăn hiển thị lỗi, thay thế tệp ảnh trong kho mã nguồn và cập nhật đường dẫn để giao diện tải ảnh từ thư mục tài nguyên tĩnh.</li><li>Điều chỉnh quy tắc lọc món ăn theo bệnh nền bằng Python và bổ sung ca kiểm thử bằng pytest để xác nhận bộ lọc áp dụng đồng thời các ràng buộc khi người dùng chọn nhiều bệnh nền.</li></ul> | 11/11/2026 | 11/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 5 | <ul><li>Rà mã nguồn và thử mở đơn thuốc ở màn hình điền sẵn thông tin. Ghi lại trường hợp hệ thống đọc sai tên thuốc để sửa tiếp.</li><li>Thử mở rộng câu hỏi tiếng Việt để tìm tài liệu tiếng Anh trong ChromaDB. Dùng bộ câu hỏi mẫu để so sánh kết quả và tham khảo cách Amazon Bedrock Evaluations tách phần tìm tài liệu khỏi phần trả lời.</li><li>Xử lý lỗi xác thực Gemini và chạy bộ đánh giá câu trả lời, sau đó đồng bộ trang Cơ sở y tế vào bản đang làm.</li></ul> | 12/11/2026 | 12/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/3361426ea733e4d1b9de3ac85419200c8c366670)<br>[AWS Bedrock RAG Evaluations](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-evaluation-metrics.html) |
| 6 | <ul><li>Dùng Docker Compose để thử build và chạy ứng dụng. Bổ sung thời gian chờ, cách thử lại và phản hồi dự phòng khi dịch vụ ngoài gặp lỗi.</li><li>Chỉnh màu ở trang Cơ sở y tế, khôi phục Google Maps và sửa khung thông tin khi bấm chọn một địa điểm.</li><li>Rà lại giao diện, ghi các lỗi còn gặp ở cảnh báo, kết quả đọc đơn thuốc và phần hiển thị tóm tắt. Sắp xếp lại thư mục tài liệu trong repo.</li><li>Tìm hiểu cách đặt điểm cơ sở y tế theo tọa độ bằng Google Maps Platform API và giới hạn khóa API của trình duyệt theo tên miền.</li></ul> | 13/11/2026 | 13/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |

### Kết quả đạt được tuần 9:

- Tái hiện được lỗi truy cập bản web cục bộ. Flask báo đã khởi động, nhưng trình duyệt vẫn không tải được trang sau khi đổi cổng.
- Tích hợp mục Dinh dưỡng vào giao diện với phần nhập bệnh nền, gợi ý món ăn và theo dõi thói quen. Đã dọn các thành phần còn sót của màn hình Hồ sơ cũ.
- Xuất danh mục công thức ViFoodRec và Wikibooks thành JSON, với nguyên liệu và cách nấu được tách riêng. Đã thay ảnh lỗi và cập nhật đường dẫn ảnh cục bộ.
- Cập nhật quy tắc lọc món ăn bằng Python và bổ sung ca kiểm thử pytest cho trường hợp áp dụng đồng thời các ràng buộc của nhiều bệnh nền.
- Có bộ câu hỏi mẫu và báo cáo so sánh kết quả truy xuất tài liệu tiếng Anh trong ChromaDB từ câu hỏi tiếng Việt. Đã xử lý lỗi xác thực Gemini và chạy bộ đánh giá câu trả lời.
- Ghi nhận trường hợp đọc sai tên thuốc khi điền sẵn thông tin đơn thuốc, cùng các lỗi còn gặp ở phần hiển thị cảnh báo, kết quả đọc đơn và bản tóm tắt.
- Chạy thử quy trình dựng và khởi động ứng dụng bằng Docker Compose. Bổ sung thời gian chờ, cơ chế thử lại và phản hồi dự phòng khi dịch vụ bên ngoài gặp lỗi.
- Khôi phục Google Maps trên trang Cơ sở y tế, chỉnh màu và khung chi tiết khi chọn địa điểm. Đã sắp xếp lại thư mục tài liệu trong kho mã nguồn.
