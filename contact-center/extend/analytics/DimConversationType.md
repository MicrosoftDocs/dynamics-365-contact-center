---
title: DimConversationType table reference
description: Reference for the DimConversationType table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimConversationType table reference

Use `DimConversationType` to filter and group conversations by how they started. The table maps conversation type codes to labels.

## Business value

Distinguish direct inbound, DID inbound, callback, agent-initiated outbound, and proactive outbound conversations in your reports.

**Reporting usage:** `FactConversation.ConversationType`.

## Grain

The table stores one row per conversation type code.

## Source tables

| Source table | Purpose |
|--------------|---------|
| HelperOptionSet | Provides conversation type codes and labels. |
| msdyn_ocliveworkitem.msdyn_conversationtype | Identifies the conversation type option set used by this dimension. |

## Columns

| Column | Type | Source | Source field | Description |
|--------|------|--------|--------------|-------------|
| `ConversationTypeCode` | INT | `HelperOptionSet` | `Option` (cast int) | Primary key. Conversation type code: 0=Inbound, 1=Inbound_DID, 2=Inbound_Callback, 3=Outbound_AgentInitiated, 4=Outbound_PESInitiated. |
| `ConversationType` | STRING | `HelperOptionSet` | `LocalizedLabel` | Human-readable label. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimConversationType` with these tables.

| Table | Purpose |
|-------|---------|
| FactConversation | Provides conversation data filtered by type. |
| HelperOptionSet | Provides the conversation type codes and labels. |
