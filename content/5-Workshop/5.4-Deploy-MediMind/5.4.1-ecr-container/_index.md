---
title: "Build Docker Image & Push to Amazon ECR"
date: 2026-11-26
weight: 1
chapter: false
pre: " <b> 5.4.1 </b> "
---

#### Review the Hardened `Dockerfile`

The project `Dockerfile` implements container security and build-caching best practices:
- **Slim Base Image & Non-Root Execution:** Uses `python:3.11-slim` and creates an unprivileged user `appuser` (`UID 1000`, `GID 1000`) owning `/app/medical_vectordb`, `/app/instance`, `/app/uploads`, and `/home/appuser/.cache/huggingface`.
- **Optional BGE Reranker Layer (`INSTALL_RERANKER`):** Defaults to `INSTALL_RERANKER=false` (~450 MB footprint, keeping Amazon ECR within the 500 MB Free Tier limit). Set `--build-arg INSTALL_RERANKER=true` when enabling local `BAAI/bge-reranker-v2-m3` cross-encoder reranking.
- **Built-in Health Probe & Entrypoint:** Exposes port `8000`, configures `HEALTHCHECK` against `http://localhost:8000/health`, and launches `uvicorn core.main_fastapi:app --host 0.0.0.0 --port 8000 --proxy-headers --forwarded-allow-ips=*`.

#### Step 1: Create a Private ECR Repository with Scan-on-Push

```bash
export AWS_REGION=ap-southeast-1
export ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
export ECR_URI="${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"

aws ecr create-repository \
  --repository-name medimind-clinical-ai \
  --image-scanning-configuration scanOnPush=true \
  --encryption-configuration encryptionType=AES256 \
  --region $AWS_REGION
```

#### Step 2: Authenticate Docker, Build & Push Image

```bash
# 1. Authenticate Docker CLI to Amazon ECR
aws ecr get-login-password --region $AWS_REGION | \
  docker login --username AWS --password-stdin $ECR_URI

# 2. Build the production image (use INSTALL_RERANKER=true if enabling local reranker)
docker build --build-arg INSTALL_RERANKER=false -t medimind-clinical-ai:v1.0.0 .

# 3. Tag and push both versioned and latest tags to ECR
docker tag medimind-clinical-ai:v1.0.0 ${ECR_URI}/medimind-clinical-ai:v1.0.0
docker tag medimind-clinical-ai:v1.0.0 ${ECR_URI}/medimind-clinical-ai:latest
docker push ${ECR_URI}/medimind-clinical-ai:v1.0.0
docker push ${ECR_URI}/medimind-clinical-ai:latest
```

**Expected Output:**

```text
Login Succeeded
...
v1.0.0: digest: sha256:8c2f... size: 2841
latest: digest: sha256:8c2f... size: 2841
```

#### Step 3: Verify Vulnerability Scan Results

```bash
aws ecr describe-image-scan-findings \
  --repository-name medimind-clinical-ai \
  --image-id imageTag=v1.0.0 \
  --region $AWS_REGION \
  --query 'imageScanFindings.findingSeverityCounts'
```

**Expected Output:**

```json
{
    "MEDIUM": 2,
    "LOW": 5
}
```
*(or `{}` when zero CVEs are reported; confirm zero `CRITICAL` findings before deploying).*

{{% notice warning %}}
Before running `docker build`, verify that `.dockerignore` explicitly excludes `.env`, `instance/`, `medical_vectordb/`, and `uploads/`. Because `Dockerfile` executes `COPY --chown=appuser:appuser . .`, omitting those directories will bake local SQLite databases, ChromaDB vectors, or local user uploads into the ECR image (both bloating the image beyond the 500 MB Free Tier limit and risking local data exposure).
{{% /notice %}}
