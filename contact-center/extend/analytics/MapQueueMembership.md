---
title: MapQueueMembership table reference
description: Reference information for the MapQueueMembership table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# MapQueueMembership table reference

Use `MapQueueMembership` to filter agent reports by queue membership. This many-to-many bridge connects agents and queues.

## Business value

The incremental snapshot retains historical memberships after agents leave queues. In Power BI, use it for queue-based agent filtering, such as "show metrics for agents in Queue X".

**Reporting usage:** In Power BI, use the bridge between DimQueue and DimSystemUser.

## Grain

The table stores one row for each agent and queue membership.

## Source tables and filters

| Source table or filter | Purpose |
|------------------------|---------|
| queuemembership | Provides agent-to-queue memberships. |
| msdyn_isomnichannelqueue = true | Includes only omnichannel queues. |

## Columns

| Column | Type | Source Entity | Source Field | Description |
|--------|------|---------------|--------------|-------------|
| `QueueId` | STRING | `queuemembership` | `queueid` | Foreign Key to DimQueue. |
| `AgentId` | STRING | `queuemembership` | `systemuserid` | Foreign Key to DimSystemUser. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

> **Incremental snapshot:** Each ETL run combines current `queuemembership` records with the previous snapshot by using UNION, then deduplicates by (`QueueId`, `AgentId`). Removing an agent from a queue doesn't remove their historical membership from the data.

## Related tables

Use `MapQueueMembership` with these dimensions.

| Table | Purpose |
|-------|---------|
| DimQueue | Provides queue attributes. |
| DimSystemUser | Provides agent attributes. |
