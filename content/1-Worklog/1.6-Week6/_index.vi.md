---
title: "Nhật ký công việc tuần 6"
date: 2026-10-19
weight: 6
chapter: false
pre: "<b>1.6.</b> "
---

### Mục tiêu tuần 6:

- Tìm hiểu cách mở rộng quy mô ứng dụng (Scaling), cân bằng tải và giám sát hệ thống với Amazon CloudWatch phục vụ cho việc triển khai AI API/Backend.
- Tìm hiểu cơ chế bộ nhớ đệm (Caching) với Amazon ElastiCache và phân phối nội dung qua CDN (CloudFront).
- Bắt đầu triển khai dự án thực tế: tìm hiểu các công nghệ, thư viện liên quan tới project và tiến hành dựng giao diện người dùng (UI) cơ bản.
- Tìm hiểu một số cách tối ưu chi phí AWS.
- Tham gia meeting FCAJ để cập nhật kiến thức thực tế từ các anh chị trong cộng đồng.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Tìm hiểu về mở rộng quy mô ứng dụng với **EC2 Auto Scaling** (Scaling, Auto Scaling Group, Load Balancer)</li><li>Tìm hiểu giải pháp giám sát hệ thống với **Amazon CloudWatch** (Logs, Metrics, Alarms)</li></ul> | 19/10/2026 | 19/10/2026 | https://cloudjourney.awsfcaj.com/ |
| 3 | <ul><li>Tìm hiểu bộ nhớ đệm trong bộ nhớ với **Amazon ElastiCache (Redis)** để lưu cache/session cho AI API</li><li>Tìm hiểu cơ bản về **Amazon Route 53** và **Amazon CloudFront**</li><li>Tham khảo cách cấp chứng chỉ TLS cho tên miền riêng bằng AWS Certificate Manager (ACM) và cách dùng AWS WAF với CloudFront để lọc yêu cầu web.</li></ul> | 20/10/2026 | 20/10/2026 | https://cloudjourney.awsfcaj.com/ |
| 4 | <ul><li>Thực hành **Workshop về mạng trên AWS** (VPC, Subnet, Security)</li><li>Thực hành lab **Xây dựng ứng dụng web có tính sẵn sàng cao** (ghép EC2 + Load Balancer + Auto Scaling + DB)</li><li>Tìm hiểu thêm cách Application Load Balancer (ALB) dùng nhóm đích và kiểm tra trạng thái để chuyển yêu cầu đến các máy chủ đang hoạt động.</li></ul> | 21/10/2026 | 21/10/2026 | https://cloudjourney.awsfcaj.com/ |
| 5 | <ul><li>Bắt đầu triển khai dự án: tìm hiểu sâu hơn các tài liệu, công nghệ và luồng nghiệp vụ liên quan tới project</li><li>Thiết kế bố cục và tiến hành dựng giao diện người dùng (UI) cơ bản cho hệ thống</li><li>Từ bản phác thảo chung, bắt đầu bố trí trang chính và cách người dùng chuyển sang các nhóm chức năng. Đây là bước dựng khung giao diện.</li><li>Chốt tên và slogan của dự án để dùng trên giao diện.</li><li>Dùng Google Stitch, Google AI Studio và ChatGPT để lên ý tưởng và phác thảo bố cục giao diện của dự án.</li></ul> | 22/10/2026 | 22/10/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical) |
| 6 | <ul><li>Tiếp tục hoàn thiện UI và chuẩn bị cấu trúc kết nối giữa Frontend với Backend/AI API</li><li>Tìm hiểu một số cách tối ưu chi phí AWS trong quá trình làm lab và triển khai dự án</li><li>Xem phần nào giao diện có thể xử lý trực tiếp và phần nào cần gửi yêu cầu đến backend hoặc dịch vụ AI.</li></ul> | 23/10/2026 | 23/10/2026 | [Dự án](https://github.com/khiemdong2005/chatbot_medical)<br>https://cloudjourney.awsfcaj.com/ |
| 7 | <ul><li>Tham gia meeting FCAJ</li></ul> | 24/10/2026 | 24/10/2026 |  |

### Kết quả đạt được tuần 6:

- Chốt tên và slogan, rồi dựng bản bố cục giao diện đầu tiên để dùng khi phát triển các màn hình.
- Tìm hiểu cách Load Balancer phân phối yêu cầu và EC2 Auto Scaling điều chỉnh số máy chủ.
- Làm quen với log, chỉ số và cảnh báo trong Amazon CloudWatch.
- Tìm hiểu khi nào có thể dùng Redis để lưu tạm, Route 53 để phân giải tên miền và CloudFront để phân phối nội dung.
- Ôn lại VPC, subnet và kiểm soát truy cập qua bài lab mạng.
- Thử kết hợp EC2, Load Balancer, Auto Scaling và cơ sở dữ liệu trong bài lab ứng dụng web.
- Tìm hiểu thêm cách kiểm soát chi phí AWS khi làm lab và chuẩn bị triển khai dự án.
- Qua buổi gặp FCAJ, tôi biết thêm về các cách xây dựng trợ lý giọng nói và cách AWS RAM chia sẻ tài nguyên giữa các tài khoản.
- Nghe chia sẻ về bảo mật ứng dụng web với AWS Security Agent và cách tổ chức runtime, bộ nhớ trong Amazon Bedrock AgentCore.
