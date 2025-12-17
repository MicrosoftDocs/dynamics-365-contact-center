---
title: View and understand real-time analytics in the User group report
description: Learn how to filter and analyze real-time metrics in the User group report in Dynamics 365 Contact Center to identify trends and improve agent and customer outcomes.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection:
ms.date: 12/17/2025
ms.custom: bap-template
---

# View and understand real-time analytics in the User group report (preview)

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Contact centers often group service representatives into dedicated teams focused on specific intents or clusters of related intents. Real-time analytics use these groupings to monitor conversations, track metrics, and surface actionable insights. Filtering by agent group enables supervisors to quickly identify trends, assess team performance, and resolve issues faster. This structured approach ensures customer needs are addressed correctly, driving operational efficiency, improving service quality, and enhancing customer satisfaction.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

You can filter this report by **Time**, **Channel**, **Line of Business**, **Intent group**, **Agent group**, **Time zone**, and **Conversation status**.

As part of visual customization, all real-time dashboards including **Summary**, **Voice**, **Bot**, **Agent**, **Ongoing Conversation**, and **Backlog conversation** reports can be filtered by intent group, intent, and line of business by using the **IntentFamilyName** in **DimIntent** dimension. Learn more in [visual customization](/dynamics365/customer-service/use/customize-reports). You can search for the data measures for intent to select specific intent-based filters.

:::image type="content" source="../media/realtime-user-group.png" alt-text="Screenshot of omnichannel realtime user group report." lightbox="../media/realtime-user-group.png":::

## Prerequisites

- You turned on the toggle for Customer Intent Agent and added the Line of business, Intent groups, and Intents. Learn more in [Customer Intent Agent](/dynamics365/contact-center/administer/manage-customer-intent-agent).
- You enabled real-time analytics for intent. Learn more in [Enable real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator).

You see the report after 24 hrs of provisioning. If you don't enable Customer Intent Agent, you might still see data measures related to intent, but no conversation details appear because configuration isn't complete.

## Metrics

|Metrics | Definition  |
|---------|---------|
|Conversations in queue    |    Conversations currently waiting in queue to be assigned to a customer service representative (service representative or representative).     |
|Agents online     |     Number of logged in representatives.|
|Agents in active conversations    |    Representatives currently handling live conversations in progress and not yet closed excluding wrap-up state. |
|Agents in wrap-up conversations    |   Service representatives who finished interacting with the customer but are still completing post-conversation tasks before closing the session. |
| Average  session handle time | Session handle time is the total time a representative spends working on a customer session, including the live interaction and any follow-up or wrap-up activities. Average Session Handle Time = Total handle time across sessions / Number of sessions handled. |
|Session timeout rate    |  Percentage of incoming sessions that the representative didn't respond to before the system's timeout threshold over the total number of assigned sessions. Session Timeout Rate (%) = (Number of timed-out sessions / Total assigned sessions) × 100. |
|Session rejection rate     |  Percentage of sessions rejected by representatives over the total number of sessions assigned to representatives. Session Rejection Rate (%)= (Number of sessions rejected by agents / Total number of sessions assigned to agents) × 100. |

## Metrics by Agent group

|Metrics | Definition  |
|---------|---------|
|Agent group name | Name of the service representative group. |
|Conversations in queue| Number of conversations waiting in queue to be assigned to a service representative per user group.|
|Longest wait time (hh:mm:ss)|	Waiting time until the service representative accepts the conversation per user group.|
|Agents online|	Number of  representatives that are currently online based on the time slicer per user group. |
|Agents available|	Number of representatives who are in the **Available** status per user group.|
|Agents in wrap-up conversations| Representatives who finished interacting with the customer but are still completing post-conversation tasks before closing the session per user group. |
|Average handle time (hh:mm:ss)|	Total handle time divided by the number of conversations handled. <br> - For Voice: msdyn_sessionparticipant.msdyn_talktime + msdyn_sessionparticipant.msdyn_holdtime + msdyn_sessionparticipant.msdyn_activewrapuptime. <br> - For Chat: msdyn_sessionparticipant.msdyn_activetime + msdyn_sessionparticipant.msdyn_activewrapuptime|

## Drilldown

In the **Metrics by agent** section, select **Detailed view** to view metrics by agent.

:::image type="content" source="../media/realtime-user-group-drilldown.png" alt-text="Screenshot of realtime user group drilldown.":::

|Metrics | Definition  |
|---------|---------|
|Conversations in queue|	Number of conversations waiting in queue to be assigned to a service representative.|
|Agents online|	Number of representatives currently online based on the time slicer. |
|Agents in active conversations|Representatives actively engaged in live conversations that are still open, excluding those in wrap-up state.|
|Average handle time|	Total handle time divided by the number of conversations handled. <br> - For Voice: msdyn_sessionparticipant.msdyn_talktime + msdyn_sessionparticipant.msdyn_holdtime + msdyn_sessionparticipant.msdyn_activewrapuptime. <br> - For Chat: msdyn_sessionparticipant.msdyn_activetime + msdyn_sessionparticipant.msdyn_activewrapuptime|
|Agents availability status|	Representatives based on their current availability status.|
|Agents in wrap-up conversations| Representatives who finished interacting with the customer but are still completing post-conversation tasks before closing the session per user group.|
|Session timeout rate|	Percentage of incoming sessions that the representative didn't respond to before the system's timeout threshold over the total number of assigned sessions. Session Timeout Rate (%) = (Number of timed-out sessions/Total assigned sessions) × 100. |
|Session rejection rate| Percentage of sessions rejected by representatives over the total number of sessions assigned to representatives. Session Rejection Rate (%)= (Number of sessions rejected by agents / Total number of sessions assigned to agents) × 100.|


### Metrics by user group

|Metrics | Definition  |
|---------|---------|
|User group name|	Name of the service representative group.|
|Conversation status|	Current status of service representative.|
|Time in presence (hh:mm:ss)|	The duration for which the service representative is in the current status.|
|Active sessions|	Number of sessions that are currently in **Active** status.|
|Closed sessions|	Number of sessions that are currently in **Closed** status.|
|Rejected sessions| Sessions rejected represent the total number of conversation sessions declined by the service representative.|
|Sessions timed out| A session times out if the representative doesn't respond within the allotted time, and the system automatically closes it.|
|Average session handle time (hh:mm:ss)|	Average Session Handle Time = Total handle time across sessions / Number of sessions handled. This metric is tracked per representative and session.|

 
## Related information

[Manage real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator)    
[Overview of Omnichannel real-time analytics dashboard](/dynamics365/customer-service/use/intro-realtime-analytics-dashboard)     
[Intent group report (preview)](realtime-intent-group-report.md)
