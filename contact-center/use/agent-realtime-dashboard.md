---
title: View and understand the bot report in Omnichannel real-time analytics
description: Learn about the bot report in Omnichannel real-time analytics
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: conceptual 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---

# View and understand the bot report in Omnichannel real-time analytics

The **Bots** report provides insights into key metrics for all the Copilot Studio bots used in your contact center. It allows you to monitor the volumes of in-progress and completed bot conversations. 

:::image type="content" source="../media/oc-realtime-dashboard.png" alt-text="Screenshot of realtime bot dashboard"::: 

## Prerequisites

- You must have the **Analytics Report Author** role to use the visual customizations in the bot dashboard. Visual customization is limited to the data available in the embedded Power BI report. If you want to add more data, you need a Power BI license and enable data model customization.

## Key metrics

Out of the box, the dashboard displays key metrics for the last 24 hours, such as total bot conversations, outgoing bot conversations, completed bot conversations, transferred bot conversations, and average bot conversation duration to help you understand bot usage and optimize performance in real time.

You can filter the report by selecting **All** to view bot performance across all channels or by choosing a specific channel. Additional filters include time, queue, time zone, and conversation status. For more information, see [Overview of Omnichannel Real-time analytics dashboards](/dynamics365/customer-service/use/intro-realtime-analytics-dashboard).

## Monitor trends

You can identify trends in realtime bot performance with interactive charts and reports such as conversations over time, average bot conversation duration, and conversations by status.

 The visual display helps you discern changes and patterns in the data so that you can act quickly to address the most important issues.

When you select a component in a chart, the data is filtered accordingly. In this way, you can view only data that is related to the selected component. For example, if you select the **Completed** component in the **Conversation status** chart, the dashboard is refreshed and shows only the conversations that are currently in the **Completed** state.

## Customize bot dashboard
You can edit the report to add the additional metrics and filters to the bot. To customize the bot dashboard, see [customize visual display](customize-agent-dashboard.md). 

## Bot details drill-down

You can select a bot from **BotName** section on the dashboard to view key metrics and insights about individual bots' performance.

Key KPIs for a bot include:

- **Total bot conversations**: The number of ongoing or closed conversations handled by the bot within the specified duration.
- **Total bot ongoing conversations**: The number of conversations currently in progress.
- **Total bot completed conversations**: The number of conversations successfully resolved or have ended within the specified duration.
- **Total bot transferred conversations**: The number of conversations that were escalated by the bot to a human agent or an external phone number within the specified duration.
- **Average conversation duration**: The average time each conversation lasts. The conversation duration is calculated from the time the bot is assigned to the conversation until the bot's involvement ends, either when the bot escalates the conversation or ends it.