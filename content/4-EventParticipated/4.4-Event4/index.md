---
title: "Event 4 - FCAJ Community Day"
date: 2026-10-31
weight: 4
chapter: false
pre: "<b>4.4.</b>"
---

# AWS First Cloud AI Journey Community Day

## Event Information

- **Event:** AWS First Cloud AI Journey Community Day.
- **Date:** Saturday, October 31, 2026.
- **My role:** Attendee.

On October 31, 2026, I attended First Cloud AI Journey Community Day. The sessions offered perspectives on learning AWS, organizing software development with AI, and building applications using Serverless services.

The sessions helped me connect AWS knowledge with the process of building and operating real products.

## 1. New to AWS? Where Should You Start?

One session addressed where beginners should start with AWS. It introduced learning resources, a suggested learning path, and AWS credit opportunities for hands-on practice.

### A Suggested Learning Order

The slide **A Suggested AWS Learning Order** presented four steps:

1. **Foundations:** build basic knowledge of cloud concepts, Regions, Availability Zones, IAM, and security.
2. **Hands-on:** use labs to learn how services work in practice.
3. **Take Notes:** record concepts, errors, and solutions.
4. **Connect:** join the community to exchange ideas and continue learning.

The session also included a live introduction to AWS learning and community resources. My takeaway was to combine reading, practice, and notes rather than only browsing many services without understanding how to use them.

## 2. Lessons Learned from Building Software Factories

**Henry (Duc) Bui**, Head of Engineering at **CloudThinker**, shared his experience in **Lessons Learned from Building Software Factories**.

This session helped me visualize how a team organizes work with coding agents: preparing context, managing repositories, checking changes, and providing evidence for reviewers to assess the results.

### A Shared Control Folder

The slide **One folder runs everything** introduced a `control` folder as the starting point for work sessions. It contains notes, skills, and environment guides. From there, the agent reaches application, infrastructure, and documentation repositories, along with the machines it needs.

My understanding was that organizing this information gives the agent a consistent place to find context and instructions, instead of starting each session with scattered information.

### Evidence in Merge Requests

Another slide illustrated attaching before-and-after screenshots in light and dark themes, on wide and narrow screens. Reviewers could then see the UI results directly in the merge request.

This was relevant to my current work on the project UI. I noted the idea of saving screenshots and clearly describing changes to make review easier.

### Sharing Test Results Across Sessions

The section **Many sessions, one shared test cache** showed multiple coding sessions using a shared test cache and check runner. The slide described reusing results when the relevant code is unchanged and rerunning checks when it changes.

This gave me another perspective on development efficiency: beyond writing code faster, time spent waiting for checks and the reuse of results also matter.

## 3. Building a Game Application with Serverless

Another session covered building a game application with Serverless, from service selection to organizing the system components. The slide **Why Serverless?** emphasized reduced server management, scaling, and usage-based pricing in the model presented.

I also noticed the point about shared responsibility: while AWS operates the infrastructure, application builders still need to care for their code, IAM, and data.

### Comparing Earlier and Later Architectures

The slides **Architecture — Then** and **Architecture — Now** showed the application at two stages. The diagrams included components for the interface, authentication, APIs, Lambda processing, data storage, and monitoring.

I did not study every connection in detail, but the comparison helped me see how architecture can evolve as application workflows and requirements become clearer. It was an example of identifying each component's role before selecting services for a project.

### The Chrono Genesis TCG Project

The session on the **Chrono Genesis TCG** project introduced **Host Private Duel**, a feature for creating private match rooms. The interface displayed private room creation, a room code, and the status of waiting for an opponent to join.

Seeing the product alongside its architecture helped me connect a UI action with the Backend components needed to support it.

## 4. Lambda Web Functions: Native HTTP Engine

One slide was titled **Lambda Web Functions: Native HTTP Engine**, with three areas: Native HTTP Socket, Full Container Support, and Direct Framework Routing.

From this introduction, I noted topics to explore about packaging web applications and Backend frameworks, receiving HTTP requests, and deploying within a Lambda environment. This was new material for me at the event, and I need to study the documentation further before applying it to my project.

## 5. AWS SQS: Asynchronous Systems

**Luong Cam Dao (FCAJ)** presented **AWS SQS: Asynchronous Systems**.

The topic gave me a direction for studying queues and asynchronous processing: separating request intake from subsequent processing. At my current stage, I noted this as something to explore further to understand Backend organization when a project has tasks that need separate processing.

## 6. Results and Lessons Learned

After Community Day, I recorded several takeaways:

- A clearer AWS learning path: foundations, practice, notes, and community connections.
- An introduction to organizing context and documentation when working with coding agents.
- The value of screenshots and check results when reviewing changes.
- An initial perspective on sharing test results across development sessions.
- A clearer connection between product interfaces and Backend architecture through the game project built with Serverless.
- Lambda and SQS topics to explore further.

## Personal Reflection

At the time of the event, my project mainly involved building the UI, setting up a Backend skeleton, and exploring the necessary structure. The most useful lessons were therefore about organizing work and dividing a system into components with clear responsibilities.

I can begin with small steps such as organizing source code, documenting workflows, and saving screenshots of the UI. Serverless, Lambda, and queues are topics to study as project requirements become clearer.

Community Day was also an opportunity to meet FCAJ members and hear practical experience from people building real products.

## Event Photos

![Introduction to an AWS learning path for beginners](/images/4-EventParticipated/4.4-Event4/aws-learning.png)

![Henry Duc Bui presenting lessons from building Software Factories](/images/4-EventParticipated/4.4-Event4/software-factories.png)

![The application's later architecture](/images/4-EventParticipated/4.4-Event4/architecture-now.png)

![The Lambda Web Functions: Native HTTP Engine slide at the event](/images/4-EventParticipated/4.4-Event4/lambda-web.png)

![Luong Cam Dao's AWS SQS: Asynchronous Systems introduction](/images/4-EventParticipated/4.4-Event4/sqs.png)
