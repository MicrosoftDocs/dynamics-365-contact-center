---
title: Monitor real-time metrics in the Wallboard view (preview)
description: Learn how to use the Wallboard view in real-time streaming analytics in Dynamics 365 Contact Center to monitor real-time operational metrics, representative presence, and conversation health.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.date: 06/23/2026
ms.custom: bap-template
---

# Monitor real-time metrics in the Wallboard view (preview)

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[This article is prerelease documentation and is subject to change.]

The **Wallboard** view in **Real-time streaming analytics** provides a consolidated, real-time view of operational metrics for supervisors and managers. The wallboard helps monitor conversation load, queue health, representative availability, service performance, and customer wait indicators from a single screen.

> [!IMPORTANT]
>
> - This is a production-ready preview feature.
> - Production-ready previews are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520).

Apply filters such as **Period**, **Channels**, and **Queues**. The **Period** filter applies only to aggregated metrics. Live metrics aren't affected by time-based filters and update only based on channel, queue, and other non-time filters.

Trend indicators show how a metric has changed compared to the previous measurement interval. They update every five minutes, and the accompanying value indicates the magnitude of the change. For example, If Abandon Rate shows as ▲ +0.4% in red, it indicates that the abandon rate has increased by 0.4 percentage points since the previous interval.

In **Real-time streaming analytics**, select the **Wallboard** tab. Use **Filter** to refine the data shown on the wallboard. The wallboard displays metric cards and presence information for the currently applied filters.

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

## Monitor active conversation volume

The **Active conversations** card shows the total number of active conversations and a split of conversation handling types. Use this card to quickly understand how many conversations are active and how the workload is distributed between representatives and virtual agents.

## Check online representative count

The **Online Representatives** card shows the number of representatives who are currently online. Use this card to compare current staffing against conversation demand.

## Review representative presence

The **Representative Presence** panel shows the number of representatives in each presence state.

Presence states can include:

- **Available**
- **Busy**
- **Busy - DND**
- **Away**
- **Offline**
- Your custom presence statuses

Each row displays the count for the representatives in a particular presence status. Use this panel to understand current workforce availability and identify whether representatives are available to receive more work.

## Track conversations waiting in queue

The **Queue backlog** card shows the number of conversations that are pending assignment. Use this card to identify queue buildup and determine whether intervention is needed.

## Review the current longest wait time

The **Current longest wait time** card shows the longest time any conversation has waited in the selected queue and is still pending assignment.

## Monitor service level

The **Service level** card shows the percentage of conversations answered within 20 seconds. Use this card to track whether the operation is meeting its response target.

## Monitor abandon rate

The **Abandon rate** card shows the percentage of customers who abandoned conversations before being answered. Use this metric to identify whether customer wait times or staffing levels are contributing to lost conversations.

## Track average speed to answer

The **Avg. Speed to answer** card shows the average time taken to answer incoming conversations. Use this card to assess how quickly the system or representatives answer incoming customer conversations.

## Related information

[Overview of real-time streaming analytics (preview)](realtime-streaming.md)  
[Assisted Service](realtime-streaming-assisted-service.md)  
[Queues](realtime-streaming-queues.md)  
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)