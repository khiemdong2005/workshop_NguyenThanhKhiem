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
- Study medical speech-to-text as a possible alternative to the current text input flow.
- Review layout, colors, and navigation to make the pages more consistent.

### Tasks carried out this week:

| Day | Task | Start date | Completion date | Reference material |
| --- | --- | --- | --- | --- |
| Monday | - Reviewed the page structure and UI elements built in Week 7.<br>- Adjusted the home and profile layouts, colors, and icons; checked how the interface changes after sign-in.<br>- Learned to separate demonstration data from the signed-in user's records. | 02/11/2026 | 02/11/2026 | Project |
| Tuesday | - Studied the frontend-to-backend flow when users upload a prescription or laboratory report image.<br>- Checked how the backend reads information, returns the required fields, and how the frontend displays them.<br>- Added checks for date of birth and gender and displayed age from the extracted data. | 03/11/2026 | 03/11/2026 | Project |
| Wednesday | - Built the initial information form and a small floating chat window.<br>- Studied how to preserve a conversation session when users move between screens.<br>- Corrected the handling of negated statements and compared the data sent by the frontend with the data stored by the backend. | 04/11/2026 | 04/11/2026 | Project |
| Thursday | - Studied how to organize user records by account.<br>- Connected processed document results with storage and the history list in the interface.<br>- Checked page reload and account switching to avoid displaying another user's data. | 05/11/2026 | 05/11/2026 | Project |
| Friday | - Reviewed the placement of messages, input fields, and buttons on the chat page.<br>- Adjusted spacing, contrast, and icons in light and dark themes.<br>- Compared the main chat page with the floating chat window to keep interaction consistent.<br>- Studied Amazon Transcribe Medical, including dictation versus clinician-patient conversation and speaker labels in a transcript. | 06/11/2026 | 06/11/2026 | Project; [AWS Transcribe Medical](https://docs.aws.amazon.com/transcribe/latest/dg/how-it-works-med.html); [Speaker diarization](https://docs.aws.amazon.com/transcribe/latest/dg/conversation-diarization-med.html) |
| Saturday | - Continued improving the medical facility search interface and map.<br>- Checked the events triggered when a user selects a facility, opens the map, or switches tabs.<br>- Fixed misplaced elements and a layout issue that made one tab affect another. | 07/11/2026 | 07/11/2026 | Project |

### Week 8 results:

- Better understood the roles of frontend and backend: the frontend receives actions, sends data, and displays results; the backend validates, processes, and stores information.
- Practiced connecting a feature from the interface to backend processing, particularly image upload and display of extracted data.
- Learned to track sign-in state, consultation sessions, and account-specific data during navigation and reloads.
- Studied how to organize records and history so information belongs to the correct account.
- Improved the interface by refining chat layout, text colors, icons, tab navigation, and the map.
- Learned that data needs checking on both sides: image extraction may miss fields, and a user's statement can be misunderstood if negation is handled incorrectly.
- Learned that Amazon Transcribe Medical can turn medical speech into text and distinguish speakers. Since its documentation focuses on US English, this was research into a possible voice-input approach, not an integrated feature.
