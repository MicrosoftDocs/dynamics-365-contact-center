---
title: DimBot table reference
description: Reference for the DimBot table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-assisted
---

# DimBot table reference

Use `DimBot` to filter bot analytics by bot name, state, or status. The table maps bot GUIDs to display names and status information.

## Business value

Use the state and status codes to analyze active and inactive bots.

**Reporting usage:** Relate `DimBotId` to `BotId` in `AggBotSession`. The expanded bot dashboard model also relates this dimension to `AggConversationBotOutcomeByBot` and `AggConversationBotOutcomeByBotTopic`. `FactBotSession` carries the same bot key but isn't imported into that dashboard model.

Learn more in [Bot table availability](../overview-data-model.md#bot-table-availability) about the difference between generated pipeline tables and additional dashboard model contracts.

## Grain

The table stores one row per bot, retaining the most recently modified version when the source contains multiple records.

## Source tables

| Source table | Purpose |
|---|---|
| `bot` | Provides bot identity, name, state, and status information. |

## Columns

| Column | Type | Source entity | Source field | Description |
|---|---|---|---|---|
| `DimBotId` | STRING | `bot` | `botid` | Primary key. Bot GUID. |
| `Bot` | STRING | `bot` | `name` | Bot display name. |
| `StateCode` | BIGINT | `bot` | `statecode` | Bot state code, such as active or inactive. |
| `StatusCode` | BIGINT | `bot` | `statuscode` | Bot status reason code. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Filters and deduplication

Rows with a null `botid` are excluded. Deduplication uses `modifiedon` to retain the latest record for each bot.

## Dashboard relationships

Use single-direction, one-to-many relationships from `DimBotId` to the aggregate `BotId` columns. Don't relate `DimBot` to `DimBotTopic`; the aggregates have independent bot and topic relationships.

Select one bot for conversation participation measures. A conversation can contribute to multiple bots, so don't sum bot rows for an overall distinct-conversation total. Use the routed measures described in [AggConversationBotOutcome](aggconversationbotoutcome.md#measures-and-filter-scope).

## Related tables

| Table | Purpose |
|---|---|
| [FactBotSession](FactBotSession.md) | Provides pipeline calculation detail; isn't imported into the bot dashboard model. |
| [AggBotSession](aggbotsession.md) | Provides preaggregated bot metrics for dashboards and reports. |
| [AggConversationBotOutcomeByBot](aggconversationbotoutcomebybot.md) | Defines conversation measures for one participating bot. |
| [AggConversationBotOutcomeByBotTopic](aggconversationbotoutcomebybottopic.md) | Defines conversation measures for one participating bot and topic. |
