---
title: Create and manaage forecast scenarios
description: Learn how to use forecast scenario reports to predict service representative, case, and conversation volumes.
ms.date: 04/11/2025
ms.topic: conceptual
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and manage forecast scenarios


This article describes how to navigate the forecast reports in Copilot Service workspace so that you can successfully meet the staffing demands of your organization.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. This feature is not intended for use in making, and should not be used to make, decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365 Copilot Service workspace, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This also includes adequately notifying end users that their communications with customer service representatives may be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their customer service representatives that their communications with end users may be monitored, recorded, or stored.

## Overview

Customer service supervisors need to ensure that they have an adequate number of customer service representatives (service representatives or representatives) available to serve their customers. Overcapacity results in higher costs, while under capacity results in longer customer wait times, which negatively affects customer satisfaction.

As a supervisor, you can use the forecast scenario reports to help plan the right level of staffing for your business which is based on the predicted volume of cases and conversations, along with the predicted service representative demand for conversations.

You can use the forecast reports for service representative, case, and conversation volumes in the following ways:

- Forecast upcoming case and conversation volumes based on historical traffic and the number of service representatives needed to meet the forecasted conversation volume. For conversation volume forecasting, if your administrator has configured AI agents for your conversational channels, the system excludes conversations that AI agents handle without having a service representative join the conversation. This function ensures that you can rely on the predicted conversation volumes for service representative staffing.

- Visualize forecasted volumes and service representative demand on a daily basis, for a time range up to six months, depending on how many days of cases or conversations were created in the past. This forecast can be used to plan service representative resourcing and recruitment, to meet future demand.

- Visualize forecast volumes and service representative demand for a time range up to six weeks, depending on how many days of cases or conversations were created in the past. This forecast can be used to schedule service representatives to meet the near-term demand.

- Slice forecasted volumes and service representative demand by channel and queue.

- View a rollup of actual and forecasted volume on an hourly, daily, weekly, monthly, and yearly basis.

- Automatically detect seasonality from historical traffic with the settings option to import your holiday calendar. This function helps the forecasting model to accurately predict case or conversation volumes during special, seasonal events.

> [!NOTE]
> Be aware of the following when using forecasting scenario reports:
>
> - Forecast reports might misstate volume estimates for many reasons, including unanticipated trends or business developments.
>
> - Forecast reports are currently available in certain geographical locations. Learn more in [Supported regions and languages for analytics and insights](/customer-service/administer/cs-region-availability-service-limits.md#supported-regions-and-languages-for-analytics-and-insights).

## Prerequisites

Before you can use the forecast reports, ensure that your administrator assigned a role to you that has **Read** privileges on the **msdyn_dataanalyticsreport_forecast** table. 

## Forecast scenario types

You can create either short-term or long-term forecasts.

- **Short term**: This report is typically used for daily forecasts. It displays an intraday view of the actual and predicted case and conversation volumes and service representative demand in intervals of 15 minutes, for a time range of up to six weeks, depending on how many days of cases or conversations were created in the past. This forecast can be used to schedule service representatives day-to-day to meet the near-term demand.

- **Long term**: This mode displays the actual and predicted case and conversation volumes and service representative demand per day, for a time range of up to six months, depending on how many days of cases or conversations were created in the past. This forecast can be used to plan service representative resourcing and recruitment to meet a future demand.

## Create a short-term or long-term forecast report

1. On the Copilot Service workspace site map, select **Forecasting** under **Workforce Management**. The **Active Forecast Scenarios** dashboard appears.
1. Select **New**, and the select either **Short-term** or **Long-term** from the dropdown menu. The **New Forecast Scenario** page appears.
1. On the **Details** card, fill in the **Name** and **Duration (Days)** fields.
1. On the **Configuration parameters** card, select the following:
      1. **Forecast entity**: Select either **Conversation** or **Case**.
      2. **Channels**: Search for and select the channel you want. You can choose multiple channels.
      1. **Queues**: Use the search option to find the queue you want, or select **New Record** > **Queues** to create one. You can choose multiple queues.
1. On the **Forecast run schedule** card, fill in the following details:
      1. **Auto-extension**: Set the toggle to **Yes** if you want to run the forecast. If you set the toggle to **No**, the forecast schedule remains in draft state and doesn't get created.
      2. **Day of the week**: For long-term forecasts only. Select the day of the week that you want the report to be created on.
      1. **Run time slot**: For short-term, use the dropdown menu to select the time window for which you want the system to use when it runs the report. The forecast scenario for short term runs every day. For long-term, select the day.
      1. **Run time zone**: Use the dropdown menu to select the time zone you want the system to use when it runs the report.
1. On the **Historical data** card, fill in the following details:
      1. **Data source**: select **Internal** or **External**.
      1. **Historical data start date**: Choose how far back in time you want to begin the data. By default, this date is two years previous from the present date when you create the report.
      1. **Seasonality**: Use the dropdown menu to select a holiday calendar if applicable.
      1. **External data**: If you're using external data as your data source, select the search field, browse to your file, and then select it.
1. Select **Save**.

## View your forecast reports

1. In **Copilot Service workspace**, select **Forecast scenarios** under **Workforce Management** in the site map. The **Active Forecast Scenarios** dashboard appears.
2. Select the **Reports** tab. A list of the reports you created appears.

The first time you access the dashboard, any scenarios you configured appear in **Draft** status until the first trigger occurs. After that, the scenario shows as in progress until it completes. For each scenario, the following details are displayed:

- **Name**: The name of you gave the scenario
- **Current Status**: The state of the scenario. This status can be **Draft**, **Completed**.
- **Interval**: The type of scenario.
- **Duration**: The length of time.
- **Target entity**: The record type.
- **Last Run On**: The date the scenario last ran. Based on the **Forecast run schedule** you selected.
- **Is recurring**: Indicates whether the scenario repeats.
- **Recurrence time slot**: The day or time the report runs.
- **Recurrence time zone**: The time zone in which the report runs.

### Data visualization

When you open a report, the following visualizations are available:

**Duration**: Allows you to input the date range or use the sliders to set the dates.

**Channel**: Select one or more channels for which you want data displayed.

**Queue**: Select one or more queues for which you want data displayed.

**Trend chart**: Shows the actual historical volumes from the past to the predicted volume in the future. The forecast is based on actual case, conversation, and service representative records created in the past.

**Detailed view**: You can filter the data in the following ways:
   - **All**: Displays the actual and forecasted numbers across all channels and queues. You can use the drill up and down buttons to drill to specific levels in the hierarchy.
   - **Channel**: Displays the actual and forecasted numbers, sliced by each channel. You can use the drill up and down buttons to drill to specific levels in the hierarchy.
   - **Queue**: Displays the actual and forecasted numbers, sliced by each queue. You can use the drill up and down buttons to drill to specific levels in the hierarchy.
