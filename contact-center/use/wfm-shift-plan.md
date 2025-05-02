---
title: Create and schedule a shift plan
description: Learn how to create and schedule a shift plan in Dynamics 365 Contact Center workspace to help you more easily manage your staffing needs.
ms.date: 04/11/2025
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Create and schedule a shift plan

As a customer service supervisor, you need to be able to manage and schedule agents based on availability, skill sets, and business needs. Being able to manage and schedule your customer service representatives (service representatives or representatives) helps you ensure that your contact center has adequate coverage for all of your customer service operations.

As a supervisor, you can use shift plans to effectively plan and schedule your customer service representatives.

A shift plan is a predefined template you create that details the structure and characteristics of a specific shift, along with the staffing requirements. It allows you to establish your organization’s shift structure and plan for your staffing needs in advance. This preparation helps ensure you have the right service representatives available at the right time to support your business operations.

A shift plan includes the following key components: 

- **Start date**: Specifies the date that the shift plan begins. This date is in the time zone that's set for the shift plan.
- **End date**: Specifies the date that the shift plan ends. This date is in the time zone that has been set for the shift plan.
- **Start time**: Specifies the time that the shift starts. The shift starts on this time for each day of the week, as defined by the *Weekly recurrence*.
- **End time**:  Specifies the time that the shift ends. The shift ends on this time for each day of the week, as defined by the *Weekly recurrence*.
- **Capacity plan**: Specifies the required number of customer service representatives needed for seamless operations during the shift defined by the plan.
- **Skills**: Specifies the preferred skills that a customer service representative needs to have to work the shift.
- **Queues**: Specifies the preferred support queues that a customer service representative has to be part of for the shift.
- **Calendar**: Defines the operational parameters of the shift plan, including any holiday calendars your contact center observes, the days of the week that the shift plan is operational (weekly recurrence), and the time zone of the shift plan.
- **Shift activities**: Specifies the customer service representative tasks and non-operational activities within a shift, such as work, training, lunch breaks, and so forth. These activities repeat for each day of the shift.

## Prerequisites

Before you can work with shift plans, your administrator must enable the feature in Copilot Service admin center. More information: [Enable shift and schedule management](../administer/wfm-enable-schedule-management.md).

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


## Schedule customer service representatives

> [!IMPORTANT]
> You can only schedule or create ad hoc bookings within the start and end time of the shift plan. Scheduling or creating bookings outside of the shift plan time window isn't supported.

Once you define your shift plan, you must schedule your customer service representatives for the shift. This step creates the necessary bookings for the service representatives that corresponds to the activities defined in the shift plan. To schedule your representatives, complete the following steps.

1. In the site map of the Copilot Service workspace app, go to **Workforce management**, and then select **Shift Planning**. The **My Shift Plans** page appears, and includes a list of any shift plans you previously defined.

1. Select the shift plan that you want to schedule by selecting the checkbox next to it, and then select **Schedule people** in the toolbar. (You might need to select the ellipsis to see the **Schedule people** option.) The shift scheduler opens.

   Alternatively, you can also navigate to the shift plan from the **My Shift Plans** list. On the Shift Plan form, select **Schedule** on the toolbar. The shift scheduler opens.

1. The scheduler displays all recommended customer service representatives by default, and shows them on the **Matched** tab. Recommended service representatives are those representatives who meet the **Skills** and **Queues** criteria of the shift plan. You can also view all customer service representatives, irrespective of whether they meet the skills or queues criteria, by selecting the **All** tab.

1. To schedule any service representative, perform the following steps:
     1. Select the plus icon (**+**) next to the representative name to add them to the shift. The **Add** dialog is displayed.<br>
     1. By default, representatives are scheduled for the entire shift plan duration.<br>
     1. If you want to schedule the representative for only specific duration, select the **Add to entire Shift plan** toggle to turn it off. You can then select the specific date duration within the shift plan.<br>
     1. Select **Save**. The necessary bookings are created and displayed on the schedule board for the representative.<br>
     1. Repeat this step for all of the representatives you want to schedule.
         > [!NOTE]
         > Each activity in the activity itinerary is created as a booking for the representative.

### Add extra bookings for a customer service representative

Complete the following steps to add extra bookings for a service representative.

1. Navigate to the date that you want to create the extra booking by using the date selector on top of the schedule board.

1. Right-click the time slot in the schedule board for the service representative you want to book, and then select **Add Shift Booking**. The **Add Shift booking** dialog is displayed.

1. Select the type of activity and the time duration for which you want to book the service representative for this activity.

1. Select **Save**. The system creates and displays the booking on the schedule board for the service representative.

### Edit or delete existing bookings for a customer service representative

> [!NOTE]
> If the booking was already **Committed**, then editing the booking moves it to **Unpublished** state. You must publish the shift plan again to publish the booking.

To edit existing bookings for a service representative, complete the following steps.

1. Use the date selector on top of the schedule board to navigate to the date that contains the booking that you want to edit.

1. Right-click the booking in the schedule board, and then select **Edit Shift Booking** to edit the booking. The **Edit Shift booking** dialog is displayed.

1. Update the activity type or the time duration of the booking.

1. Select **Save**. The booking is updated.

1. Similarly, to delete an existing booking, right-click the booking in the schedule board, and then select **Delete**. The booking is removed.

## Publish shift plan

Once you schedule the necessary service representatives, you must publish the schedules. Publishing the schedule moves the shift plan to the **Published** state. Additionally, the bookings are moved to the **Committed** state. Customer service representatives then receive notifications of their bookings via email and in the app, and can view their bookings on the **My Schedule** calendar.


Complete the following steps to publish the schedules.

1. On the schedule board for the shift plan, select **Publish**. The **Select month for publishing** dialog is displayed.

1. Select the month that you want to publish the schedules for. You can only publish schedules for one month at a time. When you select the month, the dialog shows the number of bookings that will publish.

1. Select **Continue**. The bookings are published.

1. Repeat this step for any other months for the shift plan.

   Customer service representatives receive notifications of their bookings and can view the published bookings on the **My Schedule** calendar.

## Related information

[Configure capacity planning](../administer/wfm-configure-capacity-planning.md)

