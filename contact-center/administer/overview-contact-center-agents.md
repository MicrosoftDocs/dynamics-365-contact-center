---
title: Overview of contact center agents in Dynamics 365 Contact Center
description: Get an overview of contact center agents in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: overview
ms.collection: bap-ai-copilot
ms.date: 04/27/2027
ms.custom: bap-template
---

# Overview of contact center agents

Dynamics 365 Contact Center includes AI-powered agents that automate critical operational tasks, enhance quality management, and streamline service operations. These autonomous agents work alongside your team to improve efficiency, reduce manual effort, and deliver better customer experiences.

## Customer Assist Agent

### Real-time voice agents

Real-time voice agents are AI-powered conversational agents designed to deliver natural, voice-first interactions that go beyond traditional interactive voice response (IVR) systems. Instead of relying on menu-driven inputs or text-based exchanges, these agents enable customers to speak naturally and receive immediate spoken responses, creating fluid, human-like conversations. By using real-time audio processing, real-time voice agents support instant turn-taking, natural pauses, and context-aware responses, making interactions faster, more intuitive, and more engaging for customers.

Learn more in [Real-time voice agents](/microsoft-copilot-studio/voice-realtime-voice-agents).

### Proactive engagement

Proactive engagement helps organizations initiate outbound voice interactions at scale by reaching customers with the right message, at the right time, through AI-led or representative-led experiences. It supports campaign-based outreach for scenarios such as reminders, follow-ups, service updates, and other proactive customer communications.

**Key capabilities**:

- **Outbound engagement setup**: Create proactive engagements from outbound workstreams and define the audience, routing, and business context.
- **AI-led or representative-led calls**: Choose whether calls are handled by Copilot first, by service representatives, or by a combination of both based on the engagement design.
- **Flexible dialing modes**: Use Copilot, preview, progressive, or predictive dialing modes to balance scale, speed, and service quality.
- **Operational controls**: Configure display numbers, retry behavior, quiet hours, frequency limits, and pacing rules to align outreach with business and compliance requirements.
- **Targeted outreach**: Source contacts through file upload, APIs, MCP, or Customer Insights journeys, and prioritize how calls are processed.

Learn more in [Configure proactive engagement](configure-proactive-engagement.md).

## Quality Assurance Agent

Quality Assurance Agent brings AI-powered support to supervisors and quality managers by autonomously monitoring conversations in real time and after completion.

**Key capabilities**:

- **Real-time quality evaluation**: Automatically reviews conversations as they happen and after completion
- **Proactive alerts**: Identifies quality issues early so supervisors can intervene when needed
- **Quality scoring**: Provides automated quality scores without manual review effort
- **Performance insights**: Helps improve team performance through early issue detection

**When to use**: Supervisors and quality managers who need to monitor conversation quality, ensure compliance, and improve representative performance.

## Service Operations Agent (preview)

Service Operations Agent is a self-service AI agent that supports administrators with configuration, validation, and troubleshooting tasks using natural language.

**Key capabilities**:

- **Conversational setup**: Configure channels and workstreams through natural language prompts
- **Queue management**: Assign users to queues, create skills, and manage operating hours
- **Channel management**: Sync phone numbers with Azure Communication Services and Teams
- **Diagnostics and troubleshooting**: Query capabilities and troubleshoot configuration issues
- **Best practices guidance**: Receive recommendations for contact center configuration

**When to use**: Administrators who need to quickly set up and manage contact center configuration without manual configuration steps.

### Conversation Orchestration with AI-powered playbooks (preview)

Conversation Orchestration keeps conversations actively managed throughout their lifecycle by monitoring conditions in real time and automatically applying the right actions.

**Key capabilities**:

- **Dynamic prioritization**: Automatically escalate priority based on wait time, transfer events, or other conditions
- **Overflow handling**: Route conversations to alternative resources based on agent availability
- **Intelligent routing**: Respond automatically to changing conditions without fixed rules
- **Scenario-based playbooks**: Use guided templates for common scenarios like wait time escalation and overflow

**When to use**: Supervisors and administrators who need to optimize routing efficiency, reduce wait times, and handle overflow intelligently without manual intervention.

### Related information

[Use Quality Assurance Agent](use-quality-assurance-agent.md)  
[Use Service Operations Agent](use-service-operations-agent.md)  
[Configure Conversation Orchestration](configure-conversation-orchestration.md)  