---
title: FactSession table reference
description: Reference information for the FactSession table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# FactSession table reference

Use `FactSession` to examine a single routing leg of a conversation. A **session** covers one agent's or bot's handling of that leg, from assignment to close.

## Business value

A conversation can include multiple session types:

- **Bot session:** The bot handles the initial interaction.
- **Agent session:** A session is created when the bot escalates or the customer connects directly to an agent.
- **Transfer session:** A session is created when the conversation transfers between agents or queues.

Sessions are the unit of agent performance measurement, each with its own wait time, outcome, and routing context.

This table answers:

- How long did the customer wait before the agent accepted?
- Was the session resolved, escalated, or transferred?
- What overflow or callback actions were triggered?
- What was the customer's real-time sentiment during the session?
- Why was the session created, and how was it routed?

For each person's active, talk, and hold durations, use `FactSessionParticipant`. For conversation-level CSAT, NPS, and direction, use `FactConversation`.

## Grain

The table stores one row per session (`SessionId`).

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_ocsession | Provides session identity, routing context, timestamps, reasons, and status. |
| msdyn_sessionparticipant | Provides primary agent identity, participation times, and assignment reason. |
| msdyn_sessionextension | Provides overflow, callback, routing, outcome, and engagement details. |
| msdyn_ocsessionsentiment | Provides session sentiment scores and categories. |
| msdyn_conversationmessageblock | Provides message counts and response times. |

## 1. Identity and foreign keys

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `SessionId` | STRING | `msdyn_ocsession` | `msdyn_ocsessionid` | Primary Key |
| `ConversationId` | STRING | `msdyn_ocsession` | `msdyn_liveworkitemid` | Foreign Key to FactConversation. |
| `PrimarySessionId` | STRING | `msdyn_ocsession` | `msdyn_primarysession` | Parent session in transfer chains. NULL if first session. |
| `QueueSegmentId` | STRING | `msdyn_ocsession` | `msdyn_queueextensionid` | Foreign Key to FactQueueSegment. Links session to its queue-leg. |
| `QueueId` | STRING | `msdyn_ocsession` | `msdyn_cdsqueueid` | Foreign Key to DimQueue. |
| `ChannelCode` | INT | `msdyn_ocsession` | `msdyn_channel` | Foreign Key to DimChannel. |
| `PrimaryAgentId` | STRING | `msdyn_sessionparticipant` | `msdyn_agentid` (WHERE `msdyn_mode` = 192350002, latest by `modifiedon`) | Foreign Key to DimSystemUser. NULL if bot-only. |
| `SessionStateCode` | INT | `msdyn_ocsession` | `statecode` | 0=Open, 1=Closed. |
| `SessionState` | STRING | `HelperOptionSet` | Resolved from `statecode` via HelperOptionSet → `msdyn_ocsession.statecode` | Session lifecycle state label (for example, "Open", "Closed"). |
| `SessionStatusCode` | INT | `msdyn_ocsession` | `statuscode` | Detailed session status reason within the state. |
| `SessionStatus` | STRING | `HelperOptionSet` | Resolved from `statuscode` via HelperOptionSet → `msdyn_ocsession.statuscode` | Session status label. |

---

