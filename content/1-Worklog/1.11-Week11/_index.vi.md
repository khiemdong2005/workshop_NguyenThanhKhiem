---
title: "Nhật ký công việc tuần 11"
date: 2026-11-23
weight: 11
chapter: false
pre: "<b>1.11.</b> "
---

### Mục tiêu tuần 11:

- Rà lỗi giao diện và hoàn thiện luồng đọc, đối chiếu và chỉnh sửa đơn thuốc.
- Hoàn thiện nhắc lịch hẹn, nhắc uống thuốc và xuất thông tin tiền khám theo FHIR R4.
- Hoàn thiện luồng gợi ý Dinh dưỡng theo khảo sát BMR/TDEE, dị ứng và danh mục món cố định.
- Triển khai MediMind lên AWS và kiểm tra truy cập qua HTTPS.
- Hoàn thiện Proposal, Workshop và sơ đồ kiến trúc AWS, rà dự toán và quay video demo.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Chạy thử web trên trình duyệt và sửa các lỗi hiển thị ảnh, tự điền biểu mẫu và xử lý yêu cầu khi chưa đăng nhập.</li><li>Chuẩn hóa tên thuốc từ Thông tư 20/2022/TT-BYT để đối chiếu kết quả OCR. Chạy thử luồng đọc đơn thuốc với danh mục cục bộ và API dự phòng.</li><li>Hoàn thiện phần đặt lịch và nhắc uống thuốc. Khôi phục lịch dùng thuốc đã duyệt, ẩn lịch hẹn quá hạn và bổ sung xuất dữ liệu tiền khám đã xác nhận theo FHIR R4.</li></ul> | 23/11/2026 | 23/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/commit/a950e1fffdf60f4d12fcef0ae416423ff5560ddb) |
| 3 | <ul><li>Kiểm tra OCR trên nhiều ảnh đơn thuốc có bố cục khác nhau và rà lại các trường hợp tên thuốc nhận dạng chưa đúng.</li><li>Sửa lỗi chuyển tab và thay cách gợi ý món. Hệ thống lọc danh mục theo quy tắc trước, sau đó mô hình chọn trong các món còn lại.</li></ul> | 24/11/2026 | 24/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 4 | <ul><li>Bổ sung nút chỉnh sửa trên màn hình kết quả OCR để người dùng sửa thông tin đọc sai trước khi lưu. Rà lại cấu hình API cho chatbot, OCR và Dinh dưỡng.</li><li>Hoàn thiện khảo sát BMR/TDEE theo Mifflin–St Jeor và bổ sung thông tin dị ứng. Tách mâm cơm, món lẻ và nước uống, chuẩn hóa calo theo khẩu phần và cập nhật ảnh cùng thông tin dinh dưỡng của món.</li><li>Thêm chức năng xem lại khảo sát và giữ nguyên tab đang mở, món đang xem cùng dữ liệu đã nhập khi tải lại trang. Vẽ sơ đồ luồng xử lý bằng draw.io và kiểm tra lại PR Quality Gate.</li></ul> | 25/11/2026 | 25/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 5 | <ul><li>Đối chiếu danh mục hiện có với bộ khoảng 2.500 món từ Món Ngon Mỗi Ngày. Kiểm tra món trùng và xuất bảng XLSX để so sánh hai nguồn.</li><li>Rà lại Proposal và Workshop theo phiên bản ứng dụng đang dùng. Sửa phần mô tả tính năng, số liệu danh mục món và ảnh minh họa.</li></ul> | 26/11/2026 | 26/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 6 | <ul><li>Triển khai MediMind lên AWS. Dựng Docker image bằng CodeBuild, lưu trên ECR và chạy container bằng Uvicorn trên EC2. Kiểm tra trạng thái đích trên ALB và mở ứng dụng qua HTTPS.</li><li>Đối chiếu cấu hình dịch vụ trên AWS Console để lập dự toán bằng AWS Pricing Calculator. Bổ sung 33 ảnh AWS Console và AWS CLI để minh họa các bước triển khai trong Workshop.</li><li>Đối chiếu sơ đồ triển khai với cấu hình AWS, gồm nguồn image trên ECR, quyền IAM Role để đọc cấu hình từ Secrets Manager và phần lưu trữ chia sẻ trên EFS.</li></ul> | 27/11/2026 | 27/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical/blob/main/Dockerfile#L54) |
| 7 | <ul><li>Hoàn thiện Proposal, hướng dẫn Workshop và sơ đồ kiến trúc AWS. Rà lại các bước triển khai và ảnh minh họa. Khi đối chiếu dự toán, ghi rõ bản Workshop dùng RDS Single-AZ và sơ đồ mục tiêu có phương án RDS Multi-AZ.</li><li>Quay video demo trên bản chạy ở AWS để trình bày các luồng chính của MediMind.</li></ul> | 28/11/2026 | 28/11/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |

### Kết quả đạt được tuần 11:

- Hoàn thiện luồng đặt lịch, nhắc lịch hẹn và nhắc uống thuốc. Dữ liệu tiền khám đã xác nhận có thể xuất theo FHIR R4.
- Chuẩn hóa danh mục thuốc để đối chiếu kết quả OCR. Người dùng có thể sửa thông tin đọc sai ngay trên màn hình kết quả trước khi lưu.
- Hoàn thiện luồng gợi ý món dựa trên khảo sát BMR/TDEE và thông tin dị ứng. Người dùng có thể xem mâm cơm, món lẻ và nước uống riêng, đồng thời tiếp tục từ tab đang mở sau khi tải lại trang.
- Triển khai MediMind lên AWS và kiểm tra truy cập ứng dụng qua HTTPS.
- Hoàn thiện Proposal, hướng dẫn Workshop và sơ đồ kiến trúc. Đối chiếu dự toán AWS với cấu hình triển khai và quay video trình bày các luồng chính của ứng dụng.
