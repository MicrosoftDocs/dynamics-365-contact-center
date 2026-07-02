---
title: Proactive Outbound dashboard
description: Learn how to use the Proactive Outbound dashboard to track outbound interactions, identify bottlenecks, and enhance customer engagement outcomes in Dynamics 365 Contact Center.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection:
ms.date: 07/01/2026
ms.custom: bap-template
---

# Proactive Outbound dashboard

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

The Proactive Outbound dashboard in Omnichannel historical analytics provides visibility into conversation metrics and actively monitors ongoing interactions, categorized by conversation type. It provides detailed insights into outbound customer engagements initiated through proactive outreach, helping teams monitor, analyze, and optimize strategies for higher delivery rates and improved customer experiences. The dashboard displays delivery status, result, and dial mode, enabling quick identification of trends and bottlenecks. Metrics are segmented by engagement configuration, queue, and date for actionable insights.

Proactive outbound insights are available in two dashboards:

- The **Proactive Engagement** dashboard in Omnichannel real-time analytics gives supervisors a live view of in-flight outbound work so they can monitor pending and in-progress engagements, agent availability, and pacing as it happens. Learn more in [Proactive engagement dashboard](proactive-engagement-dashboard.md).

- The **Proactive Outbound** dashboard in Omnichannel historical analytics surfaces aggregated delivery trends across configurations, queues, and dates for retrospective analysis and optimization.

Users can apply the out-of-box filters, duration, channel, queue, proactive engagement configuration, and time zone, to refine data for targeted analysis. Use the Channel filter to filter by voice agent or the bot (agent) name to filter on the exact agent.

When a proactive outbound call is initiated, an entry is created in msdyn_proactivedelivery. Based on the provided inputs, the system places the call, updates the delivery status to **Complete** (processed), and creates a corresponding conversation record. The corresponding metrics are displayed on the dashboard. Learn more in [CreateProactiveVoiceDelivery](/dynamics365/contact-center/extend/api/ccaas_createproactivevoicedelivery).

## Prerequisites

- You enabled the Proactive Outbound dashboard from Customer Service admin center. Learn more in [Enable omnichannel historical analytics for proactive outbound](/dynamics365/customer-service/administer/oc-historical-analytics-reports#enable-omnichannel-historical-analytics-for-proactive-outbound-engagements).

- To use the real-time analytics dashboard, you enabled real-time analytics for proactive engagement. Learn more in [Manage real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator).

- You [configured proactive engagement](../administer/configure-proactive-engagement.md).

- You have the Omnichannel Supervisor role.

## Access the dashboard

You can access the dashboard from the Customer Service workspace. Learn more in [Access the dashboards](/dynamics365/customer-service/use/omnichannel-analytics-insights).

:::image type="content" source="../media/proactive-outbound-report.png" alt-text="Screenshot of proactive outbound dashboard." lightbox="../media/proactive-outbound-report.png":::

## Historical analytics dashboards

The dashboard displays the proactive engagement metrics in the following charts and tables.

Charts:

- The **Total deliveries by status** bar chart displays data by the delivery status of calls that are completed, expired, and others.

- The **Processed deliveries by result** donut chart displays the data by outcomes, such as call ended and call failed.

- The **Processed deliveries by dial mode** pie chart breaks down processed deliveries by dial mode (Copilot and Progressive), including new predictive dialing.

Tables:
 
- The **Delivery metrics by Proactive Engagement Configuration** table lists each configuration, its status, priority, total deliveries, and processed deliveries, that helps teams track which setups drive results.

- The **Delivery metrics by queue** table shows delivery and processing metrics per queue that supports operational workload management.

- The **Delivery metrics by date** table shows a daily breakdown of total and processed deliveries for trend analysis.

## Panel filters

The dashboard shows ongoing interactions using the out-of-the-box filters, **Conversation Type** and **Conversation Direction**. You can also check the default panel filters applied under **Dial mode**, **Delivery Status**, **Delivery Result**. You don't need any permissions to view panel filters.

### Related information

[Configure proactive engagement](../administer/configure-proactive-engagement.md)  
[Proactive Engagement dashboard](proactive-engagement-dashboard.md)  
[Omnichannel for Customer Service dashboards](/dynamics365/customer-service/use/omnichannel-analytics-insights)    
[Enable historical analytics for proactive outbound engagements](/dynamics365/customer-service/administer/oc-historical-analytics-reports)
