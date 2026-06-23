---
title: Use the Queues view to monitor queue metrics and performance (preview)
description: Monitor queue metrics with the Queues view in Dynamics 365 Contact Center. Filter by time, channel, and queue to track queue health and performance.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.date: 06/23/2026
ms.custom: bap-template
---

# Monitor queue metrics and performance (preview)

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[This article is prerelease documentation and is subject to change.]

The **Queues** view provides queue-level operational visibility grouped by business units. You can filter by period, channel, and queue. For each queue, supervisors can access queue health by viewing metrics such as **Queue backlog**, **Current longest wait time**, **Abandon rate**, and **Average speed to answer**.

In **Real-time streaming analytics**, select the **Queues** tab.

> [!IMPORTANT]
>
> - This is a production-ready preview feature.
> - Production-ready previews are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520).
> - Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Queue details

In **Queues**, use the search functionality to find specific queues and business units. You can view the following details:

  - **Average speed to answer**: This metric is calculated as the time from when the conversation enters the queue until it's assigned to and accepted by the representative, divided by the total number of conversations that were accepted over the selected time period.

  - **Abandon rate**: Abandon rate is the percentage of incoming conversations in which the customer explicitly disconnected before the conversation is accepted by a representative, out of the total number of incoming conversations that entered the queue during the selected period.

    Abandon rate = (Number of conversations abandoned by the customer before representative acceptance / Total incoming conversations that entered the queue) × 100
     
    This metric excludes system disconnects caused by technical issues, and conversations closed because of overflow conditions.

  - **Callbacks**: Indicates the percentage of callbacks answered. Hover over or click the metric to view detailed callback statistics, including offered, opted-in, initiated, and answered callbacks for the queue.

  - **Conversation transfers (In versus Out)**: A conversation transfer is counted as inbound when a conversation moves into the queue, either manually from another source queue (user initiated) or automatically because of an overflow like the wait time in a source queue exceeds the defined threshold.

    A conversation transfer is counted as outbound when a conversation moves from the queue to another queue, either directly (user initiated) or because of an overflow like the wait time in the queue exceeds the defined threshold.
  
  - **Conversations (Answered versus Offered)**: The number of conversations answered out of the total number of conversations offered.

  - **Longest wait time**: The longest time any conversation is in the selected queue and is still pending assignment. If there are transfers, it considers conversations transferred from a source queue to the selected destination queue, and measures wait time from when the conversation entered the destination queue until the current time.

  - **Online representatives**: The number of representatives who are currently online.

  - **Pre-queue overflows (In versus Out)**: The number of conversations in a queue that overflowed in or out based on the following conditions.

      - **After hours pre-queue overflowed conversations:** Conversations that overflowed because the queue was outside operating hours.

      - **Pre-queue overflowed conversations due to customer count exceeding threshold**: Conversations that overflowed before queue entry because existing queued conversation count exceeded the configured threshold limit.

      - **Pre-queue overflowed conversations due to average wait time exceeding threshold**: Conversations that overflowed before queue entry due to average wait time in queue exceeding the configured threshold.

  -  **Queue backlog**: Count of incoming conversations in an open state that are waiting to be assigned to a representative. These conversations might come directly to a queue, or they might be escalated from a virtual agent or transferred from another queue manually or by using overflow conditions.

  - **Representative presence**: The presence status of the representatives who are members of the queue. Select **See more** to view the full list of presence statuses and the number of representatives in each status.

  - **Service level (20s)**: Percentage of conversations accepted within the threshold of 20 seconds of entering the queue, out of total conversations accepted by a human representative. Conversations answered by virtual agents aren't included in this metric.

## Related information

[Overview of real-time streaming analytics (preview)](realtime-streaming.md)  
[Wallboard](realtime-streaming-wallboard.md)  
[Assisted Service](realtime-streaming-assisted-service.md)   
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)
