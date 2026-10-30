---
title: AggVoiceConversationInsights table reference
description: Reference documentation for the AggVoiceConversationInsights aggregate table in the Dynamics 365 Customer Service Shared Analytics Platform data model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom:
  - bap-template
ai-usage: ai-assisted
---

# AggVoiceConversationInsights table reference

Use `AggVoiceConversationInsights` to report AI-generated voice behavior metrics for customer conversations. This preaggregated table supplements **AggConversation** with coaching and communication metrics that standard conversation analytics doesn't provide.

Analyze how conversations unfold, not just their outcomes, through speaking speed, talk-to-listen balance, customer monologue duration, pauses, and speaker-switch frequency.

Use this table to:

- Analyze communication patterns in voice conversations.
- Identify coaching opportunities for service representatives.
- Understand customer and service representative participation levels.
- Measure responsiveness and engagement during voice interactions.
- Supplement operational metrics with behavioral insights.

## Prerequisite

Enable Microsoft Conversation Intelligence to use these metrics. Without it, the table contains little or no data. The Voice Insights dashboard combines this table's metrics with **AggConversation** data for coaching reports.

## Grain and source

- **Grain:** One row per unique dimension combination per 15-minute interval.

```sql
GROUP BY
    DateTimeKey,
    QueueId,
    ChannelCode,
    ConversationStatusCode,
    AgentBusinessUnitId,
    ConversationDirectionCode,
    ActiveAgentId
```

### Source tables

| Source table | Purpose |
|---|---|
| FactVoiceConversationInsights | Primary source table for AI-generated voice insight metrics. Contains behavioral measures such as talking speed, talk-to-listen ratio, longest customer monologue, pause-before-speaking duration, speaker switches, ConversationId, and aggregation timestamps. |
| FactConversation | Provides conversation context used for reporting and filtering, including queue, channel, conversation status, direction, business unit, and active service representative information. |

### How rows are created

ETL combines voice conversations with matching dimension values into fixed 15-minute reporting intervals.

#### Group by

```sql
GROUP BY
    DateTimeKey,
    QueueId,
    ChannelCode,
    ConversationStatusCode,
    AgentBusinessUnitId,
    ConversationDirectionCode,
    ActiveAgentId
```

#### Example

Assume three voice conversations have the following attributes:

| Queue | Agent | Direction | Status | 15-minute interval |
|---|---|---|---|---|
| Support Voice | Agent A | Inbound | Closed | 09:00 |
| Support Voice | Agent A | Inbound | Closed | 09:00 |
| Support Voice | Agent A | Inbound | Closed | 09:00 |

The matching dimension values produce one aggregate row.

Example aggregated values:

```text
VoiceInsightCount = 3
TotalTalkingSpeed = 495
TotalTalkToListenRatio = 1.92
TotalLongestCustomerMonologueInSeconds = 288
```

Aggregation reduces storage and improves reporting performance while retaining trends and behavioral patterns across large conversation volumes.

## Dimension columns

Use the following dimensions to group and filter voice behavior by queue, service representative, business unit, and conversation type.

### Universal dimensions

| Column | Type | Source table | Source field or ETL logic | Description |
|---|---|---|---|---|
| DateTimeKey | BIGINT | FactVoiceConversationInsights | CreatedOnDateKey | Identifies the 15-minute UTC reporting interval for the aggregated record. Enables trend analysis and time-based reporting. |
| QueueId | STRING | FactConversation | QueueId (via ConversationId) | Identifies the queue associated with the conversation. Enables queue-level coaching, quality analysis, and operational reporting. |
| ChannelCode | INT | FactConversation | ChannelCode | Identifies the communication channel. This table contains voice interactions, but the column is retained for consistency across analytics tables and reporting models. |
| ConversationStatusCode | INT | FactConversation | ConversationStatusCode (via ConversationId) | Identifies the lifecycle status of the conversation, enabling analysis of voice insights by conversation outcome and resolution stage. |
| AgentBusinessUnitId | STRING | FactConversation | AgentBusinessUnitId (via ConversationId) | Identifies the business unit associated with the active service representative, supporting organizational reporting and comparison across business groups. |
| ConversationDirectionCode | INT | FactConversation | ConversationDirectionCode (via ConversationId) | Distinguishes inbound and outbound voice interactions so voice behaviors can be analyzed separately for customer-initiated and service representative-initiated conversations. |

### Table-specific dimensions

| Column | Type | Source table | Source field or ETL logic | Description |
|---|---|---|---|---|
| ActiveAgentId | STRING | FactConversation | ActiveAgentId (via ConversationId) | Identifies the last active service representative on the conversation. Enables coaching, quality review, and behavioral analysis at the individual service representative level. |

## Metric columns

Microsoft Conversation Intelligence generates these voice behavior values. Calculate averages at query time from the cumulative totals and VoiceInsightCount, rather than using stored averages. The Voice insight metrics reference article provides metric definitions and report calculations.

| Column | Type | Source table | Source field or ETL logic | Description |
|---|---|---|---|---|
| TotalLongestCustomerMonologueInSeconds | DOUBLE | FactVoiceConversationInsights | SUM(LongestCustomerMonologueInSeconds) | Stores cumulative uninterrupted customer speaking time across conversations. Used to identify interactions where customers speak for extended periods without interruption. |
| TotalPauseBeforeSpeakingInSeconds | DOUBLE | FactVoiceConversationInsights | SUM(PauseBeforeSpeakingInSeconds) | Stores cumulative service representative pause time before responding. Useful for understanding responsiveness and conversational pacing. |
| TotalSwitchesPerConversation | DOUBLE | FactVoiceConversationInsights | SUM(SwitchesPerConversation) | Stores cumulative speaker-turn switches across conversations. Higher values can indicate more interactive conversations and balanced participation. |
| TotalTalkingSpeed | DOUBLE | FactVoiceConversationInsights | SUM(TalkingSpeed) | Stores cumulative service representative speaking speed values measured in words per minute. Used to analyze communication pace and coaching opportunities. |
| TotalTalkToListenRatio | DOUBLE | FactVoiceConversationInsights | SUM(TalkToListenRatio) | Stores cumulative ratios comparing service representative speaking time with listening time. Supports assessment of conversational balance and engagement. |
| VoiceInsightCount | INT | FactVoiceConversationInsights | COUNT(*) | Stores the number of voice insight records represented in the aggregate row. Acts as the denominator for all voice insight averages. |

## Metadata columns

Use these system-generated columns for partitioning, refresh tracking, data lineage, and operational monitoring.

| Column | Type | Source table | Source field or ETL logic | Description |
|---|---|---|---|---|
| _AggregationDate | DATE | FactVoiceConversationInsights | CreatedOnDate | Stores the date associated with the aggregation interval. Used as a partition column and as a foreign key to DimDate. |
| _SourceRecordCount | INT | ETL | COUNT(*) | Stores the number of source voice insight records aggregated into the output row. Useful for validation and troubleshooting. |
| _LastRefreshedDateTimeUtc | TIMESTAMP | ETL | current_timestamp() | Stores the UTC timestamp of the most recent refresh operation. Used to verify data freshness and monitor ETL execution. |
