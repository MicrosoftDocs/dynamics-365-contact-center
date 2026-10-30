---
title: DimOverflowCondition table reference
description: Reference for the DimOverflowCondition table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimOverflowCondition table reference

Use `DimOverflowCondition` to display and filter the conditions that trigger overflow.

## Business value

The table maps condition codes to readable labels, such as **Out of operating hours**, **Queue at capacity**, and **Wait time exceeded**.

**Reporting usage:** `FactConversation.LastOverflowCondition`, `FactSession.OverflowCondition`, `ConversationAnalytics.OverflowCondition`.

## Grain

The table stores one row per overflow condition code.

## Source tables

| Source table | Purpose |
|--------------|---------|
| HelperOptionSet | Provides overflow condition codes and labels. |
| msdyn_sessionextension.msdyn_overflowcondition | Identifies the overflow condition option set used by this dimension. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `OverflowConditionCode` | INT | `HelperOptionSet` | `Option` (cast int) | Primary key. Condition code, such as 419550000=OutOfOperatingHours. |
| `OverflowCondition` | STRING | `HelperOptionSet` | `LocalizedLabel` | Human-readable condition label. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimOverflowCondition` with these tables.

| Table | Purpose |
|-------|---------|
| FactConversation | Provides the conversation's last overflow condition. |
| FactSession | Provides session overflow conditions. |
| HelperOptionSet | Provides the condition codes and labels. |
