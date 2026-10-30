---
title: DimBusinessUnit table reference
description: Reference for the DimBusinessUnit table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimBusinessUnit table reference

Use `DimBusinessUnit` to filter analytics by business unit and organizational hierarchy. The table maps business unit GUIDs to names and parent units.

## Business value

Supervisors can filter by business unit to view only their team's data.

**Reporting usage:** All fact and aggregated tables via `BusinessUnitId` foreign key.

## Grain

The table stores one row per business unit.

## Source tables

| Source table | Purpose |
|--------------|---------|
| businessunit | Provides business unit names and parent-unit relationships. |

## Columns

| Column | Type | Source entity | Source field | Description |
|--------|------|---------------|--------------|-------------|
| `BusinessUnitId` | STRING | `businessunit` | `businessunitid` | Primary key. Business unit GUID. |
| `BusinessUnitName` | STRING | `businessunit` | `name` (trimmed) | Display name. |
| `ParentBusinessUnitId` | STRING | `businessunit` | `parentbusinessunitid` | Parent business unit GUID. Null for the root unit. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |
