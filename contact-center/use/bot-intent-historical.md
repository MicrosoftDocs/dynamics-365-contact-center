---
title: View and understand real-time analytics in the Bot-Intent group report
description: Use the Bot-Intent group report to drill down into metrics by intent and representative in Dynamics 365 Contact Center, enabling better insights and operational improvements.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection:
ms.date: 12/11/2025
ms.custom: bap-template
---

# View and understand real-time analytics in the Bot-Intent report (preview)

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Supervisors can monitor historical trends across intent groups and intents for bot conversations associated with customer intent and agent interactions. The enhanced reporting delivers significant business value by providing supervisors with a dual perspective on performance through queue and intent group metrics. The integration of intent groups into analytics enables segmented analysis, that helps identify improvement opportunities across intent groups and individual intents. This comprehensive approach strengthens tracking and optimization of customer interactions, resulting in higher service quality and improved customer satisfaction. The Bot-Intent report in the Omnichannel Historical dashboard provides comprehensive insights into bot performance and customer interactions. The report supports segmented analytics by intent groups and individual intents, enabling supervisors to identify areas for improvement. 

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

You can filter this report by **Intent group**, **Duration**, **Channel**, **Queue**, **Bot Name**, **Conversation Status**, and **Time zone**.

:::image type="content" source="../media/bot-intent-dashboard.png" alt-text="Screenshot of bot-intent dashboard" lightbox="../media/bot-intent-dashboard.png":::

## Prerequisites

- You turned on the toggle for Customer Intent Agent and added the Line of business, Intent groups, and Intents. Learn more in [Customer Intent Agent](/dynamics365/contact-center/administer/manage-customer-intent-agent).
- You enabled historical analytics for intent. Learn more in [Enable real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator).

You see the report after 24 hrs of provisioning. If you don't enable Customer Intent Agent, you might still see data measures related to intent, but no conversation details appear because configuration isn't complete.

## Key metrics

|Metrics | Definition  |
|---------|---------|
|Total bot conversations| The total number of customer-initiated interactions with a Microsoft Copilot Studio bot includes conversations fully managed by the bot and those escalated to a service representative. The number of conversations deflected and escalated adds up to the total number of bot conversations. |
|Bot escalation rate | Percentage of conversations the Microsoft Copilot Studio bot escalated to a service representative out of all bot conversations. |
|Avg. escalation time (hh:mm:ss) |Average conversation duration to escalate to a service representative in hh:mm:ss format |
|Bot deflection rate |Percentage of conversations the Microsoft Copilot Studio bot deflected out of all bot conversations. Here, the conversation can either be resolved by the Microsoft Copilot Studio bot or abandoned by user before resolution. |
|Avg. deflection time (hh:mm:ss) | Average bot conversation duration that deflects within the bot in hh:mm:ss format. |
|Total bot conversations over time |The total number of customer-initiated interactions with a Copilot Studio bot includes conversations fully managed by the bot and those escalated to a service representative over selected time period.| 

## Metrics by bot

:::image type="content" source="../media/bot-intent-metrics-by-bot.png" alt-text="Screenshot of metrics by bot." lightbox="../media/bot-intent-metrics-by-bot.png":::

|Metrics | Definition  |
|---------|---------|
|Bot name | Name of all the bot / AI agents available with conversations including the intent agent.| 
|Total conversations | The total number of customer-initiated interactions with a Microsoft Copilot Studio bot includes conversations fully managed by the bot and those escalated to a service representative. The number of conversations deflected and escalated adds up to the total number of bot conversations. |
|Conversations escalated| Number of bot conversations that are escalated to representative.|  
|Bot Escalation rate  | Percentage of bot conversations that are escalated to a representative over total bot conversations. |
|Conversations deflected  | Number of bot conversations that are deflected by the AI agent either due to resolution or user abandoning the conversation.|
| Bot Deflection rate | Percentage of bot conversations that are deflected by bot over total bot conversations.  |
|Avg bot time (hh:mm:ss) | Average bot conversation duration in hh:mm:ss format that were either escalated or deflected.  |

## Metrics by intent group

|Metrics | Definition  |
|---------|---------|
|Intent Group | Name of intent group set by admin in Copilot Service admin center.|
|Total conversations| The total number of customer-initiated interactions with a Microsoft Copilot Studio bot includes conversations fully managed by the bot and those escalated to a service representative per intent group. |
|Conversations escalated | Number of bot conversations per intent group that are escalated to.|
|Bot Escalation rate  | Percentage of bot conversations that are escalated to a  representative per intent group over total bot conversations per intent group. |
|Conversations deflected  | Number of bot conversations per intent group that are deflected by the AI agent either due to resolution or user abandoning the conversation. |
| Bot Deflection rate | Percentage of bot conversations that are deflected by bot per intent group over total bot conversations per intent group. |
|Avg bot time (hh:mm:ss) | Average bot conversation duration in hh:mm:ss format that were either escalated or deflected per intent group .|

## Drill-down
 
In the **Metrics by intent group** section, select **Detailed view** to view metrics by intent.


### Metrics by intent

|Metrics | Definition  |
|---------|---------|
| Intent| | List of intents set by administrator in Copilot Service admin center.|
| Total conversations| The total number of customer-initiated interactions with a Copilot Studio bot includes conversations fully managed by the bot and those escalated to a representative per intent.|
|Conversations escalated|Number of bot conversations per intent that are escalated to representative.   |
|Bot escalation rate| Percentage of bot conversations that are escalated to a representative per intent group over total bot conversations per intent.  |
|Conversations deflected| Number of bot conversations per intent that are deflected by the AI agent either due to resolution or user abandoning the conversation. |
| Bot deflection rate|Percentage of bot conversations that are deflected by bot per intent over total bot conversations per intent group.  |
|Avg. bot time (hh:mm:ss)| Average bot conversation duration in hh:mm:ss format that were either escalated or deflected per intent .|

## Related information

[Manage real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator)    
[Overview of Omnichannel real-time analytics dashboard](/dynamics365/customer-service/use/intro-realtime-analytics-dashboard)   
[Agent group report (preview)](realtime-agent-group-report.md)
