---
title: FactConversation table reference
description: Reference information for the FactConversation table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# FactConversation table reference

Use `FactConversation` to investigate individual customer interactions, their outcomes, and overflow events. A **conversation** covers the full interaction from first contact to closure. It can span multiple sessions, such as a bot session followed by an agent session after escalation.

## Business value

The table brings together these details for each conversation:

- Outcomes, including resolution, abandonment, transfer, and escalation from a bot to an agent.
- End-to-end duration, handle time, wait time, hold time, and wrapup time.
- Customer feedback through CSAT, NPS, Customer Effort Score, and AI sentiment.
- Whether the answer time met the queue's service-level threshold.
- Bot-only, agent-only, or combined involvement, including the agent and session count.

For long-range trends, use `AggConversation`. The current semantic model retains a rolling 24-month window for that aggregate.

## Grain

The table stores one row per conversation (`ConversationId`).

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_ocliveworkitem | Provides conversation identity, context, timestamps, and ACD-stamped metrics. |
| msdyn_ocsession | Provides session counts, wait and answer times, and closure outcomes. |
| msdyn_sessionparticipant | Provides participant activity and bot or agent involvement. |
| msdyn_sessionextension | Provides overflow conditions, actions, and routing flags. |
| systemuser | Provides active agent business units and bot identification. |
| msdyn_ocliveworkitemsentiment | Provides AI sentiment scores and categories. |
| msdyn_transcript | Links sentiment records to conversations. |
| msfp_surveyresponse | Provides Customer Voice survey feedback. |
| msdyn_customerfeedbacksurveyresponse | Provides MCS survey feedback. |
| msfp_question | Identifies survey question types for sentiment analysis. |
| msfp_questionresponse | Provides survey sentiment values. |
| msdyn_conversationmessageblock | Provides message counts and response times. |

## Conversation lifecycle—when columns get their values

Interpret columns according to the conversation's lifecycle stage. Volume metrics, including counts and flags, are valid throughout the interaction. Time and quality metrics are final only after the conversation closes.

