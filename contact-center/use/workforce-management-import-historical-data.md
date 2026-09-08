---
title: Manage external data
description: Learn how to upload and manage external data for workforce management forecasts and capacity plans.
ms.date: 09/08/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---
# Manage external data

Workforce management can use data that you generate outside Dynamics 365. Use **Manage external data** when your historical workload volumes or your forecast come from another system, such as a legacy contact center platform, a third-party workforce management application, an enterprise data warehouse, or a finance planning model.

You upload external data as a CSV file in **Manage external data**. The file type that you select determines which workforce management capability consumes the file, which columns the file must contain, and how the system validates the file.

The process works as follows:

* You prepare a CSV file that matches the template for the file type that you need.
* You create a file upload record, select the file type and data interval, and attach the file.
* The system validates the file against the template for the selected file type and sets a validation status.
* After the file passes validation, you select it as an input when you create a forecast scenario or a capacity plan.

Each file type supports both a **Daily** (long-term) and an **Intraday** (short-term) data interval. Select the interval that matches the plan that consumes the file. A long-term forecast scenario or capacity plan can’t consume an intraday file, and a short-term plan can’t consume a daily file.

## Prerequisites

Before you upload an external data file, make sure that you meet the following requirements:

* Your administrator installed the Workforce Management package in the environment.
* You have the **WFM Forecaster** or **WFM Administrator** security role.
* Your file is saved in CSV format, with the exact column headers described for the file type that you’re uploading.
* Your file contains only one data interval. Don’t combine daily rows and 15-minute interval rows in the same file.
* For historical data, your file covers a continuous date range. You can include up to two years of workload history, counted back from the date when you create the forecast scenario.

## File types

The **File Type** field determines how workforce management interprets the file. Select one of the following values.

| File type | Consumed by | Use it when |
| --- | --- | --- |
| **External historical data for forecast scenario** | Forecast scenario | You want the forecasting model to learn from historical workload volumes that aren’t in Dynamics 365. |
| **External forecast data for capacity planning** | Capacity plan | You already have a volume forecast from another system and want to skip forecast generation. |
| **Capacity plan parameter override** | Capacity plan | You want service-level assumptions to vary by interval, channel, or queue instead of applying one set of values to the whole plan. |

### External historical data for forecast scenario

Upload historical workload volumes and handle time so that workforce management can generate a forecast from them. This file type replaces the default behavior of forecasting from workload history in Dynamics 365.

Use this file type when your historical workload volumes live outside Dynamics 365, when you’re migrating from another contact center platform and want forecasts to reflect history from that platform, or when you want to model a hypothetical demand pattern such as a planned campaign or a seasonal event.

The forecast scenario uses the volume and handle time in the file as its training input, and produces predicted volume for the forecast horizon. The forecast output remains a Dynamics 365 forecast scenario that you can review, adjust, and link to a capacity plan.

### External forecast data for capacity planning

Upload a volume and handle time forecast that another system produced, and use it directly as the demand input for a capacity plan.

Use this file type when your organization forecasts centrally in a planning tool and treats that output as the plan of record, when finance or operations sets volume targets that staffing must be planned against, or when you want to compare the staffing implications of an external forecast with the staffing that a Dynamics 365 forecast scenario produces.

Workforce management doesn’t generate a forecast from this file. It reads the forecast values in the file, applies your capacity plan parameters, and calculates the required number of representatives per interval.

### Capacity plan parameter override

Upload interval-level values for the configuration parameters that a capacity plan normally applies uniformly across the plan.

A capacity plan applies one target answer time, service level, shrinkage, concurrency, and occupancy assumption to every interval. Some support operations rarely work that way. Shrinkage is higher during training weeks, target answer time is tighter for a premium queue, concurrency differs between voice and chat, and overnight intervals tolerate a lower service level than the morning peak.

Use this file type to supply the values that should apply to a specific combination of interval, channel, and queue. The capacity plan uses the value from the file for any row that the file covers, and falls back to the parameter values that are configured on the plan for every interval, channel, and queue combination that the file doesn’t cover.

You can also override forecast handle time in this file. Overriding handle time changes the workload that the staffing calculation is based on, without changing the volume forecast.

## Upload an external data file

