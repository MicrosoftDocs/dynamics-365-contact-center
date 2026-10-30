---
title: FactAgentCapacityHistory table reference
description: Reference information for the FactAgentCapacityHistory table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# FactAgentCapacityHistory table reference

Use `FactAgentCapacityHistory` to examine changes in an agent's available capacity. Agents in Dynamics 365 Contact Center can have one or more **capacity profiles**, such as Chat with a maximum of three concurrent conversations or Voice with a maximum of one call. Dataverse records each capacity change, including conversation assignment or completion, supervisor force assignment, and administrator changes to the profile configuration.

## Business value

Use this table to track capacity changes over time:

- Compare available units with maximum units for each profile over time.
- Identify full capacity, when available units equal 0 and assignment is blocked.
- Identify supervisor force assignments that bypassed capacity limits.
- Review an intraday capacity timeline for each agent and profile.

For reporting summaries in 30-minute intervals, use the companion aggregate `AgentCapacityAnalytics`.

## Grain

The table stores one row per capacity state change event.

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_agentcapacityupdatehistory | Provides capacity change events, timestamps, metrics, and flags. |
| systemuser | Provides the agent's business unit. |
| msdyn_agentcapacityprofileunit | Provides agent-level overrides for maximum capacity. |

## 1. Identity and foreign keys

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `CapacityUpdateHistoryId` | STRING | `msdyn_agentcapacityupdatehistory` | `msdyn_agentcapacityupdatehistoryid` | Primary Key. MERGE key. |
| `AgentId` | STRING | `msdyn_agentcapacityupdatehistory` | `msdyn_agentid` | Foreign Key to DimSystemUser. |
| `CapacityProfileId` | STRING | `msdyn_agentcapacityupdatehistory` | `msdyn_capacityprofileid` | Foreign Key to DimCapacityProfile. |
| `BusinessUnitId` | STRING | `systemuser` | `businessunitid` via `msdyn_agentid = systemuserid` | Foreign Key to DimBusinessUnit. Broadcast join. |

---

## 2. Timestamps

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `StartDateTime` | TIMESTAMP | `msdyn_agentcapacityupdatehistory` | `msdyn_starttime` | When this capacity state began. |
| `EndDateTime` | TIMESTAMP | `msdyn_agentcapacityupdatehistory` | `msdyn_endtime` | When this capacity state ended. NULL for current/open state. |

---

## 3. Capacity metrics

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `AvailableCapacityUnits` | INT | `msdyn_agentcapacityupdatehistory` | `msdyn_availablecapacityprofileunits` | Units available. **Negative values are valid** (over-committed agent). |
| `DefaultMaxUnits` | INT | `msdyn_agentcapacityupdatehistory` | `msdyn_defaultmaxunits` | Profile-level default max, not the effective maximum. See `EffectiveMaxUnits`. |
| `EffectiveMaxUnits` | INT | Calculated | `COALESCE(msdyn_agentcapacityprofileunit.msdyn_defaultmaxunits, msdyn_defaultmaxunits)` | Maximum capacity in effect. An agent-level override takes precedence over the profile default. Uses a Type 1 slowly changing dimension (SCD), so administrator changes apply retroactively. |

---

## 4. Flags

| Column | Type | Source Entity | Source Field / ETL Logic | Description |
|--------|------|---------------|--------------------------|-------------|
| `IsAssignmentBlocked` | BOOLEAN | `msdyn_agentcapacityupdatehistory` | `msdyn_blockassignment` | New conversations blocked from routing to this agent. |
| `IsUnitBased` | BOOLEAN | `msdyn_agentcapacityupdatehistory` | `msdyn_isunitbased` | Unit-based capacity (vs conversation-count-based). |
| `IsForceAssignment` | BOOLEAN | `msdyn_agentcapacityupdatehistory` | `msdyn_isforceassignment` | Supervisor force-assigned, bypassing capacity limit. |

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
| `msdyn_agentcapacityupdatehistory` | All identity, timestamps, capacity metrics, flags |
| `systemuser` | BusinessUnitId (broadcast join on `msdyn_agentid`) |
| `msdyn_agentcapacityprofileunit` | Agent-level max override for `EffectiveMaxUnits` (broadcast join) |

## Filters

```sql
WHERE msdyn_agentcapacityupdatehistoryid IS NOT NULL
  AND msdyn_capacityprofileid IS NOT NULL
  AND statecode = 0   -- Active records only
```

## Related tables

Use `FactAgentCapacityHistory` with these dimensions.

| Table | Purpose |
|-------|---------|
| DimBusinessUnit | Provides business unit information. |
| DimCapacityProfile | Provides capacity profile attributes. |
| DimSystemUser | Provides agent attributes. |
| DimTimeZone | Supports local-time reporting. |
