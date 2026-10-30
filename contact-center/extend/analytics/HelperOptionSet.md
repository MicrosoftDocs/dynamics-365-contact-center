---
title: HelperOptionSet table reference
description: Reference information for the HelperOptionSet table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# HelperOptionSet table reference

Use `HelperOptionSet` to resolve Dataverse **option set** integer codes to readable labels. This central lookup supplies option set-based dimensions in the Shared Analytics Platform data model.

## Business value

ETL generates this table from two CDS2 metadata tables; it isn't a Dataverse entity. It resolves all Dataverse option set integer codes and supplies dimensions such as DimChannel, DimConversationType, and DimOverflowAction from a single source.

The table filters labels to your organization's primary language. **It doesn't include state or status metadata.** For those parent-child relationships, use `HelperEntityStatus`.

## Grain

Each row maps one combination of entity, option set name, and code to a localized label.

## Source tables

| Source table | What it contains |
|-------------|------------------|
| `OptionsetMetadata` | Entity-level option set definitions, such as `msdyn_channel`, `msdyn_closurereason`, and `msdyn_mode`. |
| `GlobalOptionsetMetadata` | Global option set definitions shared across entities. |

## Output columns

| Column | Type | Description |
|--------|------|-------------|
| `EntityName` | STRING | Dataverse entity name (for example, `msdyn_ocliveworkitem`, `msdyn_ocsession`) |
| `OptionSetName` | STRING | Optionset attribute name (for example, `msdyn_channel`, `msdyn_closurereason`) |
| `Option` | INT | Optionset code value |
| `LocalizedLabel` | STRING | Human-readable label in the org's primary language |
| `IsDefaultLanguage` | BOOLEAN | TRUE for the org's primary language row |
| `LocalizedLabelLanguageCode` | INT | Language code (for example, 1033=en-US) |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | Pipeline refresh timestamp |

## ETL flow

```
CDS2 Metadata Tables (auto-synced by Dataverse)
├── OptionsetMetadata
└── GlobalOptionsetMetadata
        │
        ▼  UNION ALL
        │
        ▼  Resolve org primary language (org locale → en-US fallback)
        │
        ▼  Filter: IsDefaultLanguage = True
        │
   HelperOptionSet (Delta table + in-memory cache)
        │
        ├──► DimChannel
        ├──► DimConversationType
        ├──► DimConversationDirection (hardcoded, does not use HelperOptionSet)
        ├──► DimSessionClosureReason
        ├──► DimParticipantMode
        ├──► DimOverflowAction
        ├──► DimOverflowCondition
        └──► DimPresence (BasePresenceStatus column only)

Separate table: HelperEntityStatus
  (StateMetadata + StatusMetadata → DimConversationStatus, session/segment status labels)
```

## Pipeline stage

`HelperOptionSetGenerator` runs first in the **STATIC** stage, before any dimension generator. It caches the result in `context.shared_lookup_cache` and `context.outputs` for downstream generators, avoiding another read.

## Related tables

Use `HelperOptionSet` alongside these tables. DimConversationDirection uses hardcoded values, and DimConversationStatus uses separate state/status metadata.

| Table | Purpose |
|-------|---------|
| DimChannel | Provides channel labels. |
| DimConversationDirection | Provides hardcoded direction labels without using this lookup. |
| DimConversationStatus | Provides conversation status labels from state/status metadata. |
| DimConversationType | Provides conversation type labels. |
| DimOverflowAction | Provides overflow action labels. |
| DimOverflowCondition | Provides overflow condition labels. |
| DimParticipantMode | Provides participant role labels. |
| DimPresence | Uses this lookup for BasePresenceStatus only. |
| DimSessionClosureReason | Provides session closure reason labels. |
| HelperEntityStatus | Provides hierarchical state/status metadata separately from flat option sets. |
