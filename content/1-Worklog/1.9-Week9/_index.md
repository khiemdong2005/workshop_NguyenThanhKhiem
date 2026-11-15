---
title: "Week 9 Worklog"
date: 2026-11-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 objectives:

- Learn how to divide a new feature into UI, API, business logic, and data components.
- Practice validating input, handling errors, and showing appropriate states in the frontend.
- Study document organization and retrieval evaluation in the backend.
- Continue improving the medical facility interface and synchronization between its list and map.

### Tasks carried out this week:

| Day | Task | Start date | Completion date | Reference material |
| --- | --- | --- | --- | --- |
| Tuesday | - Sketched the UI for meal suggestions and habit tracking.<br>- Studied how to separate recipe data, backend rules, API responses, and frontend display.<br>- Connected the interface to returned data and checked some incomplete-input cases. | 10/11/2026 | 10/11/2026 | [Feature notes](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/nutrition-recommendations.md); [Backend code](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/nutrition_service.py) |
| Wednesday | - Organized recipe data for searching and filtering.<br>- Added rules for several requirements in one request or an ingredient to avoid.<br>- Studied how to return a fallback from available data when an external service does not respond, rather than leaving the interface empty. | 11/11/2026 | 11/11/2026 | [Data catalog](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/recipe_catalog.py); [Processing rules](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/nutrition_rules.py) |
| Thursday | - Studied how to check answer quality using sample questions and accompanying sources.<br>- Reviewed the backend retrieval steps: receive a question, find relevant passages, and pass them to answer generation.<br>- Tried finding English documents for Vietnamese questions and noted results that did not closely match the question. | 12/11/2026 | 12/11/2026 | [Chatbot review notes](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md); [Retrieval code](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/rag_service.py) |
| Friday | - Checked the medical facility interface in light and dark themes.<br>- Adjusted the result list, map, and detail panel shown when a user selects a location.<br>- Reviewed UI state so the map and list show the same selected facility. | 13/11/2026 | 13/11/2026 | [HTML interface](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html); [JavaScript](https://github.com/khiemdong2005/chatbot_medical/blob/main/static/js/app.js) |
| Sunday | - Reviewed the backend structure and the steps for adding documents to the search collection.<br>- Studied why a larger collection sometimes returned less relevant passages; adjusted document selection and checked results using sample questions.<br>- Reorganized processing components to make later data additions and tests easier to follow. | 15/11/2026 | 15/11/2026 | [Retrieval code](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/rag_service.py); [Backend code](https://github.com/khiemdong2005/chatbot_medical/blob/main/app.py) |

### Week 9 results:

- Better understood how a feature is divided into UI, API, business logic, and data. This makes it easier to locate errors when the displayed result is wrong.
- Practiced validating input and preparing a fallback result when an external service fails.
- Learned to organize recipe data and apply filtering rules before sending results to the interface.
- Started using sample questions to check document retrieval and compare cited sources with the response.
- Found that Vietnamese questions need separate checking when much of the document collection is in English.
- Improved the medical facility interface, especially synchronization between the result list, map location, and detail panel.
- Learned that adding data also requires checking search quality; a larger collection alone can make results less focused.
