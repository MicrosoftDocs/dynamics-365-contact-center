---
title: DimSystemUser table reference
description: Reference for the DimSystemUser table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimSystemUser table reference

Use `DimSystemUser` to identify agents and users in reports, filter by business unit, and distinguish bots from human agents. The table maps GUIDs to display names and classification details.

## Business value

The table includes agent types and user types, such as Omnichannel agent and Supervisor, alongside each customer service representative's or user's identity.

**Reporting usage:** `FactConversation.ActiveAgentId`, `FactSession.PrimaryAgentId`, `FactSessionParticipant.AgentId`, `AgentPerformanceAnalytics.AgentId`, `AgentAvailabilityAnalytics.AgentId`.

## Grain

The table stores one row per system user.

## Source tables

| Source table | Purpose |
|--------------|---------|
| systemuser | Provides user identity, business unit, and classification data. |
| HelperOptionSet | Resolves agent type and user type labels for this analytics table. |

## Columns

| Column | Type | Source entity | Source field | Description |
|--------|------|---------------|--------------|-------------|
| `SystemUserId` | STRING | `systemuser` | `systemuserid` | Primary key. User GUID. |
| `FullName` | STRING | `systemuser` | `fullname` | Display name. |
| `BusinessUnitId` | STRING | `systemuser` | `businessunitid` | Foreign key to DimBusinessUnit. |
| `BotApplicationId` | STRING | `systemuser` | `msdyn_botapplicationid` | Bot application ID. Null for human agents. |
| `AgentTypeCode` | INT | `systemuser` | `msdyn_agentType` | Agent type option set code. |
| `AgentType` | STRING | `HelperOptionSet` | Resolved from `systemuser.msdyn_agentType` | Agent type label (for example, "Application User", "Bot"). |
| `SystemUserTypeCode` | INT | `systemuser` | `msdyn_usertype` | User type option set code. |
| `SystemUserType` | STRING | `HelperOptionSet` | Resolved from `systemuser.msdyn_usertype` | User type label (for example, "Omnichannel agent", "Supervisor"). |
| `IsBot` | BOOLEAN | Calculated | `msdyn_botapplicationid IS NOT NULL` | TRUE for a bot; FALSE for a human agent. Derived from BotApplicationId to simplify queries. |
| `EmailAddress` | STRING | `systemuser` | `EmailAddress` | Primary email address used for agent cards, tooltips, and identity display. |
| `IsDisabled` | BOOLEAN | `systemuser` | `isdisabled` | Whether the user account is disabled. |
| `DomainName` | STRING | `systemuser` | `domainname` | Domain login name. |
| `ManagerId` | STRING | `systemuser` | `ManagerId` | Identifies the user's manager. Join it to `DimSystemUser.SystemUserId` for manager and team rollups. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | `current_timestamp()` | Pipeline refresh timestamp. |

## Related tables

Use `DimSystemUser` with these tables.

| Table | Purpose |
|-------|---------|
| DimBusinessUnit | Provides users' business unit information. |
| FactConversation | Identifies the active agent in a conversation. |
| FactSession | Identifies the primary agent in a session. |
| FactSessionParticipant | Identifies each session participant's agent. |
| HelperOptionSet | Provides agent type and user type labels. |
