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
- Study how Amazon Bedrock Evaluations separates document retrieval assessment from generated-answer assessment for RAG.
- Continue improving the medical facility interface and synchronization between its list and map.

### Tasks carried out this week:

| Day | Task | Start date | Completion date | Reference material |
| --- | --- | --- | --- | --- |
| Tuesday | - Sketched the UI for meal suggestions and habit tracking.<br>- Studied how to separate recipe data, backend rules, API responses, and frontend display.<br>- Connected the interface to returned data and checked some incomplete-input cases. | 10/11/2026 | 10/11/2026 | Project |
| Wednesday | - Organized recipe data for searching and filtering.<br>- Added rules for several requirements in one request or an ingredient to avoid.<br>- Studied how to return a fallback from available data when an external service does not respond, rather than leaving the interface empty. | 11/11/2026 | 11/11/2026 | Project |
| Thursday | - Studied how to check answer quality using sample questions and accompanying sources.<br>- Reviewed the backend retrieval steps: receive a question, find relevant passages, and pass them to answer generation.<br>- Tried finding English documents for Vietnamese questions and noted results that did not closely match the question.<br>- Read the Amazon Bedrock Evaluations documentation to compare retrieve-only evaluation with retrieve-and-generate evaluation and relate those criteria to the project's sample questions. | 12/11/2026 | 12/11/2026 | Project; [AWS Bedrock RAG Evaluations](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-evaluation-metrics.html) |
| Friday | - Checked the medical facility interface in light and dark themes.<br>- Adjusted the result list, map, and detail panel shown when a user selects a location.<br>- Reviewed UI state so the map and list show the same selected facility. | 13/11/2026 | 13/11/2026 | Project |

### Week 9 results:

- Better understood how a feature is divided into UI, API, business logic, and data. This makes it easier to locate errors when the displayed result is wrong.
- Practiced validating input and preparing a fallback result when an external service fails.
- Learned to organize recipe data and apply filtering rules before sending results to the interface.
- Started using sample questions to check document retrieval and compare cited sources with the response.
- Learned to ask two separate questions when evaluating RAG: did the system find relevant documents, and is the answer supported by them? I studied the Amazon Bedrock Evaluations approach but did not run an AWS evaluation job.
- Found that Vietnamese questions need separate checking when much of the document collection is in English.
- Improved the medical facility interface, especially synchronization between the result list, map location, and detail panel.
