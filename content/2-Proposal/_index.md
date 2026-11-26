---
title: "Proposal"
date: 2026-09-14
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# MediMind Clinical AI  
## Unified AWS Clinical Assistant, Prescription Cross-Verification & Smart Healthcare Platform  

### 1. Executive Summary  
MediMind Clinical AI is designed to support initial symptom triage, prescription/lab-result cross-verification, medication reminders, and personalized clinical nutrition for patients and doctors in Vietnam. The platform combines a **Hybrid RAG architecture (BM25 + ChromaDB Vector + Cross-Encoder Reranker)** indexed over 364 standardized medical documents (*Vietnam Ministry of Health, kcb.vn, MedlinePlus NIH*), **Clinical Triage & Double Guardrails**, and a **Multimodal OCR Verification Pipeline** running EasyOCR in parallel with Vision LLMs (`qwen/qwen3.8-27b` via Groq API Dual-Key Failover). Containerized with Docker and deployed on **Amazon Web Services (AWS)** in the `ap-southeast-1` (Singapore) region, the system leverages a Multi-AZ 3-tier isolated VPC architecture compliant with the **AWS Well-Architected Framework** and **HIPAA-aligned security controls** (encryption in transit and at rest, Private Subnet isolation, least-privilege IAM, and PII log redaction).  

### 2. Problem Statement  
*Current Problem*  
Frontline public hospitals frequently operate at 150% – 200% capacity, resulting in 2 – 4 hour patient wait times and a lack of structured pre-consultation medical histories for doctors. Meanwhile, self-diagnosing through unverified AI tools leads to missed emergency "golden hours." Standard chatbots also struggle with negation traps (triggering false alarms when users type *"no shortness of breath"*) or hallucinating medical citations and allergenic meal recommendations. In addition, single-model OCR tools frequently misread blurry prescriptions and cause dosage errors, patients often forget their medication schedules (before/after meals), and they lack safe nutrition guidance tailored to their clinical conditions, allergies, and local Vietnamese dishes.  

*Solution*  
The platform delivers a closed-loop healthcare workflow across five core modules: (1) Multi-turn symptom intake and 3-tier risk stratification (**Green – Yellow – Red**), handling unaccented Vietnamese and negation phrases to trigger immediate **Emergency 115** alerts; (2) A multimodal OCR verification pipeline running EasyOCR and Vision LLMs in parallel, cross-checking fields, flagging discrepancies or schedule/quantity mismatches (`needs_review`), and generating visual medication schedules (*Morning – Noon – Afternoon – Evening; Before/After meals*) linked to a **server-backed in-app notification bell** upon user confirmation; (3) Grounded medical Q&A backed by 364 verified clinical documents; (4) Clinical nutrition recommendations combining **BMR/TDEE surveys**, **12 clinical/goal contexts**, and deterministic **12-allergen** *Fail-Closed Allergy Filtering* across **4,962 live Vietnamese recipes** (**2,462 ViFoodRec** + **2,500 Mon Ngon Moi Ngay**, plus **34 curated fallback options**); and (5) A 30-second Pre-Consultation Summary supporting in-app appointment scheduling across a directory of **2,144 healthcare facilities** (1,505 in HCMC and 639 in Hanoi), sending confirmation emails to the user's inbox and updating booking/cancellation alerts in the in-app notification bell. The workload runs on **Amazon EC2 (Auto Scaling Group) + Amazon EFS** and **Amazon RDS PostgreSQL (Multi-AZ)**, protected at the edge by **AWS WAF**, **CloudFront**, and **ALB**.  

*Benefits and Return on Investment (ROI)*  
The solution reduces initial medical history intake to 30 seconds, minimizes home dosage errors and missed medication doses, and prevents adverse drug/food allergy events via *Human-in-the-Loop* confirmation and server-backed reminder notifications. By packaging the read-only ChromaDB vector index (`medical_vectordb`, ~43 MB) via Docker/S3 onto EC2 local EBS and using **Amazon EFS** for `/uploads` instead of costly managed vector databases, alongside **Groq API Dual-Key Failover** within free tiers during PoC, **Dev/PoC Workshop** infrastructure costs stay at **~16.86 USD/month** (~202.32 USD/12 months), while a full **Multi-AZ Production** deployment for 10,000 monthly users costs approximately **220.95 – 233.45 USD/month** (**~0.0088 – 0.0093 USD per consultation session**)—substantially lower than running dedicated GPU clusters and managed vector databases.  

