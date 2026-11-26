---
title: "Worklog Tuần 8"
date: 2026-11-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
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
| 2 | - Xem lại cấu trúc trang và các thành phần giao diện đã dựng ở tuần 7.<br>- Chỉnh bố cục, màu sắc và biểu tượng ở trang chủ, hồ sơ; kiểm tra giao diện thay đổi như thế nào khi người dùng đăng nhập.<br>- Tìm hiểu cách tách dữ liệu minh họa ra khỏi dữ liệu của tài khoản thật. | 02/11/2026 | 02/11/2026 | Dự án |
| 3 | - Tìm hiểu luồng xử lý giữa Front-end và Back-end khi người dùng tải ảnh đơn thuốc hoặc phiếu xét nghiệm.<br>- Kiểm tra cách Back-end đọc dữ liệu, trả các trường cần thiết và cách Front-end nhận, hiển thị kết quả.<br>- Bổ sung việc đối chiếu ngày sinh, giới tính và hiển thị tuổi từ dữ liệu đã đọc. | 03/11/2026 | 03/11/2026 | Dự án |
| 4 | - Xây dựng phần giao diện nhập thông tin ban đầu và cửa sổ chat nhỏ.<br>- Tìm hiểu cách lưu trạng thái của một phiên trao đổi để dữ liệu không bị mất khi chuyển giữa các màn hình.<br>- Sửa cách ghi nhận câu phủ định và kiểm tra thông tin Front-end gửi lên có khớp với dữ liệu Back-end lưu lại hay không. | 04/11/2026 | 04/11/2026 | Dự án |
| 5 | - Tìm hiểu cách tổ chức dữ liệu hồ sơ theo từng tài khoản.<br>- Kết nối kết quả xử lý tài liệu với phần lưu trữ và danh sách lịch sử trên giao diện.<br>- Kiểm tra trường hợp tải lại trang hoặc chuyển tài khoản để tránh hiển thị nhầm dữ liệu. | 05/11/2026 | 05/11/2026 | Dự án |
| 6 | - Rà soát cách bố trí tin nhắn, ô nhập và các nút trên trang chat.<br>- Chỉnh khoảng cách, độ tương phản và biểu tượng trong giao diện sáng, tối.<br>- Đối chiếu cách hiển thị giữa trang chat chính và cửa sổ chat nhỏ để người dùng không bị thay đổi cách thao tác.<br>- Tìm hiểu Amazon Transcribe Medical: phân biệt lời đọc chính tả với hội thoại bác sĩ - bệnh nhân và cách gắn nhãn người nói trong bản chép lời. | 06/11/2026 | 06/11/2026 | Dự án; [AWS Transcribe Medical](https://docs.aws.amazon.com/transcribe/latest/dg/how-it-works-med.html); [Speaker diarization](https://docs.aws.amazon.com/transcribe/latest/dg/conversation-diarization-med.html) |
| 7 | - Tiếp tục hoàn thiện giao diện tìm kiếm cơ sở y tế và bản đồ.<br>- Kiểm tra sự kiện khi người dùng chọn một cơ sở, mở bản đồ hoặc chuyển tab.<br>- Sửa các phần tử bị lệch và lỗi bố cục khiến nội dung của tab này ảnh hưởng sang tab khác. | 07/11/2026 | 07/11/2026 | Dự án |

### Kết quả đạt được tuần 8:

- Hiểu rõ hơn vai trò của Front-end và Back-end: Front-end tiếp nhận thao tác, gửi dữ liệu và hiển thị kết quả; Back-end kiểm tra, xử lý và lưu thông tin.
- Thực hành kết nối một chức năng từ giao diện tới phần xử lý phía sau, đặc biệt là luồng tải ảnh và hiển thị dữ liệu đã đọc.
- Biết cách theo dõi trạng thái đăng nhập, phiên trao đổi và dữ liệu của từng người dùng khi chuyển trang hoặc tải lại.
- Tìm hiểu thêm cách tổ chức dữ liệu hồ sơ và lịch sử để thông tin được gắn với đúng tài khoản.
- Cải thiện khả năng sử dụng của giao diện qua việc chỉnh bố cục chat, màu chữ, biểu tượng, điều hướng tab và bản đồ.
- Nhận thấy việc kiểm tra dữ liệu ở cả hai phía là cần thiết: dữ liệu đọc từ ảnh có thể thiếu, còn thông tin người dùng nhập có thể bị hiểu sai nếu không xử lý đúng câu phủ định.
- Biết Amazon Transcribe Medical hỗ trợ chuyển lời nói y tế thành văn bản và có thể phân biệt lượt nói. Do tài liệu dịch vụ tập trung vào tiếng Anh, tôi chỉ tìm hiểu để tham khảo hướng nhập liệu bằng giọng nói, chưa tích hợp vào giao diện.
