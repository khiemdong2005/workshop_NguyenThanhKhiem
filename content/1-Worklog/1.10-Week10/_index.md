---
title: "Week 10 Worklog"
date: 2026-11-16
weight: 10
chapter: false
pre: "<b>1.10.</b>"
---

**Period** — November 16–21, 2026.

## Objectives

Building on Week 9, this week focused on OCR, meal recommendations, and the healthcare facility map, alongside OTP fixes and pre-visit summaries in the booking workflow.

## Daily work

| Day | Work completed | Start date | Completion date | References |
| --- | --- | --- | --- | --- |
| Monday | - **Model invocation for chat.** Reviewed `Converse` for structured `messages`, `ConverseStream` for incremental responses, and `InvokeModel` for model-specific input formats. Integration checks include the `modelId`, AWS Region, IAM permissions, and supported input modalities. | 16/11/2026 | 16/11/2026 | [Bedrock Runtime API](https://docs.aws.amazon.com/bedrock/latest/userguide/conversation-inference.html) |
| Tuesday | - Fixed an account-status error in OTP registration, updated Gmail SMTP code delivery and switched SMS configuration to SpeedSMS.<br>- Added `pytest-cov` to the test dependencies.<br>- Added OpenRouter models to the AI provider configuration (`015ffc0`). | 17/11/2026 | 17/11/2026 | `8b4fd5a`, `015ffc0`, `a76d732` |
| Wednesday | - Updated the OCR flow to send both the full prescription and a readable crop to the vision model.<br>- The full image preserves layout context, while the crop supports reading drug names and strengths.<br>- **Inference pricing.** For token-priced text models, look up separate input and output rates for the selected model, Region, and usage mode. RAG requests may include conversation history and retrieved passages in the input. For OCR, check how the chosen model prices image inputs. | 18/11/2026 | 18/11/2026 | `d239a92` · [Amazon Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/) |
| Thursday | - Adjusted three-dish meal sets, separated standalone savory dishes from desserts, and refined gout and fat filters.<br>- Fixed a Banitase OCR case and added cleanup for temporary crops.<br>- Added a default model for the nutrition flow as a fallback configuration in CI (`fd6b991`). | 19/11/2026 | 19/11/2026 | `8a4cd9d`, `03bd37a` |
| Friday | - Split routes out of `app.py` into five feature modules while preserving existing URLs and endpoint names.<br>- Added Groq for text tasks and kept a separate vision configuration for OCR.<br>- Moved My Appointments into the healthcare facilities view and added accessible labels to the booking form fields (`14abf71`, `731e869`).<br>- **Project estimation.** For example, 1,000 calls averaging 1,200 input tokens and 300 output tokens would use 1.2 million input tokens and 300,000 output tokens. Multiply each usage figure by its corresponding rate and sum the two subtotals. If the design uses Knowledge Bases or Guardrails, estimate those features separately according to their pricing. These usage figures are illustrative. | 20/11/2026 | 20/11/2026 | `61bdac6`, `00c06b6`, `4b09a1b` · [Amazon Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/) |
| Saturday | - Updated the Content Security Policy to allow map resources from ArcGIS and the map tile CDN.<br>- Attended AWS Student Community Day and noted the main points on layered network security. | 21/11/2026 | 21/11/2026 | `3a5f359` · [Event 6 report](../../4-eventparticipated/4.6-event6/) |

## Week 10 outcomes

- **Amazon Bedrock API and pricing.** Distinguished structured chat with `Converse`, streamed responses with `ConverseStream`, and model-specific invocation with `InvokeModel`. Identified the model ID, Region, IAM permissions, and supported inputs as integration checks. Worked through an illustrative estimate for 1,000 calls using separate input and output token rates. This was an API and pricing research exercise.
- **OTP and testing.** Fixed the account-status error during OTP registration, updated Gmail SMTP delivery and SpeedSMS configuration, and added `pytest-cov` to the test dependencies.
- **Prescription OCR.** Updated vision requests to include both a full image for layout context and a readable crop for drug names and strengths. Corrected the Banitase OCR case and added cleanup for temporary crops.
- **Meal recommendations.** Adjusted three-dish meal sets, separated standalone savory dishes from desserts, and refined gout and fat filters. Added a default model configuration for the nutrition flow in CI.
- **Backend and AI configuration.** Split routes out of `app.py` into five feature modules while preserving existing URLs and endpoint names. Added Groq for text tasks and kept a separate vision configuration for image OCR.
- **Healthcare facilities and booking.** Moved My Appointments into the facilities view, labeled booking fields for accessibility, and updated the Content Security Policy to allow resources from ArcGIS and the map tile CDN.
- **AWS Student Community Day.** Recorded lessons on network segmentation, limiting traffic to required connections, and checking connectivity after configuration changes. [Event 6 report](../../4-eventparticipated/4.6-event6/)
