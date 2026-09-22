---
title: Workforce management security roles in the Workforce Engagement Management app (preview)
description: Learn how to choose and assign workforce management security roles and compare their privileges in the Workforce Engagement Management app.
ms.date: 09/18/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.custom:
  - bap-template
---

# Workforce management security roles in the Workforce Engagement Management app (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

The Workforce Engagement Management app includes dedicated roles for forecasting, scheduling, intraday analysis, administration, and representative self-service. Assign roles that match each user's responsibilities instead of granting broad supervisory access.

Use this article to compare privileges, choose a role, and assign it to a user.

> [!IMPORTANT]
> These roles apply only within the Workforce Engagement Management app. They don't replace the Omnichannel supervisor and Omnichannel agent roles or change how those roles work in Copilot Service workspace. Existing deployments continue to work, and no migration is required.

## Available roles

| Role | Intended users |
| --- | --- |
| WFM Administrator | Administrators who configure workforce management and need access to all workforce management capabilities in the app. |
| WFM Forecaster | Planners who build forecast scenarios, capacity plans, and operation calendars and work with external historical data. |
| WFM Scheduler | Schedulers who create shift plans, assign and publish representative schedules, and approve requests. |
| WFM Intraday Analyst | Analysts who monitor adherence and intraday performance in real time and review historical reports. |
| WFM Service Rep | Customer service representatives (service representatives or representatives) who view their own schedules and submit their own requests. |

## Privileges by capability

The following tables list each role's privileges in preview.

### Forecasting

| Privilege | WFM Administrator | WFM Forecaster | WFM Scheduler | WFM Intraday Analyst | WFM Service Rep |
| --- | --- | --- | --- | --- | --- |
| Create, edit, and delete forecast scenarios | Yes | Yes | No | No | No |
| Read forecast scenarios | Yes | Yes | Yes | Yes | No |
| Copy a forecast scenario | Yes | Yes | No | No | No |
| Export a forecast | Yes | Yes | No | No | No |
| Create, edit, and delete external forecast data | Yes | Yes | No | No | No |
| Read external forecast data | Yes | Yes | Yes | Yes | No |

### Capacity planning

| Privilege | WFM Administrator | WFM Forecaster | WFM Scheduler | WFM Intraday Analyst | WFM Service Rep |
| --- | --- | --- | --- | --- | --- |
| Create, edit, and delete capacity plans | Yes | Yes | No | No | No |
| Read capacity plans | Yes | Yes | Yes | Yes | No |
| Export capacity data | Yes | Yes | No | No | No |

### Operation calendars

| Privilege | WFM Administrator | WFM Forecaster | WFM Scheduler | WFM Intraday Analyst | WFM Service Rep |
| --- | --- | --- | --- | --- | --- |
| Create, edit, and delete operation calendars | Yes | Yes | No | No | No |
| Read operation calendars | Yes | Yes | Yes | Yes | No |

### Shift plans and scheduling

| Privilege | WFM Administrator | WFM Forecaster | WFM Scheduler | WFM Intraday Analyst | WFM Service Rep |
| --- | --- | --- | --- | --- | --- |
| Create, edit, and delete shift plans | Yes | No | Yes | No | No |
| Read shift plans | Yes | No | Yes | Yes | Yes |
| Copy a shift plan | Yes | No | Yes | No | No |
| Run auto schedule | Yes | No | Yes | No | No |
| Configure break distribution | Yes | No | Yes | No | No |
| Publish schedules | Yes | No | Yes | No | No |
| Add bookings for single or multiple representatives | Yes | No | Yes | No | No |
| Modify bookings, including drag-and-drop changes | Yes | No | Yes | No | No |
| Delete bookings for single or multiple representatives | Yes | No | Yes | No | No |

### Requests

