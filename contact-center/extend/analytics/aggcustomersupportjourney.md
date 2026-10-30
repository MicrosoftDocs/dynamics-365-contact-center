---
title: AggCustomerSupportJourney table reference
description: Reference for the customer-support journey aggregate contract in the Dynamics 365 Contact Center bot dashboard model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-generated
---

# AggCustomerSupportJourney table reference

Use `AggCustomerSupportJourney` to visualize conversations moving through customer-support stages. In the bot dashboard model, source and destination categories define each transition, and conversation counts provide its edge weight.

> [!IMPORTANT]
> This reference describes the table expected by the dashboard model; it doesn't confirm that the pipeline provisions it. Check [Bot table availability](../overview-data-model.md#bot-table-availability) before using this table in reports or Fabric integrations.

## Grain

Each row groups a source-to-destination transition by 15-minute UTC interval, queue, channel, conversation status, direction, and conversation type.

`ConversationCount` counts contributions to an edge, not distinct conversations overall. One conversation can contribute to multiple transitions, so don't sum journey edges for total bot conversations.

## Columns

These are Power BI semantic types, not physical Delta schema types.

| Column | Semantic type | Description |
|---|---|---|
| `DateTimeKey` | int64 | 15-minute UTC time key used for date and hour filtering. |
| `QueueId` | string | Queue key. |
| `ChannelCode` | int64 | Conversation channel code. |
| `ConversationStatusCode` | int64 | Conversation status code. |
| `ConversationDirectionCode` | int64 | Conversation direction code. |
| `ConversationTypeCode` | int64 | Conversation type code. |
| `Source` | string | Starting category for the journey edge. |
| `Destination` | string | Ending category for the journey edge. |
| `ConversationCount` | int64 | Conversation contributions for the edge. |
| `_SourceRecordCount` | int64 | Aggregation diagnostics count. |
| `_LastRefreshedDateTimeUtc` | dateTime | UTC refresh timestamp. |
| `_AggregationDate` | dateTime | Date used for partitioning and incremental refresh. |

Use the column name `Destination`, not its legacy misspelling, `Denstination`. The dashboard contract has no `DimTopicId` or `ConversationAttributeMappingId` column.

## Measures and relationships

For a journey visualization, bind `Source`, `Destination`, and **Journey Conversations**, which sums `ConversationCount`.

| Table column | Related column |
|---|---|
| `DateTimeKey` | `ProxyUtcDateId.UtcDateTimeKey`. |
| `QueueId` | `DimQueue.QueueId`. |
| `ChannelCode` | `DimChannel.ChannelCode`. |
| `ConversationStatusCode` | `DimConversationStatus.ConversationStatusCode`. |
| `ConversationDirectionCode` | `DimConversationDirection.ConversationDirectionCode`. |
| `ConversationTypeCode` | `DimConversationType.ConversationTypeCode`. |

Filter dates through `ProxyUtcDateId`, `DimTimeZone`, and `DimDate`. Don't relate `_AggregationDate` directly to `DimDate.Date`.

The table has neither bot nor topic keys and no relationship to `DimBot` or `DimBotTopic`. Selecting a bot name doesn't filter the journey through those dimensions.

## Related information

- [AggBotSession table reference](aggbotsession.md).
- [AggConversationBotOutcome table reference](aggconversationbotoutcome.md).
