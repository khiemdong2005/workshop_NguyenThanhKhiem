---
title: "Week 8 Worklog"
date: 2026-11-02
weight: 8
chapter: false
pre: "<b>1.8.</b> "
---

### Week 8 Objectives:

- Continue developing the frontend and backend from the foundation prepared in Week 7.
- Learn how a user action moves from the interface to the backend and how the result returns to the frontend.
- Practice managing UI state, consultation sessions, and data associated with user accounts.
- Study medical speech-to-text as a possible alternative to the current text input flow.
- Review layout, colors, and navigation to make the pages more consistent.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Updated the HTML and Tailwind CSS for a lighter theme, replaced icons, and rearranged the patient record screen for signed-in users.</li></ul> | 02/11/2026 | 02/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/d97eaf3e6ac6e50c0ea84a6aecea89561bba62e5) |
| 3 | <ul><li>Brought the new design into the website and checked how the chatbot looks up documents before answering. Outlined a pre-visit question and summary flow.</li><li>Connected the Python pipeline for reading prescription and lab report images to the JavaScript interface. Checked date of birth and sex and displayed age from the extracted data. Removed the health insurance ID field from the results screen.</li><li>Noted what to change in chat: shorter replies, history that is easier to reopen, and a small chat window that stays available when switching tabs.</li></ul> | 03/11/2026 | 03/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/4b2a5c4ff90749b91d639b8e2fb832dec6a09bb3) |
| 4 | <ul><li>Fixed a JavaScript issue that blocked tab switching. Updated the home page, patient records, and mini chat to use a consistent style.</li><li>Simplified the profile page by removing the national ID and health insurance fields from this form. Added controls to show or hide the phone number and email address.</li><li>Rearranged the healthcare facilities page into two columns and adjusted icons that were hard to see.</li><li>Built the initial intake flow and added tests with pytest. Fixed how denied symptoms were recorded, saved consultation state, and separated sample records from account data. Noted a case where the wrong summary opened for follow-up.</li><li>Updated the chatbot's document retrieval index.</li></ul> | 04/11/2026 | 04/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/d991d39976a2a53e86887b4158f0ba9e9007f4aa) |
| 5 | <ul><li>Used Flask, SQLAlchemy, and SQLite to save prescription and lab report results to the correct user record. Added a history list and summary so users could reopen saved information.</li><li>Reorganized the workshop report folder and used Hugo to check the Vietnamese and English versions.</li></ul> | 05/11/2026 | 05/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/57609455992883a7f00d25d97c4e8979193abdb7) |
| 6 | <ul><li>Updated the chatbot page to match the blue reference design and improved text and button contrast. Removed the redundant 115 button from the interface and replaced icons that did not match the interface.</li><li>Read the Amazon Transcribe Medical documentation to see how it labels speakers in medical conversations.</li></ul> | 06/11/2026 | 06/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/44ddf49a46f3d13e2c06d4de5e3ef69eac847f62)<br>[AWS Transcribe Medical](https://docs.aws.amazon.com/transcribe/latest/dg/how-it-works-med.html)<br>[Speaker diarization](https://docs.aws.amazon.com/transcribe/latest/dg/conversation-diarization-med.html) |
| 7 | <ul><li>Reviewed intake session access, signed-out behavior, and mobile layout. Added account-level access checks and related tests.</li><li>Made the Leaflet map with OpenStreetMap tiles visible by default on the healthcare facilities page. Updated the map button and fixed hard-to-read banner text.</li><li>Fixed an HTML layout issue that caused the home page's Explore cards to appear in other tabs.</li><li>Updated the ChromaDB index so the chatbot could look up documents.</li></ul> | 07/11/2026 | 07/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/3f8fdf77be4d18171e310d8650a9d687fea09b26) |

### Week 8 Achievements:

- Completed the read-and-save flow for the current version. Users can upload a prescription or lab report image, see the extracted results, and reopen them in their account history.
- Updated the home, profile, and chat screens with the lighter design.
- Fixed how chat records denied symptoms and keeps an intake session when users switch screens.
- Added access checks for account records and intake sessions.
- Fixed home page cards appearing in other tabs and adjusted how the healthcare facilities map opens.
- Learned how Amazon Transcribe Medical distinguishes speakers. Voice input remained a research topic.
