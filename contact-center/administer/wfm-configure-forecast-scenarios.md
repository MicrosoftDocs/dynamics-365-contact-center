---
title: Enable forecasting
description: Learn how to enable forecasting features so supervisors can predict case and conversation volumes and representative demand.
ms.date: 11/21/2025
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
search.audienceType: 
  - admin
  - customizer
  - enduser
ms.custom: 
  - dyn365-customerservice
---

# Enable volume forecasting for supervisors

Forecasting allows supervisors to predict case and conversation volumes demand based on historical trends.

Key benefits:

- **Long term Forecast:** Predict conversation and case volumes at a daily level for up to six months.
- **Short term Forecast:** Generate 15-minute interval forecasts for up to six weeks to manage real-time demand fluctuations.
- **Scenario Forecasting:** Model different business scenarios to assess their impact on workload and staffing.
- **Data Slicing:** Break down forecasted data by channels and queues for granular insights.
- **Import External Data:** Incorporate historical data from external systems via file import to enhance forecast accuracy.
- **Export Forecasts:** Download forecast data into spreadsheets for further analysis.
- **Visualize Trends:** View daily, weekly, and monthly forecast trends using interactive charts.

## Prerequisites

Complete the steps in [Set up user management](wfm-user-management.md).
    
## Enable forecasting

1.	In the site map of the Copilot Service admin center app, go to **Operations**, and then select **Workforce management**. The **Workforce management** page appears.
1.	In **Forecasting**, select **Manage** next to **Forecast volume**.
1.	On the **Forecast volume** page, set the **Enable forecasting** toggle to **On**.
1.	Select **Save and Close**.

## Enable AI-based forecasting (preview)

As an administrator, you can enable AI-based forecasting for your organization. This feature allows AI to dynamically select the best forecasting method for each scenario. When this feature is enabled, supervisors can choose the AI-based option in their forecast scenario details.

Key benefits:

- **Ensures the highest forecast accuracy**: Automatically chooses the model best suited to the customer’s historical patterns, seasonality, trends, and data quality.
- **Eliminates guesswork and manual tuning**: Removes the need for users to understand complex statistical models or test multiple methods themselves.
- **Adapts to changing business patterns**: Dynamically reevaluates which model performs best as demand, channels, or customer behavior evolve.
- **Improves operational efficiency**: Enables supervisors to better staff, schedule, and drive budget decisions with more reliable forecasts.
- **Provides transparency**: Reasoning and confidence scores explain why a specific model was selected, helping build trust in forecast outputs.

AI-based forecasts include an **AI Reasoning** tab in the job history to show how the model made its decision. When supervisors use AI-based forecasting, an AI disclaimer appears in the UI.

> [!Note]
> - Auto-refresh is disabled for AI-based forecasting. Forecasts must be run manually.
> - AI-based forecasting requires AI credits. Ensure your organization has sufficient credits before enabling this feature.

To enable AI-based forecasting for all forecast scenarios, complete the following steps:

1. In the site map of the Customer Service or Copilot Service admin center, go to **Operations**, and then select **Workforce management**. The **Workforce management** page appears.
1. In **Forecasting, select **Manage** next to **Forecast volume**.
1. On the **Forecast volume** page, set the **Enable forecasting** toggle to **On**.
1. Select the **Allow dynamic forecasting (AI-based)** checkbox.
1. Select **Save and close**.

