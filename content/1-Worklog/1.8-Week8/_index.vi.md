---
title: "Worklog Tuần 8"
date: 2026-11-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

- Tiếp nối phần giao diện và cấu trúc Backend đã chuẩn bị ở tuần 7 để xây dựng các luồng nghiệp vụ đầu tiên cho dự án MediMind AI.
- Tìm hiểu cách tiếp nhận thông tin triệu chứng theo từng phiên tư vấn, bảo toàn ngữ cảnh hội thoại và phân biệt dữ liệu người dùng khai báo với dữ liệu hệ thống suy ra.
- Thực hành trích xuất thông tin từ đơn thuốc, phiếu xét nghiệm; xác định cách lưu và hiển thị lại kết quả trong hồ sơ của đúng người dùng.
- Cải thiện khả năng sử dụng của giao diện chat, hồ sơ cá nhân và trang tìm kiếm cơ sở y tế trên cả chế độ sáng và tối.
- Rà soát vấn đề an toàn dữ liệu: quyền truy cập hồ sơ, sự đồng ý của người dùng trước khi lưu bản tóm tắt tư vấn và cách xử lý khi phiên làm việc thay đổi.

### Các công việc đã thực hiện trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Rà soát bố cục giao diện đã dựng ở tuần 7, thống nhất tông màu sáng và hệ biểu tượng phù hợp với bối cảnh y tế.<br>- Điều chỉnh cách hiển thị hồ sơ bệnh án theo trạng thái đăng nhập để thông tin của người dùng được trình bày rõ ràng hơn.<br>- Ghi nhận các điểm cần kết nối giữa giao diện, hồ sơ và luồng tiếp nhận triệu chứng. | 02/11/2026 | 02/11/2026 | Mã nguồn MediMind AI và bản thiết kế giao diện |
| 3 | - Tìm hiểu luồng xử lý tài liệu y tế từ ảnh đầu vào đến dữ liệu có cấu trúc; triển khai các bước đọc đơn thuốc và kết quả xét nghiệm.<br>- Bổ sung việc đối chiếu ngày sinh, giới tính từ kết quả trích xuất trước khi đưa thông tin vào giao diện; tính và hiển thị tuổi từ ngày sinh thay vì nhập thủ công.<br>- Kiểm tra cách truyền các trường dữ liệu từ Backend sang Frontend để hạn chế thiếu hoặc sai thông tin hiển thị. | 03/11/2026 | 03/11/2026 | Mã nguồn xử lý OCR và giao diện hồ sơ của dự án |
| 4 | - Phát triển luồng tiếp nhận triệu chứng ban đầu và cửa sổ chat nổi để người dùng có thể trao đổi khi đang xem các trang khác.<br>- Rà soát việc lưu phiên tư vấn, đồng bộ dữ kiện giữa phần tiếp nhận và chatbot; sửa trường hợp câu phủ định bị hiểu thành triệu chứng có mặt.<br>- Thiết kế lại trang chủ, hồ sơ cá nhân và phần cơ sở y tế theo cùng một hệ thống giao diện; kiểm tra việc chuyển tab và hiển thị dữ liệu đúng tài khoản. | 04/11/2026 | 04/11/2026 | Mã nguồn MediMind AI, ghi chú về luồng tiếp nhận và thiết kế UI |
| 5 | - Tổ chức việc lưu đơn thuốc và kết quả xét nghiệm vào hồ sơ người dùng sau khi xử lý.<br>- Bổ sung phần lịch sử và tóm tắt để có thể xem lại tài liệu đã tải lên, thay vì chỉ hiển thị kết quả trong một phiên sử dụng.<br>- Kiểm tra mối liên hệ giữa tài liệu, phiên tư vấn và thông tin hồ sơ để giảm nguy cơ nhầm dữ liệu giữa các tài khoản. | 05/11/2026 | 05/11/2026 | Mã nguồn chức năng hồ sơ và xử lý tài liệu |
| 6 | - Rà soát bố cục trang chatbot theo các màn hình tham chiếu; điều chỉnh khoảng cách, màu chữ và độ tương phản để nội dung hội thoại dễ đọc hơn.<br>- Thay các biểu tượng trang trí liên quan đến AI bằng biểu tượng y tế có ý nghĩa rõ hơn; kiểm tra giao diện ở các trạng thái sáng và tối.<br>- Đối chiếu cách hiển thị câu hỏi, phản hồi và thành phần điều hướng giữa chat chính và chat nổi. | 06/11/2026 | 06/11/2026 | Bản thiết kế giao diện và mã nguồn Frontend |
| 7 | - Cải thiện trang tìm kiếm cơ sở y tế với danh sách kết quả và bản đồ tương tác; làm rõ nút mở bản đồ và trạng thái hiển thị hiện tại.<br>- Điều chỉnh thanh công cụ tìm kiếm, màu sắc, bố cục thẻ thông tin; sửa lỗi bố cục khiến các tab ảnh hưởng lẫn nhau.<br>- Kiểm tra khả năng theo dõi vị trí cơ sở y tế từ danh sách sang bản đồ. | 07/11/2026 | 07/11/2026 | Mã nguồn trang cơ sở y tế và bản thiết kế UI |
| Chủ nhật | - Hoàn thiện việc theo dõi phiên tư vấn và đồng bộ dữ kiện tiếp nhận với nội dung chat.<br>- Điều chỉnh quy trình để bản tóm tắt lâm sàng chỉ được lưu khi người dùng xem lại và xác nhận; sửa mẫu email OTP và một số lỗi hiển thị trong luồng tư vấn.<br>- Rà soát chức năng xem lại hội thoại, phân biệt bản nháp trong phiên với bản tóm tắt đã được người dùng chấp thuận lưu. | 08/11/2026 | 08/11/2026 | Mã nguồn phiên tư vấn, hồ sơ và tài liệu cải thiện chatbot |

