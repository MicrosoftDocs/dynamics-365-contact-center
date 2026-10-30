---
title: Contact center Historical analytics agent dashboard Dynamics 365 Contact Center
description: Learn about Contact center Historical analytics agent dashboard Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: overview
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-assisted
---

# Agent dashboard

Use the **Agent** dashboard to review customer service representative activity across sessions, channels, queues, and conversation statuses. Supervisors can assess session volume, acceptance and rejection patterns, handle and response times, consult and monitor activity, and representative availability.

Review all service representatives in the summary view, or open the drill-down view for one representative. The individual view shows the same types of metrics for the selected representative, with daily breakdowns.

## Data source

The **Agent** dashboard uses aggregate performance and availability data: `AggAgentPerformance` for session performance sections and `AggAgentAvailability` for the availability section. Learn more in [AggAgentPerformance](../extend/analytics/aggagentperformance.md) and [AggAgentAvailability](../extend/analytics/aggagentavailability.md).

## Filter the dashboard

Filter agent session data to focus on the representatives, periods, and other subsets you want to review.

| Filter | Description |
|---|---|
| **Date** | Select a predefined or custom date range. |
| **Channel** | Filter metrics by communication channel. |
| **Queue** | View metrics for one queue or all queues. |
| **Agent** | Filter metrics by service representative. |
| **Conversation status** | Filter data by conversation status. |
| **TimeZoneCode** | Display metrics in the selected time zone. |

## Key performance indicators

Review these high-level KPIs for a summary of agent session activity under the selected filters.

| Metric | Description |
|---|---|
| Accepted sessions | Counts sessions accepted by service representatives. |
| Rejected sessions | Counts sessions rejected by service representatives. |
| Transfer rate (Agent) | Percentage of handled sessions transferred by service representatives. |
| Agent Avg handle time | Average time service representatives spent handling sessions. |
| Total sessions | Counts all sessions associated with service representatives. |
| Timed out sessions | Counts sessions that timed out before acceptance. |

## Review visualizations

Use the visualizations to monitor session activity and identify changes in workload and handling performance over time.

| Visualization | Description | Use this visualization to |
|---|---|---|
| Accepted sessions | Shows accepted sessions during the selected period. | - Identify changes in accepted session volume.<br>- Review changes in representative workload over time.<br>- Monitor customer interaction activity trends. |
| Average session handle time | Shows the average session handle time trend during the selected period. | - Identify changes in handling duration.<br>- Review whether sessions take longer to complete.<br>- Monitor operational efficiency and workload trends. |

## Session metrics by agent

Use **Session metrics by agent** to review detailed metrics grouped by service representative.

### Session summary

On **Session summary**, compare session outcomes and volume for each service representative. Review volume, acceptance, rejection, timeout, transfer, and handling trends across representatives.

| Metric | Description |
|---|---|
| Total Sessions | Counts all sessions associated with the service representative. |
| Accepted Sessions | Counts sessions accepted by the service representative. |
| Session Rejected/Timed Out Rate | Percentage of sessions rejected or timed out. |
| Rejected Sessions | Counts sessions rejected by the service representative. |
| Session Rejected Rate | Percentage of offered sessions rejected by the service representative. |
| Timed Out Sessions | Counts sessions that timed out before the service representative accepted them. |
| Session Timeout Rate | Percentage of offered sessions that timed out. |
| Transferred Sessions | Counts sessions transferred by the service representative. |
| Transfer Rate (Agent) | Percentage of handled sessions transferred by the service representative. |
| Agent Avg Session Time | Average duration of sessions associated with the service representative. |
| Agent Avg Handle Time | Average time the service representative spent handling sessions. |
| Accept Rate | Percentage of offered sessions accepted by the service representative. |
| Total Sessions Handled | Number of sessions where the service representative responded or handled the interaction. |
| Open Sessions | Counts sessions still in progress. |

### Session details

On **Session details**, review time and messaging metrics for each service representative. Use them to analyze handling behavior, response patterns, and messaging volume.

| Metric | Description |
|---|---|
| Agent Avg Active Time | Average time the service representative actively engaged in a session. |
| Agent Avg Inactive Time | Average inactive time during sessions. |
| Agent Avg Wait Time | Average time from queue assignment to acceptance. |
| Agent Avg Active Chat Time | Average active chat time during sessions. |
| Agent Avg Talk Time | Average talk time for voice sessions. |
| Agent Avg Hold Time | Average hold time for voice sessions. |
| Agent Avg Wrapup Time | Average wrap-up time after sessions. |
| Agent Avg Response Time | Average response time during sessions. |
| Agent Avg First Response Time | Average time to send the first response. |
| Avg Incoming Messages | Average number of incoming messages per session. |
| Avg Outgoing Messages | Average number of outgoing messages per session. |
| Total Incoming Messages | Counts all incoming messages received in sessions. |
| Total Outgoing Messages | Counts all outgoing messages sent in sessions. |

### Consult and monitor

On **Consult and monitor**, review consult and monitor session metrics to assess how customer service representatives use these capabilities during customer interactions.

| Metric | Description |
|---|---|
| Consult sessions | Counts sessions with a consult. |
| Average consult time | Average consult-session duration. |
| Average consult wrap-up time | Average wrap-up time for consult sessions. |
| Consult requests accepted | Counts accepted consult requests. |
| Consult requests rejected | Counts rejected consult requests. |
| Monitor sessions | Counts monitor sessions. |
| Average monitor time | Average monitor-session duration. |

### Availability

On **Availability**, review duration metrics by representative presence state. Use them to identify availability patterns and assess how representative time is distributed across states.

| Metric | Description |
|---|---|
| Login duration (hrs) | Total time the service representative was signed in. |
| Available duration (hrs) | Time the service representative spent in an available state. |
| Busy duration (hrs) | Time the service representative spent in a busy state. |
| Away duration (hrs) | Time the service representative spent in an away state. |
| Offline duration (hrs) | Time the service representative spent offline. |

## Agent drill-down view

To review an individual representative:

1. Select a metric value for a service representative.
2. Select **Details**.

The drill-down view shows dashboard KPIs, trend charts, and daily metrics for the selected representative:

- KPI cards for accepted sessions, rejected sessions, transfer rate, average handle time, total sessions, and timed out sessions.
- Trend charts for accepted sessions and average session handle time.
- **Agent metrics by date** with the same tab structure as the main table: **Session summary**, **Session details**, **Consult/Monitor**, and **Availability**.
- An **Hourly details** option where available for the selected section.

## Agent metrics by date

Use **Agent metrics by date** to review daily breakdowns for the selected representative. It groups the metrics from **Session metrics by agent** by time period so you can identify trends, monitor operational performance, and investigate changes in representative activity over time.

## Personalize your dashboard

Save filtered views as bookmarks. Customize visualizations, metrics, filters, and layouts to focus on the data most relevant to your organization. Learn more in [Manage bookmarks for reports](/dynamics365/customer-service/use/manage-bookmarks) and [Customize visual display](/dynamics365/customer-service/use/customize-reports).
