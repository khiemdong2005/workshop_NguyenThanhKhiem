---
title: "Provision RDS PostgreSQL, S3 & Secrets Manager"
date: 2026-11-26
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---

#### Step 1: Provision Amazon RDS for PostgreSQL (Private DB Subnet)

While local development defaults to SQLite (`sqlite:///./instance/medimind.db`), production deployment replaces SQLite with **Amazon RDS for PostgreSQL** via `DATABASE_URL` and `psycopg2-binary` to guarantee ACID transactions and concurrent worker safety.

1. In the **RDS Console** (`ap-southeast-1`), go to **Subnet groups -> Create DB subnet group**: name it `medimind-db-subnet-group`, select **VPC** `medimind-vpc`, choose AZs `ap-southeast-1a` & `ap-southeast-1b`, add `medimind-private-db-a` (`10.0.21.0/24`) and `medimind-private-db-b` (`10.0.22.0/24`), and click **Create**.
2. Go to **Databases -> Create database** -> select **Standard create** -> **Engine type:** `PostgreSQL` (`16.x`), **Templates:** `Free tier`, and configure:
   - **DB instance identifier:** `medimind-pg-db` | **Master username:** `medimind_admin` (set a strong password)
   - **Instance configuration:** `Burstable classes` -> `db.t4g.micro` (2 vCPU, 1 GB RAM — covered by 750h Free Tier)
   - **Storage:** `20 GiB` `General Purpose SSD (gp3)`; expand **Additional storage configuration** and ensure **Enable storage encryption (AWS KMS)** is checked
   - **Connectivity:** `Don't connect to an EC2 compute resource`, **VPC:** `medimind-vpc`, **DB subnet group:** `medimind-db-subnet-group`, **Public access:** `No`, **Existing VPC security groups:** `sg-medimind-rds` (`TCP 5432`)
   - **Additional configuration:** **Initial database name:** `medimind` -> click **Create database**. Once status becomes `Available`, copy the **Endpoint** (`<RDS_ENDPOINT>`) from the **Connectivity & security** tab.

When the Flask/SQLAlchemy startup routine (`create_app()`) runs on EC2, `core/models.py` initializes and migrates the 7 relational tables:

| Table (`__tablename__`) | ORM Model | Stored Clinical & Application Data |
| :--- | :--- | :--- |
| `users` | `User` | Accounts (`patient` / `doctor`), hashed passwords, Google `sub`, BHYT & clinical profile |
| `medical_documents` | `MedicalDocument` | Uploaded lab/prescription file metadata, SHA/storage path, owner RBAC, diagnosis |
| `prescription_history` | `PrescriptionHistory` | Verified medication schedules (*Morning – Noon – Afternoon – Evening*) |
| `clinical_consultations` | `ClinicalConsultation` | Triage risk level/score, differential summary, grounded citations |
| `intake_sessions` | `IntakeSessionRecord` | Multi-turn structured intake state & confirmed Pre-Consultation Summary |
| `medical_appointments` | `MedicalAppointment` | Booked clinic appointments across the 2,144 facilities |
| `user_notifications` | `UserNotification` | Server-backed medication reminders & appointment booking/cancellation alerts |

#### Step 2: Create the Encrypted Amazon S3 Backup Bucket & Lifecycle Policy

MediMind persists live ChromaDB vectors and uploads on EBS for sub-millisecond local I/O while archiving encrypted backups and prescription snapshots to **Amazon S3**:

```bash
ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
BACKUP_BUCKET="medimind-clinical-backup-${ACCOUNT_ID}"

aws s3api create-bucket \
  --bucket $BACKUP_BUCKET \
  --region ap-southeast-1 \
  --create-bucket-configuration LocationConstraint=ap-southeast-1

# Block all public access & enable default SSE-S3 encryption + versioning
aws s3api put-public-access-block \
  --bucket $BACKUP_BUCKET \
  --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"

aws s3api put-bucket-versioning \
  --bucket $BACKUP_BUCKET \
  --versioning-configuration Status=Enabled
```

Apply an **S3 Lifecycle Policy** (`lifecycle.json`) to transition aged backups to **S3 Standard-IA** after 30 days and **S3 Glacier** after 90 days:

```json
{
  "Rules": [
    {
      "ID": "MediMindBackupArchiveTiering",
      "Status": "Enabled",
      "Filter": { "Prefix": "backups/" },
      "Transitions": [
        { "Days": 30, "StorageClass": "STANDARD_IA" },
        { "Days": 90, "StorageClass": "GLACIER" }
      ]
    }
  ]
}
```

```bash
aws s3api put-bucket-lifecycle-configuration \
  --bucket $BACKUP_BUCKET \
  --lifecycle-configuration file://lifecycle.json
```

#### Step 3: Store Sensitive Runtime Credentials in AWS Secrets Manager

Create **3 secret groups** (`$0.40/secret/month` = `$1.20/month`) so zero API keys or DB passwords are ever baked into Docker images or Git:

```bash
# 1. Core App & RDS Connection Secret
aws secretsmanager create-secret \
  --name medimind/app-db \
  --description "MediMind Flask secret key and RDS PostgreSQL URI" \
  --secret-string '{
    "SECRET_KEY": "<GENERATED_64_HEX_SECRET>",
    "DATABASE_URL": "postgresql+psycopg2://medimind_admin:<DB_PASS>@<RDS_ENDPOINT>:5432/medimind"
  }' --region ap-southeast-1

# 2. Multi-Channel Authentication & OTP Secret
aws secretsmanager create-secret \
  --name medimind/auth-otp \
  --description "Google OAuth 2.0, Gmail SMTP, SpeedSMS, and Maps keys" \
  --secret-string '{
    "GOOGLE_CLIENT_ID": "<GOOGLE_CLIENT_ID>",
    "GOOGLE_CLIENT_SECRET": "<GOOGLE_CLIENT_SECRET>",
    "GOOGLE_REDIRECT_URI": "https://medimind.yourdomain.com/api/auth/google/callback",
    "SMTP_USERNAME": "<EMAIL>@gmail.com",
    "SMTP_PASSWORD": "<GMAIL_APP_PASSWORD>",
    "SPEEDSMS_AUTH_TOKEN": "<SPEEDSMS_TOKEN>",
    "GOOGLE_MAPS_API_KEY": "<MAPS_API_KEY>"
  }' --region ap-southeast-1

# 3. Workload-Isolated Groq Dual-Key AI Provider Keys (with optional Gemini fallback)
aws secretsmanager create-secret \
  --name medimind/ai-providers \
  --description "Groq Dual-Key Failover and task-specific keys (plus optional Gemini fallback)" \
  --secret-string '{
    "AI_PROVIDER": "groq",
    "GROQ_MODEL": "qwen/qwen3.8-27b",
    "GROQ_API_KEY": "<GROQ_PRIMARY_KEY>",
    "GROQ_API_KEY_2": "<GROQ_SECONDARY_FAILOVER_KEY>",
    "GROQ_CHAT_API_KEY": "<GROQ_CHAT_KEY>",
    "GROQ_OCR_API_KEY": "<GROQ_OCR_KEY>",
    "GROQ_NUTRITION_API_KEY": "<GROQ_NUTRITION_KEY>",
    "GEMINI_API_KEY": "<OPTIONAL_GEMINI_FALLBACK_KEY>"
  }' --region ap-southeast-1
```
