---
title: DimPresence table reference
description: Reference for the DimPresence table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimPresence table reference

Use `DimPresence` to filter availability reports by agent presence. The table maps presence GUIDs to base status codes, names, and display text.

## Business value

Filter availability dashboards by statuses such as Available, Busy, Away, and Offline. Custom presences, such as "Training Break" and "Lunch", map to one of five base statuses.

**Reporting usage:** `FactAgentStatusHistory.PresenceId`, `AggAgentAvailability.PresenceId`.

## Grain

The table stores one row per presence configuration.

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_presence | Provides presence configurations and display text. |

## Columns

| Column | Type | Source entity | Source field | Description |
|--------|------|---------------|--------------|-------------|
| `PresenceId` | STRING | `msdyn_presence` | `msdyn_presenceid` | Primary key. Presence configuration GUID. |
| `BasePresenceStatusCode` | INT | `msdyn_presence` | `msdyn_basepresencestatus` | Base status option set code. Five fixed values: 192360000=Available, 192360001=Busy, 192360002=Busy-DND, 192360003=Away, 192360004=Offline. Used for base-level rollups in DAX. |
| `BasePresenceStatus` | STRING | `HelperOptionSet` | `LocalizedLabel` via `HelperOptionSet` → `msdyn_presence.msdyn_basepresencestatus` | Human-readable base status (Available, Busy, Busy-DND, Away, Offline). |
| `PresenceName` | STRING | `msdyn_presence` | `msdyn_name` | Presence name, which might be custom, such as "Training Break" or "Lunch". For built-in presences, it matches BasePresenceStatus. |
| `PresenceStatusText` | STRING | `msdyn_presence` | `msdyn_presencestatustext` | Text shown to agents in the UI. Each custom presence maps to exactly one base status. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimPresence` with these tables.

| Table | Purpose |
|-------|---------|
| AggAgentAvailability | Provides availability aggregates by presence. |
| FactAgentStatusHistory | Provides agent presence history. |
| HelperOptionSet | Provides base status labels. |