```
════════════════════════════════════════════════════════════════════════════════════════════════════════════
                                    CONVERSATION LIFECYCLE
════════════════════════════════════════════════════════════════════════════════════════════════════════════

  Customer              Agent                   Session                 Conversation
  initiates             accepts                 closes                  closes
      │                     │                       │                       │
      ▼                     ▼                       ▼                       ▼
══════●═════════════════════●═══════════════════════●═══════════════════════●════════════════► time
      │                     │                       │                       │
┌─────┴────────────────┐    │                       │                       │
│ 1. IDENTITY &        │    │                       │                       │
│    CONTEXT (15)      │    │                       │                       │
│                      │    │                       │                       │
│ ConversationId       │    │                       │                       │
│ ChannelCode          │    │                       │                       │
│ QueueId              │    │                       │                       │
│ ConversationState/   │    │                       │                       │
│   StatusCode         │    │                       │                       │
│ AgentBusinessUnitId  │    │                       │                       │
└──────────────────────┘    │                       │                       │
      │                     │                       │                       │
      │ ┌───────────────────┴──────────────────┐    │                       │
      │ │ 2. TIMESTAMPS &                      │    │                       │
      │ │    WAITING (13)                      │    │                       │
      │ │                                      │    │                       │
      │ │ FirstWaitTimeInSeconds               │    │                       │
      │ │ SpeedToAnswerTimeInSeconds           │    │                       │
      │ │ IsAbandoned, IsShortAbandoned        │    │                       │
      │ │ TimeToAbandonInSeconds               │    │                       │
      │ │ IsInServiceLevel                     │    │                       │
      │ └──────────────────────────────────────┘    │                       │
      │                     │                       │                       │
      │ ┌───────────────────┴───────────────────────┴──────────────────┐    │
      │ │ 3. HANDLING & INTERACTION (24)                               │    │
      │ │    ───────────── accumulating until close ─────────────────► │    │
      │ │                                                              │    │
      │ │ Involvement:  IsBotInvolved, IsAgentInvolved,                │    │
      │ │               IsOnlyBotInvolved                              │    │
      │ │ Acceptance:   IsOffered, IsAgentAccepted, IsEngaged          │    │
      │ │ Bot Outcomes: IsBotEscalated, IsBotResolved                  │    │
      │ │ Counts:       SessionCount, AgentSessionCount                │    │
      │ │ Durations:    HandleTime, TalkTime, HoldTime,                │    │
      │ │               ActiveTime, InactiveTime, ActiveChatTime       │    │
      │ │ Messages:     IncomingMessages, OutgoingMessages,            │    │
      │ │               FirstResponseTime, TotalResponseTime           │    │
      │ └──────────────────────────────────────────────────────────────┘    │
      │                     │                       │                       │
      │ ┌───────────────────┴───────────────────────┴──────────────────┐    │
      │ │ 4. TRANSFERS & OVERFLOW (7)                                  │    │
      │ │    ───────────── can happen anytime ───────────────────────► │    │
      │ │                                                              │    │
      │ │ TransferCount, IsCallback, IsExternalTransfer,               │    │
      │ │ IsVoicemail, IsOutOfOperatingHours,                          │    │
      │ │ LastOverflowConditionCode, LastOverflowActionCode            │    │
      │ └──────────────────────────────────────────────────────────────┘    │
      │                     │                       │                       │
      │                     │  ┌────────────────────┴──────────────────┐    │
      │                     │  │ 5. WRAPUP, CLOSE & OUTCOME (7)       │    │
      │                     │  │                                       │    │
      │                     │  │ WrapupTimeInSeconds                   │    │
      │                     │  │ ActiveWrapupTimeInSeconds             │    │
      │                     │  │ ClosedOnDateTime                      │    │
      │                     │  │ ConversationDurationInSeconds         │    │
      │                     │  │ CustomerEffortInSeconds               │    │
      │                     │  │ ConversationOutcome                   │    │
      │                     │  └───────────────────────────────────────┘    │
      │                     │                       │                       │
      │                     │                       │  ┌────────────────────┴──────┐
      │                     │                       │  │ 6. QUALITY &             │
      │                     │                       │  │    SENTIMENT (9)         │
      │                     │                       │  │                          │
      │                     │                       │  │ Survey_CSATScore         │
      │                     │                       │  │ Survey_NPSScore          │
      │                     │                       │  │ Survey_CustomerEffortScore│
      │                     │                       │  │ Survey_IsResolved        │
      │                     │                       │  │ Survey_Source             │
      │                     │                       │  │ SentimentPulse/Zone      │
      │                     │                       │  │ Survey_SentimentScore    │
      │                     │                       │  └──────────────────────────┘
      │                     │                       │                       │
══════╪═════════════════════╪═══════════════════════╪═══════════════════════╪════════════════
      │                     │                       │                       │
      ◄── Volume metrics (counts, flags)—valid at any point ────────────►│
      │                     │                       │                       │
      │                     ◄── Time metrics—accumulating per ETL run ───►
      │                     │                       │                       │
      │                     │                       │    All metrics final ─►
      │                     │                       │                       │
════════════════════════════════════════════════════════════════════════════════════════════
```

**Reporting guidance:**
- ETL recalculates every field whenever the conversation record changes, for example, when a session starts, a transfer occurs, or the conversation closes.
- Use volume metrics at any stage to see the current workload.
- Report time-based and quality metrics only when `ConversationStatusCode = Closed`.
- The aggregation layer enforces this restriction through the `ConversationStatusCode` dimension; FactConversation itself doesn't.

---

## 1. Identity and context

