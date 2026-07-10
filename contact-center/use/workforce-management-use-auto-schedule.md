---
title: Schedule representatives with auto-schedule
description: Learn how to use the auto-schedule feature to schedule large numbers of representatives for activities.
ms.date: 07/10/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Use auto schedule to schedule representatives

If you have many customer service representatives (service representatives or representatives) to schedule activities for, use auto-schedule on the schedule board to quickly create a shift plan.

## Use auto schedule

1. In the site map of Copilot Service workspace, select **Shift planning** in **Workforce Management**. The **Shift Planning** page appears.
1. Select the shift plan you want to use to schedule the representatives, and then select **Schedule Workforce** on the command bar. The shift scheduler board appears.
1. Select **Schedule**, and then select **Auto-Schedule**. The **Auto-Schedule Criteria** pane appears.
1. For **Duration**, select the start and end dates for the activity.
1. Set the filters for **Agent availability**, **Match Skills**, and **Match Queue** as required.
1. Set the **Availability order** to either **Most Available to Least** or **Least Available to Most**.
1. Select **Schedule**. The schedule board updates with the scheduled activities.
1. Select **Publish**. The system sends a booking notification to the scheduled representatives.

## Configure break distribution

Use break distribution settings to automatically place meal and break activities in representative schedules.

In the **Break distribution** section, select the break types that you want to configure, and then specify the scheduling rules for each break type:

- **Minimum time from shift start**: The earliest time a break can be scheduled after a shift begins.
- **Maximum time from shift start**: The latest time a break can be scheduled after a shift begins.
- **Minimum time before next break**: The minimum amount of time required between breaks.

When you finish configuring the settings, select **Schedule**. The schedule board updates and displays the generated breaks in each representative's activity itinerary.

> [!NOTE]
> You can configure only activity types that are:
> - Added to the shift plan.
> - Configured in Copilot Service admin center with **Activity type** set to **Non productive** and **Subtype** set to **Meal/Break**.

After the schedule is generated, review the proposed break assignments. The system prompts you to either accept or reject the generated schedule:

- Select **Accept** to save the generated schedule and make it available for publishing.
- Select **Reject** to discard the proposed schedule and return the schedule board to its previous state.
   
## Related information

[Configure shift activity types](../administer/workforce-management-shift-activity-types.md)
