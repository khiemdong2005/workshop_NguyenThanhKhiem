---
report_key: "workshopChapters"
report_language: "vi"
report_fields: {"shortTitle": "Minh chứng Demo Live", "customTitle": "5.7. Minh chứng Sản phẩm Chạy Thực tế (Live Demo & Video)", "summary": "Tổng hợp minh chứng vận hành thực tế của MediMind Clinical AI trên hạ tầng AWS Multi-AZ (ap-southeast-1): đường dẫn HTTPS đang chạy live qua Amazon CloudFront + AWS WAF, video demo toàn luồng trên YouTube, mã nguồn GitHub và ảnh đối chiếu thực tế.", "content": "Sản phẩm MediMind Clinical AI đang hoạt động trực tuyến tại https://d2typ9pphzk4as.cloudfront.net với video demo đầy đủ tại https://www.youtube.com/watch?v=vF3kyvuShqo, mã nguồn công khai trên GitHub và bảng dự toán AWS Pricing Calculator 13 dịch vụ.", "notes": "", "steps": [{"num": "5.7.1", "title": "Liên kết Sản phẩm Live & Tài nguyên Đối chiếu Chính thức", "summary": "Toàn bộ sản phẩm triển khai thực tế, video ghi hình demo, mã nguồn dự án và bảng dự toán chi phí đều được công khai để Mentor và hội đồng trực tiếp kiểm chứng:", "table": {"headers": ["Hạng mục minh chứng", "Đường dẫn truy cập trực tiếp"], "rows": [["Ứng dụng Live HTTPS (CloudFront + AWS WAF)", "[https://d2typ9pphzk4as.cloudfront.net](https://d2typ9pphzk4as.cloudfront.net)"], ["Video Demo Trực tiếp Toàn luồng (YouTube)", "[Xem Video Demo MediMind Clinical AI](https://www.youtube.com/watch?v=vF3kyvuShqo)"], ["Mã nguồn Triển khai (`main`)", "[github.com/MediMind-Clinical-AI/chatbot_medical](https://github.com/MediMind-Clinical-AI/chatbot_medical)"], ["Dự toán Chi phí AWS (13 dịch vụ)", "[AWS Pricing Calculator ($228.76/tháng)](https://calculator.aws/#/estimate?id=ec26a26022ee93e0eb9785a0048f4dca71eb6fb3)"]]}}, {"num": "5.7.2", "title": "Video Demo Trực tiếp Sản phẩm & Hạ tầng AWS Multi-AZ (YouTube)", "summary": "Video dưới đây trình diễn toàn bộ luồng vận hành trực tiếp trên `https://d2typ9pphzk4as.cloudfront.net` kèm phần đối chiếu trực quan các tài nguyên AWS đang chạy thật trong Region `ap-southeast-1` (Singapore) và lớp biên `us-east-1`.", "video": {"youtubeId": "vF3kyvuShqo", "url": "https://www.youtube.com/watch?v=vF3kyvuShqo", "title": "MediMind Clinical AI — Live Demo trên AWS Multi-AZ"}, "bullets": ["**Xác thực & Quản trị Hồ sơ:** Đăng nhập Google OAuth 2.0, đăng ký xác thực Email OTP 6 số, Onboarding hồ sơ sức khỏe lần đầu, đổi mật khẩu và kiểm chứng chặn sai mật khẩu.", "**Sàng lọc Lâm sàng & Hybrid RAG:** Khung chat nổi đồng bộ trực tiếp sang tab Trợ lý sức khỏe, từ chối câu hỏi ngoài phạm vi y tế và kích hoạt thẻ cảnh báo Cờ Đỏ khẩn cấp (*Double Guardrails*).", "**OCR Đối soát Đơn thuốc & Dinh dưỡng:** Tải ảnh đơn thuốc để Vision LLM bóc tách hoạt chất/liều dùng, tạo lịch nhắc uống thuốc; lập thực đơn dinh dưỡng theo Món lẻ / Combo mâm cơm kèm công thức nấu.", "**Cơ sở Y tế & Đặt lịch khám:** Tìm kiếm cơ sở y tế theo vị trí trên Google Maps, điền phiếu khai tiền khám, đặt lịch hẹn và nhận Email xác nhận tự động.", "**Đối chiếu Hạ tầng AWS Multi-AZ:** CloudFront HTTPS, AWS WAF chặn SQL Injection (`403 BLOCK`), VPC 3 tầng 6 Subnets, ALB `2/2 Healthy`, 2 Private EC2 ASG, EFS Dual-AZ, Private RDS PostgreSQL, Secrets Manager, CloudWatch Alarms và AWS Budgets."]}, {"num": "5.7.3", "title": "Ảnh Minh chứng Hệ thống Chạy Thực tế (ALB 2/2 Healthy, CloudFront HTTPS & Lâm sàng)", "summary": "Bộ ảnh đối chiếu nhanh từ môi trường Live xác nhận đồng thời 3 lớp: cân bằng tải Multi-AZ (`2/2 Healthy`), kiểm thử đầu cuối qua CloudFront Edge (`SGN50-P1`, `RAG ready`, `Circuit Breaker CLOSED`) và phản hồi cảnh báo lâm sàng trên giao diện người dùng thật.", "images": [{"url": "static/images/5-Workshop/5.5-Operations/21-alb-2healthy.png", "caption": "Ảnh 21 (AWS Console) — Target Group medimind-tg đạt 2/2 Healthy trải đều 2 Private EC2 ở ap-southeast-1a và ap-southeast-1b"}, {"url": "static/images/5-Workshop/5.5-Operations/22-live-health-cloudfront.jpg", "caption": "Ảnh 22 (Live HTTPS) — Kiểm thử /health ok, /ready ready (RAG & Circuit Breaker CLOSED), CSP/X-Frame-Options tại CloudFront SGN50-P1"}, {"url": "static/images/5-Workshop/5.5-Operations/24-live-clinical-triage-redflag.jpg", "caption": "Ảnh 24 (Live App) — MediMind Clinical AI kích hoạt Cảnh báo Nguy cơ cao tức thì với ca đau thắt ngực cấp cứu trên CloudFront HTTPS"}], "note": "Chi tiết kiểm thử bảo mật AWS WAF SQL Injection (`403 BLOCK`), CloudWatch Alarms và AWS Budgets được ghi nhận tại Chương **5.5**; kịch bản dọn dẹp tài nguyên chờ chạy sau khi hoàn tất nghiệm thu nằm tại Chương **5.6**."}]}
report_index: 6
report_shared: {"code": "5.7", "url": "https://d2typ9pphzk4as.cloudfront.net"}
title: "Minh chứng sản phẩm chạy thực tế"
date: "2026-11-28"
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

