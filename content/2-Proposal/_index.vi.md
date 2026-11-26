---
title: "Bản đề xuất"
date: 2026-09-14
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# MediMind Clinical AI  
## Nền tảng Trợ lý Y tế Lâm sàng, Đối soát Đơn thuốc & Chăm sóc Sức khỏe Thông minh trên AWS  

### 1. Tóm tắt điều hành  
MediMind Clinical AI được thiết kế nhằm hỗ trợ sàng lọc triệu chứng ban đầu, đối soát đơn thuốc/phiếu xét nghiệm, nhắc lịch uống thuốc và tư vấn dinh dưỡng cá nhân hóa cho người bệnh và bác sĩ tại Việt Nam. Hệ thống kết hợp kiến trúc **Hybrid RAG (BM25 + ChromaDB Vector + Cross-Encoder Reranker)** trên 364 tài liệu y khoa chuẩn hóa (*Bộ Y Tế, kcb.vn, MedlinePlus NIH*), cơ chế bảo vệ hai lớp (**Clinical Triage & Double Guardrails**) và **Pipeline OCR Đối soát** xử lý song song EasyOCR cùng Vision LLM (`qwen/qwen3.8-27b` qua Groq API Dual-Key Failover). Nền tảng được đóng gói Docker và triển khai trên hạ tầng **Amazon Web Services (AWS)** khu vực `ap-southeast-1` (Singapore) với kiến trúc VPC 3 tầng mạng tách biệt đa vùng sẵn sàng (**Multi-AZ**), tuân thủ **AWS Well-Architected Framework** và chuẩn bảo mật dữ liệu y tế **HIPAA**.  

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Các bệnh viện tuyến đầu thường xuyên quá tải 150% – 200% công suất, khiến người bệnh chờ đợi 2 – 4 giờ và bác sĩ thiếu bản tóm tắt bệnh sử trước khám. Đồng thời, việc người dân tự tra cứu triệu chứng qua các công cụ AI không kiểm chứng dễ dẫn đến bỏ lỡ "giờ vàng" cấp cứu. Các chatbot thông thường cũng dễ mắc bẫy phủ định (báo động giả khi người bệnh nhập *"không khó thở"*) hoặc tự bịa nguồn trích dẫn y khoa và thực đơn gây dị ứng. Ngoài ra, các công cụ OCR đơn lẻ dễ nhận diện sai trên đơn thuốc mờ dẫn đến nhầm liều dùng, người bệnh lại hay quên lịch uống thuốc (trước/sau bữa ăn), đồng thời thiếu gợi ý dinh dưỡng an toàn theo bệnh lý và món ăn quen thuộc tại Việt Nam.  

*Giải pháp*  
Nền tảng xây dựng quy trình chăm sóc sức khỏe khép kín gồm 5 phân hệ: (1) Sàng lọc triệu chứng đa lượt phân tầng 3 mức nguy cơ (**Xanh – Vàng – Đỏ**), xử lý tiếng Việt không dấu và bẫy phủ định để kích hoạt gọi **Cấp cứu 115** kịp thời; (2) Pipeline OCR đối soát chạy song song EasyOCR và Vision LLM, đối chiếu chéo từng trường dữ liệu, gắn cờ `needs_review` khi sai lệch dữ liệu hoặc lệch cữ/số lượng thuốc và chuyển thành lịch nhắc uống thuốc trực quan (*Sáng – Trưa – Chiều – Tối; Trước/Sau ăn*) kết nối **chuông thông báo lưu trữ trên server** sau khi người dùng xác nhận; (3) Tra cứu tri thức có căn cứ từ 364 tài liệu y khoa chuẩn; (4) Tư vấn dinh dưỡng lâm sàng kết hợp khảo sát **BMR/TDEE**, **12 ngữ cảnh bệnh lý** – **12 nhóm dị ứng** (*Fail-Closed Allergy Filtering*) từ **4.962 công thức món Việt chạy trực tiếp** (**2.462 ViFoodRec** + **2.500 Món Ngon Mỗi Ngày**, cùng **34 món tuyển chọn**); và (5) Xuất hồ sơ tóm tắt tiền khám 30 giây, hỗ trợ đặt lịch khám trong ứng dụng theo danh mục **2.144 cơ sở y tế** (1.505 tại TP.HCM và 639 tại Hà Nội), gửi email xác nhận về hộp thư người dùng và cập nhật thông báo đặt/hủy lịch trên chuông thông báo. Toàn bộ ứng dụng chạy trên **Amazon EC2 (Auto Scaling Group) + Amazon EFS** và **Amazon RDS PostgreSQL (Multi-AZ)**, bảo vệ biên bởi **AWS WAF**, **CloudFront** và **ALB**.  

