---
title: Use real-time assisted service in real-time streaming analytics
description: Real-time assisted service gives contact center supervisors live visibility into queue backlog, service level, and abandon rate. Learn how to monitor performance.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.date: 11/04/2026
ms.topic: concept-article
ms.custom: bap-template
---

# Use real-time assisted service

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

The **Assisted service** view provides an interactive, drill-down view of contact center performance. Unlike wallboards, this view supports detailed analysis and investigation. It includes live metrics, such as current active conversations, and aggregated metrics, such as answer rate and abandon rate.

In the Contact Center Supervisor app, in **Real-time streaming analytics**, select **Assisted Service**.

Trendline indicators compare a metric with the preceding equivalent time period. For example, **Last 15 minutes** compares the metric with the previous 15 minutes. Trendline indicators appear in green, red, or gray to help supervisors quickly identify performance trends. The color of a delta is determined by the threshold configuration for the metric.

For example, **Active Conversations with Representatives** displays deltas in gray because this metric doesn't have defined out-of-the-box higher-is-better or lower-is-better thresholds. **Service Level** might display an increasing delta in green because higher values indicate better performance. **Abandon Rate** might display an increasing delta in red because lower values are preferred, making an increase an unfavorable trend.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Assisted Service capabilities

Use the Assisted service view to:

- Filter data by period, channel, business unit, and queues. Learn more in [Filter options](realtime-streaming.md#filter-options).
- Review performance funnels.
- Understand relationships between metrics.
- Investigate issues identified on the wallboard.

Select **See details** for a metric to view:

- Metric definition and calculation methodology
- Metric trends (improving or deteriorating) over the selected time period
- Threshold values (Normal, At risk, and Critical) configured for the metric

These details help supervisors understand what each metric means and how it's calculated. Visual thresholds help distinguish between healthy performance and metrics that require attention.

## Assisted Service

> [!NOTE]
> Percentage-based metrics are calculated using data from the selected time period. The percentage is then calculated based on the conversations within that set that meet the metric outcome. For example, if you select the last 15 minutes, **Answer rate** considers only conversations offered to the queue during those 15 minutes and determines how many of them were answered. A conversation offered 30 minutes ago isn't included, even if it was answered within the last 15 minutes.

Assisted service includes insights into the following areas:

### Conversation volume (Assisted and self-service)

This section provides an overview of conversation volume and shows how conversations are distributed between self-service agents and representatives. The section includes the following metrics:

- **Total conversations**: The **Total conversations** metric displays the total number of customer conversations during the selected time period. This metric includes all conversations regardless of how they're handled. The metric also shows the percentage distribution between inbound and outbound conversations.

    - Inbound: Conversations initiated by customers.
    - Outbound: Conversations initiated by representatives or automated systems.

- **Conversations offered**: The total number of conversations that entered the queue, including conversations that customers abandoned before a representative accepted them. This metric identifies how incoming conversations are distributed between self-service and assisted-service channels. Conversations are categorized as:

    - To self-service agents: Conversations initially routed to self-service automation.
    - To representatives directly: Conversations routed directly to human representatives without engaging self-service.

- **Active conversations**: The **Active conversations** metric shows the number of conversations currently in progress. This metric includes conversations that are actively being handled across all service channels. Active conversations are categorized as:

    - With self-service agents: Conversations currently being handled by automation.
    - With representatives: Conversations currently being handled by human representatives.

### Assisted Service Operations Summary

For human-assisted interactions, real-time streaming analytics provides visibility into the following metrics:

  - **Answer rate**: Percentage of conversations that representatives accept out of the conversations offered during the selected period. This rate is calculated by dividing accepted conversations by total offered conversations and multiplying by 100.

  - **Active conversations**: The total number of ongoing conversations currently being handled by self-service agents and representatives. Active conversations include all conversations currently in an active state. The representative or the self-service agent and the customer are both engaged.

  - **Representative presence**: The presence status of each representative, including Offline, Available, Away, Busy, and Busy-DND. This metric also includes any custom presence statuses configured in the system.

  - **Queue backlog**: Count of incoming conversations in Open state that are pending assignment from the queue. These incoming conversations might be directly routed to a queue, escalated from a self-service agent, transferred from another queue manually, or routed due to overflow conditions.

  - **Longest wait time**: The longest time any conversation is in the selected queue or selected set of queues and is still pending assignment. For transferred conversations, it considers conversations transferred from a source queue to the selected destination queue, and measures wait time from when the conversation entered the destination queue until the current time.

  - **Abandon rate**: Percentage of conversations disconnected by customers after queue entry but before representative acceptance, out of total queued conversations over the selected period of time. This metric also shows the count of abandoned conversations out of those that were offered to the queue.

  - **System disconnected conversations**: Conversations that the system ends automatically after queue entry but before representative assignment, due to technical, inactivity, or overflow conditions.

  - **Service level**: The percentage of conversations answered within the service-level target configured for the queue out of the total conversations offered to the queue. If no target is explicitly set, 20 seconds is treated as the default. 
  
  It's calculated as conversations answered within the queue's configured service-level target divided by the total conversations offered to the queue × 100. If you select multiple queues, you evaluate conversations against the service-level target configured for each queue, and aggregate the results across the selected queues.

  Learn how to [define queue-specific thresholds](/dynamics365/customer-service/administer/queues-omnichannel#define-metrics-threshold-for-a-queue).

  - **Average speed to answer**: Average time from when the conversation enters the queue to when a representative accepts it.

  -  **Queue transfer rate**: The percentage of conversation queue entries that resulted in a transfer to another queue, including representative-initiated transfers and transfers due to in-queue overflow.

### Overflow metrics

These metrics display information related to prequeue and in-queue overflowed conversations. They indicate the percentage of initiated callbacks that customers successfully answer. Select **See details** for the metrics to view a graphical breakdown of overflowed conversations by routing outcome, such as transfers to another queue, transfers to an external number, and conversations routed to voicemail.

  - **After-hours pre-queue overflowed conversations**: Conversations that overflowed before entering the queue because the queue was outside operating hours.

  - **Pre-queue capacity overflow rate**: Percentage of conversations that overflowed before queue entry because the existing queued conversation count exceeded the configured threshold limit.

  - **Pre-queue wait time overflow rate**: Percentage of conversations that overflowed before queue entry due to the average wait time in queue exceeding the configured threshold.

  - **In-queue wait time overflow rate**: Percentage of conversations that overflowed after entering the queue because their wait time exceeded the configured threshold.

  - **Callbacks answered**: Shows the percentage of initiated callbacks that customers answer, calculated as answered callbacks divided by the count of callbacks initiated × 100. The funnel also shows how many callbacks were offered and, of those, how many were opted in, initiated, and answered.

## Related information

[Overview of real-time streaming analytics](realtime-streaming.md)  
[Wallboard](realtime-streaming-wallboard.md)  
[Queues](realtime-streaming-queues.md)  
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)
