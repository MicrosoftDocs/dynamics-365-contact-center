---
title: Monitor self-service operations in real time
description: Use the Self Service view to monitor containment, escalation, engagement volume, language, intent, and agent performance metrics.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.date: 11/04/2026
ms.custom: bap-template
---

# Monitor self-service operations in real time

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

The **Self Service** view helps supervisors monitor self-service agent performance across customer conversations. It provides visibility into containment outcomes, escalation trends, self-service engagement volumes, supported languages, customer intents, and operational health metrics.

In the Contact Center Supervisor app, in **Real-time streaming analytics**, select **Self Service**. The **Self Service** view appears, which displays operational metrics and trends related to self-service agent interactions.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

Apply filters such as **Period**, **Channel**, **Business Unit**, and **Queue**. Learn more in [Filter options](realtime-streaming.md#filter-options).

> [!NOTE]
> - Live metrics update in real time and don't use the selected **Period** filter. Only **Channel**, **Queue**, and other non-time filters are applied.
> - All non-live metrics reflect data from the time interval selected in the **Period** filter.
> - For percentage-based metrics, the selected time period determines the set of conversations used to calculate the metric. The percentage is then calculated based on the conversations within that set that meet the metric outcome. For example, if you select the last 15 minutes, Answer rate considers only conversations offered to the queue during those 15 minutes and determines how many of them were answered. A conversation offered 30 minutes ago isn't included, even if it was answered within the last 15 minutes.

## Conversation Volume (Assisted Service and Self-Service)

The **Conversation volume split** section provides a high-level view of customer conversation volumes and routing distribution.

- **Total conversations**: Shows the total number of customer conversations created. The metric also breaks down conversations by:

    - **Inbound**: Conversations initiated by customers.
    - **Outbound**: Conversations initiated by the organization.

- **Conversations offered**: The total number of conversations that entered the queue, including conversations that customers abandoned before a representative accepted them. This metric identifies how incoming conversations are distributed between self-service and assisted-service channels. Conversations are categorized as:

    - To self-service agents: Conversations initially routed to self-service automation.
    - To representatives directly: Conversations routed directly to human representatives without engaging self-service.

- **Active conversations**: Shows the number of conversations currently in progress. The metric separates active conversations into:

    - Conversations currently handled by self-service agents
    - Conversations currently handled by representatives

## Self-service agent performance

The **Self-service agent performance** section provides insight into the effectiveness of self-service agents and customer outcomes.

- **Self-service agent engaged conversations**: Shows the number of conversations handled by self-service agents during the time selected in the **Period** filter. The metric includes:

    - **Active**: Conversations that a self-service agent is currently handling.
    - **Completed**: Conversations that self-service processed. This category includes all conversations that a self-service agent resolved, escalated to a human representative (whether active or closed), or that the customer abandoned during self-service. It also includes conversations that ended due to a self-service agent failure during the interaction.

- **Containment rate**: Shows the percentage of conversations that a self-service agent resolved without requiring escalation. The following categories provide a breakdown of completed self-service conversations:

    - **Contained**: Conversations that the self-service agent resolved.
    - **Escalated**: Conversations that the self-service agent transferred to a representative.
    - **Fallback**: Conversations that the self-service agent routed through fallback handling paths.

- **Self-service agent engaged conversations by last language**: Shows the top 10 conversations by volume that self-service agents handle, grouped by last language. Use this metric to understand language trends and identify opportunities for multilingual optimization.

- **Self-service agent engaged conversations by final intents**: Shows the top 10 conversations by volume that self-service agents handle, grouped by final intent. This visualization can help identify common customer requests, high-volume support topics, and opportunities for content and intent optimization.

- **Self-service agent active conversations**: Shows the number of self-service agent conversations that are currently in progress.

- **Average self-service agent duration**: Shows the average duration of conversations that self-service agents handle. Use this metric to understand engagement duration and identify unusually long interactions.

- **Average time to escalate**: The average time a self-service agent takes to escalate a conversation to a human representative after engaging with the customer. Lower values might indicate rapid escalation, while higher values might indicate extended self-service engagement before transfer.

- **Average time to contain**: Shows the average time a self-service agent takes to resolve a conversation, measured from the time the self-service agent becomes engaged. This metric helps evaluate containment efficiency.

## Self-service agents

The **Self-service agents** section provides performance metrics for individual self-service agents.

For each agent, the view displays:

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

Select **See details** on any tile to view more information for the selected metric and investigate conversation trends in greater detail.

## Related information

[Overview of real-time streaming analytics](realtime-streaming.md)  
[Wallboard](realtime-streaming-wallboard.md)  
[Queues](realtime-streaming-queues.md)  
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)  
[Assisted service](realtime-streaming-assisted-service.md)
