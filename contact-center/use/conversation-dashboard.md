---
title: Conversation dashboard
description: Learn how you can use the contact center conversation dashboard.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: concept-article
ms.collection:
ms.date: 10/30/2026
ms.update-cycle: 180-days
ai-usage: ai-assisted
---
# Conversation dashboard

Use the **Conversation** dashboard to review customer conversations across your organization. Supervisors and managers can monitor demand and service performance and identify opportunities to improve service levels and workforce planning.

The dashboard combines key performance indicators (KPIs), trend charts, and drill-down views for conversation volume, engagement, wait times, handling efficiency, transfers, and abandonment.

Use the dashboard to:

- Monitor customer demand across engagement channels.
- Assess how efficiently conversations are handled.
- Identify queues that require extra staffing or process improvements.
- Track customer wait times and abandonment trends.
- Compare performance across channels, queues, and time periods.
- Use historical conversation data to support staffing and operational planning decisions.

## Filter the dashboard

By default, you see data for the past month across all channels, queues, and service representatives.

Filter the dashboard by:

- **Date range**.
- **Channel**.
- **Queue**.
- **Conversation status**.
- **Time zone**.

Use these filters to compare performance across channels and queues, analyze specific periods, investigate representative performance, and identify demand and operational efficiency trends. Your selections persist when you switch between historical analytics dashboards.

## Data source

The **Conversation** dashboard uses the `AggConversation` aggregate table in the Shared Analytics Platform data model. Learn more in [AggConversation table reference](../extend/analytics/aggconversation.md).

## Key performance indicators

Review these KPIs for a summary of conversation performance.

| Metric | Description |
|----------|-------------|
| **Incoming conversations** | Counts customer conversations initiated during the selected period and presented to a service representative. Use it to assess customer demand across supported engagement channels. |
| **Engaged conversations** | Counts incoming conversations accepted by a service representative. Customer and representative interaction begins at engagement. Use the count to measure how many conversations receive representative attention. |
| **Abandon rate** | Shows the percentage of conversations customers abandon before engaging with a service representative. A high rate can indicate insufficient staffing, long wait times, or routing inefficiencies. |
| **Average speed to answer** | Measures the average wait before a service representative accepts a conversation. Supervisors can use it to evaluate responsiveness and monitor queue performance. |
| **Average handle time** | Measures the average time service representatives spend handling customer conversations. Use it to assess workload distribution and conversation complexity. |
| **Transfer rate** | Shows the percentage of conversations transferred between representatives or queues. A high rate can indicate routing issues, skill mismatches, or frequent escalation patterns. |

## Review charts and visualizations

| Chart | Description | Use this chart to |
|---------|-------------|-------------------|
| **Incoming conversations versus engaged conversations** | Compares incoming and engaged conversation counts over time. | - Identify customer demand trends.<br>- Determine whether staffing is sufficient.<br>- Monitor the gap between incoming and engaged conversations.<br>- Investigate periods of increased abandonment or service delays.<br><br>Large differences between incoming and engaged conversations can indicate staffing constraints or operational bottlenecks. |
| **Incoming conversations by channel** | Shows how incoming conversations are distributed across supported channels, such as chat, voice, SMS, and social messaging channels. | - Identify the channels with the highest conversation volume.<br>- Assess customer channel preferences.<br>- Allocate staffing based on channel demand.<br>- Monitor changes in channel usage over time. |
| **Abandon rate trend** | Tracks abandon rate over time to identify recurring periods of high abandonment. | - Identify customer abandonment patterns.<br>- Monitor the impact of staffing and queue performance.<br>- Detect service issues that affect customer engagement. |
| **Average speed to answer trend** | Shows how quickly conversations are answered during the selected period. | - Evaluate responsiveness.<br>- Assess staffing effectiveness.<br>- Monitor routing performance over time. |
| **Average handle time trend** | Shows handle time trends and changes in conversation duration. | - Identify changes in conversation complexity.<br>- Monitor representative workload.<br>- Evaluate operational efficiency. |
| **Average customer effort trend** | Shows the effort customers expend during interactions. | - Identify opportunities to improve customer experiences.<br>- Optimize support workflows.<br>- Monitor customer effort trends over time. |

## Conversation metrics by queue

Use **Conversation metrics by queue** to review individual queue performance and identify queues that need operational attention. The metrics use conversation data in the context of the selected queue.

| Metric | Description |
|----------|----------|
| Incoming conversations | Counts customer conversations routed to the selected queue. |
| Engaged conversations | Counts conversations in the queue accepted by a service representative. |
| Abandon rate | Shows the percentage of queue conversations customers abandoned before engagement with a service representative. |
| Average speed to answer | Measures the average queue wait before a service representative accepted the conversation. |
| Average handle time | Measures the average time service representatives spent handling conversations routed through the queue. |

## Conversation metrics by channel

Use **Conversation metrics by channel** to review customer engagement and operational performance across channels.

### Conversation summary

Review the following metrics for each channel.

| Metric | Description |
|----------|----------|
| Incoming conversations | Counts customer conversations initiated through the channel. |
| Engaged conversations | Counts channel conversations accepted by a service representative. |
| Abandon rate | Shows the percentage of channel conversations customers abandoned before engagement. |
| Average wait time | Average time customers waited before connecting with a service representative through the channel. |
| Average speed to answer | Average time required for a service representative to accept incoming conversations on the channel. |
| Average handle time | Measures the average time service representatives spent handling conversations on the channel. |
| Transfer rate | Shows the percentage of channel conversations transferred after engagement. |

### Conversation details

Use conversation details to investigate individual interactions and channel-specific trends. These details provide additional information for selected channels.

## Conversation metrics by date

Use the date-based view to identify recurring operational patterns and monitor daily performance changes.

### Hourly details

Select a date to review hourly metrics for that day.

Use hourly analysis to:

- Identify peak demand periods.
- Review changes in conversation volume throughout the day.
- Optimize staffing coverage.
- Monitor service levels during busy periods.

## Personalize your dashboard

Save filtered views as bookmarks. Customize visualizations, metrics, filters, and layouts to focus on the data most relevant to your organization. Learn more in [Manage bookmarks for reports](/dynamics365/customer-service/use/manage-bookmarks) and [Customize visual display](/dynamics365/customer-service/use/customize-reports).
