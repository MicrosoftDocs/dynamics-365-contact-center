---
title: DimConversationStatus table reference
description: Reference for the DimConversationStatus table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimConversationStatus table reference

Use `DimConversationStatus` to filter conversations by a specific status or a broader lifecycle state. The table maps status codes to readable labels and parent state codes.

## Business value

This shared dimension supports conversation facts and aggregates. In Power BI, one slicer can filter multiple aggregate tables by a detailed status, such as Open, Active, Closed, or Resolved, or by a broad state, such as all statuses in the "Open" state.

**Reporting usage:** `FactConversation.ConversationStatusCode`, `AggConversation`, `AggAgentPerformance`, `AggQueuePerformance`, `AggVoiceConversationInsights`.

## Grain

The table stores one row per status code.

## Source tables

| Source table | Purpose |
|--------------|---------|
| HelperEntityStatus | Provides entity status metadata for this analytics table. |
| EntityName = 'msdyn_ocliveworkitem' | Filters the metadata to `msdyn_ocliveworkitem`. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `ConversationStatusCode` | INT | `HelperEntityStatus` | `StatusCode` | Primary key. Status code (1-7) that matches the foreign key in fact and aggregate tables. |
| `ConversationStatus` | STRING | `HelperEntityStatus` | `StatusCodeLocalizedLabel` | Status label (Open, Active, Waiting, Closed, Wrap-up, Resolved, Scheduled). |
| `ConversationStateCode` | INT | `HelperEntityStatus` | `StateCode` | Parent state code (0-3). Groups related statuses. |
| `ConversationState` | STRING | `HelperEntityStatus` | `StateCodeLocalizedLabel` | State label (Open, Closed, Resolved, Scheduled). |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

### State-to-status hierarchy

Each lifecycle state contains the following statuses.

```
State 0 (Open)
  ├── Status 1 (Open)
  ├── Status 2 (Active)
  ├── Status 3 (Waiting)
  └── Status 5 (Wrap-up)

State 1 (Closed)
  └── Status 4 (Closed)

State 2 (Resolved)
  └── Status 6 (Resolved)

State 3 (Scheduled)
  └── Status 7 (Scheduled)
```

### DAX filter patterns

Filter by `ConversationStatus` for a specific status, such as **Closed**. Filter by `ConversationState` for all statuses in a lifecycle state. For example, the Open state includes Open, Active, Waiting, and Wrap-up.

```dax
-- Filter by specific status
CALCULATE(..., DimConversationStatus[ConversationStatus] = "Closed")

-- Filter by broad state (all statuses in "Open" state = Open, Active, Waiting, Wrap-up)
CALCULATE(..., DimConversationStatus[ConversationState] = "Open")
```

## Related tables

Use `DimConversationStatus` with these tables.

| Table | Purpose |
|-------|---------|
| AggAgentPerformance | Provides representative performance aggregates filtered by conversation status. |
| AggConversation | Provides conversation aggregates filtered by status. |
| AggQueuePerformance | Provides queue performance aggregates filtered by conversation status. |
| AggVoiceConversationInsights | Provides voice insight aggregates filtered by conversation status. |
| FactConversation | Provides detailed conversation data. |
| HelperEntityStatus | Provides status and state metadata. |
