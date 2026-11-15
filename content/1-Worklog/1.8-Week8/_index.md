---
title: "Week 8 Worklog"
date: 2026-11-02
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 objectives:

- Build the first functional workflows for MediMind AI on the UI and backend foundation prepared in Week 7.
- Study how to collect symptom information across consultation sessions, preserve conversation context, and distinguish user statements from system inferences.
- Practice extracting information from prescriptions and laboratory reports, then storing and displaying the results in the correct user's record.
- Improve usability across chat, profile, and medical facility search pages in both light and dark themes.
- Review data safety concerns, including record access, user consent before saving a consultation summary, and changes of session or account.

### Work completed this week:

| Day | Work | Start date | Completion date | Reference material |
| --- | --- | --- | --- | --- |
| Monday | - Reviewed the UI structure prepared in Week 7 and aligned the light theme and medical icon set.<br>- Refined the medical record view for signed-in users.<br>- Identified the connections required between the UI, user record, and symptom intake workflow. | 02/11/2026 | 02/11/2026 | MediMind AI source code and UI designs |
| Tuesday | - Studied the processing path from a medical document image to structured data and implemented prescription and lab-result reading steps.<br>- Added checks for extracted date of birth and gender before displaying them; derived the patient's age from the date of birth.<br>- Verified the transfer of these fields from backend processing to the frontend. | 03/11/2026 | 03/11/2026 | Project OCR and medical record code |
| Wednesday | - Developed the initial symptom intake workflow and a floating chat widget.<br>- Reviewed session persistence and synchronization between intake and chat, and corrected cases where a negated symptom was treated as present.<br>- Redesigned the home, profile, and medical facility views within a shared visual system; checked tab switching and account-specific display. | 04/11/2026 | 04/11/2026 | MediMind AI code, intake notes, and UI designs |
| Thursday | - Organized storage of processed prescriptions and lab results in user records.<br>- Added history and summaries so users could review documents after the original session.<br>- Checked the relationship between documents, consultation sessions, and account records to reduce the risk of mixing data between users. | 05/11/2026 | 05/11/2026 | Medical record and document-processing code |
| Friday | - Reviewed the chatbot layout against reference screens and improved spacing, text colors, and contrast.<br>- Replaced decorative AI icons with clearer medical icons and checked both theme variants.<br>- Compared the presentation of questions, responses, and navigation in the main chat and floating chat. | 06/11/2026 | 06/11/2026 | UI designs and frontend code |
| Saturday | - Improved medical facility search using a result list and interactive map, with a clearer map action and display state.<br>- Refined the search toolbar, colors, and facility cards; fixed a layout issue affecting tab independence.<br>- Checked navigation from a listed facility to its map location. | 07/11/2026 | 07/11/2026 | Medical facility code and UI designs |
| Sunday | - Improved consultation session tracking and synchronized intake facts with chat content.<br>- Required users to review and confirm a clinical summary before it was saved; fixed the OTP email template and consultation UI issues.<br>- Reviewed conversation history and distinguished session drafts from summaries approved for storage. | 08/11/2026 | 08/11/2026 | Consultation, record, and chatbot improvement code |

### Week 8 results:

- Established a connected workflow from **symptom intake to conversation, document processing, and record review**. This clarified each component's role and the points where frontend and backend data must stay synchronized.
- Practiced turning prescriptions and laboratory reports into structured information and checking demographic fields before display. Extracted data still requires review and should not be assumed accurate.
- Improved consultation persistence and the handling of negated facts. Distinguishing a present symptom from a denied one is essential to preserving the user's meaning.
- Added a place for prescriptions and lab results in the user record, with history and summaries for later review. This work highlighted the need to associate data with the correct account and keep test data separate from real records.
- Made the home, chat, profile, and facility interfaces more consistent in color, iconography, and layout; the interactive map helps users locate facilities from search results.
- Added explicit user confirmation before saving a consultation summary. This demonstrated the difference between temporary session data and health information retained for later use.
- Document processing and chatbot responses remain tools for initial information support. Health-related results require user review and do not replace assessment by a qualified professional.
