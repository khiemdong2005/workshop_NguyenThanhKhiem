---
title: "Cấu hình ALB, CloudFront, WAF và Route 53"
date: 2026-11-26
weight: 3
chapter: false
pre: " <b> 5.4.3 </b> "
---

#### Bước 1: Tạo Target Group & Application Load Balancer (Public Subnets)

1. Mở **EC2 Console** (`ap-southeast-1`) -> thanh trái **Load Balancing -> Target Groups -> Create target group**:
   - **Target type:** `Instances` | **Target group name:** `medimind-tg` | **Protocol/Port:** `HTTP` / `8000`
   - **VPC:** `medimind-vpc`
   - Mở mục **Health checks**: **Health check path:** `/health` -> **Advanced health check settings -> Healthy threshold:** `2`, **Interval:** `15` -> **Next**.
   - Chọn máy chủ `medimind-app-server`, giữ port `8000`, nhấn **Include as pending below** -> **Create target group**.
2. Mở **AWS Certificate Manager (ACM) Console** tại vùng **`ap-southeast-1`** -> **Request certificate -> Request a public certificate** -> nhập tên miền của bạn (`medimind.yourdomain.com`), chọn **DNS validation** -> **Request** -> vào chi tiết chứng chỉ nhấn **Create records in Route 53** để tự xác thực.
3. Quay lại **EC2 Console -> Load Balancing -> Load Balancers -> Create load balancer -> Application Load Balancer -> Create**:
   - **Load balancer name:** `medimind-alb` | **Scheme:** `Internet-facing` | **IP address type:** `IPv4`
   - **Network mapping:** chọn **VPC** `medimind-vpc`, tích chọn cả 2 AZ và gán subnet `medimind-public-a` (`ap-southeast-1a`) và `medimind-public-b` (`ap-southeast-1b`)
   - **Security groups:** gỡ `default`, chọn **`sg-medimind-alb`**
   - **Listeners and routing:** Listener `HTTPS : 443` chọn **Forward to** `medimind-tg` và gắn chứng chỉ **ACM Regional** ở bước 2; nhấn **Add listener** thêm `HTTP : 80` chọn **Redirect to URL** `HTTPS : 443` (mã `301`) -> **Create load balancer**.

{{% notice info %}}
Nhờ cấu hình `TRUST_PROXY_HEADERS=true` và `TRUSTED_PROXY_COUNT=2` trong `/etc/medimind.env` (vì lưu lượng đi qua 2 tầng proxy `CloudFront -> ALB -> EC2`; chỉ đặt `=1` nếu truy cập trực tiếp qua ALB không qua CloudFront), ứng dụng MediMind cắt đúng IP người dùng (`ips[-trusted_proxy_count]` trong `X-Forwarded-For`) và giao thức HTTPS (`X-Forwarded-Proto`) để thực thi giới hạn tần suất (`core/rate_limit_service.py`) và tạo link callback OAuth chuẩn xác.
{{% /notice %}}

#### Bước 2: Tạo AWS WAF Web ACL (Tường lửa Lớp 7)

Mở **AWS WAF & Shield Console** -> mục **Web ACLs** -> ở ô **Region** phía trên chọn **`Global (CloudFront)`** -> nhấn **Create web ACL**:
- **Name:** `medimind-edge-waf` | **Resource type:** `Amazon CloudFront distributions` -> **Next**.
- Ở bước **Add rules**:
  - Nhấn **Add rules -> Add managed rule groups -> AWS managed rule groups** và bật **3 bộ luật**:
    1. **Core rule set (`AWSManagedRulesCommonRuleSet`)** — Chặn các lỗ hổng OWASP Top 10, XSS và Path Traversal.
    2. **SQL database (`AWSManagedRulesSQLiRuleSet`)** — Lọc mã độc SQL Injection nhắm vào API đăng nhập và tìm kiếm.
    3. **Known bad inputs (`AWSManagedRulesKnownBadInputsRuleSet`)** — Từ chối header giả mạo và mẫu quét lỗ hổng phổ biến.
  - Nhấn **Add rules -> Add my own rules and rule groups -> Rule builder**: đặt tên `MediMindRateLimit`, **Type:** `Rate-based rule`, **Rate limit:** `1000` yêu cầu / 5 phút / IP -> **Action:** `Block` -> **Create web ACL**.

#### Bước 3: Cấu hình Amazon CloudFront & Route 53 DNS

1. Mở lại **AWS Certificate Manager (ACM) Console** và **chuyển Region góc phải sang `us-east-1` (N. Virginia)** -> yêu cầu **Chứng chỉ ACM Global** cho `medimind.yourdomain.com` và nhấn **Create records in Route 53** *(bắt buộc tại `us-east-1` để gắn tên miền tùy chỉnh cho CloudFront)*.
2. Mở **CloudFront Console -> Distributions -> Create distribution**:
   - **Origin domain:** chọn DNS của **`medimind-alb`** | **Protocol:** `HTTPS only` (Minimum TLSv1.2).
   - **Default cache behavior:** **Viewer protocol policy:** `Redirect HTTP to HTTPS`; **Cache policy:** `CachingDisabled`; **Origin request policy:** `AllViewer`.
   - **Web Application Firewall (WAF):** chọn **Use existing WAF configuration** -> chọn **`medimind-edge-waf`**.
   - **Settings -> Custom SSL certificate:** chọn chứng chỉ ACM ở `us-east-1` và điền **Alternate domain name (CNAME):** `medimind.yourdomain.com` -> **Create distribution**.
   - Sau khi tạo xong, mở tab **Behaviors -> Create behavior** để tách riêng 2 đường dẫn:
     - **Behavior 1 (`/static/*`):** **Cache policy:** `CachingOptimized` để lưu đệm CSS, JS, hình ảnh món ăn/giao diện tại Edge (tận dụng gói miễn phí **1 TB/tháng**).
     - **Behavior 2 (`/api/*`, bao gồm `/api/auth/*`):** **Cache policy:** `CachingDisabled` + **Origin request policy:** `AllViewer` để các luồng sàng lọc lâm sàng, tải đơn thuốc OCR và callback OAuth (`/api/auth/google/callback`) đi thẳng về backend kèm đầy đủ Cookie/Header.
3. Mở **Route 53 Console -> Hosted zones** -> chọn domain của bạn -> **Create record**: **Record name:** `medimind`, **Record type:** `A`, bật **Alias**, **Route traffic to:** `Alias to CloudFront distribution` -> chọn tên miền CloudFront (`dxxxxxxxxxxxx.cloudfront.net`) -> **Create records**.
