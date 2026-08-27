---
title: Use the Quality Assurance Agent dashboard in Dynamics 365 Contact Center
description: Use the Quality Assurance Agent dashboard to analyze quality trends, track KPIs, and identify opportunities to improve service performance.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection: get-started
ms.date: 08/25/2026
ms.custom: bap-template
---

# Use the Quality Assurance Agent dashboard

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

The Quality Assurance Agent historical analytics dashboard helps supervisors monitor conversation quality by using key performance indicators (KPIs) and visual analytics. The dashboard combines quality scores, quality dips, and supervisor notification data to help supervisors identify improvement opportunities, track trends, and evaluate quality across service representatives over time.

> [!IMPORTANT]
> - This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature isn't intended for use in making—and shouldn't be used to make—decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This responsibility also includes adequately notifying end users that their communications with representatives might be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users might be monitored, recorded, or stored.
> - Customers should avoid using the system to infer or make conclusions about emotional or psychological states of employees or customers, such as stress levels, intent, or sentiment beyond supported signals. The system doesn't reliably detect mental or emotional conditions.

## Prerequisites

Before you use the Quality Assurance Agent historical analytics dashboard, ensure that:

- You have access to Dynamics 365 Contact Center.
- Quality and coaching capabilities are configured for supervisors and representatives.
- You [enabled historical analytics for Quality Assurance Agent](/dynamics365/customer-service/administer/oc-historical-analytics-reports#enable-historical-analytics-for-quality-assurance-agent).

## View the quality and coaching historical analytics dashboard

The dashboard includes summary cards and charts that provide graphical views of quality KPIs. Use these visuals to identify which quality indicators are performing well, which indicators need attention, and how quality changes over time and across representatives.

By default, the dashboard shows KPIs for the last 60 days and for all channels, queues, and representatives in your system. Use the **Duration**, **Channel**, **Queue**, and **Customer Service representative** filters to refine the dashboard data.

The dashboard shows when its data was last updated. Use **Edit dashboard**, **Bookmarks**, and **Update bookmark** to customize the dashboard and save preferred views. Learn more in [Manage bookmarks](/dynamics365/customer-service/use/manage-bookmarks).

:::image type="content" source="../media/quality-assurance-agent-dashboard.png" alt-text="Quality Assurance Agent dashboard with quality score, quality dip, notification, and representative performance metrics." lightbox="../media/quality-assurance-agent-dashboard.png":::

## Dashboard details

The dashboard includes the following KPI cards.

| Metric | Description |
|---|---|
| **Avg. quality score** | The average quality score across all evaluated conversations during the selected period, on a scale of 0–100. |
| **% with quality dips** | The percentage of conversations in which the quality score dropped below the quality threshold during the selected period. |
| **Supervisor notifications sent** | The number of notifications sent to supervisors when quality scores dropped below the threshold. |

## Dashboard charts

The dashboard includes charts that help supervisors analyze quality patterns and trends.

| Chart | Description |
|---|---|
| **Quality score by indicator** | Shows the average quality score for each quality indicator. Use this chart to identify high- and low-scoring quality indicators. |
| **Quality score / Threshold breach rate** | Switch between the tabs to compare quality scores and threshold breach rates. |
| **Quality score over time** | Tracks quality scores over time and shows whether they remained above the quality threshold. |

## View quality by representative

The **By Customer Service Representative** table shows quality performance for each representative.

| Column | Description |
|---|---|
| **Customer Service Representative** | The representative's name. |
| **Conversations** | The number of evaluated conversations that the representative handled during the selected period. |
| **Quality score** | The average quality score for the representative's conversations. |
| **Threshold breaches** | The number of times the representative's conversations breached the configured quality threshold. |

## Related information

[Configure quality and coaching skills](../administer/configure-quality-coach.md)  
[Use quality and coaching skills](use-quality-coach.md#use-quality-and-coaching-skills)  
[Responsible AI FAQ for AI agents](../implement/faq-rai-ai-agents.md)
