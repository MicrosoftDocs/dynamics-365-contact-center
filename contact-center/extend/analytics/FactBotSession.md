---
title: FactBotSession table reference
description: Reference for the FactBotSession table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-assisted
---

# FactBotSession table reference

`FactBotSession` contains session-level calculation details for bots and Copilot Studio agents. The bot processing pipeline uses these details to build `AggBotSession`.

> [!IMPORTANT]
> This pipeline-generated fact isn't imported into the bot dashboard model. The dashboard uses aggregates and dimensions; it doesn't expose individual bot-session records through this fact. Its presence in the pipeline doesn't establish supported direct access or Fabric availability. Learn more in [Bot table availability](../overview-data-model.md#bot-table-availability).

The implementation supports standard bot analytics, but not advanced bot analytics or intent enrichment. Columns retained for compatibility with those features contain null values.

## Business value

Use this table to answer questions such as:

- Did the bot engage the customer?
- Did the bot resolve, escalate, or abandon the session?
- Which topic handled the session or triggered an escalation?
- How long did the bot session last?
- Which conversation, queue, channel, and language were associated with the session?
- What customer satisfaction score was submitted for the session?

Use [AggBotSession](aggbotsession.md) for dashboard visuals and aggregate reports. Dashboard conversation measures use the separate [conversation outcome aggregate family](aggconversationbotoutcome.md), not this session detail.

## Grain

The table stores one row per bot session. When records share the same `BotSessionId` and `SessionId`, it retains the most recently modified record.

## Source tables

| Source table | Purpose |
|---|---|
| `msdyn_botsession` | Provides bot session identity, timing, engagement, topic, outcome, and CSAT data. |
| `msdyn_ocsession` | Provides queue, conversation linkage, closure, timing, and session creation data. |
| `msdyn_ocliveworkitem` | Provides conversation title, status, channel, direction, and type. |
| `msdyn_sessionparticipant` | Provides session assignment information and the primary participant. |
| `systemuser` | Identifies whether the primary participant is a bot or service representative. |
| `msdyn_ocphonecallengagementctx` | Provides the dialed number for voice conversations. |
| `msdyn_ocliveworkitemcontextitem` | Provides conversation language context. |
| `msdyn_oclwicontextitemelastic` | Provides elastic conversation language context. |
| `msdyn_oclanguage` | Maps language values to language names. |

## Identity and bot session columns

| Column | Type | Source entity | Source field or logic | Description |
|---|---|---|---|---|
| `BotSessionId` | STRING | `msdyn_botsession` | `msdyn_botsessionid` | Primary key. Bot session identifier. |
| `SessionId` | STRING | `msdyn_botsession` | `msdyn_sessionid` | Omnichannel session associated with the bot session. |
| `ConversationId` | STRING | `msdyn_ocsession` | `msdyn_liveworkitemid` | Conversation associated with the session. |
| `BotId` | STRING | `msdyn_botsession` | `msdyn_botid` | Bot GUID. Foreign key to `DimBot.DimBotId`. |
| `SessionStartTime` | STRING | `msdyn_botsession` | Formatted `msdyn_startedon` | Bot session start time in ISO 8601 format. |
| `DurationInSeconds` | BIGINT | Calculated | Difference between `msdyn_endedon` and `msdyn_startedon` | Bot session duration. The value is null when either timestamp is unavailable. |
| `CreatedDateId` | BIGINT | Calculated | 30-minute key derived from `SessionStartTime` | Time-slot key for reporting. |

## Bot session metric columns

| Column | Type | Source entity | Source field or logic | Description |
|---|---|---|---|---|
| `CSATScore` | BIGINT | `msdyn_botsession` | `msdyn_csatscore`; null becomes 0 | Bot session customer satisfaction score. |
| `IsBotEngaged` | INT | `msdyn_botsession` | `msdyn_isengaged` | Indicates whether the bot engaged the customer. |
| `SessionOutcome` | BIGINT | `msdyn_botsession` | `msdyn_outcome`; null becomes -1 | Bot session outcome option-set code. |
| `BotTopicName` | STRING | `msdyn_botsession` | `msdyn_topicname` | Topic that handled the bot session. |
| `EscalatedTopic` | STRING | Calculated | Latest escalated topic in the conversation | Topic that triggered escalation for the conversation. |
| `SessionOutcomeReason` | BIGINT | `msdyn_botsession` | `msdyn_outcomereason`; null becomes 0 | Bot session outcome-reason option-set code. |
| `SessionOutcomeReasonName` | STRING | Calculated | Option-set mapping of `msdyn_outcomereason` | Human-readable outcome reason, such as `Resolved` or `AgentTransferRequestedByUser`. |

## Omnichannel session columns