### 3. Solution Architecture  
The platform adopts an **AWS 3-Tier Multi-AZ VPC (`10.0.0.0/16`)** architecture spanning two Availability Zones (`ap-southeast-1a` and `ap-southeast-1b`) in `ap-southeast-1` to completely isolate compute and database layers from direct public Internet access. Incoming user traffic routes through **Amazon Route 53**, **AWS WAF**, and **Amazon CloudFront** to an **Application Load Balancer (ALB)** in the `Public Subnet`, forwarding internal requests on port `8000` to Docker containers on **Amazon EC2** instances within an **Auto Scaling Group** inside `Private App Subnet 1 & 2`. Uploaded files (`./uploads`) are shared across EC2 instances via **Amazon EFS** with backups to **Amazon S3** over an **S3 Gateway Endpoint** (while the read-only **ChromaDB index `./medical_vectordb`** is baked into the Docker image or synced from S3 to each EC2's local EBS volume to prevent SQLite-over-NFS file locking), and seven transactional tables reside in **Amazon RDS for PostgreSQL (Primary & Standby with Sync Replication)** (`SQL :5432`) inside `Private Database Subnet 1 & 2`. All outbound requests to **Groq API**, **Google OAuth 2.0**, and **Gmail SMTP / SpeedSMS** traverse **NAT Gateway 1 & 2**.  

![MediMind Clinical AI AWS Multi-AZ Architecture](/images/2-Proposal/architecture.jpg)


*AWS Services Used*  
- *Amazon Route 53 & Amazon CloudFront*: High-availability DNS routing, static asset edge caching (1 TB free/month), and backend origin masking.  
- *AWS WAF & AWS Certificate Manager (ACM)*: Layer-7 firewall defending against OWASP Top 10 and rate abuse, paired with free SSL/TLS 1.3 certificates (Global `us-east-1` for CloudFront and Regional `ap-southeast-1` for ALB).  
- *Application Load Balancer (ALB) & NAT Gateway*: Handles TLS termination in the `Public Subnet` and provides secure outbound internet access for `Private App Subnet 1 & 2`.  
- *Amazon EC2 (Auto Scaling Group) & Amazon EFS*: Hosts the containerized application (`PORT=8000`) with auto-scaling capacity, **Amazon EFS** shared storage for `/uploads`, and local EBS storage for the read-only ChromaDB index (364 documents).  
- *Amazon RDS for PostgreSQL (Multi-AZ)*: Fully managed relational database isolated in `Private Database Subnet 1 & 2` (`SQL :5432`) with synchronous Primary/Standby replication and automatic failover, storing user, document, prescription, notification, intake, and appointment records.  
- *Amazon ElastiCache for Redis (optional Multi-AZ scale-out)*: Stores shared OTP and rate-limiting state across EC2 instances in the Auto Scaling Group (alternatively backed by RDS PostgreSQL in cost-saving mode).  
- *Amazon S3, S3 Gateway Endpoint & Amazon ECR*: Stores encrypted backups/archives of medical uploads and RAG snapshots via a private **S3 Gateway Endpoint**, plus private Docker container images in ECR.  
- *AWS Secrets Manager, CloudWatch, AWS IAM, Cost Explorer & AWS Budgets*: Centralizes runtime API secrets, collects PII-redacted application logs/metrics/alarms, enforces least-privilege access via an `EC2 IAM Role`, and monitors cost alerts.  

*Component Design*  
- *Edge & Security Layer*: Route 53, WAF, CloudFront, and ALB filter malicious traffic and enforce end-to-end HTTPS encryption.  
- *Application & AI Layer (`Private App Subnet`)*: Python backend (`app.py` / `core/main_fastapi.py`) orchestrating Double Guardrails, Hybrid RAG (BM25 + ChromaDB + BGE Reranker), multimodal OCR cross-checking, in-app notification bell (`/api/notifications`) for appointments and medication reminders, deterministic nutrition rule filtering (12 clinical contexts, 12 allergen groups, 10 avoidance rules), and Circuit Breaker fallbacks.  
- *Data & Storage Layer (`Private Database Subnet` & Storage)*: RDS PostgreSQL (Primary & Standby) manages seven core tables (`users`, `medical_documents`, `prescription_history`, `clinical_consultations`, `intake_sessions`, `medical_appointments`, `user_notifications`); **shared Redis** (Amazon ElastiCache `cache.t4g.micro` or PostgreSQL-backed fallback) handles OTP and rate-limiting state across multi-EC2 deployments; **Amazon EFS** shares `/uploads`; **local EBS** holds read-only ChromaDB indices; **Amazon S3** retains long-term backups.  
- *External Integrations*: Google OAuth 2.0 login, 6-digit OTP and appointment confirmation emails via Gmail SMTP / SpeedSMS, multi-key AI inference via **Groq Dual-Key Failover**, and interactive facility mapping across 2,144 clinics via Google Maps Platform API.  

### 4. Technical Implementation  
*Implementation Phases*  
The project was executed from clinical core engineering to AWS cloud deployment across four phases:  
1. *Research & Architecture Design*: Standardized medical datasets, designed the AWS 3-Subnet Multi-AZ VPC architecture, 7-table PostgreSQL schema, and REST API specifications (Weeks 1–2).  
2. *Clinical Core & RAG Development*: Built Double Guardrails with negation handling, indexed 364 medical documents in Hybrid RAG, and engineered the multimodal OCR cross-verification pipeline (Weeks 3–6).  
3. *Feature Expansion & Web SPA*: Integrated **4,962 live Vietnamese recipes** (**2,462 ViFoodRec** + **2,500 Mon Ngon Moi Ngay**, 34 curated options, 2,474 verified dish photos) with BMR/TDEE surveys, 2,144 healthcare facilities, appointment booking, in-app notifications, OAuth/OTP authentication, and the Web SPA (Weeks 7–8).  
4. *Containerization, AWS Deployment & Verification*: Packaged Docker images to Amazon ECR, provisioned EC2 (Auto Scaling Group) + EFS + RDS (Multi-AZ) + ALB + WAF + Secrets Manager, and validated 95 automated test files against quality checks (Weeks 9–12).  

*Technical Requirements*  
- *Backend & AI Pipeline*: Python (`Flask` / `FastAPI` gateway, `SQLAlchemy`), `ChromaDB`, `rank-bm25`, `BAAI/bge-reranker-v2-m3`, `EasyOCR`, `Redis` (OTP/RateLimit), and multi-key **Groq Dual-Key** integration (`GROQ_API_KEY`, `GROQ_API_KEY_2`, `GROQ_CHAT_API_KEY`, `GROQ_OCR_API_KEY`, `GROQ_NUTRITION_API_KEY`) protected by Circuit Breaker and HTTP 429 Retry policies.  
- *File & Data Hardening*: Magic-byte binary validation, anti-Decompression/Zip Bomb limits (images ≤ 25 MP, PDFs ≤ 30 pages, DOCX compression ratio < 50x), CSRF protection, and automated PII redaction in logs.  
- *AWS Infrastructure*: VPC `10.0.0.0/16` in `ap-southeast-1`, strict Security Group chaining across ALB (`443`), EC2 (`8000`), and RDS (`5432`), and runtime secret injection via AWS Secrets Manager and EC2 IAM Role.  

### 5. Roadmap & Milestones  
- *Pre-Internship (Month 0)*: Assessed frontline hospital triage bottlenecks and curated 364 clinical guidelines (*Vietnam Ministry of Health, MedlinePlus NIH*), **4,962 live Vietnamese recipes** (**2,462 ViFoodRec** + **2,500 Mon Ngon Moi Ngay**; 5,862 total cleaned recipes), and 2,144 medical facilities.  
- *Internship (Months 1–3 / 12 Weeks)*:  
  - Month 1 (Weeks 1–4): Designed the AWS 3-Subnet VPC architecture, core Clinical Triage engine, Double Guardrails, and relational database schema.  
  - Month 2 (Weeks 5–8): Completed Hybrid RAG, multimodal OCR verification pipeline, Clinical Nutrition Studio (BMR/TDEE + multi-condition filtering), facility booking, in-app notifications, and Web SPA interface.  
  - Month 3 (Weeks 9–12): Pushed Docker images to Amazon ECR, deployed on EC2 + EFS + RDS (Multi-AZ) + ALB + WAF, executed 95 automated test files (`pytest`), and prepared the Workshop Live Demo.  
- *Post-Deployment*: Expand interoperability with HL7 FHIR health record standards and pilot deployment in satellite outpatient clinics.  

### 6. Budget Estimation  
Costs were estimated using AWS On-Demand pricing in the **Singapore (`ap-southeast-1`)** region across two scenarios: **Dev/PoC Workshop** (Single-AZ leveraging AWS Free Tier / Free Tier Credits with on-demand ALB/NAT demo hours torn down afterward) and **Multi-AZ Production** (matching the Section 3 architecture for 10,000 monthly active users running 24/7).  

*Infrastructure Costs (Dev / PoC Workshop Environment)*  
- Amazon EC2 (`t3.micro` / `t3.small`, port 8000): 0.00 – 3.17 USD/month (`t3.micro` covered by 750 hours/month Free Tier with swap/local reranker disabled; `t3.small` 2 GB RAM ~120 demo hours at ~0.0264 USD/hour).  
- Amazon EFS / EBS (`/uploads` & `medical_vectordb` ~43 MB within 5 GB EFS Free Tier / Free Tier Credits and 30 GB EBS Free Tier): 0.00 USD/month.  
- Amazon RDS for PostgreSQL (`db.t4g.micro` Single-AZ, port 5432): 0.00 USD/month (covered by 750 hours + 20 GB Free Tier for the first 12 months).  
- Application Load Balancer & 1 NAT Gateway (~40 demo/testing hours): ~3.97 USD/month (3.37 USD hourly ALB + NAT GW charges plus ~0.60 USD for 3 Public IPv4 addresses on ALB/NAT, as the 750 free IPv4 hours apply to EC2 only).  
- Amazon S3 (`Backup / Archive` ~2 GB), S3 Gateway Endpoint & Amazon ECR: ~0.00 – 0.15 USD/month (500 MB/month private ECR Free Tier for 12 months; ~0.05–0.15 USD/month if the EasyOCR/OpenCV image exceeds 1–2 GB).  
- AWS Secrets Manager (3 secret groups): 1.20 USD/month (0.40 USD/secret).  
- Amazon CloudFront (15 GB), ACM (TLS 1.3), CloudWatch, AWS IAM, Cost Explorer & AWS Budgets: 0.00 USD/month (Always-Free / Free Tier).  
- Amazon Route 53 (1 Hosted Zone + 50,000 queries): 0.52 USD/month.  
- AWS WAF (1 Web ACL + 3 Managed Rules, full month): 8.00 USD/month (5.00 USD Web ACL + 1.00 USD × 3 rule groups; ~0.44 USD if enabled only for 40 demo hours).  
- External AI & Auth Services (Groq API Dual-Key Free Tier, Gmail SMTP, Google OAuth, Google Maps Platform within free tier): 0.00 USD/month.  

*Total (Dev / PoC Workshop)*: **~16.86 USD/month** (~202.32 USD/12 months; delete/stop ALB & NAT Gateway after demos to avoid ~72 USD/month 24/7 baseline charges).  

*Multi-AZ Production Scaling Estimate (10,000 users / 25,000 consultations / 8,000 OCR scans per month, 24/7 — aligned with Section 3 diagram)*  
- 2 × Amazon EC2 (`t3.small` in Auto Scaling Group, `2 × 0.0264 USD/hr × 730h`): ~38.54 USD/month.  
- Amazon EFS Standard (~5 GB for `/uploads`) & 2 × root EBS (`gp3` 20 GB for read-only `medical_vectordb`): ~5.64 USD/month.  
- Amazon RDS for PostgreSQL Multi-AZ (`db.t4g.micro` Primary + Standby ~0.050 USD/hr + 20 GB `gp3` Multi-AZ): ~41.10 USD/month.  
- 1 × ALB + 2 × NAT Gateways (24/7) + 4 Public IPv4 addresses (14.60 USD) + LCU/Data Processing (~20 GB): ~122.32 USD/month.  
- Amazon ElastiCache Redis (`cache.t4g.micro` — optional addition beyond the base diagram for shared OTP/rate-limit state across 2 EC2s): ~12.50 USD/month *(or 0.00 USD if OTP/rate-limit state is stored on RDS PostgreSQL)*.  
- AWS WAF (~8.60 USD) + Secrets Manager (1.20 USD) + Route 53 (~0.70 USD) + S3/ECR/CloudWatch (~2.85 USD) + CloudFront (< 1 TB Always-Free): ~13.35 USD/month.  
- *Total Multi-AZ Production AWS Infrastructure*: **~233.45 USD/month** (with ElastiCache Redis; or **~220.95 USD/month** using RDS-backed state), equivalent to **~0.0088 – 0.0093 USD per consultation session** (excludes Groq pay-as-you-go API upgrades if high traffic exceeds free-tier rate limits).  

### 7. Risk Assessment  
*Risk Matrix*  
- Missed emergency red flags or negation traps (*"no shortness of breath"*): High impact, medium probability.  
- OCR misinterpretation on blurry or glaring handwritten prescriptions or HTTP 429 rate limits: High impact, medium probability.  
- Malicious file uploads (Decompression/Zip Bombs) or unauthorized record access (IDOR): High impact, low probability.  
- External AI provider outages (Groq API) or budget overruns: Medium impact, low probability.  

*Mitigation Strategies*  
- Clinical & Negation Safety: Double Guardrails (`core/triage.py`) pair deterministic emergency keyword pre-checks (supporting unaccented Vietnamese and negation phrases) with LLM response post-checks to trigger Emergency 115 guidance on red flags and block unauthorized antibiotic prescriptions.  
- Prescription OCR Verification & Reminders: Parallel EasyOCR + Vision LLM execution with HTTP 429 retry/Dual-Key Failover, automated `needs_review=True` flagging on field or schedule/quantity mismatches, mandatory *Human-in-the-Loop* user confirmation before saving medication schedules, and server-backed in-app reminder notifications.  
- Security & Cost Control: Strict Private Subnet isolation for EC2 and RDS, magic-byte & size validation (`core/storage_service.py`), PII log redaction, and **AWS Budgets** alerts set at a 20 USD threshold.  

*Contingency Plan*  
- Trigger the **Circuit Breaker** (`core/circuit_breaker.py`) after 5 consecutive external API failures to fail over seamlessly to the local **Fallback Clinical Engine** and deterministic nutrition filtering without UI downtime.  
- Rapidly restore ChromaDB indices and relational records from encrypted **Amazon S3** backups and automated **Amazon RDS** snapshots.  

### 8. Expected Results  
*Technical Improvements*  
Deliver a production-ready multimodal clinical AI platform backed by **95 automated test files (`pytest`)** covering symptom triage (negation handling and emergency red flags), parallel prescription OCR verification, Hybrid RAG retrieval across 364 standardized clinical documents, deterministic allergy/condition nutrition filtering, and appointment scheduling with medication reminders plus Circuit Breaker failover during external AI outages.  

*Long-Term Value*  
Establish a secure, cost-efficient AWS Multi-AZ reference architecture (**~0.0088 – 0.0093 USD per session** at 10,000-user scale) that can be reused and scaled across outpatient clinics and primary healthcare facilities to reduce triage congestion and improve medication safety.
