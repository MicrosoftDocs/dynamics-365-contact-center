---
title: Create and manage shift rotation policies
description: Learn how supervisors can create and manage shift rotation policies to rotate customer service representatives across time slots.
ms.date: 07/10/2026
ms.topic: how-to
author: cbms03
ms.author: cbrahmandam
ms.reviewer: laalexan
---

# Create and manage shift rotation policies

As a supervisor, use shift rotation policies to rotate customer service representatives (service representatives or representatives) across recurring time slots on a configurable cadence. Use rotation policies to balance workload, support around-the-clock coverage, and ensure fair shift distribution across representatives. The scheduler consults the rotation policy when it generates bookings, drawing representatives from the cohort whose rotation position matches the booking time.

## Prerequisites

- An administrator must enable the shift rotation policies feature in Customer Service admin center under **Workforce Management** > **Shift and Scheduling**.

## Access shift rotation policies

You access shift rotation policies from the Customer Service workspace.

1. Open **Customer Service workspace**.
1. Go to **Workforce Management**.
1. Select **Shift rotation policies**.

## View and manage shift rotation policies

The **Shift rotation policies** page lists all rotation policies in your organization. For each policy, you can view:

- Policy name
- Status (Active or Paused)
- Cadence
- Number of slots
- Assigned shift plans
- Activation date

You can filter, sort, and search the list to find specific policies.

## Manage shift rotation policies

### Create a shift rotation policy

1. On the **Shift rotation policies** page, select **New**.
1. Enter a unique **Policy name**.
1. Select the **Activation date**. The activation date marks the start of the first rotation cycle, and you can't change it after you save the policy.
1. Select the **Timezone** for the policy. The slot times reflect the same time zone that you set for the shift rotation policy.
1. Set the **Cadence** by entering the number of days in each rotation cycle.
1. Add time slots:
   1. Select **Add slot**.
   1. Enter the **Start time** and **End time** for the slot.
   1. Search for and select the representatives to assign.
   1. Select **Save & Close**.
   1. Repeat until you have between 2 and 24 slots.
1. Select **Save** to create the policy.

> [!NOTE]
> A representative can belong to only one rotation policy at a time. Within a single policy, a representative can be assigned to multiple slots.

### Edit a shift rotation policy

1. On the **Shift rotation policies** page, select the policy to edit.
1. Update the policy name, cadence, slot configuration, or representative assignments.
1. Select **Save**.

> [!IMPORTANT]
> Edits to a shift rotation policy take effect on the next scheduler run. Previously generated schedules aren't changed.

### Pause and resume a shift rotation policy

1. On the **Shift rotation policies** page, select the policy.
1. Select **Pause** to freeze the rotation at the current cycle.
1. Select **Resume** to restart rotation from the frozen cycle.

> [!NOTE]
> While a policy is paused, service representatives stay in their current slot positions. The scheduler continues to draw representatives from those positions until the policy resumes.

### Delete a shift rotation policy

1. On the **Shift rotation policies** page, select the policy.
1. Select **Delete**.
1. Confirm the deletion.

> [!IMPORTANT]
> You can't delete a shift rotation policy assigned to one or more shift plans. Remove the policy from each shift plan before deleting it.

### Assign a shift rotation policy to a shift plan

1. On the shift planning page, select the shift plan you want to change from the list.
1. In the shift plan settings, select **Rotation policy**.
1. Select the policy from the list.
1. Select **Save**.

> [!NOTE]
> A shift plan can have only one rotation policy. You can assign a rotation policy to multiple shift plans.

## Related information

[Configure shift activity types](../administer/workforce-management-shift-activity-types.md)

<!--
## Additional capabilities

### Pool resolution

When the scheduler generates bookings for a shift plan with a rotation policy, it draws CSRs in the following order:

- **Bid-locked CSRs** assigned to the shift plan
- **Cohort CSRs** whose rotation position matches the booking time
- **Flexible workforce** CSRs not assigned to any active rotation policy
- **Cross-policy borrow** from CSRs in other rotation policies whose current slot overlaps the booking time

If the scheduler can't fill demand from any of these sources, it flags the activity as unstaffable for supervisor review.

### Booking source visibility

Each booking generated under a rotation policy is tagged with a source classification:

- Cohort
- Flexible
- Borrow
- Bid-locked

Supervisors can filter bookings on the schedule board by source classification to understand how each booking was filled.

### Activity splitting

When a shift plan activity crosses a slot boundary, the scheduler splits the activity into segments. Each segment is staffed from the cohort serving that slot.

> [!NOTE]
> Removing a CSR from a rotation policy doesn't cancel their existing bookings. The CSR joins the flexible workforce immediately, and future scheduler runs reflect the change.

> [!IMPORTANT]
> Only the auto-scheduler honors shift rotation policies. Manual assignments made on the schedule board don't follow the rotation policy.
