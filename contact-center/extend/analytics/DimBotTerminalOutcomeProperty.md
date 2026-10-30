---
title: DimBotTerminalOutcomeProperty table reference
description: Reference for the localized terminal bot outcome dimension contract in the Dynamics 365 Contact Center bot dashboard model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-generated
---

# DimBotTerminalOutcomeProperty table reference

Use `DimBotTerminalOutcomeProperty` to display localized terminal conversation outcomes, reasons, and reason groups. All three conversation outcome aggregates in the bot dashboard model share this table.

> [!IMPORTANT]
> This reference describes the table expected by the dashboard model; it doesn't confirm that the pipeline provisions it. Check [Bot table availability](../overview-data-model.md#bot-table-availability) before using this table in reports or Fabric integrations.

## Grain and key

Each row maps a terminal outcome and reason to labels in one language. The row is identified by `TerminalOutcomeAttributeMappingId` and `LocalizedLabelLanguageCode` together.

The language-neutral mapping key uses the null-safe format `o:{LastSessionOutcome-or-null}|r:{LastSessionOutcomeReason-or-null}`. The same mapping key can appear in multiple language rows.

## Columns

These are Power BI semantic types, not physical Delta schema types.

| Column | Semantic type | Description |
|---|---|---|
| `TerminalOutcomeAttributeMappingId` | string | Language-neutral terminal outcome and reason mapping key. |
| `LastSessionOutcome` | int64 | Terminal conversation outcome code. |
| `LastSessionOutcomeReason` | int64 | Terminal conversation outcome-reason code. |
| `LastSessionOutcomeName` | string | Localized terminal outcome label. |
| `LastSessionOutcomeReasonName` | string | Localized terminal outcome-reason label. |
| `LastSessionOutcomeReasonGroupName` | string | Localized outcome-reason group label. |
| `LocalizedLabelLanguageCode` | int64 | Language code (LCID) for the labels. |
| `IsDefaultLanguage` | boolean | Indicates whether the row uses the default language. |
| `_LastRefreshedDateTimeUtc` | dateTime | UTC refresh timestamp. |

Terminal conversation outcome codes and bot session outcome codes belong to different option-set families. Don't use `AggBotSession.SessionOutcome` or `SessionOutcomeReason` to label terminal conversation outcomes.

## Relationships

`LocalizationLanguageLocale.LanguageCode` filters `LocalizedLabelLanguageCode`. The property table's mapping key then filters the matching key in these aggregates through active, single-direction, many-to-many relationships:

| Aggregate table | Related column |
|---|---|
| [AggConversationBotOutcome](aggconversationbotoutcome.md). | `TerminalOutcomeAttributeMappingId`. |
| [AggConversationBotOutcomeByBot](aggconversationbotoutcomebybot.md). | `TerminalOutcomeAttributeMappingId`. |
| [AggConversationBotOutcomeByBotTopic](aggconversationbotoutcomebybottopic.md). | `TerminalOutcomeAttributeMappingId`. |

Don't use either repeated numeric outcome code as a relationship key. Filter languages through the locale path. Don't join multiple language rows directly to aggregates in a way that multiplies stored counts.

## Reporting considerations

Use localized name columns for report categories. The aggregates' hidden `ConversationOutcome` tokens filter measures; they aren't localized display labels.

**Terminal Outcome Conversations** uses the routed conversation-count measure. **Terminal Outcome Conversation %** divides this value by the selected terminal-outcome total, preserving the selected bot, topic, and other report filters.

## Related information

- [AggConversationBotOutcome table reference](aggconversationbotoutcome.md).
- [LocalizationLanguageLocale table reference](LocalizationLanguageLocale.md).
