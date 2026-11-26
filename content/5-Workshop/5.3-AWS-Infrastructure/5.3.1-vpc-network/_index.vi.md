---
title: "Cấu hình VPC, Subnet và Security Group"
date: 2026-11-26
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

#### Bước 1: Tạo VPC & 6 Subnet qua 2 Availability Zones

1. Mở **Amazon VPC Console** tại khu vực `ap-southeast-1` (Singapore) -> chọn **Your VPCs** -> **Create VPC**:
   - Chọn **Resources to create:** `VPC only` | **Name tag:** `medimind-vpc` | **IPv4 CIDR block:** `10.0.0.0/16` -> nhấn **Create VPC**.
   - Vào lại **Actions** -> **Edit VPC settings** -> tích chọn đồng thời **Enable DNS resolution** và **Enable DNS hostnames** -> **Save** (hoặc chạy CLI):

```bash
export AWS_REGION=ap-southeast-1

VPC_ID=$(aws ec2 create-vpc --cidr-block 10.0.0.0/16 \
  --tag-specifications 'ResourceType=vpc,Tags=[{Key=Name,Value=medimind-vpc}]' \
  --query 'Vpc.VpcId' --output text --region $AWS_REGION)

aws ec2 modify-vpc-attribute --vpc-id $VPC_ID --enable-dns-support '{"Value":true}'
aws ec2 modify-vpc-attribute --vpc-id $VPC_ID --enable-dns-hostnames '{"Value":true}'
```

2. Vào **Subnets** -> **Create subnet** -> chọn VPC `medimind-vpc` và tạo lần lượt **6 Subnet** trải đều trên 2 vùng sẵn sàng `ap-southeast-1a` và `ap-southeast-1b`:

| Tên Subnet | Availability Zone | Dải CIDR | Vai trò trong Kiến trúc |
| :--- | :--- | :--- | :--- |
| `medimind-public-a` | `ap-southeast-1a` | `10.0.1.0/24` | Đặt ALB & NAT Gateway |
| `medimind-public-b` | `ap-southeast-1b` | `10.0.2.0/24` | Dự phòng High Availability cho ALB |
| `medimind-private-app-a` | `ap-southeast-1a` | `10.0.11.0/24` | Đặt máy chủ Amazon EC2 + EBS |
| `medimind-private-app-b` | `ap-southeast-1b` | `10.0.12.0/24` | Subnet dự phòng tầng Ứng dụng |
| `medimind-private-db-a` | `ap-southeast-1a` | `10.0.21.0/24` | Đặt RDS PostgreSQL chính |
| `medimind-private-db-b` | `ap-southeast-1b` | `10.0.22.0/24` | Subnet thứ 2 cho RDS Subnet Group |

#### Bước 2: Khởi tạo Internet Gateway, NAT Gateway & Route Tables

1. **Internet Gateway:** Vào **VPC -> Internet gateways -> Create internet gateway** -> đặt tên `medimind-igw` -> **Create** -> chọn **Actions -> Attach to VPC** -> gắn vào `medimind-vpc`.
2. **NAT Gateway:** Vào **VPC -> NAT gateways -> Create NAT gateway**:
   - **Name:** `medimind-nat-gw` | **Subnet:** chọn `medimind-public-a` | **Connectivity type:** `Public` -> nhấn **Allocate Elastic IP** -> **Create NAT gateway**.
   - Nhờ `medimind-nat-gw`, EC2 ở mạng riêng có thể kéo ECR Image và gọi API ra Groq API (và Gemini fallback), Google OAuth, Gmail SMTP và SpeedSMS nhưng vẫn chặn 100% kết nối chiều vào từ Internet.
3. **Route Tables:** Vào **VPC -> Route tables -> Create route table** tạo 3 bảng định tuyến; ở mỗi bảng vào tab **Subnet associations -> Edit subnet associations** để gắn các Subnet tương ứng và vào tab **Routes -> Edit routes** để thêm tuyến `0.0.0.0/0`:

