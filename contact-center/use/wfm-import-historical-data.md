---
title: Import historical data
description: Learn how to import historical data to use in your case and conversation forecast scenarios.
ms.date: 04/11/2025
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---
# Import historical data

When you create a forecast scenario, use historical data as the input source for the forecasting model to predict future volume. Historical data can be tracked up to two years from the date when you create the forecast report. To configure the report to use historical data, you must first upload a historical data file.

## Import a historical data file 

1. In the site map of Copilot Service workspace, select **Forecast External Data** under **Workforce Management**. The **Active File uploads** page appears.
1. Select **New**. The **New WEM File Upload** page appears.
1. For **Name**, enter a name for the file.
1. For **File data interval**, select either **Intraday** (short term) or **Daily** (long term).
1. Select **Save**.
1. For **File**, select **Choose File**, and then browse to and select the file you want to use.
1. Select **Save**.

You can now use this file as your data source when you [create a new forecast report](wfm-forecast-scenarios.md#create-a-short-term-or-long-term-forecast-report).
