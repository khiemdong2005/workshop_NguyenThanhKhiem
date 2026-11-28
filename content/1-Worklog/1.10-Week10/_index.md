---
title: "Week 10 Worklog"
date: 2026-11-16
weight: 10
chapter: false
pre: "<b>1.10.</b> "
---

### Week 10 Objectives:

- Switch chatbot text tasks from Gemini to Groq and explore OpenRouter and Amazon Bedrock.
- Rework prescription OCR so the vision model can process both the full prescription and a readable crop.
- Integrate registration OTP delivery through Gmail SMTP and SpeedSMS.
- Complete the healthcare facilities map and carry the pre-visit summary into appointment booking.
- Refine the meal recommendation filter and improve offline testing in CI.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Synced the OCR recapture screen and added date-of-birth and age extraction to the digitized prescription data.</li><li>Reviewed offline tests and aligned the FastAPI and Starlette versions in CI with the dependency lockfile.</li><li>Read the Amazon Bedrock Runtime documentation and compared three operations. Converse handles chat messages, ConverseStream streams responses, and InvokeModel accepts model-specific input formats.</li></ul> | 16/11/2026 | 16/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical)<br>[Amazon Bedrock Runtime](https://docs.aws.amazon.com/bedrock/latest/userguide/conversation-inference.html) |
| 3 | <ul><li>Integrated the team's registration OTP changes, including the account-status fix, Gmail SMTP code delivery, and the switch to SpeedSMS for SMS.</li><li>Synced the team's OpenRouter model configuration and the addition of pytest-cov to the test dependencies.</li><li>Adjusted the login interface and updated the rule that prevents duplicate ingredients in side dishes.</li><li>Reviewed the Google OAuth 2.0 redirect and callback flow, along with how the backend sends OTP codes through Gmail SMTP.</li></ul> | 17/11/2026 | 17/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 4 | <ul><li>Reworked OCR image preparation to send both the full prescription and a readable crop to the vision model. The full image retains the layout, while the crop helps the model read medication names and strengths.</li><li>Reviewed Bedrock pricing and estimated chatbot tokens (including chat history and retrieved RAG passages) separately from prescription image inputs.</li></ul> | 18/11/2026 | 18/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical)<br>[Amazon Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/) |
| 5 | <ul><li>Addressed a medication-name OCR error and added cleanup for temporary image crops after processing.</li><li>Adjusted three-dish meal sets, separated standalone savory dishes from desserts, and refined the nutrition filters.</li><li>Added a default model configuration for the nutrition workflow in offline CI tests.</li></ul> | 19/11/2026 | 19/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 6 | <ul><li>Switched chatbot text tasks from Gemini to Groq in the integrated build. Kept a separate vision model configuration for prescription image processing.</li><li>Synced the team's refactor that moved Flask routes from app.py into five modules while preserving existing URLs and endpoint names.</li><li>Integrated booking into the healthcare facilities page, moved <strong>My Appointments</strong> into that view, added accessible form labels, and carried the pre-visit summary into the booking step.</li><li>Estimated token usage for 1,000 chatbot calls. Assuming 1,200 input and 300 output tokens per call, the totals are 1.2 million input and 300,000 output tokens.</li><li>Reviewed model selection criteria for the Groq API, including supported input types, rate limits, and configurations for text chat and image OCR.</li></ul> | 20/11/2026 | 20/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical)<br>[Amazon Bedrock Pricing](https://aws.amazon.com/bedrock/pricing/) |
| 7 | <ul><li>Finished the healthcare facilities map configuration by updating the Content Security Policy (CSP) to allow ArcGIS resources and map tiles from the CDN.</li><li>Added a fast response mode for informational questions.</li><li>Attended AWS Student Community Day and took notes on network segmentation, connectivity checks, and layered security.</li></ul> | 21/11/2026 | 21/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical)<br>[Event 6 report](../../4-eventparticipated/4.6-event6/) |

### Week 10 Achievements:

- The chatbot uses Groq for text tasks, and OCR has a separate vision model configuration. Reviewed OpenRouter and Bedrock Runtime operations and prepared a sample token estimate.
- The OCR workflow sends the full prescription with a readable crop, extracts date of birth and age, addresses a medication-name recognition error, and removes temporary crops.
- Integrated registration OTP delivery through Gmail SMTP and SpeedSMS, including updated account-status handling during registration.
- Completed the healthcare facilities map CSP configuration for ArcGIS and the CDN. Booking carries the pre-visit summary and includes My Appointments and accessible form labels.
- Updated three-dish meal assembly, nutrition filtering rules, and the fallback configuration for offline tests.
- Synced the team's five Flask route modules and pytest-cov dependency. Aligned FastAPI and Starlette in CI with the lockfile.
- Recorded network segmentation and connectivity checks after AWS Student Community Day. [Event 6 report](../../4-eventparticipated/4.6-event6/)
