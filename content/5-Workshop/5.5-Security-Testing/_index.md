---
title: "Security, Quality Gates & Observability"
date: 2026-11-26
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Application Security Hardening

Beyond perimeter defenses (**AWS WAF**, **CloudFront**, and **3-Tier VPC isolation**), MediMind enforces defense-in-depth at the application layer:

| Security Control | Implementation File | Enforced Policy & Limits |
| :--- | :--- | :--- |
| **Upload & Magic-Byte Validation** | `core/storage_service.py` | Allows only `jpg`, `jpeg`, `png`, `pdf`, `docx`, `doc`; max `10 MB` file (`5 MB` base64); validates binary file headers (Magic Bytes) and prevents path traversal (`is_safe_path`). |
| **Anti-Decompression & Zip Bomb** | `core/storage_service.py` | Caps images at $\le 25\text{ MP}$ and `8000px` dimensions; PDFs at $\le 30\text{ pages}$; DOCX archives at $\le 50\text{ MB}$ uncompressed, $\le 500$ entries, and $< 50\text{x}$ compression ratio. |
| **CSRF & Rate Limiting** | `core/csrf_protection.py`, `core/rate_limit_service.py` | Validates CSRF tokens on state-changing requests and enforces per-IP rate limits respecting ALB proxy headers. |
| **RBAC & PII Log Redaction** | `core/models.py`, `core/logging_redaction.py` | Enforces `owner_id` checks across all documents/consultations (preventing IDOR) and masks phone numbers, emails, and tokens before logs reach CloudWatch. |

#### Fault Tolerance & AI Circuit Breaker (`core/circuit_breaker.py`)

To prevent cascading failures when external LLM providers (**Groq API Dual-Key** / **Gemini** fallback) experience rate limits or downtime, `core/circuit_breaker.py` wraps AI calls in a thread-safe 3-state state machine (`failure_threshold=5`, `cooldown_seconds=30.0`):

{{< mermaid >}}
graph LR
    CLOSED["CLOSED (Normal AI Inference)"] -->|"5 consecutive transient errors"| OPEN["OPEN (Fail-Fast 0ms -> Fallback Engine)"]
    OPEN -->|"After 30s cooldown"| HALF["HALF_OPEN (1 Probe Request)"]
    HALF -->|"Probe succeeds"| CLOSED
    HALF -->|"Probe fails"| OPEN
{{< /mermaid >}}

{{% notice info %}}
**Clinical Safety Guarantee:** The **Emergency Pre-check** (`core/triage.py`) executes deterministically *before* the Circuit Breaker. Life-threatening Red Flag emergencies (`115`) always respond immediately even when external AI providers are in `OPEN` state.
{{% /notice %}}

#### Automated Testing & Release Quality Gates

Run the full automated test suite (**95 test files** under `tests/test_*.py`) and verify compliance against the SHA-256 frozen thresholds in `evaluation/quality_gates.json`:

```bash
pytest -q
```

**Expected Output:** All 95 test files execute cleanly with `0 failed` (Exit Code `0`).

> **[Screenshot 20: `pytest -q` Passing All 95 Automated Test Files]** — `static/images/5-Workshop/5.5-Security-Testing/20-pytest-pass.png`

| Evaluation Category | Metric (`evaluation/quality_gates.json`) | Required Threshold |
| :--- | :--- | :---: |
| **Clinical Safety** | `emergency_recall_min` | **100%** (`1.0`) |
| **Clinical Safety** | `negation_accuracy_pct_min` | **100.0%** |
| **Clinical Safety** | `unsafe_advice_rate_pct_max` | **0.0%** |
| **Clinical Safety** | `false_reassurance_rate_pct_max` | **0.0%** |
| **Clinical Safety** | `visual_hallucination_rate_pct_max` | **0.0%** |
| **Clinical Safety** | `fallback_safety_rate_pct_min` & `guardrail_success_rate_pct_min` | **100.0%** |
| **RAG Retrieval** | `holdout_recall_at_5_min` | **$\ge$ 85%** |
| **RAG Retrieval** | `candidate_recall_at_20_min` | **$\ge$ 90%** |
| **RAG Retrieval** | `expansion_recall_at_5_min` (Cross-Language) | **$\ge$ 91%** |
| **RAG Retrieval** | `expansion_candidate_recall_at_20_min` | **$\ge$ 95%** |

#### Observability, Prometheus/Grafana & AWS Budgets

1. **Local & VM Observability Stack (`monitoring/docker-compose.observability.yml`):** Scrape `/metrics` from the application (`PORT=8000`) into **Prometheus (`:9090`)** and **Grafana (`:3000`)**, alongside the built-in `/system` health dashboard:

```bash
docker compose -f monitoring/docker-compose.observability.yml up -d
```

2. **SRE & SIEM Alert Rules (`monitoring/alert_rules.yml`):**
   - `HighHttpErrorRate` (5xx error rate `> 5%` over 1m)
   - `HighRequestLatency` (P95 latency `> 2.0s` over 1m)
   - `EmergencyTriageSpike` (surge in emergency red-flag triage events)
   - `HighMemoryLoad` (`medimind_system_memory_load_percent > 90%`)
   - `SecurityAttackSpike` (brute-force/fuzzing/malicious upload spike `> 5` events/min)
3. **AWS CloudWatch & AWS Budgets:** Inspect PII-redacted application logs in `/medimind/clinical-api`, check Metrics/Alarms, and configure an **AWS Budgets** billing alarm at **$20.00/month** for the Dev/PoC environment:

```bash
export AWS_REGION=ap-southeast-1
export ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)

# 1. Tail application logs (verify phone/email/API keys are redacted)
aws logs tail /medimind/clinical-api --since 30m --region $AWS_REGION

# 2. Check CloudWatch Metric Alarms status
aws cloudwatch describe-alarms --region $AWS_REGION --query 'MetricAlarms[*].[AlarmName,StateValue]' --output table

# 3. Verify AWS Budgets 20 USD threshold
aws budgets describe-budgets --account-id $ACCOUNT_ID --query 'Budgets[*].[BudgetName,BudgetLimit.Amount,CalculatedSpend.ActualSpend.Amount]' --output table
```

**Expected Output:**

```text
# aws logs tail (PII redacted)
2026-11-26T12:20:01 INFO request completed path=/api/chat phone=[REDACTED] status=200

# aws cloudwatch describe-alarms & budgets
-----------------------------------------------
|                DescribeAlarms               |
+------------------------------------+--------+
|  medimind-ec2-high-cpu             |  OK    |
+------------------------------------+--------+
```

> **[Screenshot 21: CloudWatch Logs `/medimind/clinical-api` Showing PII Redaction (`[REDACTED]`) & CloudWatch Alarm / AWS Budgets `OK`]** — `static/images/5-Workshop/5.5-Security-Testing/21-cloudwatch-budgets.png`