*Lợi ích và hoàn vốn đầu tư (ROI)*  
Giải pháp giúp rút ngắn thời gian khai thác bệnh sử ban đầu xuống còn 30 giây, giảm sai sót dùng thuốc/quên cữ uống thuốc tại nhà và ngăn ngừa biến cố dị ứng/tương tác thuốc nhờ cơ chế xác nhận *Human-in-the-Loop* cùng chuông thông báo nhắc lịch lưu trữ trên server. Nhờ nạp chỉ mục vector ChromaDB (`medical_vectordb`, ~86 MB) dạng chỉ đọc từ Docker/S3 xuống ổ đĩa EC2 kết hợp **Amazon EFS** cho `/uploads` thay cho các dịch vụ Managed Vector DB đắt đỏ và tận dụng **Groq API Dual-Key** tối ưu hạn mức miễn phí ở giai đoạn thử nghiệm, chi phí hạ tầng giai đoạn **Dev/PoC Workshop** chỉ ở mức **~16,86 USD/tháng** (~202,32 USD/12 tháng), còn hạ tầng AWS **Production Multi-AZ** cho quy mô 10.000 người dùng/tháng đạt khoảng **220,95 – 233,45 USD/tháng** (**~0,0088 – 0,0093 USD/phiên tư vấn**, tương đương **~225 – 240 VNĐ/lượt**), tiết kiệm đáng kể so với chi phí thuê cụm GPU và Managed Vector DB riêng.  

### 3. Kiến trúc giải pháp  
Nền tảng áp dụng kiến trúc **AWS 3-Tier Multi-AZ VPC (`10.0.0.0/16`)** trải trên 2 Availability Zones (`ap-southeast-1a`, `ap-southeast-1b`) tại khu vực `ap-southeast-1` nhằm cô lập hoàn toàn tầng tính toán và cơ sở dữ liệu khỏi truy cập Internet trực tiếp. Lưu lượng người dùng đi qua **Route 53**, **AWS WAF** và **Amazon CloudFront** tới **Application Load Balancer (ALB)** tại `Public Subnet`, sau đó định tuyến nội bộ qua cổng `8000` vào container trên **Amazon EC2** thuộc **Auto Scaling Group** nằm trong `Private App Subnet 1 & 2`. Thư mục tệp tải lên (`./uploads`) được chia sẻ qua **Amazon EFS** gắn cho các EC2 và sao lưu sang **Amazon S3** thông qua **S3 Gateway Endpoint** (còn chỉ mục **ChromaDB `./medical_vectordb`** dạng chỉ đọc được đóng gói trong Docker image hoặc đồng bộ từ S3 xuống EBS cục bộ của từng EC2 để tránh lỗi khóa file SQLite qua NFS), trong khi 7 bảng dữ liệu giao dịch lưu tại **Amazon RDS PostgreSQL (Primary & Standby với Sync Replication)** (`SQL :5432`) trong `Private Database Subnet 1 & 2`. Mọi kết nối chiều ra tới **Groq API**, **Google OAuth 2.0** và **Gmail SMTP / SpeedSMS** đều đi qua **NAT Gateway 1 & 2**.  

<img width="2560" height="1674" alt="architecture" src="https://github.com/user-attachments/assets/ab55faef-924c-40ff-8622-f7a663c190ec" />


