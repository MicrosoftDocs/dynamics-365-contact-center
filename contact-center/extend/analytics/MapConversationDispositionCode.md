---
title: MapConversationDispositionCode table reference
description: Reference information for the MapConversationDispositionCode table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# MapConversationDispositionCode table reference

Use `MapConversationDispositionCode` to connect conversations to their disposition codes through a many-to-many bridge.

## Business value

One conversation can have multiple disposition codes, and one code can apply to multiple conversations. The bridge is available only in the detail model: `GROUP BY` removes `ConversationId`, so aggregate tables don't use it.

**Reporting usage:** In Power BI, use the bridge between FactConversation/FactSession and DimDispositionCode.

## Grain

The table stores one row for each disposition code assigned to a conversation.

## Source tables

| Source table | Purpose |
|--------------|---------|
| msdyn_conversationdispositioncodemap | Provides conversation-to-disposition-code assignments. |

## Columns

| Column | Type | Source Entity | Source Field | Description |
|--------|------|---------------|--------------|-------------|
| `ConversationDispositionCodeMapId` | STRING | `msdyn_conversationdispositioncodemap` | `msdyn_conversationdispositioncodemapid` | Primary key. Mapping record GUID. |
| `ConversationId` | STRING | `msdyn_conversationdispositioncodemap` | `msdyn_ocliveworkitemid` | Foreign Key to FactConversation. |
| `DispositionCodeId` | STRING | `msdyn_conversationdispositioncodemap` | `msdyn_ocdispositioncodeid` | Foreign Key to DimDispositionCode. |
| `DispositionCodeValue` | STRING | `msdyn_conversationdispositioncodemap` | `msdyn_dispositioncodevalue` | Denormalized label included for convenience. Get the authoritative label through the foreign key join to DimDispositionCode. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `MapConversationDispositionCode` with these tables.

| Table | Purpose |
|-------|---------|
| DimDispositionCode | Provides disposition code labels. |
| FactConversation | Provides the mapped conversations. |
| FactSession | Provides session details for reporting through the bridge. |
