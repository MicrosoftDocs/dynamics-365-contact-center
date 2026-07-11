---
title: Create and schedule a shift plan
description: Learn how to create and schedule a shift plan in Copilot Service workspace to help you more easily manage your staffing needs.
ms.date: 07/07/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and schedule a shift plan

As a customer service supervisor, you use shift plans to plan and schedule customer service representatives (service representatives, representatives) based on availability, skills, and business requirements. Shift plans help ensure your contact center has the appropriate coverage to support daily operations.

A shift plan is a predefined template that defines the structure of a shift and its staffing requirements. By creating shift plans in advance, you can standardize shift patterns and ensure the right service representatives are available at the right time.

A shift plan includes the following key components: 

- **Start date**: The date that the shift plan begins, based on the time zone defined for the plan.
- **End date**: The date on which the shift plan ends, based on the time zone defined for the plan.
- **Start time**: The time the shift plan starts each day, as defined by the weekly recurrence.
- **End time**: The time that the shift plan ends, as defined by the Weekly recurrence.
- **Capacity plan**: The number of service representatives required during the shift.
- **Skills**: The preferred skills a service representative must have to work the shift.
- **Queues**: The support queues that service representatives are assigned to during the shift.
- **Calendar**: The operational settings for the shift plan, including the time zone, weekly recurrence, and any holiday calendars observed by the contact center.
- **Shift activities**: The operational and nonoperational activities that occur during the shift, such as work time, training, and breaks. These activities repeat for each day of the shift.

## Prerequisites

Before you can work with shift plans, your administrator must enable the feature in Copilot Service admin center. Learn more in [Enable shift and schedule management](../administer/workforce-management-enable-schedule-management.md).

## Create a shift plan

1. In the site map of the Copilot Service workspace app, go to **Workforce management**, and then select **Shift Planning**. The **My Shift Plans** page appears.
1. Select **New**, and then select either **Schedule manually** or **Schedule with capacity plan** from the dropdown menu. The **New Shift Plan** page appears.
1. On the **Plan Details** card, fill in the following required details:
     - **Shift Plan Name**: The name for the shift plan.
     - **Start Date**: The start date for the shift plan.
     - **End Date**: The end date for the shift plan.
     - **Required Staff**: The number of staff members needed for the shift.
     - **Start time**: The shift start time. Once you save the shift plan, you can't change this time.
     - **End time**: The shift end time.
     - **Time zone**: The time zone where the shift occurs. Once you save the shift plan, you can't change the time zone.
1. On the **Activity Itinerary** card, select **Add activity**, and then select the activities you want to add the shift from the dropdown menu. You can update the duration of any activity after adding it to the **Activity Itinerary** by hovering on the activity. Handle bars appear on the activity box. You can select the respective handle bar, and then drag it to increase or decrease the duration of the activity. You can also change the order of activities or delete them as follows:
   - To move the activity, drag the activity up or down. You can also right-click the activity, and then select **Move up** or **Move down**.
   - To delete the activity, select the activity, and then press the **Del** key on your keyboard. You can also right-click the activity, and then select **Delete**.
1. Select **Save**.

## Schedule shift plan resources

To schedule resources for your shift plan, select [Schedule Workforce](workforce-management-schedule-workforce.md).

## Related information

[Configure capacity planning](../administer/workforce-management-configure-capacity-planning.md)
