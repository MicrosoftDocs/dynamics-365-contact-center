---
title: Create and manage capacity plans
description: Learn how to create and manage capacity plans to forecast staffing requirements in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and manage capacity plans

Capacity planning helps you forecast staffing needs and ensure that the right number of customer service representatives (service representatives or representatives) is available at the right time. It aligns workforce capacity with expected service demand at different levels of detail.

You can plan capacity in the following ways:

- **Short-term planning**: Forecast staffing needs in 15-minute intervals for up to six weeks, with allowance for real-time adjustments.
- **Long-term planning**: Plan daily staffing requirements for up to three years to support strategic workforce decisions.
- **Scenario analysis**: Model different workload scenarios to assess the effect of demand changes.
- **Data slicing**: Review staffing projections by channel and queue.

> [!IMPORTANT]
> This feature is intended to help customer service managers and supervisors improve team performance and customer satisfaction. Don't use this feature to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. You're responsible for using Dynamics 365 Contact Center and its associated features in compliance with all applicable laws.

## Prerequisites

Before you create a capacity plan, verify that the following prerequisites are met:

- The Workforce Management for Customer Service package is installed.
- Workforce management and forecasting features are enabled in Copilot Service admin center.
- If you plan to use a forecast scenario, the scenario is available and has completed at least one forecast run.
- Your administrator assigned the required security roles.

## Create a capacity plan

1. In the site map of Copilot Service workspace, select **Capacity planning** under **Workforce Management**. The **Active Capacity Plans** page appears.
1. Select **New**, and then select either **Short-term** or **Long-term**. The **New Capacity Plan** page appears.
1. On the **Details** card, enter a name for the capacity plan.
1. Select a source for the plan:
   - Select a forecast scenario to use its forecasted volume and average handle time (AHT), when available.
   - Select an external forecast file to use forecast data generated outside Dynamics 365.
1. Configure the target entity, forecast interval, time zone, and planning group.
1. On the **Details** card, set **Auto refresh after forecast** to **Yes** if you want the capacity plan to regenerate automatically after the forecast runs. When this option is on, the forecast must run before the capacity plan is generated. If you set it to **No**, you can select **Create New Snapshot** to generate the capacity plan immediately.

   > [!NOTE]
   > You can have up to 10 forecast scenarios with **Auto refresh after forecast** turned on.

1. On the **Configuration parameters** card, configure the following settings:
   - **Service level (%)**: The percentage of interactions that must be answered within the target answer time.
   - **Shrinkage (%)**: The percentage of time that representatives are unavailable to handle interactions, such as time spent on breaks or other activities.
   - **Target answer time (seconds)**: The number of seconds in which representatives should answer interactions.
   - **Concurrency**: The number of simultaneous interactions per representative. Use 1 for voice calls. For chat and messaging channels, set the value based on your operating model.
   - **Occupancy (%)**: The target percentage of time that representatives spend handling interactions.
1. On the **Staffing Hours** card, enter **FTE hours per day**. This value is the standard number of working hours in one full-time-equivalent day. The default is 8 hours.
1. If you need different assumptions for specific channels, queues, dates, or time intervals, upload a parameter override file.
1. Select **Save**.

## Select an input method

You can create a capacity plan by using one of the following input methods.

### Use a forecast scenario

Select a forecast scenario as the demand source. The capacity plan uses forecasted volume and, when available, forecasted AHT from the scenario to calculate staffing requirements.

Changes to the forecast output, including AHT updates or overrides, affect the resulting staffing projections.

### Upload an external forecast file

Upload an external forecast file when your forecast data comes from another system. The file can include forecasted volume and AHT values for the intervals included in the capacity plan.

## Use a parameter override file

Upload a parameter override file to apply different staffing assumptions for specific channels, queues, dates, and time intervals. You can use the file to override values such as service-level targets, target answer time, shrinkage, concurrency, occupancy, and AHT for the applicable intervals.

Overrides affect the staffing projections generated for those intervals. Review the capacity plan output after the plan completes to confirm that the expected values were applied.

## How AHT is used in capacity planning

AHT represents the average time required to handle a customer interaction. Capacity planning uses forecasted or externally provided AHT together with forecasted volume and staffing assumptions to calculate the required number of representatives.

Higher AHT values generally result in higher staffing requirements. If AHT values are adjusted for specific intervals, the corresponding staffing projections are recalculated.

## View your capacity plans

1. In the site map of Copilot Service workspace, select **Capacity planning** under **Workforce Management**.
1. Select the capacity plan that you want to review.
1. Select the **Reports** tab to review the plan output.

From the capacity plan page, you can also perform the following actions:

- Select **View job history** to review plan runs and their status.
- Select **Run capacity plan** to recalculate staffing requirements on demand.
- Select **Refresh** to display the latest plan information.

## Filter and analyze capacity plan output

Use the following filters to focus your analysis:

- **Duration**: Select a date range for the staffing projections.
- **Interval**: Select the applicable daily, weekly, or monthly interval.
- **Channel**: Select one or more communication channels.
- **Queue**: Select one or more queues.

Use the available view options to display the data in a flat view or a time-based hierarchy, such as **Year** > **Month** > **Week** > **Day**. Use drill-up and drill-down controls to navigate the hierarchy.

Capacity plan output can include the following metrics:

- Forecasted volume
- Average handle time
- Average speed to answer
- Service level (%)
- Shrinkage (%)
- Concurrency
- Occupancy (%)
- Required representatives
- Required representatives with shrinkage

Use the charts and detailed data tables to compare forecast demand, staffing assumptions, and projected staffing requirements.

## Review capacity plan status and job history

A capacity plan can have one of the following statuses:

- **Draft**: The capacity plan hasn't run yet.
- **In progress**: The capacity plan is currently running.
- **Completed**: Staffing projections are available.

Open **View job history** to monitor plan runs and review the job status, job type, and run details. When you run a plan on demand, a background job calculates the staffing requirements. The staffing projections update after the job completes.

## Export capacity plan data

1. Open the capacity plan version that you want to export.
1. Select the download option.
1. When the system indicates that the download is being prepared, open the job history.
1. When the job is complete, download the capacity plan output from the job entry.

## Use a planning group with a capacity plan

When you create a capacity plan from a forecast scenario, the capacity plan automatically inherits the forecast scenario's planning group. The planning group keeps the capacity plan aligned with the forecast scenario's time zone, channels, and queues.

When you create a capacity plan from an uploaded forecast file, select the planning group manually.

Learn more in [Use planning groups](workforce-management-use-planning-groups.md).

## Related information

[Use the adherence tracker](workforce-management-adherence-tracker.md)  
[Configure shift activity types](../administer/workforce-management-shift-activity-types.md)  
[Enable adherence historical analytics](../administer/workforce-management-enable-adherence-historical-analytics.md)
