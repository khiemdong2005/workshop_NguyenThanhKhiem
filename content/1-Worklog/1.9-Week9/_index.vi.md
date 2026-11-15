---
title: "Worklog Tuần 9"
date: 2026-11-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

- Tìm hiểu cách tổ chức dữ liệu món ăn và sử dụng dữ liệu đó để xây dựng phần gợi ý dinh dưỡng.
- Thực hành xây dựng các điều kiện lọc khi người dùng có nhiều nhu cầu sức khỏe hoặc cần tránh một số nguyên liệu.
- Tìm hiểu cách đánh giá câu trả lời của chatbot và cách tìm tài liệu phù hợp với câu hỏi tiếng Việt.
- Tiếp tục cải thiện trang cơ sở y tế và rà soát kho tài liệu dùng cho phần hỏi đáp.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 3 | - Tìm hiểu những thông tin cần có khi gợi ý món ăn: tên món, nguyên liệu, cách chế biến và yêu cầu của người dùng.<br>- Bắt đầu xây dựng trang gợi ý món ăn và phần ghi nhận thói quen ăn uống.<br>- Phân chia công việc giữa phần dữ liệu, quy tắc lựa chọn món và giao diện hiển thị. | 10/11/2026 | 10/11/2026 | [Tài liệu dinh dưỡng](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/nutrition-recommendations.md); [mã nguồn](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/nutrition_service.py) |
| 4 | - Tìm hiểu cách xử lý khi một người dùng đưa ra nhiều tình trạng sức khỏe cùng lúc hoặc cần tránh một nguyên liệu cụ thể.<br>- Thu thập, làm sạch và sắp xếp dữ liệu công thức món ăn để có thể tra cứu trong ứng dụng.<br>- Kiểm tra trường hợp không gọi được dịch vụ AI và hiển thị các món đã qua bước lọc thay cho kết quả từ AI. | 11/11/2026 | 11/11/2026 | [Tài liệu dinh dưỡng](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/nutrition-recommendations.md); [danh mục món ăn](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/recipe_catalog.py) |
| 5 | - Tìm hiểu cách đánh giá câu trả lời: nội dung có liên quan đến câu hỏi hay không, nguồn dẫn có đúng với tài liệu tìm được hay không và lời khuyên có phù hợp không.<br>- Thử cách tìm tài liệu tiếng Anh cho câu hỏi tiếng Việt; ghi nhận trường hợp tìm đúng chủ đề và trường hợp kết quả chưa liên quan.<br>- Tiếp tục chỉnh giao diện trang cơ sở y tế. | 12/11/2026 | 12/11/2026 | [Ghi chú chatbot](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md); [mã nguồn RAG](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/rag_service.py) |
| 6 | - Kiểm tra trang cơ sở y tế ở chế độ sáng và tối, chỉnh những chỗ màu chữ hoặc thẻ thông tin khó đọc.<br>- Khôi phục bản đồ và chỉnh khung thông tin chi tiết khi chọn một cơ sở.<br>- Xem lại cách chuyển từ danh sách kết quả sang vị trí trên bản đồ. | 13/11/2026 | 13/11/2026 | [Giao diện dự án](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html) |
| Chủ nhật | - Rà soát các tài liệu dùng để trả lời câu hỏi sức khỏe; tìm hiểu vì sao khi thêm nhiều tài liệu, một số câu hỏi lại nhận kết quả chưa đúng trọng tâm.<br>- Phân loại và bổ sung tài liệu phù hợp, kiểm tra lại cách tìm kiếm bằng các câu hỏi mẫu.<br>- Sắp xếp lại một số phần của Backend để việc kiểm tra và bổ sung tài liệu về sau thuận tiện hơn. | 15/11/2026 | 15/11/2026 | [Mã nguồn truy xuất tài liệu](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/rag_service.py) |

### Kết quả đạt được tuần 9:

- Hiểu thêm cách chuẩn bị dữ liệu món ăn trước khi sử dụng trong một chức năng gợi ý: cần có nguồn, nguyên liệu rõ ràng và cách xử lý các trường hợp không phù hợp.
- Bước đầu xây dựng được trang gợi ý món ăn, danh mục công thức và phần theo dõi thói quen.
- Biết cách kết hợp điều kiện lọc với dữ liệu có sẵn để xử lý yêu cầu tránh nguyên liệu hoặc nhiều nhu cầu cùng lúc.
- Tập đánh giá câu trả lời của chatbot dựa trên câu hỏi, nội dung phản hồi và nguồn tài liệu đi kèm, thay vì chỉ kiểm tra chatbot có trả lời hay không.
- Nhận thấy câu hỏi tiếng Việt có thể khó tìm đúng tài liệu khi phần lớn nguồn viết bằng tiếng Anh; cần thử nhiều câu hỏi để xem cách tìm kiếm có thực sự phù hợp.
- Hoàn thiện thêm trang cơ sở y tế và bản đồ để việc xem danh sách, vị trí và thông tin chi tiết thuận tiện hơn.
- Hiểu rằng mở rộng kho tài liệu không đồng nghĩa với tìm kiếm tốt hơn; cần chọn lọc tài liệu và kiểm tra kết quả sau mỗi lần bổ sung.
