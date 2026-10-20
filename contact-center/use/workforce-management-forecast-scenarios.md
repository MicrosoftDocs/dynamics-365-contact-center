---
title: Create and manage forecast scenarios
description: Learn how to use forecast scenario reports to predict case and conversation volumes in Dynamics 365 Contact Center and Customer Service.
ms.date: 10/19/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and manage forecast scenarios

Create a forecast scenario to define what to analyze and how often to generate predictions. Short-term and long-term scenarios both forecast volume and average handle time (AHT) from your historical data. They differ in interval and horizon. This article describes how to create short-term and long-term forecast scenarios and how to manage them after creation.

> [!IMPORTANT]
> Forecasting isn't intended for use in making decisions that affect a person's employment. You're responsible for using this feature in compliance with applicable laws, including those that govern access to employee analytics and the monitoring, recording, and storage of communications with end users. For the complete responsible-use notice, review the [Overview of forecasting](workforce-management-forecast-overview.md).

## Prerequisites

- A security role with the **Read** privilege on the `msdyn_dataanalyticsreport_forecast` table.
- For an external data source, upload the file beforehand through the **Manage External Data** option. Learn more in [Import historical data for forecast scenarios](workforce-management-import-historical-data.md).
- Enough historical data for each queue and channel to support the forecast duration and start date. Learn more in [Understand minimum data requirements and forecast accuracy](#understand-minimum-data-requirements-and-forecast-accuracy).

## Create a forecast scenario

Create a forecast scenario to define what data to analyze, when forecast values start, and how often to generate forecasts. Ensure you have enough historical data for the start date and duration you choose. Learn more in [Understand minimum data requirements and forecast accuracy](#understand-minimum-data-requirements-and-forecast-accuracy).

1. In the site map of Copilot Service workspace, select **Forecasting** under **Workforce Management**. The **Active Forecast Scenarios** page appears.
1. Select **New**, and then select either **Short-term** or **Long-term**. The **New Forecast Scenario** page appears.
1. On the **Details** card, enter the following information:

   - **Name**: Specify a unique name so you can identify the scenario later.
   - **Forecast Start Date**: Select the first date you want to see forecast values for. The date must fall within the supported forecast window for the forecast type. A later start date requires more historical data.
   - **Duration (Days)**: Enter the number of days to forecast, starting from the **Forecast Start Date**.
     - Short-term scenarios support up to 84 days.
     - Long-term scenarios support up to 1,095 days.
   - **Interval**: Values are set automatically to intraday (short-term) or daily (long-term).
   - **Time zone**: Select the time zone for forecast generation and display.

1. On the **Configuration parameters** card, configure the following options:

   - **Forecast entity**: Select **Conversation** or **Case**.
   - **Channels**: Select one or more channels.
   - **Queues**: Select one or more queues.

1. On the **Historical data** card, configure the following options:

   - **Data source**: Select **Internal** or **External**.
   - **Historical data start date**: Select the start date.
   - **Seasonality**: Select a holiday calendar.
   - **External data**: If you selected **External** as the data source, upload the file. You must upload the file beforehand through the **Manage External Data** option. Learn more in [Import historical data for forecast scenarios](workforce-management-import-historical-data.md).

1. On the **Forecast refresh schedule** card, configure the following options:

   - **Auto refresh**: Turn on to run the forecast on a regular schedule.
   - **Day of the week**: Select the day the forecast runs. This option is available for long-term forecasts.
   - **Run time slot**:
     - For short-term forecasts, select the time window used for daily forecast runs.
     - For long-term forecasts, select the scheduled run time.

1. Select **Save**.

> [!NOTE]
> - After you save, the scenario doesn't run immediately. It stays in **Draft** until its first scheduled run.
> - Auto refresh isn't available when you use an external data source.

## Associate a forecast scenario with a planning group

Select a planning group when you create or edit a forecast scenario to use the demand scope defined for that group.

When you select a planning group:

- The **Time zone**, **Channel**, and **Queue** values are populated from the planning group and become read-only. This behavior keeps the forecast scenario aligned with the planning group's configuration.
- The forecast scenario uses the planning group's time zone, channels, and queues when it generates the forecast.

When you don't select a planning group, you can manually configure the **Time zone**, **Channel**, and **Queue** values. The existing scenario-creation workflow remains unchanged.

The forecast scenario list includes a **Planning group** column. Use the column to sort or filter scenarios by planning group.

Capacity plans created from a forecast scenario inherit the scenario's planning group. If you create a capacity plan from an uploaded forecast file, select the planning group manually.

Learn more in [Set up and manage planning groups](workforce-management-use-planning-groups.md).

## Manage an existing scenario

After you create a scenario, return to it to keep the forecast current. You can update its inputs as your business changes, generate a fresh forecast on demand, check the status of past runs, or remove scenarios you no longer need.

To manage a scenario, open it from the **Active Forecast Scenarios** page, and then select an action on the command bar.

### Edit the scenario

Select **Edit** to update editable inputs, such as the **Name**, **Duration (Days)**, **Historical data start date**, **Seasonality**, and refresh schedule. After creation, you can't change the settings that define the scenario: **Forecast type**, **Interval**, **Forecast entity**, and **Data source**.

### Create a new snapshot

Select **Create New Snapshot** to generate a new version of the forecast output that reflects the latest history and any changes you made to the scenario. The newest snapshot becomes the default that capacity planning uses, and you can switch to or revert to an earlier snapshot in the report.

When you create a new snapshot, the following actions occur:

- Forecasting starts a background job to generate the forecast for the scenario.
- Progress appears in the job history.
- When the job finishes, the report updates with the new output version.
- Capacity planning data refreshes automatically from the latest forecast.

> [!NOTE]
> **Create New Snapshot** is unavailable when **Auto refresh** is turned on.

### View output

Select **View Output** to open the report and analyze actual and predicted volume and AHT.

### View job history

Use job history to confirm that a forecast ran successfully and to troubleshoot when results look wrong or are missing. It records every scheduled and on-demand run for the scenario, so you can see what ran, when, and whether it succeeded.

1. Open a forecast scenario.
1. Select **View Job History** to review past runs and their status.

The job history shows the following details for each run:

- **Job status**: Whether the run is in progress, completed, or failed.
- **Job type**: The kind of run, such as a forecast scenario run.
- **Run details**: The timing of the run and related information.

If a queue and channel are flagged with **Insufficient Historical Data**, review their completion status to determine whether a forecast was generated **with reduced confidence** or skipped. Learn about the generation and skip conditions in [When history is insufficient](#when-history-is-insufficient).

### Delete a scenario

Select **Delete** to remove a scenario you no longer need. You can't delete a scenario that a capacity plan uses.

## Understand minimum data requirements and forecast accuracy

Forecasting checks the historical data for each queue and channel before it generates a forecast. If a queue and channel don't have the minimum amount of history, forecasting generates a forecast with reduced confidence or skips that queue and channel.

### How forecast dates affect the data requirement

Forecasting always starts predicting on the day after the **Historical End Date**, the last day with actual data. If you select a later **Forecast Start Date**, forecasting still predicts the days in between but doesn't show them. These hidden days are the **gap**. Because forecasting predicts the gap, the gap counts toward the history you need.

For example, if the historical end date is September 30, 2026, and you select a forecast start date of October 9, the gap is eight days (October 1 through October 8). With a duration of 20 days, you see predictions for October 9 through October 28.

Available history is counted in calendar days, from the **Historical data start date** through the **Historical End Date**, including both dates.

### Minimum historical data

The system calculates the requirement for each queue and channel. All values in the following table are calendar days. Round fractional results up to the next full day.

| Forecast type | Required history, including the gap | Baseline history with no gap |
| --- | --- | --- |
| Short-term | Gap + duration | Duration |
| Long-term | (Gap + duration) / 2, rounded up | Duration / 2, rounded up |

For example, a 365-day long-term forecast with no gap requires 183 days of history, not 182 days.

### When history is insufficient

If a queue and channel have enough history to meet the gap-adjusted requirement, forecasting generates their forecast normally. The grace period described in this section applies only when history falls short of that requirement. It isn't a limit on gaps when sufficient history is available.

If history falls short of the gap-adjusted requirement, the queue and channel are flagged with **Insufficient Historical Data**. Forecasting still generates a forecast **with reduced confidence** only when both of the following conditions are met:

- The gap is within the grace period: no more than half the duration, rounded up to a full day, for short-term forecasts; no more than 90 days for long-term forecasts.
- Available history meets the baseline requirement with no gap: at least the duration for short-term forecasts, or half the duration rounded up for long-term forecasts.

If either condition isn't met, forecasting skips that queue and channel and generates no forecast for them. The reason remains **Insufficient Historical Data**. Review the queue and channel completion status to distinguish a forecast generated **with reduced confidence** from a skipped forecast. For information about reviewing runs, go to [View job history](#view-job-history).

### Short-term examples

For a 20-day short-term forecast, the baseline history requirement is 20 days and the grace period is 10 days.

| Gap (days) | Available history (days) | Required history (days) | Result for the queue and channel |
| --- | --- | --- | --- |
| 0 | 30 | 20 | Forecast generated. |
| 0 | 15 | 20 | Skipped: history is below the 20-day baseline. **Insufficient Historical Data**. |
| 8 | 22 | 28 | Forecast generated with **Insufficient Historical Data** and **reduced confidence**: the gap is within 10 days and history meets the 20-day baseline. |
| 12 | 22 | 32 | Skipped: history is below the requirement and the gap exceeds 10 days. **Insufficient Historical Data**. |
| 12 | 32 | 32 | Forecast generated: history meets the gap-adjusted requirement, so the grace period doesn't apply. |

### Long-term examples

For a 365-day long-term forecast, the baseline history requirement is 183 days and the grace period is 90 days.

| Gap (days) | Available history (days) | Required history (days) | Result for the queue and channel |
| --- | --- | --- | --- |
| 0 | 200 | 183 | Forecast generated. |
| 0 | 150 | 183 | Skipped: history is below the 183-day baseline. **Insufficient Historical Data**. |
| 60 | 205 | 213 | Forecast generated with **Insufficient Historical Data** and **reduced confidence**: the gap is within 90 days and history meets the 183-day baseline. |
| 120 | 205 | 243 | Skipped: history is below the requirement and the gap exceeds 90 days. **Insufficient Historical Data**. |
| 120 | 243 | 243 | Forecast generated: history meets the gap-adjusted requirement, so the grace period doesn't apply. |

### Forecast accuracy

Meeting the minimum requirement lets forecasting run, but it doesn't guarantee an accurate forecast. To get more reliable results:

- Provide as much history as you can. Forecast accuracy improves as more historical data accumulates.
- Keep the gap small. Selecting a forecast start date close to the historical end date reduces the history you need.
- Review forecasts flagged with **Insufficient Historical Data** before you use them for capacity planning. These forecasts are generated **with reduced confidence**.

## Related information

[Overview of forecasting](workforce-management-forecast-overview.md)  
[Forecast with weighted average (preview)](workforce-management-forecast-weighted-average.md)  
[Import historical data for forecast scenarios](workforce-management-import-historical-data.md)
