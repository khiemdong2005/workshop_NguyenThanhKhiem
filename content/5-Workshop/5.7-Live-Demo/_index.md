---
report_key: "workshopChapters"
report_language: "en"
report_fields: {"shortTitle": "Live Product Proof", "customTitle": "5.7. Live Product Proof (Demo Link & Video)", "summary": "Consolidated live production evidence for MediMind Clinical AI running on AWS Multi-AZ (ap-southeast-1): live HTTPS endpoint via Amazon CloudFront + AWS WAF, end-to-end YouTube walkthrough video, public GitHub repository, and verified runtime screenshots.", "content": "MediMind Clinical AI is live at https://d2typ9pphzk4as.cloudfront.net with a complete end-to-end YouTube demo video at https://www.youtube.com/watch?v=kbFEEDeEY2I, public GitHub repository, and official 13-service AWS Pricing Calculator estimate.", "notes": "", "steps": [{"num": "5.7.1", "title": "Live Production Links & Official Verification Resources", "summary": "All live deployment endpoints, recorded demo video, source repository, and cost estimate are publicly accessible for direct mentor and panel verification:", "table": {"headers": ["Verification Artifact", "Direct Access Link"], "rows": [["Live HTTPS Application (CloudFront + AWS WAF)", "[https://d2typ9pphzk4as.cloudfront.net](https://d2typ9pphzk4as.cloudfront.net)"], ["End-to-End Live Demo Video (YouTube)", "[Watch MediMind Clinical AI Demo Video](https://www.youtube.com/watch?v=kbFEEDeEY2I)"], ["Deployment Source Repository (`main`)", "[github.com/MediMind-Clinical-AI/chatbot_medical](https://github.com/MediMind-Clinical-AI/chatbot_medical)"], ["AWS Cost Estimation (13 Services)", "[AWS Pricing Calculator ($228.76/month)](https://calculator.aws/#/estimate?id=ec26a26022ee93e0eb9785a0048f4dca71eb6fb3)"]]}}, {"num": "5.7.2", "title": "End-to-End Live Demo Video & AWS Multi-AZ Walkthrough (YouTube)", "summary": "This video demonstrates the full live user journey on `https://d2typ9pphzk4as.cloudfront.net` alongside live AWS Console verification across `ap-southeast-1` (Singapore) and the global edge tier (`us-east-1`).", "video": {"youtubeId": "kbFEEDeEY2I", "url": "https://www.youtube.com/watch?v=kbFEEDeEY2I", "title": "MediMind Clinical AI — Live Demo on AWS Multi-AZ"}, "bullets": ["**Authentication & Profile:** Google OAuth 2.0 sign-in, 6-digit Email OTP registration, first-login health onboarding, password change, and invalid-password rejection.", "**Clinical Triage & Hybrid RAG:** Floating chat syncing seamlessly to the Health Assistant tab, off-topic non-medical refusal, and urgent Red-Flag alert banner (*Double Guardrails*).", "**Prescription OCR & Nutrition:** Uploading a prescription image for Vision LLM extraction/reconciliation and medication reminders; generating single-dish and full meal-combo nutrition plans with cooking recipes.", "**Healthcare Facilities & Booking:** Locating clinics/hospitals on Google Maps, submitting pre-visit intake notes, booking appointments, and receiving automated confirmation emails.", "**AWS Multi-AZ Verification:** CloudFront HTTPS, AWS WAF SQL Injection blocking (`403 BLOCK`), 3-tier 6-subnet VPC, ALB `2/2 Healthy`, 2 Private EC2 ASG nodes, Dual-AZ EFS, Private RDS PostgreSQL, Secrets Manager, CloudWatch Alarms, and AWS Budgets."]}, {"num": "5.7.3", "title": "Live Runtime Screenshots (ALB 2/2 Healthy, CloudFront HTTPS & Clinical Triage)", "summary": "Quick visual proof captured directly from the live deployment confirming Multi-AZ load balancing (`2/2 Healthy`), CloudFront edge verification (`SGN50-P1`, `RAG ready`, `Circuit Breaker CLOSED`), and real-time clinical safety guardrails.", "images": [{"url": "static/images/5-Workshop/5.5-Operations/21-alb-2healthy.png", "caption": "Figure 21 (AWS Console) — Target Group medimind-tg reporting 2/2 Healthy across 2 Private EC2 nodes in ap-southeast-1a and ap-southeast-1b"}, {"url": "static/images/5-Workshop/5.5-Operations/22-live-health-cloudfront.jpg", "caption": "Figure 22 (Live HTTPS) — Verified /health ok, /ready ready (RAG & Circuit Breaker CLOSED), CSP/X-Frame-Options at CloudFront SGN50-P1"}, {"url": "static/images/5-Workshop/5.5-Operations/24-live-clinical-triage-redflag.jpg", "caption": "Figure 24 (Live App) — MediMind Clinical AI live HTTPS app triggering an immediate High-Risk Emergency Triage banner for acute chest pain"}], "note": "Detailed AWS WAF SQL Injection (`403 BLOCK`) testing, CloudWatch Alarms, and AWS Budgets verification are documented in Chapter **5.5**; the prepared post-defense teardown runbook is documented in Chapter **5.6**."}]}
report_index: 6
report_shared: {"code": "5.7", "url": "https://d2typ9pphzk4as.cloudfront.net"}
title: "Live Product Proof"
date: "2026-11-28"
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

