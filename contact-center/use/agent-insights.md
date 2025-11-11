---
title: View Agent insights dashboard
description: Know how the Agent insights dashboard can help you, as a supervisor, monitor the performance of the autonomous agents in Dynamics 365 Contact Center and Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot 
ms.date: 11/14/2025
ms.custom: bap-template
---

# View Agent insights dashboard

Autonomous agents are intelligent tools designed to enhance customer service efficiency in Dynamics 365 Contact Center and Dynamics 365 Customer Service. With generative AI, they improve customer intent discovery and real-time knowledge management and support self-service and assisted scenarios.

## Prerequisite

Administrator enabled the [Agent insights dashboard](../administer/enable-agent-insights.md).

## Use the Agent insights dashboard

The Agent insights dashboard equips supervisors with real-time visibility into key performance indicators and operational trends regarding their AI agents, enabling confident, data-driven decision making throughout their autonomous transformation journey.

The dashboard capabilities include:

- **Filters**: Specify the exact segment of traffic to gather insights through the line of business, intent group, and channel filters.
- **Conversation and Case pivot**: Pivot between the conversation and case view to gain insights into the complete program picture.
- **Top KPIs**: Gain insights into autonomous agents and customer service representatives' (service representatives or representatives) performance through metrics such as total volume, autonomous rate, and quality score.
- **Goal setting capabilities for top KPIs**: Define goals for your top KPIs across your organization.
- **AI agent-level insights**: Quickly assess the impact the AI agents are driving for the organization and the areas of opportunity for improvement with easy access to deeper-level insights.
- **Volume breakdown**: View the volume breakdown by line of business, intent group, or channels to identify the top volume drivers and their autonomous rate per grouping if applicable.
- **Volume funnel**: View and analyze the path of conversations or cases to identify the share of engagements that are escalated to service representatives.

For granular insights, select the links to the real-time and historical analytics reports available on the dashboard.

## Conversation performance

The Conversation performance report displays information on the conversations serviced by autonomous agents.

:::image type="content" source="../media/agent-insights-conversations-performance.png" alt-text="Screenshot of conversations performance pivot." lightbox="../media/agent-insights-conversations-performance.png":::

### Top KPIs for conversations

The following metrics are available.

| Metric                   | Definition                                                                                                         |
|--------------------------|--------------------------------------------------------------------------------------------------------------------|
| Active conversations     | Total number of conversations that are active.                                                   |
| Closed conversations     | Total number of conversations that were closed or abandoned. |
| Autonomous rate          | The percentage of conversations that were engaged by AI agents only and weren't routed to a representative.        |
| Quality score            | Score that evaluates how well a conversation met defined quality standards.|
| Sentiment score          | Machine learning generated customer sentiment of the communication between the user and the customer. | 

## Case performance

The Case performance report displays information on the cases serviced by autonomous agents.

:::image type="content" source="../media/agent-insights-cases-performance.png" alt-text="Screenshot of cases performance pivot." lightbox="../media/agent-insights-cases-performance.png":::

### Top KPIs for cases

The following metrics are available.

| Metric                | Definition                                                                                                                |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------|
| Active cases          | Total number of cases that are active in real time.                                                                       |
| Closed cases          | Total number of cases that were closed or abandoned |
| Quality score         | Score that evaluates how well a case met defined quality standards. |
| Days to close         | Average number of days spent from case creation to case closure. |

## Summary of AI agents performance

The following metrics are available.

| Autonomous agent| Metric  | Definition    |
|-----------------|-------|-----------------|
| Customer Intent Agent |                 | |
| | Conversation count                    | The total number of conversations that the Customer Intent Agent was automatically connected to or added to after the conversation started. |
| | Solutions generated by AI             | The total number of solutions generated by AI at the request of a service representative.|
| | Conversations closed by AI | The total number of conversations that were resolved or abandoned without being transferred to a service representative. |
| Case Management Agent |                 | |
| | Cases processed by AI     | The number of cases handled without being transferred to a service representative. |
| | Cases enriched by AI     | Number of cases that were enriched autonomously by the Case Management Agent. |
| | Emails sent or drafted by AI agent    | The number of emails sent or drafted autonomously or with AI assistance. |
| Quality Evaluation Agent    | | |
| | Quality evaluations                    | Total number of evaluations where evaluations were performed. |
|| Quality score                            | Score that indicates how well the defined quality standards were met. |
|| Evaluations below quality thresholds     | Number of evaluations below the target evaluation threshold.|
| Customer Knowledge Management Agent |   | |
| | Knowledge evaluations          | The total number of cases or conversations evaluated for knowledge creation and/or updates. |
| | Articles drafted by AI       | The total number of knowledge articles drafted autonomously or with human review.|
| | Articles published by AI | The total number of knowledge articles published autonomously. |

## FAQ

### How can I set goals for my top KPIs?

Learn how to set goals in [Configure KPI goals](../administer/enable-agent-insights.md#configure-kpi-goals)

### Can I use this dashboard when some AI agents only are enabled?

Yes, the dashboard dynamically displays metrics for those AI agents only that're enabled.

### I don't see insights for a case or conversation pivot or line of business?

The dashboard displays insights for enabled AI agents only. Currently, insights for line of business and intent level aren't available.

### Related information

[Use Case Management Agent to create and update cases (preview)](/dynamics365/customer-service/use/use-case-creation-agent)  
[Use knowledge insights for Customer Knowledge Management Agent (preview)](/dynamics365/customer-service/use/admin-km-agent-insights)  