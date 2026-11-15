---
title: "Week 8 Worklog"
date: 2026-11-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 objectives:

- Continue improving the interface and features prepared in Week 7.
- Learn how to collect symptom information, keep conversations by session, and show the information back to users.
- Practice reading prescriptions and laboratory results from images and adding the extracted information to user records.
- Review the chat, profile, and medical facility pages so they are easier to use.

### Tasks carried out this week:

| Day | Task | Start date | Completion date | Reference material |
| --- | --- | --- | --- | --- |
| Monday | - Reviewed the interface built in Week 7 and listed the parts that still needed work.<br>- Adjusted colors, icons, and the record view for signed-in users.<br>- Learned to separate the current user's information from sample data shown in the interface. | 02/11/2026 | 02/11/2026 | [Project interface](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html) |
| Tuesday | - Studied the steps involved in handling a prescription or lab-report image: receiving the image, reading its text, and displaying relevant fields.<br>- Practiced checking date of birth and gender and calculating age from the extracted information.<br>- Checked missing or misread fields to avoid showing incorrect details in the record. | 03/11/2026 | 03/11/2026 | [OCR workflow](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/ocr_parallel_service.py); [prescription processing](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/prescription_service.py) |
| Wednesday | - Continued work on the initial symptom questions and a small floating chat window.<br>- Learned how to preserve each conversation session and corrected cases where “no symptom” was recorded as a present symptom.<br>- Adjusted the home, profile, and medical facility layouts and checked navigation between tabs. | 04/11/2026 | 04/11/2026 | [Intake service](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/intake_service.py); [chatbot notes](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md) |
| Thursday | - Practiced saving processed prescriptions and lab results in user records.<br>- Added a history list so users can review earlier documents.<br>- Checked that records remain linked to the correct account after sign-in, page reload, or session changes. | 05/11/2026 | 05/11/2026 | [Application code](https://github.com/khiemdong2005/chatbot_medical/blob/main/app.py) |
| Friday | - Reviewed the chat page and the placement of questions and answers.<br>- Adjusted text colors, spacing, and icons for readability in light and dark themes.<br>- Compared the main chat page with the floating chat window. | 06/11/2026 | 06/11/2026 | [Interface](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html); [JavaScript](https://github.com/khiemdong2005/chatbot_medical/blob/main/static/js/app.js) |
| Saturday | - Improved medical facility search and the map view.<br>- Refined the search bar, facility cards, and map button for clearer interaction.<br>- Checked a layout problem that caused content from different tabs to interfere with one another. | 07/11/2026 | 07/11/2026 | [Project interface](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html) |
| Sunday | - Reviewed the user flow from symptom intake to the consultation summary.<br>- Required users to review and confirm a summary before saving it.<br>- Fixed the verification email template and issues when reviewing chat history. | 08/11/2026 | 08/11/2026 | [Chatbot notes](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md) |

### Week 8 results:

- Better understood how to organize a user flow from entering symptoms to reviewing the conversation.
- Practiced extracting information from prescriptions and lab reports and learned to check fields before adding them to a record.
- Learned how to save documents by account and show a history for later review.
- Recognized the importance of recording negation correctly: omitting “no” can change the meaning of a symptom statement.
- Improved the chat, record, and medical facility interfaces so they are more consistent than in the previous week.
- Learned more about user control of personal information: a consultation summary should be reviewed and confirmed before it is saved.
