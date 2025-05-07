---
title: Import historical data
description: Learn how to import historical data to use in your case and conversation forecast scenarios.
ms.date: 05/02/2025
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

> [!NOTE]  
> The File has to be a CSV file with the format mentioned below.

1. For **Name**, enter a name for the file.
1. For **File data interval**, select either **Intraday** (short term) or **Daily** (long term).
1. Select **Save**.
1. For **File**, select **Choose File**, and then browse and select the required file.
1. Select **Save**.

You can now use this file as your data source when you [create a new forecast report](wfm-forecast-scenarios.md#create-a-short-term-or-long-term-forecast-report).

## Required data

Refer to the following tables to understand the required headers, values, and descriptions.


### Daily Data:

 **DateTime** | **ChannelId** | **ChannelName** | **QueueId** | **QueueName** | **Volume** | **AHT** | **Interval** | **MaxVolumeByHour** | **AgentCount** 
--------------|---------------|-----------------|-------------|---------------|------------|---------|--------------|---------------------|----------------


 
### Intra Day Data:###
 **DateTime** | **ChannelId** | **ChannelName** | **QueueId** | **QueueName** | **Volume** | **AHT** | **Interval** | **MaxVolumeByHour** 
--------------|---------------|-----------------|-------------|---------------|------------|---------|--------------|---------------------

### Description  
**DateTime:** The Date and Time for the forecast data point. Format: yyyy-MM-dd HH:mm:ss  

**ChannelId:** Id of the channel like voice, web or any custom channel. This is the value from the system you have obtained the data from. If you are not aware, the value can be left at 1  

**ChannelName:** Channel - Name of the channel corresponding to that Id from your host system  

**QueueId:** 1 - Id of the queue that the datapoint corresponds to, from your host system. If you are not aware, the value can be left at 1.  

**QueueName:** - Name of the queue corresponding to the Id from your host system.  

**Volume:**  No. of incidents/conversations for the day with the combination of queue and channel. This should be a whole number.  

**AHT:** Average duration of one incident/conversation interaction, in minutes. This should be a whole number.  

**Interval:**   
* “Daily” – For daily data  
* “15 min” – For the intraday data  

**MaxVolumeByHour:** The Maximum number of interactions/conversations, per day. This should be a whole number.  

**AgentCount:** The number of agents required. (This is ONLY for the Daily Forecast)
