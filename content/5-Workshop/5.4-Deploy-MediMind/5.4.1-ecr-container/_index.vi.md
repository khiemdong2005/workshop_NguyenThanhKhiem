---
title: "Build Docker Image & Đẩy lên Amazon ECR"
date: 2026-11-26
weight: 1
chapter: false
pre: " <b> 5.4.1 </b> "
---

#### Rà soát Cấu trúc `Dockerfile` Chuẩn Bảo mật

Tệp `Dockerfile` của dự án áp dụng đầy đủ tiêu chuẩn an toàn container và tối ưu dung lượng:
- **Base Image Gọn nhẹ & Non-Root User:** Sử dụng `python:3.11-slim` và tạo người dùng không đặc quyền `appuser` (`UID 1000`, `GID 1000`) sở hữu các thư mục `/app/medical_vectordb`, `/app/instance`, `/app/uploads` và `/home/appuser/.cache/huggingface`.
- **Tham số Tùy chọn BGE Reranker (`INSTALL_RERANKER`):** Mặc định `INSTALL_RERANKER=false` giữ image nhẹ (~450 MB, nằm trong hạn mức 500 MB Free Tier của Private ECR). Bật `--build-arg INSTALL_RERANKER=true` khi cần kích hoạt mô hình tái xếp hạng cục bộ `BAAI/bge-reranker-v2-m3`.
- **Healthcheck & Entrypoint:** Mở cổng `8000`, tích hợp `HEALTHCHECK` kiểm tra `http://localhost:8000/health` và khởi chạy `uvicorn core.main_fastapi:app --host 0.0.0.0 --port 8000 --proxy-headers --forwarded-allow-ips=*`.

#### Bước 1: Tạo Kho lưu trữ Amazon ECR Riêng tư (Scan-on-Push)

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

#### Bước 2: Đăng nhập ECR, Build và Push Docker Image

```bash
# 1. Đăng nhập Docker CLI vào Amazon ECR
aws ecr get-login-password --region $AWS_REGION | \
  docker login --username AWS --password-stdin $ECR_URI

# 2. Build image production (đặt INSTALL_RERANKER=true nếu dùng reranker cục bộ)
docker build --build-arg INSTALL_RERANKER=false -t medimind-clinical-ai:v1.0.0 .

# 3. Gắn tag và đẩy image lên ECR
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

#### Bước 3: Kiểm tra Báo cáo Quét Lỗ hổng Bảo mật

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
*(hoặc `{}` nếu không phát hiện CVE; đảm bảo `CRITICAL` = `0` trước khi triển khai).*

{{% notice warning %}}
Trước khi chạy `docker build`, hãy kiểm tra lại tệp `.dockerignore` đã liệt kê đầy đủ `.env`, `instance/`, `medical_vectordb/` và `uploads/`. Vì `Dockerfile` dùng `COPY --chown=appuser:appuser . .`, nếu thiếu các dòng này trong `.dockerignore`, CSDL SQLite cục bộ, chỉ mục ChromaDB hoặc ảnh bệnh nhân tải lên máy cá nhân sẽ bị đóng gói thẳng vào Docker Image đẩy lên ECR (vừa phình image vượt 500 MB Free Tier, vừa gây lộ dữ liệu cục bộ).
{{% /notice %}}
