---
title: "Introduction"
date: 2026-11-26
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Problem Statement

Many frontline public hospitals in Vietnam routinely operate over capacity, resulting in multi-hour patient wait times and forcing physicians to start consultations without structured pre-visit medical histories. Meanwhile, unverified general-purpose AI chatbots create severe clinical risks:
- **Missed Emergency Golden Hours & Negation Traps:** Simple keyword matchers fail to detect subtle red-flag emergencies or trigger false alarms when patients type *"I have no shortness of breath"* (*"tôi không khó thở"*).
- **Handwritten Prescription & Dosage Errors:** Blurry or abbreviated prescriptions lead to missed schedules, unsafe antibiotic self-medication, and drug/allergy interactions.
- **Medical & Nutritional Hallucinations:** Unconstrained LLMs invent medical citations, fabricate calorie counts, or recommend dishes containing patient allergens.

#### Core Clinical Modules of MediMind Clinical AI

To solve these bottlenecks end-to-end, the codebase implements five tightly integrated modules:

| Module | Core Implementation Files | Key Capabilities & Data Scope |
| :--- | :--- | :--- |
| **1. Clinical Triage & Double Guardrails** | `core/triage.py`, `core/intake_service.py`, `core/chat_service.py` | 3-tier risk stratification (**Green – Yellow – Red**), accent-free Vietnamese & negation pre-check, immediate **Emergency 115** bypass, post-check blocking unauthorized antibiotic prescribing. |
| **2. Multimodal OCR Verification Pipeline** | `core/pipeline_orchestrator.py`, `core/ocr/ocr_parallel_service.py`, `core/ocr/groq_schema_service.py`, `core/ocr/reconciliation_service.py` | Uses **Vision LLM** (`qwen/qwen3.8-27b` via Groq Dual-Key Failover, with an optional local **EasyOCR** branch), reconciles field-by-field (`needs_review=True` on field or schedule/quantity mismatch), validates rules, and links reminders via `/api/notifications` after user confirmation. |
| **3. Grounded Hybrid Medical RAG** | `core/rag_service.py`, `core/reranker_service.py`, `ingest.py` | Hybrid retrieval combining in-house Python **BM25** lexical search, **ChromaDB** vector search over **364 standardized clinical documents** from *MedlinePlus NIH* (paired with triage reference guidelines from *Vietnam MoH – kcb.vn*), bilingual query expansion, and `BAAI/bge-reranker-v2-m3` reranking. |
| **4. Clinical Nutrition Studio** | `core/nutrition/nutrition_meal_planner.py`, `core/nutrition/nutrition_rules.py`, `core/nutrition/monngonmoingay_catalog.py`, `core/nutrition/recipe_catalog.py` | **BMR/TDEE** surveys and deterministic multi-condition + 12-allergen *Fail-Closed* filtering across **2,500 Vietnamese recipes (*Mon Ngon Moi Ngay*)**. |
| **5. 30-Second Summary & Booking** | `core/facilities_service.py`, `core/appointment_service.py`, `core/shared/notification_service.py` | Generates structured **Pre-Consultation Summaries**, supports in-app booking across **2,144 healthcare facilities** (1,505 HCMC + 639 Hanoi), sends confirmation emails to the user's inbox, and persists server-backed alerts. |

#### Target AWS 3-Tier VPC Architecture (`ap-southeast-1`)

![MediMind AWS Architecture](/images/5-Workshop/5.1-Workshop-overview/aws_architecture_current.png)

##### End-to-End Request & Data Flows (Flows 1 – 9)

