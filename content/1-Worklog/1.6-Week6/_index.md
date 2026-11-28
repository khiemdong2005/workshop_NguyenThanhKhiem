---
title: "Week 6 Worklog"
date: 2026-10-19
weight: 6
chapter: false
pre: "<b>1.6.</b> "
---

### Week 6 Objectives:

- Understand application scaling, load balancing, and system monitoring with Amazon CloudWatch for AI API/Backend deployment.
- Learn about in-memory caching mechanisms with Amazon ElastiCache and content delivery via CDN (Amazon CloudFront).
- Begin actual project implementation: research project-related technologies and libraries, and build the basic user interface (UI).
- Explore AWS cost optimization strategies.
- Attend the FCAJ meeting to gain practical insights from community speakers.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | <ul><li>Learn about application scaling with **EC2 Auto Scaling** (Scaling, Auto Scaling Group, Load Balancer)</li><li>Explore system monitoring with **Amazon CloudWatch** (Logs, Metrics, Alarms)</li></ul> | 19/10/2026 | 19/10/2026 | https://cloudjourney.awsfcaj.com/ |
| 3 | <ul><li>Learn about in-memory caching with **Amazon ElastiCache (Redis)** for AI API session/cache storage</li><li>Learn the fundamentals of **Amazon Route 53** and **Amazon CloudFront**</li><li>Reviewed how to use AWS Certificate Manager (ACM) for custom-domain TLS certificates and AWS WAF with CloudFront to filter web requests.</li></ul> | 20/10/2026 | 20/10/2026 | https://cloudjourney.awsfcaj.com/ |
| 4 | <ul><li>Complete the **AWS Networking Workshop** (VPC, Subnet, Security)</li><li>Practice the **Building a High-Availability Web Application** lab (combining EC2 + Load Balancer + Auto Scaling + DB)</li><li>Explored how an Application Load Balancer (ALB) uses target groups and health checks to route requests to healthy servers.</li></ul> | 21/10/2026 | 21/10/2026 | https://cloudjourney.awsfcaj.com/ |
| 5 | <ul><li>Start project implementation: research documentation, technologies, and business workflows related to the project</li><li>Design the layout and build the basic user interface (UI) for the system</li><li>Used the overall sketch to start laying out the main page and how users would reach each group of features. This was the initial interface layout.</li><li>Finalized the project name and tagline for the interface.</li><li>Used Google Stitch, Google AI Studio, and ChatGPT to explore ideas and sketch the project’s interface layout.</li></ul> | 22/10/2026 | 22/10/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical) |
| 6 | <ul><li>Continue refining the UI and prepare the integration structure between the Frontend and Backend/AI API</li><li>Explore AWS cost optimization techniques during lab practice and project development</li><li>Reviewed which actions could be handled in the interface and which would need a request to the backend or AI service.</li></ul> | 23/10/2026 | 23/10/2026 | [Project](https://github.com/khiemdong2005/chatbot_medical)<br>https://cloudjourney.awsfcaj.com/ |
| 7 | <ul><li>Attend the FCAJ meeting</li></ul> | 24/10/2026 | 24/10/2026 |  |

### Week 6 Achievements:

- Settled on a name and tagline and drafted the first interface layout to guide development of the screens.
- I learned how a load balancer distributes requests and how EC2 Auto Scaling adjusts the number of servers.
- I got familiar with logs, metrics, and alarms in Amazon CloudWatch.
- I looked at when to use Redis for caching, Route 53 for DNS, and CloudFront for content delivery.
- I revisited VPCs, subnets, and access controls in a networking lab.
- I tried combining EC2, a load balancer, Auto Scaling, and a database in a web application lab.
- I looked into AWS cost controls while doing labs and planning the project deployment.
- The FCAJ meetup introduced me to different approaches to voice assistants and how AWS RAM shares resources across accounts.
- I also heard about web application security with AWS Security Agent and how Amazon Bedrock AgentCore handles runtime and memory.