| Privilege | WFM Administrator | WFM Forecaster | WFM Scheduler | WFM Intraday Analyst | WFM Service Rep |
| --- | --- | --- | --- | --- | --- |
| Create, edit, and delete a shift bid | Yes | No | No | No | Yes |
| Read shift bids | Yes | No | Yes | No | Yes |
| Approve or decline a shift bid | Yes | No | Yes | No | No |
| Create, edit, and delete a shift swap | Yes | No | No | No | Yes |
| Read shift swaps | Yes | No | Yes | No | Yes |
| Accept or reject a shift swap | Yes | No | No | No | Yes |
| Raise a swap offer | Yes | No | No | No | Yes |
| Accept a swap offer | Yes | No | No | No | No |
| Create, edit, read, and delete a time-off request | Yes | No | Yes | No | Yes |
| Approve or decline a time-off request | Yes | No | Yes | No | No |
| View request management | Yes | No | Yes | No | Yes |

### Monitoring and reporting

| Privilege | WFM Administrator | WFM Forecaster | WFM Scheduler | WFM Intraday Analyst | WFM Service Rep |
| --- | --- | --- | --- | --- | --- |
| View the adherence tracker | Yes | No | No | Yes | No |
| View the adherence history report | Yes | No | No | Yes | No |
| Export the adherence history report | Yes | No | No | Yes | No |
| View the intraday performance report, real-time view | Yes | No | No | Yes | No |
| Export the intraday performance report, real-time view | Yes | No | No | Yes | No |
| View the intraday performance report, historical view | Yes | No | No | Yes | No |
| Export the intraday performance report, historical view | Yes | No | No | Yes | No |

### Representative self-service

| Privilege | WFM Administrator | WFM Forecaster | WFM Scheduler | WFM Intraday Analyst | WFM Service Rep |
| --- | --- | --- | --- | --- | --- |
| View shift bookings | Yes | No | Yes | No | Yes |
| View shift summary | Yes | No | No | No | Yes |
| View the schedule calendar | Yes | No | No | No | Yes |

### Administration

Only the WFM Administrator role can open **Admin settings** and configure workforce management. This role can:

- Manage users.
- Turn volume forecasting, capacity planning, schedule management, shift-based routing, shift rotations, representative calendar, bidding, and swapping on or off.
- Create, edit, and delete shift activity types and time-off request types.
- Turn adherence historical analytics and intraday performance reporting on or off.
- Manage workforce alerts.
- Allow representatives to accept their schedules.
- Manage the shift swap expiry period.

## Choose a role

Use the following table to match a user's responsibilities to a role.

| If the user needs to | Assign this role |
| --- | --- |
| Configure workforce management or perform all workforce management functions | WFM Administrator |
| Predict demand and translate it into staffing requirements | WFM Forecaster |
| Build shift plans, assign representatives, and approve their requests | WFM Scheduler |
| Monitor adherence and service performance throughout the day | WFM Intraday Analyst |
| View their own schedule and submit their own bids, swaps, and time-off requests | WFM Service Rep |

The WFM Scheduler and WFM Intraday Analyst roles can read forecast scenarios and capacity plans but can't change them. This read-only access lets schedulers and analysts review the plans they work against without granting planning privileges.

A user can have multiple roles. For example, assign WFM Forecaster and WFM Scheduler to a planner who also builds schedules.

## Assign a role to a user

1. Sign in to the Power Platform admin center.
1. In the site map, select **Environments**, and then select your environment.
1. Select **Settings** > **Users + permissions** > **Users**.
1. Select the user to update, and then select **Manage security roles**.
1. Select the workforce management role to assign.
1. Select **Save**.

The Workforce Engagement Management app appears in the user's list of apps the next time they sign in.

## How role assignment affects app visibility

To access the app, users must have a workforce management role listed in this article or a [quality management role](workforce-management-quality-management-security-roles.md). Users without one of these roles don't have the app in their list of apps.

Within the app, the site map reflects the user's assigned roles. A user assigned only WFM Service Rep can access their schedule calendar, shift summary, and requests, but not forecasting or scheduling nodes.

Learn more in [Workforce Engagement Management app](../use/workforce-management-wem-app-overview.md).

## Related information

- [Workforce Engagement Management app](../use/workforce-management-wem-app-overview.md)
- [Quality management security roles](workforce-management-quality-management-security-roles.md)
- [Install the Workforce Management for Customer Service package](workforce-management-package-installation.md)
- [Overview of workforce management](/dynamics365/customer-service/use/workforce-management-overview)
