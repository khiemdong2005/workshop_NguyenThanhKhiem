---
title: "Configure ALB, CloudFront, WAF & Route 53"
date: 2026-11-26
weight: 3
chapter: false
pre: " <b> 5.4.3 </b> "
---

#### Step 1: Create Target Group & Application Load Balancer (Public Subnets)

1. Open **EC2 Console** (`ap-southeast-1`) -> left menu **Load Balancing -> Target Groups -> Create target group**:
   - **Target type:** `Instances` | **Target group name:** `medimind-tg` | **Protocol/Port:** `HTTP` / `8000`
   - **VPC:** `medimind-vpc`
   - Under **Health checks**, set **Health check path:** `/health`, expand **Advanced health check settings** -> **Healthy threshold:** `2`, **Interval:** `15` -> **Next**.
   - Select `medimind-app-server` on port `8000`, click **Include as pending below** -> **Create target group**.
2. Open **AWS Certificate Manager (ACM) Console** in **`ap-southeast-1`** -> **Request certificate -> Request a public certificate** -> enter `medimind.yourdomain.com`, choose **DNS validation** -> **Request** -> click **Create records in Route 53** inside the certificate detail page.
3. Go back to **EC2 Console -> Load Balancing -> Load Balancers -> Create load balancer -> Application Load Balancer -> Create**:
   - **Load balancer name:** `medimind-alb` | **Scheme:** `Internet-facing` | **IP address type:** `IPv4`
   - **Network mapping:** select **VPC** `medimind-vpc`, select both AZs with `medimind-public-a` (`ap-southeast-1a`) and `medimind-public-b` (`ap-southeast-1b`)
   - **Security groups:** remove `default` and attach **`sg-medimind-alb`**
   - **Listeners and routing:** set `HTTPS : 443` to **Forward to** `medimind-tg` with the regional ACM certificate; click **Add listener** for `HTTP : 80` -> **Redirect to URL** `HTTPS : 443` (`301`) -> **Create load balancer**.

{{% notice info %}}
Because `TRUST_PROXY_HEADERS=true` and `TRUSTED_PROXY_COUNT=2` are set in `/etc/medimind.env` (accounting for 2 proxy hops `CloudFront -> ALB -> EC2`; set `=1` only if routing directly to ALB without CloudFront), MediMind accurately extracts the real client IP (`ips[-trusted_proxy_count]` from `X-Forwarded-For`) and HTTPS scheme (`X-Forwarded-Proto`) for rate limiting (`core/rate_limit_service.py`) and OAuth callback URLs.
{{% /notice %}}

> **[Screenshot 12: Target Group `medimind-tg` (`Healthy` on `:8000`) & ALB `medimind-alb` (`Active`, HTTPS `:443`)]** — `static/images/5-Workshop/5.4-Deploy-MediMind/12-alb-tg-healthy.png`

#### Step 2: Create an AWS WAF Web ACL (Layer-7 Firewall)

Open **AWS WAF & Shield Console -> Web ACLs**, switch the top **Region** dropdown to **`Global (CloudFront)`**, and click **Create web ACL**:
- **Name:** `medimind-edge-waf` | **Resource type:** `Amazon CloudFront distributions` -> **Next**.
- In **Add rules**:
  - Click **Add rules -> Add managed rule groups -> AWS managed rule groups** and enable:
    1. **Core rule set (`AWSManagedRulesCommonRuleSet`)** — Blocks OWASP Top 10 exploits, XSS, and path traversal attempts.
    2. **SQL database (`AWSManagedRulesSQLiRuleSet`)** — Filters SQL injection payloads targeting auth and search APIs.
    3. **Known bad inputs (`AWSManagedRulesKnownBadInputsRuleSet`)** — Rejects malformed headers and known vulnerable scanner patterns.
  - Click **Add rules -> Add my own rules and rule groups -> Rule builder**: name it `MediMindRateLimit`, **Type:** `Rate-based rule`, **Rate limit:** `1000` requests per 5 minutes per IP, **Action:** `Block` -> **Create web ACL**.

> **[Screenshot 13: AWS WAF Web ACL `medimind-edge-waf` (Global CloudFront) with 4 Defensive Rules]** — `static/images/5-Workshop/5.4-Deploy-MediMind/13-waf-rules.png`

#### Step 3: Configure Amazon CloudFront & Route 53 DNS

1. Open **AWS Certificate Manager (ACM) Console** and **switch Region to `us-east-1` (N. Virginia)** -> request a **Global ACM Certificate** for `medimind.yourdomain.com` and click **Create records in Route 53** *(required in `us-east-1` for CloudFront custom CNAMEs)*.
2. Open **CloudFront Console -> Distributions -> Create distribution**:
   - **Origin domain:** select **`medimind-alb`** DNS | **Protocol:** `HTTPS only` (TLSv1.2+).
   - **Default cache behavior:** **Viewer protocol policy:** `Redirect HTTP to HTTPS`; **Cache policy:** `CachingDisabled`; **Origin request policy:** `AllViewer`.
   - **Web Application Firewall (WAF):** choose **Use existing WAF configuration** -> select **`medimind-edge-waf`**.
   - **Settings -> Custom SSL certificate:** pick the `us-east-1` ACM certificate and enter **Alternate domain name (CNAME):** `medimind.yourdomain.com` -> **Create distribution**.
   - Open the distribution's **Behaviors -> Create behavior** tab to configure path rules:
     - **Behavior 1 (`/static/*`):** **Cache policy:** `CachingOptimized` (serves CSS, JS, and recipe/UI images from edge within the **1 TB/month Always-Free** tier).
     - **Behavior 2 (`/api/*`, including `/api/auth/*`):** **Cache policy:** `CachingDisabled` + **Origin request policy:** `AllViewer` so clinical triage, OCR uploads, and OAuth callbacks (`/api/auth/google/callback`) bypass edge caching and preserve cookies/headers.
3. In **Route 53 Console -> Hosted zones**, open your domain -> **Create record**: **Record name:** `medimind`, **Record type:** `A`, toggle **Alias** on, **Route traffic to:** `Alias to CloudFront distribution`, select `dxxxxxxxxxxxx.cloudfront.net` -> **Create records**.

> **[Screenshot 14: CloudFront Distribution (`Deployed`, Behaviors `/static/*`, `/api/*`) & Route 53 Alias `A` Record]** — `static/images/5-Workshop/5.4-Deploy-MediMind/14-cloudfront-route53.png`
