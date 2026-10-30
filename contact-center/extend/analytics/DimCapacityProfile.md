---
title: DimCapacityProfile table reference
description: Reference for the DimCapacityProfile table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimCapacityProfile table reference

Use `DimCapacityProfile` to filter capacity analytics by profile, such as a chat or voice profile. The table maps profile GUIDs to display names and includes default capacity and assignment settings.

## Business value

Profiles have display names such as "Chat Profile" and "Voice Profile". Use the default maximum capacity units and block-assignment flag to interpret each profile's settings.

**Reporting usage:** `FactAgentCapacityHistory.CapacityProfileId`, `AggAgentCapacity.CapacityProfileId`.

## Grain

The table stores one row per capacity profile.

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_capacityprofile | Provides capacity profile names and settings. |

## Columns

| Column | Type | Source entity | Source field | Description |
|--------|------|---------------|--------------|-------------|
| `CapacityProfileId` | STRING | `msdyn_capacityprofile` | `msdyn_capacityprofileid` | Primary key. Capacity profile GUID. |
| `CapacityProfileName` | STRING | `msdyn_capacityprofile` | `msdyn_name` | Display name. |
| `DefaultMaxUnits` | INT | `msdyn_capacityprofile` | `msdyn_defaultmaxunits` | Default maximum capacity units for the profile. Agent-level overrides are stored in `msdyn_agentcapacityprofileunit`. |
| `IsBlockAssignment` | BOOLEAN | `msdyn_capacityprofile` | `msdyn_blockassignment` | Whether this profile blocks assignment when capacity is exhausted. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimCapacityProfile` with these capacity tables.

| Table | Purpose |
|-------|---------|
| AggAgentCapacity | Provides aggregate capacity data by profile. |
| FactAgentCapacityHistory | Provides capacity history by profile. |
