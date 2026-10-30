---
title: DimDispositionCode table reference
description: Reference for the DimDispositionCode table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimDispositionCode table reference

Use `DimDispositionCode` to display and analyze the outcome tags agents apply after a conversation. The table maps disposition code IDs to readable labels.

## Business value

Disposition labels include "Billing Issue", "Technical Support", and "Resolved". One conversation can have multiple disposition codes. This dimension is available only in the detail model; aggregate tables don't use it.

**Reporting usage:** Detail tables via `MapConversationDispositionCode` bridge.

## Grain

The table stores one row per disposition code definition.

| Column | Type | Source entity | Source field | Description |
|--------|------|---------------|--------------|-------------|
| `DispositionCodeId` | STRING | `msdyn_ocdispositioncode` | `msdyn_ocdispositioncodeid` | Primary key. Disposition code GUID. |
| `DispositionCodeName` | STRING | `msdyn_ocdispositioncode` | `msdyn_name` | Display name. |
| `DispositionCodeValue` | STRING | `msdyn_ocdispositioncode` | `msdyn_dispositioncodevalue` | Code value (localizable). |
| `DispositionCodeCategoryId` | STRING | `msdyn_ocdispositioncode` | `msdyn_dispositioncodecategoryid` | Foreign key to the disposition code category used for grouping. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimDispositionCode` with this mapping table.

| Table | Purpose |
|-------|---------|
| MapConversationDispositionCode | Links conversations to their disposition codes. |