*Dịch vụ AWS sử dụng*  
- *Amazon Route 53 & Amazon CloudFront*: Phân giải DNS, lưu đệm tài nguyên tĩnh (1 TB miễn phí/tháng) và ẩn địa chỉ gốc máy chủ.  
- *AWS WAF & AWS Certificate Manager (ACM)*: Tường lửa lớp 7 chống OWASP Top 10, Rate Limiting và cấp phát chứng chỉ SSL/TLS 1.3 miễn phí (tầng Global `us-east-1` cho CloudFront và Regional `ap-southeast-1` cho ALB).  
- *Application Load Balancer (ALB) & NAT Gateway*: Thực hiện TLS Termination tại `Public Subnet` và cấp quyền truy cập chiều ra an toàn cho `Private App Subnet 1 & 2`.  
- *Amazon EC2 (Auto Scaling Group) & Amazon EFS*: Máy chủ chạy container ứng dụng (`PORT=8000`) tự động mở rộng theo tải; gắn **Amazon EFS** chia sẻ thư mục `/uploads` và nạp chỉ mục ChromaDB (364 tài liệu) dạng chỉ đọc từ image/S3 xuống EBS cục bộ.  
- *Amazon RDS for PostgreSQL (Multi-AZ)*: Cơ sở dữ liệu quan hệ cô lập trong `Private Database Subnet 1 & 2` (`SQL :5432`) gồm Primary và Standby đồng bộ dữ liệu tự động chuyển đổi dự phòng (Auto Failover), quản lý người dùng, hồ sơ y tế, thông báo và lịch hẹn.  
- *Amazon S3, S3 Gateway Endpoint & Amazon ECR*: Lưu trữ sao lưu (`Backup / Archive`) hồ sơ và snapshot RAG qua kết nối nội bộ **S3 Gateway Endpoint**, đồng thời quản lý Docker Image riêng tư trên ECR.  
- *AWS Secrets Manager, CloudWatch, AWS IAM, Cost Explorer & AWS Budgets*: Quản lý khóa API tập trung, thu thập log/metrics/cảnh báo đã ẩn danh PII, phân quyền tối thiểu qua `EC2 IAM Role` và theo dõi ngân sách.  

*Thiết kế thành phần*  
- *Tầng Biên & Bảo mật*: Route 53, WAF, CloudFront và ALB chặn tấn công mạng và mã hóa toàn bộ lưu lượng HTTPS.  
- *Tầng Ứng dụng & AI (`Private App Subnet`)*: Backend Python (`app.py` / `core/main_fastapi.py`) xử lý Double Guardrails, Hybrid RAG (BM25 + ChromaDB + BGE Reranker), OCR đối soát, chuông thông báo (`/api/notifications`) cho lịch hẹn/nhắc uống thuốc, bộ lọc dinh dưỡng tất định (12 ngữ cảnh bệnh lý, 12 nhóm dị ứng, 10 quy tắc kiêng kỵ) và Circuit Breaker dự phòng.  
- *Tầng Dữ liệu & Lưu trữ (`Private Database Subnet` & Storage)*: RDS PostgreSQL (Primary & Standby) lưu 7 bảng nghiệp vụ (`users`, `medical_documents`, `prescription_history`, `clinical_consultations`, `intake_sessions`, `medical_appointments`, `user_notifications`); **Redis dùng chung** (Amazon ElastiCache `cache.t4g.micro` hoặc đồng bộ qua RDS ở chế độ tiết kiệm) lưu OTP/Rate Limiting cho đa thực thể EC2; **Amazon EFS** chia sẻ `/uploads`; **EBS cục bộ** lưu chỉ mục ChromaDB chỉ đọc; **Amazon S3** lưu bản sao lưu dài hạn.  
- *Tích hợp Dịch vụ Ngoài*: Xác thực qua Google OAuth 2.0, gửi OTP 6 số và email xác nhận lịch hẹn qua Gmail SMTP / SpeedSMS, suy luận AI đa khóa (**Groq Dual-Key Failover**) và hiển thị bản đồ 2.144 cơ sở y tế qua Google Maps Platform API.  

### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai*  
Dự án được xây dựng đồng bộ từ lõi lâm sàng đến hạ tầng AWS qua 4 giai đoạn chính:  
1. *Khảo sát & Thiết kế Kiến trúc*: Thu thập dữ liệu y khoa chuẩn hóa, thiết kế sơ đồ AWS 3-Subnet Multi-AZ VPC, lược đồ 7 bảng PostgreSQL và đặc tả API (Tuần 1–2).  
2. *Phát triển Lõi Lâm sàng & RAG*: Xây dựng Double Guardrails chống bẫy phủ định, chỉ mục Hybrid RAG 364 tài liệu và Pipeline OCR đối soát (Tuần 3–6).  
3. *Mở rộng Nghiệp vụ & Giao diện SPA*: Tích hợp **4.962 công thức món Việt** (**2.462 ViFoodRec** + **2.500 Món Ngon Mỗi Ngày**, 34 món tuyển chọn, 2.474 ảnh thật) kèm khảo sát BMR/TDEE, danh mục 2.144 cơ sở y tế, đặt lịch khám, chuông thông báo nhắc thuốc/lịch hẹn, xác thực OAuth/OTP và giao diện Web SPA (Tuần 7–8).  
4. *Đóng gói Container, Triển khai AWS & Kiểm định*: Đóng gói Docker lên Amazon ECR, cấu hình EC2 (Auto Scaling Group) + EFS + RDS (Multi-AZ) + ALB + WAF + Secrets Manager, chạy 94 tệp kiểm thử tự động và đánh giá benchmark (Tuần 9–12).  

*Yêu cầu kỹ thuật*  
- *Backend & AI Pipeline*: Python (`Flask` / `FastAPI` gateway, `SQLAlchemy`), `ChromaDB`, `rank-bm25`, `BAAI/bge-reranker-v2-m3`, `EasyOCR`, `Redis` (OTP/RateLimit), tích hợp đa khóa **Groq Dual-Key** (`GROQ_API_KEY`, `GROQ_API_KEY_2`, `GROQ_CHAT_API_KEY`, `GROQ_OCR_API_KEY`, `GROQ_NUTRITION_API_KEY`) kèm Circuit Breaker cùng Retry Policy xử lý HTTP 429.  
- *An toàn Tệp & Dữ liệu*: Kiểm tra Magic Bytes chống giả mạo định dạng, chặn Decompression/Zip Bomb (ảnh ≤ 25 MP, PDF ≤ 30 trang, tỷ lệ nén DOCX < 50x), bảo vệ CSRF và ẩn danh PII tự động trong log.  
- *Hạ tầng AWS*: VPC `10.0.0.0/16` tại `ap-southeast-1`, Security Groups phân tách chặt chẽ giữa ALB (`443`), EC2 (`8000`) và RDS (`5432`), nạp biến môi trường động từ AWS Secrets Manager thông qua EC2 IAM Role.  

### 5. Lộ trình & Mốc triển khai  
- *Trước thực tập (Tháng 0)*: Khảo sát bài toán quá tải y tế tuyến đầu, thu thập 364 tài liệu phác đồ (*Bộ Y Tế, MedlinePlus NIH*), **4.962 công thức món Việt chạy trực tiếp** (**2.462 ViFoodRec** + **2.500 Món Ngon Mỗi Ngày**, tổng 5.862 công thức đã làm sạch) và danh mục 2.144 cơ sở y tế.  
- *Thực tập (Tháng 1–3 / 12 Tuần)*:  
  - Tháng 1 (Tuần 1–4): Thiết kế kiến trúc AWS 3-Subnet VPC, phát triển lõi Clinical Triage, Double Guardrails và cơ sở dữ liệu.  
  - Tháng 2 (Tuần 5–8): Hoàn thiện Hybrid RAG, Pipeline OCR đối soát, Clinical Nutrition Studio (BMR/TDEE + lọc đa bệnh nền), đặt lịch khám, chuông thông báo nhắc thuốc và giao diện Web SPA.  
  - Tháng 3 (Tuần 9–12): Đóng gói Docker lên ECR, triển khai trên EC2 + EFS + RDS (Multi-AZ) + ALB + WAF, chạy 94 tệp kiểm thử tự động (`pytest`) và chuẩn bị Live Demo Workshop.  
- *Sau triển khai*: Mở rộng tích hợp chuẩn liên thông dữ liệu y tế HL7 FHIR và triển khai thử nghiệm tại các phòng khám đa khoa vệ tinh.  

### 6. Ước tính ngân sách  
Chi phí được ước tính theo đơn giá On-Demand tại khu vực **Singapore (`ap-southeast-1`)** cho hai giai đoạn: **Dev/PoC Workshop** (chạy Single-AZ tận dụng AWS Free Tier / Free Tier Credits và chỉ bật ALB/NAT theo giờ demo rồi tắt) và **Production Multi-AZ** (khớp 100% sơ đồ mục 3 cho 10.000 người dùng/tháng chạy 24/7).  