These columns identify the conversation and its routing context before interaction begins.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `ConversationId` | STRING | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitemid` | Primary key. Unique identifier for the conversation. |
| `ChannelCode` | INT | `msdyn_ocliveworkitem` | `msdyn_channel` | Channel the customer used to contact you. Foreign key to DimChannel. Examples include 192360000=LiveChat and 192440000=Voice. |
| `ConversationTypeCode` | INT | `msdyn_ocliveworkitem` | `msdyn_conversationtype` | Foreign Key to DimConversationType. Classification of the conversation (0=Inbound, 1=Inbound_DID, 2=Inbound_Callback, 3=Outbound_AgentInitiated, 4=Outbound_PESInitiated). |
| `ConversationDirectionCode` | INT | `msdyn_ocliveworkitem` | `msdyn_isoutbound` | Whether the conversation is inbound or outbound. 0=Inbound, 1=Outbound. Foreign Key to DimConversationDirection. |
| `LiveWorkStreamId` | STRING | `msdyn_ocliveworkitem` | `msdyn_liveworkstreamid` | Foreign Key to DimLiveWorkStream. Workstream that routed this conversation. |
| `QueueId` | STRING | `msdyn_ocliveworkitem` | `msdyn_cdsqueueid` | Queue where the conversation was routed. Foreign Key to DimQueue. |
| `ActiveAgentId` | STRING | `msdyn_ocliveworkitem` | `msdyn_activeagentid` | Last active agent who handled the conversation. Foreign Key to DimSystemUser. NULL for bot-only conversations. |
| `OwnerId` | STRING | `msdyn_ocliveworkitem` | `ownerid` | Owning agent or team for the conversation record. |
| `AgentBusinessUnitId` | STRING | `systemuser` | `systemuser.businessunitid` where `systemuser.systemuserid` = `msdyn_ocliveworkitem.msdyn_activeagentid` | Business unit of the last active agent. Used for BU-level filtering in reports. NULL if no active agent (abandoned/bot-only). |
| `OwningBusinessUnitId` | STRING | `msdyn_ocliveworkitem` | `owningbusinessunit` | Business unit of the conversation owner. Always populated, even for abandoned conversations. |
| `Subject` | STRING | `msdyn_ocliveworkitem` | `subject` | Conversation subject line set by the system or agent. |
| `Title` | STRING | `msdyn_ocliveworkitem` | `msdyn_title` | Omnichannel-assigned title for the conversation. |
| `IsThirdPartyConversation` | BOOLEAN | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_thirdpartyconversation` | Whether a third party (for example, external consultant, supervisor) was brought into the conversation. |
| `ConversationStatusCode` | INT | `msdyn_ocliveworkitem` | `statuscode` | Detailed status reason within the state. Foreign Key to DimConversationStatus. (1=Open, 2=Active, 3=Waiting, 4=Closed, 5=Wrap-up, 6=Resolved, 7=Scheduled) |


---

## 2. Timestamps and waiting

