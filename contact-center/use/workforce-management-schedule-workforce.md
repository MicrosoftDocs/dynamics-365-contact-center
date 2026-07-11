---
title: Manage schedules in Workforce Management
description: Use the Schedule Workforce page to view, manage, and publish customer service representative schedules across shift plans in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 07/10/2026
ms.topic: how-to
author: cbms03
ms.author: cbrahmandam
ms.reviewer: laalexan
---

# Manage schedules in Workforce Management

The **Schedule Workforce** page enables supervisors to view, manage, and publish schedules for customer service representatives (service representatives, representatives) across shift plans. It provides an interactive schedule board to assign activities, adjust schedules, and monitor workforce coverage in real time.

## Access the Schedule Workforce page

You can access the schedule board in Copilot Service workspace from either of the following locations:

- Select **Schedule Workforce** from the site map.
- Open a shift plan page and select **Schedule Workforce**.

## View schedules on the schedule board

The schedule board displays activities assigned to service representatives across shift plans. Each activity appears as a tile on the representative's timeline.

Hover over an activity to view the following details:
  - Activity name  
  - Shift plan name  
  - Start and end times  
  - Status (for example, **Committed** or **Unpublished**)  

## Change the schedule view

Use the time-granularity options in the upper-right corner of the schedule board to adjust the level of detail displayed. You can sort by the following options:

  - **15 minutes**
  - **30 minutes**
  - **Hourly**

Smaller intervals provide more detailed scheduling information, while larger intervals provide a broader view of the schedule.

## Understand activity tiles

Activity tiles represent scheduled work  to representatives.

Each tile:

- Displays the activity duration.
- Uses the corresponding activity type color as configured in Copilot Service admin center.
- Can be moved between representatives or time slots by dragging and dropping.
- Can be expanded or collapsed for improved visibility.
- Supports copy and paste keyboard shortcuts. 

## Filter representatives

Filter the schedule board to display only the representatives relevant to your scheduling needs.

Available filters include skill and queues.

You can apply multiple filters simultaneously. Only representatives who match all selected criteria are displayed.

## Focus on a specific shift plan

When you select a shift plan, the schedule board updates and displays the following information:

- Demand for the selected shift plan
- Representatives associated with the shift plan

Use **Representative assignment view** to control which representatives appear on the schedule board:

| View | Description |
|--------|--------|
| All | Displays all representatives. |
| Matched | Displays representatives who match demand criteria. |
| Shift bids | Displays representatives who submit bids. |
| Assigned | Displays representatives who are already assigned to a shift plan. |

## Add representatives to a shift plan and publish the schedule

> [!NOTE]
> You can publish schedules in segments of up to six weeks.

1. Select one or more representatives.
1. Select **Add**.
1. Select **Add agents to schedule**.
1. Add representatives for the entire schedule or specific days.
1. Select **Publish**.
1. Select the date range to publish.
1. Confirm the publication operation.

## View daily paid hours

The schedule board displays each representative's paid hours next to their name.

The calculation includes only activities marked as **Paid** in Copilot Service admin center.

## View representative details

Select a representative's name on the schedule board to open a details pane that displays:

- Assigned skills
- Assigned queues
- A link to the representative's calendar
You can view the calendar in the following formats:

- Day
- Week
- Month
- Agenda

## Add extra bookings

1. Go to the required date on the schedule board.
1. Right-click the desired time slot for a representative.
1. Select **Add shift booking**.
1. Select an activity type.
1. Specify the booking duration.
1. Select **Save**.

The booking appears on the schedule board.

## Add ad-hoc activities

1. Select one or more representatives.
1. Select **Add** > **Add ad-hoc activity**.
1. In the side pane, select an activity.
1. Specify the start time and duration.
1. Verify the time zone.
1. Select **Schedule ad-hoc activity**.

> [!IMPORTANT]
> You can schedule ad-hoc activities only for the current day. To assign activities on future dates, add them directly from the schedule board.

## Edit bookings

If you need to update a booking, you can either drag it to a new time slot or edit it directly.

> [!NOTE]
> If you edit a booking in the **Committed** state, the booking changes to the **Unpublished** state. Republish the shift plan to make the updated booking available.

### Move a booking by using drag and drop

1. Select a booking on the schedule board.
1. Drag the booking to a different time slot or representative.
1. Release the booking in the new location.

### Edit a booking manually

1. Go to the relevant date.
1. Right-click the booking.
1. Select **Edit shift booking**.
1. Update the activity type or duration.
1. Select **Save**.

## Delete a booking

1. Right-click the booking.
1. Select **Delete**.
1. Confirm the deletion.

The booking is removed from the schedule.

## Remove representatives from a shift plan

1. Select one or more representatives.
1. Select **Delete**.
1. Choose one of the following options:
   - Remove from entire shift plan
   - Remove from specific days
1. Confirm the removal.
