---
title: Overview of real-time streaming analytics (preview)
description: Real-time streaming analytics deliver event-driven metric updates so supervisors see the current state of their contact center. Explore live monitoring and faster decisions today.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.date: 06/23/2026
ms.topic: concept-article
ms.custom: bap-template
---

# Overview of real-time streaming analytics (preview)

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[This article is prerelease documentation and is subject to change.]

Real-time streaming analytics provides supervisors with visibility into contact center operations, so they can monitor key metrics as they change and take immediate action.

> [!IMPORTANT]
>
> - This is a production-ready preview feature.
> - Production-ready previews are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520).

Supervisors rely on operational metrics such as queue backlog, representative availability, service level, abandon rate, and so on to make time-critical decisions. Traditional dashboards refresh at scheduled intervals and re-render entire views, which can delay the availability of insights during active monitoring.

Real-time streaming analytics uses an event-driven architecture to deliver live metric updates. It gives supervisors a current view of contact center performance. It enables faster responses, reduced wait times, proactive service-level agreement management, and better staffing decisions. By working with streaming data, configurable KPIs, and intuitive wallboards, supervisors can respond more quickly to operational issues, manage staffing more effectively, and improve customer experiences.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Prerequisites

Before you use real-time streaming analytics, make sure that the following requirements are met:

- Omnichannel for Contact Center is configured and in use.
- You have the Omnichannel Supervisor role to view analytics dashboards and take action.
- Customer interaction channels (such as, voice, chat, or or other asynchronous messaging channels) are set up and generate live interaction data.

## Access real-time streaming analytics

Sign in to your org. Access the dashboards by using the https://supervisor-preview URL. Depending on your environment type (production or first release) and your organization's region, use one of the following links.

|URL |Environment  |
|---------|---------|
|portal.us.fre.contactcenterai.powerplatform.com/experience/supervisor     |    FRE     |
|portal.eu.fre.contactcenterai.powerplatform.com/experience/supervisor     |    FRE     |
|portal.ca.fre.contactcenterai.powerplatform.com/experience/supervisor  |    FRE     |
|portal.au.fre.contactcenterai.powerplatform.com/experience/supervisor     |    FRE     |
|portal.ae.contactcenterai.powerplatform.com/experience/supervisor    |   PROD      |
|portal.as.contactcenterai.powerplatform.com/experience/supervisor    |     PROD    |
|portal.au.contactcenterai.powerplatform.com/experience/supervisor     |   PROD      |
|portal.br.contactcenterai.powerplatform.com/experience/supervisor    |    PROD     |
|portal.ca.contactcenterai.powerplatform.com/experience/supervisor    |    PROD     |
|portal.ch.contactcenterai.powerplatform.com/experience/supervisor     |  PROD       |
|portal.de.contactcenterai.powerplatform.com/experience/supervisor    |  PROD       |
|portal.eu.contactcenterai.powerplatform.com/experience/supervisor    |   PROD      |
|portal.fr.contactcenterai.powerplatform.com/experience/supervisor     |  PROD       |
|portal.in.contactcenterai.powerplatform.com/experience/supervisor    |    PROD     |
|portal.it.contactcenterai.powerplatform.com/experience/supervisor     |  PROD       |
|portal.jp.contactcenterai.powerplatform.com/experience/supervisor    | PROD        |
|portal.kr.contactcenterai.powerplatform.com/experience/supervisor     |    PROD     |
|portal.no.contactcenterai.powerplatform.com/experience/supervisor    |    PROD     |
|portal.pl.contactcenterai.powerplatform.com/experience/supervisor     |    PROD     |
|portal.se.contactcenterai.powerplatform.com/experience/supervisor    |    PROD     |
|portal.sg.contactcenterai.powerplatform.com/experience/supervisor     |   PROD      |
|portal.uk.contactcenterai.powerplatform.com/experience/supervisor     |   PROD      |
|portal.us.contactcenterai.powerplatform.com/experience/supervisor    | PROD        |
|portal.za.contactcenterai.powerplatform.com/experience/supervisor    |  PROD       |

## Top navigation tabs

The following views are available:

| View | Description |
|------|-------------|
| [Wallboard](realtime-streaming-wallboard.md) | Provides a consolidated view of operational metrics, queue health, representative availability, and service performance. |
| [Assisted Service](realtime-streaming-assisted-service.md) | Provides detailed analysis of contact center performance, including trends, service metrics, and conversation insights. |
| [Queues](realtime-streaming-queues.md) | Displays queue-level metrics such as backlog, wait times, service levels, and abandon rates. |
| [Representatives](realtime-streaming-representatives.md) | Shows representative availability, presence status, workload, and performance metrics. |
| [Conversations](realtime-streaming-conversations.md)| Provides visibility into active, queued, and completed customer conversations and supports conversation management actions. |

## Filter options

Use the filter dropdown to refine results based on the available attributes. For example: **Period**, **Channel**, and **Queues**.

## Understand metric types

Metrics in real-time streaming analytics are categorized into two types:

### Live metrics

Live metrics reflect the current operational state and update continuously. These metrics are identified by a **Live** tag in the user interface. Examples of live metrics:

- Active conversations
- Queue backlog
- Online representatives
- Longest wait time

### Aggregated metrics

Aggregated metrics summarize data over a selected time period. These metrics adhere to the time period you select and update as the underlying data changes. Examples of aggregated metrics:

- Service level
- Abandon rate
- Average speed to answer

## Thresholds and visual indicators

Metrics have predefined thresholds that indicate their operational state. Understanding these indicators helps you identify when action is needed.

| Status | Description | Visual indicator |
|--------|-------------|------------------|
| **Normal** | Metric is within expected range | Default display |
| **At risk** | Metric is approaching critical levels | Amber background with **At risk** tag |
| **Critical** | Metric is outside acceptable thresholds | Red background with **Critical** tag |

Select **See details** for any metric to view threshold ranges, metric definitions, calculations, and trendlines. Trendlines indicate improving or deteriorating trends. This option is available in every dashboard except wallboards.

## Related information

[Wallboard](realtime-streaming-wallboard.md)  
[Assisted Service](realtime-streaming-assisted-service.md)  
[Queues](realtime-streaming-queues.md)  
[Representatives](realtime-streaming-representatives.md)  
[Conversations](realtime-streaming-conversations.md)