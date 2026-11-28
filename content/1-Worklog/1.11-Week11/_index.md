---
title: "Week 11 Worklog"
date: 2026-11-23
weight: 11
chapter: false
pre: "<b>1.11.</b> "
---

### Week 11 Objectives:

- Fix interface issues and refine prescription reading, verification, and editing.
- Complete appointment and medication reminders and export pre-visit data in FHIR R4 format.
- Complete Nutrition recommendations using the BMR/TDEE questionnaire, allergy information, and a fixed recipe catalog.
- Deploy MediMind to AWS and verify HTTPS access.
- Finalize the Proposal, Workshop guide, and AWS architecture diagram, review the estimate, and record a demo video.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Tested the web app in the browser and fixed issues with images, form autofill, and requests from signed-out users.</li><li>Standardized medication names from Circular 20/2022/TT-BYT for checking OCR results. Tested the prescription workflow with the local catalog and API fallback.</li><li>Finished the booking and medication reminder updates. Restored reviewed medication schedules, hid expired appointments, and added FHIR R4 export for confirmed pre-visit data.</li></ul> | 23/11/2026 | 23/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/a950e1fffdf60f4d12fcef0ae416423ff5560ddb) |
| 3 | <ul><li>Tested OCR with prescription images that used different layouts and reviewed cases where medication names were misread.</li><li>Fixed tab navigation and changed how the app recommends meals. The app filters the catalog by rule, then the model selects from the remaining dishes.</li></ul> | 24/11/2026 | 24/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 4 | <ul><li>Added an edit button to the OCR results screen so users can correct extracted information before saving. Reviewed the API configuration for chat, OCR, and Nutrition.</li><li>Completed the Mifflin–St Jeor BMR/TDEE questionnaire and added allergy information. Separated meal sets, individual dishes, and drinks, standardized serving calories, and updated recipe photos and nutrition data.</li><li>Added a way to revisit the survey and kept the active tab, open recipe, and survey inputs when the page reloads. Documented the workflow in draw.io and rechecked the PR Quality Gate.</li></ul> | 25/11/2026 | 25/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 5 | <ul><li>Compared the existing catalog with around 2,500 recipes from Món Ngon Mỗi Ngày. Checked for overlap and exported an XLSX comparison.</li><li>Reviewed the Proposal and Workshop guide against the working application. Updated feature descriptions, recipe counts, and illustrations.</li></ul> | 26/11/2026 | 26/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 6 | <ul><li>Deployed MediMind to AWS. Built the Docker image with CodeBuild, stored it in ECR, and ran the container with Uvicorn on EC2. Checked the ALB target status and opened the app over HTTPS.</li><li>Reviewed service settings in the AWS Console to prepare an AWS Pricing Calculator estimate. Added 33 AWS Console and AWS CLI screenshots illustrating the deployment steps in the Workshop guide.</li><li>Checked the deployment diagram against the AWS configuration, including the image source in ECR, IAM role access to Secrets Manager, and shared storage in EFS.</li></ul> | 27/11/2026 | 27/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/blob/main/Dockerfile#L54) |
| 7 | <ul><li>Finalized the Proposal, Workshop guide, and AWS architecture diagram. Reviewed the deployment steps and screenshots. In the estimate review, identified Single-AZ RDS as the Workshop configuration and Multi-AZ RDS as an option in the target architecture.</li><li>Recorded a demo video on the AWS deployment to show MediMind's main workflows.</li></ul> | 28/11/2026 | 28/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |

### Week 11 Achievements:

- Completed appointment booking, appointment reminders, and medication reminders. Confirmed pre-visit data can be exported in FHIR R4 format.
- Standardized the medication catalog used to check OCR results. Users can correct extracted information on the results screen before saving.
- Completed meal recommendations based on BMR/TDEE and allergy inputs. Users can view meal sets, individual dishes, and drinks separately and return to the same tab after reloading.
- Deployed MediMind to AWS and verified HTTPS access.
- Finalized the Proposal, Workshop guide, and architecture diagram. Checked the AWS estimate against the deployment configuration and recorded a video showing the main application workflows.
