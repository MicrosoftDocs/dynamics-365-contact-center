---
title: DimBotTopic table reference
description: Reference for the shared bot-topic dimension contract in the Dynamics 365 Contact Center bot dashboard model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-generated
---

# DimBotTopic table reference

Use `DimBotTopic` to select and label topics consistently across bot session metrics and topic-level conversation outcomes. Both aggregates in the bot dashboard model use the same topic identity.

> [!IMPORTANT]
> This reference describes the table expected by the dashboard model; it doesn't confirm that the pipeline provisions it. Check [Bot table availability](../overview-data-model.md#bot-table-availability) before using this table in reports or Fabric integrations.

## Grain and identity

The contract defines one row per bot and topic identifier pair, with neither identifier null. `BotId` and `BotTopicId` establish identity; the display name doesn't.

Renaming a topic changes its label, not its identity. Different topic IDs remain separate members even if their labels match.

## Columns

These are Power BI semantic types, not physical Delta schema types.

| Column | Semantic type | Description |
|---|---|---|
| `BotTopicKey` | string | Stable relationship key for a bot and topic identifier pair. |
| `BotId` | string | Bot identifier. |
| `BotTopicId` | string | Source topic identifier, hidden in the semantic model. |
| `BotTopicName` | string | Topic display label, grouped by `BotTopicKey` in the semantic model. |
| `_LastRefreshedDateTimeUtc` | dateTime | Refresh timestamp. |

The key contract uses the lowercase SHA-256 hexadecimal digest of `<length(BotId)>:<BotId>|<length(BotTopicId)>:<BotTopicId>`. Lengths are Spark character lengths; hashing uses UTF-8 bytes without trimming, case folding, or Unicode normalization. The key is null if either identifier is null.

The dimension retains historically observed identities and uses the latest nonblank label. A missing label doesn't change an otherwise valid identity.

## Relationships and reporting

Use independent, single-direction relationships from `DimBotTopic.BotTopicKey` to these aggregate columns:

| Aggregate table | Column |
|---|---|
| [AggBotSession](aggbotsession.md) dashboard contract. | `BotTopicKey`. |
| [AggConversationBotOutcomeByBotTopic](aggconversationbotoutcomebybottopic.md). | `BotTopicKey`. |

Use `DimBotTopic.BotTopicName` for topic selectors and grouped rows. Include the identity key in the grouping to keep topics with matching labels separate.

Don't relate `DimBotTopic` to `DimBot`; the aggregates already have independent bot relationships. Conversation participation measures require one bot and one topic identity. Unsupported multiple-topic selections return blank rather than a sum of overlapping conversation counts.

## Related information

- [DimBot table reference](DimBot.md).
- [AggBotSession table reference](aggbotsession.md).
- [AggConversationBotOutcomeByBotTopic table reference](aggconversationbotoutcomebybottopic.md).