*Chi phí hạ tầng (Giai đoạn Dev / PoC Workshop)*  
- Amazon EC2 (`t3.micro` / `t3.small`, cổng 8000): 0,00 – 3,17 USD/tháng (`t3.micro` miễn phí 750 giờ Free Tier kèm swap/tắt reranker cục bộ; `t3.small` 2 GB RAM chạy ~120 giờ demo ở mức ~$0.0264/giờ).  
- Amazon EFS / EBS (lưu `/uploads` & `medical_vectordb` ~86 MB trong hạn mức 5 GB EFS Free Tier / Free Tier Credits và 30 GB EBS Free Tier): 0,00 USD/tháng.  
- Amazon RDS PostgreSQL (`db.t4g.micro` Single-AZ, cổng 5432): 0,00 USD/tháng (miễn phí 750 giờ + 20 GB Free Tier 12 tháng đầu).  
- Application Load Balancer & 1 NAT Gateway (~40 giờ kiểm thử/demo): ~3,97 USD/tháng (gồm $3,37 phí giờ ALB + NAT GW và ~$0,60 cho 3 Public IPv4 của ALB/NAT vì gói 750h IPv4 Free Tier chỉ áp dụng cho EC2).  
- Amazon S3 (`Backup / Archive` ~2 GB), S3 Gateway Endpoint & Amazon ECR: ~0,00 – 0,15 USD/tháng (ECR miễn phí 500 MB/tháng trong 12 tháng đầu; nếu image đóng gói kèm EasyOCR/OpenCV vượt ngưỡng ~1–2 GB tốn thêm ~$0,05–$0,15/tháng).  
- AWS Secrets Manager (3 nhóm Secrets): 1,20 USD/tháng (`$0.40/secret`).  
- Amazon CloudFront (15 GB), ACM (TLS 1.3), CloudWatch, AWS IAM, Cost Explorer & AWS Budgets: 0,00 USD/tháng (Always-Free / Free Tier).  
- Amazon Route 53 (1 Hosted Zone + 50.000 queries): 0,52 USD/tháng.  
- AWS WAF (1 Web ACL + 3 Managed Rules, bật cả tháng): 8,00 USD/tháng (`$5.00` Web ACL + `$1.00 × 3` rule groups; nếu chỉ bật 40h demo tính theo giờ là ~$0,44).  
- Dịch vụ AI & Xác thực ngoài (Groq API Dual-Key Free Tier, Gmail SMTP, Google OAuth): 0,00 USD/tháng.  

*Tổng (Dev / PoC Workshop)*: **~16,86 USD/tháng** (~430.000 VNĐ/tháng, **~202,32 USD/12 tháng**; lưu ý tắt/xóa ALB & NAT Gateway sau khi demo để tránh phát sinh ~$72/tháng nếu chạy 24/7).  

*Chi phí mở rộng Production Multi-AZ (10.000 người dùng / 25.000 phiên tư vấn / 8.000 lượt OCR mỗi tháng, chạy 24/7 — đúng theo sơ đồ mục 3)*  
- 2 × Amazon EC2 (`t3.small` trong Auto Scaling Group, `2 × $0.0264/h × 730h`): ~38,54 USD/tháng.  
- Amazon EFS Standard (~5 GB cho `/uploads`) & 2 × EBS gốc (`gp3` 20 GB chứa `medical_vectordb` read-only): ~5,64 USD/tháng.  
- Amazon RDS PostgreSQL Multi-AZ (`db.t4g.micro` Primary + Standby `~$0.050/h` + 20 GB `gp3` Multi-AZ): ~41,10 USD/tháng.  
- 1 × ALB + 2 × NAT Gateway (24/7) + 4 Public IPv4 (`$14.60`) + LCU & Data Processing (~20 GB): ~122,32 USD/tháng.  
- Amazon ElastiCache Redis (`cache.t4g.micro` làm Shared State OTP/RateLimit cho 2 EC2): ~12,50 USD/tháng *(tùy chọn: $0,00 nếu chuyển OTP/RateLimit lưu qua RDS PostgreSQL)*.  
- AWS WAF (~8,60 USD) + Secrets Manager (1,20 USD) + Route 53 (~0,70 USD) + S3/ECR/CloudWatch (~2,85 USD) + CloudFront (< 1 TB Always-Free): ~13,35 USD/tháng.  
- *Tổng hạ tầng AWS Production Multi-AZ*: **~233,45 USD/tháng** (nếu dùng ElastiCache Redis; hoặc **~220,95 USD/tháng** nếu lưu OTP/RateLimit trên RDS), tương đương **~0,0088 – 0,0093 USD/phiên tư vấn** (**~225 – 240 VNĐ/phiên**; chưa gồm phí nâng cấp Groq Pay-as-you-go nếu lưu lượng cao vượt Free Tier).  

