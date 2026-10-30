---
title: FactQueueSegment table reference
description: Reference information for the FactQueueSegment table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# FactQueueSegment table reference

Use `FactQueueSegment` to examine each queue's part in a conversation. A **queue segment** covers the time spent in a specific queue. The system creates a segment each time a conversation enters a queue, so a transfer from Queue A to Queue B produces **two** segments, one for each queue.

## Business value

Use this table to answer:

- How long did the customer wait in this specific queue before an agent accepted?
- Was this queue leg abandoned (the customer left before an agent accepted)?
- Was this the result of a transfer from another queue?
- How much handle time, hold time, and wrapup time occurred within this queue leg?
- Did the conversation transfer out of this queue?

Queues are supervisors' primary workforce management unit. This table provides the queue-leg details behind wait time, abandonment, and SLA metrics, and supplies `AggQueuePerformance` for aggregate queue reporting.

> **Segments vs. conversations:** Aggregated counts are **segment counts**, not distinct conversation counts. A transferred conversation counts once in each queue.

## Grain

The table stores one row per queue segment (`QueueSegmentId`).

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_queueextension | Provides queue segment identity, timing, durations, flags, and classification. |

## 1. Identity and foreign keys

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `QueueSegmentId` | STRING | `msdyn_queueextension` | `msdyn_queueextensionid` | Primary Key. |
| `ConversationId` | STRING | `msdyn_queueextension` | `msdyn_conversationid` | Foreign Key to FactConversation. |
| `QueueId` | STRING | `msdyn_queueextension` | `msdyn_queueid` | Foreign Key to DimQueue. |
| `SegmentStateCode` | INT | `msdyn_queueextension` | `statecode` | 0=Active (open), 1=Inactive (closed). |
| `SegmentState` | STRING | `HelperOptionSet` | Resolved from `statecode` via HelperOptionSet → `msdyn_queueextension.statecode` | Segment lifecycle state label (for example, "Active", "Inactive"). |
| `SegmentStatusCode` | INT | `msdyn_queueextension` | `statuscode` | Detailed segment status reason within the state. |
| `SegmentStatus` | STRING | `HelperOptionSet` | Resolved from `statuscode` via HelperOptionSet → `msdyn_queueextension.statuscode` | Segment status label. |

---

