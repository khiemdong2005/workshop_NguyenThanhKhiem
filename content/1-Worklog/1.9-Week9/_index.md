---
title: "Week 9 Worklog"
date: 2026-11-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 objectives:

- Learn how to organize recipe data for a nutrition suggestion feature.
- Practice applying filters when users have several health needs or need to avoid certain ingredients.
- Study how to review chatbot answers and find useful references for Vietnamese questions.
- Continue improving the medical facility page and review the documents used for question answering.

### Tasks carried out this week:

| Day | Task | Start date | Completion date | Reference material |
| --- | --- | --- | --- | --- |
| Tuesday | - Identified the information needed for meal suggestions: dish name, ingredients, preparation steps, and user requirements.<br>- Started building the meal suggestion page and a habit tracking area.<br>- Separated work on data, selection rules, and the display interface. | 10/11/2026 | 10/11/2026 | [Nutrition notes](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/nutrition-recommendations.md); [source code](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/nutrition_service.py) |
| Wednesday | - Studied how to handle several health conditions or an ingredient to avoid in one request.<br>- Collected, cleaned, and organized recipe data for local lookup.<br>- Checked the case where the AI service is unavailable and showed filtered catalog items instead. | 11/11/2026 | 11/11/2026 | [Nutrition notes](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/nutrition-recommendations.md); [recipe catalog](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/recipe_catalog.py) |
| Thursday | - Studied how to review an answer: whether it addresses the question, cites a document that was actually found, and gives appropriate guidance.<br>- Tried finding English documents for Vietnamese questions and noted both relevant and less relevant results.<br>- Continued adjusting the medical facility interface. | 12/11/2026 | 12/11/2026 | [Chatbot notes](https://github.com/khiemdong2005/chatbot_medical/blob/main/docs/chatbot-improvements.md); [RAG code](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/rag_service.py) |
| Friday | - Checked the medical facility page in light and dark themes and corrected text or cards that were hard to read.<br>- Restored the map and improved the detail panel shown after selecting a facility.<br>- Reviewed navigation from the result list to the corresponding map location. | 13/11/2026 | 13/11/2026 | [Project interface](https://github.com/khiemdong2005/chatbot_medical/blob/main/templates/index.html) |
| Sunday | - Reviewed the documents used for health-related answers and studied why adding more documents sometimes produced less focused search results.<br>- Classified and added relevant documents, then checked retrieval with sample questions.<br>- Reorganized parts of the backend to make later checks and document additions easier. | 15/11/2026 | 15/11/2026 | [Document retrieval code](https://github.com/khiemdong2005/chatbot_medical/blob/main/core/rag_service.py) |

### Week 9 results:

- Learned how to prepare recipe data for suggestions, including the need for clear sources and ingredient information.
- Built an initial meal suggestion page, recipe catalog, and habit tracking area.
- Practiced combining filtering rules with local data for ingredient exclusions and multiple user needs.
- Started reviewing chatbot answers against the question, response, and cited sources rather than only checking whether the chatbot responded.
- Found that Vietnamese questions may be harder to match with documents written mostly in English; more sample questions are needed to assess search quality.
- Improved the medical facility page and map so the list, locations, and details are easier to use together.
- Learned that adding documents does not automatically improve retrieval; documents need to be selected and results checked after each addition.
