---
title: FactSessionParticipant table reference
description: Reference information for the FactSessionParticipant table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# FactSessionParticipant table reference

Use `FactSessionParticipant` to examine each agent's or bot's involvement in a session. Unlike the session-level view in `FactSession`, this table records **every participant** individually.

## Business value

Use this table to analyze participants by role:

- **Primary agent** (mode 192350002): The agent who handled the session end to end.
- **Consult agent** (mode 192350003): An agent brought in for consultation during the session.
- **Monitor agent** (mode 192350004): A supervisor silently monitoring the session.

This table answers:

- How long was each agent actively engaged (active time, talk time, hold time, wrapup)?
- Which sessions had consult or monitor participants?
- When did each participant join and leave?
- How did each participant's idle time compare with active time?

Use the participant details for agent performance drill-down, consult and monitor analytics, and capacity modeling. For aggregates by `ParticipantModeCode`, use `AggAgentPerformance`.

## Grain

The table stores one row per participant per session (`SessionParticipantId`).

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_sessionparticipant | Provides participant identity, role, timestamps, and activity durations. |

## 1. Identity and foreign keys

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `SessionParticipantId` | STRING | `msdyn_sessionparticipant` | `msdyn_sessionparticipantid` | Primary Key |
| `SessionId` | STRING | `msdyn_sessionparticipant` | `msdyn_omnichannelsession` | Foreign Key to FactSession. |
| `AgentId` | STRING | `msdyn_sessionparticipant` | `CASE WHEN msdyn_externalparticipantchannel IS NULL OR msdyn_externalparticipantchannel = '' THEN msdyn_agentid ELSE msdyn_externalparticipantchannel END` | Foreign Key to DimSystemUser. Falls back to external participant channel for transferred calls (v1 DimSystemUserId logic). |
| `ParticipantModeCode` | INT | `msdyn_sessionparticipant` | `msdyn_mode` | Foreign Key to DimParticipantMode. 192350002=Primary, 192350003=Consult, 192350004=Monitor. |

---

## 2. Timestamps

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `AgentAddedOnDateTime` | TIMESTAMP | `msdyn_sessionparticipant` | `msdyn_addedon` | When the agent was added to the session. |
| `AgentJoinedOnDateTime` | TIMESTAMP | `msdyn_sessionparticipant` | `msdyn_joinedon` | When the agent joined. NULL if added but never accepted. |
| `AgentLeftOnDateTime` | TIMESTAMP | `msdyn_sessionparticipant` | `msdyn_lefton` | When the agent left. NULL if still active. |

---

## 3. Duration metrics (seconds)

Dataverse stores all `msdyn_sessionparticipant` time metrics in seconds. This table passes them through without conversion.

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `ActiveTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | `msdyn_activetime` | Time the agent was actively engaged. |
| `InactiveTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | `msdyn_inactivetime` | Time the session was inactive (no agent response). |
| `IdleTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | `msdyn_idletime` | Time the agent was idle. |
| `TalkTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | `msdyn_talktime` | Voice talk time. |
| `HoldTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | `msdyn_holdtime` | Hold time. |
| `ActiveChatTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | `msdyn_activechattime` | Active chat engagement time. |
| `ActiveWrapupTimeInSeconds` | BIGINT | `msdyn_sessionparticipant` | `msdyn_activewrapuptime` | Active wrapup / after-call work time. |
| `TotalParticipantTimeInSeconds` | BIGINT | Calculated | `unix_timestamp(msdyn_lefton) - unix_timestamp(msdyn_joinedon)` | Wall-clock participation duration. NULL if either timestamp absent. |

---

## 4. Classification

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `LeftOnReason` | STRING | `msdyn_sessionparticipant` | `msdyn_leftonreason` | Why the agent left: AgentReject, AgentTimeout, AgentLeft, SessionComplete. |

---

## 5. ETL and system

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `_StartDate` | DATE | `to_date(msdyn_sessionparticipant.createdon)` | Delta partition column. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | `current_timestamp()` | Pipeline refresh timestamp. |

---

## Source entities

| Dataverse entity | Contribution |
|-----------|---------------------|
| `msdyn_sessionparticipant` | All 16 business columns—identity, role, timestamps, duration metrics |

> **Single source:** The table uses no secondary joins or deduplication. Each participant has one `msdyn_sessionparticipantid` per session.

## Filters

```sql
WHERE msdyn_sessionparticipantid IS NOT NULL
```

## Related tables

Use `FactSessionParticipant` with these tables.

| Table | Purpose |
|-------|---------|
| AggAgentPerformance | Provides performance aggregates by participant role. |
| DimParticipantMode | Provides Primary, Consult, and Monitor role labels. |
| DimSystemUser | Provides agent attributes. |
| DimTimeZone | Supports local-time reporting. |
| FactSession | Provides session-level context. |
