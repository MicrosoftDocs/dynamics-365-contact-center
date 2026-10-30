---
title: FactVoiceConversationInsights table reference
description: Reference information for the FactVoiceConversationInsights table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# FactVoiceConversationInsights table reference

Use `FactVoiceConversationInsights` to review AI-generated call quality metrics from Dynamics 365 **Conversation Intelligence**. After a voice call ends, the system analyzes its recording. Supervisors can use the resulting behavioral metrics to identify coaching opportunities, such as agents speaking too quickly, listening too little, or leaving long pauses.

## Business value

Use this table to answer:

- How fast did the agent speak, in words per minute?
- What was the ratio of agent talk time to customer talk time?
- How often did speakers switch?
- How long did the agent pause before responding?
- What was the longest uninterrupted customer monologue?

The table includes only voice conversations with Conversation Intelligence enabled. If the feature isn't enabled for your organization, the table is empty. Use `AggVoiceConversationInsights` for summaries by reporting interval.

## Grain

The table stores one row per voice conversation with AI insights.

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_ocliveworkitem | Provides conversation identity, channel, and creation date. |
| msdyn_conversationinsight | Provides the five voice quality metrics. |

## 1. Identity and context

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `ConversationId` | STRING | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitemid` | Primary Key. Voice conversation identifier. Foreign Key to FactConversation. Agent/queue/channel available via FactConversation join. |
| `CreatedOnDateTime` | TIMESTAMP | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_createdon` | When the conversation was created. |
| `CreatedOnDateKey` | BIGINT | Calculated | `YYYYMMDDHHMM` (15-min aligned) from `msdyn_ocliveworkitem.msdyn_createdon` | 15-minute time slot key. Foreign Key to `DimTimeZone.UtcDateTimeKey` for timezone conversion in Power BI. |

---

## 2. Voice quality metrics

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `LongestCustomerMonologueInSeconds` | DOUBLE | `msdyn_conversationinsight` | `msdyn_calllongestcustomermonologue / 1000` | Longest uninterrupted customer speech (ms → sec). DOUBLE—division can produce decimal seconds. |
| `PauseBeforeSpeakingInSeconds` | DOUBLE | `msdyn_conversationinsight` | `msdyn_callaveragepause / 1000` | Average agent pause before responding (ms → sec). DOUBLE—division can produce decimal seconds. |
| `SwitchesPerConversation` | DOUBLE | `msdyn_conversationinsight` | `msdyn_callswitchesperconversation` | Number of speaker turn switches. DV source is Decimal(38,2). |
| `TalkingSpeed` | DOUBLE | `msdyn_conversationinsight` | `msdyn_calltalkingspeed` | Agent speaking speed (words per minute). DV source is Decimal(38,2). |
| `TalkToListenRatio` | DOUBLE | `msdyn_conversationinsight` | `msdyn_calltalktolistenratio` | Ratio of agent talk time vs customer talk time (0–1). DV source is Decimal(38,2). |

---

## 3. ETL and system

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `_StartDate` | DATE | `to_date(msdyn_ocliveworkitem.msdyn_createdon)` | Delta partition column. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | `current_timestamp()` | Pipeline refresh timestamp. |

---

## Source entities

| Dataverse entity | Contribution |
|-----------|---------------------|
| `msdyn_ocliveworkitem` | Conversation identity, channel filter, creation date |
| `msdyn_conversationinsight` | All 5 voice quality metrics (INNER join, latest by `modifiedon`) |

## Filters and dedup

```sql
WHERE msdyn_channel = '192440000'           -- Voice only
  AND msdyn_channelinstanceid IS NULL  -- Contact center conversations only (NULL = contact center, NOT NULL = partner/sales)
-- Only conversations with AI insights included (INNER JOIN on msdyn_conversationinsight)
```

**Deduplication:** A conversation can have multiple `msdyn_conversationinsight` records, for example, after a transcript update triggers reprocessing. ETL uses `ROW_NUMBER() OVER (PARTITION BY msdyn_conversationid ORDER BY modifiedon DESC) = 1` to retain only the latest insight and maintain one row per conversation.

## Related tables

Use `FactVoiceConversationInsights` with these tables.

| Table | Purpose |
|-------|---------|
| AggVoiceConversationInsights | Provides aggregate voice quality metrics. |
| DimTimeZone | Supports local-time reporting. |
| FactConversation | Provides agent, queue, and channel context. |