Use these columns to identify when the conversation began and how long the customer waited for acceptance.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `CreatedOnDateTime` | TIMESTAMP | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_createdon` | When the conversation was created in the system. Primary timestamp for time-bucketing (15-min aggregation) and partitioning. |
| `FirstWaitStartedOnDateTime` | TIMESTAMP | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_firstwaitstartedon` | When the customer first entered the queue and started waiting for an agent. Starting point for wait time and SLA calculations. |
| `FirstWaitTimeInSeconds` | BIGINT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_conversationfirstwaittimeinseconds` | ACD-stamped time from queue entry to first agent acceptance. Key metric for SLA and average wait time. |
| `WaitTimeInSeconds` | BIGINT | `msdyn_ocsession` | For each `msdyn_ocsession`: `msdyn_agentacceptedon` - `msdyn_sessioncreatedon`. <br> If `msdyn_agentacceptedon` is NULL: `msdyn_sessionclosedon` - `msdyn_sessioncreatedon`. <br> Summed across all sessions. | Total time the customer spent waiting across all sessions in the conversation, including transfers. Unlike FirstWaitTime which is first-queue only, this captures cumulative wait across re-queues. |
| `SpeedToAnswerTimeInSeconds` | BIGINT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_conversationfirstwaittimeinseconds` WHERE `IsAgentAccepted = 1`, else NULL. | ACD-stamped time from queue entry to first agent acceptance. NULL if no agent accepted (abandoned/bot-only). Aligned with realtime dashboard. |
| `AnswerTimeInSeconds` | BIGINT | `msdyn_ocsession` | For each `msdyn_ocsession`: `msdyn_agentacceptedon` - `msdyn_sessioncreatedon`. <br> If `msdyn_agentacceptedon` is NULL: returns 0. <br> Summed across all sessions. | Total answer time summed across all sessions including transfers. Returns 0 for sessions where no agent accepted. Different from SpeedToAnswer which is first-session only—this captures total across the full conversation lifecycle. |
| `IsAbandoned` | BOOLEAN | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_isabandoned` | Whether the customer abandoned the conversation before an agent accepted. Key metric for queue performance. |
| `IsShortAbandoned` | BOOLEAN | Calculated (ETL) | Derived: `IsAbandoned = 1` AND `FirstWaitTimeInSeconds` <= threshold from `DimQueue.ShortAbandonedThreshold` (per-queue config). **FALSE if threshold not configured.** | Whether the customer abandoned within the queue's short-abandon window. FALSE when threshold not configured on the queue. |
| `TimeToAbandonInSeconds` | BIGINT | Calculated (ETL) | `FirstWaitTimeInSeconds` WHERE `IsAbandoned = 1`. NULL if not abandoned. | Time from queue entry to customer abandonment. Same value as FirstWaitTimeInSeconds for abandoned conversations, NULL otherwise. Used for abandonment buckets (10s, 30s, 60s). |
| `IsInServiceLevel` | BOOLEAN | Calculated (ETL) | Derived: `IsAgentAccepted = 1` AND `msdyn_isoutbound = 0` AND `FirstWaitTimeInSeconds` <= threshold from `DimQueue.ServiceLevelThreshold` (per-queue config). **TRUE if threshold not configured.** | Whether the conversation was answered within the queue's SLA target. TRUE when threshold not configured (all conversations considered in SLA). |
| `CreatedOnDate` | DATE | Calculated | Date portion of `msdyn_ocliveworkitem.msdyn_createdon` | Date of conversation creation. Delta Lake partition column for efficient data pruning. |
| `CreatedOnDateKey` | BIGINT | Calculated | `YYYYMMDDHHMM` (15-min aligned) from `msdyn_ocliveworkitem.msdyn_createdon` | 15-minute time slot key. Foreign Key to `DimTimeZone.UtcDateTimeKey` for timezone conversion in Power BI. |
| `ModifiedOnDateTime` | TIMESTAMP | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_modifiedon` | When the conversation record was last updated in Dataverse. Used for incremental processing—identifies records changed since last ETL checkpoint. |

---

## 3. Handling and interaction

These columns describe involvement, offering and acceptance, bot outcomes, session counts, durations, messages, and response times, in lifecycle order. Handle, talk, hold, and wrapup durations use ACD-stamped conversation fields from `msdyn_ocliveworkitem`. Active and inactive time come from the session-participant rollup.

