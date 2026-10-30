---
title: DimTimeZone table reference
description: Reference for the DimTimeZone table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimTimeZone table reference

Use `DimTimeZone` to report UTC activity in local time. The table maps UTC 15-minute slots to local date and time attributes for each supported time zone offset.

## Business value

The Power BI time zone slicer uses this mapping. For example, selecting "GMT+05:30" resolves the local date, hour, and day for each UTC slot.

**Reporting usage:** All fact and aggregated tables via `DateTimeKey` → `UtcDateTimeKey`.

## Grain

The table stores one row per UTC 15-minute slot and time zone offset.

## Source tables

| Source table | Purpose |
|--------------|---------|
| DimDate | Provides the UTC 15-minute slots expanded by time zone offset. |

## Columns

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `UtcDateTimeKey` | BIGINT | From DimDate | Primary Key. UTC 15-minute slot key. Foreign Key target for `DateTimeKey` on all fact/agg tables. |
| `TimeZoneCode` | STRING | 34 fixed offsets | GMT offset string (for example, `GMT+05:30`, `GMT-07:00`). UTC is the bare string `GMT` (no offset). Matches the value emitted by the D365 reporting control's `Utils.getTimeZoneCodeByOffsetMinutes`. |
| `LocalDateTimeKey` | BIGINT | Computed | Local 15-minute slot key after applying the offset. Foreign key to `DimDate.DateTimeKey`. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | Pipeline refresh timestamp. |

> **Regeneration:** DimTimeZone depends on DimDate. Both regenerate automatically in the same STATIC phase when DimDate regenerates.

> **34 offsets:** Covers all standard offsets from GMT-12:00 to GMT+13:00, including half-hour (GMT+05:30 India, GMT+03:30 Iran) and quarter-hour (GMT+05:45 Nepal) offsets. UTC is encoded as the bare string `GMT` (not `GMT+00:00`) to match the D365 reporting control's filter output.

## Related tables

Use `DimTimeZone` with this dimension.

| Table | Purpose |
|-------|---------|
| DimDate | Provides the date and time attributes for local reporting. |
