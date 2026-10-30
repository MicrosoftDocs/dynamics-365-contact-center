---
title: AggAgentCapacity table reference
description: Reference information for the AggAgentCapacity aggregate table in the Dynamics 365 Customer Service Shared Analytics Platform data model.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-assisted
---
# AggAgentCapacity table reference

Use `AggAgentCapacity` to analyze service representative capacity by profile over time. It summarizes capacity-change history in fixed 30-minute UTC intervals for comparison across periods, representatives, profiles, and business units.

The table contains capacity summaries, not individual conversations. Use it with `AggAgentAvailability` to analyze capacity separately from presence.

## Grain and source

- **Grain:** One row per service representative, capacity profile, 30-minute UTC interval, and business unit, per day.
- **Primary source table:** `FactAgentCapacityHistory`.

### Source tables

| Source table | Purpose |
|---|---|
| `FactAgentCapacityHistory` | Stores capacity-history records and is the primary source for the aggregate table. |
| `DimCapacityProfile` | Stores capacity-profile metadata, including profile name, default maximum units, and block-assignment setting. |
| `FactAgentCapacityProfileUnit` | Stores service representative-level capacity-profile overrides used to determine effective maximum capacity. |
| `systemuser` | Resolves `AgentId` to `BusinessUnitId` during ETL processing. |

## How data is aggregated

The aggregation process:

1. Reads capacity-state changes from `msdyn_agentcapacityupdatehistory` through `FactAgentCapacityHistory`.
2. Splits a capacity state at 30-minute boundaries when the state spans more than one interval.
3. Resolves the business unit from `systemuser`.
4. Uses the service representative override as the effective maximum capacity when an override exists. Otherwise, it uses the capacity profile’s default maximum capacity units.
5. Aggregates the split records into one row for each 30-minute interval.

## Dimension columns

Use the following dimensions to group and filter capacity by time, service representative, profile, and organizational structure.

| Column | Type | Source | Source field or ETL logic | Description |
|----------|----------|----------|----------|----------|
| DateTimeKey | BIGINT | FactAgentCapacityHistory | 30-minute aligned key derived from StartDateTime | 30-minute UTC reporting interval. Use it for capacity trends and joins to date and time dimensions. |
| AgentId | STRING | FactAgentCapacityHistory | Direct from source | Service representative whose capacity is recorded. Links to workforce, performance, and organizational reporting dimensions. |
| CapacityProfileId | STRING | FactAgentCapacityHistory | Direct from source | Service representative's capacity profile. Use it to analyze utilization and availability by workload type or routing profile. |
| BusinessUnitId | STRING | systemuser | Resolved by joining the service representative to systemuser.businessunitid and denormalized during ETL | Service representative's business unit, used for capacity reporting across departments or business groups. |

## Metric columns

These 30-minute measurements describe capacity availability, utilization, and assignment behavior for dashboards and custom reports. [Capacity metrics reference](../../use/capacity-metrics-dashboard.md) provides metric definitions and report calculations.

| Column | Type | Source | Calculation or ETL logic | Description |
|----------|----------|----------|----------|----------|
| TotalCapacityUnits | DOUBLE | FactAgentCapacityHistory | SUM(EffectiveMaxUnits * duration) / SUM(duration) | Time-weighted average maximum capacity during the interval: the capacity that could be assigned to the service representative. |
| AvailableCapacityUnits | DOUBLE | FactAgentCapacityHistory | SUM(AvailableCapacityUnits * duration) / SUM(duration) | Time-weighted average capacity remaining for new assignments during the interval. Negative values mean assigned work exceeded the configured limit. |
| BlockedAssignmentDurationInSeconds | BIGINT | FactAgentCapacityHistory | SUM(duration WHERE msdyn_blockassignment = true) | Total seconds during which capacity limits blocked new work assignments. |
| IsUnitBased | BOOLEAN | FactAgentCapacityHistory | MAX(IsUnitBased) | Indicates whether the capacity profile uses unit-based capacity calculations or profile-based capacity calculations. Use this field to distinguish between different capacity-management models in reporting. |
| CapacityUpdateCount | INT | FactAgentCapacityHistory | COUNT(*) | Number of contributing capacity-change events. Higher values can indicate frequent adjustments during the interval. |

## Metadata columns

Use these system-generated columns for partitioning, data lineage, refresh monitoring, troubleshooting, and data quality and freshness checks.

| Column | Type | Source | Calculation or ETL logic | Description |
|----------|----------|----------|----------|----------|
| _AggregationDate | DATE | FactAgentCapacityHistory | Date portion of the 30-minute interval start time | Interval date, used for partitioning and joins to the date dimension. |
| _SourceRecordCount | INT | ETL | COUNT(*) | Number of source records combined into the row. Use it for validation and data quality investigations. |
| _LastRefreshedDateTimeUtc | TIMESTAMP | ETL | current_timestamp() | UTC timestamp of the most recent table refresh. Use it to check freshness and monitor ETL execution. |
