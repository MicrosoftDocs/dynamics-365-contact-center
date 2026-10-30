---
title: AggBotSession table reference
description: Reference for the AggBotSession aggregate table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-assisted
---

# AggBotSession table reference

> [!NOTE]
> Copilot Studio bot is renamed as Copilot agent (agent or AI agent). Human agent is now renamed as customer service representative (service representative or representative). You might come across references to the old and new terms while we update the product UI, documentation, and training content.


Use `AggBotSession` to report session volume, engagement, outcomes, duration, and customer satisfaction for bots and Copilot Studio agents. The table stores preaggregated session data.

> [!IMPORTANT]
> - In this context, bot refers to 
> - This implementation supports standard bot analytics, but not advanced bot analytics or intent enrichment. The bot dashboard model expects additional columns and separate conversation outcome aggregates. Learn more in [Bot table availability](../overview-data-model.md#bot-table-availability).

## Pipeline grain and source

The table combines bot sessions with matching dimension values into fixed 15-minute reporting intervals.

- **Grain:** One row for each unique combination of dimension columns in a 15-minute interval.
- **Source table:** `FactBotSession`.

Learn more about timestamp storage and local-time conversion in [Data model architecture](../overview-data-model.md#data-model-architecture).

### Group by

```sql
GROUP BY
    DateTimeKey,
    QueueId,
    ChannelCode,
    ConversationStatusCode,
    ConversationDirectionCode,
    BotId,
    BotTopicName,
    SessionOutcome,
    SessionOutcomeReason,
    IsBotEngaged,
    ConversationOutcome
```

## Dimension columns

| Column | Type | Source field | Description |
|---|---|---|---|
| `DateTimeKey` | BIGINT | 15-minute bucket derived from `SessionStartTime` | Identifies the UTC reporting interval. If the session start is null, midnight on `_StartDate` is used. |
| `QueueId` | STRING | `DimQueueId` | Queue associated with the bot session. |
| `ChannelCode` | INT | `ChannelId` | Conversation channel code. |
| `ConversationStatusCode` | INT | `StatusId` | Conversation status code. |
| `ConversationDirectionCode` | INT | `IsOutbound` | Conversation direction code. |
| `BotId` | STRING | `BotId` | Bot GUID. Foreign key to `DimBot`. |
| `BotTopicName` | STRING | `BotTopicName` | Topic that handled the bot session. |
| `SessionOutcome` | BIGINT | `SessionOutcome` | Bot session outcome option-set code. |
| `SessionOutcomeReason` | BIGINT | `SessionOutcomeReason` | Bot session outcome-reason option-set code. |
| `IsBotEngaged` | INT | `IsBotEngaged` | Indicates whether the bot engaged the customer. |
| `ConversationOutcome` | STRING | `ConversationOutcome` | Conversation-level outcome, such as `Bot deflected` or `Bot escalated`. |

Group by `BotTopicName` for topic-level analysis. It's part of the grain, so a large number of distinct topic names might increase the aggregate row count.

## Metric columns

Calculate percentages and averages at query time from the stored additive counts and totals.

### Volume and outcome columns

| Column | Type | Source logic | Description |
|---|---|---|---|
| `BotSessionCount` | BIGINT | `COUNT(*)` | Total bot sessions. Denominator for session-level rates. |
| `EngagedSessionCount` | BIGINT | Sum of `IsBotEngaged` | Sessions in which the bot engaged the customer. |
| `AbandonedSessionCount` | BIGINT | Count where `SessionOutcome = 419550003` | Sessions abandoned by the customer. |
| `EscalatedSessionCount` | BIGINT | Count where `SessionOutcome = 419550002` | Sessions escalated to a service representative or external number. |
| `ResolvedSessionCount` | BIGINT | Count where `SessionOutcome = 419550001` | Sessions resolved by the bot. |
| `BotConversationCount` | BIGINT | Sum of `IsPrimaryBotSessionOfConversation` | Additive conversation count attributed to the earliest bot session. |

### Duration and satisfaction columns

| Column | Type | Source logic | Description |
|---|---|---|---|
| `TotalDurationInSeconds` | BIGINT | Sum of `DurationInSeconds` | Total bot session duration used to calculate average bot time. |
| `DurationSessionCount` | BIGINT | Count of sessions with a duration | Denominator for average bot session duration. |
| `TotalOCSessionBotTimeMinutes` | BIGINT | Sum of closed omnichannel session durations | Total omnichannel session time in minutes used for average deflection and escalation time. |
| `OCSessionBotTimeCount` | BIGINT | Count of closed omnichannel sessions | Denominator for average deflection and escalation time. |
| `TotalCSATScore` | BIGINT | Sum of `CSATScore` | Total customer satisfaction score. |
| `CSATResponseCount` | BIGINT | Count where `CSATScore > 0` | Number of sessions with a customer satisfaction response. |

You can filter the pipeline's compatibility count by `ConversationOutcome`, but it doesn't reproduce conversation counts for participating bots or topics. The dashboard doesn't import `BotConversationCount`; it uses the [conversation outcome aggregate family](aggconversationbotoutcome.md) for conversation measures.

## Metadata columns

| Column | Type | Description |
|---|---|---|
| `_AggregationDate` | DATE | Date associated with the aggregation interval. Delta Lake partition column. |
| `_SourceRecordCount` | INT | Number of `FactBotSession` records included in the aggregate row. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | UTC timestamp of the most recent table refresh. |

## Conversation-count attribution

`BotConversationCount` attributes each identified conversation to its earliest bot session. This additive marker counts each conversation once across the complete aggregate without scanning the detail fact. Date filters use that session's reporting interval, which might differ from the conversation-created interval.

If you group by an attribute that can change between sessions, such as queue, bot, topic, outcome reason, or engagement, only the earliest session's value receives the conversation count. Don't use this count in place of the dashboard's participation-based conversation measures.

## Dashboard model contract

The dashboard imports the session columns and metrics listed in the preceding section, except `BotConversationCount`. It also expects these columns, which the pipeline schema described here doesn't produce.

| Additional column | Semantic type | Purpose |
|---|---|---|
| `ConversationTypeCode` | int64 | Filters sessions through `DimConversationType`. |
| `BotTopicKey` | string | Relates sessions to the shared `DimBotTopic` identity. |
| `BotTopicId` | string | Source topic identifier. |

Check the actual table schema before refreshing a custom model; the baseline pipeline output might not meet the expanded import contract. For conversation counts, rates, and deflection or escalation times, use [AggConversationBotOutcome](aggconversationbotoutcome.md) and its participation tables.

## Relationships

The bot dashboard model uses many-to-one, single-direction relationships to these dimensions and its UTC date proxy:

| AggBotSession column | Dimension column |
|---|---|
| `DateTimeKey` | `ProxyUtcDateId.UtcDateTimeKey` |
| `QueueId` | `DimQueue.QueueId` |
| `ChannelCode` | `DimChannel.ChannelCode` |
| `ConversationStatusCode` | `DimConversationStatus.ConversationStatusCode` |
| `ConversationDirectionCode` | `DimConversationDirection.ConversationDirectionCode` |
| `ConversationTypeCode` (dashboard contract only) | `DimConversationType.ConversationTypeCode` |
| `BotId` | `DimBot.DimBotId` |
| `BotTopicKey` (dashboard contract only) | `DimBotTopic.BotTopicKey` |

Filter dates and hours through `ProxyUtcDateId`, `DimTimeZone`, and `DimDate`. Use `_AggregationDate` only for partitioning and incremental refresh, not a direct relationship to `DimDate.Date`, whose values repeat at 15-minute grain.

Don't create a fact-to-fact relationship between **AggBotSession** and conversation or session fact tables.

## Related information

- [FactBotSession table reference](FactBotSession.md)
- [DimBot table reference](DimBot.md)
- [DimBotTopic table reference](DimBotTopic.md)
- [AggConversationBotOutcome table reference](aggconversationbotoutcome.md)
- [Bot metrics reference for Shared Analytics Platform](../../use/bot-metrics.md)
