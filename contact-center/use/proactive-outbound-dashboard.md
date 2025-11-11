---
title: Proactive Outbound dashboard
description: Learn how to use the Proactive Outbound dashboard to track outbound interactions, identify bottlenecks, and enhance customer engagement outcomes in Dynamics 365 Contact Center.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: conceptual
ms.collection:
ms.date: 11/11/2025
ms.custom: bap-template
---

# Proactive Outbound dashboard

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

The Proactive Outbound dashboard in Omnichannel historical analytics tracks conversation metrics and monitors ongoing conversations by conversation direction (incoming or outgoing) and conversation type. It provides detailed insights into outbound customer engagements initiated through proactive outreach, helping teams monitor, analyze, and optimize strategies for higher delivery rates and improved customer experiences. The dashboard displays delivery status, result, and dial mode, enabling quick identification of trends and bottlenecks. Delivery metrics are segmented by proactive engagement configuration, queue, and date for granular analysis and targeted improvements.

Users can apply out-of-box filters, such as duration, channel, queue, proactive engagement configuration, and time zone, to refine data for targeted analysis. 

## Access the dashboard

You can access the dashboard from the Customer Service workspace. Learn more in [Access the dashboards](/dynamics365/customer-service/use/omnichannel-analytics-insights).

You need to enable the Proactive Outbound dashboard from Customer Service admin center. Learn more in [Enable omnichannel historical analytics for proactive outbound](/dynamics365/customer-service/administer/oc-historical-analytics-reports).

:::image type="content" source="../media/proactive-outbound-report.png" alt-text="Screenshot of proactive outbound dashboard." lightbox="../media/proactive-outbound-report.png":::

## Interactive charts and tables

The dashboard displays these charts and tables for quick analysis.

Charts:

- **Total deliveries by status** bar chart displays (completed, expired, and others).
- **Processed deliveries by result** donut chart shows call outcomes. For example, call ended, call failed. 
- **Processed deliveries by dial mode** pie chart breaks down processed deliveries by dial mode (Copilot and Progressive), including new predictive dialing.

Tables:
 
- **Delivery metrics by Proactive Engagement Configuration** table lists each configuration, its status, priority, total deliveries, and processed deliveries, helping teams track which setups drive results.

- **Delivery metrics by queue** table shows delivery and processing metrics per queue, supporting operational workload management.

- **Delivery metrics by date** table shows a daily breakdown of total and processed deliveries for trend analysis.

## Panel filters

The dashboard is prefiltered by the default panel filters **Conversation type** and **Conversation direction** to show outbound interactions only. You can also check the default panel filters applied under **Dial mode**, **Delivery Status**, **Delivery Result**. You don't need any permissions to view panel filters. 

## Related information

[Omnichannel for Customer Service dashboards](/dynamics365/customer-service/use/omnichannel-analytics-insights)    
[Enable historical analytics for proactive outbound engagements](/dynamics365/customer-service/administer/oc-historical-analytics-reports)