### 3.1 Involvement—who touched the conversation

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IsBotInvolved` | BOOLEAN | `msdyn_sessionparticipant` + `systemuser` | 1 if any `msdyn_sessionparticipant` for this conversation has `systemuser.msdyn_botapplicationid IS NOT NULL`. | Whether a bot handled the conversation at any point. |
| `IsAgentInvolved` | BOOLEAN | `msdyn_sessionparticipant` + `systemuser` | 1 if any primary participant (`msdyn_mode` = 192350002) has `systemuser.msdyn_botapplicationid IS NULL`. | Whether at least one human agent was involved. |
| `IsOnlyBotInvolved` | BOOLEAN | Calculated (ETL) | Derived: `IsBotInvolved = 1 AND IsAgentInvolved = 0` | Whether the conversation was handled entirely by a bot with no human agent involvement. |

### 3.2 Offering and acceptance—was it offered to an agent and handled

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IsOffered` | BOOLEAN | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_isagentsession = 1` AND `ConversationDirectionCode = 0` | Whether the conversation was offered to a human agent queue. ACD-stamped—includes pure queue abandons where no participant record exists. Only inbound. Denominator for abandon rate. |
| `IsAgentAssigned` | BOOLEAN | `msdyn_ocsession` + `msdyn_sessionparticipant` + `systemuser` | 1 if any session has `msdyn_ocsession.msdyn_agentassignedon IS NOT NULL` AND primary participant is human (`systemuser.msdyn_botapplicationid IS NULL`). | Whether a human agent was assigned (may not have accepted yet). |
| `IsAgentAccepted` | BOOLEAN | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_isagentaccepted` | Whether a human agent accepted the conversation. ACD-stamped field. |
| `IsEngaged` | BOOLEAN | Calculated (ETL) | Derived: `IsOffered = 1 AND IsAgentAccepted = 1` | Whether the conversation was both offered to and accepted by a human agent. Used for engaged conversation counts. |
| `IsHandledWithResponse` | BOOLEAN | Calculated (ETL) | Derived: `IsEngaged = 1 AND FirstResponseTimeInSeconds IS NOT NULL` | Whether the agent actually sent a response (not just accepted). For auto-accept scenarios where acceptance alone doesn't mean "handled". |

### 3.3 Bot outcomes

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IsBotAccepted` | BOOLEAN | `msdyn_sessionparticipant` + `systemuser` | 1 if bot participant AND (`msdyn_sessionparticipant.msdyn_joinedon` OR `msdyn_sessionparticipant.msdyn_lefton` is not empty). | Whether the bot actually accepted and participated (not just assigned). |
| `IsBotEscalated` | BOOLEAN | `msdyn_ocsession` + `systemuser` | 1 if bot session AND `msdyn_ocsession.msdyn_closurereason` IN (192350000, 192350026, 192350029, 192350030, 192350031). | Whether the bot escalated to a human agent. Closure reasons: Default, BotTransferToAgent, BotCallFailure*. |
| `IsBotResolved` | BOOLEAN | `msdyn_ocsession` + `systemuser` | 1 if bot session AND `msdyn_ocsession.msdyn_closurereason` IN (192350005, 192350020, 192350021, 192350022, 192350027). If `IsBotEscalated = 1`, forced to 0 (escalation takes precedence). | Whether the bot resolved without a human agent. Closure reasons: ConversationClosed, CustomerDisconnect, AgentEnd, CustomerEnd, BotEnd. |

### 3.4 Session counts

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `SessionCount` | INT | `msdyn_ocsession` | COUNT of `msdyn_ocsession.msdyn_sessionid` for this conversation. | Total sessions (bot + agent). A transfer creates a new session. |
| `AgentSessionCount` | INT | `msdyn_ocsession` + `msdyn_sessionparticipant` + `systemuser` | COUNT of sessions where primary participant is human (`systemuser.msdyn_botapplicationid IS NULL`). | Human agent sessions only. Excludes bot sessions. |

### 3.5 Duration metrics

Handle, talk, hold, and chat durations use ACD-stamped fields from `msdyn_ocliveworkitem`. Active and inactive durations use the session-participant rollup.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `HandleTimeInSeconds` | BIGINT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_conversationhandletimeinseconds` | ACD-stamped total handle time across all sessions. |
| `TalkTimeInSeconds` | BIGINT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_conversationtalktimeinseconds` | ACD-stamped total voice talk time across all sessions. Voice channel only. |
| `HoldTimeInSeconds` | BIGINT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_conversationholdtimeinseconds` | ACD-stamped total hold time across all sessions. Voice channel only. |
| `ActiveTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | SUM of `msdyn_sessionparticipant.msdyn_activetime` for primary participants (`msdyn_mode` = 192350002) across all sessions. | Total active engagement time across all sessions. |
| `InactiveTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | SUM of `msdyn_sessionparticipant.msdyn_inactivetime` for primary participants (`msdyn_mode` = 192350002) across all sessions. | Total inactive time (customer idle) across all sessions. |
| `ActiveChatTimeInSeconds` | BIGINT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_conversationactivechattimeinseconds` | ACD-stamped active chat time. Chat channel only. |

### 3.6 Messages and response time

These counts and response times combine `msdyn_conversationmessageblock` data across all sessions.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IncomingMessages` | BIGINT | `msdyn_conversationmessageblock` | SUM of `msdyn_inboundmessagecountwithinoh` across all sessions (`msdyn_agentresponsesessionid`). | Total customer messages within operating hours. |
| `OutgoingMessages` | BIGINT | `msdyn_conversationmessageblock` | SUM of `msdyn_outboundmessagecountwithinoh` across all sessions (`msdyn_agentresponsesessionid`). | Total agent messages within operating hours. |
| `FirstResponseTimeInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | Block WHERE msdyn_isfirstresponsetime = true → COALESCE(msdyn_responsetimeadjforoh, msdyn_responsetimenotadjforoh) / 1000. NOT from LWI field (has bug—always 0 for out-of-OH conversations). | How long the customer waited from first message to the first agent reply. Key customer experience metric. |
| `FirstResponseTimeAfterAcceptanceInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | Same isfirstresponsetime = true block → COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) / 1000 | How quickly the first agent responded after accepting. Measures agent responsiveness only, excludes queue wait. |
| `TotalResponseTimeInSeconds` | DOUBLE | `msdyn_conversationmessageblock` | SUM of COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) / 1000 across all blocks for this conversation WHERE value >= 0 | Sum of agent response times across all exchanges. Numerator for avg response time. |
| `MessageBlockCount` | BIGINT | `msdyn_conversationmessageblock` | COUNT of blocks WHERE COALESCE(msdyn_agentresponsetimeadjforoh, msdyn_agentresponsetimenotadjforoh) IS NOT NULL AND >= 0 | Number of customer→agent message exchanges. Denominator for avg response time. |
| `AvgResponseTimeInSeconds` | DOUBLE | Calculated | `TotalResponseTimeInSeconds / NULLIF(MessageBlockCount, 0)` | Average agent response time. No averaging-averages issue. |

