---
title: DimSessionClosureReason table reference
description: Reference for the DimSessionClosureReason table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimSessionClosureReason table reference

Use `DimSessionClosureReason` to understand why sessions ended. The table maps closure reason codes in the 192350000 series to readable labels.

## Business value

Reasons include agent rejection, agent transfer, bot escalation, customer disconnection, and timeout.

**Reporting usage:** `FactSession.ClosureReason`.

## Grain

The table stores one row per closure reason code.

## Source tables

| Source table | Purpose |
|--------------|---------|
| HelperOptionSet | Provides closure reason codes and labels. |
| msdyn_ocsession.msdyn_closurereason | Identifies the closure reason option set used by this dimension. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `ClosureReasonCode` | INT | `HelperOptionSet` | `Option` (cast int) | Primary key. Closure reason code, such as 192350000=Default, 192350001=AgentReject, or 192350026=BotTransferToAgent. |
| `ClosureReason` | STRING | `HelperOptionSet` | `LocalizedLabel` | Human-readable label (for example, "Agent Reject", "Bot Transfer To Agent", "Customer Disconnect"). |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimSessionClosureReason` with these tables.

| Table | Purpose |
|-------|---------|
| FactSession | Provides session closure reasons. |
| HelperOptionSet | Provides the reason codes and labels. |