# 5.7. Minh chứng Sản phẩm Chạy Thực tế (Live Demo & Video)

Tổng hợp minh chứng vận hành thực tế của **MediMind Clinical AI** trên hạ tầng AWS Multi-AZ (`ap-southeast-1`): đường dẫn HTTPS đang chạy live qua Amazon CloudFront + AWS WAF, video demo toàn luồng trên YouTube, mã nguồn GitHub và ảnh đối chiếu thực tế.

## 5.7.1 — Liên kết Sản phẩm Live & Tài nguyên Đối chiếu Chính thức

| Hạng mục minh chứng | Đường dẫn truy cập trực tiếp |
| --- | --- |
| Ứng dụng Live HTTPS (CloudFront + AWS WAF) | [https://d2typ9pphzk4as.cloudfront.net](https://d2typ9pphzk4as.cloudfront.net) |
| Video Demo Trực tiếp Toàn luồng (YouTube) | [Xem Video Demo MediMind Clinical AI](https://www.youtube.com/watch?v=vF3kyvuShqo) |
| Mã nguồn Triển khai (`main`) | [github.com/MediMind-Clinical-AI/chatbot_medical](https://github.com/MediMind-Clinical-AI/chatbot_medical) |
| Dự toán Chi phí AWS (13 dịch vụ) | [AWS Pricing Calculator ($228.76/tháng)](https://calculator.aws/#/estimate?id=ec26a26022ee93e0eb9785a0048f4dca71eb6fb3) |

## 5.7.2 — Video Demo Trực tiếp Sản phẩm & Hạ tầng AWS Multi-AZ (YouTube)

Video dưới đây trình diễn toàn bộ luồng vận hành trực tiếp trên `https://d2typ9pphzk4as.cloudfront.net` kèm phần đối chiếu trực quan các tài nguyên AWS đang chạy thật trong Region `ap-southeast-1` (Singapore) và lớp biên `us-east-1`.

<div style="margin: 1rem 0 1.25rem; border: 1px solid #e2e8f0; border-radius: 10px; overflow: hidden; background: #fff;">
  <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; background: #0f172a;">
    <iframe src="https://www.youtube.com/embed/vF3kyvuShqo" title="MediMind Clinical AI — Live Demo trên AWS Multi-AZ" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
  </div>
  <div style="display: flex; justify-content: space-between; align-items: center; gap: 12px; padding: 10px 14px; background: #f8fafc; border-top: 1px solid #e2e8f0; flex-wrap: wrap;">
    <span style="font-size: 0.92rem; color: #334155;">MediMind Clinical AI — Live Demo trên AWS Multi-AZ</span>
    <a href="https://www.youtube.com/watch?v=vF3kyvuShqo" target="_blank" rel="noopener noreferrer" style="display: inline-block; padding: 6px 12px; background: #0f172a; color: #ffffff; border-radius: 6px; font-size: 0.85rem; font-weight: 600; text-decoration: none;">Mở trên YouTube ↗</a>
  </div>
</div>

- **Xác thực & Quản trị Hồ sơ:** Đăng nhập Google OAuth 2.0, đăng ký xác thực Email OTP 6 số, Onboarding hồ sơ sức khỏe lần đầu, đổi mật khẩu và kiểm chứng chặn sai mật khẩu.
- **Sàng lọc Lâm sàng & Hybrid RAG:** Khung chat nổi đồng bộ trực tiếp sang tab Trợ lý sức khỏe, từ chối câu hỏi ngoài phạm vi y tế và kích hoạt thẻ cảnh báo Cờ Đỏ khẩn cấp (*Double Guardrails*).
- **OCR Đối soát Đơn thuốc & Dinh dưỡng:** Tải ảnh đơn thuốc để Vision LLM bóc tách hoạt chất/liều dùng, tạo lịch nhắc uống thuốc; lập thực đơn dinh dưỡng theo Món lẻ / Combo mâm cơm kèm công thức nấu.
- **Cơ sở Y tế & Đặt lịch khám:** Tìm kiếm cơ sở y tế theo vị trí trên Google Maps, điền phiếu khai tiền khám, đặt lịch hẹn và nhận Email xác nhận tự động.
- **Đối chiếu Hạ tầng AWS Multi-AZ:** CloudFront HTTPS, AWS WAF chặn SQL Injection (`403 BLOCK`), VPC 3 tầng 6 Subnets, ALB `2/2 Healthy`, 2 Private EC2 ASG, EFS Dual-AZ, Private RDS PostgreSQL, Secrets Manager, CloudWatch Alarms và AWS Budgets.

## 5.7.3 — Ảnh Minh chứng Hệ thống Chạy Thực tế (ALB 2/2 Healthy, CloudFront HTTPS & Lâm sàng)

![Ảnh 21 (AWS Console) — Target Group medimind-tg đạt 2/2 Healthy trải đều 2 Private EC2 ở ap-southeast-1a và ap-southeast-1b](/images/5-Workshop/5.5-Operations/21-alb-2healthy.png)
*Ảnh 21 (AWS Console) — Target Group medimind-tg đạt 2/2 Healthy trải đều 2 Private EC2 ở ap-southeast-1a và ap-southeast-1b*

![Ảnh 22 (Live HTTPS) — Kiểm thử /health ok, /ready ready (RAG & Circuit Breaker CLOSED), CSP/X-Frame-Options tại CloudFront SGN50-P1](/images/5-Workshop/5.5-Operations/22-live-health-cloudfront.jpg)
*Ảnh 22 (Live HTTPS) — Kiểm thử /health ok, /ready ready (RAG & Circuit Breaker CLOSED), CSP/X-Frame-Options tại CloudFront SGN50-P1*

![Ảnh 24 (Live App) — MediMind Clinical AI kích hoạt Cảnh báo Nguy cơ cao tức thì với ca đau thắt ngực cấp cứu trên CloudFront HTTPS](/images/5-Workshop/5.5-Operations/24-live-clinical-triage-redflag.jpg)
*Ảnh 24 (Live App) — MediMind Clinical AI kích hoạt Cảnh báo Nguy cơ cao tức thì với ca đau thắt ngực cấp cứu trên CloudFront HTTPS*
