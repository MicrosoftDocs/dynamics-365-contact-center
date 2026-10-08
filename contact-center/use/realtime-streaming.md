---
title: Overview of real-time streaming analytics (preview)
description: Learn how real-time streaming analytics provides live contact center metrics for operational monitoring and faster decision-making.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.date: 10/07/2026
ms.topic: concept-article
ms.custom: bap-template
---

# Overview of real-time streaming analytics (preview)

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[This article is prerelease documentation and is subject to change.]

Real-time streaming analytics gives supervisors visibility into contact center operations so they can monitor key metrics as they change and take immediate action.

> [!IMPORTANT]
>
> - This is a production-ready preview feature.
> - Production-ready previews are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520).

Supervisors use operational metrics such as queue backlog, representative availability, service level, and abandon rate to make time-sensitive decisions. Traditional dashboards refresh at scheduled intervals and re-render entire views, which can delay insights during active monitoring.

Real-time streaming analytics uses an event-driven architecture to deliver live performance insights, enabling supervisors to respond faster, manage staffing effectively, maintain service levels, and enhance customer experiences.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Prerequisites

Before you use real-time streaming analytics, make sure that the following requirements are met:

- Omnichannel for Contact Center is configured and in use.
- You have the Omnichannel Supervisor role to view analytics dashboards and take action.
- Customer interaction channels, such as voice, chat, or other asynchronous messaging channels, are configured and generate live interaction data.

## Access real-time streaming analytics

Sign in to your organization. Access the dashboards by using the `https://supervisor-preview` URL. Depending on your environment type (production or first release) and organization region, use one of the following links.

|URL |Environment  |  GEO  |
|---------|---------|----------|
|portal.us.fre.contactcenterai.powerplatform.com/experience/supervisor     |    FRE     | United States|
|portal.eu.fre.contactcenterai.powerplatform.com/experience/supervisor     |    FRE     | Europe|
|portal.ca.fre.contactcenterai.powerplatform.com/experience/supervisor  |    FRE     | Canada |
|portal.au.fre.contactcenterai.powerplatform.com/experience/supervisor     |    FRE     | Australia |
|portal.as.contactcenterai.powerplatform.com/experience/supervisor    |     PROD    | Asia |
|portal.au.contactcenterai.powerplatform.com/experience/supervisor     |   PROD      | Australia |
|portal.br.contactcenterai.powerplatform.com/experience/supervisor    |    PROD     | Brazil |
|portal.ca.contactcenterai.powerplatform.com/experience/supervisor    |    PROD     | Canada |
|portal.eu.contactcenterai.powerplatform.com/experience/supervisor    |   PROD      | Europe |
|portal.fr.contactcenterai.powerplatform.com/experience/supervisor     |  PROD       | France |
|portal.de.contactcenterai.powerplatform.com/experience/supervisor    |  PROD       | Germany|
|portal.in.contactcenterai.powerplatform.com/experience/supervisor    |    PROD     | India |
|portal.jp.contactcenterai.powerplatform.com/experience/supervisor    | PROD        | Japan |
|portal.ch.contactcenterai.powerplatform.com/experience/supervisor     |  PROD       | Switzerland|
|portal.ae.contactcenterai.powerplatform.com/experience/supervisor    |   PROD      | United Arab Emirates|
|portal.uk.contactcenterai.powerplatform.com/experience/supervisor     |   PROD      |United Kingdom |
|portal.us.contactcenterai.powerplatform.com/experience/supervisor    | PROD        | United States |


## Top navigation tabs

The following views are available in real-time streaming analytics:

| View | Description |
|------|-------------|
| [Wallboard](realtime-streaming-wallboard.md) | Provides a consolidated view of operational metrics, queue health, representative availability, and service performance. |
| [Assisted Service](realtime-streaming-assisted-service.md) | Provides detailed analysis of contact center performance, including trends, service metrics, and conversation insights. |
| [Queues](realtime-streaming-queues.md) | Displays queue-level metrics such as backlog, wait times, service levels, and abandon rates. |
| [Representatives](realtime-streaming-representatives.md) | Shows representative availability, presence status, workload, and performance metrics. |
| [Conversations](realtime-streaming-conversations.md)| Provides visibility into active, queued, and completed customer conversations and supports conversation management actions. |
| [Self Service](realtime-streaming-self-service.md) | Provides visibility into containment outcomes, escalation trends, self-service engagement volumes, supported languages, customer intents, and operational health metrics. |

## Filter options

Use the filter dropdown to refine results based on the following attributes.

- **Period**: Use the **Period** filter to view metrics for a specific time range, such as the last 15 minutes, hour, or day. The selected period applies to historical and aggregated metrics across the dashboard. Live metrics ignore the selected **Period** filter and update based only on applicable real-time filters, such as **Business Unit**, **Channel**, and **Queue**.

- **Channel**: Use the **Channel** filter to scope analytics data to a specific engagement channel, such as voice, chat, SMS, or social messaging. Filtering by channel helps supervisors analyze performance, activity, and workload metrics for a particular communication method.

- **Business Unit**: Filter dashboard metrics by business unit. Select a business unit to view data only for the associated representatives, conversations, queues, and operational activities. Select **All business units** to view organization-wide metrics. The selected business unit filter is applied consistently across all dashboard tabs.

- **Queues**: Use the **Queue** filter to view metrics for one or more queues. Applying a queue filter narrows the displayed data to conversations, representatives, and operational metrics associated with the selected queues, helping supervisors monitor queue-specific performance and staffing levels.

- **Representative**: Applicable to the **Representative** view only. Learn more in [Monitor representatives in real time (preview)](realtime-streaming-representatives.md).


## Understand metric types

Metrics in real-time streaming analytics are categorized into two types:

### Live metrics

Live metrics show the current operational state and update continuously. You can identify these metrics in the user interface by the **Live** tag. Examples include:

- Active conversations
- Queue backlog
- Online representatives
- Longest wait time

### Aggregated metrics

Aggregated metrics summarize data over a selected time period. These metrics follow the selected time period and update as the underlying data changes. Examples include:

- Service level
- Abandon rate
- Average speed to answer

## Thresholds and visual indicators

Metrics have predefined thresholds that indicate their operational state. Understanding these indicators helps you identify when action is needed.

| Status | Description | Visual indicator |
|--------|-------------|------------------|
| **Normal** | Metric is within expected range. | Default display. |
| **At risk** | Metric is approaching critical levels. | Amber background with **At risk** tag. |
| **Critical** | Metric is outside acceptable thresholds. | Red background with **Critical** tag. |

Select **See details** for any metric to view threshold ranges, metric definitions, calculations, and trendlines. Trendlines indicate whether metrics are improving or deteriorating. This option is available in every dashboard except the Wallboard view.

## Language support

Learn more about the languages supported for real-time streaming analytics in [Explore feature availability by language](https://releaseplans.microsoft.com/en-US/availability-reports/?report=featurelangreport).

The dashboard language is determined in the following priority order:

- If you configure a user-level locale setting in the Dataverse organization, it takes the highest priority.
- If you don't configure a user-level locale, the system uses the organization-level locale setting.
- If neither a user-level nor organization-level locale is configured, the system uses the browser locale setting.

## Related information

[Wallboard](realtime-streaming-wallboard.md)  
[Assisted Service](realtime-streaming-assisted-service.md)  
[Queues](realtime-streaming-queues.md)  
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)
