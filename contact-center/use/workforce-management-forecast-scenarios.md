---
title: Create and manage forecast scenarios
description: Learn how to use forecast scenario reports to predict case and conversation volumes in Dynamics 365 Contact Center and Customer Service.
ms.date: 08/17/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and manage forecast scenarios

[!INCLUDEcc-feature-availability-embedded-yes]

Create a forecast scenario to define what to analyze and how often to generate predictions. Short-term and long-term scenarios both forecast volume and average handle time (AHT) from your historical data. They differ in interval and horizon. This article describes how to create short-term and long-term forecast scenarios and how to manage them after creation.

> [!IMPORTANT]
> Forecasting isn't intended for use in making decisions that affect a person's employment. You're responsible for using this feature in compliance with applicable laws, including those that govern access to employee analytics and the monitoring, recording, and storage of communications with end users. For the complete responsible-use notice, review the [Overview of forecasting](workforce-management-forecast-overview.md).

## Prerequisites

- A security role with the **Read** privilege on the `msdyn_dataanalyticsreport_forecast` table.
- For an external data source, upload the file beforehand through the **Manage External Data** option. Learn more in [Import historical data for forecast scenarios](workforce-management-import-historical-data.md).

## Create a forecast scenario

Create a forecast scenario to define what data to analyze and how often to generate forecasts.

1. In the site map of Copilot Service workspace, select **Forecasting** under **Workforce Management**. The **Active Forecast Scenarios** page appears.
1. Select **New**, and then select either **Short-term** or **Long-term**. The **New Forecast Scenario** page appears.
1. On the **Details** card, enter the following information:

   - **Name**: Specify a unique name so you can identify the scenario later.
   - **Duration (Days)**: Enter the number of days the forecast covers.
     - Short-term scenarios support up to 42 days.
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
> - Forecast accuracy improves as more historical data accumulates.

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

### Delete a scenario

Select **Delete** to remove a scenario you no longer need. You can't delete a scenario that a capacity plan uses.

## Related information

- [Overview of forecasting](workforce-management-forecast-overview.md)
- [Forecast with weighted average (preview)](workforce-management-forecast-weighted-average.md)
- [Import historical data for forecast scenarios](workforce-management-import-historical-data.md)
