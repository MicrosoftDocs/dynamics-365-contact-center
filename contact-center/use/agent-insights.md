---
title: View Agent insights dashboard (preview)
description: Know how the Agent insights dashboard can help you, as a supervisor, monitor the performance of the autonomous agents in Dynamics 365 Contact Center and Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot 
ms.date: 08/01/2025
ms.custom: bap-template
---

# View Agent insights dashboard (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Autonomous agents are intelligent tools designed to enhance customer service efficiency in Dynamics 365 Contact Center and Dynamics 365 Customer Service. With generative AI, they improve customer intent discovery and real-time knowledge management and support self-service and assisted scenarios.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## View the Agent insights dashboard

The Agent insights dashboard provides insights into the performance of the autonomous agents, allowing you to monitor their effectiveness and make data-driven decisions to optimize their use.

The dashboard capabilities include:

- **Filters**: Specify the exact segment of traffic to gather insights through the line of business, intent group, and channel filters.
- **Conversation and Case pivot**: Pivot between the conversation and case view to gain insights into the complete program picture.
- **Top KPIs**: Gain insights into autonomous agents and customer service representatives' (service representatives or representatives) performance through metrics such as total volume and average handling time.
- **AI agent-level insights**: Quickly assess the impact the AI agents are driving for the organization and the areas of opportunity for improvement.
- **Volume breakdown**: View the volume breakdown by line of business, intent group, or channels to identify the top volume drivers and their autonomous rate per grouping if applicable.
- **Volume funnel**: View and analyze the path of conversations or cases to identify the share of engagements that are escalated to service representatives.

## Conversation performance

The Conversation performance report displays information on the conversations serviced by autonomous agents. The following metrics are available.

### Top KPIs for conversations

The following metrics are available.

| Metric                   | Definition                                                                                                         |
|--------------------------|--------------------------------------------------------------------------------------------------------------------|
| Total conversations      | Total conversations conducted with representatives or AI agents.                                                   |
| Autonomous rate          | The percentage of conversations that were engaged by AI agents only and weren't routed to a representative.        |
| Average handle time      | The time spent from conversation assignment to conversation close including representative and AI agent conversations. |
| Ongoing conversations    | Total conversations that are currently in active or open state for both representatives and AI agents.              |
| Abandon rate             | Total conversations where the conversation is abandoned and not handled or resolved by an AI agent or service representative. |
| Unassigned conversations | Total conversations that are awaiting in the queue to be assigned to a service representative.                      |

## Case performance

The Case performance report displays information on the cases serviced by autonomous agents.

### Top KPIs for cases

The following metrics are available.

| Metric                | Definition                                                                                                                |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------|
| Active cases          | Total number of cases that are active in real time.                                                                       |
| Unassigned cases      | Total cases awaiting representative assignment (no case owner assigned).                                                   |
| Incoming cases        | Total cases created during the selected period.                                                                   |
| Days to close         | Average number of days to close a case for all cases created during the selected period (date closed minus date created). |
| Cases followed up     | Total cases that are followed up by either service representative or AI agent (status is set to **Waiting for details**).                              |

## Summary of AI agents performance

The following metrics are available.

| Autonomous agent| Metric  | Definition    |
|-----------------|-------|-----------------|
| Customer Intent Agent |                 | |
| | Engagement count                      | Total number of conversations where Customer Intent Agent is engaged. |
| | Solutions attempted (assisted service)| Total number of conversations where a solution was identified for the intent and attempted to use to resolve the conversation (knowledge article, action taken, custom agent).<br> **NOTE**: In preview, this feature isn't available for IVR or voice agents. |
| |Autonomous resolutions                 | Total number of conversations that were completed without requiring a service representative to be assigned (handled autonomously by Customer Intent Agent). |
| Case Management Agent |                 | |
| | Autonomous case processing volume     | Number of cases with autonomous actions to assist in processing the case. |
| | Autonomous case enrichment volume     | Number of cases that were enriched autonomously by the Case Management Agent. |
| | Emails sent or drafted by AI agent    | Number of emails sent by the Case Management Agent, including fully autonomous and human-approved emails. |
| Customer Knowledge Management Agent |   | |
| | Total evaluations performed           | Total number of evaluations performed across cases and conversations. |
| | AI Agent articles drafted       | Number of articles drafted by AI agent.|
| | Autonomously generated articles published | Number of articles that were autonomously published for AI agent or service representatives use. |

### Related information

[Use Case Management Agent to create and update cases (preview)](/dynamics365/customer-service/use/use-case-creation-agent)  
[Use knowledge insights for Customer Knowledge Management Agent (preview)](/dynamics365/customer-service/use/admin-km-agent-insights)  