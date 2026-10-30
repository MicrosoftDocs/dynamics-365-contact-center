---
title: DimChannel table reference
description: Reference for the DimChannel table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimChannel table reference

Use `DimChannel` to filter reports by channel and display names instead of option set codes.

## Business value

Reports can show "Voice," "Live chat," and "Email" instead of codes such as 192440000. The table excludes the Entity Records channel (192350000) because it isn't customer-facing.

**Reporting usage:** `FactConversation.ChannelCode`, `FactSession.ChannelCode`, all aggregated tables.

## Grain

The table stores one row per channel code.

## Source tables

| Source table | Purpose |
|--------------|---------|
| HelperOptionSet | Provides channel option set codes and labels. |
| msdyn_liveworkstream.msdyn_streamsource | Identifies the channel option set used by this dimension. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `ChannelCode` | INT | `HelperOptionSet` | `Option` (cast int) | Primary key. Channel code, such as 192360000=LiveChat or 192440000=Voice. |
| `Channel` | STRING | `HelperOptionSet` | `LocalizedLabel` | Human-readable name (for example, Live chat, Voice, Email). |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimChannel` with these tables.

| Table | Purpose |
|-------|---------|
| FactConversation | Provides conversation data filtered by channel. |
| FactSession | Provides session data filtered by channel. |
| HelperOptionSet | Provides the channel codes and labels. |
