---
title: Use real-time assisted service in real-time streaming analytics (preview)
description: Real-time assisted service gives contact center supervisors live visibility into queue backlog, service level, and abandon rate. Learn how to monitor performance.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.date: 06/23/2026
ms.topic: concept-article
ms.custom: bap-template
---

# Use real-time assisted service (preview)

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[This article is prerelease documentation and is subject to change.]

The **Assisted service** view provides an interactive, drill-down view of contact center performance. Unlike wallboards, this view is designed for detailed analysis and investigation. Assisted service includes both live metrics (for example, current active conversations) and aggregated metrics (for example, answer rate or abandon rate).

> [!IMPORTANT]
>
> - This is a production-ready preview feature.
> - Production-ready previews are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520).

Trendline indicators show the exact lines plotted on graph with the interval of an hour. Trendline indicators are displayed in green, red, or grey to help supervisors quickly identify performance trends. The color of a delta is determined by the threshold configuration defined for the metric. For example, Active Conversations (with Representatives) and Active Conversations (with Virtual Agents) display deltas in grey because these metrics don't have defined higher-is-better or lower-is-better thresholds. Service Level might display an increasing delta in green because higher values indicate better performance. Abandon Rate might display an increasing delta in red because lower values are preferred, making an increase an unfavorable trend.

In **Real-time streaming analytics**, select the **Assisted Service** tab.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Assisted service capabilities

Use assisted service to:

- Filter data by period, channel, and queues.
- Review performance funnels.
- Understand how metrics relate to one another.
- Investigate issues identified on the wallboard.

Select **See details** for a metric to view:

- Metric definition and calculation methodology.
- Trendlines show how metric trends (improving or deteriorating) over the selected time period.
- Threshold values (Normal, At risk, and Critical) configured for the metric.

This transparency helps supervisors understand what each metric means and how it's calculated. Visual thresholds help distinguish between healthy performance and metrics that require attention.

## Assisted service insights

Assisted service includes insights into the following areas:

### Conversation volume split

The **Total Conversations** card in this section provides breakdowns such as the total number of conversations created over the selected time period, including both inbound and outbound conversations.

### Self-serve and containment

This section contains the **Virtual Agent containment rate** metric, which displays the percentage of virtual agent-handled conversations that are fully resolved without escalation to a representative. Also, this card displays the count of contained and escalated conversations and the virtual agent duration.

  - **Average virtual agent duration**: The time taken by a virtual agent to manage a conversation, measured from when the virtual agent engages with the customer until the interaction is either resolved by the virtual agent, escalated to a representative, abandoned by the customer, or disconnected.

### Assisted service

For human-assisted interactions, real-time streaming analytics provides visibility into the following metrics:

  - **Answer rate**: Percentage of offered conversations that representatives accept during the selected period. This rate is calculated by dividing accepted conversations by total offered conversations and multiplying by 100.

  - **Active conversations**: The total number of ongoing virtual agent and representative conversations. Active conversations include all conversations currently in an active state. The representative or the virtual agent and the customer are both engaged.

  - **Abandon rate**: Percentage of conversations disconnected by customers after queue entry but before representative acceptance, out of total queued conversations over the selected period of time.

  - **Average speed to answer**: Average time from when the conversation enters the queue to when a representative accepts it.

  - **Current longest wait time**: The longest time any conversation is in the selected queue or selected set of queues and is still pending assignment. For transferred conversations, it considers conversations transferred from a source queue to the selected destination queue, and measures wait time from when the conversation entered the destination queue until the current time.

  - **Queue backlog**: Count of incoming conversations in open state that are pending assignment from the queue. These incoming conversations might be directly routed to a queue, escalated from virtual agent, transferred from another queue manually, or routed due to overflow conditions.

  - **Representative presence**: The presence status of each representative, including Offline, Available, Away, Busy, and Busy-DND. This also includes any custom presence statuses configured in the system.

  - **Service level (20s)**: Percentage of conversations accepted by representatives within 20 seconds of entering a queue.

  - **System disconnected conversations**: Conversations that the system ends automatically after queue entry but before representative assignment, due to technical, inactivity, or overflow conditions.

## Overflow metrics

These metrics display the information related to prequeue and in-queue overflowed conversations. It indicates the percentage of initiated callbacks successfully answered by customers.

  - **After-hours Pre-queue overflowed conversations**: Conversations that overflowed before entering the queue because the queue was outside operating hours.

  - **Pre-queue capacity overflow rate**: Percentage of conversations that overflowed before queue entry because the existing queued conversation count exceeded the configured threshold limit.

  - **Pre-queue wait time overflow rate**: Percentage of conversations that overflowed before queue entry due to the average wait time in queue exceeding the configured threshold.

  - **In-queue wait time overflow rate**: Percentage of conversations that overflowed after entering the queue because their wait time exceeded the configured threshold.

  - **Callbacks answered**: Shows the percentage of initiated callbacks that customers successfully answer. Calculate the percentage as the count of conversations where customers answered the callback divided by the count of callbacks initiated, multiplied by 100.

## Related information

[Overview of real-time streaming analytics (preview)](realtime-streaming.md)  
[Wallboard](realtime-streaming-wallboard.md)  
[Queues](realtime-streaming-queues.md)  
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)