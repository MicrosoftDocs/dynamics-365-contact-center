---
title: Use the Queues view to monitor queue metrics and performance
description: Use the Queues view to monitor queue health, wait times, transfers, overflows, callbacks, and representative availability.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.date: 11/02/2026
ms.custom: bap-template
---

# Monitor queue metrics and performance

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

The **Queues** view provides queue-level operational metrics grouped by business unit. Filter the view by period, channel, business unit, or queue to monitor metrics. Learn more in [Filter options](realtime-streaming.md#filter-options).

In the Contact Center Supervisor app, in **Real-time streaming analytics**, select **Queues**.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Queue health

This section displays the following metrics:

- **Queue backlog**: The number of incoming conversations in an open state that are waiting to be assigned to a representative. These conversations might come directly to a queue, or they might be escalated from a self-service agent or transferred from another queue manually or by using overflow conditions.

- **Current longest wait time**: The longest time any conversation is in the selected queue and is still pending assignment. If there are transfers, it considers conversations transferred from a source queue to the selected destination queue, and measures wait time from when the conversation entered the destination queue until the current time.

- **Abandon rate**: The percentage of incoming conversations where the customer explicitly disconnects before a representative accepts the conversation, out of all incoming conversations that entered the queue during the selected period.

  Abandon rate = (Number of conversations abandoned by the customer before representative acceptance / Total incoming conversations that entered the queue) × 100

  This metric excludes system disconnects caused by technical issues, and conversations closed because of overflow conditions.

- **Average speed to answer**: This metric is calculated as the time from when the conversation enters the queue until it's accepted by the representative, divided by the total number of conversations that were offered in the queue over the selected time period.

- **Service level**: The percentage of conversations answered within the service-level target configured for the queue out of the total conversations offered to the queue. It's calculated as conversations answered within the queue's configured service-level target divided by the total conversations offered to the queue × 100.

- **Unique inbound conversations**:  The number of customer-initiated conversations created in the system. Each conversation is counted as a unique conversation, regardless of transfers. For example, if a conversation is transferred to another queue, it's counted as one unique conversation and two conversation segments.

- **Never accepted conversations**: The number of conversations waiting for assignment in the current queue that haven't been accepted by a representative in any queue during their lifecycle.

- **Active conversations with representatives**: The number of conversations currently in progress with any representative in the queue.

- **Conversations in wrap-up**: The number of conversations currently in the wrap-up state, where the customer interaction ends and the representative completes post-interaction work before closing the session.

> [!NOTE]
> Percentage-based metrics are calculated using data from the selected time period. The percentage is then calculated based on the conversations within that set that meet the metric outcome. For example, if you select the last 15 minutes, **Answer rate** considers only conversations offered to the queue during those 15 minutes and determines how many of them were answered. A conversation offered 30 minutes ago isn't included, even if it was answered within the last 15 minutes.

## Queue-level conversation segment metrics

Use the metrics to monitor conversation and segment activity for queues. The metrics provide visibility into the current state of conversations and conversation segments, including conversations that are ongoing or in wrap-up, segments waiting in a queue, and abandoned or closed segments. A conversation segment is created when a conversation is transferred to a different queue or when a representative initiates a consult-to-queue request to seek assistance with the customer conversation.

Select **See details** on a metric to view more information.

- **Total segments**: Total conversation segments created because of queue transfers or consults initiated to a different queue.

- **Engaged segments**: The number of conversation segments accepted by representatives. This number includes segments created when conversations are transferred between queues and when consult requests are initiated to the queue.

- **Segments waiting in queue**: Includes customer-initiated conversations and consult requests that are pending assignment to a representative.

- **Abandoned segments**: The number of conversation segments where the customer disconnected before a representative accepted the conversation. This metric excludes canceled consult requests, which are included in the Unsuccessful consult segment metric.

- **Closed segments**: The number of closed conversation segments that weren't abandoned. This number includes segments closed by the system, representative, or customer after the conversation was accepted, and consult segments closed after they were accepted.

- **Unsuccessful consult segments**: Number of consult requests that were canceled, timed out, or rejected.

## Queue details table

The table provides real-time visibility into queue activity and representative availability. It displays key metrics for each queue to help you understand conversation volume, backlog, service levels, transfers, and representative presence.

Use search in the **Queues** view to find specific queues. The view includes the following metrics for each queue:

- **Queue backlog**: For this metric, see [Queue health](#queue-health).

- **Online representatives**: The number of representatives who are currently online.

- **Representative presence**: The number of representatives who are members of the queue, in different presence statuses.

- **Conversations (Answered versus Offered)**: The number of conversations answered out of the total number of conversations offered.

- **Active conversations**: The number of conversations currently in progress with any representative in the queue.

- **Average speed to answer**: For this metric, see [Queue health](#queue-health).

- **Abandon rate**: For this metric, see [Queue health](#queue-health).

- **Service level**: For this metric, see [Queue health](#queue-health).

- **Conversation transfers (In versus Out)**: A conversation transfer-in is counted when a conversation moves into the queue, from another source queue. It could be a user-initiated transfer or transferred to the queue automatically because of an overflow like the wait time in a source queue exceeded the defined threshold.

  A conversation transfer-out is counted when a conversation moves from the queue to another queue, either directly (user initiated) or because of an overflow like the wait time in the queue exceeded the defined threshold.

- **Pre-queue overflows (In versus Out)**: The number of conversations in a queue that overflowed in or out based on the following conditions:

  - **After hours pre-queue overflowed conversations:** Conversations that overflowed because the queue was outside operating hours.

  - **Pre-queue overflowed conversations due to customer count exceeding threshold**: Conversations that overflowed before queue entry because existing queued conversation count exceeded the configured threshold limit.

  - **Pre-queue overflowed conversations due to average wait time exceeding threshold**: Conversations that overflowed before queue entry due to average wait time in queue exceeding the configured threshold.

- **Callbacks**: Indicates the percentage of callbacks answered. Hover over or select the metric to view detailed callback statistics, including offered, opted-in, initiated, and answered callbacks for the queue.

- **Never accepted conversations**: For this metric, see [Queue health](#queue-health).

- **Engaged segments**: For this metric, see [Queue-level conversation segment metrics](#queue-level-conversation-segment-metrics). 

- **Closed segments**: For this metric, see [Queue-level conversation segment metrics](#queue-level-conversation-segment-metrics). 

- **Unsuccessful consult segments**: For this metric, see [Queue-level conversation segment metrics](#queue-level-conversation-segment-metrics). 

- **Conversations in wrap-up**: For this metric, see [Queue health](#queue-health).

- **Abandoned segments**: For this metric, see [Queue-level conversation segment metrics](#queue-level-conversation-segment-metrics).

## Related information

[Overview of real-time streaming analytics](realtime-streaming.md)  
[Wallboard](realtime-streaming-wallboard.md)  
[Assisted Service](realtime-streaming-assisted-service.md)   
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)  
[Self-service](realtime-streaming-self-service.md#monitor-self-service-operations-in-real-time)