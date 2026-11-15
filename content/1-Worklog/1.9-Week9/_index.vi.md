---
title: "Worklog Tuần 9"
date: 2026-11-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

- Mở rộng MediMind AI từ chức năng tư vấn ban đầu sang hỗ trợ lựa chọn món ăn và theo dõi thói quen, đồng thời xác định rõ giới hạn của gợi ý dinh dưỡng trong một ứng dụng sức khỏe.
- Tìm hiểu cách kết hợp dữ liệu công thức món ăn có nguồn gốc với quy tắc lọc và mô hình ngôn ngữ, tránh để mô hình tự tạo nguyên liệu hoặc khẳng định lợi ích y khoa chưa được kiểm chứng.
- Đánh giá chất lượng câu trả lời của chatbot, chú ý đến sự phù hợp của nguồn trích dẫn, các tình huống cần cảnh báo an toàn và câu hỏi tiếng Việt khi tài liệu chủ yếu bằng tiếng Anh.
- Cải thiện khả năng tìm kiếm cơ sở y tế và cách trình bày thông tin trên giao diện.
- Nghiên cứu vấn đề suy giảm độ liên quan của kết quả truy xuất khi kho tài liệu RAG được mở rộng; tổ chức lại dữ liệu và các thành phần Backend để thuận tiện kiểm thử.

### Các công việc đã thực hiện trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 3 | - Thiết kế và triển khai **Nutrition Studio** với luồng xem gợi ý món ăn, tạo nội dung công thức có hỗ trợ AI và ghi nhận thói quen sử dụng.<br>- Phân chia phần giao diện, quy tắc lọc món ăn và dịch vụ xử lý ở Backend; xác định dữ liệu nào do ứng dụng kiểm soát và dữ liệu nào chỉ là giải thích từ mô hình.<br>- Viết các ca kiểm thử cơ bản cho quy tắc dinh dưỡng và luồng tương tác. | 10/11/2026 | 10/11/2026 | Mã nguồn Nutrition Studio và tài liệu gợi ý dinh dưỡng của dự án |
| 4 | - Mở rộng quy tắc gợi ý cho trường hợp người dùng nêu đồng thời nhiều tình trạng sức khỏe hoặc yêu cầu tránh một số thành phần.<br>- Nhập và làm sạch dữ liệu công thức món ăn để tạo danh mục tra cứu cục bộ; bổ sung phương án hiển thị kết quả đã lọc khi dịch vụ AI không sẵn sàng.<br>- Rà soát tên món, nguyên liệu và nguồn dữ liệu để tránh trình bày nội dung do mô hình sinh ra như một công thức đã được xác minh. | 11/11/2026 | 11/11/2026 | Tài liệu Nutrition recommendations, dữ liệu công thức và mã nguồn dự án |
| 5 | - Thiết lập các tình huống đánh giá câu trả lời chatbot, kiểm tra việc sử dụng nguồn tài liệu và các trường hợp cần phản hồi an toàn thay vì đưa ra kết luận y khoa chắc chắn.<br>- Thử nghiệm mở rộng truy vấn giữa tiếng Việt và tiếng Anh nhằm cải thiện khả năng tìm tài liệu liên quan; phân biệt kết quả thử nghiệm với chất lượng đã được kiểm định trong thực tế.<br>- Đồng bộ cách trình bày phần cơ sở y tế với các trang khác của ứng dụng. | 12/11/2026 | 12/11/2026 | Tài liệu cải thiện chatbot, bộ đánh giá và mã nguồn giao diện |
| 6 | - Rà soát giao diện tìm kiếm cơ sở y tế ở các chế độ màu, sửa sự không nhất quán của màu chữ và thành phần hiển thị.<br>- Khôi phục bản đồ Google Maps và cải thiện khung thông tin chi tiết khi chọn một cơ sở trong danh sách.<br>- Kiểm tra mối liên hệ giữa danh sách, vị trí bản đồ và nội dung chi tiết để giảm thao tác lặp cho người dùng. | 13/11/2026 | 13/11/2026 | Mã nguồn trang cơ sở y tế và bản thiết kế UI |
| Chủ nhật | - Phân tích hiện tượng kết quả truy xuất kém liên quan khi bổ sung nhiều tài liệu vào kho tri thức RAG; rà soát cách tuyển chọn, phân loại và tìm kiếm tài liệu.<br>- Bổ sung tập tài liệu y tế đã tuyển chọn, điều chỉnh luồng truy xuất và xây dựng các phép đánh giá để so sánh kết quả trên bộ câu hỏi phát triển.<br>- Tổ chức lại một phần cấu trúc Backend và cấu hình để các thành phần xử lý có trách nhiệm rõ ràng hơn. | 15/11/2026 | 15/11/2026 | Mã nguồn RAG, tài liệu đánh giá truy xuất và dữ liệu tuyển chọn |

### Kết quả đạt được tuần 9:

- Xây dựng được Nutrition Studio gồm giao diện, danh mục công thức, quy tắc lọc và chức năng theo dõi thói quen. Tôi hiểu thêm về cách tách **dữ liệu gốc**, **quy tắc kiểm soát** và **phần diễn giải của AI** trong cùng một luồng gợi ý.
- Bổ sung dữ liệu món ăn có thể tra cứu cục bộ và phương án dự phòng khi dịch vụ AI không phản hồi. Kết quả dự phòng cần được ghi rõ là danh sách đã lọc, không được mô tả như kết quả xếp hạng bởi AI.
- Bước đầu xây dựng cách đánh giá chatbot theo tình huống, kiểm tra nguồn trích dẫn và hành vi an toàn. Các phép kiểm thử kỹ thuật giúp phát hiện lỗi triển khai nhưng chưa đủ để chứng nhận độ chính xác lâm sàng.
- Thực hành tìm kiếm tài liệu giữa tiếng Việt và tiếng Anh; nhận thấy truy vấn đa ngôn ngữ cần được đo trên bộ dữ liệu độc lập để tránh đánh giá quá lạc quan.
- Cải thiện tính nhất quán của trang cơ sở y tế, khôi phục bản đồ và hoàn thiện khung thông tin chi tiết để người dùng dễ đối chiếu địa điểm với kết quả tìm kiếm.
- Nhận diện bài toán **retrieval dilution**: khi số lượng tài liệu tăng, các đoạn ít liên quan có thể lấn át nguồn cần thiết. Việc tuyển chọn dữ liệu, kiểm soát phiên bản kho tài liệu và đánh giá theo câu hỏi mẫu là các bước quan trọng trước khi mở rộng RAG.
- Các gợi ý dinh dưỡng và câu trả lời của chatbot chỉ hỗ trợ tham khảo ban đầu; hệ thống chưa tạo kế hoạch ăn uống cá nhân được chuyên gia thẩm định và không thay thế tư vấn của bác sĩ hoặc chuyên gia dinh dưỡng.
