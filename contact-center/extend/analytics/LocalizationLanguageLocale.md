---
title: LocalizationLanguageLocale table reference
description: Reference information for the LocalizationLanguageLocale table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ms.custom: bap-template
ai-usage: ai-assisted
---

# LocalizationLanguageLocale table reference

Use `LocalizationLanguageLocale` to resolve the language of dimension labels. The table maps Windows LCID codes to locale strings, such as 1033 -> en-US and 1036 -> fr-FR.

## Business value

Power BI and external consumers use this static 45-row lookup to resolve label languages. Windows LCIDs never change.

**Critical for localization:** Without this table, the embedded Dynamics 365 report always displays the default language.

**Reporting usage:** Use the table for Power BI language resolution, the Dynamics 365 SingleReportControl localization filter, and external dimension queries that use `LocalizedLabelLanguageCode`.

## Grain

The table stores one row per language locale (45 rows).

## Source tables

| Source table | Purpose |
|--------------|---------|
| LocalizationLanguageLocaleConfig.csv | Provides the static language-to-locale mappings. |

## Columns

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `LanguageCode` | INT | Static CSV | Primary key. Windows Locale ID, such as 1033=en-US or 1036=fr-FR. |
| `LanguageLocale` | STRING | Static CSV | Locale string (for example, en-US, fr-FR, ja-JP). |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System (`current_timestamp()`) | Pipeline refresh timestamp. |
