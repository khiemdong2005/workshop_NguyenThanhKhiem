---
title: "Worklog Tuần 9"
date: 2026-11-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

- Tìm hiểu cách chia một chức năng mới thành phần giao diện, API, xử lý nghiệp vụ và dữ liệu.
- Thực hành kiểm tra dữ liệu đầu vào, xử lý trường hợp lỗi và hiển thị trạng thái phù hợp trên Front-end.
- Tìm hiểu cách tổ chức kho tài liệu và đánh giá kết quả tìm kiếm trong phần Back-end.
- Tìm hiểu cách Amazon Bedrock Evaluations tách việc đánh giá truy xuất tài liệu và đánh giá câu trả lời của hệ thống RAG.
- Tiếp tục cải thiện giao diện cơ sở y tế và cách đồng bộ danh sách với bản đồ.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 3 | - Phác thảo giao diện cho phần gợi ý món ăn và theo dõi thói quen.<br>- Tìm hiểu cách chia chức năng thành dữ liệu công thức, quy tắc xử lý ở Back-end, API và phần hiển thị ở Front-end.<br>- Kết nối giao diện với dữ liệu trả về, đồng thời kiểm tra một số trường hợp nhập thông tin chưa đầy đủ. | 10/11/2026 | 10/11/2026 | [Tài liệu chức năng](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/nutrition-recommendations.md); [Mã nguồn Back-end](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/nutrition_service.py) |
| 4 | - Tổ chức lại dữ liệu công thức để có thể tìm kiếm và lọc theo yêu cầu.<br>- Viết các điều kiện xử lý trường hợp có nhiều yêu cầu cùng lúc hoặc cần tránh một thành phần.<br>- Tìm hiểu cách trả kết quả dự phòng từ dữ liệu có sẵn khi dịch vụ bên ngoài không phản hồi, thay vì để giao diện không có kết quả. | 11/11/2026 | 11/11/2026 | [Danh mục dữ liệu](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/recipe_catalog.py); [Quy tắc xử lý](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/nutrition_rules.py) |
| 5 | - Tìm hiểu cách kiểm tra chất lượng câu trả lời của hệ thống bằng bộ câu hỏi mẫu và nguồn tài liệu đi kèm.<br>- Xem lại các bước tìm kiếm tài liệu trong Back-end: nhận câu hỏi, tìm đoạn liên quan và chuyển kết quả cho phần tạo câu trả lời.<br>- Thử tìm tài liệu tiếng Anh bằng câu hỏi tiếng Việt và ghi nhận những trường hợp kết quả chưa sát nội dung hỏi.<br>- Đọc tài liệu Amazon Bedrock Evaluations để phân biệt đánh giá chỉ truy xuất tài liệu với đánh giá cả truy xuất và tạo câu trả lời; so sánh các tiêu chí này với bộ câu hỏi mẫu đang dùng. | 12/11/2026 | 12/11/2026 | [Ghi chú kiểm tra chatbot](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md); [Mã nguồn tìm kiếm tài liệu](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/rag_service.py); [AWS Bedrock RAG Evaluations](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-evaluation-metrics.html) |
| 6 | - Kiểm tra lại giao diện cơ sở y tế ở chế độ sáng và tối.<br>- Chỉnh cách hiển thị danh sách, bản đồ và khung thông tin chi tiết khi người dùng chọn một địa điểm.<br>- Rà soát trạng thái giao diện để bản đồ và danh sách cùng hiển thị đúng cơ sở đang được chọn. | 13/11/2026 | 13/11/2026 | [Giao diện HTML](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html); [JavaScript](https://github.com/khiemdong2005/chatbot_medical/blob/main/static/js/app.js) |
| Chủ nhật | - Rà soát cấu trúc Back-end và các bước đưa tài liệu vào kho tìm kiếm.<br>- Tìm hiểu vì sao khi số tài liệu tăng, một số câu hỏi lại nhận về đoạn chưa liên quan; điều chỉnh cách chọn tài liệu và kiểm tra bằng câu hỏi mẫu.<br>- Sắp xếp lại các phần xử lý để việc bổ sung dữ liệu và kiểm thử về sau dễ theo dõi hơn. | 15/11/2026 | 15/11/2026 | [Mã nguồn tìm kiếm tài liệu](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/rag_service.py); [Mã nguồn Back-end](https://github.com/khiemdong2005/chatbot_medical/blob/main/app.py) |

### Kết quả đạt được tuần 9:

- Hiểu rõ hơn cách tổ chức một chức năng theo các lớp: giao diện, API, xử lý nghiệp vụ và dữ liệu. Cách chia này giúp xác định lỗi nằm ở phần nào khi kết quả hiển thị chưa đúng.
- Thực hành kiểm tra dữ liệu đầu vào và chuẩn bị kết quả dự phòng khi một dịch vụ bên ngoài gặp lỗi.
- Biết cách sắp xếp dữ liệu công thức và áp dụng các điều kiện lọc trước khi trả kết quả cho giao diện.
- Bước đầu biết cách dùng câu hỏi mẫu để kiểm tra phần tìm kiếm tài liệu và đối chiếu nguồn đi kèm với câu trả lời.
- Hiểu thêm cách tách hai câu hỏi khi đánh giá RAG: hệ thống có tìm đúng tài liệu không và câu trả lời có dựa đúng vào tài liệu đó không. Tôi chỉ tham khảo phương pháp trong Amazon Bedrock Evaluations, chưa chạy một evaluation job trên AWS.
- Nhận thấy việc tìm tài liệu cho câu hỏi tiếng Việt cần được kiểm tra riêng khi kho tài liệu có nhiều nội dung tiếng Anh.
- Cải thiện phần giao diện cơ sở y tế, nhất là cách đồng bộ danh sách kết quả, vị trí trên bản đồ và khung thông tin chi tiết.
- Hiểu rằng việc bổ sung thêm dữ liệu phải đi cùng kiểm tra chất lượng tìm kiếm; nếu chỉ tăng số lượng tài liệu, kết quả có thể khó đúng trọng tâm hơn.
