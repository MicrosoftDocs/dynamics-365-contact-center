---
title: Historical analytics overview for the Shared Analytics Platform
description: Learn how historical analytics on the Shared Analytics Platform helps you understand customer experience, service performance, and staffing.
ms.date: 10/30/2026
ms.topic: overview
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
ai-usage: ai-assisted
---

# Overview of contact center historical analytics in the Shared Analytics Platform

The Shared Analytics Platform turns operational data into consistent metrics for historical reporting and analysis. In Dynamics 365 Contact Center, use these metrics to understand customer experience, assess service representative performance, and identify opportunities to improve contact center operations.

Use historical analytics to monitor trends, investigate outcomes, and make informed decisions based on consistent metric definitions.

Contact Center historical analytics builds on existing Omnichannel historical reports to help you understand customer demand, evaluate service performance, and make informed staffing and coaching decisions. Shared metric definitions give your teams a consistent basis for reviewing results, with less duplicated effort preparing data and calculating measures for separate reports.

You can customize supported Power BI reports to align with your business priorities. For a broader view of your operations, use Microsoft Fabric to combine supported analytics data with other business data. Contact Center historical analytics requires separate enablement. Using Fabric also requires separate configuration, appropriate licensing or capacity, and permissions. Learn more in [Choose your Contact Center analytics journey](../administer/modern-contact-center-analytics-journey.md).

> [!NOTE]
> - Contact Center historical analytics and [Omnichannel historical analytics](/dynamics365/customer-service/use/omnichannel-analytics-insights) can coexist in the same environment, so you can enable Contact Center historical analytics without disabling Omnichannel historical analytics.
> - Metric definitions and units can differ from existing Omnichannel historical reports, so results might not be identical.

## How the platform turns data into insights

The platform consolidates analytics data in a Microsoft-managed Fabric lakehouse. It uses a star schema that supports dashboard performance while preserving detailed data for investigation and custom analysis.

The architecture consists of three layers.

### Ingestion and storage

The ingestion and storage layer moves contact center data from Dataverse into the analytics platform and stores historical interaction data in Microsoft OneLake by using the open Delta Parquet format.

Direct ingestion avoids legacy CSV conversion and synchronizes data from Dataverse to the analytics layer in under 15 minutes. Columnar storage helps dashboards retrieve relevant metrics without scanning unrelated rows and allows analytics and AI experiences to use retained conversation history and business context.

Learn more in [Link your Dataverse environment to Microsoft Fabric and unlock deep insights](/power-apps/maker/data-platform/azure-synapse-link-view-in-fabric) and [OneLake](/fabric/onelake/onelake-overview).

### Transformation and semantic model

The analytics data model uses a star schema, which connects activity records and summaries to descriptive information. You don't need to work with these tables to use built-in dashboards, but understanding their roles can help when you investigate results or discuss reporting needs with a report builder.

| Table type | What it contributes to your analysis |
|---|---|
| Dimension tables | Provide context, such as the service representative, queue, channel, or presence state. Use this information to filter and group results. |
| Fact tables | Store detailed activity, such as individual sessions or capacity events. These records support detailed analysis and drill-through investigations. |
| Aggregate tables | Store precalculated totals and counts. These summaries support high-volume dashboard queries and historical trend analysis with less processing. |

Shared definitions and relationships give these tables business meaning, so reports and supported AI experiences can interpret the data consistently. Learn more in [Understand the Shared Analytics Platform platform and analytics data model](../extend/overview-data-model.md).

### Analytics consumption

The consumption layer makes the standardized data available to multiple analytics experiences, including Power BI reports, Fabric integrations, and custom dashboards.

Organizations can use OneLake shortcuts to connect their governed Fabric workspaces directly to the central data lake without replicating the data.

## Find the right dashboard and metrics for your business question

Choose a dashboard and metrics based on the business activity you want to examine. A conversation measures a customer interaction, a session focuses on service representative activity within an interaction, and a queue segment focuses on work within a queue. These levels of detail help you investigate the same operation from different perspectives.

| What do you want to understand? | Dashboard | Metric references |
|---|---|---|
| How much customer demand do you receive, and what are the outcomes? | [Conversation dashboard](conversation-dashboard.md) covers volume, engagement, abandonment, transfers, response times, service levels, and customer experience. | [Conversation metrics](conversation-metrics.md). |
| Where does work wait, transfer, or leave a queue? | [Queue dashboard](queue-segments-dashboard.md) covers queue workload, routing efficiency, wait times, abandonment, and service levels. | [Queue segment metrics](queue-segment-metrics.md). |
| How do service representatives handle work, and what is their availability? | [Agent dashboard](contact-center-agent-dashboard.md) covers session handling, response times, handle time, consults, monitoring, availability, and workload trends. | [Session metrics](session-metrics-dashboard.md), [availability metrics](availability-metrics.md), and [capacity metrics](capacity-metrics-dashboard.md). |
| How effectively do bots and Copilot Studio agents engage and assist customers? | [Bot dashboard](bot-dashboard.md) covers engagement, resolution, abandonment, deflection, escalation, duration, and customer satisfaction. | [Bot metrics](bot-metrics.md). |
| What patterns in voice conversations might need coaching or review? | [Voice insights dashboard](voice-dashboard.md) covers speaking patterns, pauses, monologues, and other voice interaction signals. | [Voice insight metrics](voice-insight-metrics.md). |

For staffing analysis, availability metrics show login activity and time spent in presence states. Capacity metrics help you understand workload distribution, capacity utilization, and readiness for assignments.

Review the linked metric references before comparing results or building a custom report. They explain definitions, calculations, and reporting considerations that affect interpretation.

## Extend analysis for your organization

You can customize supported reports or build custom analytics. Your organization can use OneLake shortcuts to connect a governed Fabric workspace to supported data in the central lake without replicating it.

For help choosing between report customization, Power BI data model customization, and Microsoft Fabric, see [Choose your Contact Center analytics journey](../administer/modern-contact-center-analytics-journey.md).

## Related information

- [Enable Contact Center historical analytics](../administer/enable-contact-center-analytics.md).
- [Understand the analytics data model and table references](../extend/overview-data-model.md).
- [Connect Microsoft Fabric to Dataverse by using a service principal](../extend/connect-dataverse-shortcut.md).
