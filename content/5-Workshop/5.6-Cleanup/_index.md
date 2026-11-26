---
title: "Clean up"
date: 2026-11-26
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

Congratulations on completing the **MediMind Clinical AI on AWS** workshop! You successfully designed a 3-Tier isolated VPC, deployed a containerized clinical AI workload backed by EBS ChromaDB and RDS PostgreSQL, hardened the edge with Route 53, WAF, CloudFront, ACM, and ALB, and verified all safety quality gates.

#### Dependency-Ordered Cleanup Checklist

To avoid dangling Elastic Network Interfaces (ENIs) or unexpected AWS charges after the demo, delete resources in the exact dependency order below:

1. **Amazon Route 53:** Delete the `A` Alias record pointing to your CloudFront distribution inside your Hosted Zone.
2. **Amazon CloudFront & AWS WAF:** Disable and delete the CloudFront distribution, then delete the `medimind-edge-waf` Web ACL (`CLOUDFRONT` scope).
3. **Application Load Balancer & ACM:** Delete `medimind-alb`, target group `medimind-tg`, and any unused regional/global ACM certificates.
4. **Amazon EC2 & Amazon EBS:** Terminate `medimind-app-server` and verify both the root volume and the 20 GB ChromaDB `gp3` EBS volume are deleted (or detach and delete if `DeleteOnTermination` was disabled).
5. **NAT Gateway & Elastic IP:** Delete `medimind-nat-gw`, wait for its status to become `Deleted`, and **explicitly release the associated Elastic IP (EIP)**.
6. **Amazon RDS PostgreSQL & DB Subnet Group:** Delete `medimind-pg-db` (skip final snapshot for workshop labs), wait until deletion completes, then delete `medimind-db-subnet-group`.
7. **Amazon S3 & Amazon ECR:** Because **S3 Versioning** was enabled in Section 5.3.2, `aws s3 rm --recursive` only writes *Delete Markers* and leaves old object versions intact (causing `BucketNotEmpty` on `aws s3 rb`). In the S3 Console click **Empty** and type *`permanently delete`*, or purge all `Versions` and `DeleteMarkers` via CLI before deleting the bucket and ECR repository:

```bash
export AWS_REGION=ap-southeast-1
export ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
export BACKUP_BUCKET="medimind-clinical-backup-${ACCOUNT_ID}"

# Purge all S3 Object Versions and DeleteMarkers before removing the bucket
python3 - << 'EOF'
import os, json, subprocess
b = os.environ["BACKUP_BUCKET"]
data = json.loads(subprocess.check_output(["aws", "s3api", "list-object-versions", "--bucket", b]))
objs = [{"Key": x["Key"], "VersionId": x["VersionId"]} for k in ("Versions", "DeleteMarkers") for x in data.get(k, [])]
for i in range(0, len(objs), 1000):
    subprocess.check_call(["aws", "s3api", "delete-objects", "--bucket", b, "--delete", json.dumps({"Objects": objs[i:i+1000]})])
EOF

aws s3 rb s3://${BACKUP_BUCKET} --region $AWS_REGION

# Delete ECR repository and all stored image layers
aws ecr delete-repository --repository-name medimind-clinical-ai --force --region $AWS_REGION
```

8. **Secrets Manager, CloudWatch Logs & IAM Role:** Delete the 3 secrets (`medimind/app-db`, `medimind/auth-otp`, `medimind/ai-providers`), delete log group `/medimind/clinical-api`, and remove `medimind-ec2-role` plus its instance profile:

```bash
for SECRET_ID in medimind/app-db medimind/auth-otp medimind/ai-providers; do
  aws secretsmanager delete-secret --secret-id $SECRET_ID --force-delete-without-recovery --region $AWS_REGION
done
aws logs delete-log-group --log-group-name /medimind/clinical-api --region $AWS_REGION
```

9. **Security Groups, Route Tables, IGW, Subnets & VPC:** Delete `sg-medimind-rds`, `sg-medimind-ec2`, and `sg-medimind-alb`; disassociate and delete custom route tables; detach and delete `medimind-igw`; delete the 6 subnets; and delete `medimind-vpc`.
10. **Local Docker Environment:** Stop and clean local containers and observability stacks:

```bash
docker compose down -v
docker compose -f monitoring/docker-compose.observability.yml down -v
```

{{% notice tip %}}
**Cost-Safety Reminder:** Unattached **Elastic IPs** (`$0.005/hr`), running **NAT Gateways** (`$0.059/hr` in `ap-southeast-1`), and **AWS Secrets Manager** secrets left in recovery without `--force-delete-without-recovery` continue incurring charges. Always verify `EC2 -> Elastic IPs`, `VPC -> NAT Gateways`, and `AWS Billing -> Bills` 24 hours after cleanup.
{{% /notice %}}
