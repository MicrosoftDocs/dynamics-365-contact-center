---
title: View and understand the bot report in Omnichannel real-time analytics
description: Learn about the bot report in Omnichannel real-time analytics.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: conceptual 
ms.collection: 
ms.date: 08/25/2025
ms.custom: bap-template 
---

# View and understand the bot report in Omnichannel real-time analytics

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]


The **Bot** report provides insights into key metrics for all the Copilot agents used in your contact center. It allows you to monitor the volumes of in-progress and completed AI agent conversations.

Out of the box, the dashboard displays key metrics for the last 24 hours to help you understand AI agent usage and optimize performance in real time.

You can filter the report by selecting **All** to view AI agent performance across all channels or by choosing a specific channel. Filters include time, queue, time zone, and conversation status. Learn more in [Overview of Omnichannel real-time analytics dashboards](/dynamics365/customer-service/use/intro-realtime-analytics-dashboard#filter-information-displayed-on-dashboard).


## Key metrics

Key performance indicators (KPIs) for AI agents include:

- **Total bot conversations**: The number of ongoing or closed conversations handled by the AI agent within the specified duration.
- **Total bot ongoing conversations**: The number of conversations currently in progress.
- **Total bot completed conversations**: The number of conversations that are successfully resolved or end within the specified duration.
- **Total bot transferred conversations**: The number of AI agent conversations that are escalated to a customer service representative or an external phone number within the specified duration.
- **Average conversation duration**: The average time each conversation lasts. The conversation duration is calculated from the time the AI agent is assigned to the conversation until the AI agent escalates the conversation or ends it.

:::image type="content" source="../media/oc-realtime-bot-dashboard.png" alt-text="Screenshot of realtime bot dashboard"::: 

## Monitor trends

You can identify trends in real-time AI agent performance with interactive charts and reports such as conversations over time, average AI agent conversation duration, and conversations by status.

You can filter the data in the chart by selecting a component. For example, if you select the **Completed bot conversations** component in **Conversations over time**, the dashboard shows the conversations that are currently in the **Completed** state.

## Bot details drill-down

You can select an AI agent from the **Bot name** filter on the dashboard to view key metrics and insights about individual AI agents' performance.

## Customize bot dashboard

You can edit the report to add the following AI agent specific metrics and filters to the dashboard:

- Dialed number identification service (DNIS)
- Last language
- Fallback action calls
- Bot session level outcome reasons

Learn more about how to customize the bot dashboard in [customize visual display](customize-agent-dashboard.md). 

> [!NOTE]
> You must have the **Analytics Report Author** role to use the visual customizations in the bot dashboard. Visual customization is limited to the data available in the embedded Power BI report. If you want to add more data, you need a Power BI license and enable data model customization.
