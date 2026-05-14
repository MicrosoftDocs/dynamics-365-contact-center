---
title: Estimate AI agent credits from forecasts
description: Use AI credit estimation in Dynamics 365 Customer Service and Dynamics 365 Contact Center to project AI credit consumption based on forecasted demand.
ms.date: 05/14/2026
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Estimate AI agent credits from forecasts

AI credit estimation in Dynamics 365 Customer Service and Contact Center helps workforce planners translate forecasted demand into projected AI credit consumption. Organizations can use these estimates to model AI adoption, plan budgets, and understand how forecasted workloads affect AI usage.

AI credit estimation is integrated with Workforce Management forecasting scenarios and supports out-of-the-box AI agents in Customer Service and Contact Center.

> [!IMPORTANT]
> AI credit estimation provides projected AI credit usage for planning purposes only. Actual credit consumption can vary based on factors such as workload volume, conversation complexity, and runtime conditions. Estimates don't represent billing commitments. We recommend validating projections against observed usage over time.

## Prerequisites

- [Workforce Management](../administer/wfm-package-installation.md) is set up.
- Forecast scenarios are configured with forecasted case or conversation volumes.

## Create a forecast scenario

Before you estimate AI credit consumption, create and run a forecast scenario.

1. In **Copilot Service workspace**, got to **Workforce Management** > **Forecasting**.
1. Select **New forecast scenario**.
1. Define the planning horizon.
1. Select an entity type such as **Case** or **Conversation**.
1. Select the queues and channels to include in the forecast.
1. Run the forecast to generate predicted workload volumes.

The forecasting model analyzes historical traffic patterns, including seasonal trends and workload variations, to generate projected demand across queues and channels.

## Estimate AI agent credits

After the forecast scenario is generated, you can estimate AI credit consumption for supported AI agents.

1. Open the forecast scenario output view.
1. Select **Estimate AI agent credits**.
1. Select one or more AI agents for which you want to estimate credit consumption. Supported agents include:
    - **Quality Evaluation Agent**
    - **Case Management Agent**
    - **Customer Intent Agent**
1. Define the percentage of forecasted workload that each AI agent or feature is expected to handle.
1. Review the projected AI credit consumption.

The estimator provides the following metrics:

- **Total credit consumption**: The total projected AI credits required for the selected forecast period.
- **Average consumption per month**: The average projected AI credit usage per month.
- **Maximum monthly consumption**: The highest projected AI credit usage during a single month.

## Analyze detailed consumption data

Use the volume data details table to analyze projected AI credit consumption at a granular level.

You can review AI credit consumption across:

- Time intervals, such as hourly or daily periods
- Queues
- Channels

This detailed breakdown helps you identify peak demand periods and understand where AI usage is highest.

## Refine planning scenarios

You can refine estimates by adjusting forecast assumptions and AI adoption levels.

For example, you can:

- Modify forecasted workload assumptions.
- Adjust AI adoption percentages.
- Run multiple forecast scenarios to compare projected consumption outcomes.

These projections help organizations support budgeting, operational planning, and AI adoption decisions.

## Review estimation results

AI credit estimation provides a unified view of forecasted workload demand and projected AI credit requirements. Organizations can use these insights to validate assumptions, optimize AI usage, and plan workforce capacity more effectively.

### Related information

- [Create and manage forecast scenarios](wfm-forecast-scenarios.md)
- [Import historical data](wfm-import-historical-data.md)
