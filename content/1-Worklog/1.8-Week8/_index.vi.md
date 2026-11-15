---
title: "Worklog Tuần 8"
date: 2026-11-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

- Tiếp tục hoàn thiện giao diện và các chức năng đã chuẩn bị từ tuần 7.
- Tìm hiểu cách tiếp nhận triệu chứng, lưu nội dung trao đổi theo từng phiên và hiển thị lại thông tin cho người dùng.
- Thực hành đọc đơn thuốc, kết quả xét nghiệm từ ảnh và đưa thông tin vào hồ sơ cá nhân.
- Rà soát cách trình bày trang chat, hồ sơ và danh sách cơ sở y tế để người dùng dễ theo dõi hơn.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Xem lại giao diện đã dựng ở tuần 7 và liệt kê các phần cần chỉnh sửa.<br>- Điều chỉnh màu sắc, biểu tượng và cách hiển thị hồ sơ khi người dùng đăng nhập.<br>- Tìm hiểu cách phân biệt thông tin của người đang sử dụng với dữ liệu minh họa trong giao diện. | 02/11/2026 | 02/11/2026 | [Giao diện dự án](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html) |
| 3 | - Tìm hiểu các bước xử lý một ảnh đơn thuốc hoặc phiếu xét nghiệm: nhận ảnh, đọc nội dung và đưa các trường cần thiết ra giao diện.<br>- Thực hành đối chiếu ngày sinh, giới tính và cách tính tuổi từ thông tin đã đọc được.<br>- Kiểm tra những trường hợp dữ liệu thiếu hoặc đọc sai để không hiển thị nhầm trong hồ sơ. | 03/11/2026 | 03/11/2026 | [Luồng OCR](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/ocr_parallel_service.py); [Xử lý đơn thuốc](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/prescription_service.py) |
| 4 | - Tiếp tục xây dựng phần hỏi thông tin triệu chứng ban đầu và cửa sổ chat nhỏ trên trang.<br>- Tìm hiểu cách giữ nội dung trao đổi theo từng phiên; sửa trường hợp người dùng nói “không có triệu chứng” nhưng chương trình lại ghi nhận là có.<br>- Chỉnh bố cục trang chủ, hồ sơ và trang cơ sở y tế; kiểm tra việc chuyển giữa các tab. | 04/11/2026 | 04/11/2026 | [Xử lý tiếp nhận](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/intake_service.py); [ghi chú chatbot](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md) |
| 5 | - Thực hành lưu đơn thuốc và kết quả xét nghiệm đã xử lý vào hồ sơ của người dùng.<br>- Bổ sung danh sách lịch sử để có thể xem lại tài liệu cũ.<br>- Kiểm tra dữ liệu được gắn với đúng tài khoản khi đăng nhập, tải lại trang hoặc chuyển phiên. | 05/11/2026 | 05/11/2026 | [Mã nguồn ứng dụng](https://github.com/khiemdong2005/chatbot_medical/blob/main/app.py) |
| 6 | - Xem lại giao diện trang chat và cách sắp xếp khu vực câu hỏi, câu trả lời.<br>- Điều chỉnh màu chữ, khoảng cách và biểu tượng để nội dung dễ đọc trong chế độ sáng và tối.<br>- So sánh cách hiển thị giữa trang chat chính và cửa sổ chat nhỏ. | 06/11/2026 | 06/11/2026 | [Giao diện](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html); [JavaScript](https://github.com/khiemdong2005/chatbot_medical/blob/main/static/js/app.js) |
| 7 | - Hoàn thiện phần tìm kiếm cơ sở y tế và xem vị trí trên bản đồ.<br>- Chỉnh thanh tìm kiếm, thẻ thông tin và nút mở bản đồ để thao tác rõ ràng hơn.<br>- Kiểm tra lỗi bố cục khiến nội dung của các tab ảnh hưởng lẫn nhau. | 07/11/2026 | 07/11/2026 | [Giao diện dự án](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html) |
| Chủ nhật | - Rà soát lại quá trình trao đổi của người dùng từ bước khai triệu chứng đến lúc xem tóm tắt.<br>- Điều chỉnh để người dùng xem và xác nhận trước khi lưu bản tóm tắt tư vấn.<br>- Sửa mẫu email mã xác thực và một số vấn đề khi xem lại lịch sử chat. | 08/11/2026 | 08/11/2026 | [Ghi chú chatbot](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md) |

### Kết quả đạt được tuần 8:

- Hiểu rõ hơn cách tổ chức một luồng sử dụng từ lúc người dùng nhập triệu chứng đến khi xem lại nội dung đã trao đổi.
- Thực hành đọc thông tin từ đơn thuốc và kết quả xét nghiệm, đồng thời biết cần kiểm tra lại các trường dữ liệu trước khi đưa vào hồ sơ.
- Biết cách lưu tài liệu theo tài khoản và hiển thị lịch sử để người dùng có thể tra cứu lại.
- Nhận ra việc ghi nhận đúng câu phủ định trong lời khai là cần thiết; nếu bỏ qua từ “không”, thông tin triệu chứng có thể bị hiểu sai.
- Hoàn thiện thêm giao diện chat, hồ sơ và trang cơ sở y tế. Các phần này đã có cách trình bày thống nhất hơn so với tuần trước.
- Tìm hiểu thêm về quyền kiểm soát thông tin cá nhân: bản tóm tắt tư vấn cần được người dùng xem và xác nhận trước khi lưu.
