---
title: "Week 9 Worklog"
date: 2026-11-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 objectives:

- Extend MediMind AI beyond initial consultation with meal suggestions and habit tracking while defining the limits of nutrition guidance in a health application.
- Study how to combine a sourced recipe catalog, filtering rules, and a language model without letting the model invent ingredients or unverified medical benefits.
- Evaluate chatbot answers for source relevance, safety-sensitive cases, and Vietnamese questions against predominantly English reference material.
- Improve medical facility search and the presentation of facility details.
- Investigate declining retrieval relevance as the RAG corpus grows, and organize data and backend components for repeatable testing.

### Work completed this week:

| Day | Work | Start date | Completion date | Reference material |
| --- | --- | --- | --- | --- |
| Tuesday | - Designed and implemented **Nutrition Studio** with meal suggestions, AI-assisted recipe content, and habit tracking.<br>- Separated the user interface, meal-filtering rules, and backend service; identified which information comes from application-controlled data and which is model-generated explanation.<br>- Added initial tests for nutrition rules and interaction flows. | 10/11/2026 | 10/11/2026 | Nutrition Studio code and project nutrition guidance |
| Wednesday | - Extended recommendation rules for users who describe multiple health conditions or ingredients to avoid.<br>- Imported and cleaned recipe data for a local catalog, with a clearly labeled filtered fallback when the AI service is unavailable.<br>- Reviewed recipe names, ingredients, and source records so model output would not be presented as a verified original recipe. | 11/11/2026 | 11/11/2026 | Nutrition recommendations documentation, recipe data, and source code |
| Thursday | - Set up chatbot answer-quality scenarios to examine source use and cases requiring a safe response instead of a definite medical conclusion.<br>- Experimented with Vietnamese-to-English query expansion to find relevant documents, distinguishing development results from real-world validation.<br>- Aligned the medical facility interface with the rest of the application. | 12/11/2026 | 12/11/2026 | Chatbot improvement notes, evaluation materials, and UI code |
| Friday | - Reviewed the medical facility search page in both themes and fixed inconsistent text and component colors.<br>- Restored Google Maps and improved the detail drawer shown when a facility is selected.<br>- Checked how the result list, map position, and detail panel work together to reduce repeated navigation. | 13/11/2026 | 13/11/2026 | Medical facility code and UI designs |
| Sunday | - Investigated less relevant retrieval results after expanding the RAG knowledge base; reviewed document selection, classification, and search behavior.<br>- Expanded the curated medical corpus, adjusted the retrieval flow, and built development evaluations for comparing results on sample questions.<br>- Reorganized parts of the backend and configuration to make component responsibilities clearer. | 15/11/2026 | 15/11/2026 | RAG source code, retrieval evaluation notes, and curated data |

### Week 9 results:

- Built Nutrition Studio with a UI, recipe catalog, filtering rules, and habit tracking. This clarified the distinction between **source data**, **application-controlled constraints**, and **AI explanations** within one recommendation workflow.
- Added a local recipe catalog and a fallback when the AI provider is unavailable. Fallback items must be labeled as filtered catalog results rather than described as AI-ranked suggestions.
- Established development scenarios for examining chatbot answers, citations, and safety behavior. Technical tests can detect implementation faults but do not establish clinical accuracy.
- Practiced cross-language document search and learned that multilingual retrieval should be assessed with independent questions and relevance judgments to avoid optimistic conclusions.
- Improved the medical facility page's consistency, restored the map, and refined the detail drawer so users can compare locations with search results more easily.
- Identified **retrieval dilution**: as the corpus grows, less relevant passages may crowd out needed sources. Curation, corpus versioning, and repeatable query-based evaluation are important before further expansion.
- Nutrition suggestions and chatbot answers provide initial information support. The application does not produce a clinician-validated personal meal plan and does not replace medical or dietetic advice.
