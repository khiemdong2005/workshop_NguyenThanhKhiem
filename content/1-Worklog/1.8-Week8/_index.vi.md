---
title: "Nhật ký công việc tuần 8"
date: 2026-11-02
weight: 8
chapter: false
pre: "<b>1.8.</b> "
---

### Mục tiêu tuần 8:

- Tiếp tục xây dựng Front-end và Back-end từ phần khung đã chuẩn bị ở tuần 7.
- Tìm hiểu cách một thao tác trên giao diện được gửi đến Back-end, xử lý rồi trả kết quả về Front-end.
- Thực hành quản lý trạng thái giao diện, phiên làm việc và dữ liệu gắn với tài khoản người dùng.
- Tìm hiểu cách chuyển lời nói trong hội thoại y tế thành văn bản để so sánh với luồng nhập chữ hiện tại.
- Rà soát bố cục, màu sắc và cách điều hướng để các trang trong ứng dụng thống nhất hơn.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Chỉnh HTML và Tailwind CSS để đổi giao diện sang tông sáng, thay biểu tượng và sắp lại màn hình hồ sơ sau đăng nhập.</li></ul> | 02/11/2026 | 02/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/d97eaf3e6ac6e50c0ea84a6aecea89561bba62e5) |
| 3 | <ul><li>Đưa thiết kế mới lên web và xem lại cách chatbot tra cứu tài liệu trước khi trả lời. Lên hướng cho luồng hỏi bệnh và tóm tắt trước khám.</li><li>Nối phần đọc ảnh đơn thuốc và phiếu xét nghiệm viết bằng Python với giao diện JavaScript. Đối chiếu ngày sinh, giới tính và hiển thị tuổi từ dữ liệu đọc được. Bỏ trường mã BHYT khỏi màn hình kết quả.</li><li>Ghi lại các điểm cần chỉnh ở chatbot: phản hồi ngắn hơn, lịch sử dễ mở lại và cửa sổ chat nhỏ dùng được khi chuyển tab.</li></ul> | 03/11/2026 | 03/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/4b2a5c4ff90749b91d639b8e2fb832dec6a09bb3) |
| 4 | <ul><li>Sửa lỗi JavaScript khiến người dùng không chuyển được tab. Chỉnh lại Trang chủ, hồ sơ và cửa sổ chat nhỏ cho cùng kiểu giao diện.</li><li>Đơn giản hóa trang hồ sơ, bỏ các ô CCCD và BHYT khỏi biểu mẫu này. Thêm nút ẩn hoặc hiện số điện thoại và email.</li><li>Bố trí lại trang Cơ sở y tế thành hai cột và chỉnh các biểu tượng khó nhìn.</li><li>Làm luồng hỏi bệnh ban đầu và viết bài kiểm thử bằng pytest. Sửa cách ghi nhận khi người dùng phủ nhận triệu chứng, lưu phiên trao đổi và tách hồ sơ mẫu khỏi dữ liệu tài khoản. Ghi lại trường hợp mở sai bản tóm tắt để kiểm tra tiếp.</li><li>Cập nhật chỉ mục tra cứu tài liệu của chatbot.</li></ul> | 04/11/2026 | 04/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/d991d39976a2a53e86887b4158f0ba9e9007f4aa) |
| 5 | <ul><li>Dùng Flask, SQLAlchemy và SQLite để lưu kết quả đọc đơn thuốc và phiếu xét nghiệm vào đúng hồ sơ người dùng. Thêm danh sách lịch sử và phần tóm tắt để người dùng mở lại thông tin đã lưu.</li><li>Sắp xếp lại thư mục báo cáo workshop và chạy Hugo để xem bản Việt và Anh.</li></ul> | 05/11/2026 | 05/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/57609455992883a7f00d25d97c4e8979193abdb7) |
| 6 | <ul><li>Chỉnh trang chatbot theo mẫu tông xanh, tăng độ tương phản của chữ và nút. Bỏ nút 115 bị trùng trên giao diện và thay các biểu tượng còn lệch kiểu.</li><li>Đọc tài liệu Amazon Transcribe Medical để xem cách dịch vụ gắn nhãn người nói trong hội thoại y tế.</li></ul> | 06/11/2026 | 06/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/44ddf49a46f3d13e2c06d4de5e3ef69eac847f62)<br>[AWS Transcribe Medical](https://docs.aws.amazon.com/transcribe/latest/dg/how-it-works-med.html)<br>[Speaker diarization](https://docs.aws.amazon.com/transcribe/latest/dg/conversation-diarization-med.html) |
| 7 | <ul><li>Rà quyền truy cập phiên hỏi bệnh, tình trạng khách chưa đăng nhập và bố cục trên điện thoại. Bổ sung kiểm tra quyền xem dữ liệu của từng tài khoản và các bài test liên quan.</li><li>Chỉnh trang Cơ sở y tế để bản đồ Leaflet hiện sẵn với nền OpenStreetMap. Sửa nút mở bản đồ và màu chữ khó đọc trên banner.</li><li>Sửa lỗi HTML làm các thẻ Khám phá của Trang chủ xuất hiện khi chuyển sang tab khác.</li><li>Cập nhật chỉ mục ChromaDB để chatbot tra cứu tài liệu.</li></ul> | 07/11/2026 | 07/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/3f8fdf77be4d18171e310d8650a9d687fea09b26) |

### Kết quả đạt được tuần 8:

- Xong phần đọc và lưu tài liệu theo tài khoản ở bản hiện tại. Người dùng tải ảnh đơn thuốc hoặc phiếu xét nghiệm, xem kết quả trên màn hình rồi mở lại trong mục lịch sử.
- Chỉnh được giao diện sáng cho Trang chủ, hồ sơ và trang chat theo bố cục đã thử.
- Sửa cách chatbot ghi nhận câu phủ định và giữ phiên hỏi bệnh khi người dùng đổi màn hình.
- Bổ sung kiểm tra quyền truy cập hồ sơ và phiên hỏi bệnh của từng tài khoản.
- Sửa được lỗi thẻ Trang chủ hiện sang tab khác và chỉnh cách mở bản đồ cơ sở y tế.
- Tìm hiểu cách Amazon Transcribe Medical tách lượt nói. Phần nhập liệu giọng nói vẫn ở mức tham khảo.
