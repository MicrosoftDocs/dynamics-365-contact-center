---
title: Forecast with weighted average (preview)
description: Learn how to build a weighted average forecast (preview) from selected historical days in Workforce Management for Dynamics 365 Customer Service and Contact Center.
ms.date: 08/19/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Forecast with weighted average (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

A weighted average forecast builds the prediction from a set of historical days that you choose, with a weight assigned to each day. Instead of fitting a trend over a long history, the model blends the intraday patterns of your selected days according to their weights. Use it when you want a forecast grounded in specific comparable days. For example, base the forecast for an upcoming promotion on the pattern of past promotion days. A weighted average scenario produces both volume and average handle time (AHT) intraday patterns, along with confidence intervals.

> [!IMPORTANT]
> Forecasting isn't intended for use in making decisions that affect a person's employment. You're responsible for using this feature in compliance with applicable laws, including those that govern access to employee analytics and the monitoring, recording, and storage of communications with end users. For the complete responsible-use notice, see [Overview of forecasting](workforce-management-forecast-overview.md).

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Create a weighted average forecast scenario

1. In the site map of Copilot Service workspace, select **Forecasting** under **Workforce Management**.
1. On the **Active Forecast Scenarios** page, select **New** > **Weighted average forecast scenario**.
1. On the **Details** card, enter a **Name**, a **Forecast start date**, a **Duration (days)**, and a **Time zone**.
1. On the **Historical Data** card, the **Data source** is **External** and read-only. Select your uploaded file in **External data**.
1. On the **Configuration** card, select the **Forecast entity** (**Conversation** or **Case**).
1. Select **Save**.

> [!NOTE]
> Weighted average forecasting supports only external data sources during preview.

## Adjust the forecast

Open the scenario and select the **Adjust Forecast** tab to define how the weighted average is built. As you change the source days and weights, the preview chart and summary metrics update.

### Set the forecast target

Under **Forecast Target**, choose the **Channel**, **Queue**, and the **Apply To** date that the pattern applies to. To revert your changes, select **Discard Unsaved Changes** or **Discard All Changes**.

### Select and weight source days

Under **Source Data — Historical Days**, select the historical days to base the forecast on. The weighted average across those days produces the forecast. To manage the list, use **Add Source Day** and **Remove Selected**, and then choose a weighting mode:

- **Manual**: Edit each weight directly. The normalized percentage updates as you type.
- **Recency**: Weights more recent days higher automatically.
- **Equal**: Gives every selected day the same weight.

Each source-day row shows the **Date**, **Day of Week**, **Total Volume**, an intraday volume pattern and intraday AHT pattern, the **Weight**, and the **Normalized percentage**.

### Review the preview and confidence

Summary tiles show the number of **Source Days**, the **Weighted Avg Volume**, and the **80% Confidence Interval** and **95% Confidence Interval**.

The **Forecast Preview — Intraday Distribution** chart plots the weighted average intraday pattern, with confidence bands. Switch between **Spline** and **Line** views. **Source Comparison** shows volume per source day.

## Related information

- [Overview of forecasting](workforce-management-forecast-overview.md)  
- [Create and manage forecast scenarios](workforce-management-forecast-scenarios.md)  
- [Import historical data for forecast scenarios](workforce-management-import-historical-data.md)
