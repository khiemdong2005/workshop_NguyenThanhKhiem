---
title: "Week 6 Worklog"
date: 2026-10-19
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

- Understand application scaling, load balancing, and system monitoring with Amazon CloudWatch for AI API/Backend deployment[cite: 1].
- Learn about in-memory caching mechanisms with Amazon ElastiCache and content delivery via CDN (Amazon CloudFront)[cite: 1, 2].
- Begin actual project implementation: research project-related technologies and libraries, and build the basic user interface (UI).
- Explore AWS cost optimization strategies.
- Attend the FCAJ meeting to gain practical insights from community speakers.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Learn about application scaling with **EC2 Auto Scaling** (Scaling, Auto Scaling Group, Load Balancer)[cite: 1] <br> - Explore system monitoring with **Amazon CloudWatch** (Logs, Metrics, Alarms)[cite: 1] | 19/10/2026 | 19/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - Learn about in-memory caching with **Amazon ElastiCache (Redis)** for AI API session/cache storage[cite: 1] <br> - Learn the fundamentals of **Amazon Route 53** and **Amazon CloudFront**[cite: 1, 2] | 20/10/2026 | 20/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Wed | - Complete the **AWS Networking Workshop** (VPC, Subnet, Security)[cite: 1, 2] <br> - Practice the **Building a High-Availability Web Application** lab (combining EC2 + Load Balancer + Auto Scaling + DB)[cite: 1, 2] | 21/10/2026 | 21/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Thu | - Start project implementation: research documentation, technologies, and business workflows related to the project <br> - Design the layout and build the basic user interface (UI) for the system | 22/10/2026 | 22/10/2026 | |
| Fri | - Continue refining the UI and prepare the integration structure between the Frontend and Backend/AI API <br> - Explore AWS cost optimization techniques during lab practice and project development | 23/10/2026 | 23/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Sat | - Attend the FCAJ meeting | 24/10/2026 | 24/10/2026 | Event FCAJ |

### Week 6 Achievements:

- Clearly understood how **EC2 Auto Scaling** and **Load Balancer** work, as well as how to use **Amazon CloudWatch** to track logs, monitor metrics, and set up system alarms[cite: 1].

- Understood the role of **Amazon ElastiCache (Redis)** in caching AI API responses, along with basic usage of **Route 53** and **CloudFront**[cite: 1, 2].

- Consolidated networking knowledge (VPC, Subnet, Security) and successfully integrated EC2 + Load Balancer + Auto Scaling + DB into a high-availability web application[cite: 1, 2].

- Initiated project development: gained a clearer understanding of the required technologies and tools, and built the foundational UI ready for AI feature integration in the upcoming steps.

- Learned additional ways to optimize costs on AWS when operating infrastructure and developing the project.

- **Attended the FCAJ meeting and gained valuable practical insights:**
  + **Hear, Think, Speak (Mr. Kiet Tran - Revve AI):** Explored AI interview & Contact Center platforms[cite: 5], and compared 3 approaches to building a Voice Agent: *Cascade* (ASR -> LLM -> TTS, which remains better suited for Vietnamese thanks to the controllable intermediate text checkpoint), *Speech-to-Speech (S2S)*, and *Full Duplex S2S*[cite: 8].
  + **AWS Resource Access Manager (RAM) (Mr. Long Huynh):** Understood the multi-account challenge, the concept of AWS RAM, and the Anatomy of a Resource Share (sharing resources with sub-accounts), end-to-end sharing workflows across more than 40 services, a deep dive into Regions/Global/AZ IDs, and applying RAM within an Enterprise Landing Zone[cite: 7].
  + **AWS Security Agent & Bedrock AgentCore:** Listened to Mr. Thinh's sharing on securing web applications with **AWS Security Agent** (along with its real-world pricing model)[cite: 3, 6] and Mr. Xuan An's session
