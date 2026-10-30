---
title: FactAgentStatusHistory table reference
description: Reference information for the FactAgentStatusHistory table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# FactAgentStatusHistory table reference

Use `FactAgentStatusHistory` to review an agent's availability over time. **Presence status** can be Available, Busy, Away, Busy-DND, Offline, or a custom status such as "Training Break" or "Lunch". Dataverse records each presence change and the status period's start and end times. Changes can come from the agent, a supervisor override, or the system, such as automatically setting Busy when the agent accepts a conversation.

## Business value

Use this table to track the full agent presence timeline:

- Review when each agent held a status, such as Available from 9:00–9:45 and Busy from 9:45–10:30.
- Measure the duration of each status period.
- Identify who changed the status—agent, supervisor, or system—through `PresenceModifiedByUserId`.
- Review the available capacity snapshot taken when the status changed.

For reporting summaries in 30-minute intervals, use the companion aggregate `AggAgentAvailability`.

## Grain

The table stores one row per agent status period (`StatusHistoryId`).

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_agentstatushistory | Provides status periods, capacity snapshots, and presence changes. |
| systemuser | Provides the agent's business unit. |

## 1. Identity and foreign keys

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `StatusHistoryId` | STRING | `msdyn_agentstatushistory` | `msdyn_agentstatushistoryid` | Primary Key. One row per status period. |
| `AgentId` | STRING | `msdyn_agentstatushistory` | `msdyn_agentid` | Foreign Key to DimSystemUser. |
| `PresenceId` | STRING | `msdyn_agentstatushistory` | `msdyn_presenceid` | Foreign Key to DimPresence. |
| `BusinessUnitId` | STRING | `systemuser` | `businessunitid` via `msdyn_agentid = systemuserid` | Foreign Key to DimBusinessUnit. Denormalized at ETL. Type 1 SCD. |

---

## 2. Timestamps

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `StartDateTime` | TIMESTAMP | `msdyn_agentstatushistory` | `msdyn_starttime` | When this status period began. |
| `EndDateTime` | TIMESTAMP | `msdyn_agentstatushistory` | `msdyn_endtime` | When this status period ended. NULL for in-progress. |

---

## 3. Duration and capacity

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `StatusDurationInSeconds` | BIGINT | Computed | `unix_timestamp(EndDateTime) - unix_timestamp(StartDateTime)` | Duration of this status period in seconds. NULL if in-progress. |
| `AvailableCapacity` | INT | `msdyn_agentstatushistory` | `msdyn_availablecapacity` | Available capacity snapshot at time of status change. |

---

## 4. Flags

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IsLoggedIn` | BOOLEAN | `msdyn_agentstatushistory` | `msdyn_isagentloggedin` | TRUE if agent is logged in (presence != Offline). |
| `PresenceModifiedByUserId` | STRING | `msdyn_agentstatushistory` | `msdyn_presencemodifiedbyuserid` | Foreign Key to DimSystemUser. Who changed the presence—agent themselves, supervisor, or system. |

---

## 5. ETL and system

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `_StartDate` | DATE | `to_date(msdyn_starttime)` | Delta partition column. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | `current_timestamp()` | Pipeline refresh timestamp. |

---

## Source entities

| Dataverse entity | Contribution |
|-----------|---------------------|
| `msdyn_agentstatushistory` | Status history ID, agent, presence, start/end times, capacity, logged-in flag, presence modifier |
| `systemuser` | BusinessUnitId (via `msdyn_agentid`) |

## Filters

```sql
WHERE msdyn_agentstatushistoryid IS NOT NULL
```

## Related tables

Use `FactAgentStatusHistory` with these tables.

| Table | Purpose |
|-------|---------|
| AggAgentAvailability | Provides 30-minute presence summaries. |
| DimBusinessUnit | Provides business unit information. |
| DimPresence | Provides presence names and base status classifications. |
| DimSystemUser | Provides agent and presence modifier attributes. |
| DimTimeZone | Supports local-time reporting. |
