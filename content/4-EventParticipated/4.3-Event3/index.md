---
title: "Event 3 - FCAJ Mini Meeting"
date: 2026-10-24
weight: 3
chapter: false
pre: "<b>4.3.</b>"
---

# FCAJ Mini Meeting: Voice AI, AWS RAM, Security Agent, and AgentCore

## Event Information

- **Event:** FCAJ Mini Meeting.
- **Date:** Saturday, October 24, 2026.
- **My role:** Attendee.

On October 24, 2026, I attended a mini meeting organized by the First Cloud AI Journey community. The sessions covered Vietnamese Voice AI, resource sharing across AWS accounts, web application security, and AI Agent architecture.

This report records what I learned from the meeting, based on my notes and photographs of the presentation slides.

## 1. Hear, Think, Speak — Session by Kiet Tran

Kiet Tran, an AI Engineer at Revve AI, presented **Hear, Think, Speak: Building a Vietnamese voice-AI contact center on AWS**. I heard about the Voice AI platform, applications related to interviews and contact centers, and the challenges of bringing voice conversations into a real system.

One point that stood out was that a conversation needs more than a correct answer. The system also needs to detect when the user has finished speaking, process the input, and respond with suitable latency to keep the interaction natural.

### Three Approaches to Building a Voice Agent

The presentation introduced three approaches:

- **Cascade:** separates the pipeline into ASR → LLM → TTS, converting speech into text, processing the text, and generating a spoken response.
- **Speech-to-Speech (S2S):** processes audio input and output through a speech model.
- **Full Duplex S2S:** aims for simultaneous listening and speaking to bring interaction closer to a human conversation.

According to the session, the team continued to use **Cascade in production** while experimenting with and monitoring S2S approaches. For the team's Vietnamese use case, Cascade allowed them to choose suitable components and control responses through an intermediate text step.

I learned that architecture choices should reflect practical requirements, including Vietnamese speech quality, content review, logging, and the ability to replace individual components.

### Call Processing and AWS Architecture

The call-flow slide showed several cooperating components: a SIP server, media server, noise cancellation, turn detection, speech-to-text, an LLM with a flow engine, and text-to-speech.

The Revve architecture presentation described deployment within one Region and within the customer's account. I saw how the components serving web access, phone calls, models, and data were connected within the system.

Kiet also shared a POC for a Vietnamese bank, covering request intake, verification, intent identification, and handling through APIs or transfer to a human agent. This example helped me understand the importance of business workflows and human handoff in a Voice AI application.

## 2. AWS Resource Access Manager — Session by Long Huynh

Long Huynh presented **AWS Resource Access Manager (AWS RAM)**. The session began with the challenges of managing multiple AWS accounts and the need to share resources between them.

My notes covered the following topics:

- **The Multi-account Challenge:** difficulties in managing resources across multiple accounts.
- **What is AWS RAM:** an introduction to its role in resource sharing.
- **Anatomy of a Resource Share:** resources, the recipients of a share, and permissions.
- **How Sharing Works End to End:** the sharing flow from the resource owner's account to the consuming account.
- **Regions, Global and AZ IDs:** considerations about resource scope and Availability Zone identifiers.
- **RAM in the Landing Zone:** resource sharing in an enterprise environment.

According to my notes from the session, the speaker mentioned support for sharing resources from more than 40 services. My main takeaway was that sharing requires clarity about which resources are shared, which accounts can use them, and what permissions they receive.

This session gave me an initial view of infrastructure organization across multiple accounts, beyond working with individual services in a single account.

## 3. AWS Security Agent — Session by Thinh

Thinh presented **Securing Your Web Apps With AWS Security Agent**. I was introduced to an approach to web application security supported by an agent and the considerations involved in applying it to a project.

One topic that stood out was **Design Security Review**. The slide described using Markdown documents or Terraform code as input to review a design against configured security requirement packs.

This helped me understand that security review can begin with system documentation and design, rather than waiting until an application is complete.

Thinh also discussed costs in a section titled **The Pricing Reality**. My takeaway was to consider the scope of the assessment and the time an agent spends performing its tasks when evaluating usage costs.

## 4. Amazon Bedrock AgentCore — Session by Xuan An

Xuan An presented **Amazon Bedrock AgentCore**, focusing on Runtime and Memory Architecture. The session introduced AI Agent, Agentic AI, and Agentic System concepts before moving into AgentCore Runtime and AgentCore Memory.

In the Memory section, I heard about organizing interactions as events and concepts such as Memory ID, Actor ID, Session ID, Payload, Timestamp, and Branch. The slide helped me visualize how information from an interaction session can be stored and organized.

I also noted **Kiro Crew** and **App & Extensibility**, which were mentioned during the meeting. These are topics I would like to explore further to understand how they could relate to project development.

## 5. Results and Lessons Learned

The mini meeting gave me an initial understanding of several topics:

- The three Voice Agent approaches and why the team chose Cascade for the Vietnamese use case presented.
- How a Voice AI system combines audio processing, models, business workflows, and infrastructure.
- AWS RAM and the challenge of sharing resources across multiple accounts.
- The value of reviewing security during design and considering costs when using supporting tools.
- AgentCore Runtime, Memory, and the organization of information within an interaction session.

At this stage, my project is only beginning to take shape through its UI and Backend skeleton. The sessions helped me identify components to study later. I see them as reference knowledge for understanding system structure, rather than technologies I have already fully implemented in my project.

## Personal Reflection

The most relevant lesson for my project was how each system is divided into components with clear responsibilities. For both Voice AI and AI Agents, choosing a model is only one part of the work. I also need to understand where data goes, how it is processed, and how interaction sessions are managed.

The meeting gave me further direction for learning and an opportunity to meet community members and hear practical experience from FCAJ speakers.

## Event Photos

![Opening slide of Kiet Tran's Hear, Think, Speak session](/images/4-EventParticipated/4.3-Event3/hear-think-speak.png)

![Long Huynh's AWS Resource Access Manager session](/images/4-EventParticipated/4.3-Event3/aws-ram.png)

![Web application security with AWS Security Agent](/images/4-EventParticipated/4.3-Event3/security-agent.png)

![Xuan An's introduction to Amazon Bedrock AgentCore](/images/4-EventParticipated/4.3-Event3/agentcore.png)
