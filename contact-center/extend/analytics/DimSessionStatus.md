---
title: DimSessionStatus table reference
description: Reference for the DimSessionStatus table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimSessionStatus table reference

Use `DimSessionStatus` to filter reports by session status and display labels instead of status codes.

## Business value

Like `DimConversationStatus`, this table maps codes to readable labels, but it applies to the session entity (`msdyn_ocsession`).

**Reporting usage:** `FactSession.SessionStatus`.

## Grain

The table stores one row per session status code.

## Source tables

| Source table | Purpose |
|--------------|---------|
| HelperOptionSet | Provides session status codes and labels. |
| msdyn_ocsession.StatusMetadata | Provides status metadata for the session entity. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `SessionStatusCode` | INT | `HelperOptionSet` | `Option` (cast int) | Primary key. Session status code. |
| `SessionStatus` | STRING | `HelperOptionSet` | `LocalizedLabel` | Human-readable label. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimSessionStatus` with these tables.

| Table | Purpose |
|-------|---------|
| DimConversationStatus | Provides the corresponding status dimension for conversations. |
| FactSession | Provides session status values. |
| HelperOptionSet | Provides the status codes and labels. |
