---
title: Create and manage capacity plans
description: Learn how to set up capacity plans to help you forecast staffing needs and effectively manage your workforce.
ms.date: 04/30/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and manage capacity plans

Capacity planning helps you forecast staffing needs and ensure that the right number of customer service representatives (service representatives, representatives) is available at the right time. It aligns workforce capacity with expected service demand at different levels of detail.

You can plan capacity in the following ways:

- **Short-term planning**: Forecast staffing needs in 15-minute intervals for up to six weeks with allowance for real-time adjustments.
- **Long-term planning**: Plan daily staffing requirements for up to six months to support strategic workforce decisions.
- **Scenario analysis**: Model different workload scenarios to assess the impact of demand changes.
- **Data slicing**: View staffing projections by channel and queue.

## Prerequisites

- The **Workforce Management for Customer Service** package is installed.
- Workforce management features are enabled in Copilot Service admin center.

## Create a capacity plan

1. In the site map of Copilot Service workspace, select **Capacity planning** in **Workforce Management**. The **Active Capacity Plans** page appears.
1. Select **New**, and then select either **Short-term** or **Long-term** from the dropdown menu. The **New Capacity Plan** page appears.
1. On the **Details** card, fill in the **Name**, and then search for the **Forecast Scenario** you want to use.
1. On the **Configuration parameters** card, fill in the following details:
     - **Service Level (%)**: Percentage of conversations that must meet the target answer time. For example, a service level of 80% with a target answer time of 77 seconds means that 80% of conversations must be answered within 77 seconds.
     - **Shrinkage**: Percentage of time representatives are unavailable to handle conversations (for example, breaks or other activities). Higher values require more representatives to meet service-level targets. This percentage accounts for time spent on breaks or other activities that take them away from handling cases and conversations. If you increase this number, the percentage of time that the service representatives are unavailable goes up, which means you would need more service representatives to meet the service-level agreement.
     - **Target Answer Time (Seconds)**: Number of seconds in which representatives should answer conversations.
     - **Concurrency (#)**: The number of simultaneous interactions per representative. Set 1 for voice calls. For chat and messaging channels, set as needed.
1. On the **Forecast run schedule** card, make sure the toggle for **Auto-extension** is set to **Yes**.
   > [!Note]  
   > You can have up to 10 forecast scenarios with Auto-extension enabled.
1. Select **Save**.

## View your capacity plans

1. In the site map of **Copilot Service workspace**, select **Capacity planning** in **Workforce Management**. The **Active Forecast Scenarios** dashboard appears.
1. Select the plan you want to view from the list, and then select the **Reports** tab.

### Data filters and visualizations

When you open a report, the following filters and visualizations are available:

- **Duration**: Select a date range or use the sliders to set the dates.
- **Intervals**: Select **Daily**, **Weekly**, or **Monthly**.
- **Channel**: Select one or more channels for which you want data displayed.
- **Queue**: Select one or more queues for which you want data displayed.

In the **Capacity Plan Output** section, **Detailed view**, you can filter the data in the following ways:
   - **All**: View capacity across all channels and queues.
   - **Channel**: View capacity by each channel. 
   - **Queue**: View capacity by queue. 
 
You can use the drill up and down buttons to drill to navigate the hierarchy.