# 5.7. Live Product Proof (Demo Link & Video)

Consolidated live production evidence for **MediMind Clinical AI** running on AWS Multi-AZ (`ap-southeast-1`): live HTTPS endpoint via Amazon CloudFront + AWS WAF, end-to-end YouTube walkthrough video, public GitHub repository, and verified runtime screenshots.

## 5.7.1 — Live Production Links & Official Verification Resources

| Verification Artifact | Direct Access Link |
| --- | --- |
| Live HTTPS Application (CloudFront + AWS WAF) | [https://d2typ9pphzk4as.cloudfront.net](https://d2typ9pphzk4as.cloudfront.net) |
| End-to-End Live Demo Video (YouTube) | [Watch MediMind Clinical AI Demo Video](https://www.youtube.com/watch?v=kbFEEDeEY2I) |
| Deployment Source Repository (`main`) | [github.com/MediMind-Clinical-AI/chatbot_medical](https://github.com/MediMind-Clinical-AI/chatbot_medical) |
| AWS Cost Estimation (13 Services) | [AWS Pricing Calculator ($228.76/month)](https://calculator.aws/#/estimate?id=ec26a26022ee93e0eb9785a0048f4dca71eb6fb3) |

## 5.7.2 — End-to-End Live Demo Video & AWS Multi-AZ Walkthrough (YouTube)

This video demonstrates the full live user journey on `https://d2typ9pphzk4as.cloudfront.net` alongside live AWS Console verification across `ap-southeast-1` (Singapore) and the global edge tier (`us-east-1`).

<div style="margin: 1rem 0 1.25rem; border: 1px solid #e2e8f0; border-radius: 10px; overflow: hidden; background: #fff;">
  <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; background: #0f172a;">
    <iframe src="https://www.youtube.com/embed/kbFEEDeEY2I" title="MediMind Clinical AI — Live Demo on AWS Multi-AZ" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0;" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
  </div>
  <div style="display: flex; justify-content: space-between; align-items: center; gap: 12px; padding: 10px 14px; background: #f8fafc; border-top: 1px solid #e2e8f0; flex-wrap: wrap;">
    <span style="font-size: 0.92rem; color: #334155;">MediMind Clinical AI — Live Demo on AWS Multi-AZ</span>
    <a href="https://www.youtube.com/watch?v=kbFEEDeEY2I" target="_blank" rel="noopener noreferrer" style="display: inline-block; padding: 6px 12px; background: #0f172a; color: #ffffff; border-radius: 6px; font-size: 0.85rem; font-weight: 600; text-decoration: none;">Open on YouTube ↗</a>
  </div>
</div>

- **Authentication & Profile:** Google OAuth 2.0 sign-in, 6-digit Email OTP registration, first-login health onboarding, password change, and invalid-password rejection.
- **Clinical Triage & Hybrid RAG:** Floating chat syncing seamlessly to the Health Assistant tab, off-topic non-medical refusal, and urgent Red-Flag alert banner (*Double Guardrails*).
- **Prescription OCR & Nutrition:** Uploading a prescription image for Vision LLM extraction/reconciliation and medication reminders; generating single-dish and full meal-combo nutrition plans with cooking recipes.
- **Healthcare Facilities & Booking:** Locating clinics/hospitals on Google Maps, submitting pre-visit intake notes, booking appointments, and receiving automated confirmation emails.
- **AWS Multi-AZ Verification:** CloudFront HTTPS, AWS WAF SQL Injection blocking (`403 BLOCK`), 3-tier 6-subnet VPC, ALB `2/2 Healthy`, 2 Private EC2 ASG nodes, Dual-AZ EFS, Private RDS PostgreSQL, Secrets Manager, CloudWatch Alarms, and AWS Budgets.

## 5.7.3 — Live Runtime Screenshots (ALB 2/2 Healthy, CloudFront HTTPS & Clinical Triage)

![Figure 21 (AWS Console) — Target Group medimind-tg reporting 2/2 Healthy across 2 Private EC2 nodes in ap-southeast-1a and ap-southeast-1b](/images/5-Workshop/5.5-Operations/21-alb-2healthy.png)
*Figure 21 (AWS Console) — Target Group medimind-tg reporting 2/2 Healthy across 2 Private EC2 nodes in ap-southeast-1a and ap-southeast-1b*

![Figure 22 (Live HTTPS) — Verified /health ok, /ready ready (RAG & Circuit Breaker CLOSED), CSP/X-Frame-Options at CloudFront SGN50-P1](/images/5-Workshop/5.5-Operations/22-live-health-cloudfront.jpg)
*Figure 22 (Live HTTPS) — Verified /health ok, /ready ready (RAG & Circuit Breaker CLOSED), CSP/X-Frame-Options at CloudFront SGN50-P1*

![Figure 24 (Live App) — MediMind Clinical AI live HTTPS app triggering an immediate High-Risk Emergency Triage banner for acute chest pain](/images/5-Workshop/5.5-Operations/24-live-clinical-triage-redflag.jpg)
*Figure 24 (Live App) — MediMind Clinical AI live HTTPS app triggering an immediate High-Risk Emergency Triage banner for acute chest pain*
