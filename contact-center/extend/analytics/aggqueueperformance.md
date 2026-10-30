---
title: AggQueuePerformance table (Dynamics 365 Customer Service analytics)
description: Reference information for the AggQueuePerformance table in the Shared Analytics Platform data model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-assisted
---

# AggQueuePerformance table

Use `AggQueuePerformance` to report queue volume, abandonment, service levels, transfers, and handling time from preaggregated data.

The source is the **Segment (msdyn_queueextension)** entity. Each source record represents a **queue segment**, one queue interaction within a conversation.

A conversation that transfers across queues can produce multiple records. Incoming, engaged, and abandoned metrics therefore count **queue segments**, not distinct conversations.

The table is optimized for **queue-level reporting** on routing efficiency, service-level performance, and workload distribution.

### Source tables

These sources combine segment activity, conversation context, and queue configuration for reporting on workload, responsiveness, service levels, transfers, customer feedback, and outcomes.

| Source table | Purpose |
|---|---|
| `FactQueueSegment` | Primary source table for queue-segment activity. Each record represents a queue leg within a conversation and contains queue-specific lifecycle, wait-time, handle-time, transfer, and engagement information. |
| `FactConversation` | Provides conversation-level attributes that aren't stored on queue segments, including channel, direction, conversation status, service representative business unit, sentiment, and survey values. These attributes are joined by `ConversationId` and denormalized into the aggregate table. |
| `DimQueue` | Provides queue configuration data used during aggregation, including service-level thresholds and short-abandon settings that determine SLA and abandonment classifications. |

### How rows are created

ETL combines queue segments with matching dimension values into fixed 15-minute reporting intervals.

#### Group by

```sql
GROUP BY
    DateTimeKey,
    QueueId,
    ChannelCode,
    ConversationStatusCode,
    BusinessUnitId,
    ConversationDirectionCode,
    SegmentStateCode,
    SegmentState,
    SegmentStatusCode,
    SegmentStatus
```

#### Example

Assume three queue segments have the following values:

| Queue | Channel | Direction | Segment status | 15-minute interval |
|---|---|---|---|---|
| Support | Chat | Inbound | Completed | 09:00 |
| Support | Chat | Inbound | Completed | 09:00 |
| Support | Chat | Inbound | Completed | 09:00 |

The matching dimension values produce one aggregate row.

Example output:

```text
TotalSegments = 3
EngagedSegments = 2
AbandonedSegments = 1
TotalHandleTimeInSeconds = 1240
TotalFirstWaitTimeInSeconds = 310
```

Aggregation reduces storage and improves dashboard and report performance while preserving analytical accuracy.

## Dimension columns

Use these dimensions to group and filter queue performance by queue, channel, direction, conversation status, and segment lifecycle.

| Column | Type | Source | Source field or ETL logic | Description |
|---|---|---|---|---|
| `DateTimeKey` | `BIGINT` | `FactQueueSegment` | Derived from `SegmentStartDateTime` | Identifies the 15-minute UTC reporting interval for the aggregated row. This column supports trend analysis, period comparisons, and time-based reporting. |
| `QueueId` | `STRING` | `FactQueueSegment` | `QueueId` | Identifies the queue associated with the segment. This column is used to analyze workload, responsiveness, abandonment, and service-level performance across queues. |
| `ChannelCode` | `INT` | `FactConversation` | Joined through `ConversationId` | Identifies the communication channel, such as chat, voice, SMS, or social messaging, enabling channel-based reporting and comparison. |
| `ConversationStatusCode` | `INT` | `FactConversation` | Joined through `ConversationId` | Identifies the conversation status associated with the segment, allowing reports to analyze queue activity by conversation outcome and lifecycle stage. |
| `BusinessUnitId` | `STRING` | `FactConversation` | Joined through `ConversationId` | Identifies the Dataverse business unit that owns the queue. Use this column for organizational reporting on queue-segment performance. |
| `ConversationDirectionCode` | `INT` | `FactConversation` | Joined through `ConversationId` | Identifies whether the conversation was inbound or outbound, helping distinguish customer demand from proactive outreach activities. |
| `SegmentStateCode` | `INT` | `FactQueueSegment` | `SegmentStateCode` | Stores the lifecycle state code of the queue segment. This value is used for filtering and lifecycle analysis. |
| `SegmentState` | `STRING` | `FactQueueSegment` | `SegmentState` | Stores the human-readable lifecycle state label used in reports and filters. |
| `SegmentStatusCode` | `INT` | `FactQueueSegment` | `SegmentStatusCode` | Identifies the detailed segment status reason and provides additional insight into queue-segment outcomes. |
| `SegmentStatus` | `STRING` | `FactQueueSegment` | `SegmentStatus` | Displays the readable segment status label used in dashboard filters, reporting, and troubleshooting. |

## Metric columns

Calculate engagement and abandonment rates, service levels, wait and handle times, and customer experience metrics from these counts and totals. The table doesn't store percentages or averages. The Queue segment metrics reference article provides metric definitions and DAX calculations.

### Volume columns

Use these counts to assess queue demand, workload, engagement, abandonment, transfers, and service levels.

