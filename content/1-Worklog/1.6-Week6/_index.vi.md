---
title: "Worklog Tuần 6"
date: 2026-10-19
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

- Nắm vững cách mở rộng quy mô ứng dụng (Scaling), cân bằng tải và giám sát hệ thống với Amazon CloudWatch phục vụ cho việc triển khai AI API/Backend[cite: 1].
- Tìm hiểu cơ chế bộ nhớ đệm (Caching) với Amazon ElastiCache và phân phối nội dung qua CDN (CloudFront)[cite: 1, 2].
- Bắt đầu triển khai dự án thực tế: tìm hiểu các công nghệ, thư viện liên quan tới project và tiến hành dựng giao diện người dùng (UI) cơ bản.
- Tìm hiểu một số cách tối ưu chi phí AWS.
- Tham gia meeting FCAJ để cập nhật kiến thức thực tế từ các anh chị trong cộng đồng.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu về mở rộng quy mô ứng dụng với **EC2 Auto Scaling** (Scaling, Auto Scaling Group, Load Balancer)[cite: 1] <br> - Tìm hiểu giải pháp giám sát hệ thống với **Amazon CloudWatch** (Logs, Metrics, Alarms)[cite: 1] | 19/10/2026 | 19/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Tìm hiểu bộ nhớ đệm trong bộ nhớ với **Amazon ElastiCache (Redis)** để lưu cache/session cho AI API[cite: 1] <br> - Tìm hiểu cơ bản về **Amazon Route 53** và **Amazon CloudFront**[cite: 1, 2] | 20/10/2026 | 20/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Thực hành **Workshop về mạng trên AWS** (VPC, Subnet, Security)[cite: 1, 2] <br> - Thực hành lab **Xây dựng ứng dụng web có tính sẵn sàng cao** (ghép EC2 + Load Balancer + Auto Scaling + DB)[cite: 1, 2] | 21/10/2026 | 21/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Bắt đầu triển khai dự án: tìm hiểu sâu hơn các tài liệu, công nghệ và luồng nghiệp vụ liên quan tới project <br> - Thiết kế bố cục và tiến hành dựng giao diện người dùng (UI) cơ bản cho hệ thống | 22/10/2026 | 22/10/2026 | |
| 6 | - Tiếp tục hoàn thiện UI và chuẩn bị cấu trúc kết nối giữa Frontend với Backend/AI API <br> - Tìm hiểu một số cách tối ưu chi phí AWS trong quá trình làm lab và triển khai dự án | 23/10/2026 | 23/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 7 | - Tham gia meeting FCAJ | 24/10/2026 | 24/10/2026 | Event FCAJ |

### Kết quả đạt được tuần 6:

- Hiểu rõ cơ chế hoạt động của **EC2 Auto Scaling**, **Load Balancer** và biết cách sử dụng **Amazon CloudWatch** để theo dõi logs, metrics, tạo cảnh báo (alarm) cho hệ thống[cite: 1].

- Hiểu được vai trò của **Amazon ElastiCache (Redis)** trong việc làm bộ nhớ đệm (caching) cho AI API, cũng như cách dùng **Route 53** và **CloudFront** ở mức cơ bản[cite: 1, 2].

- Củng cố kiến thức về mạng (VPC, Subnet, Security) và thực hành ghép nối thành công các thành phần EC2 + Load Balancer + Auto Scaling + DB thành ứng dụng web có tính sẵn sàng cao[cite: 1, 2].

- Bước đầu bắt tay vào triển khai dự án: nắm rõ hơn các công nghệ, công cụ cần thiết cho project và dựng được giao diện (UI) cơ bản phục vụ cho việc tích hợp tính năng AI ở các bước tiếp theo.

- Biết thêm một số cách tối ưu chi phí trên AWS khi vận hành hạ tầng và phát triển dự án.

- **Tham gia meeting FCAJ và tiếp thu được nhiều kiến thức thực tế:**
  + **Hear, Think, Speak (Anh Kiệt Trần - Revve AI):** Tìm hiểu nền tảng AI phỏng vấn & Contact Center, so sánh 3 hướng xây dựng Voice Agent gồm *Cascade* (ASR -> LLM -> TTS, hiện vẫn tốt cho tiếng Việt hơn nhờ kiểm soát được bước text ở giữa), *Speech-to-Speech (S2S)* và *Full Duplex S2S*[cite: 5, 8].
  + **AWS Resource Access Manager (RAM) (Anh Long Huỳnh):** Hiểu bài toán Multi-account challenge, khái niệm AWS RAM và Anatomy of Resource Share (chia sẻ tài nguyên cho các tài khoản con), luồng hoạt động end-to-end hỗ trợ chia sẻ hơn 40 dịch vụ, tìm hiểu sâu về Regions/Global/AZ IDs và ứng dụng RAM trong Enterprise Landing Zone[cite: 7].
  + **AWS Security Agent & Bedrock AgentCore:** Lắng nghe chia sẻ từ anh Thịnh về bảo mật ứng dụng web với **AWS Security Agent** (cùng bài toán chi phí thực tế)[cite: 3, 6] và phần chia sẻ từ anh Xuân An về **Amazon Bedrock AgentCore** (Runtime & Memory Architecture), **Kiro Crew**, phát triển App và khả năng mở rộng (App & Extensibility)[cite: 4].
