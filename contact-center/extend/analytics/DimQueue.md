---
title: DimQueue table reference
description: Reference for the DimQueue table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimQueue table reference

Use `DimQueue` to filter analytics by queue and interpret queue-specific service thresholds. The table maps queue GUIDs to display names and types.

## Business value

The table includes each queue's SLA and short-abandon thresholds, which ETL uses to precompute `InServiceLevel` and `IsShortAbandoned`. It also identifies queues configured for omnichannel routing.

**Reporting usage:** All fact and aggregated tables via `QueueId` Foreign Key.

## Grain

The table stores one row per queue.

## Source tables

| Source table | Purpose |
|--------------|---------|
| queue | Provides queue source data for this analytics table. |

## Columns

| Column | Type | Source entity | Source field | Description |
|--------|------|---------------|--------------|-------------|
| `QueueId` | STRING | `queue` | `queueid` | Primary key. Queue GUID. |
| `QueueName` | STRING | `queue` | `name` | Queue display name. |
| `QueueType` | INT | `queue` | `msdyn_queuetype` | Queue type, for example messaging or voice. |
| `IsOmniChannelQueue` | BOOLEAN | `queue` | `msdyn_isomnichannelqueue` | Indicates whether the queue is configured for omnichannel routing. Filter this column to `true` for omnichannel-only reports. |
| `ServiceLevelThreshold` | INT | `queue` | `msdyn_queueservicelevelthreshold` | SLA threshold in seconds. ETL uses it to calculate `IsInServiceLevel`. |
| `ShortAbandonedThreshold` | INT | `queue` | `msdyn_shortabandonedthreshold` | Short-abandon threshold in seconds. ETL uses it to calculate `IsShortAbandoned`. |
| `BusinessUnitId` | STRING | `queue` | `owningbusinessunit` | Foreign key to DimBusinessUnit. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimQueue` with this dimension.

| Table | Purpose |
|-------|---------|
| DimBusinessUnit | Provides the queue's business unit information. |
