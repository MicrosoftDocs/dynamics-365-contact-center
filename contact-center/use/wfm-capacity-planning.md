---
title: Create and manage capacity planning
description: Learn how to set up capacity plans to help you effectively manage your workforce.
ms.date: 04/11/2025
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and manage capacity planning

Capacity planning ensures you have the right number of customer service representatives (service representatives or representatives) available at the right time. It lets you forecast staffing needs at different levels of detail to align workforce capacity with the expected service demand.

You can plan capacity in the following ways:

- **Short-term planning**: Forecast staffing needs in 15 min intervals for up to six weeks, that allow real-time adjustments.
- **Long-term planning**: Plan daily staffing requirements for up to six months to support strategic workforce decisions.
- **Scenario analysis**: Model different workload scenarios to assess the impact of changes in demand.
- **Data slicing**: View staffing projections by specific channels and queues for insights.

## Prerequisites

Your administrator has installed the **Workforce Management for Customer Service** package in the Power Platform admin center app and then enabled the feature in Copilot Service admin center.

## Create a capacity plan

1. In the site map of Copilot Service workspace, select **Capacity planning** in **Workforce Management**. The **Active Capacity Plans** page appears.
1. Select **New**, and the select either **Short-term** or **Long-term** from the dropdown menu. The **New Capacity Plan** page appears.
1. On the **Details** card, fill in the **Name**, and then search for the **Forecast Scenario** you want to use.
1. On the **Configuration parameters** card, fill in the following details:
     - **Service Level (%)**: The percentage of the conversations needed to meet the target answer time. For example, if you set your required service level percentage to 80 and your target answer time to 77, it indicates that you want 80 percent of your conversations to be answered in 77 seconds or less.
     - **Shrinkage**: The percentage of time service representatives are unavailable to handle conversations. If you increase this number, the percentage of time that the service representatives are unavailable goes up, which means you would need more service representatives to meet the service-level agreement.
     - **Target Answer Time (Seconds)**: The number of seconds in which you want your service representatives to answer their conversations.
     - **Concurrency (#)**: The number of simultaneous interactions per service representative. For voice calls, this value should be set to one. For chats and messaging channels, this value can be set as desired.
1. On the **Forecast run schedule** card, make sure the toggle for **Auto-extension** is set to **Yes**.
1. Select **Save**.

## View your capacity plans

1. In the site map of **Copilot Service workspace**, select **Capacity planning** in **Workforce Management**. The **Active Forecast Scenarios** dashboard appears.
1. Select the plan you want to view from the list, and then select the **Reports** tab.

### Data filters and visualizations

When you open a report, the following filters and visualizations are available:

- **Duration**: Allows you to enter the date range or use the sliders to set the dates.
- **Intervals**: Select the **Daily**, **Weekly**, or **Monthly** view.
- **Channel**: Select one or more channels for which you want data displayed.
- **Queue**: Select one or more queues for which you want data displayed.

In the **Capacity Plan Output** section, **Detailed view**, you can filter the data in the following ways:

**Detailed view**: You can filter the data in the following ways:
   - **All**: Displays the capacity numbers across all channels and queues.
   - **Channel**: Displays the capacity numbers, sliced by each channel. 
   - **Queue**: Displays the capacity numbers, sliced by each queue. 
 
You can use the drill up and down buttons to drill to specific levels in the hierarchy.

