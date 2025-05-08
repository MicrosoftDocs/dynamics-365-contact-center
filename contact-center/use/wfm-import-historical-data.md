---
title: Import historical data
description: Learn how to import historical data to use in your case and conversation forecast scenarios.
ms.date: 05/07/2025
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
   > You must use the CSV file format and format the headers and explained in [Required data](#required-data).

1. For **Name**, enter a name for the file.
1. For **File data interval**, select either **Intraday** (short term) or **Daily** (long term).
1. Select **Save**.
1. For **File**, select **Choose File**, and then browse and select the required file.
1. Select **Save**.

You can now use this file as your data source when you [create a new forecast report](wfm-forecast-scenarios.md#create-a-short-term-or-long-term-forecast-report).

## Required data

Refer to the following example tables to understand the required headers, values, and descriptions.

### Daily (long-term) data

 **DateTime** | **ChannelId** | **ChannelName** | **QueueId** | **QueueName** | **Volume** | **AHT** | **Interval** | **MaxVolumeByHour** | **AgentCount** 
--------------|---------------|-----------------|-------------|---------------|------------|---------|--------------|---------------------|----------------

#### Daily data descriptions

**DateTime**: The date and time for the forecast data point. The format is as follows: yyyy-MM-dd HH:mm:ss  
**ChannelId**: The channel ID, such as voice, web or any custom channel. This is the value from the system you obtained the data from. If you don't know the value, leave it as "1".  
**ChannelName**: The name of the channel that corresponds to your host system's ID.  
**QueueId**: The ID of the queue that the datapoint corresponds to, from your host system. If you don't know the value, leave it as "1".  
**QueueName**: The name of the queue that corresponds to your host system's ID.  
**Volume**: The number of incidents or conversations for the day with the combination of queue and channel. The value should be a whole number.  
**AHT**: The average duration of one incident or conversation interaction, in minutes. The value should be a whole number.  
**Interval**: Daily  
**MaxVolumeByHour**: The maximum number of interactions/conversations, per day. The value should be a whole number.  
**AgentCount**: (Daily forecast only) The number of agents required.  
 
### Intraday (short-term) data:
 **DateTime** | **ChannelId** | **ChannelName** | **QueueId** | **QueueName** | **Volume** | **AHT** | **Interval** | **MaxVolumeByHour** 
--------------|---------------|-----------------|-------------|---------------|------------|---------|--------------|---------------------

#### Intraday data descriptions

**DateTime**: The date and time for the forecast data point. The format is as follows: yyyy-MM-dd HH:mm:ss  
**ChannelId**: The channel ID, such as voice, web or any custom channel. This is the value from the system you obtained the data from. If you don't know the value, leave it as "1".  
**ChannelName**: The name of the channel that corresponds to your host system's ID.  
**QueueId**: The ID of the queue that the datapoint corresponds to, from your host system. If you don't know the value, leave it as "1".  
**QueueName**: The name of the queue that corresponds to your host system's ID.  
**Volume**: The number of incidents or conversations for the day with the combination of queue and channel. The value should be a whole number.  
**AHT**: The average duration of one incident or conversation interaction, in minutes. The value should be a whole number.  
**Interval**: 15 min  
**MaxVolumeByHour**: The maximum number of interactions/conversations, per day. The value should be a whole number. 

### Related information

[Create and manage forecast scenarios](wfm-forecast-scenarios.md)
