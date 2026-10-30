---
title: AggAgentPerformance table (Dynamics 365 Customer Service analytics)
description: Reference information for the AggAgentPerformance table in the Shared Analytics Platform data model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.custom: bap-template
ai-usage: ai-assisted
---
# AggAgentPerformance table reference

Use `AggAgentPerformance` for supervisor and operational reports on service representative performance. It combines session, participant, conversation, messaging, callback, response-time, quality, and sentiment data in a preaggregated model.

The table includes only customer service representative participation in customer interactions; it excludes agent-only sessions. Supervisors and analysts can compare workload, responsiveness, handling effort, customer experience outcomes, and callback performance across primary, consult, and monitor roles.

Use this table with conversation-level and queue-level analytics to:

- Analyze service representative workload and participation levels.
- Measure responsiveness and handling efficiency.
- Evaluate performance across primary, consult, and monitor roles.
- Track callback performance and adoption.
- Monitor customer experience metrics such as CSAT, NPS, and sentiment.
- Support workforce management and coaching scenarios.

## Grain and source

**Grain:** One row per unique combination of the 12 dimensions listed below. `DateTimeKey` identifies the 15-minute interval when the session was created. Multiple sessions can contribute to one row.

The table is aggregated by the following dimensions.

```sql
GROUP BY
    DateTimeKey,
    QueueId,
    ChannelCode,
    ConversationStatusCode,
    AgentBusinessUnitId,
    ConversationDirectionCode,
    AgentId,
    SessionStateCode,
    SessionState,
    SessionStatusCode,
    SessionStatus,
    ParticipantModeCode
```

Each row combines session and participant records with matching dimension values. It doesn't represent an individual session.

### Source tables

These sources combine session and participant activity with conversation context.

| Source table | Purpose |
|---|---|
| **FactSession** | Primary source for session-level metrics, including queue information, channel, wait times, answer times, handling durations, session durations, callback attributes, and session outcomes. |
| **FactSessionParticipant** | Provides participant-level activity such as agent identity, participant role, active time, inactive time, idle time, talk time, hold time, chat time, wrap-up time, and participant message activity. |
| **FactConversation** | Provides conversation-level attributes, including conversation status, conversation direction, service representative business unit, customer sentiment, CSAT scores, and NPS scores. |

### How rows are created

Data processing assigns each session to a 15-minute interval based on its creation time, combines it with participant and conversation details, and groups records with matching dimension values. It doesn't split session activity across intervals.

`TotalSessions` and `_SourceRecordCount` count the combined records, not distinct sessions. A session with multiple participants contributes a record for each participant. Sessions without a matching participant record are also retained.

For example:

| Queue | Agent | Role | Channel | Status | Interval |
|---------|---------|---------|---------|---------|---------|
| Support | Agent A | Primary | Chat | Closed | 09:00 |
| Support | Agent A | Primary | Chat | Closed | 09:00 |
| Support | Agent A | Primary | Chat | Closed | 09:00 |

These three accepted sessions produce one aggregate row if all 12 dimension values match, including those not shown in the example.

Example output:

```text
AcceptedSessions = 3
TotalHandleTimeInSeconds = 1800
TotalResponseTimeInSeconds = 420
TotalIncomingMessages = 95
```

Aggregation improves reporting performance while retaining activity patterns and workload characteristics.

## Dimension columns

Use the following dimensions to group and filter performance by queue, channel, organizational unit, participant role, and session outcome.

### Universal dimensions

| Column | Type | Source table | Source field or ETL logic | Description |
|---|---|---|---|---|
| DateTimeKey | BIGINT | FactSession | CreatedOnDateKey | Identifies the 15-minute interval when the session was created. Enables trend analysis by session creation time. |
| QueueId | STRING | FactSession | QueueId | Identifies the queue associated with the session. Supports queue-level workload and performance analysis. |
| ChannelCode | INT | FactSession | ChannelCode | Identifies the channel used for customer interaction, such as voice or messaging. |
| ConversationStatusCode | INT | FactConversation | ConversationStatusCode (via ConversationId) | Identifies the status of the parent conversation, allowing performance analysis by conversation outcome. |
| AgentBusinessUnitId | STRING | FactConversation | AgentBusinessUnitId (via ConversationId) | Identifies the business unit associated with the service representative. Supports organizational reporting and performance comparisons. |
| ConversationDirectionCode | INT | FactConversation | ConversationDirectionCode (via ConversationId) | Distinguishes inbound and outbound interactions. |

### Table-specific dimensions

| Column | Type | Source table | Source field or ETL logic | Description |
|---|---|---|---|---|
| AgentId | STRING | FactSessionParticipant | AgentId | Identifies the service representative associated with the activity record. Enables individual performance reporting and coaching analysis. |
| SessionStateCode | INT | FactSession | SessionStateCode | Identifies the lifecycle state of the session. |
| SessionState | STRING | FactSession | SessionState | Human-readable session lifecycle status used in reports and filters. |
| SessionStatusCode | INT | FactSession | SessionStatusCode | Detailed session status reason within the state. |
| SessionStatus | STRING | FactSession | SessionStatus | Human-readable session status value used for reporting and filtering. |
| ParticipantModeCode | INT | FactSessionParticipant | ParticipantModeCode | Identifies the participant role in the session, such as Primary, Consult, or Monitor. |

### Participant mode reference

| Code | Value | Description |
|---|---|---|
| 192350002 | Primary | Primary service representative responsible for handling the session. |
| 192350003 | Consult | Consult participant who can actively participate in the interaction. |
| 192350004 | Monitor | Monitoring participant or supervisor observing the interaction. |

