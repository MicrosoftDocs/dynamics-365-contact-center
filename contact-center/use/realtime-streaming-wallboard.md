---
title: Monitor real-time metrics in the Wallboard view
description: Learn how to use the Wallboard view in real-time streaming analytics in Dynamics 365 Contact Center to monitor real-time operational metrics, representative presence, and conversation health.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.date: 11/02/2026
ms.custom: bap-template
---

# Monitor real-time metrics in the Wallboard view

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

Use the **Wallboard** view in Dynamics 365 Contact Center to monitor operational metrics, representative presence, and conversation health in real time. The wallboard helps you monitor conversation load, queue health, representative availability, service performance, and customer wait indicators from a single screen.

In the Contact Center Supervisor app, in **Real-time streaming analytics**, select **Wallboard**. The wallboard displays metric cards and presence status information for the currently applied filters. Apply filters such as **Period**, **Channels**, **Business Unit**, and **Queues**. Learn more in [Filter options](realtime-streaming.md#filter-options).

Trend indicators show how a metric changed compared with the previous measurement interval. They update every five minutes, and the accompanying value indicates the magnitude of the change. For example, if **Abandon Rate** shows as ▲ +0.4% in red, it indicates that the abandon rate increased by 0.4 percentage points since the previous interval.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Use the wallboard for operational monitoring

Use the wallboard to:

- Monitor real-time conversation demand.
- Check queue health and customer wait conditions.
- Review workforce availability and presence distribution.
- Track response and service performance metrics.
- Identify metrics marked as critical or at risk.

> [!NOTE]
> Percentage-based metrics are calculated using data from the selected time period. The percentage is then calculated based on the conversations within that set that meet the metric outcome. For example, if you select the last 15 minutes, **Answer rate** considers only conversations offered to the queue during those 15 minutes and determines how many of them were answered. A conversation offered 30 minutes ago isn't included, even if it was answered within the last 15 minutes.

- **Active conversations**: The total number of active conversations and a split of conversation handling types. Use this metric to quickly understand how many conversations are active and how the workload is distributed between representatives and virtual agents.

- **Online Representatives**: The number of representatives who are currently online. Use this metric to compare current staffing against conversation demand.

- **Representative Presence**: The panel shows the number of representatives in each presence state.

    Presence states can include:
    - **Available**
    - **Busy**
    - **Busy - DND**
    - **Away**
    - **Offline**
    - Your custom presence statuses

    Each row displays the number for the representatives in a particular presence status. Use this panel to understand current workforce availability and identify whether representatives are available to receive more work.

- **Queue backlog**: The number of conversations that are pending assignment. Use this metric to identify queue buildup and determine whether intervention is needed.

- **Current longest wait time**: The longest time any conversation has waited in the selected queue and is still pending assignment.

- **Service level**: The percentage of conversations answered within the service-level target configured for the queue out of the total conversations offered to the queue.

    It's calculated as conversations answered within the queue's configured service-level target divided by the total conversations offered to the queue × 100. If you select multiple queues, you evaluate conversations against the service-level target configured for each queue, and aggregate the results across the selected queues. If a queue doesn't have a configured target, the default target of 20 seconds applies.

    Learn how to [define queue-specific thresholds](/dynamics365/customer-service/administer/queues-omnichannel#define-metrics-threshold-for-a-queue).

- **Abandon rate**: The percentage of conversations that customers disconnect before a representative accepts them. If a conversation is transferred from one queue to another, the abandon rate is calculated separately for each queue. Use this metric to identify potential issues with customer wait times or staffing levels that might contribute to abandoned conversations.

- **Average speed to answer**: The average time from when a conversation enters a queue until a representative accepts it. If a conversation is transferred from one queue to another, the metric is calculated separately for each queue. Use this metric to monitor how quickly representatives accept incoming customer conversations.

## Related information

[Overview of real-time streaming analytics](realtime-streaming.md)  
[Assisted Service](realtime-streaming-assisted-service.md)  
[Queues](realtime-streaming-queues.md)  
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)  
[Self-service](realtime-streaming-self-service.md#monitor-self-service-operations-in-real-time)