## 2. Timestamps

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `CreatedOnDateTime` | TIMESTAMP | `msdyn_ocsession` | `msdyn_sessioncreatedon` | When the session was created. |
| `QueueAssignedOnDateTime` | TIMESTAMP | `msdyn_ocsession` | `msdyn_queueassignedon` | When assigned to queue. |
| `AgentAssignedOnDateTime` | TIMESTAMP | `msdyn_ocsession` | `msdyn_agentassignedon` | When agent was assigned. |
| `AgentAcceptedOnDateTime` | TIMESTAMP | `msdyn_ocsession` | `msdyn_agentacceptedon` | When agent clicked Accept. |
| `PrimaryAgentJoinedOnDateTime` | TIMESTAMP | `msdyn_sessionparticipant` | `msdyn_joinedon` (primary participant) | When agent actually joined. |
| `PrimaryAgentLeftOnDateTime` | TIMESTAMP | `msdyn_sessionparticipant` | `msdyn_lefton` (primary participant) | When agent left. NULL if still active. |
| `ClosedOnDateTime` | TIMESTAMP | `msdyn_ocsession` | `msdyn_sessionclosedon` | When session was closed. |
| `CallbackOfferAcceptedOnDateTime` | TIMESTAMP | `msdyn_sessionextension` | `msdyn_callbackacceptedtime` | When customer accepted the callback offer. NULL if not a callback. |
| `CallbackCustomerAddedOnDateTime` | TIMESTAMP | `msdyn_sessionextension` | `msdyn_callbackcustomeraddedtime` | When customer was added to the callback call. NULL if callback not completed. |
| `OverflowTriggeredOnDateTime` | TIMESTAMP | `msdyn_sessionextension` | `msdyn_overflowtriggertimestamp` | When overflow was triggered. |
| `CreatedOnDateKey` | BIGINT | Calculated | `YYYYMMDDHHMM` (15-min aligned) from `msdyn_ocsession.msdyn_sessioncreatedon` | 15-minute time slot key. Foreign Key to `DimTimeZone.UtcDateTimeKey` for timezone conversion in Power BI. |

---

## 3. Computed durations

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `WaitTimeInSeconds` | BIGINT | Calculated | `COALESCE(msdyn_agentacceptedon, msdyn_sessionclosedon) - msdyn_sessioncreatedon` | Creation to acceptance. Uses close time if never accepted. |
| `AnswerTimeInSeconds` | BIGINT | Calculated | `COALESCE(msdyn_agentacceptedon, msdyn_sessioncreatedon) - msdyn_sessioncreatedon` | Creation to acceptance. Returns 0 if never accepted. |
| `HandleTimeInSeconds` | BIGINT | Calculated | **Voice** (channel=192440000): `Hold + Talk + ActiveWrapup`; fallback to `ActiveTime` if all zero. **Chat/DM**: `ActiveChat + ActiveWrapup`; fallback to `ActiveTime` if both null/zero. Aligned with v1 and ACD realtime formula. | Channel-aware handle time from session participant activity components. |
| `SessionEngagedTimeInSeconds` | BIGINT | Calculated | `msdyn_sessionclosedon - msdyn_agentacceptedon` | Wall-clock from acceptance to close. NULL if never accepted or still open. |
| `SessionDurationInSeconds` | BIGINT | Calculated | `msdyn_sessionclosedon - msdyn_sessioncreatedon` | Total session duration (creation to close). NULL if still open. |

> **HandleTime vs SessionEngagedTime:** `SessionEngagedTimeInSeconds` = `msdyn_sessionclosedon - msdyn_agentacceptedon`. It's the elapsed time from acceptance to close and is NULL if the agent never accepted or the session is still open. `HandleTimeInSeconds` uses the v1 channel-aware component sum, aligned with the ACD realtime dashboard:
> - **Voice HandleTimeInSeconds:** HoldTime + TalkTime + ActiveWrapupTime.
> - **Chat/DM HandleTimeInSeconds:** ActiveChatTime + ActiveWrapupTime.
> - **Fallback for HandleTimeInSeconds:** ActiveTime when component fields are missing in older data from before 10.4 2024.

---

