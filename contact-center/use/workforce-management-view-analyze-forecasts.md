---
title: View and analyze forecast results
description: Learn how to analyze, filter, export, and manage forecast results in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 08/19/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# View and analyze forecast results

After a forecast scenario runs, open its report to compare actual demand with forecasted demand by time, channel, and queue. The report is available for all forecast scenario types.

## Open a forecast report

1. In the site map of Copilot Service workspace, select **Forecasting** under **Workforce Management**.
1. On the **Active Forecast Scenarios** page, open a scenario, and then select **View Output**.
1. Use the report header to change the report context:
   - Review the scenario name and applied filters.
   - Use the **Snapshot** selector to select a forecast version.

## Filter the report and select a view

Use the report filters and view settings to control the data that appears.

| Setting | Description |
|---|---|
| **Duration** | Set the date range by using the date pickers. |
| **Channel(s)** and **Queue(s)** | Limit the report to specific channels and queues. |
| **Show AHT** | Turn on this setting to display average handle time (AHT) with volume. |
| **View** | Select **Intraday** to display forecasts by individual time interval. To analyze trends at different levels of aggregation, select a time hierarchy, such as **Year > Month > Week > Day** or **Year > Month > Day**. |

## Read the volume chart

The volume chart displays historical actual volume and predicted future volume.

- Select **Aggregate** to display a combined line.
- Select **Per-dimension** to split the chart by channel and queue.
- Use **Smart zoom** to focus on a specific time range. Select **Reset zoom** to return to the full range.
- Point to a data point to display the value for that interval.

## Read the volume data table

The **Volume data** table displays forecast results for each period based on the selected forecast interval. The data is organized by channel and queue so that you can compare actual and forecasted workloads across dimensions.

For each channel and queue combination, the table includes the following values:

- **Actual Volume** — Historical interaction volume recorded for the period.
- **Forecast Volume** — Predicted interaction volume for the period.
- **Actual AHT** — Historical average handle time, when **Show AHT** is turned on.
- **Forecast AHT** — Predicted average handle time, when **Show AHT** is turned on.

To focus on specific channels, queues, or time periods, filter the data from a column header.

> [!NOTE]
> Actual values are populated when the forecast snapshot is refreshed and the corresponding forecast period moves into the past. Future periods display forecast values until actual data becomes available.

## Download the forecast

Select **Export to Excel** to download the forecast data currently displayed in the table.

The exported file includes the results for the selected date range, channels, queues, and view settings. Use the file for further analysis, to share data with stakeholders, or to create custom reports outside Workforce Management.

## Work with snapshots

Each forecast output refresh creates a snapshot version.

- Use the **Snapshot** selector to switch between versions.
- To rename a snapshot, select **Edit** (pencil icon), enter the new name in the **Edit snapshot** dialog, and then save your changes.
- The most recent snapshot is selected by default and is the version that capacity planning uses. If needed, revert to an earlier version.

## Related information

- [Overview of forecasting](workforce-management-forecast-overview.md)  
- [Create and manage forecast scenarios](workforce-management-forecast-scenarios.md)  
- [Estimate AI agent credits from forecasts](workforce-management-credit-estimation.md)
