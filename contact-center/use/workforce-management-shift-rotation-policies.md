---
title: Create and manage shift rotation policies
description: Learn how supervisors can create and manage shift rotation policies for service representatives in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 08/21/2026
ms.topic: how-to
author: cbms03
ms.author: cbrahmandam
ms.reviewer: laalexan
---

# Create and manage shift rotation policies

As a supervisor, use shift rotation policies to rotate customer service representatives (representatives) across recurring time slots on a configurable cadence. Rotation policies help balance workloads, support 24/7 coverage, and distribute shifts fairly.

When the scheduler generates bookings, it uses the rotation policy to select representatives whose rotation positions match the booking times.

## Prerequisites

An administrator must enable the shift rotation policies feature in Customer Service admin center under **Workforce Management** > **Shift and Scheduling**.

## Access shift rotation policies

1. Open **Customer Service workspace**.
1. Go to **Workforce Management**.
1. Select **Shift rotation policies**.

## View and manage shift rotation policies

The **Shift rotation policies** page lists all rotation policies in your organization. For each policy, you can review the following information:

- Policy name
- Status, such as Active or Paused
- Cadence
- Number of slots
- Assigned shift plans
- Activation date

You can filter, sort, and search the list to find a specific policy.

## Create a shift rotation policy

1. On the **Shift rotation policies** page, select **New**.
1. Enter a unique **Policy name**.
1. Select the **Activation date**.

   The activation date marks the beginning of the first rotation cycle. You can't change the activation date after you save the policy.

1. Select the **Timezone** for the policy.

   Slot times reflect the time zone configured for the shift rotation policy.

1. In **Cadence**, enter the number of days in each rotation cycle.
1. Add a time slot:

   1. Select **Add slot**.
   1. Enter the **Start time** and **End time**.
   1. Select whether the slot applies to every day of the week or only to specific days. You can also configure different start and end times for each day.
   1. Search for and select the representatives to assign.
   1. Select **Save & Close**.

1. Repeat the previous step until the policy contains between 2 and 24 slots.
1. Select **Save** to create the policy.

> [!NOTE]
> A representative can belong to only one rotation policy at a time. Within that policy, the representative can be assigned to multiple slots.

## Edit a shift rotation policy

1. On the **Shift rotation policies** page, select the policy that you want to edit.
1. Update the policy name, cadence, slot configuration, or representative assignments.
1. Select **Save**.

> [!IMPORTANT]
> Changes to a shift rotation policy take effect during the next scheduler run. Previously generated schedules aren't updated.

## Pause or resume a shift rotation policy

1. On the **Shift rotation policies** page, select the policy.
1. Select one of the following actions:
   - Select **Pause** to freeze the rotation at its current cycle.
   - Select **Resume** to restart the rotation from the frozen cycle.

> [!NOTE]
> While a policy is paused, representatives remain in their current slot positions. The scheduler continues to select representatives from those positions until the policy resumes.

## Delete a shift rotation policy

1. On the **Shift rotation policies** page, select the policy.
1. Select **Delete**.
1. Confirm the deletion.

> [!IMPORTANT]
> You can't delete a shift rotation policy that's assigned to one or more shift plans. Remove the policy from each shift plan before you delete it.

## Assign a shift rotation policy to a shift plan

You can assign a shift plan from a rotation policy or select a rotation policy from a shift plan.

### Assign a shift plan from a rotation policy

1. On the **Shift rotation policies** page, open the rotation policy.
1. Select **Assign Shift Plan**.
1. Select the shift plan that you want to assign to the rotation policy.
1. Select **Assign Selected**.

> [!IMPORTANT]
> You can reassign a shift plan from one rotation policy to another. After you reassign the shift plan, remove existing schedules for the affected representatives and rerun scheduling for the changes to take effect.

### Assign a rotation policy from a shift plan

1. On the shift planning page, open the shift plan.
1. In the shift plan settings, select **Rotation policy**.
1. Select the rotation policy from the list.
1. Select **Save**.

> [!NOTE]
> A shift plan can have only one rotation policy. You can assign the same rotation policy to multiple shift plans.
