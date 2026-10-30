---
title: DimOverflowAction table reference
description: Reference for the DimOverflowAction table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimOverflowAction table reference

Use `DimOverflowAction` to display and filter the actions taken when an overflow condition occurs.

## Business value

The table maps action codes to readable labels. Actions include callback, external transfer, voicemail, and transfer to queue.

**Reporting usage:** `FactConversation.LastOverflowAction`, `FactSession.OverflowAction`, `ConversationAnalytics.OverflowAction`.

## Grain

The table stores one row per overflow action code.

## Source tables

| Source table | Purpose |
|--------------|---------|
| HelperOptionSet | Provides overflow action codes and labels. |
| msdyn_sessionextension.msdyn_overflowaction | Identifies the overflow action option set used by this dimension. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `OverflowActionCode` | INT | `HelperOptionSet` | `Option` (cast int) | Primary key. Action code, such as 419550001=Callback, 419550002=ExternalTransfer, or 419550003=Voicemail. |
| `OverflowAction` | STRING | `HelperOptionSet` | `LocalizedLabel` | Human-readable action label. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimOverflowAction` with these tables.

| Table | Purpose |
|-------|---------|
| FactConversation | Provides the conversation's last overflow action. |
| FactSession | Provides session overflow actions. |
| HelperOptionSet | Provides the action codes and labels. |