### 7. Đánh giá rủi ro  
*Ma trận rủi ro*  
- Bỏ sót dấu hiệu cấp cứu hoặc mắc bẫy phủ định (*"không khó thở"*): Ảnh hưởng cao, xác suất trung bình.  
- Sai lệch nhận diện OCR trên đơn thuốc viết tay mờ/lóa hoặc quá tải HTTP 429: Ảnh hưởng cao, xác suất trung bình.  
- Tải lên tệp độc hại (Decompression/Zip Bomb) hoặc truy cập trái phép hồ sơ (IDOR): Ảnh hưởng cao, xác suất thấp.  
- Gián đoạn API từ nhà cung cấp AI bên ngoài (Groq API) hoặc vượt ngân sách: Ảnh hưởng trung bình, xác suất thấp.  

*Chiến lược giảm thiểu*  
- Lâm sàng & Phủ định: Áp dụng Double Guardrails (`core/triage.py`) kết hợp quy tắc tiền kiểm từ khóa cấp cứu (hỗ trợ tiếng Việt không dấu và cụm từ phủ định) cùng bước hậu kiểm phản hồi LLM, tự động cảnh báo gọi 115 khi có dấu hiệu nguy kịch và chặn việc tự kê đơn kháng sinh.  
- OCR Đơn thuốc & Nhắc uống thuốc: Chạy song song EasyOCR & Vision LLM kèm cơ chế retry HTTP 429/Dual-Key Failover, tự động gắn cờ `needs_review=True` khi lệch trường hoặc lệch cữ/số lượng thuốc, bắt buộc người dùng xác nhận (*Human-in-the-Loop*) trước khi lưu lịch uống thuốc và gửi nhắc nhở qua chuông thông báo trên server.  
- Bảo mật & Hạ tầng: Cô lập EC2 và RDS trong Private Subnets, kiểm tra Magic Bytes & giới hạn kích thước tệp (`core/storage_service.py`), ẩn danh PII trong log và cài đặt cảnh báo **AWS Budgets** ở ngưỡng 20 USD.  

*Kế hoạch dự phòng*  
- Kích hoạt **Circuit Breaker** (`core/circuit_breaker.py`) tự động ngắt mạch sau 5 lỗi API liên tiếp để chuyển sang **Fallback Clinical Engine** và bộ lọc dinh dưỡng tất định mà không làm treo hệ thống.  
- Khôi phục nhanh chỉ mục ChromaDB và cơ sở dữ liệu từ bản sao lưu định kỳ trên **Amazon S3** và Automated Snapshots của **Amazon RDS**.  

### 8. Kết quả kỳ vọng  
*Cải tiến kỹ thuật*  
Hoàn thiện nền tảng trợ lý y tế đa phương thức kèm bộ **94 tệp kiểm thử tự động (`pytest`)** bao phủ sàng lọc triệu chứng (xử lý phủ định và cờ đỏ cấp cứu), đối soát đơn thuốc OCR song song, truy xuất tri thức Hybrid RAG trên 364 tài liệu chuẩn hóa, lọc dị ứng/bệnh lý dinh dưỡng tất định và quy trình đặt lịch – nhắc uống thuốc với cơ chế dự phòng Circuit Breaker khi dịch vụ AI ngoài gián đoạn.  

*Giá trị dài hạn*  
Cung cấp kiến trúc tham chiếu chuẩn AWS bảo mật cao và tối ưu chi phí (**~225 – 240 VNĐ/phiên tư vấn** ở hạ tầng Production Multi-AZ cho quy mô 10.000 người dùng), có thể tái sử dụng và mở rộng cho các phòng khám, bệnh viện tuyến cơ sở nhằm giảm tải khâu sàng lọc tiếp đón và nâng cao an toàn sử dụng thuốc cho cộng đồng.
