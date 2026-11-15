---
title: "Week 8 Worklog"
date: 2026-11-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 objectives:

- Continue developing the frontend and backend from the foundation prepared in Week 7.
- Learn how a user action moves from the interface to the backend and how the result returns to the frontend.
- Practice managing UI state, consultation sessions, and data associated with user accounts.
- Review layout, colors, and navigation to make the pages more consistent.

### Tasks carried out this week:

| Day | Task | Start date | Completion date | Reference material |
| --- | --- | --- | --- | --- |
| Monday | - Reviewed the page structure and UI elements built in Week 7.<br>- Adjusted the home and profile layouts, colors, and icons; checked how the interface changes after sign-in.<br>- Learned to separate demonstration data from the signed-in user's records. | 02/11/2026 | 02/11/2026 | [HTML interface](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html); [JavaScript](https://github.com/khiemdong2005/chatbot_medical/blob/main/static/js/app.js) |
| Tuesday | - Studied the frontend-to-backend flow when users upload a prescription or laboratory report image.<br>- Checked how the backend reads information, returns the required fields, and how the frontend displays them.<br>- Added checks for date of birth and gender and displayed age from the extracted data. | 03/11/2026 | 03/11/2026 | [Document processing](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/pipeline_orchestrator.py); [OCR](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/ocr_parallel_service.py) |
| Wednesday | - Built the initial information form and a small floating chat window.<br>- Studied how to preserve a conversation session when users move between screens.<br>- Corrected the handling of negated statements and compared the data sent by the frontend with the data stored by the backend. | 04/11/2026 | 04/11/2026 | [Intake session service](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/intake_service.py); [JavaScript](https://github.com/khiemdong2005/chatbot_medical/blob/main/static/js/app.js) |
| Thursday | - Studied how to organize user records by account.<br>- Connected processed document results with storage and the history list in the interface.<br>- Checked page reload and account switching to avoid displaying another user's data. | 05/11/2026 | 05/11/2026 | [Backend source code](https://github.com/khiemdong2005/chatbot_medical/blob/main/app.py); [Prescription processing](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/prescription_service.py) |
| Friday | - Reviewed the placement of messages, input fields, and buttons on the chat page.<br>- Adjusted spacing, contrast, and icons in light and dark themes.<br>- Compared the main chat page with the floating chat window to keep interaction consistent. | 06/11/2026 | 06/11/2026 | [HTML interface](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html); [JavaScript](https://github.com/khiemdong2005/chatbot_medical/blob/main/static/js/app.js) |
| Saturday | - Continued improving the medical facility search interface and map.<br>- Checked the events triggered when a user selects a facility, opens the map, or switches tabs.<br>- Fixed misplaced elements and a layout issue that made one tab affect another. | 07/11/2026 | 07/11/2026 | [HTML interface](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html); [JavaScript](https://github.com/khiemdong2005/chatbot_medical/blob/main/static/js/app.js) |
| Sunday | - Reviewed the consultation session data from the initial form to the summary screen.<br>- Adjusted the interface and backend so a summary is saved only after user confirmation.<br>- Fixed the verification email template and checked conversation history again. | 08/11/2026 | 08/11/2026 | [Chat workflow notes](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md); [Session handling](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/intake_service.py) |

### Week 8 results:

- Better understood the roles of frontend and backend: the frontend receives actions, sends data, and displays results; the backend validates, processes, and stores information.
- Practiced connecting a feature from the interface to backend processing, particularly image upload and display of extracted data.
- Learned to track sign-in state, consultation sessions, and account-specific data during navigation and reloads.
- Studied how to organize records and history so information belongs to the correct account.
- Improved the interface by refining chat layout, text colors, icons, tab navigation, and the map.
- Learned that data needs checking on both sides: image extraction may miss fields, and a user's statement can be misunderstood if negation is handled incorrectly.
- Completed the user confirmation step before saving a consultation summary.
