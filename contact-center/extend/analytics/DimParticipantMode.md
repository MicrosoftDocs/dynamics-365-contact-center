---
title: DimParticipantMode table reference
description: Reference for the DimParticipantMode table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimParticipantMode table reference

Use `DimParticipantMode` to distinguish agents' roles in a session when you filter or group reports.

## Business value

The table maps participant mode codes to labels for three roles: primary handler, consult advisor, and silent monitor.

**Reporting usage:** `FactSessionParticipant.ParticipantModeCode`, `AggAgentPerformance.ParticipantModeCode`.

## Grain

The table stores one row per participant mode, for exactly three rows.

## Source tables

| Source table | Purpose |
|--------------|---------|
| HelperOptionSet | Provides participant mode codes and labels. |
| msdyn_sessionparticipant.msdyn_mode | Identifies the participant mode option set used by this dimension. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `ParticipantModeCode` | INT | `HelperOptionSet` | `Option` (cast int) | Primary key. 192350002=Primary, 192350003=Consult, 192350004=Monitor. |
| `ParticipantModeName` | STRING | `HelperOptionSet` | `LocalizedLabel` | Human-readable label (Primary, Consult, Monitor). |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimParticipantMode` with these tables.

| Table | Purpose |
|-------|---------|
| AggAgentPerformance | Provides performance aggregates by participant mode. |
| FactSessionParticipant | Provides individual participants' session roles. |
| HelperOptionSet | Provides the mode codes and labels. |
