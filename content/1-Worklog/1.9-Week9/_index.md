---
title: "Week 9 Worklog"
date: 2026-11-09
weight: 9
chapter: false
pre: "<b>1.9.</b> "
---

### Week 9 Objectives:

- Run the app with Flask and Docker Compose and investigate local access issues.
- Build the Nutrition section and use pytest to check meal filtering when multiple health conditions are selected.
- Use Python to standardize recipes from ViFoodRec and Wikibooks, export the JSON catalog, and check meal images.
- Evaluate how ChromaDB retrieves English documents for Vietnamese queries and review Gemini's answers.
- Review prescription extraction and improve the healthcare facilities map built with Google Maps.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Started the previous week's web app locally with Flask and checked browser access. Flask reported that the server had started, but the browser could not load the interface.</li><li>Changed the Flask listening port and retried browser access to check for a possible port conflict. The access issue persisted on the new port.</li></ul> | 09/11/2026 | 09/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 3 | <ul><li>The initial plan could not be implemented, so I added a Nutrition section to the main interface in place of the old records screen.</li><li>Built the form for selecting health conditions, meal suggestions, and habit tracking. Removed buttons and elements left over from the previous screen.</li></ul> | 10/11/2026 | 10/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 4 | <ul><li>Imported the ViFoodRec recipe table and used a Python script to collect additional data from Wikibooks. Filtered out unsuitable rows, separated ingredients and instructions, and exported JSON for the recipe catalog.</li><li>Identified meal images that failed to load, replaced the image files in the repository, and updated the interface to load them from the static assets directory.</li><li>Updated the Python meal-filtering rules and added a pytest case to verify that the filter applies the constraints for all selected health conditions together.</li></ul> | 11/11/2026 | 11/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 5 | <ul><li>Reviewed the code and tried opening a prescription in the prefilled form. Noted a drug name the app misread for follow-up.</li><li>Tried expanding Vietnamese questions to retrieve English documents from ChromaDB. Compared the results on sample questions and read how Amazon Bedrock Evaluations assesses retrieval and answers separately.</li><li>Resolved a Gemini authentication issue and ran the answer evaluation set, then synced the healthcare facilities page into the working version.</li></ul> | 12/11/2026 | 12/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical/commit/3361426ea733e4d1b9de3ac85419200c8c366670)<br>[AWS Bedrock RAG Evaluations](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-evaluation-metrics.html) |
| 6 | <ul><li>Tried building and running the application with Docker Compose. Added timeouts, retries, and fallback responses for external service failures.</li><li>Updated the facilities page colors, restored Google Maps, and adjusted the detail panel for the selected location.</li><li>Reviewed the interface and noted remaining issues with alerts, prescription results, and the summary display. Reorganized the documentation in the repository.</li><li>Looked at how to place facility markers by coordinate with Google Maps Platform APIs and restrict a browser API key by website.</li></ul> | 13/11/2026 | 13/11/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |

### Week 9 Achievements:

- Reproduced the local web access issue. Flask reported that it had started, but the browser still could not load the page after changing ports.
- Integrated the Nutrition section with health-condition input, meal suggestions, and habit tracking. Removed leftover elements from the previous records screen.
- Exported the ViFoodRec and Wikibooks recipe catalog to JSON with separate fields for ingredients and cooking instructions. Replaced broken images and updated their local paths.
- Updated the Python meal-filtering rules and added a pytest case for applying the constraints of multiple health conditions together.
- Prepared sample questions and a report comparing ChromaDB retrieval of English documents from Vietnamese queries. Resolved the Gemini authentication issue and ran the answer evaluation set.
- Recorded a drug-name recognition error in the prefilled prescription form and remaining display issues involving alerts, prescription results, and summaries.
- Tried building and starting the app with Docker Compose. Added timeouts, retries, and fallback responses for external service failures.
- Restored Google Maps on the healthcare facilities page and updated its colors and selected-location detail panel. Reorganized the documentation directory in the repository.
