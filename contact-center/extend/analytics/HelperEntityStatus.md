---
title: HelperEntityStatus table reference
description: Reference information for the HelperEntityStatus table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# HelperEntityStatus table reference

Use `HelperEntityStatus` to look up Dataverse entity status labels and their parent states. This flattened table maps **statuscode** values to labels and includes each parent **statecode** value and label.

## Business value

The table supports these uses:

- Build state and status lookups separately from `HelperOptionSet`: state and status are **hierarchical**, with state as parent and status as child, whereas option sets are flat.
- Reuse status metadata across any entity with statecode/statuscode, including conversations, sessions, segments, and cases.
- One row per entity × status code—no self-join is needed to build dimension tables

## Grain

The table stores one row per entity × status code × language.

## Source tables

| Source table | What it contributes |
|-------------|---------------------|
| `StatusMetadata` | StatusCode, parent StateCode, StatusCode localized label |
| `StateMetadata` | StateCode localized label (joined via StatusMetadata.State = StateMetadata.State) |

## ETL logic

```sql
SELECT
    status.EntityName,
    CAST(status.Status AS INT)              AS StatusCode,
    status.LocalizedLabel                   AS StatusCodeLocalizedLabel,
    CAST(status.State AS INT)               AS StateCode,
    state.LocalizedLabel                    AS StateCodeLocalizedLabel,
    status.IsDefaultLanguage,
    status.LocalizedLabelLanguageCode,
    current_timestamp()                     AS _LastRefreshedDateTimeUtc
FROM StatusMetadata status
LEFT JOIN StateMetadata state
    ON state.EntityName = status.EntityName
    AND state.State = status.State
    AND state.LocalizedLabelLanguageCode = status.LocalizedLabelLanguageCode
```

## Output columns

| Column | Type | Description |
|--------|------|-------------|
| `EntityName` | STRING | Dataverse entity name (for example, `msdyn_ocliveworkitem`, `msdyn_ocsession`) |
| `StatusCode` | INT | The statuscode value |
| `StatusCodeLocalizedLabel` | STRING | Status label in the org's primary language (for example, "Open", "Active", "Closed") |
| `StateCode` | INT | The parent statecode value |
| `StateCodeLocalizedLabel` | STRING | State label in the org's primary language (for example, "Open", "Closed", "Resolved") |
| `IsDefaultLanguage` | BOOLEAN | TRUE for the org's primary language row |
| `LocalizedLabelLanguageCode` | INT | Language code (for example, 1033=en-US) |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | Pipeline refresh timestamp |

## Example data (`msdyn_ocliveworkitem`)

```
| EntityName             | StatusCode | StatusCodeLocalizedLabel | StateCode | StateCodeLocalizedLabel |
|------------------------|-----------|-------------------------|----------|------------------------|
| msdyn_ocliveworkitem   | 1         | Open                    | 0        | Open                   |
| msdyn_ocliveworkitem   | 2         | Active                  | 0        | Open                   |
| msdyn_ocliveworkitem   | 3         | Waiting                 | 0        | Open                   |
| msdyn_ocliveworkitem   | 4         | Closed                  | 1        | Closed                 |
| msdyn_ocliveworkitem   | 5         | Wrap-up                 | 0        | Open                   |
| msdyn_ocliveworkitem   | 6         | Resolved                | 2        | Resolved               |
| msdyn_ocliveworkitem   | 7         | Scheduled               | 3        | Scheduled              |
```

## Building a status dimension (for example, `DimConversationStatus`)

Read the table directly to build a status dimension. No joins are required.

```sql
SELECT
    StatusCode              AS ConversationStatusCode,
    StatusCodeLocalizedLabel AS ConversationStatus,
    StateCode               AS ConversationStateCode,
    StateCodeLocalizedLabel AS ConversationState
FROM HelperEntityStatus
WHERE EntityName = 'msdyn_ocliveworkitem'
    AND IsDefaultLanguage = 1
```

## Localization support (post-April)

The table stores all available languages in `LocalizedLabelLanguageCode`. To build localized dimensions, filter by language rather than `IsDefaultLanguage = 1`.

```sql
WHERE EntityName = 'msdyn_ocliveworkitem'
    AND LocalizedLabelLanguageCode = @selectedLocaleId
```

## Pipeline stage

The pipeline generates this table and `HelperOptionSet` in the **STATIC** stage, before generating dimension tables.

## Related tables

Use `HelperEntityStatus` with these tables.

| Table | Purpose |
|-------|---------|
| DimConversationStatus | Provides the conversation status dimension built from this metadata. |
| HelperOptionSet | Provides flat option set lookups separately from hierarchical state and status metadata. |
