---
title: Bot-Intent dashboard
description: Leverage the Bot-Intent dashboard to identify patterns in bot interactions and refine your customer service strategies in Dynamics 365 Contact Center.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection:
ms.date: 12/16/2025
ms.custom: bap-template
---

# Bot-Intent dashboard (preview)

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

The Bot-Intent dashboard provides detailed insights about bot performance and customer engagement, supporting targeted analytics for continuous improvement. Supervisors can track historical trends in bot conversations and agent interactions by analyzing intent groups and individual intents. 

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

You can filter this dashboard by **Intent group**, **Duration**, **Channel**, **Queue**, **Bot Name**, **Conversation Status**, and **Time zone**.

:::image type="content" source="../media/bot-intent-dashboard.png" alt-text="Screenshot of bot-intent dashboard" lightbox="../media/bot-intent-dashboard.png":::

## Prerequisites

- You turned on the toggle for Customer Intent Agent and added the Line of business, Intent groups, and Intents. Learn more in [Customer Intent Agent](/dynamics365/contact-center/administer/manage-customer-intent-agent).
- You enabled historical analytics for intent. Learn more in [Enable historical analytics for intent](dynamics365/customer-service/administer/oc-historical-analytics-reports#enable-historical-analytics-for-intent).

You see the dashboard after 24 hours of provisioning. If you don't enable Customer Intent Agent, you might still see data measures related to intent, but no conversation details appear because the configuration isn't complete.

## Key metrics

|Metrics | Definition  |
|---------|---------|
|Total bot conversations| The total number of customer-initiated interactions with a Copilot Studio bot. Includes conversations fully managed by the bot and those escalated to a service representative. The total includes both deflected and escalated conversations. |
|Bot escalation rate | Percentage of conversations the Copilot Studio bot escalated to a service representative out of all bot conversations. |
|Avg. escalation time (hh:mm:ss) |Average conversation duration to escalate to a service representative in hh:mm:ss format. |
|Bot deflection rate |Percentage of conversations the Copilot Studio bot deflected out of all bot conversations. Here, the conversation can either be resolved by the Copilot Studio bot or abandoned by the user before resolution. |
|Avg. deflection time (hh:mm:ss) | Average bot conversation duration that deflects within the bot in hh:mm:ss format. |
|Total bot conversations over time |The total number of customer-initiated interactions with a Copilot Studio bot. Includes conversations fully managed by the bot and those escalated to a service representative over a selected time period.| 

## Metrics by bot

:::image type="content" source="../media/bot-intent-metrics-by-bot.png" alt-text="Screenshot of metrics by bot." lightbox="../media/bot-intent-metrics-by-bot.png":::

|Metrics | Definition  |
|---------|---------|
|Bot name | Name of all the bots or AI agents available with conversations that include the intent agent.| 
|Total conversations | The total number of customer-initiated interactions with a Copilot Studio bot. Includes conversations fully managed by the bot and those escalated to a service representative. The total includes both deflected and escalated conversations. |
|Conversations escalated| Number of bot conversations that are escalated to representative.|  
|Bot escalation rate  | Percentage of bot conversations that are escalated to a representative over total bot conversations. |
|Conversations deflected  | Number of bot conversations that are deflected by the AI agent either due to resolution or user abandoning the conversation.|
| Bot deflection rate | Percentage of bot conversations that are deflected by bot over total bot conversations.  |
|Avg bot time (hh:mm:ss) | Average bot conversation duration in hh:mm:ss format that are either escalated or deflected.  |

## Metrics by intent group

:::image type="content" source="../media/bot-intent-metrics-by-intent-group.png" alt-text="Screenshot metrics by intent group drilldown." lightbox="../media/bot-intent-metrics-by-intent-group.png":::

|Metrics | Definition  |
|---------|---------|
|Intent group | Name of intent group set by admin in Copilot Service admin center.|
|Total conversations| The total number of customer-initiated interactions with a Copilot Studio bot. Includes conversations fully managed by the bot and those escalated to a service representative per intent group. |
|Conversations escalated | Number of bot conversations per intent group that are escalated to representative.|
|Bot escalation rate  | Percentage of bot conversations that are escalated to a representative per intent group over total bot conversations per intent group. |
|Conversations deflected  | Number of bot conversations per intent group that are deflected by the AI agent either due to resolution or user abandoning the conversation. |
| Bot deflection rate | Percentage of bot conversations that are deflected by bot per intent group over total bot conversations per intent group. |
|Avg bot time (hh:mm:ss) | Average bot conversation duration in hh:mm:ss format that are either escalated or deflected per intent group .|

## Drill-down
 
In the **Metrics by intent group** section, select **Details** to view metrics by intent.

### Metrics by intent

|Metrics | Definition  |
|---------|---------|
| Intent| List of intents set by the administrator in Copilot Service admin center.|
| Total conversations| The total number of customer-initiated interactions with a Copilot Studio bot. Includes conversations fully managed by the bot and those escalated to a representative per intent.|
|Conversations escalated| Number of bot conversations per intent that are escalated to representative.   |
|Bot escalation rate| Percentage of bot conversations that are escalated to a representative per intent group over total bot conversations per intent.  |
|Conversations deflected| Number of bot conversations per intent that are deflected by the AI agent either due to resolution or user abandoning the conversation. |
| Bot deflection rate|Percentage of bot conversations that are deflected by bot per intent over total bot conversations per intent group.  |
|Avg. bot time (hh:mm:ss)| Average bot conversation duration in hh:mm:ss format that were either escalated or deflected per intent.|

## Related information

[Manage real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator)    
[Overview of Omnichannel real-time analytics dashboard](/dynamics365/customer-service/use/intro-realtime-analytics-dashboard)   
[Agent group report (preview)](realtime-agent-group-report.md)
