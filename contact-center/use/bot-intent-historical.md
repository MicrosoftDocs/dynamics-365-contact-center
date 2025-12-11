---
title: View and understand real-time analytics in the Bot-Intent group report
description: Use the Intent group report to drill down into metrics by intent and representative in Dynamics 365 Contact Center, enabling better insights and operational improvements.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection:
ms.date: 11/21/2025
ms.custom: bap-template
---

# View and understand real-time analytics in the Bot-Intent report (preview)

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

As a supervisor, organizing contact center data by intent, intent groups, and line of business lets you monitor conversations and track metrics effectively. Real-time analytics powered by these attributes provide immediate insights into customer behavior, helping identify trends, optimize agent performance, and resolve queries faster. This structured approach improves service quality and operational efficiency, driving higher customer satisfaction.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]


You can filter this report by **Time**, **Channel**, **Line of Business**, **Intent group**, **Agent group**, **Time zone**, and **Conversation status**.

As part of visual customization, all real-time dashboards including **Summary**, **Voice**, **Bot**, **Agent**, **Ongoing Conversation**, and **Backlog conversation** reports can be filtered by intent group, intent, and line of business by using the **IntentFamilyName** in **DimIntent** dimension. Learn more in [visual customization](/dynamics365/customer-service/use/customize-reports). You can search for the data measures for intent to select specific intent-based filters.

## Prerequisites

- You turned on the toggle for Customer Intent Agent and added the Line of business, Intent groups, and Intents. Learn more in [Customer Intent Agent](/dynamics365/contact-center/administer/manage-customer-intent-agent).
- You enabled real-time analytics for intent. Learn more in [Enable real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator).

You see the report after 24 hrs of provisioning. If you don't enable Customer Intent Agent, you might still see data measures related to intent, but no conversation details appear because configuration isn't complete.

## Metrics by Intent group

|Metrics | Definition  |
|---------|---------|
|Intent Group Name|	Name of intent group set by the administrator in Customer Service admin center.|
|Conversations in queue|	Conversations per intent group currently waiting in queue to be assigned to a service representative.|
|Longest wait time (hh:mm:ss)|	Waiting time until the service representative accepts the conversation per intent group.|
|Abandoned rate| The percentage of incoming conversations that end before engagement by a representative or AI agent, calculated over the total number of incoming conversations per intent group. Includes: <br> - Customer exits before assignment. <br> - Customer disconnects after assignment but before representative acceptance.|
|Agents online|	Number of representatives currently online based on the time slicer per intent group.|
|Agents available|	Service representatives who are currently in **Available** status per intent group.|
|Agents in wrap-up conversations|	Service representatives who finished interacting with the customer but are still completing post-conversation tasks before closing the session per intent group.|
|Average handle time (hh:mm:ss)|	Total handle time divided by the number of conversations handled per intent group. <br> - For Voice: msdyn_sessionparticipant.msdyn_talktime + msdyn_sessionparticipant.msdyn_holdtime + msdyn_sessionparticipant.msdyn_activewrapuptime <br> - For Chat: msdyn_sessionparticipant.msdyn_activetime + msdyn_sessionparticipant.msdyn_activewrapuptime.|


## Drill-down 

In the **Metrics by intent** section, select **Detailed view** to view metrics by intent.

|Metrics | Definition  |
|---------|---------|
|Engaged conversations|	Conversations offered and accepted by the service representative.|
|Average handle time|	Total handle time divided by the number of conversations handled. <br> - For Voice: msdyn_sessionparticipant.msdyn_talktime + msdyn_sessionparticipant.msdyn_holdtime + msdyn_sessionparticipant.msdyn_activewrapuptime. <br>- For Chat: msdyn_sessionparticipant.msdyn_activetime + msdyn_sessionparticipant.msdyn_activewrapuptime.|
|Agents online|	Number of representatives currently online based on the time slicer.|
|Abandoned rate| The percentage of incoming conversations that end before engagement by a representative or AI agent, calculated over the total number of incoming conversations per intent group. Includes: <br> - Customer exits before assignment. <br> - Customer disconnects after assignment but before representative acceptance.|
|Transfer rate|	Total number of incoming sessions transferred from one representative, agent, or queue to another during the conversation, over the total number of incoming sessions.|


### Metrics by intent

|Metrics | Definition  |
|---------|---------|
|Intent Name|	Name of the intent set in in Customer Service admin center.|
|Engaged conversations|	Conversations offered and accepted by the service representative per intent.|
|Average handle time (hh:mm:ss)|	Total handle time divided by the number of conversations handled per intent. <br> - For Voice: msdyn_sessionparticipant.msdyn_talktime + msdyn_sessionparticipant.msdyn_holdtime + msdyn_sessionparticipant.msdyn_activewrapuptime. <br> - For Chat: msdyn_sessionparticipant.msdyn_activetime + msdyn_sessionparticipant.msdyn_activewrapuptime.|
|Abandoned rate|	The percentage of incoming conversations that end before engagement by a representative or AI agent, calculated over the total number of incoming conversations per intent group. Includes: <br> - Customer exits before assignment. <br> - Customer disconnects after assignment but before representative acceptance.|
|Session transfer rate|	Total number of incoming sessions transferred from one representative, agent, or queue to another during the conversation, over the total number of incoming sessions per intent.|


## Related information

[Manage real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator)    
[Overview of Omnichannel real-time analytics dashboard](/dynamics365/customer-service/use/intro-realtime-analytics-dashboard)   
[Agent group report (preview)](realtime-agent-group-report.md)