## 4. Messages and response

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IncomingMessages` | BIGINT | `msdyn_conversationmessageblock` | `SUM(msdyn_inboundmessagecountwithinoh)` WHERE `msdyn_agentresponsesessionid` = session | Customer messages within operating hours. |
| `OutgoingMessages` | BIGINT | `msdyn_conversationmessageblock` | `SUM(msdyn_outboundmessagecountwithinoh)` WHERE `msdyn_agentresponsesessionid` = session | Agent messages within operating hours. |
| `FirstResponseTimeInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | Block with MIN(msdyn_agentmessagetime) per session → COALESCE(msdyn_responsetimeadjforoh, msdyn_responsetimenotadjforoh) / 1000. Naturally skips rejected/bot/no-response sessions. | How long the customer waited for the first reply in this session, from the customer's perspective. |
| `FirstResponseTimeAfterAcceptanceInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | Same block (MIN msdyn_agentmessagetime) → COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) / 1000 | How quickly the agent responded after accepting this session. Measures agent responsiveness only, excludes queue wait. |
| `TotalResponseTimeInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | SUM of COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) / 1000 across all blocks WHERE value >= 0 | Sum of agent response times across all exchanges in this session. Numerator for avg response time. |
| `MessageBlockCount` | BIGINT | `msdyn_conversationmessageblock` | COUNT of blocks WHERE COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) IS NOT NULL AND >= 0 | Number of customer→agent message exchanges in this session. Denominator for avg response time. |
| `AvgResponseTimeInSeconds` | DOUBLE | Calculated | `TotalResponseTimeInSeconds / NULLIF(MessageBlockCount, 0)` | Average agent response time for this session. Computed from message block totals—no averaging-averages issue. |

---

