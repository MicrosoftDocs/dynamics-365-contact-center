---
title: DimConversationDirection table reference
description: Reference for the DimConversationDirection table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimConversationDirection table reference

Use `DimConversationDirection` to filter and label inbound and outbound conversations.

## Business value

The table maps direction codes to the Inbound and Outbound labels so reports don't need to display numeric codes.

**Reporting usage:** `FactConversation.ConversationDirectionCode`, all aggregated tables.

## Grain

The table stores one row per direction.

## Source tables

| Source table | Purpose |
|--------------|---------|
| [(0, "Inbound"), (1, "Outbound")] | Provides the fixed direction mapping for this analytics table. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `ConversationDirectionCode` | INT | Hardcoded | 0 or 1 | Primary key. 0=Inbound, 1=Outbound. Matches the direction foreign key in fact and aggregate tables. |
| `ConversationDirection` | STRING | Hardcoded | "Inbound" / "Outbound" | Human-readable label. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimConversationDirection` with this table.

| Table | Purpose |
|-------|---------|
| FactConversation | Provides conversation data filtered by direction. |
