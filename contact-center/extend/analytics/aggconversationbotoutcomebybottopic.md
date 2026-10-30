---
title: AggConversationBotOutcomeByBotTopic table reference
description: Reference for the bot-topic participation conversation aggregate contract in the Dynamics 365 Contact Center bot dashboard model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-generated
---

# AggConversationBotOutcomeByBotTopic table reference

Use `AggConversationBotOutcomeByBotTopic` to report outcomes and trends for one selected bot and topic. Repeated sessions for the same bot and topic don't count as separate conversations.

> [!IMPORTANT]
> This reference describes the table expected by the dashboard model; it doesn't confirm that the pipeline provisions it. Check [Bot table availability](../overview-data-model.md#bot-table-availability) before using this table in reports or Fabric integrations.

## Grain and contribution rule

Each distinct combination of conversation, bot, and topic identifiers must contribute once to the conversation count. Aggregation groups these contributions by bot and topic identity, plus the common conversation-created time, queue, channel, status, direction, conversation type, and terminal outcome dimensions.

Repeated sessions for the same conversation, bot, and topic don't increase `ConversationCount`. Because a conversation can involve multiple topics, counts are **not additive across bots or topics**.

The model imports the Delta aggregate, not a conversation-detail fact, and doesn't expose `ConversationId`.

## Columns

The table has the same columns, semantic types, and meanings as [AggConversationBotOutcome](aggconversationbotoutcome.md#columns), plus these topic and bot columns.

| Column | Semantic type | Description |
|---|---|---|
| `BotId` | string | Participating bot identifier. |
| `BotTopicKey` | string | Stable bot and topic identity key. Relates to `DimBotTopic.BotTopicKey`. |
| `BotTopicId` | string | Source topic identifier, hidden in the semantic model. |
| `BotTopicName` | string | Topic display label. Use the shared dimension for report selections. |

Bot and topic IDs identify a topic, not its display name. Renaming a topic doesn't change its identity. Two topic IDs remain distinct even if their names match.

`TotalOCSessionBotTimeMinutes` and `OCSessionBotTimeCount` are weighted by qualifying bot-session rows within each bot and topic context. Unlike `ConversationCount`, these duration contributions aren't deduplicated.

## Reporting considerations

Select one bot and one `DimBotTopic.BotTopicKey` through the shared topic dimension. Use routed conversation measures; don't sum participation counts across topics.

Routed conversation measures return blank for explicit multiple-topic selections or a topic context without one bot. For overall totals, use [AggConversationBotOutcome](aggconversationbotoutcome.md). For one bot without a topic selection, use [AggConversationBotOutcomeByBot](aggconversationbotoutcomebybot.md).

## Relationships

`BotId` relates to [DimBot](DimBot.md), and `BotTopicKey` relates independently to [DimBotTopic](DimBotTopic.md), using many-to-one relationships.

The table also uses the common queue, channel, status, direction, conversation-type, terminal-label, and UTC-to-local date paths described in [AggConversationBotOutcome relationships](aggconversationbotoutcome.md#relationships).

Don't relate `DimBotTopic` to `DimBot` or create aggregate-to-aggregate relationships. `_AggregationDate` supports partitioning and incremental refresh, not a direct relationship to `DimDate.Date`.

## Related information

- [DimBotTopic table reference](DimBotTopic.md).
- [AggConversationBotOutcome table reference](aggconversationbotoutcome.md).
- [AggConversationBotOutcomeByBot table reference](aggconversationbotoutcomebybot.md).