---

## 4. Transfers and overflow

Use these columns to track movement between queues, transfers to external numbers, voicemail routing, and overflow.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `TransferCount` | INT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_transfercount` | Number of times the conversation was transferred between queues or agents. |
| `IsCallback` | BOOLEAN | `msdyn_sessionextension` | 1 if any `msdyn_sessionextension.msdyn_overflowaction` = 419550001 for this conversation. | Whether the conversation was routed as a callback due to overflow. |
| `IsExternalTransfer` | BOOLEAN | `msdyn_sessionextension` | 1 if any `msdyn_sessionextension.msdyn_overflowaction` = 419550002 for this conversation. | Whether the conversation was transferred to an external phone number due to overflow. |
| `IsVoicemail` | BOOLEAN | `msdyn_sessionextension` | 1 if any `msdyn_sessionextension.msdyn_overflowaction` = 419550003 for this conversation. | Whether the conversation was routed to voicemail due to overflow. |
| `IsOutOfOperatingHours` | BOOLEAN | `msdyn_sessionextension` | 1 if any `msdyn_sessionextension.msdyn_overflowcondition` = 419550000 for this conversation. | Whether the conversation came in outside of configured business operating hours. |
| `LastOverflowConditionCode` | INT | `msdyn_sessionextension` | `msdyn_sessionextension.msdyn_overflowcondition` from the last-closed session extension | Foreign Key to DimOverflowCondition. Overflow trigger for the most recent session. |
| `LastOverflowActionCode` | INT | `msdyn_sessionextension` | `msdyn_sessionextension.msdyn_overflowaction` from the last-closed session extension | Foreign Key to DimOverflowAction. Overflow action taken for the most recent session. |

---

## 5. Wrapup, close, and outcome

These columns describe how the conversation ended, including wrapup, closure, total duration, and final outcome.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `WrapupInitiatedOnDateTime` | TIMESTAMP | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_wrapupinitiatedon` | When the conversation entered wrapup state. |
| `WrapupTimeInSeconds` | BIGINT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_conversationwrapuptimeinseconds` | ACD-stamped total wrapup time across all sessions. |
| `ActiveWrapupTimeInSeconds` | BIGINT | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_conversationactivewrapuptimeinseconds` | ACD-stamped active wrapup time across all sessions. Subset of WrapupTimeInSeconds. |
| `ClosedOnDateTime` | TIMESTAMP | `msdyn_ocliveworkitem` | `msdyn_ocliveworkitem.msdyn_closedon` | When the conversation was closed. NULL if still open/active. |
| `ConversationDurationInSeconds` | BIGINT | Calculated | `msdyn_ocliveworkitem.msdyn_closedon` - `msdyn_ocliveworkitem.msdyn_createdon` | Wall-clock duration from creation to close. NULL if not yet closed. |
| `CustomerEffortInSeconds` | BIGINT | Calculated | `msdyn_ocliveworkitem.msdyn_wrapupinitiatedon` - `msdyn_ocliveworkitem.msdyn_createdon` | Time from creation to wrapup initiation—customer-facing effort. NULL if wrapup not initiated. |
| `ConversationOutcome` | STRING | `msdyn_ocsession` + `systemuser` | Derived from bot/agent flags (rows 28-38) and `msdyn_ocsession.msdyn_closurereason`. | Conversation outcome classification: Bot resolved, Bot escalated, Direct agent conversations. Derived at ETL. |