### Kết quả đạt được tuần 8:

- Hình thành luồng làm việc liên tục từ **tiếp nhận triệu chứng → hội thoại → xử lý tài liệu → xem lại thông tin trong hồ sơ**. Qua quá trình này, tôi hiểu rõ hơn vai trò của mỗi thành phần và điểm cần đồng bộ dữ liệu giữa Frontend với Backend.
- Thực hành chuyển thông tin từ đơn thuốc, phiếu xét nghiệm sang dữ liệu có cấu trúc; bổ sung bước đối chiếu các trường nhân khẩu học trước khi hiển thị. Tôi nhận thấy kết quả trích xuất cần được kiểm tra và cho phép người dùng xem lại, không thể mặc nhiên coi là chính xác.
- Cải thiện cách lưu phiên tư vấn và xử lý dữ kiện phủ định. Việc phân biệt “có triệu chứng” với “không có triệu chứng” là yêu cầu quan trọng để tránh làm sai lệch ngữ cảnh của chatbot.
- Đơn thuốc và kết quả xét nghiệm đã có nơi lưu trong hồ sơ người dùng, kèm lịch sử và tóm tắt để tra cứu. Tôi hiểu thêm về yêu cầu gắn dữ liệu với đúng tài khoản và tránh để dữ liệu thử nghiệm lẫn với dữ liệu thật.
- Giao diện trang chủ, chat, hồ sơ và cơ sở y tế được thống nhất hơn về màu sắc, biểu tượng và bố cục; bản đồ tương tác hỗ trợ xem vị trí cơ sở từ kết quả tìm kiếm.
- Quy trình lưu bản tóm tắt tư vấn đã có bước xác nhận chủ động của người dùng. Đây là bài học thực tế về quyền kiểm soát dữ liệu sức khỏe và sự khác nhau giữa dữ liệu tạm thời trong phiên với dữ liệu được lưu lâu dài.
- Phần xử lý tài liệu và phản hồi của chatbot vẫn là tính năng hỗ trợ thông tin ban đầu; các kết quả liên quan đến sức khỏe cần được người dùng kiểm tra và không thay thế đánh giá chuyên môn của nhân viên y tế.
