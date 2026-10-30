---
title: AggAgentAvailability table reference
description: Reference information for the AggAgentAvailability table in the Shared Analytics Platform data model for Dynamics 365 Customer Service.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# AggAgentAvailability table reference

Use `AggAgentAvailability` to analyze service representative presence and availability in fixed 30-minute UTC intervals. Supervisors and analysts can review workforce availability without querying individual status history records.

The table supports the following reporting needs:

- Analyze service representative availability trends over time.
- Understand how time is distributed across presence states.
- Identify patterns in status changes and workforce behavior.
- Support workforce planning and operational reporting.
- Use preaggregated data for availability dashboards and custom analytics that need fast queries.

## Grain

For a specific business unit, each row records the time a service representative spends in one presence status during a 30-minute UTC interval.

## Source table

| Source table | Purpose |
|--------------|---------|
| FactAgentStatusHistory | Stores detailed service representative presence history and status transitions. |

Learn more about timestamp storage and local-time conversion in [Data model architecture](../overview-data-model.md#data-model-architecture).

## How data is aggregated

The aggregation process:

1. Reads presence history from FactAgentStatusHistory.
2. Groups presence records into 30-minute UTC windows.
3. Calculates the total duration spent in each presence status.
4. Counts transitions into each presence status.
5. Stores aggregated results at the defined reporting grain.

## Boundary splitting logic

Presence periods that cross reporting intervals are split at each 30-minute boundary.

For example, an **Away** period from 09:15 through 10:45 contributes:

- 09:00–09:30 window: 900 seconds.
- 09:30–10:00 window: 1,800 seconds.
- 10:00–10:30 window: 1,800 seconds.
- 10:30–11:00 window: 900 seconds.

A status transition counts only in the interval where it occurred, not in each interval spanned by the status period.

## Dimension columns

Use the following dimensions to group and filter availability reports.

| Column | Type | Description |
|----------|--------|-------------|
| DateTimeKey | BIGINT | 30-minute UTC reporting interval for time-based analysis and date/time joins. Foreign key to DimTimeZone.UtcDateTimeKey. |
| AgentId | STRING | Service representative whose availability is recorded. Links to user-related reporting through DimSystemUser. |
| PresenceId | STRING | Presence state for the recorded duration. Foreign key to DimPresence, which supports base and custom presence values. |
| BusinessUnitId | STRING | Service representative's business unit when aggregation was processed. Foreign key to DimBusinessUnit. |

## Metric columns

Use these totals to calculate availability and workforce management metrics.

| Column | Type | Description |
|----------|--------|-------------|
| StatusDurationInSeconds | BIGINT | Total seconds spent in the presence status during the 30-minute interval. A single row has a maximum of 1,800 seconds. |
| StatusChangeCount | INT | Transitions into the presence state during the interval. Each presence-history record that begins in the interval contributes one. |

## Metadata columns

Use these columns for partitioning, refresh tracking, and data lineage.

| Column | Type | Description |
|----------|--------|-------------|
| _AggregationDate | DATE | Reporting interval date, used for partitioning in analytics storage and as a foreign key to the date dimension. |
| _SourceRecordCount | INT | Number of detailed source records contributing to the row. Use it for validation and troubleshooting. |
| _LastRefreshedDateTimeUtc | TIMESTAMP | UTC timestamp of the most recent refresh that populated the row. Use it for operational monitoring and data lineage. |

## Related tables

Use `AggAgentAvailability` with these tables.

| Table | Purpose |
|---------|---------|
| FactAgentStatusHistory | Source table that stores detailed presence history. |
| DimPresence | Provides presence names and status classifications. |
| DimSystemUser | Provides service representative attributes. |
| DimBusinessUnit | Provides organizational hierarchy information. |
| DimTimeZone | Supports time-zone conversion and reporting. |
| AggAgentCapacity | Provides aggregated capacity information that complements presence reporting. |