---

## 6. Quality and sentiment

Use these columns to review survey feedback, AI sentiment, and customer-reported resolution.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `Survey_CSATScore` | DOUBLE | `msdyn_customerfeedbacksurveyresponse` + `msfp_surveyresponse` | Primary: `msdyn_customerfeedbacksurveyresponse` → `msdyn_satisfactionmetricvalue` JSON where type = 'csat', joined via `msdyn_regardingobjectid`. <br> Fallback: `msfp_surveyresponse` → `msfp_satisfactionmetricvalue` JSON where type = 'csat', joined via `msfp_embedcontextparameters` JSON ConversationId. | Customer satisfaction score. MCS preferred, Customer Voice as fallback. |
| `Survey_NPSScore` | INT | `msdyn_customerfeedbacksurveyresponse` + `msfp_surveyresponse` | Primary: `msdyn_customerfeedbacksurveyresponse.msdyn_response` JSON → `MCS_NetPromoterScore` (latest by `modifiedon`). <br> Fallback: `msfp_surveyresponse.msfp_npsscore` (direct INT column) when MCS NPS is NULL. | Net Promoter Score. MCS preferred, Customer Voice as fallback. |
| `Survey_CustomerEffortScore` | INT | `msdyn_customerfeedbacksurveyresponse` | `msdyn_response` JSON → `MCS_CustomerEffortScore`. Latest by `modifiedon`. MCS only—Customer Voice does not have this field. | Customer Effort Score—how easy/difficult the customer found the interaction. |
| `Survey_IsResolved` | BOOLEAN | `msdyn_customerfeedbacksurveyresponse` | `msdyn_response` JSON → `MCS_Resolution`. 1 if starts with "Yes", 0 otherwise, NULL if absent. MCS only. | Whether the customer reported their issue as resolved. |
| `Survey_IsResolvedInFirstContact` | BOOLEAN | `msdyn_customerfeedbacksurveyresponse` | `msdyn_response` JSON → `MCS_Resolution`. 1 if = "Yes, during my first contact", 0 otherwise. MCS only. | First Contact Resolution (FCR). |
| `Survey_Source` | STRING | Calculated (ETL) | `"MCS"` if `msdyn_customerfeedbacksurveyresponse` found (preferred). `"CustomerVoice"` if only `msfp_surveyresponse` found (fallback). NULL if no survey response. | Which survey entity the scores came from. MCS preferred, Customer Voice as fallback. |
| `SentimentPulse` | DOUBLE | `msdyn_ocliveworkitemsentiment` | `msdyn_ocliveworkitemsentiment.msdyn_sentimentpulse`, joined via `msdyn_transcript.msdyn_liveworkitemid` = conversation ID. Dedup by `modifiedon DESC`. | AI-computed sentiment score (0-100). Higher = more positive. |
| `SentimentZone` | STRING | `msdyn_ocliveworkitemsentiment` | `msdyn_ocliveworkitemsentiment.msdyn_sentimentzone`, same join path as SentimentPulse. | AI sentiment category: Positive, Neutral, or Negative. |
| `Survey_SentimentScore` | DOUBLE | `msfp_questionresponse` | AVG of `msfp_questionresponse.msfp_sentimentvalue` where question type = 647390001. 0 values treated as NULL. | Survey-based sentiment score. Different from AI SentimentPulse—comes from explicit survey questions. |

