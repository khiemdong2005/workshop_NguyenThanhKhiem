---
title: "Week 7 Worklog"
date: 2026-10-26
weight: 7
chapter: false
pre: "<b>1.7.</b> "
---

### Week 7 Objectives:

- Build the first web version and integrate a chatbot that accepts text and images and retrieves supporting documents.
- Fix image uploads and develop the prescription OCR flow.
- Compare PaddleOCR, TrOCR, and sending images to a model API to choose an approach for reading prescriptions.
- Review the proposal, cost estimate, and AWS architecture diagram.
- Attend AWS First Cloud AI Journey Community Day.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Committed the first version of the app with a web interface, electronic health records (EHR), prescription OCR, and symptom triage.</li><li>Used Flask to handle requests and kept the interface, model instructions, and triage logic in separate files.</li><li>Reorganized the project README.</li></ul> | 26/10/2026 | 26/10/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/bcde09c8f6a54244178c6bbb0b09d631b3c88a6a) |
| 3 | <ul><li>Removed a few unnecessary features and tried the website.</li><li>Used Gemini Vision to let the chatbot accept questions and images. Loaded medical documents for the chatbot to look up before answering (RAG) and added reference images.</li><li>Added two layers of response checks and updated Vietnamese and English support for the chatbot flow through Flask and FastAPI.</li></ul> | 27/10/2026 | 27/10/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/474f6e62efc39933d3efde62f07a2b7e1c879abc) |
| 4 | <ul><li>Fixed the chat attachment button so it opened the image picker.</li><li>Fixed the flow for handling skin images, switched to Gemini 3.1 Flash-Lite, and added a fallback model.</li><li>Checked how to run FastAPI and inspect the API in Swagger, then reviewed where account information was stored.</li><li>Compared using PaddleOCR or TrOCR to read the prescription with sending the image to a model API.</li><li>Used UI/UX Pro Max guidance to review icons, switched to SVG icons that fit the medical interface, simplified the chat display, and added medication schedule tracking.</li></ul> | 28/10/2026 | 28/10/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/3ff6ec2aa3f2ea54cec086854d16bd2338c5cba6) |
| 5 | <ul><li>Removed hardcoded absolute paths and configured the app to locate .env from the project root.</li><li>Tried a hybrid OCR flow for prescriptions: prepare the image, read the text with OCR, and pass it to Gemini for analysis.</li><li>Connected the extracted data to the prescription screen, simplified its layout, and fixed a tab navigation issue.</li><li>Read about Amazon Comprehend Medical and noted its limitations for Vietnamese data.</li></ul> | 29/10/2026 | 29/10/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/5dbd223863df779f72717589e7074e27251c3d14)<br>[AWS Comprehend Medical](https://docs.aws.amazon.com/comprehend-medical/latest/dev/) |
| 6 | <ul><li>Tried a dark background, then switched to a light design with hospital imagery. Adjusted the navigation bar and three main content panels.</li><li>Reviewed what the AWS diagram needed to show and compared it with the components already in the app.</li><li>Updated the index so the chatbot could search the newer set of medical documents.</li></ul> | 30/10/2026 | 30/10/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/cb34ab66e5765c7b1f2c507d891c4748774125eb) |
| 7 | <ul><li>Reviewed the proposal and workshop criteria, focusing on architecture, the demo, and presentation. Revisited how the proposal described the prescription-reading model.</li><li>Redrew the AWS architecture in 16:9 for presentation and exported SVG and PNG versions.</li><li>Attended AWS First Cloud AI Journey Community Day, listened to the talks, and met other FCAJ members.</li></ul> | 31/10/2026 | 31/10/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/baa06e19ac20c41ca75a74bfecca16cf1b338561) |

### Week 7 Achievements:

- Published the first web version in the repository, with initial screens for health records, prescription reading, and symptom triage.
- Connected Gemini Vision to the chatbot and used RAG to retrieve relevant documents. Updated the vector index by the end of the week.
- Fixed the button that opens the chat image picker.
- Tried a hybrid OCR flow that separates text extraction from AI analysis. PaddleOCR, TrOCR, and Amazon Comprehend Medical were researched as options.
- Updated the interface with a light background and rearranged the navigation bar and content panels.
- Updated the proposal with an AWS cost estimate and exported the 16:9 architecture diagram as SVG and PNG.
- Attended FCAJ Community Day on 31 October and spoke with members.