1. In the site map of Copilot Service workspace, under **Workforce Management**, select **Manage External Data**. The **Active File uploads** page appears.
2. Select **New**. The **New WEM File Upload** page appears.
3. In **Name**, enter a descriptive name for the file. Include the file type, the interval, and the period that the data covers, so that you can easily identify the record later. For example: Voice history intraday Jan-Feb 2025.
4. For **File data interval**, select **Intraday** (short term) or **Daily** (long term).
5. For **File Type**, select one of the following values:
   * **External forecast data for capacity planning**
   * **Capacity plan parameter override**
   * **External historical data for forecast scenario**
6. Select **Save**. The **File** field becomes editable after the record is created.

   > [!NOTE]
   > The **File** field is locked until the record exists. Until you save, the field shows the message that the record isn't created yet.

7. For **File**, select **Choose File**, and then select your CSV file.
8. Select **Save**. Validation runs automatically, and **Validation Status** is set.
9. Check **Validation Status**. If the file failed validation, correct the file and upload it again. For more information, go to [Validate an uploaded file](#validate-an-uploaded-file).

After the file passes validation, select it as the data source when you create a forecast scenario or a capacity plan. The file appears in the data source list only for plans that match its file type and data interval.

### Use external data in a forecast scenario

When you create or edit a forecast scenario, set the historical data source to **External**, and then select the validated file in **Forecast external data file**.

### Use external data in a capacity plan

When you create or edit a capacity plan, select the external file source, and then select the validated file in **External forecast file**. To override capacity plan parameters, select a validated parameter override file separately in **Capacity plan parameter override**.

## File templates

The following sections describe the required column headers, formats, and sample values for each file type.

The following rules apply to all file types:

* The file must be in CSV format (end with .csv extension), use commas as separators, and be saved as UTF-8.
* The first row must contain all required column headers exactly as shown, including capitalization. Don’t rename or omit required columns. You can include extra columns.
* For daily data, use the **DateTime** format `yyyy-MM-dd`, such as `2026-09-03`.
* For intraday data, use the **DateTime** format `yyyy-MM-dd HH:mm`, such as `2026-09-03 14:30`.
* For an intraday file, **DateTime** values must fall on 15-minute boundaries: 00:00, 00:15, 00:30, and 00:45.
* For a daily file, use one row per date, per channel, per queue.
* All numeric values must be whole numbers. Don’t include thousands separators, currency symbols, or percentage signs.
* Express percentage values as whole numbers. For example, enter 85, not 0.85 or 85%.
* Every combination of **DateTime**, **ChannelId**, and **QueueId** must be unique within the file.
* For files with multiple channels or queues, assign each channel and queue a distinct, consistent ID. Include a row for every relevant channel, queue, and time-period combination.

### External historical data for forecast scenario

#### Columns

| Column | Format | Description |
| --- | --- | --- |
| **DateTime** | yyyy-MM-dd for daily data; yyyy-MM-dd HH:mm for intraday data | The date and time of the data point. For an intraday file, use 15-minute intervals. For a daily file, use one row per date. |
| **ChannelId** | Whole number | A distinct identifier for the channel in the source system, such as voice, chat, or a custom channel. Use the same ID for that channel in every upload. |
| **ChannelName** | Text | The channel name that corresponds to the channel identifier in the source system. |
| **QueueId** | Whole number or Text | A distinct identifier for the queue in the source system. Use the same ID for that queue in every upload. |
| **QueueName** | Text | The queue name that corresponds to the queue identifier in the source system. |
| **Volume** | Whole number | The workload volume, or number of cases or conversations, for the interval, for the combination of channel and queue. |
| **AHT** | Whole number | The average handling time for one case or conversation in the interval, in seconds. |

> [!IMPORTANT]
> The system ignores the legacy **Interval**, **MaxVolumeByHour**, and **AgentCount** columns. Other extra columns are also allowed. Validation fails if a required column is missing or if a data row contains a different number of values than the header row.

#### Intraday sample

| DateTime | ChannelId | ChannelName | QueueId | QueueName | Volume | AHT |
| --- | --- | --- | --- | --- | --- | --- |
| 2025-01-01 00:00 | 1 | CHName1 | 1 | Q1 | 89 | 107 |
| 2025-01-01 00:00 | 1 | CHName1 | 2 | Q2 | 89 | 109 |
| 2025-01-01 00:00 | 2 | CHName2 | 1 | Q1 | 89 | 103 |
| 2025-01-01 00:15 | 1 | CHName1 | 1 | Q1 | 89 | 110 |
| 2025-01-01 00:15 | 1 | CHName1 | 2 | Q2 | 89 | 103 |

#### Daily sample

| DateTime | ChannelId | ChannelName | QueueId | QueueName | Volume | AHT |
| --- | --- | --- | --- | --- | --- | --- |
| 2025-01-01 | 2 | CHName2 | 2 | Q2 | 89 | 106 |
| 2025-01-01 | 1 | CHName1 | 2 | Q2 | 89 | 105 |
| 2025-01-02 | 2 | CHName2 | 1 | Q1 | 88 | 102 |
| 2025-01-02 | 1 | CHName1 | 1 | Q1 | 88 | 104 |

### External forecast data for capacity planning

#### Columns

| Column | Format | Description |
| --- | --- | --- |
| **DateTime** | yyyy-MM-dd for daily data; yyyy-MM-dd HH:mm for intraday data | The date and time of the forecast data point. For an intraday file, use 15-minute intervals. For a daily file, use one row per date. |
| **ChannelId** | Whole number | A distinct identifier for the channel in the source system. Use the same ID for that channel in every upload. |
| **ChannelName** | Text | The channel name that corresponds to the channel identifier in the source system. |
| **QueueId** | Whole number or Text | A distinct identifier for the queue in the source system. Use the same ID for that queue in every upload. |
| **QueueName** | Text | The queue name that corresponds to the queue identifier in the source system. |
| **Forecast** | Whole number | The forecast number of cases or conversations for the interval, for the combination of channel and queue. |
| **ForecastAHT** | Whole number | The forecast average handling time for one case or conversation in the interval, in seconds. |

#### Intraday sample

| DateTime | ChannelId | ChannelName | QueueId | QueueName | Forecast | ForecastAHT |
| --- | --- | --- | --- | --- | --- | --- |
| 2026-03-20 00:00 | 2 | CHName2 | 2 | Q2 | 100 | 200 |
| 2026-03-20 00:15 | 2 | CHName2 | 2 | Q2 | 105 | 203 |
| 2026-03-20 00:30 | 2 | CHName2 | 2 | Q2 | 110 | 206 |
| 2026-03-20 00:45 | 2 | CHName2 | 2 | Q2 | 115 | 209 |

#### Daily sample

| DateTime | ChannelId | ChannelName | QueueId | QueueName | Forecast | ForecastAHT |
| --- | --- | --- | --- | --- | --- | --- |
| 2026-03-20 | 2 | CHName2 | 2 | Q2 | 100 | 200 |
| 2026-03-21 | 1 | CHName1 | 2 | Q2 | 105 | 203 |
| 2026-03-22 | 2 | CHName2 | 1 | Q1 | 110 | 206 |
| 2026-03-23 | 1 | CHName1 | 1 | Q1 | 115 | 209 |

### Capacity plan parameter override

#### Columns

| Column | Format | Description |
| --- | --- | --- |
| **DateTime** | yyyy-MM-dd for daily data; yyyy-MM-dd HH:mm for intraday data | The date and time of the interval that the override values apply to. For an intraday file, use 15-minute intervals. For a daily file, use one row per date. |
| **ChannelId** | Whole number | The channel identifier that the override applies to. |
| **QueueId** | Whole number or Text | The queue identifier that the override applies to. |
| **TargetAnswerTime** | Whole number | The target answer time, in seconds. Used with **ServiceLevel**. For example, a target answer time of 25 with a service level of 80 means that 80 percent of conversations must be answered within 25 seconds. |
| **ServiceLevel** | Whole number (percentage) | The percentage of conversations that must be answered within the target answer time. |
| **Shrinkage** | Whole number (percentage) | The percentage of paid time that representatives aren’t available to handle conversations, such as breaks, training, and meetings. Higher values increase the number of representatives that are required. |
| **Concurrency** | Whole number | The number of conversations that one representative handles at the same time. Use 1 for voice. Set a higher value for chat and messaging channels. |
| **Occupancy** | Whole number (percentage) | The maximum percentage of available time that representatives should spend handling work. Acts as a ceiling that prevents the staffing calculation from planning for sustained full utilization. |
| **ForecastAHT** | Whole number | The average handling time, in seconds, to use for the interval instead of the forecast handle time. |

> [!NOTE]
> The parameter override file doesn’t include the **ChannelName** and **QueueName** columns. Rows are matched on **ChannelId** and **QueueId** only.

#### Intraday sample

| DateTime | ChannelId | QueueId | TargetAnswerTime | ServiceLevel | Shrinkage | Concurrency | Occupancy | ForecastAHT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2026-03-20 00:00 | 2 | 2 | 25 | 25 | 25 | 1 | 85 | 100 |
| 2026-03-20 00:15 | 2 | 2 | 25 | 25 | 25 | 1 | 90 | 500 |

#### Daily sample

| DateTime | ChannelId | QueueId | TargetAnswerTime | ServiceLevel | Shrinkage | Concurrency | Occupancy | ForecastAHT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2026-03-20 | 2 | 2 | 86 | 25 | 25 | 1 | 85 | 500 |

#### Partial coverage

The override file doesn’t need to cover every interval in the capacity plan. Include only the rows that need different values. For any interval, channel, and queue combination that the file doesn’t include, the capacity plan uses the parameter values that are configured on the plan.

For example, if shrinkage is 25 percent for most of the plan but 40 percent during a training week, include rows only for the training week, and set shrinkage on the plan to 25.

## Validate an uploaded file

Every file is validated when you save the record. Validation confirms that the file structure matches the template for the selected file type, and that the data in the file is usable by the capability that consumes it. The result appears in the read-only **Validation Status** field on the file upload record. The status can be **Not Validated**, **In Progress**, **Successful**, or **Error**. If validation fails, open the external data record and review **Error Details** for the affected row numbers and validation messages.

Validation checks the following conditions:

* **File format.** The file is a readable CSV file and isn't empty.
* **Columns.** All required columns for the selected file type are present and named exactly as specified. Extra columns are allowed.
* **Row structure.** Each data row contains the same number of values as the header row.
* **Data types.** Numeric columns contain whole numbers, and text columns contain values.
* **Date and time format.** **DateTime** values parse correctly and use the expected format.
* **Interval alignment.** For an intraday file, **DateTime** values fall on 15-minute boundaries. For a daily file, dates aren't repeated for the same channel and queue.
* **Duplicates.** No two rows share the same combination of **DateTime**, **ChannelId**, and **QueueId**.
* **Value ranges.** Percentage columns are between 0 and 100, volume and handle time values aren't negative, and concurrency is at least 1.

Consider the following validation behavior:

* Validation runs against the file type that you selected. The same file can pass for one file type and fail for another, because each type expects a different set of columns.
* A file that fails validation is saved as a record but isn't available as a data source for a forecast scenario or capacity plan.
* To fix a failed file, correct the source CSV file and upload it again. You can attach a corrected file to the existing record and save it to run validation again.

### Common validation issues

| Issue | Resolution |
| --- | --- |
| A required column is missing, misspelled, or has different capitalization. | Compare the header row with the template for the selected file type and correct the required column. |
| A data row contains a different number of values than the header row. | Add or remove values so that every row has the same number of values as the header row. |
| **DateTime** values don’t parse. | Use `yyyy-MM-dd` for daily data or `yyyy-MM-dd HH:mm` for intraday data. Check that a spreadsheet application didn’t reformat the column when the file was saved as CSV. |
| Intraday timestamps don’t align to 15-minute intervals. | Round timestamps to 00, 15, 30, or 45 minutes, and aggregate volume and recalculate handle time for the combined intervals. |
| Duplicate rows exist for the same date, channel, and queue. | Aggregate the duplicate rows into a single row for each combination. |
| Numeric columns contain decimals, percentage signs, or thousands separators. | Round values to whole numbers and remove formatting characters. |
| The selected data interval doesn’t match the file contents. | Set **File data interval** to **Intraday** for 15-minute data, or **Daily** for daily data. |

## Best practices

* Name uploads consistently so that you can identify the file type, interval, and period from the record name.
* Validate a small sample file before you upload a full history file. A structural problem is faster to diagnose in a file with a few rows.
* Keep channel and queue identifiers stable across uploads. If identifiers change between files, forecast scenarios treat the data as unrelated queues.
* To save a CSV file, select **Save as** > **UTF-8 (Comma delimited)**.
* For parameter overrides, include only the rows that differ from the plan-level configuration. Smaller override files are easier to review and audit.

## Related information

* [Create and manage forecast scenarios](workforce-management-forecast-scenarios.md)
* [Create and manage capacity plans](workforce-management-capacity-planning.md)
* [Overview of workforce management](/dynamics365/customer-service/use/workforce-management-overview)
* [Create and manage shift plans](workforce-management-shift-plan.md)
