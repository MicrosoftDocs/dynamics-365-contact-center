---
title: Configure shift activity types
description: Learn how to configure shift activity types to define work activities and support scheduling and resource planning.
ms.date: 07/10/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
search.audienceType: 
  - admin
  - customizer
  - enduser
ms.custom: 
  - dyn365-customerservice
---

# Configure shift activity types

Shift activity types define the type of work performed as part of a booking. They help you manage and schedule customer service representatives (service representatives or representatives) more efficiently by categorizing tasks, aligning resources with required skills, and ensuring the right coverage at the right time.

## Prerequisites

Complete the steps in [Set up user management](workforce-management-user-management.md).

## Configure a shift activity type

1. In the site map of the Copilot Service admin center app, select **Workforce management** in **Operations**. The **Workforce management** page appears.
1. In **Shift & Schedule Management**, select **Manage** next to **Activity types**.
1. On the **Shift activity types** page, select **New**. The **New Shift Activity Type** page appears.
1. Enter the following details:
     - **Name**: The name of your activity type.
     - **Description (optional)**: A description of the activity.
     - **Assignment status**: Select a status.
     - **Work Type**: Select if the work type is **Productive** or **Non Productive**.  
        - **Subtype**: (optional) For a non-productive work type, you can define if it's for meal or break.  
     - **Duration** (optional): Although this field is optional, you must select a value for the activity to be available in the shift plan.
     - **Owner**: Select an owner for the activity type.
     - **Color** (optional): If you want to change the color of how the activity type appears on the activity board bookings, select the color box. Then, choose the color you want from the color palette.
     - **Dark Theme Color** (optional): If you want to change the dark theme color, select the color box, and then choose the color you want from the color palette.
     - **Adherence**: If you want the activity to be tracked for adherence tracking, turn on the toggle. If you want adherence to be tracked for certain presence states, choose the option you want from the dropdown menu.
       - **Tolerance (HH:mm:ss)**: Defines the grace period before adherence tracking begins.

         > [!Note]  
         > When you set a tolerance value, a delay is allowed between the scheduled start time of an activity and when adherence is enforced. For example, if the tolerance is set to **00:05:00** and an activity is scheduled to start at **10:00 AM**, the representative is considered adherent as long as they're in the mapped presence status until **10:05:00**. If the representative isn't in the expected presence status starting from **10:05:01**, they're marked as nonadherent.

1. Select **Save and Close**.

> [!NOTE]
> Only activity subtypes set as meal or break are available for break distribution configuration in the auto-schedule menu.

## Related information

[Manage schedules in Workforce Management](../use/workforce-management-schedule-workforce.md)  
[Create and schedule a shift plan](../use/workforce-management-shift-plan.md)