## 5. Flags

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IsAgentSession` | BOOLEAN | `msdyn_sessionparticipant` + `systemuser` | TRUE if primary participant's `msdyn_botapplicationid` IS NULL | Primary participant is human. |
| `IsBotSession` | BOOLEAN | `msdyn_sessionparticipant` + `systemuser` | TRUE if primary participant's `msdyn_botapplicationid` IS NOT NULL | Primary participant is bot. |
| `IsAgentAccepted` | BOOLEAN | `msdyn_sessionparticipant` | TRUE if `IsAgentSession` AND `msdyn_joinedon IS NOT NULL` | Human agent accepted and joined. |
| `IsBotAccepted` | BOOLEAN | `msdyn_sessionparticipant` | TRUE if `IsBotSession` AND (`msdyn_joinedon` OR `msdyn_lefton` IS NOT NULL) | Bot accepted and participated. |
| `IsAgentAssigned` | BOOLEAN | `msdyn_ocsession` | TRUE if `msdyn_agentassignedon IS NOT NULL` AND `IsAgentSession` | Agent was assigned (may not have accepted). |
| `IsEngaged` | BOOLEAN | `msdyn_sessionextension` | `msdyn_isengaged` (latest by `modifiedon`) | Session actively engaged by agent. |
| `IsBotEscalated` | BOOLEAN | Calculated | TRUE if `IsBotSession` AND `msdyn_closurereason` IN (192350000, 192350026, 192350029, 192350030, 192350031) | Bot escalated to human. |
| `IsBotResolved` | BOOLEAN | Calculated | TRUE if `IsBotSession` AND `msdyn_closurereason` IN (192350005, 192350020, 192350021, 192350022, 192350027) | Bot resolved without agent. |
| `IsSessionEscalated` | BOOLEAN | Calculated | TRUE if `msdyn_closurereason` IN (192350000, 192350026, 192350029, 192350030, 192350031) | Session ended with escalation (any session—bot or agent). |
| `IsSessionResolved` | BOOLEAN | Calculated | TRUE if `msdyn_closurereason` IN (192350005, 192350020, 192350021, 192350022, 192350027) | Session ended with resolution (any session—bot or agent). |
| `IsCallbackOffered` | BOOLEAN | `msdyn_sessionextension` | TRUE if `msdyn_overflowaction = '419550001'` | Callback offered to customer. |
| `IsExternalTransfer` | BOOLEAN | `msdyn_sessionextension` | TRUE if `msdyn_overflowaction = '419550002'` | Overflowed to external transfer. |
| `IsVoicemail` | BOOLEAN | `msdyn_sessionextension` | TRUE if `msdyn_overflowaction = '419550003'` | Overflowed to voicemail. |
| `IsOutOfOperatingHours` | BOOLEAN | `msdyn_sessionextension` | TRUE if `msdyn_overflowcondition = '419550000'` | Outside operating hours. |
| `IsSessionTransferred` | BOOLEAN | `msdyn_sessionextension` | TRUE if `msdyn_overflowaction IN ('419550002', '419550004')` | Session was transferred. |

---

## 6. Reason codes and outcome

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `ClosureReasonCode` | INT | `msdyn_ocsession` | `msdyn_closurereason` | Foreign Key to DimSessionClosureReason. Why the session ended. |
| `SessionCreationReason` | INT | `msdyn_ocsession` | `msdyn_sessioncreationreason` | Why the session was created, such as a new conversation or transfer. |
| `SessionAssignReason` | STRING | `msdyn_sessionparticipant` | `msdyn_assignreason` (primary participant) | How the agent was assigned, such as auto-assign, push, or supervisor assignment. |
| `RoutingType` | STRING | `msdyn_sessionextension` | `msdyn_routingtype` (latest by `modifiedon`) | How the session was routed, such as push or pick. |
| `OverflowActionCode` | INT | `msdyn_sessionextension` | `msdyn_overflowaction` (latest by `modifiedon`) | Foreign Key to DimOverflowAction. What happened when overflow triggered. |
| `OverflowConditionCode` | INT | `msdyn_sessionextension` | `msdyn_overflowcondition` (latest by `modifiedon`) | Foreign Key to DimOverflowCondition. What condition triggered overflow. |
| `SessionOutcome` | INT | `msdyn_sessionextension` | `msdyn_outcome` (latest by `modifiedon`) | Session outcome numeric value, such as resolved or escalated. Not an optionset—plain integer. |
| `SessionOutcomeReason` | STRING | `msdyn_sessionextension` | `msdyn_outcomereason` (latest by `modifiedon`) | Additional detail on why the session ended with this outcome. |

---

## 7. Sentiment

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `SentimentPulse` | DOUBLE | `msdyn_ocsessionsentiment` | `msdyn_sentimentpulse` (latest by `modifiedon` per session) | Real-time AI sentiment score. |
| `SentimentZone` | STRING | `msdyn_ocsessionsentiment` | `msdyn_sentimentzone` (same dedup) | Sentiment category: Positive, Neutral, Negative. |

---

## 8. ETL and system

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `_StartDate` | DATE | `to_date(msdyn_ocsession.msdyn_sessioncreatedon)` | Delta partition column. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | `current_timestamp()` | Pipeline refresh timestamp. |

---

## Source entities

| Dataverse entity | Contribution |
|-----------|---------------------|
| `msdyn_ocsession` | Identity, conversation Foreign Key, queue, channel, timestamps, closure/creation reasons, status |
| `msdyn_sessionparticipant` | Primary agent ID, join/left timestamps, assign reason (filtered to `msdyn_mode = 192350002`, latest by `modifiedon`) |
| `msdyn_sessionextension` | Overflow action/condition, callback timestamps, routing type, outcome, engagement flag (latest by `modifiedon`) |
| `msdyn_ocsessionsentiment` | Sentiment pulse and zone (latest by `modifiedon`) |
| `msdyn_conversationmessageblock` | Message counts, response times (aggregated per session via `msdyn_agentresponsesessionid`) |

> **Pipeline note:** FactSession runs before FactConversation. `StgConversationSessionAgg` groups FactSession rows by conversation and passes the aggregates to FactConversation through `context.outputs`.

## Filters

```sql
WHERE msdyn_ocsessionid IS NOT NULL
```

## Related tables

Use `FactSession` with these tables.

| Table | Purpose |
|-------|---------|
| DimChannel | Provides channel names. |
| DimOverflowAction | Provides overflow action labels. |
| DimOverflowCondition | Provides overflow trigger labels. |
| DimQueue | Provides queue attributes. |
| DimSessionClosureReason | Provides closure reason labels. |
| DimSystemUser | Provides primary agent attributes. |
| DimTimeZone | Supports local-time reporting. |
| FactConversation | Provides parent conversation attributes and feedback. |
| FactQueueSegment | Provides the session's queue-leg details. |
| FactSessionParticipant | Provides each participant's activity and durations. |
| HelperOptionSet | Provides related lookup, detail, mapping, or aggregated data for reporting. |
