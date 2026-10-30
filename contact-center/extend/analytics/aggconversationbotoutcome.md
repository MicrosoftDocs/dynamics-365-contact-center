---
title: AggConversationBotOutcome table reference
description: Reference for the AggConversationBotOutcome table contract in the Dynamics 365 Contact Center bot dashboard model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-generated
---

# AggConversationBotOutcome table reference

Use `AggConversationBotOutcome` to report overall bot conversation counts, deflection and escalation rates, and terminal outcomes. The dashboard imports it separately from session aggregates, keeping conversation metrics independent of the earliest bot session's attributes.

> [!IMPORTANT]
> This reference describes the table expected by the dashboard model; it doesn't confirm that the pipeline provisions it. Check [Bot table availability](../overview-data-model.md#bot-table-availability) before using this table in reports or Fabric integrations.

## Grain and source contract

Each row groups conversations with the same 15-minute UTC conversation-created key, queue, channel, status, direction, conversation type, conversation outcome, terminal outcome, terminal reason, and terminal outcome mapping key.

Before aggregation, each eligible conversation must contribute once to the conversation count. The model imports the resulting Delta aggregate, not a conversation-detail fact, and doesn't expose `ConversationId`.

Use `CreatedOnDateKey` for conversation creation time, not bot session start. Use `_AggregationDate` for partitioning and incremental refresh.

## Columns

These are Power BI semantic types: `int64` represents whole numbers without distinguishing physical `INT` from `BIGINT`; `dateTime` represents imported dates and timestamps.

| Column | Semantic type | Description |
|---|---|---|
| `CreatedOnDateKey` | int64 | Canonical 15-minute UTC conversation-created key. |
| `QueueId` | string | Conversation queue key. |
| `ChannelCode` | int64 | Conversation channel code. |
| `ConversationStatusCode` | int64 | Conversation status code. |
| `ConversationDirectionCode` | int64 | Conversation direction code. |
| `ConversationTypeCode` | int64 | Conversation type code. |
| `ConversationOutcome` | string | Hidden classification used by measures: `Bot deflected` or `Bot escalated`. |
| `LastSessionOutcome` | int64 | Terminal conversation outcome code. Don't substitute the bot session outcome code. |
| `LastSessionOutcomeReason` | int64 | Terminal conversation outcome-reason code. |
| `TerminalOutcomeAttributeMappingId` | string | Language-neutral key for localized terminal outcome and reason labels. |
| `ConversationCount` | int64 | Number of conversation contributions in the group. |
| `TotalOCSessionBotTimeMinutes` | int64 | Total qualifying omnichannel session duration in whole minutes. |
| `OCSessionBotTimeCount` | int64 | Number of qualifying internal bot-session rows with a nonblank omnichannel session duration. |
| `_SourceRecordCount` | int64 | Aggregation diagnostics count. |
| `_LastRefreshedDateTimeUtc` | dateTime | UTC refresh timestamp. |
| `_AggregationDate` | dateTime | Date used for partitioning and incremental refresh. |

The duration numerator and denominator are weighted by qualifying bot-session rows, not deduplicated conversations. Multiple qualifying rows can contribute duration for one conversation.

## Measures and filter scope

**Total Bot Conversations** selects its source table based on your bot and topic selection.

| Filter scope | Conversation-count source |
|---|---|
| No bot or topic selection. | `AggConversationBotOutcome`. |
| One bot, without a topic selection. | [AggConversationBotOutcomeByBot](aggconversationbotoutcomebybot.md). |
| One bot and one topic identity. | [AggConversationBotOutcomeByBotTopic](aggconversationbotoutcomebybottopic.md). |
| Explicit multiple-bot or unsupported topic selection. | The measure returns blank rather than an invalid participation total. |

**Conversation Deflected** and **Conversation Escalated** filter the selected source's count by `ConversationOutcome`. Each rate divides by **Total Bot Conversations**. **Sessions per Conversation** divides session volume by the same routed conversation count.

**Avg Deflection Time (min)** and **Avg Escalation Time (min)** use the duration numerator and denominator from the corresponding routed source. Don't calculate an overall total by summing bot or topic participation counts.

## Relationships

The dashboard model uses these filter paths:

| Table column | Related column |
|---|---|
| `CreatedOnDateKey` | `ProxyUtcDateId.UtcDateTimeKey`. |
| `QueueId` | `DimQueue.QueueId`. |
| `ChannelCode` | `DimChannel.ChannelCode`. |
| `ConversationStatusCode` | `DimConversationStatus.ConversationStatusCode`. |
| `ConversationDirectionCode` | `DimConversationDirection.ConversationDirectionCode`. |
| `ConversationTypeCode` | `DimConversationType.ConversationTypeCode`. |
| `TerminalOutcomeAttributeMappingId` | `DimBotTerminalOutcomeProperty.TerminalOutcomeAttributeMappingId`. |

Terminal labels use a many-to-many relationship because each mapping key has multiple language rows in the property table. `LocalizationLanguageLocale` supplies the language filter. Learn more in [DimBotTerminalOutcomeProperty](DimBotTerminalOutcomeProperty.md).

Filter dates and hours through `ProxyUtcDateId`, `DimTimeZone`, and `DimDate`. Don't relate `_AggregationDate` directly to `DimDate.Date`; date values repeat at the dimension's 15-minute grain.

This overall aggregate has no direct relationship to `DimBot` or `DimBotTopic`. Use routed measures to filter by bot or topic through the participation tables. Don't create relationships between aggregates.

## Related information

- [AggBotSession table reference](aggbotsession.md).
- [AggConversationBotOutcomeByBot table reference](aggconversationbotoutcomebybot.md).
- [AggConversationBotOutcomeByBotTopic table reference](aggconversationbotoutcomebybottopic.md).