---

## 7. ETL and system

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `_StartDate` | DATE | Date portion of `msdyn_ocliveworkitem.msdyn_createdon` | Delta Lake partition column. Same value as CreatedOnDate (row 26). Enables partition pruning for efficient incremental reads. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | Set by ETL at pipeline runtime | When this row was last written/updated by the ETL pipeline. Used for freshness monitoring and debugging. |

---

## Source entities

| Dataverse entity | Contribution |
|-----------|---------------------|
| `msdyn_ocliveworkitem` | Identity, Foreign Keys, timestamps, ACD-stamped durations (handle, talk, hold, wrapup, first wait), status, direction, title, abandoned/outbound flags, transfer count |
| `msdyn_ocsession` | Session counts, wait/answer/speed-to-answer, closure reasons → outcomes, bot escalation/resolution |
| `msdyn_sessionparticipant` | Active/inactive time, bot/agent detection (via `systemuser.msdyn_botapplicationid`), agent acceptance |
| `msdyn_sessionextension` | Overflow condition/action, callback/voicemail/external transfer flags |
| `systemuser` | BusinessUnitId (via `msdyn_activeagentid`), bot detection (`msdyn_botapplicationid`) |
| `msdyn_ocliveworkitemsentiment` + `msdyn_transcript` | SentimentPulse, SentimentZone |
| `msfp_surveyresponse` + `msdyn_customerfeedbacksurveyresponse` | Survey_CSATScore, Survey_NPSScore, Survey_CustomerEffortScore, Survey_IsResolved, Survey_IsResolvedInFirstContact, Survey_Source |
| `msfp_question` + `msfp_questionresponse` | Survey_SentimentScore |
| `msdyn_conversationmessageblock` | IncomingMessages, OutgoingMessages, FirstResponseTimeInSeconds, FirstResponseTimeAfterAcceptanceInSeconds, TotalResponseTimeInSeconds, MessageBlockCount |

> **Pipeline dependency:** **FactConversation runs after FactSession.** The FactSession generator supplies in-memory session fields through `StgConversationSessionAgg`, aggregated by conversation.

## Filters

```sql
WHERE msdyn_ocliveworkitemid IS NOT NULL
  AND msdyn_channel != '192350000'   -- Exclude Entity Records channel
```

## Related tables

Use `FactConversation` with these tables.

| Table | Purpose |
|-------|---------|
| AggConversation | Provides conversation aggregates for trend reporting. |
| DimChannel | Provides channel names. |
| DimConversationDirection | Provides inbound and outbound labels. |
| DimConversationStatus | Provides conversation status labels. |
| DimConversationType | Provides conversation type labels. |
| DimLiveWorkStream | Provides workstream attributes. |
| DimOverflowAction | Provides overflow action labels. |
| DimOverflowCondition | Provides overflow trigger labels. |
| DimQueue | Provides queue attributes and thresholds. |
| DimSystemUser | Provides active agent attributes. |
| DimTimeZone | Supports local-time reporting. |
| FactSession | Provides the individual sessions within a conversation. |
