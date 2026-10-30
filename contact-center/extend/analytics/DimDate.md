---
title: DimDate table reference
description: Reference for the DimDate table in the Shared Analytics Platform data model for Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# DimDate table reference

Use `DimDate` to filter and group analytics by year, quarter, month, week, day, hour, or 15-minute slot. This generated date and time dimension has 96 slots per day.

## Business value

Every fact and aggregated table joins here for time-based reporting—year, quarter, month, week, day, hour, and 15-minute slot. Its 15-minute grain supports both 15-minute conversation and session aggregates and 30-minute availability and capacity aggregates.

**Reporting usage:** All fact and aggregated tables via `CreatedOnDateKey` → `DimTimeZone.UtcDateTimeKey` → `DimDate.DateTimeKey`. Aggregated tables also join via `_AggregationDate` → `DimDate.Date`.

## Grain

The table stores one row per 15-minute slot (96 slots per day).

## Source tables

| Source table | Purpose |
|--------------|---------|
| Self-generated via Spark SQL—no Dataverse entity | Generates this analytics table in Spark SQL. |

## Columns

| Column | Type | Source | Description |
|--------|------|--------|-------------|
| `DateTimeKey` | BIGINT | Computed (`YYYYMMDDHHmm`) | Primary key. 15-minute surrogate key referenced by `DimTimeZone.LocalDateTimeKey`. |
| `Date` | DATE | Computed | Calendar date (for example, `2026-03-10`). |
| `DateTime` | TIMESTAMP | Computed | Full timestamp (for example, `2026-03-10 14:15:00`). |
| `Year` | INT | Computed | 4-digit calendar year. |
| `HalfYearNumber` | INT | Computed | `1` (Jan–Jun) or `2` (Jul–Dec). |
| `HalfYearName` | STRING | Computed | `H1` or `H2`. |
| `QuarterNumber` | INT | Computed | `1`–`4`. |
| `QuarterName` | STRING | Computed | `Q1`, `Q2`, `Q3`, `Q4`. |
| `MonthNumber` | INT | Computed | `1`–`12`. |
| `MonthShortName` | STRING | Computed | Month abbreviation, such as Jan, Feb, or Mar. |
| `MonthStartDate` | DATE | Computed | First day of the month. Used for month-level aggregations. |
| `MonthYearLabel` | STRING | Computed | `MonthShortName + ' ' + Year` (for example, `Mar 2026`). Label for displays and slicers. |
| `MonthYearSort` | STRING | Computed | `YYYYMM` (for example, `202603`). Sorts chronologically as a string. |
| `WeekOfYear` | INT | Computed | ISO week number. |
| `DayOfWeekName` | STRING | Computed | Day abbreviation, such as Mon, Tue, or Wed. |
| `HourOfDay` | INT | Computed | `0`–`23`. |
| `HourLabel` | STRING | Computed | Display format `HH:00` (for example, `14:00`). |
| `MinuteOfSlot` | INT | Computed | `0`, `15`, `30`, or `45`. The minute component of the 15-minute slot. |
| `_LastRefreshedDateTimeUtc` | TIMESTAMP | System | Pipeline refresh timestamp. |

> **Coverage:** The table covers the retention start date through 12 months beyond the end of the current year. It's regenerated when the remaining coverage approaches six months.

## Related tables

Use `DimDate` with this table.

| Table | Purpose |
|-------|---------|
| DimTimeZone | Maps UTC reporting times to local date and time keys. |
