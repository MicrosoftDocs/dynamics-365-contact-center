---
title: Set up your workforce
description: Learn how to set up workforce with the required roles and skills.
ms.date: 04/14/2025
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

# Set up your workforce with required roles and skills

The first step to managing your workforce is to set up your users with the correct security roles and skills. This ensures that each customer service representative (service representative or representative) is appropriately assigned to their role and equipped with the necessary skill sets to meet the demands of your contact center. 

This article walks you through the process of creating users and assigning the appropriate security roles and skills to help you enable effective workforce management.

## Create supervisors and service representatives and assign security roles.

You can create service representatives and supervisors either manually or by bulk upload using the [User Management](/dynamics365/customer-service/administer/users-user-profiles) feature in Dynamics 365. 

Make sure your users are assigned the following security roles: 

- Supervisors must be assigned the Omnichannel supervisor security role.
- Service representatives must be assigned the Omnichannel agent security role.

## Assign skills and proficiency levels  

Before assigning tasks and scheduling, you must equip your service representatives with the necessary skills and proficiency levels. This ensures that the right individuals are assigned to the appropriate tasks based on their expertise.

### Create the required skills

1. In the site map of the Copilot Service admin center app, go to **Operations**, and then select **Workforce management**. The **Workforce management** page appears.
1. In **User management**, select **Manage** next to **Skills hub**.
1. On the **Skills** card, select **Create**, and then enter the required details.
1. Select **Save**.

### Assign skills and proficiency levels

1. In the site map of the Copilot Service admin center app, go to **Operations**, and then select **Workforce management**. The **Workforce management** page appears.
1. In **User management**, select **Manage** next to **Enhanced user management**.
1. Select the users for whom you want to assign skills, and then on the **Update user attributes** dropdown menu, select **Update skills**.
1. Select the relevant skills and proficieny levels to assign to the user(s).
1. Select **Save**.

## Create bookable resources

For service representatives to be scheduled for activities, you must create a bookable resource entity for each representative.

1. In the site map of the Copilot Service admin center app, go to **Operations**, and then select **Workforce management**. The **Workforce management** page appears.
1. In **Workforce setup**, select **View** next to **User management**. The **User managment** page opens.
1. Select **Manage** next to **Users**.
1. Select the user, and then on the page that opens, select the **Details** page. The page refreshes and displays the user's details.
1. Select the **Omnichannel** tab. 
1. On the **Skills Configuration** card, select **New Bookable Resource**.
1. Enter the following details:
   - **Resource Type**: Select **User**.
   - **Name**: Name of the user.
   - **Time zone**: Select the user's time zone in the dropdown menu.
1. Select **Save**. 

## Add Workhours 

You can customize the work hours for each user to ensure that they're available for scheduling at the appropriate times. While the system initially uses default work hours, defining custom work hours allows you to specify when each resource is available, accommodating varying schedules and operational needs. 

1. In the site map of the Copilot Service admin center app, go to **Operations**, and then select **Workforce management**. The **Workforce management** page appears.
1. In **Workforce setup**, select **View** next to **User management**. The **User managment** page opens.
1. Select **Manage** next to **Users**.
1. Select the user, and then on the page that opens, select the **Details** page. The page refreshes and displays the user's details.
1. Select the **Omnichannel** tab. 
1. On the **Skills Configuration** card, select **Bookable Resource**, and then select **Show Work Hours**.
1. You can either update the existing hours for all events, or select **New** > **Working Hours** to add new working hours.
1. Set the start and end times of the resource's work hours, and then select a repeat pattern. For recurring working hours, where resources can have different working hours on different days of the week, use the **Custom repeat pattern**.
1. Set the time zone for the resource’s work hours to ensure that the system uses them correctly. 
1. Select **Save** to save the work hours and update the work hour calendar.
