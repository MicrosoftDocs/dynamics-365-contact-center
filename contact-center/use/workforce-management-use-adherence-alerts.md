---
title: Use workforce alerts for adherence notifications (preview)
description: Learn how to enable, create, and manage adherence alerts for workforce management in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 09/21/2026
ms.topic: how-to
ms.custom:
  - bap-template
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
---

# Use workforce alerts for adherence notifications (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

Use workforce alerts to notify supervisors when customer service representatives (service representatives or representatives) are out of adherence with their published schedule.

An adherence alert compares the actual presence of representatives in selected shift plans with their scheduled activity for the current day. When representatives are out of adherence, the alert sends an in-app notification to the supervisors you specify and, optionally, to the affected representatives.

The process works as follows:

- An administrator enables workforce alerts in Copilot Service admin center.
- A supervisor creates an adherence alert in Copilot Service workspace and specifies the planning group, shift plans, linked activity types, expiration date, and notification recipients.
- A background monitor evaluates adherence against the current day's shifts in the selected plans on a recurring cycle.
- Recipients get an in-app notification and can open the alert details to identify affected representatives, their scheduled activity and presence, and how long they've been out of adherence.
- A supervisor addresses the deviation and marks the alert as resolved.

Adherence alerts are informational. They don't change presence, reroute conversations, or modify the published schedule.

## Prerequisites

Before you create an adherence alert, make sure that you meet the following requirements:

- Your administrator installed the Workforce Management for Customer Service package and enabled workforce management in Copilot Service admin center.
- You [created a shift plan and published bookings](workforce-management-shift-plan.md) for the representatives you want to monitor. Only published shift plans are available for selection.

## Enable workforce alerts

Workforce alerts are turned off by default. An administrator must enable the feature before supervisors can access the **Workforce alerts** page in Copilot Service workspace.

1. In the Copilot Service admin center site map, under **Operations**, select **Workforce management**.
1. On the **Workforce management** page, expand **Intraday management**.
1. Next to **Workforce alerts (preview)**, select **Manage**.
1. Set **Enable workforce alerts** to **On**.

Supervisors must refresh Copilot Service workspace for the setting to take effect. The same setting controls adherence alerts and [volume spike alerts](workforce-management-use-volume-spike-alerts.md).

If you turn off workforce alerts, existing alert definitions are retained. However, supervisors can't create or edit alerts, and no new notifications are sent.

## Create an adherence alert

Supervisors create and manage alerts in the Copilot Service workspace app.

1. In the Copilot Service workspace site map, select **Workforce alerts**.
1. Select **New**, and then select **Adherence alert**.
1. In the **Create an alert** pane, enter the following details, and then select **Save**.

| Field | Description |
|---|---|
| **Workforce alert type** | Read-only. Identifies the alert type. For this alert, the value is **Adherence**. |
| **Alert name** | Required. Enter a unique, descriptive name. The name appears in notifications and alert details. |
| **Planning group** | Select the planning group whose shift plans you want to monitor. The planning group determines which shift plans are available. For plans that aren't linked to a planning group, select **Not applicable**. |
| **Shift plans** | Required. Select one or more published shift plans. The system evaluates every representative scheduled in the selected plans. Selected plans appear as chips below the field, and you can remove a plan before you save. If you selected **Not applicable** as the planning group, all selected plans must use the same time zone. After you select the first plan, plans in other time zones are unavailable. |
| **Linked activity types** | Required. Select scheduled activity types to monitor, such as **Call** and **Chat**. Only activity types with **Track adherence** turned on are listed. The system evaluates adherence only during intervals when a representative is scheduled for a selected activity type. |
| **Alert expiration date** | Required. Enter the date after which the system no longer evaluates the alert. The date is interpreted in the shift plan's time zone, shown below the field. The default is the latest expiration date among the selected shift plans. You can choose an expiration from now through that latest expiration date, but not a past date. |
| **Notification recipients** | Required. Select one or more supervisors to receive an in-app notification when the system raises the alert. |
| **Notify service representatives** | Optional. Turn on this setting to also notify representatives who are out of adherence. When the schedule calendar is enabled, representatives can select **Check schedule** in their notification to open it. |