| Route Table | Subnet Liên kết | Tuyến `0.0.0.0/0` | Tuyến Nội bộ |
| :--- | :--- | :--- | :--- |
| `rt-public` | `medimind-public-a`, `medimind-public-b` | `medimind-igw` | `10.0.0.0/16 -> local` |
| `rt-private-app` | `medimind-private-app-a`, `medimind-private-app-b` | `medimind-nat-gw` | `10.0.0.0/16 -> local` |
| `rt-private-db` | `medimind-private-db-a`, `medimind-private-db-b` | *Không có (cô lập hoàn toàn)* | `10.0.0.0/16 -> local` |

{{% notice note %}}
**Amazon RDS** yêu cầu DB Subnet Group phải có ít nhất 2 Subnet thuộc 2 Availability Zones khác nhau; hãy đảm bảo cả `medimind-private-db-a` và `medimind-private-db-b` đều gắn vào `rt-private-db`.
{{% /notice %}}

#### Bước 3: Thiết lập Security Group Lồng nhau (Chained Security Groups)

Vào **VPC -> Security Groups -> Create security group** (chọn VPC `medimind-vpc`), tạo lần lượt 3 Security Group và thiết lập các tab **Inbound rules** / **Outbound rules** theo nguyên tắc mỗi tầng chỉ tin cậy Security Group ID của tầng đứng ngay trước nó:

| Security Group | Luật Inbound (Giao thức / Cổng / Nguồn) | Luật Outbound |
| :--- | :--- | :--- |
| `sg-medimind-alb` | `HTTPS (443)` và `HTTP (80)` từ CloudFront Prefix List / `0.0.0.0/0` | `TCP 8000` tới `sg-medimind-ec2` |
| `sg-medimind-ec2` | `TCP 8000` **chỉ** từ `sg-medimind-alb` *(không mở cổng SSH 22)* | `TCP 5432` tới `sg-medimind-rds`; `HTTPS (443)` & `587` (SMTP) qua NAT |
| `sg-medimind-rds` | `TCP 5432` **chỉ** từ `sg-medimind-ec2` | Giới hạn nội bộ VPC |

#### Bước 4: Tạo IAM Role `medimind-ec2-role` & Instance Profile

Mở **IAM Console -> Roles -> Create role** -> chọn **Trusted entity type:** `AWS service`, **Use case:** `EC2` -> đặt tên **`medimind-ec2-role`** và gắn các quyền **strict Least Privilege** sau (AWS Console tự động tạo Instance Profile trùng tên; sau khi tạo Role, vào tab **Permissions -> Add permissions -> Create inline policy -> tab JSON** để dán policy thứ 3):
1. Managed policy **`AmazonSSMManagedInstanceCore`** (truy cập shell EC2 qua **Session Manager** không cần mở cổng 22 hay tạo SSH key).
2. Managed policy **`AmazonEC2ContainerRegistryReadOnly`** (kéo Docker Image từ Amazon ECR).
3. Inline policy **`MediMindRuntimeAccess`** cấp quyền đọc Secrets Manager (`medimind/*`), ghi/đọc S3 backup bucket và đẩy log lên CloudWatch:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ReadMediMindSecrets",
      "Effect": "Allow",
      "Action": ["secretsmanager:GetSecretValue", "secretsmanager:DescribeSecret"],
      "Resource": "arn:aws:secretsmanager:ap-southeast-1:*:secret:medimind/*"
    },
    {
      "Sid": "S3BackupAndArchive",
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:GetObject", "s3:ListBucket", "s3:DeleteObject"],
      "Resource": [
        "arn:aws:s3:::medimind-clinical-backup-*",
        "arn:aws:s3:::medimind-clinical-backup-*/*"
      ]
    },
    {
      "Sid": "CloudWatchAppLogs",
      "Effect": "Allow",
      "Action": ["logs:CreateLogGroup", "logs:CreateLogStream", "logs:PutLogEvents"],
      "Resource": "arn:aws:logs:ap-southeast-1:*:log-group:/medimind/*"
    }
  ]
}
```
