---
title: "Workshop"
date: 2026-11-26
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Building & Deploying MediMind Clinical AI on AWS

#### Overview

**MediMind Clinical AI** is an end-to-end multimodal clinical assistant, prescription/lab-result cross-verification, medication reminder, and personalized clinical nutrition platform designed for patients and physicians in Vietnam. In this hands-on workshop, you will package the Python/Docker application (`app.py` and `core/main_fastapi.py`), provision a **HIPAA-aligned AWS 3-Tier VPC (`10.0.0.0/16`)** infrastructure in **`ap-southeast-1` (Singapore)**, and deploy a production-ready workload featuring **Hybrid RAG (BM25 + ChromaDB + Cross-Encoder Reranker)**, **Double Guardrails**, and a **Multimodal OCR Verification Pipeline**.

{{% notice info %}}
**Key Workshop Scope & Outcomes**
- **Clinical Safety:** **Double Guardrails** (`core/triage.py`) handle unaccented Vietnamese and negation phrases, trigger Emergency 115 guidance on red flags, and block unauthorized antibiotic prescribing, covered by **95 automated `pytest` test files**.
- **Grounded Medical Knowledge:** Hybrid RAG indexed over **364 standardized medical documents** (*Vietnam Ministry of Health, kcb.vn, MedlinePlus NIH*), **4,962 live Vietnamese recipes** (**2,462 ViFoodRec** + **2,500 Mon Ngon Moi Ngay**, plus **34 curated options**) with Fail-Closed Allergy Filtering and **BMR/TDEE** surveys, and **2,144 healthcare facilities** (1,505 in HCMC and 639 in Hanoi).
- **Cost Efficiency:** **~16.86 USD/month** (~202.32 USD/year) in Dev/PoC Workshop mode (Single-AZ with AWS Free Tier + Groq Dual-Key API), and **~220.95 – 233.45 USD/month** (**~0.0088 – 0.0093 USD per consultation session**) in Multi-AZ Production at 10,000-user scale.
{{% /notice %}}

#### Workshop Learning Objectives

By completing this workshop, you will learn how to:
1. Architect a **3-Tier Isolated VPC** (`Public Subnet`, `Private App Subnet`, `Private Database Subnet`) with chained Security Groups and zero public exposure for compute and database tiers.
2. Provision **Amazon RDS for PostgreSQL**, **Amazon S3** with Lifecycle policies, and **AWS Secrets Manager** for least-privilege runtime secret injection via an **EC2 IAM Role**.
3. Build a hardened non-root Docker image (`python:3.11-slim`), push it to **Amazon ECR**, attach an encrypted **Amazon EBS (`gp3`)** volume for persistent **ChromaDB** vector storage, and ingest 364 medical documents.
4. Expose the application securely through **Amazon Route 53**, **AWS WAF**, **Amazon CloudFront**, **AWS Certificate Manager (TLS 1.3)**, and an **Application Load Balancer (ALB)**.
5. Validate end-to-end clinical triage, negation handling, parallel OCR reconciliation, nutrition filtering (BMR/TDEE + ViFoodRec/Mon Ngon Moi Ngay), Circuit Breaker resilience, and **Prometheus/Grafana + CloudWatch** observability, then cleanly tear down all AWS resources.

#### Content

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Provision AWS 3-Tier Infrastructure](5.3-AWS-Infrastructure/)
4. [Containerize & Deploy MediMind AI](5.4-Deploy-MediMind/)
5. [Security, Quality Gates & Observability](5.5-Security-Testing/)
6. [Clean up](5.6-Cleanup/)
