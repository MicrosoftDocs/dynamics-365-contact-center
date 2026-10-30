---
title: AggConversation table reference
description: Reference documentation for the AggConversation aggregate table in the Dynamics 365 Customer Service Shared Analytics Platform data model, including DAX measure patterns.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom:
  - bap-template
ai-usage: ai-assisted
---

# AggConversation table reference

Use `AggConversation` for conversation volume, abandonment, service level, time, quality, message, and session measures. Its preaggregated data supports performance reporting without querying individual `FactConversation` records.

## Grain and source

The table combines conversations with matching dimension values into fixed 15-minute reporting intervals.

- **Grain:** One row for each unique combination of dimension columns in a 15-minute interval.
- **Source table:** `FactConversation`.

Learn more about timestamp storage and local-time conversion in [Data model architecture](../overview-data-model.md#data-model-architecture).

### Group by

Each unique combination of these dimensions produces a separate row.

```sql
GROUP BY
    DateTimeKey,
    QueueId,
    ChannelCode,
    ConversationStatusCode,
    BusinessUnitId,
    ConversationDirectionCode,
    ConversationTypeCode,
    OverflowConditionCode,
    OverflowActionCode
```

### Source tables

| Source table | Purpose |
|----------|---------|
| `FactConversation` | Primary source table that stores conversation lifecycle, duration, message, sentiment, survey, and routing data. |
| `DimQueue` | Provides queue-related attributes and reporting context. |
| `DimChannel` | Provides channel metadata such as Chat, Voice, SMS, and social channels. |
| `DimConversationStatus` | Provides conversation status values used for reporting and filtering. |
| `DimConversationDirection` | Provides inbound and outbound conversation classifications. |
| `DimConversationType` | Provides conversation-type classifications. |
| `DimOverflowCondition` | Provides overflow trigger definitions. |
| `DimOverflowAction` | Provides overflow action definitions. |

### How the source data is used

ETL reads `FactConversation`, derives reporting dimensions, and aggregates metrics into 15-minute intervals. It stores counts and totals, not precalculated averages, so reports can calculate rates and averages at query time.

### Example: How a row is created

Assume three conversations have the following values:

| Queue | Channel | Direction | Status | 15-minute window |
|---------|---------|---------|---------|---------|
| Support | Chat | Inbound | Closed | 09:00–09:15 |
| Support | Chat | Inbound | Closed | 09:00–09:15 |
| Support | Chat | Inbound | Closed | 09:00–09:15 |

The matching dimension values produce one aggregate row.

Example aggregated values:

```text
IncomingConversations = 3
EngagedConversations = 2
AbandonedConversations = 1
TotalHandleTimeInSeconds = 1240
TotalWaitTimeInSeconds = 310
```

Aggregation reduces storage and improves query performance for dashboards and historical reports.

## Dimension columns

Use these dimensions to group and filter interactions by queue, channel, conversation type, routing outcome, and organizational ownership.

| Column | Type | Description |
|----------|----------|---------|
| `DateTimeKey` | BIGINT | Identifies the 15-minute UTC reporting interval for the aggregated row. This column enables time-based trending, filtering, and comparison across reporting periods. |
| `QueueId` | STRING | Identifies the queue associated with the conversation. Use this column to analyze workload, customer demand, and performance across queues. |
| `ChannelCode` | INT | Identifies the communication channel used for the conversation, such as chat, voice, SMS, or social messaging. |
| `ConversationStatusCode` | INT | Identifies the current or final conversation status and enables outcome-based reporting and analysis. |
| `BusinessUnitId` | STRING | Identifies the Dataverse business unit that owns the queue. Use this column to group conversation metrics by the queue's owning business unit. |
| `ConversationDirectionCode` | INT | Identifies whether the conversation was inbound or outbound, allowing separation of customer demand from proactive outreach activity. |
| `ConversationTypeCode` | INT | Identifies the conversation category used for routing and reporting segmentation. |
| `OverflowConditionCode` | INT | Identifies the condition that triggered overflow processing, such as queue length, capacity thresholds, or wait-time limits. This dimension helps analysts understand why standard routing could not continue. |
| `OverflowActionCode` | INT | Identifies the action taken when overflow occurred, such as transfer, callback, or reassignment. This dimension is useful for evaluating the effectiveness of overflow strategies. |

## Metric columns

Dashboards, reports, and custom analytics calculate averages and percentages from these counts and totals at query time. The conversation metrics reference article provides metric definitions and DAX calculations.

### Volume columns

Use these counts to report conversation demand and outcomes, including engagement, abandonment, transfers, service levels, and workload.

| Column | Type | Description |
|----------|----------|---------|
| `TotalConversations` | INT | Stores the total number of conversations represented by the aggregated row, regardless of outcome, direction, or routing path. |
| `IncomingConversations` | INT | Stores the number of inbound conversations offered to a service representative. This value serves as a primary workload indicator for contact center operations. |
| `OutgoingConversations` | INT | Stores the number of outbound conversations initiated by service representatives. |
| `EngagedConversations` | INT | Stores the number of incoming conversations accepted by a service representative. |
| `AbandonedConversations` | INT | Stores the number of conversations that ended before a service representative accepted the interaction. |
| `BotConversations` | INT | Stores the number of conversations in which a bot participated during the customer journey. |
| `TransferredConversations` | INT | Stores the number of conversations transferred at least once between queues or service representatives. |
| `CallbackConversations` | INT | Stores the number of conversations routed to callback processing because of overflow conditions or routing policies. |
| `ShortAbandonedConversations` | INT | Stores the number of conversations abandoned within the configured short-abandon threshold. |
| `InSLAConversations` | INT | Stores the number of conversations answered within the configured service-level threshold. |
| `RespondedConversations` | INT | Stores the number of conversations in which a service representative sent at least one response. |

### Service-level bucket columns

Use these counts to compare answer times for engaged conversations against common service-level thresholds and report their distribution.

| Column | Type | Description |
|----------|----------|---------|
| `AnsweredIn10Sec` | INT | Stores the number of engaged conversations answered within 10 seconds. |
| `AnsweredIn20Sec` | INT | Stores the number of engaged conversations answered within 20 seconds. |
| `AnsweredIn30Sec` | INT | Stores the number of engaged conversations answered within 30 seconds. |
| `AnsweredIn40Sec` | INT | Stores the number of engaged conversations answered within 40 seconds. |
| `AnsweredIn50Sec` | INT | Stores the number of engaged conversations answered within 50 seconds. |
| `AnsweredIn60Sec` | INT | Stores the number of engaged conversations answered within 60 seconds. |
| `AnsweredIn120Sec` | INT | Stores the number of engaged conversations answered within 120 seconds. |

### Abandonment bucket columns

Use these counts to identify abandonment timing, wait-time tolerance, and trends.

| Column | Type | Description |
|----------|----------|---------|
| `AbandonedIn10Sec` | INT | Stores the number of conversations abandoned within 10 seconds. |
| `AbandonedIn30Sec` | INT | Stores the number of conversations abandoned within 30 seconds. |
| `AbandonedIn60Sec` | INT | Stores the number of conversations abandoned within 60 seconds. |

### Duration and response columns

Use these cumulative values to analyze customer waits, service representative effort, responsiveness, conversation complexity, and overall duration. All durations are in seconds. Calculate averages at query time from the stored totals.

| Column | Type | Description |
|---|---|---|
| `TotalSpeedToAnswerInSeconds` | `BIGINT` | Stores the cumulative time customers waited before a service representative accepted incoming conversations. Used to calculate average speed of answer and service responsiveness metrics. |
| `TotalHandleTimeInSeconds` | `BIGINT` | Stores the total amount of time service representatives spent handling conversations, including active interaction and post-interaction activities. |
| `TotalWaitTimeInSeconds` | `BIGINT` | Stores the cumulative customer wait time across conversations before engagement or resolution. |
| `TotalTalkTimeInSeconds` | `BIGINT` | Stores the total active voice conversation time between customers and service representatives. |
| `TotalHoldTimeInSeconds` | `BIGINT` | Stores the total amount of time customers spent on hold during voice interactions. |
| `TotalActiveTimeInSeconds` | `BIGINT` | Stores the cumulative time conversations were actively progressing through customer-service interactions. |
| `TotalInactiveTimeInSeconds` | `BIGINT` | Stores the cumulative time conversations remained inactive because of customer inactivity, waiting periods, or other non-active states. |
| `TotalWrapupTimeInSeconds` | `BIGINT` | Stores the total time spent completing post-conversation activities such as documentation, disposition, and follow-up actions. |
| `TotalActiveWrapupTimeInSeconds` | `BIGINT` | Stores the portion of wrap-up time during which service representatives actively performed post-conversation work. |
| `TotalActiveChatTimeInSeconds` | `BIGINT` | Stores the total time spent actively participating in digital messaging conversations. |
| `TotalConversationDurationInSeconds` | `BIGINT` | Stores the cumulative end-to-end duration of conversations from initiation through completion. |
| `TotalCustomerEffortInSeconds` | `BIGINT` | Stores the total amount of time customers spent completing interactions, providing an indicator of overall customer effort. |
| `TotalFirstResponseTimeInSeconds` | `DOUBLE` | Stores the cumulative time between conversation initiation and the first response sent by a service representative. |
| `TotalResponseTimeInSeconds` | `DOUBLE` | Stores the cumulative response time across all service representative-to-customer message exchanges. |
| `MessageBlockCount` | `INT` | Stores the total number of message-response exchanges used to calculate response-time metrics. |
| `TotalFirstResponseTimeAfterAcceptanceInSeconds` | `DOUBLE` | Stores the cumulative time between conversation acceptance and the first response sent by a service representative. |
| `FirstResponseTimeAfterAcceptanceCount` | `INT` | Stores the number of conversations that contributed to first-response-after-acceptance calculations. |
| `TotalTimeToAbandonInSeconds` | `BIGINT` | Stores the cumulative amount of time customers waited before abandoning conversations. |

### Quality and sentiment columns

Use customer feedback scores and AI-generated sentiment for customer experience analysis, quality monitoring, satisfaction reports, and trends. Calculate averages during reporting from the stored totals and counts.

| Column | Type | Description |
|---|---|---|
| `Survey_TotalCSATScore` | `DOUBLE` | Stores the cumulative customer satisfaction (CSAT) score from survey responses associated with conversations. |
| `Survey_CSATResponseCount` | `INT` | Stores the number of survey responses included in customer satisfaction calculations. |
| `TotalSentimentPulse` | `DOUBLE` | Stores the cumulative AI-generated sentiment score calculated from conversation interactions. |
| `SentimentPulseCount` | `INT` | Stores the number of sentiment observations included in AI-generated sentiment calculations. |
| `Survey_TotalSentimentScore` | `DOUBLE` | Stores the cumulative sentiment score collected through customer surveys. |
| `Survey_SentimentScoreCount` | `INT` | Stores the number of survey sentiment responses represented in the aggregated row. |
| `PositiveSentimentCount` | `INT` | Stores the number of conversations classified with positive sentiment. |
| `NeutralSentimentCount` | `INT` | Stores the number of conversations classified with neutral sentiment. |
| `NegativeSentimentCount` | `INT` | Stores the number of conversations classified with negative sentiment. |
| `Survey_TotalNPSScore` | `DOUBLE` | Stores the cumulative Net Promoter Score (NPS) from customer survey responses. |
| `Survey_NPSResponseCount` | `INT` | Stores the number of Net Promoter Score responses used in NPS calculations. |

### Message and session columns

Use these counts to assess communication volume, engagement, and conversation complexity, including the routing sessions needed to complete interactions.

| Column | Type | Description |
|---|---|---|
| `TotalIncomingMessages` | `INT` | Stores the total number of customer messages received across aggregated conversations. |
| `TotalOutgoingMessages` | `INT` | Stores the total number of messages sent by service representatives across aggregated conversations. |
| `TotalSessionCount` | `INT` | Stores the total number of sessions associated with conversations, including transfers and multiple routing legs. |
| `TotalAgentSessionCount` | `INT` | Stores the total number of service representative sessions associated with conversations, providing insight into routing complexity and service representative involvement. |

## Metadata columns

Use these system-generated columns for partitioning, data lineage, refresh monitoring, troubleshooting, and data quality and freshness checks, rather than typical business reporting.

| Column | Type | Description |
|----------|----------|---------|
| `_AggregationDate` | DATE | Stores the date associated with the aggregation interval. The column is used for table partitioning and joins to the date dimension. |
| `_SourceRecordCount` | INT | Stores the number of source records combined to create the aggregated output row. Use this column for validation and data-quality investigations. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | Stores the UTC timestamp of the most recent table refresh. Use this column to verify data freshness and monitor ETL execution. |

## Overflow filtering logic

Overflow occurs when capacity constraints, queue thresholds, service-level targets, or other configured conditions prevent standard routing. Use `OverflowConditionCode` and `OverflowActionCode` to identify the trigger and resulting routing decision.

Abandonment metrics generally exclude overflow conversations because overflow is a routing outcome, not customer abandonment. For example, an overflow conversation redirected to a callback is typically not counted as abandoned.

Overflow remains part of the aggregation grain, so you can:

- Include overflow conversations in routing analysis.
- Exclude overflow conversations from abandonment reporting.
- Compare overflow triggers and overflow actions.
- Evaluate the effectiveness of overflow policies and routing strategies.
