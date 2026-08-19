---
title: Overview of forecasting
description: Learn how Workforce Management forecasting predicts conversation and case volume and average handle time so you can plan staffing in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 08/19/2026
ms.topic: overview
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Overview of forecasting

Forecasting predicts the future demand on your support operations so you can plan staffing and day-to-day operations with confidence. A forecast estimates two things, broken down by channel and queue: how much work will arrive (the volume of conversations and cases) and how long each interaction takes to handle (the average handle time, or AHT).

Forecasting is the first stage of Workforce Management. Its output feeds capacity planning, which calculates staffing requirements, and those requirements drive scheduling.

> [!IMPORTANT]
> This feature helps customer service managers and supervisors enhance their team's performance and improve customer satisfaction. Don't use this feature to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. You're solely responsible for using Dynamics 365 Customer Service, Dynamics 365 Contact Center, Copilot Service workspace, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and to monitoring, recording, and storing communications with end users. This compliance includes adequately notifying end users that their communications with customer service representatives might be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Also, have a mechanism in place to inform your customer service representatives that their communications with end users might be monitored, recorded, or stored.

## What you can forecast

Every forecast scenario produces two related measures, which you can slice by channel and queue:

- **Volume**: The number of conversations or cases expected in each time interval. Forecasting excludes conversations that AI agents handle without a service representative joining.
- **Average handle time (AHT)**: The expected handling time per interaction in each interval. To view AHT alongside volume, turn on **Show AHT** in the report.

## Forecast scenario types

When you create a scenario, choose one of three types. Short-term and long-term scenarios apply a trend-based (linear) model to your historical data. A weighted average scenario builds the forecast from specific historical days that you select and weight.

### Short-term forecast scenario

Predicts intraday volume and AHT in 15-minute intervals for a horizon of up to six weeks (42 days). The available range depends on how much historical data you have. Use a short-term scenario for daily staffing and intraday planning.

### Long-term forecast scenario

Predicts daily volume and AHT for a horizon of up to three years (1,096 days), depending on available history. Use a long-term scenario for seasonal and business planning.

### Weighted average forecast scenario (preview)

Builds a forecast for a target channel and queue by combining a set of historical days, each with an assigned weight. The weighted average across those days produces the intraday volume and AHT pattern, together with confidence intervals. Use a weighted average scenario when you want a forecast grounded in specific comparable days. For example, base the forecast for an upcoming promotion on the pattern of previous promotion days.

> [!NOTE]
> Weighted average forecasting is in preview.

## Compare the forecast scenario types

The following table compares the three scenario types across key characteristics.

| Characteristic | Short-term | Long-term | Weighted average (preview) |
|---|---|---|---|
| Interval | 15 minutes (intraday) | Daily | 15 minutes (intraday) |
| Maximum horizon | 6 weeks (42 days) | 3 years (1,096 days) | Set by start date and duration |
| Forecast type | Linear | Linear | Weighted average |
| Method | Trend model over history | Trend model over history | Weighted blend of days |
| Data source | Internal or external | Internal or external | External |
| Auto refresh | Supported (internal) | Supported (internal) | Manual only |

## How forecasting fits into Workforce Management

Forecasting is the foundation of the planning lifecycle:

1. Forecasting estimates future volume and AHT.
1. Capacity planning uses the default forecast snapshot to calculate staffing requirements.
1. Scheduling turns those requirements into shifts.

## Key considerations to enhance forecast accuracy

For the most accurate forecasts, use historical data that meets the following criteria:

- **Non-sparse data**: The dataset includes a record for every day, with no missing or incomplete entries. When each day has a recorded volume, the model has a complete set of observations to learn from.
- **Clear weekly pattern**: Volume follows a consistent weekly pattern. For example, weekends consistently have lower volumes and workdays have higher volumes, or the reverse. A repeating pattern gives forecasting a reliable basis to work from.
- **Volume-based accuracy**: When the other criteria are met, forecast quality improves with larger volume inputs. Higher data volumes produce a more accurate and robust forecast.
- **Absence of level shifts**: Recent days and future periods don't have sudden or significant shifts in volume levels. When volumes stay stable, historical patterns remain relevant and dependable.
- **Longer historical dataset**: When all the preceding criteria are met, a longer history further improves accuracy. More history gives the model a broader view of patterns and trends over time, so it can capture more variation and produce more accurate forecasts.

> [!NOTE]
> Forecasts provide reliable estimates but might not fully account for external factors such as unexpected trends or sudden business needs.

## Prerequisites

- A security role with the **Read** privilege on the `msdyn_dataanalyticsreport_forecast` table.

## Regional availability

Forecast reports are available in specific geographic regions. For more information, see [Supported regions and languages for analytics and insights](/dynamics365/customer-service/administer/cs-region-availability-service-limits).

## Related information

- [Create and manage forecast scenarios](workforce-management-forecast-scenarios.md)  
- [Forecast with weighted average (preview)](workforce-management-forecast-weighted-average.md)  
- [Estimate AI agent credits for a forecast](workforce-management-credit-estimation.md)  
- [Import historical data for forecast scenarios](workforce-management-import-historical-data.md)
