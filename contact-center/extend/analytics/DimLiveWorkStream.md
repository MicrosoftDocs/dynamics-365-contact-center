---
title: DimLiveWorkStream table reference
description: Reference for the DimLiveWorkStream table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimLiveWorkStream table reference

Use `DimLiveWorkStream` to analyze conversation and session details by workstream. The table maps workstream GUIDs to display names and channel codes.

## Business value

A workstream defines a channel's routing rules, capacity profile, and operating hours. A channel can have multiple workstreams, such as three chat workstreams for different product lines. This dimension is used only in detail tables, not aggregates.

**Reporting usage:** Detail tables only—`FactConversation.LiveWorkStreamId`, `FactSession` (via conversation join). Not used in aggregated tables.

## Grain

The table stores one row per workstream.

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_liveworkstream | Provides workstream names and channel codes. |

## Columns

| Column | Type | Source entity | Source field | Description |
|--------|------|---------------|--------------|-------------|
| `LiveWorkStreamId` | STRING | `msdyn_liveworkstream` | `msdyn_liveworkstreamid` | Primary key. Workstream GUID. |
| `LiveWorkStreamName` | STRING | `msdyn_liveworkstream` | `msdyn_name` | Display name (for example, "Product Support Chat", "Sales Voice"). |
| `ChannelCode` | INT | `msdyn_liveworkstream` | `msdyn_streamsource` | Channel this workstream handles. Foreign key to DimChannel. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimLiveWorkStream` with these tables.

| Table | Purpose |
|-------|---------|
| DimChannel | Provides channel labels. |
| FactConversation | Provides conversation details by workstream. |
| FactSession | Provides session details through a conversation join. |