1. **Flow `1. DNS Query / Response`:** End-user browsers resolve the application domain via **Amazon Route 53** to the nearest edge location.
2. **Flow `2. HTTPS : 443` (Edge Security & CDN):** Traffic passes through **AWS WAF** (OWASP Top 10, SQLi/XSS, and rate-limiting rules) into **Amazon CloudFront** secured by **AWS Certificate Manager (ACM Global)** to cache static assets (`static/css`, `static/js`, `static/images`).
3. **Flow `3. HTTPS : 443` (VPC Ingress):** Dynamic requests (`/api/*`, `/auth/*`) traverse the **Internet Gateway** into **`Amazon VPC (10.0.0.0/16)`** in `ap-southeast-1`.
4. **Flow `4. HTTPS : 443` (ALB TLS Termination):** The **Application Load Balancer (ALB)** in the `Public Subnet` terminates TLS using a regional **ACM** certificate and executes `/health` checks.
5. **Flow `5. HTTP : 8000` (Private App Tier):** ALB forwards traffic on port `8000` (`PORT=8000`) to the containerized **Amazon EC2** instance inside the `Private App Subnet` (zero public IP). EC2 pulls container images from **Amazon ECR**, reads secrets from **AWS Secrets Manager**, streams PII-redacted logs to **Amazon CloudWatch**, persists **ChromaDB (`./medical_vectordb`)** and **`./uploads`** on an attached **Amazon EBS (`gp3`)** volume, and archives snapshots to **Amazon S3**.
6. **Flow `6. SQL : 5432` (Isolated Database Tier):** The application connects over port `5432` (`psycopg2-binary` + SQLAlchemy) to **Amazon RDS for PostgreSQL** inside the `Private Database Subnet`, managing 7 core ORM tables (`users`, `medical_documents`, `prescription_history`, `clinical_consultations`, `intake_sessions`, `medical_appointments`, `user_notifications`).
7. **Flows `7a, 7b, 7c` (Outbound Egress via NAT Gateway):** Outbound API calls from the `Private App Subnet` route through the **NAT Gateway** and **Internet Gateway** to external services:
   - **`7a. Token & UserInfo`:** Exchanges OAuth authorization codes with **Google OAuth 2.0** (`/api/auth/google/callback`).
   - **`7b. Send OTP`:** Sends 6-digit verification codes and appointment confirmation emails via **Gmail SMTP** (`smtp.gmail.com:587`) and **SpeedSMS**.
   - **`7c. LLM / Vision AI`:** Calls **Groq Dual-Key Failover** (`core/ai/llm_provider.py`, `qwen/qwen3.8-27b`) using workload-isolated API keys for clinical chat, verification, OCR extraction, and nutrition ranking.
8. **Flow `8. Google OAuth Consent`:** The user browser interacts directly with Google's OAuth 2.0 consent screen before redirecting back to the application callback.
9. **Flow `9. Healthcare Facility Map`:** The browser renders interactive facility maps and directions across **2,144 clinics** via **Leaflet / OpenStreetMap** (with optional **Google Maps Platform API** support).

#### AWS Services & External Integrations Inventory

| Layer | Service / Component | Purpose in MediMind Clinical AI |
| :--- | :--- | :--- |
| **Edge & DNS** | **Amazon Route 53, AWS WAF, Amazon CloudFront, ACM** | High-availability DNS, Layer-7 firewall, 1 TB/month free edge caching, TLS 1.3 certificates. |
| **Networking** | **Amazon VPC (`10.0.0.0/16`), ALB, NAT Gateway, IGW** | 3-tier network isolation (`Public`, `Private App`, `Private DB`), TLS termination, controlled outbound egress. |
| **Compute & Storage** | **Amazon EC2, Amazon EBS (`gp3`), Amazon ECR, Amazon S3** | Runs Docker container on port `8000`, persists ChromaDB & uploads on EBS, stores private images in ECR, archives encrypted backups in S3. |
| **Database** | **Amazon RDS for PostgreSQL (`db.t4g.micro`)** | Managed relational database (`:5432`) isolated in `Private Database Subnet` replacing local SQLite for production concurrency. |
| **Security & Ops** | **AWS Secrets Manager, Amazon CloudWatch, AWS IAM, AWS Budgets** | Runtime secret injection via `EC2 IAM Role`, PII-redacted centralized logging, and 20 USD Dev budget alerts. |
| **External APIs** | **Groq API (Dual-Key), Google OAuth, Gmail SMTP, SpeedSMS, Leaflet / OpenStreetMap (optional Google Maps)** | Vision/Chat AI inference, multi-channel authentication/OTP, and 2,144-facility geolocation. |

#### Cost Summary (`ap-southeast-1`)

| Environment Scenario | Workload Profile | Monthly Cost (USD) | Key Cost Optimization Lever |
| :--- | :--- | :---: | :--- |
| **Dev / PoC Workshop (Single-AZ)** | ~500 consultations, ~200 OCR scans/month; AWS Free Tier (`t3.micro`/`t3.small`, EFS/EBS, `db.t4g.micro`, S3, ECR, CloudFront) + ~40h ALB/NAT (incl. 3 Public IPv4) | **~16.86 USD / month**<br>*(~202.32 USD / year)* | Local EBS ChromaDB instead of managed Vector DB + Groq Dual-Key Free Tier (`0.00 USD` token cost). |
| **Multi-AZ Production (10,000 MAU)** | 24/7 operation: 10,000 users, 25,000 consultations, 8,000 OCR scans/month (`2 × t3.small` + EFS `/uploads` + RDS Multi-AZ + ALB + `2 × NAT GW` + WAF + Secrets; optional ElastiCache Redis) | **~220.95 – 233.45 USD / month** | **~0.0088 – 0.0093 USD per consultation session**, substantially lower than dedicated GPU clusters and managed vector DBs. |