| Column | Type | Source | Source field or ETL logic | Description |
|---|---|---|---|---|
| `TotalSegments` | `INT` | `FactQueueSegment` | `COUNT(*)` | Stores the total number of queue segments that entered the queue during the reporting interval. Provides the primary measure of queue workload and demand. |
| `EngagedSegments` | `INT` | `FactQueueSegment` | `SUM(CASE IsEngaged = 1)` | Stores the number of queue segments associated with conversations accepted by a service representative. Indicates handled queue demand. |
| `AbandonedSegments` | `INT` | `FactQueueSegment` | `SUM(CASE IsAbandoned = 1)` | Stores the number of queue segments that ended before a service representative accepted the interaction. Used to evaluate queue abandonment patterns. |
| `ShortAbandonedSegments` | `INT` | `FactQueueSegment` | `SUM(CASE IsShortAbandoned = 1)` | Stores the number of segments abandoned within the configured short-abandon threshold. Helps distinguish immediate disconnects from longer queue waits. |
| `InSLASegments` | `INT` | `FactQueueSegment` | `SUM(CASE IsInServiceLevel = 1)` | Stores the number of queue segments answered within the configured service-level target. Used as the basis for SLA reporting. |
| `TransferredInSegments` | `INT` | `FactQueueSegment` | `SUM(CASE IsTransferredIn = 1)` | Stores the number of queue segments received from another queue. Helps identify transferred workload entering the queue. |
| `TransferredOutSegments` | `INT` | `FactQueueSegment` | `SUM(CASE IsTransferredOut = 1)` | Stores the number of queue segments transferred to another queue. Helps identify queues that frequently reroute work. |

### Duration and response columns

Use these cumulative values to measure customer waits, service representative effort, responsiveness, and interaction complexity. All durations are in seconds. Reports calculate averages at query time from the stored totals.

| Column | Type | Source field or ETL logic | Description |
|---|---|---|---|
| `TotalFirstWaitTimeInSeconds` | `BIGINT` | `SUM(FirstWaitTimeInSeconds)` | Stores cumulative customer wait time before a conversation is accepted by a service representative while in the queue. |
| `WaitTimeCount` | `INT` | Count where `FirstWaitTimeInSeconds` isn't null and `IsEngaged = 1` | Stores the number of engaged segments that contributed wait-time values. Used as a denominator when calculating average wait-time metrics. |
| `TotalHandleTimeInSeconds` | `BIGINT` | `SUM(HandleTimeInSeconds)` | Stores the cumulative handling effort associated with engaged queue segments. |
| `TotalTalkTimeInSeconds` | `BIGINT` | `SUM(TalkTimeInSeconds)` | Stores the cumulative voice conversation time between customers and service representatives. |
| `TotalHoldTimeInSeconds` | `BIGINT` | `SUM(HoldTimeInSeconds)` | Stores the cumulative time customers spent on hold while interacting with a service representative. |
| `TotalActiveTimeInSeconds` | `BIGINT` | `SUM(ActiveTimeInSeconds)` | Stores the total time interactions were actively progressing. |
| `TotalInactiveTimeInSeconds` | `BIGINT` | `SUM(InactiveTimeInSeconds)` | Stores the total inactive time associated with queue segments. |
| `TotalActiveWrapupTimeInSeconds` | `BIGINT` | `SUM(ActiveWrapupTimeInSeconds)` | Stores the cumulative active wrap-up effort performed after interactions are completed. |
| `TotalResponseTimeInSeconds` | `DOUBLE` | `SUM(TotalResponseTimeInSeconds)` | Stores cumulative response time across all message exchanges associated with queue segments. |
| `MessageBlockCount` | `INT` | `SUM(MessageBlockCount)` | Stores the total number of message-exchange blocks used to calculate response-time metrics. |
| `TotalFirstResponseTimeInSeconds` | `DOUBLE` | `SUM(FirstResponseTimeInSeconds)` | Stores cumulative time between the customer's first message and the service representative's first response. |
| `FirstResponseTimeCount` | `INT` | Count where `FirstResponseTimeInSeconds` isn't null | Stores the number of segments that contributed first-response-time values. |
| `TotalFirstResponseTimeAfterAcceptanceInSeconds` | `DOUBLE` | `SUM(FirstResponseTimeAfterAcceptanceInSeconds)` | Stores cumulative time between service representative acceptance and the first response sent after acceptance. |
| `FirstResponseTimeAfterAcceptanceCount` | `INT` | Count where `FirstResponseTimeAfterAcceptanceInSeconds` isn't null | Stores the number of segments that contributed first-response-after-acceptance values. |

### Quality columns

Survey values join to queue segments through `ConversationId`. A conversation can move through multiple queues, so the same customer feedback can contribute to multiple segments.

| Column | Type | Source field or ETL logic | Description |
|---|---|---|---|
| `Survey_TotalCSATScore` | `DOUBLE` | `SUM(Survey_CSATScore)` through `ConversationId` | Stores the cumulative customer satisfaction (CSAT) score associated with queue segments. |
| `Survey_CSATResponseCount` | `INT` | Count where `Survey_CSATScore` isn't null | Stores the number of customer satisfaction survey responses represented in the aggregated row. |
| `Survey_TotalNPSScore` | `DOUBLE` | `SUM(Survey_NPSScore)` through `ConversationId` | Stores the cumulative Net Promoter Score (NPS) associated with queue segments. |
| `Survey_NPSResponseCount` | `INT` | Count where `Survey_NPSScore` isn't null | Stores the number of NPS survey responses represented in the aggregated row. |

## Metadata columns

Use these system-generated columns for partitioning, refresh monitoring, data lineage, troubleshooting, and data quality checks, rather than typical business reporting.

| Column | Type | Source | Source field or ETL logic | Description |
|---|---|---|---|---|
| `_AggregationDate` | `DATE` | `FactQueueSegment` | Date portion of `SegmentStartDateTime` | Stores the date associated with the aggregation interval. Used for partitioning and joins to `DimDate`. |
| `_SourceRecordCount` | `INT` | ETL | `COUNT(*)` | Stores the number of source segment records combined to create the aggregated row. |
| `_LastRefreshedDateTimeUtc` | `TIMESTAMP` | ETL | `current_timestamp()` | Stores the UTC timestamp of the most recent table refresh and supports refresh monitoring and data-quality validation. |