> [!NOTE]
> Use **Linked activity types** to focus alerts on activities where a deviation affects service levels. If you select only **Call** and **Chat**, the system doesn't raise alerts for representatives scheduled for breaks, training, or other offline activities.

## View and respond to an alert

When an alert is raised, each notification recipient gets an in-app notification in Copilot Service workspace. The notification identifies the shift plan and the number of representatives who are out of adherence.

1. Select **View Details** in the notification to open the alert details.
1. Review the following information to determine who is out of adherence and how long the deviation has continued.

| Element | Description |
|---|---|
| **Title** | The name of the alert that was raised. |
| **Shift plan** | The shift plan that the alert monitors. Select the link to open the plan. |
| **Alert type** | The type of alert. For this alert, the value is **Adherence alert**. |
| **Status** | The alert state: **Active** or **Resolved**. |
| **Adherence Tracker** | A link to the real-time adherence tracker, which provides the full team view and adherence timeline. |
| **Out of adherence** | The number of representatives who were out of adherence at the time of evaluation. |
| **As of** | The evaluation date and time, shown in the shift plan's time zone. |
| **Name** | The representative who is out of adherence. |
| **Scheduled activity** | The activity scheduled for the representative in the evaluated interval, such as **Chat**. |
| **Presence** | The representative's presence at the time of evaluation, such as **Available** or **Not logged in**. |
| **Out of adherence for** | How long the representative has been out of adherence, in hours, minutes, and seconds. |

Use **Presence** and **Out of adherence for** to prioritize your response. For a broader view of the team and its adherence timeline, select **Adherence Tracker**. Learn more about [using the adherence tracker](workforce-management-adherence-tracker.md).

> [!NOTE]
> Adherence alerts aren't instantaneous. A background monitor evaluates adherence on a recurring cycle, so notifications can arrive after the deviation begins. The **As of** timestamp identifies the last evaluation, not the current state. For the current state of the team, open **Adherence Tracker**.

## Resolve an alert

After you address the deviation, mark the alert as resolved so that other supervisors know it's handled.

1. In the alert details, select **More options (...)**, and then select **Mark resolved**.
1. In the **Resolve alert?** dialog, select **Confirm**.

The status changes to **Resolved**, and the alert details show who resolved it and when. Resolution applies to everyone who can access the alert, not only the person who resolved it.

## What service representatives experience

If **Notify service representatives** is on, an affected representative gets an **Activity alert** notification in their workspace. The notification shows the scheduled activity and prompts the representative to switch to it as soon as possible.

The representative can select **Check schedule** to open the **Schedule Calendar** tab. The calendar shows the day's scheduled activities, such as chat, call, and break blocks, in the shift plan's time zone. Representatives can also open the notification later from the notification panel to review or dismiss it.

> [!NOTE]
> **Check schedule** appears only when the schedule calendar is enabled in Copilot Service admin center. If the calendar isn't enabled, representatives still receive the activity alert but can't open their schedule from the notification.

## Manage existing alerts

The **Active Workforce alerts** view lists the alerts that you created and shows **Alert name** and **Created On**. By default, the view shows active alerts.

### Edit an alert

1. In the **Workforce alerts** list, select the alert name.
1. In the **Edit alert** pane, update the linked activity types, expiration date, notification recipients, or representative notification setting.

You can't change the planning group or shift plans after creating an alert. To monitor a different plan, create a new alert.

Review alert configurations after you republish a shift plan or change its activity types. The selected plans determine which representatives are evaluated.

### Find inactive alerts

To find alerts that are no longer running, clear or change the **Status** filter.

### Delete an alert

Deleting an alert permanently removes it.

1. Select the alert in the **Workforce alerts** list.
1. Select **Delete**.

## Related information

- [Use workforce alerts for volume spikes (preview)](workforce-management-use-volume-spike-alerts.md)
- [Use the adherence tracker](workforce-management-adherence-tracker.md)
- [Use the adherence history report](workforce-management-use-adherence-history-report.md)
- [Create and manage shift plans](workforce-management-shift-plan.md)
- [Create and manage forecast scenarios](workforce-management-forecast-scenarios.md)