| Column | Type | Source entity | Source field or logic | Description |
|---|---|---|---|---|
| `DimQueueId` | STRING | `msdyn_ocsession` | `msdyn_cdsqueueid`; falls back to `msdyn_queueextensionid` | Queue associated with the session. Foreign key to `DimQueue`. |
| `OCSessionIsAgentSession` | INT | Calculated | Derived from the latest primary participant | Indicates whether the primary participant is a service representative. |
| `OCSessionClosureReason` | INT | `msdyn_ocsession` | `msdyn_closurereason` | Omnichannel session closure reason code. |
| `OCSessionClosedOnDateTime` | TIMESTAMP | `msdyn_ocsession` | `msdyn_sessionclosedon` | Date and time when the session closed. |
| `OCSessionCreatedOnDateTime` | TIMESTAMP | `msdyn_ocsession` | `msdyn_sessioncreatedon` | Date and time when the session was created. |
| `OCSessionCSATScore` | STRING | Compatibility column | Null | Placeholder retained for schema compatibility. |
| `SessionCreationReason` | INT | `msdyn_ocsession` | `msdyn_sessioncreationreason` | Reason the session was created. |
| `SessionAssignReason` | STRING | `msdyn_sessionparticipant` | `msdyn_assignreason` | Reason the accepted participant was assigned to the session. |
| `SessionIntentId` | STRING | Compatibility column | Null | Intent identifier placeholder. Intent enrichment isn't included in the current release. |

## Conversation columns

| Column | Type | Source entity | Source field or logic | Description |
|---|---|---|---|---|
| `OCConversationTopicId` | STRING | Compatibility column | Null | Conversation topic identifier placeholder. |
| `ConversationUrl` | STRING | Compatibility column | Null | Conversation deep-link placeholder. |
| `ConversationTitle` | STRING | `msdyn_ocliveworkitem` | `msdyn_title` | Conversation title. |
| `StatusId` | INT | `msdyn_ocliveworkitem` | `statuscode` | Conversation status code. Foreign key to `DimConversationStatus`. |
| `ChannelId` | INT | `msdyn_ocliveworkitem` | `msdyn_channel` | Conversation channel code. Foreign key to `DimChannel`. |
| `PrimaryChannelId` | INT | Compatibility column | Null | Primary-channel placeholder. |
| `ConversationOutcome` | STRING | Calculated | `Bot escalated` if any session in the conversation escalated; otherwise `Bot deflected` | Conversation-level bot outcome used for deflection and escalation metrics. |
| `ConversationAttributeMappingId` | STRING | Calculated | Pipe-delimited conversation attributes | Composite attribute key used by reporting. |
| `IsOutbound` | INT | `msdyn_ocliveworkitem` | `msdyn_isoutbound`; null becomes 0 | Indicates whether the conversation is outbound. |
| `ConversationType` | STRING | `msdyn_ocliveworkitem` | `msdyn_conversationtype` | Conversation type. |
| `ProactiveEngagementConfigId` | STRING | Compatibility column | Null | Proactive engagement configuration placeholder. |
| `ActiveAgentGroupId` | STRING | Compatibility column | Null | Active agent-group placeholder. |

## Language and dialed number columns

| Column | Type | Source entity | Source field or logic | Description |
|---|---|---|---|---|
| `DNIS` | STRING | `msdyn_ocphonecallengagementctx` | `msdyn_tophone` | Dialed number for an inbound voice conversation. |
| `LastLanguage` | STRING | Context and language tables | Latest `va_Language` value mapped to `msdyn_languagename` | Last language observed in the conversation. |

## Aggregation support column

| Column | Type | Source entity | Source field or logic | Description |
|---|---|---|---|---|
| `IsPrimaryBotSessionOfConversation` | INT | Calculated | 1 for the earliest bot session in each conversation; otherwise 0 | Supports additive conversation counts in `AggBotSession`. Conversations without a `ConversationId` have a value of 0. |

This marker counts each identified conversation once across complete history, attributing it to the earliest bot session. Date filters use that session's reporting interval. Groups based on attributes that can change between sessions, such as topic or queue, use the earliest session's value. This compatibility marker isn't the dashboard's participation-based conversation measure.

## ETL and system columns

| Column | Type | Source or logic | Description |
|---|---|---|---|
| `_StartDate` | DATE | Date from `SessionStartTime`; falls back to the bot-session creation date | Delta Lake partition column. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | `current_timestamp()` | Pipeline refresh timestamp. |

## Filters and deduplication

- Rows are deduplicated by `msdyn_botsessionid` and `msdyn_sessionid`, retaining the latest record by `modifiedon`.
- `EscalatedTopic` uses the latest escalated bot session in each conversation.
- `LastLanguage` uses the most recent language context value in each conversation.

## Related tables

| Table | Purpose |
|---|---|
| [DimBot](DimBot.md) | Provides bot names and status information. |
| DimChannel | Provides channel names. |
| DimConversationDirection | Provides inbound and outbound labels. |
| DimConversationStatus | Provides conversation status labels. |
| DimDate | Provides calendar attributes. |
| DimQueue | Provides queue attributes. |
| DimTimeZone | Supports local time conversion. |
| [AggBotSession](aggbotsession.md) | Provides reporting-ready bot session aggregates. |
