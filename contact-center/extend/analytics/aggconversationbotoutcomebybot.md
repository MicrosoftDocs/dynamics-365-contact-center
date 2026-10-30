---
title: AggConversationBotOutcomeByBot table reference
description: Reference for the bot-participation conversation aggregate contract in the Dynamics 365 Contact Center bot dashboard model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-generated
---

# AggConversationBotOutcomeByBot table reference

Use `AggConversationBotOutcomeByBot` to report outcomes, trends, and durations for one participating bot. A conversation contributes to every bot that participated, not just its first or last bot.

> [!IMPORTANT]
> This reference describes the table expected by the dashboard model; it doesn't confirm that the pipeline provisions it. Check [Bot table availability](../overview-data-model.md#bot-table-availability) before using this table in reports or Fabric integrations.

## Grain and contribution rule

Each distinct conversation and bot pair must contribute once to the conversation count. Aggregation groups these contributions by `BotId` and the common conversation-created time, queue, channel, status, direction, conversation type, and terminal outcome dimensions.

Repeated sessions with the same bot don't increase that bot's `ConversationCount`. A conversation involving two bots counts once for each, so counts are **not additive across bots**.

The model imports the Delta aggregate, not a conversation-detail fact, and doesn't expose `ConversationId`.

## Columns

The table has the same columns, semantic types, and meanings as [AggConversationBotOutcome](aggconversationbotoutcome.md#columns), plus `BotId`.

| Column | Semantic type | Description |
|---|---|---|
| `BotId` | string | Participating bot identifier. Relates to `DimBot.DimBotId`. |

`ConversationCount` counts each conversation and bot pair once. By contrast, `TotalOCSessionBotTimeMinutes` and `OCSessionBotTimeCount` retain qualifying bot-session-row weighting for that bot; they aren't deduplicated to one duration per conversation.

## Reporting considerations

Select one bot and use the model's routed **Total Bot Conversations** measure. Conversation deflection, escalation, and duration measures use the same routing.

Don't sum `ConversationCount` across bots for an overall total or arbitrary multi-bot selection. For an unfiltered overall value, use `AggConversationBotOutcome`. Explicit multiple-bot selections return blank from the routed measure.

For one bot and one topic, use [AggConversationBotOutcomeByBotTopic](aggconversationbotoutcomebybottopic.md) instead.

## Relationships

`BotId` has a many-to-one relationship to [DimBot](DimBot.md). The table also uses the common queue, channel, status, direction, conversation-type, terminal-label, and UTC-to-local date paths described in [AggConversationBotOutcome relationships](aggconversationbotoutcome.md#relationships).

`_AggregationDate` is a partition and incremental-refresh field, not a direct relationship to `DimDate.Date`. Don't create relationships between aggregate tables.

## Related information

[AggConversationBotOutcome table reference](aggconversationbotoutcome.md)  
[AggConversationBotOutcomeByBotTopic table reference](aggconversationbotoutcomebybottopic.md)  
[DimBot table reference](DimBot.md)  
