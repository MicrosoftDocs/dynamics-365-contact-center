---
title: Use shift swapping
description: Learn how to create, offer, accept, and cancel shift swap requests to manage your work schedule in Dynamics 365 Contact Center.
ms.date: 11/16/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
ms.collection:
---

# Use shift swapping

As a customer service representative, use shift swapping to manage your schedule. Swap scheduled work with another representative while ensuring that shifts stay covered.

By using shift swapping, you can:

- Swap your entire shift with another representative.
- Swap a specific booking or activity instead of the full shift.
- Specify the date and preferred time range that you want to work instead.
- Make an offer on an eligible public shift swap request that another representative created.
- Turn on **Public Post** to make your request available to eligible representatives.

## Prerequisites

Your administrator must enable shift swapping and add you to the Public WEM request team. Learn more in [Enable shift swapping](../administer/workforce-management-enable-shift-swapping.md).

## How shift swapping works

A shift swap starts with a scheduled shift or booking that you want to swap. Identify the scheduled work that you want to swap and specify when you're available to work instead. Then, choose one of the following options:

- **Make an offer on an existing public request**: Leave **Public Post** turned off to view eligible public shift swap requests that other representatives created. Select one of the displayed shifts to make an offer for that swap. Only eligible public posts are displayed. If no public requests match your availability, the list is empty.
- **Post your request publicly**: Turn on **Public Post** to share your request with members of the Public WEM request team who meet the eligibility conditions. **Public Post** doesn't notify representatives when you post the request.

Only the representative who created a public request can accept an offer. Making an offer counts as your confirmation, so you don't need to confirm again. After the representative who created the request accepts an offer, the shifts are swapped automatically.

If the number of days that your administrator set for shift swap expiry passes, the request can no longer be accepted. The representative who created it can still cancel it.

### Swap an entire shift or a specific booking

You can create a request for your entire shift or for a specific booking within the shift.

- **Entire shift**: Set **Full shift day** to **Yes** to include your entire scheduled shift for the selected date in the swap.
- **Specific booking**: If you don't want to swap the entire shift, select a specific booking or scheduled activity. The form populates the **Start Time** and **End Time** for the booking, and calculates the **Hours**.

### Who can view a public post

A posted shift appears on the **Select shift to swap** card only when all the following conditions are met:

- The post is open and public, and another representative created it.
- The posted shift overlaps the date and time that the representative selected.
- The posted shift is published.
- Both shift plans use the same time zone.
- If the representative's shift plan has queues, the person who created the post belongs to at least one of those queues. If the shift plan has skills, the person who created the post has at least one of those skills.
- Neither representative has a conflicting booking outside their shift plan during the swapped time.

### Notifications

Representatives aren't notified when a public shift swap request is posted. After a swap is completed, both representatives receive the standard schedule change notification, which is the same notification that's sent for any other schedule change. This notification follows your administrator's schedule notification settings.

### Example

Suppose you're scheduled for a morning shift but prefer to work an evening shift. Select your morning shift, specify the date and evening time range when you're available, and then do one of the following actions:

- Leave **Public Post** turned off, and select an eligible evening shift from another representative's public request.
- Turn on **Public Post** so that eligible representatives can view your morning shift and make an offer.

After the representative who created the post accepts an offer, the shifts are swapped automatically, and both schedules are updated.

## Before you create a shift swap request

Ensure that you:

- Select the correct date and shift plan for the scheduled work that you want to swap.
- Decide whether to swap the full shift or an individual booking.
- Specify when you're available to work instead.
- Decide whether to make an offer on an existing public request or turn on **Public Post**.
- If you're making an offer on a public request, confirm that the posted shift meets the conditions in [Who can view a public post](#who-can-view-a-public-post).

## Create a shift swap request

1. In the site map of Copilot Service workspace, select **Request Management** in **Workforce Management**. The **All Active Requests** page appears.
1. Select **New**, and then select **Shift Swap**. The **New swap request** page appears.
1. On the **Select shift** card, enter the following information:
    - **Date**: Select the date of the shift that you want to swap.
    - **Shift Plan**: Select the applicable shift plan.
    - **Full shift day**: Select **Yes** to swap the entire shift.
    - **Booking**: If you aren't swapping the full shift, select the booking or activity that you want to swap.
    - **Note**: Enter more information, if needed.
1. On the **Select shift to swap** card, review the default values and update them if needed:
    - **Availability date**: Select the date of the shift that you want to receive.
    - **Preferred time range**: For a partial-day swap, specify a time range that includes the posted booking. For a full-shift-day swap, the time-range fields are disabled, and the search covers the selected day.
1. Choose how you want to find the other side of the swap:
    - To make an offer on an existing public request, leave **Public Post** turned off, and then select an eligible posted shift from the list. If no matching public posts exist, the list is empty. Learn more in [Make an offer on a public shift swap request](#make-an-offer-on-a-public-shift-swap-request).
    - To post your request, turn on **Public Post**. The request becomes visible to representatives who meet the eligibility conditions.
1. Select **Save**.

## Make an offer on a public shift swap request

To offer your shift in response to another representative's public request:

1. In the site map of Copilot Service workspace, select **Request Management** in **Workforce Management**.
1. Select **New**, and then select **Shift Swap**. The **New swap request** page appears.
1. On the **Select shift** card, select the shift plan and date, and choose whether to offer the full shift day or a specific booking.
1. Leave **Public Post** turned off.
1. On the **Select shift to swap** card, review the default values and update them if needed. Set **Availability date** to the date of the shift that you want to receive. For a partial-day swap, set **Preferred time range** to include the posted booking. For a full-shift-day swap, the time-range fields are disabled, and the search covers the selected day. Then, select the posted shift.
1. Select **Save**.

Your offer is added to the other representative's public request, and no new request is created. Several representatives can make offers on the same public request.

## Accept an offer on your public shift swap request

1. In the site map of Copilot Service workspace, select **Request Management** in **Workforce Management**.
1. Open the public shift swap request that you created.
1. Review the dates, times, bookings, and representative details for each offer.
1. Select the offer that you want, and then select **Accept**.

The shifts are swapped automatically, and both representatives' schedules are updated. Offers that you don't accept don't change anyone's schedule.

## Cancel a shift swap request

1. In the site map of Copilot Service workspace, select **Request Management** in **Workforce Management**.
1. Open the shift swap request that you created.
1. Select **Cancel**.

The request is canceled, and no schedule changes are made. You can cancel a request even after it passes the shift swap expiry period.

### Related information

[Enable shift swapping](../administer/workforce-management-enable-shift-swapping.md)  
[Set up your workforce with roles and skills](../administer/workforce-management-user-management.md)  
[Overview of Copilot Service workspace](ccw-overview.md)  
[Use shift bidding to select shifts](workforce-management-representative-shift-bidding.md)
