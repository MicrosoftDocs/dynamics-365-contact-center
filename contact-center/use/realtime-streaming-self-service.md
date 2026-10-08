---
title: Monitor self-service operations in real time (preview)
description: Use the Self Service view to monitor containment, escalation, engagement volume, language, intent, and agent performance metrics.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.date: 10/07/2026
ms.custom: bap-template
---

# Monitor self-service operations in real time (preview)

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[This article is prerelease documentation and is subject to change.]

The **Self Service** view helps supervisors monitor self-service agent performance across customer conversations. It provides visibility into containment outcomes, escalation trends, self-service engagement volumes, supported languages, customer intents, and operational health metrics.

> [!IMPORTANT]
>
> - This is a production-ready preview feature.
> - Production-ready previews are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520).

In **Real-time streaming analytics**, select the **Self Service** tab. The **Self Service** view displays operational metrics and trends related to self-service agent interactions.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

Apply filters such as **Period**, **Channel**, **Business Unit**, and **Queue**. Learn more in [Filter options](realtime-streaming.md#filter-options).

> [!NOTE]
> - Live metrics update in real time and don't use the selected **Period** filter. Only **Channel**, **Queue**, and other non-time filters are applied.
> - All non-live metrics reflect data from the time interval selected in the **Period** filter.
> - For percentage-based metrics, calculations are based only on conversations completed within the last 15 minutes. Conversations that reached the relevant outcome during that period but were completed outside the 15-minute window aren't included.

## Conversation volume split

The **Conversation volume split** section provides a high-level view of customer conversation volumes and routing distribution.

- **Total conversations**: Displays the total number of customer conversations created. The metric also breaks down conversations by:

    - **Inbound**: Conversations initiated by customers.
    - **Outbound**: Conversations initiated by the organization.

### Conversations offered

Displays the total number of conversations offered for handling. The metric distinguishes between conversations that were:

- Offered to self-service agents.
- Routed directly to customer service representatives.

### Active conversations

Displays the number of conversations currently in progress. The metric separates active conversations into:

- Conversations currently handled by self-service agents.
- Conversations currently handled by representatives.

## Self-service agent performance

The **Self-service agent performance** section provides insight into the effectiveness of self-service agents and customer outcomes.

- **Self-service agent engaged conversations**: Shows the number of conversations handled by self-service agents during the time selected in the **Period** filter. The metric includes:

    - **Active**: Conversations that a self-service agent currently handles.
    - **Completed**: Conversations that self-service successfully processes. This category includes all conversations that self-service resolves, escalates to a human representative (whether active or closed), or that the customer abandons during self-service. It also includes conversations that end due to a bot failure during the interaction.

- **Containment rate**: Shows the percentage of conversations that self-service successfully resolves without requiring escalation. The following categories provide a breakdown of completed self-service conversations:

    - **Contained**: Conversations that the self-service agent successfully resolves.
    - **Escalated**: Conversations that the self-service agent transfers to a representative.
    - **Fallback**: Conversations that the self-service agent routes through fallback handling paths.
    - **Customer abandonments**: Conversations that customers disconnect while interacting with the self-service agent before escalation to a representative.

- **Self-service engaged conversations by last language**: Shows the top 10 conversations by volume that self-service agents handle, grouped by last language. Use this metric to understand language trends and identify opportunities for multilingual optimization.

- **Self-service engaged conversations by final intents**: Shows the top 10 conversations by volume that self-service agents handle, grouped by final intents. This visualization can help identify common customer requests, high-volume support topics, and opportunities for content and intent optimization.

- **Active conversations**: Shows the number of self-service conversations that are currently in progress.

- **Average self-service agent duration**: Shows the average duration of conversations that self-service agents handle. Use this metric to understand engagement duration and identify unusually long interactions.

- **Average time to escalate**: The average time a self-service agent takes to escalate a conversation to a human representative after engaging with the customer. Lower values might indicate rapid escalation, while higher values can indicate extended self-service engagement before transfer.

- **Average time to contain**: Shows the average time a self-service agent takes to resolve a conversation, measured from the time the self-service agent becomes engaged. This metric helps evaluate containment efficiency.

## Self-service agents

The **Self-service agents** section provides performance metrics for individual self-service agents.

For each agent, the dashboard displays:

- **Self-service agent name**: Name of the self-service agent.
- **Engaged conversations**: Total conversations in which the self-service agent was engaged.
- **Active conversations**: Conversations currently being handled by the agent.
- **Escalated conversations**: Conversations transferred from the agent to a representative.
- **Escalation rate**: Percentage of engaged conversations that were escalated.
- **Average time to escalate**: Average duration before escalation occurred.
- **Contained conversations**: Conversations resolved without escalation.
- **Containment rate**: Percentage of conversations successfully contained.
- **Average time to contain**: Average duration required to resolve a conversation.
- **Average agent duration**: Average conversation duration for the agent.

Use the search box to locate a specific self-service agent and review its performance metrics.

## View detailed metrics

Select **See details** on any dashboard tile to view more information for the selected metric and investigate conversation trends in greater detail.

## Related information

[Overview of real-time streaming analytics (preview)](realtime-streaming.md)  
[Wallboard](realtime-streaming-wallboard.md)  
[Queues](realtime-streaming-queues.md)  
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)  
[Assisted service](realtime-streaming-assisted-service.md)