## 2. Timestamps

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `SegmentStartDateTime` | TIMESTAMP | `msdyn_queueextension` | `msdyn_starttime` | When conversation entered this queue (segment created). |
| `WaitStartedOnDateTime` | TIMESTAMP | `msdyn_queueextension` | `msdyn_waitstartedon` | When customer last started waiting. Initially equals SegmentStartDateTime. Updated on same-queue transfers (agent transfer within the same queue doesn't create a new segment—only resets the wait start). |
| `AgentAssignedOnDateTime` | TIMESTAMP | `msdyn_queueextension` | `msdyn_agentassignedon` | When agent was assigned in this queue. |
| `AgentAcceptedOnDateTime` | TIMESTAMP | `msdyn_queueextension` | `msdyn_agentacceptedon` | When agent accepted. NULL if not engaged. |
| `SegmentEndDateTime` | TIMESTAMP | `msdyn_queueextension` | `msdyn_endtime` | When this queue-leg ended. NULL if still active. |
| `ClosedOnDateTime` | TIMESTAMP | `msdyn_queueextension` | `msdyn_closedon` | When this queue-leg was closed. |

---

## 3. Duration metrics (seconds)

Durations apply to each queue leg. After a transfer, Q1 receives only the time spent in Q1, and Q2 receives only the time spent in Q2.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `FirstWaitTimeInSeconds` | BIGINT | `msdyn_queueextension` | `msdyn_firstwaittimeinseconds` | Wait from segment start to first agent acceptance. Key metric for ASA / SLA. |
| `HandleTimeInSeconds` | BIGINT | `msdyn_queueextension` | `msdyn_handletime` | Handle time in this queue-leg. |
| `TalkTimeInSeconds` | BIGINT | `msdyn_queueextension` | `msdyn_talktime` | Voice talk time in this queue-leg. |
| `HoldTimeInSeconds` | BIGINT | `msdyn_queueextension` | `msdyn_holdtime` | Hold time in this queue-leg. |
| `ActiveTimeInSeconds` | BIGINT | `msdyn_queueextension` | `msdyn_activetime` | Active engagement time in this queue-leg. |
| `InactiveTimeInSeconds` | BIGINT | `msdyn_queueextension` | `msdyn_inactivetime` | Inactive time in this queue-leg. |
| `ActiveWrapupTimeInSeconds` | BIGINT | `msdyn_queueextension` | `msdyn_activewrapuptime` | Active wrapup / after-call work time in this queue-leg. |
| `SegmentDurationInSeconds` | BIGINT | Calculated | `msdyn_endtime - msdyn_starttime` | Total segment duration from queue entry to queue exit. NULL if still active. |
| `FirstResponseTimeInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | From sessions in this segment: first session with valid FirstResponseTimeInSeconds. COALESCE(msdyn_responsetimeadjforoh, msdyn_responsetimenotadjforoh) / 1000. Skips rejected/bot sessions. | How long the customer waited for the first reply in this queue-leg. |
| `FirstResponseTimeAfterAcceptanceInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | Same first responding session → COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) / 1000 | How quickly the agent responded after accepting, in this queue-leg. |
| `TotalResponseTimeInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | SUM of COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) / 1000 across sessions linked to this segment WHERE value >= 0 | Sum of agent response times in this queue-leg. Numerator for avg response time. |
| `MessageBlockCount` | BIGINT | `msdyn_conversationmessageblock` | COUNT of blocks across sessions linked to this segment WHERE COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) IS NOT NULL AND >= 0 | Number of customer→agent message exchanges in this queue-leg. Denominator for avg response time. |
| `AvgResponseTimeInSeconds` | DOUBLE | Calculated | `TotalResponseTimeInSeconds / NULLIF(MessageBlockCount, 0)` | Average agent response time in this queue-leg. |

---

## 4. Flags

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IsEngaged` | BOOLEAN | `msdyn_queueextension` | TRUE if `msdyn_agentacceptedon IS NOT NULL` | Agent accepted this queue-leg. |
| `IsAbandoned` | BOOLEAN | `msdyn_queueextension` | `msdyn_isabandoned` | Customer abandoned before agent accepted. |
| `IsShortAbandoned` | BOOLEAN | Calculated (ETL) | `IsAbandoned = 1 AND FirstWaitTimeInSeconds <= DimQueue.ShortAbandonedThreshold`. **FALSE if threshold not configured.** | Abandoned within the queue's short-abandon window. Pre-computed via DimQueue join at ETL. |
| `IsInServiceLevel` | BOOLEAN | Calculated (ETL) | `IsEngaged = 1 AND FirstWaitTimeInSeconds <= DimQueue.ServiceLevelThreshold`. **TRUE if threshold not configured.** | Answered within the queue's SLA target. Pre-computed via DimQueue join at ETL. |
| `IsTransferredIn` | BOOLEAN | `msdyn_queueextension` | TRUE if `msdyn_sourcequeue IS NOT NULL` | Arrived via transfer from another queue. |
| `IsTransferredOut` | BOOLEAN | `msdyn_queueextension` | TRUE if `msdyn_targetqueue IS NOT NULL` | Transferred out to another queue. |

---

## 5. Classification

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `CreationReason` | STRING | `msdyn_queueextension` | `msdyn_creationreason` | Why this segment was created (new conversation, transfer, overflow). |
| `ClosureReason` | STRING | `msdyn_queueextension` | `msdyn_closurereason` | Why this segment ended. |

---

## 6. ETL and system

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `_StartDate` | DATE | `to_date(msdyn_queueextension.msdyn_starttime)` | Delta partition column. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | `current_timestamp()` | Pipeline refresh timestamp. |

---

## Source entities

| Dataverse entity | Contribution |
|-----------|---------------------|
| `msdyn_queueextension` | Identity, timestamps, durations, flags, classification |
| `msdyn_conversationmessageblock` | Response time metrics—joined via `msdyn_ocsession.msdyn_queueextensionid` (session → segment link) |
| `DimQueue` | `ShortAbandonedThreshold`, `ServiceLevelThreshold`—joined at ETL for `IsShortAbandoned` and `IsInServiceLevel` pre-computation |

> **Primary source:** `msdyn_queueextension` records aren't deduplicated. ETL joins `DimQueue` only to calculate threshold-based flags.

> **Feeds QueuePerformanceAnalytics:** At aggregation time, joins with `FactConversation` supply ChannelCode, ConversationStatusCode, and BusinessUnitId. A join with `DimQueue` supplies SLA and ShortAbandon thresholds.

## Filters

```sql
WHERE msdyn_queueextensionid IS NOT NULL
```

## Related tables

Use `FactQueueSegment` with these tables.

| Table | Purpose |
|-------|---------|
| AggQueuePerformance | Provides aggregated queue segment metrics. |
| DimQueue | Provides queue attributes and thresholds. |
| DimTimeZone | Supports local-time reporting. |
| FactConversation | Provides parent conversation context. |
| HelperOptionSet | Provides related lookup, detail, mapping, or aggregated data for reporting. |