## Metric columns

The table stores counts and totals, not calculated averages. Reports use these values to calculate performance metrics at query time.

### Volume metrics

Use volume metrics to measure workload, participation, session outcomes, and transfers.

| Column | Type | Source | Source field or ETL logic | Description |
|---|---|---|---|---|
| TotalSessions | INT | FactSession + FactSessionParticipant | COUNT(*) | Counts combined session and participant records, including sessions without a matching participant. It isn't a distinct session count. |
| AcceptedSessions | INT | FactSession + FactSessionParticipant | Mode-aware acceptance logic | Stores sessions accepted by the participant according to role-specific acceptance criteria. |
| RejectedSessions | INT | FactSession + FactSessionParticipant | Mode-aware rejection logic | Stores sessions rejected by participants according to role-specific rejection conditions. |
| TimedOutSessions | INT | FactSession + FactSessionParticipant | Mode-aware timeout logic | Stores sessions that timed out before participant acceptance. |
| TransferredSessions | INT | FactSession | Transfer closure reasons | Stores sessions transferred by the service representative to another destination. |

### Time metrics

Use these durations to measure handling effort, engagement, inactivity, and session lifecycle timing. All values are in seconds.

| Column | Type | Description |
|---|---|---|
| TotalHandleTimeInSeconds | BIGINT | Stores cumulative session handling time for participating service representatives. |
| TotalWaitTimeInSeconds | BIGINT | Stores cumulative customer wait time before session acceptance. |
| TotalAnswerTimeInSeconds | BIGINT | Stores cumulative answer time across sessions. |
| TotalActiveTimeInSeconds | BIGINT | Stores cumulative active engagement time during customer interactions. |
| TotalInactiveTimeInSeconds | BIGINT | Stores cumulative inactive time during sessions. |
| TotalIdleTimeInSeconds | BIGINT | Stores cumulative idle time where the participant wasn't actively handling work. |
| TotalTalkTimeInSeconds | BIGINT | Stores cumulative voice conversation time. |
| TotalHoldTimeInSeconds | BIGINT | Stores cumulative customer hold time. |
| TotalActiveChatTimeInSeconds | BIGINT | Stores cumulative active messaging time. |
| TotalWrapupTimeInSeconds | BIGINT | Stores cumulative post-interaction wrap-up effort. |
| TotalSessionDurationInSeconds | BIGINT | Stores cumulative session duration for completed sessions. |

### Response time metrics

Use these totals and counts to calculate service representative response times during customer interactions.

| Column | Type | Description |
|---|---|---|
| TotalFirstMessageResponseTimeInSeconds | DOUBLE | Stores cumulative first-response times across conversations. |
| FirstMessageResponseCount | INT | Stores the number of interactions contributing to first-response calculations. |
| TotalResponseTimeInSeconds | DOUBLE | Stores cumulative response times across all customer-service representative exchange cycles. |
| MessageBlockCount | INT | Stores the total number of customer-to-service representative exchange cycles. |
| TotalFirstResponseTimeAfterAcceptanceInSeconds | DOUBLE | Stores cumulative time between session acceptance and first response. |
| FirstResponseTimeAfterAcceptanceCount | INT | Stores the number of interactions contributing to first-response-after-acceptance calculations. |

### Quality metrics

Use customer feedback and sentiment metrics to evaluate service representative performance.

| Column | Type | Description |
|---|---|---|
| TotalSentimentPulse | DOUBLE | Stores cumulative AI-generated sentiment values associated with conversations handled by the service representative. |
| SentimentPulseCount | INT | Stores the number of sentiment observations represented in the aggregated row. |
| Survey_TotalCSATScore | DOUBLE | Stores cumulative customer satisfaction scores. |
| Survey_CSATResponseCount | INT | Stores the number of customer satisfaction survey responses. |
| Survey_TotalNPSScore | DOUBLE | Stores cumulative Net Promoter Scores. |
| Survey_NPSResponseCount | INT | Stores the number of Net Promoter Score survey responses. |

### Message and callback metrics

Use these metrics to measure messaging activity and callback performance across customer interactions.

| Column | Type | Description |
|---|---|---|
| TotalIncomingMessages | INT | Stores the total number of customer messages. |
| TotalOutgoingMessages | INT | Stores the total number of service representative messages. |
| CallbacksOffered | INT | Stores the number of callback opportunities presented to customers. |
| CallbacksOptedIn | INT | Stores the number of callback offers accepted by customers. |
| CallbacksInitiated | INT | Stores callbacks that progressed through offer, acceptance, and service representative assignment. |
| CallbacksAcceptedByAgent | INT | Stores callback sessions accepted by a service representative. |
| CallbacksAnswered | INT | Stores callbacks where the customer successfully connected after callback initiation. |

## Metadata columns

Use these system-generated columns for partitioning, refresh tracking, operational monitoring, and data lineage.

| Column | Type | Source table | Source field or ETL logic | Description |
|---|---|---|---|---|
| _AggregationDate | DATE | FactSession | CreatedOnDate | Date associated with the aggregation interval. Used as a partition column and foreign key to DimDate. |
| _SourceRecordCount | INT | ETL | COUNT(*) | Number of source records aggregated into the output row. Useful for validation and troubleshooting. |
| _LastRefreshedDateTimeUtc | TIMESTAMP | ETL | current_timestamp() | UTC timestamp of the most recent ETL refresh operation. |
