---
title: Create and manage forecast scenarios
description: Learn how to use forecast scenario reports to predict case and conversation volumes in Dynamics 365 Contact Center and Customer Service.
ms.date: 04/09/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and manage forecast scenarios

Learn how to access and interpret forecast reports in Copilot Service workspace to ensure accurate staffing decisions.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. This feature isn't intended for use in making, and you shouldn't use it to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365 Copilot Service workspace, this feature, and any associated feature or service in compliance with all applicable laws. This compliance includes laws that relate to accessing individual employee analytics, and monitoring, recording, and storing communications with end users. This compliance also includes your responsibility to adequately notify end users that their communications with customer service representatives might be monitored, recorded, or stored and as required by applicable laws, obtaining consent from end users before your organization uses this feature with them. Customers are also encouraged to have a mechanism in place to inform their customer service representatives that their communication with end users might be monitored, recorded, or stored.

## Overview

Forecast scenarios are essential to predict future demand in terms of volume, such as the number of customer interactions, cases, or conversations that are expected within your contact center.

You can use the forecast reports for case and conversation volumes in the following ways:

- Forecast upcoming case and conversation volumes using historical traffic data, whether sourced internally from Dynamics 365 or externally from an imported file upload.
- Rely on predicted conversation volumes for service representative planning if your administrator configured AI agents for your conversation channels. The system excludes conversations that AI agents handle without having a service representative join the conversation.
- Forecast case and conversation volumes on a daily basis for a time range up to six months for long-term business planning.
- Forecast case and conversation volumes at 15-minute intervals for a time range of up to six weeks for short-term staffing and intraday planning.
- Slice forecasted volumes and service representative demand by channel and queue.
- View a rollup of actual and forecasted volume on an hourly, daily, weekly, monthly, and yearly basis.
- Automatically detect seasonality from historical traffic with the settings option to import your holiday calendar. This function helps the forecasting model to predict case or conversation volumes during special, seasonal events.
- Trigger forecasts on demand with the **Run forecast scenario** option.

> [!NOTE]
> - Forecast reports provide accurate volume estimates but might not fully account for external factors, such as unexpected trends or sudden business needs.
>
> - Forecast reports are currently available in specific geographical locations. Learn more in [Supported regions and languages for analytics and insights](/dynamics365/customer-service/administer/cs-region-availability-service-limits#supported-regions-and-languages-for-analytics-and-insights).

## Prerequisites

- Your administrator assigned a role to you that has **Read** privileges on the **msdyn_dataanalyticsreport_forecast** table. 

## Forecast scenario types

You can create either short-term or long-term forecasts.

- **Short term**: This report is typically used for daily forecasts. It shows intraday actual and predicted case and conversation volumes in 15-minute intervals for up to six weeks. The available forecast range depends on how much historical case or conversation data exists.

- **Long term**: This report shows the actual and predicted daily case and conversation volumes for up to six months. The available forecast range depends on how much historical case or conversation data exists.

## Create a short-term or long-term forecast report

1. In the site map of Copilot Service workspace, select **Forecasting** under **Workforce Management**. The **Active Forecast Scenarios** dashboard appears.
1. Select **New**, and then select either **Short-term** or **Long-term** from the dropdown menu. The **New Forecast Scenario** page appears.
1. On the **Details** card, fill in the **Name** and **Duration (Days)** fields.
1. On the **Configuration parameters** card, select the following:
      1. **Forecast entity**: Select either **Conversation** or **Case**.
      1. **Channels**: Search for and select the channel you want. You can select multiple channels.
      1. **Queues**: Use the search option to find the queue you want or select **New Record** > **Queues** to create one. You can select multiple queues.
1. On the **Forecast run schedule** card, fill in the following details:
      1. **Auto-extension**: Set the toggle to **Yes** if you want to run the forecast. If you set the toggle to **No**, the forecast schedule remains in draft state and doesn't get created.
         >[!NOTE]  
         > You can have up to 10 forecast scenarios with Auto-extension enabled. 
      1. **Day of the week**: Select the weekday on which the report should be generated. Use for long-term forecasts only. 
      1. **Run time slot**: For short-term, use the dropdown menu to select the time window you want the system to use when it runs the report. The forecast scenario for short term runs every day. For long-term, select the day.
      1. **Run time zone**: Use the dropdown menu to select the time zone you want the system to use when it runs the report.
1. On the **Historical data** card, fill in the following details:
      1. **Data source**: Select **Internal**: Select **Internal** or **External**.
      1. **Historical data start date**: Select the date from which you want to track the data. By default, this date is set to two years before the current date when you create the report.
      1. **Seasonality**: Use the dropdown menu to select a holiday calendar if applicable.
      1. **External data**: If you're using external data as your data source, select the search field, browse to your file, and then select it. Learn how to import an external data file in [Import data for forecast scenarios](wfm-import-historical-data.md).
1. Select **Save**.

> [!NOTE]  
> - The forecast scenario runs within two hours of initial setup. Subsequent runs follow the schedule set on the **Forecast Run Schedule** card.
> - Forecasts generated with internal data from the managed workforce system remain available even when data is limited. However, forecast accuracy improves as the volume of data increases. 

## View your forecast reports

1. In the site map of Copilot Service workspace, select **Forecast scenarios** under **Workforce Management**. The **Active Forecast Scenarios** dashboard appears.
1. Select the **Reports** tab. A list of the reports you created appears.

The first time you access the dashboard, scenarios you configured appear in **Draft** status until the first run occurs. After that, the scenario shows as **In progress** until it completes. For each scenario, the following details are displayed:

- **Name**: The name of you gave the scenario.
- **Current Status**: The state of the scenario. This status can be **Draft**, **Completed**.
- **Interval**: The type of scenario.
- **Duration**: The length of time.
- **Target entity**: The record type.
- **Last Run On**: The date the scenario last ran. This date is based on the **Forecast run schedule** you selected.
- **Is recurring**: Indicates whether the scenario repeats.
- **Recurrence time slot**: The day or time the report runs.
- **Recurrence time zone**: The time zone in which the report runs.

### Data visualization

When you open a report, the following visualizations are available:

**Duration**: Allows you to enter the date range or use the sliders to set the dates.

**Channel**: Select one or more channels for which you want data displayed.

**Queue**: Select one or more queues for which you want data displayed.

**Trend chart**: Shows the actual historical volumes from the past to the predicted volume in the future. The forecast is based on actual case and conversation records created in the past.

**Detled view**: You can filter the data in the following ways:
   - **All**: Displays the actual and forecasted numbers across all channels and queues. 
   - **Channel**: Displays the actual and forecasted numbers, sliced by each channel. 
   - **Queue**: Displays the actual and forecasted numbers, sliced by each queue.
     
     For all the filters, you can use the drill up and down buttons to drill to specific levels in the hierarchy.

### Run forecasts on demand

As a supervisor, you can manually trigger a forecast run for a scenario by selecting **Run forecast scenario**. This capability supports planning and operational analysis scenarios where you need refreshed forecast results without waiting for the next scheduled run.

When you run a forecast scenario on demand, the following actions occur:

- The system starts a background job to generate the forecast for the current scenario.
- Forecast generation runs asynchronously and can take varying amounts of time depending on data volume and scenario configuration.
- Supervisors can monitor progress and status in the job history.
- After the background job completes, updated forecast outputs are avlable in forecast reports and views.
- Completion of the forecast run also triggers a capacity planning job to refresh staffing requirements based on the latest forecast output.

