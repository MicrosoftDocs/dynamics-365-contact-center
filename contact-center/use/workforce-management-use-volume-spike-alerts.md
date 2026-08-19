---
title: Use workforce alerts for volume spikes (preview)
description: Learn how to enable, create, evaluate, and manage volume spike alerts for workforce management in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 08/19/2026
ms.topic: how-to
ms.custom:
  - bap-template
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
---

# Use workforce alerts for volume spikes (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

Use workforce alerts to notify supervisors when conversation volume stays above forecast for a specified number of intervals.

Contact center demand doesn't always match the forecast. When conversation volume stays above forecast, service levels can decline before supervisors know that a queue needs attention.

A volume spike alert monitors real-time conversation volume for the queues in a shift plan. It compares actual volume with the linked forecast plan for the same interval and sends an in-app notification when the configured threshold and duration are met.

The process works as follows:

- An administrator enables workforce alerts in Copilot Service admin center.
- A supervisor creates a volume spike alert in Copilot Service workspace and specifies the shift plan, deviation threshold, duration, expiration date, and notification recipients.
- A background monitor evaluates the queues in the selected shift plan on a recurring schedule.
- When the alert conditions are met, recipients get an in-app notification and can open a detailed interval-by-interval comparison of forecast and actual volume.

Volume spike alerts are informational. They don't reroute conversations, change staffing, or modify the published schedule.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

Before you create a volume spike alert, make sure that you meet the following requirements:
- Configure forecasting and scheduling, and publish a shift plan that has an associated capacity plan and forecast. You can't create an alert for a manually created shift plan that doesn't have a linked capacity plan.
- Include the queues that you want to monitor in the capacity plan that's linked to the shift plan.
- Ensure real-time conversation data is available for those queues.

## Enable workforce alerts

Workforce alerts are turned off by default. An administrator must enable the feature before supervisors can access the **Workforce alerts** page in Copilot Service workspace.

1. In the Copilot Service admin center site map, under **Operations**, select **Workforce management**.
1. On the **Workforce management** page, expand **Intraday management**.
1. Next to **Workforce alerts (preview)**, select **Manage**.
1. Set **Enable workforce alerts** to **On**.

The setting is available to supervisors after they refresh Copilot Service workspace.

If you turn off workforce alerts, existing alert definitions are retained. However, supervisors can't create or edit alerts, and no new notifications are sent.

## Create a volume spike alert

Supervisors create and manage alerts in Copilot Service workspace.

1. In the Copilot Service workspace site map, select **Workforce alerts**.
1. Select **New**, and then select **Volume spike alert**.
1. In the **Create an alert** pane, enter the alert details, and then select **Save**.

| Field | Description |
|---|---|
| **Workforce alert type** | Read-only. Identifies the alert type. For this alert, the value is **Volume spike**. |
| **Alert name** | Required. Enter a unique, descriptive name. The name appears in notifications and alert details. |
| **Shift plan** | Required. Select the shift plan that contains the queues to monitor. The system evaluates all queues in the selected plan. |
| **Linked forecast plan** | Read-only. The linked forecast plan is populated from the selected shift plan and provides the comparison baseline. |
| **Above forecast (%)** | Required. Enter the percentage by which actual volume must exceed forecast volume for an interval to meet the threshold. The default value is 5 percent. |
| **For duration (intervals)** | Required. Enter the number of consecutive intervals that must meet the threshold before the system raises an alert. The default value is 1. An interval can be 15, 30, or 60 minutes, based on the linked forecast. |
| **Alert expiration date** | Required. Enter the date after which the system no longer evaluates the alert. The default value is the shift plan end date. |
| **Notification recipients** | Required. Select one or more users to receive an in-app notification when the system raises the alert. |

> [!NOTE]
> An interval is the smallest time unit in the linked forecast plan. The **For duration (intervals)** value represents consecutive intervals. For example, if the forecast uses 15-minute intervals, a duration of 2 means that the deviation must continue for 30 minutes.

### Example

A supervisor wants to know when the billing queue is significantly busier than planned without receiving an alert for every small fluctuation. The supervisor configures the alert as follows:

- **Above forecast (%):** 25
- **For duration (intervals):** 2

With a 15-minute forecast interval, an alert isn't raised if volume is 30 percent above forecast for one interval and then returns to normal. An alert is raised if volume remains at least 25 percent above forecast for two consecutive intervals.

## How volume spike alerts are evaluated

A background monitor runs every five minutes. For each active, unexpired alert, the monitor completes the following actions:

1. Identifies the queues in the shift plan that's referenced by the alert.
1. Retrieves actual conversation volume for each recently completed interval for those queues.
1. Retrieves forecast volume for the corresponding interval from the linked forecast plan.
1. Calculates the percentage above forecast. The interval meets the threshold when the deviation is greater than or equal to the **Above forecast (%)** value.
1. Sends an in-app notification to each recipient when the number of consecutive intervals that meet the threshold reaches the **For duration (intervals)** value.

Consider the following evaluation behavior:

- A notification can arrive up to one monitor cycle after the interval that triggered it. Alerts support intraday awareness and response, not subminute detection.
- Intervals must be consecutive. An interval that falls below the threshold restarts the count.
- Evaluation stops after the alert expiration date or when the alert is inactive.
- Only queues in the selected shift plan are evaluated. If you add a queue to the shift plan, the monitor includes it in a subsequent run.

## View and respond to an alert

When an alert is raised, each notification recipient gets an in-app notification in Copilot Service workspace. Select the notification or the **Workforce Alert** icon on the workspace side panel to open the alert details.

The alert details help you determine whether the spike is significant, how large it is, and how long it has continued.

| Element | Description |
|---|---|
| **Title** | The queue that triggered the alert, followed by the alert name. |
| **Alert type** | The type of alert. For this alert, the value is **Volume spike alert**. |
| **Status** | The current alert state, such as **Active** or **Resolved**. |
| **Summary** | A description of the detected condition, including the number of consecutive intervals. |
| **Detected** | The date and time when the monitor detected the condition. |
| **Current volume** | The actual conversation volume in the most recent evaluated interval and the forecast volume for the same interval. |
| **Spike size** | The percentage by which actual volume exceeded forecast volume in the most recent evaluated interval. |
| **Interval breakdown** | A table with the interval start time, forecast volume, actual volume, percentage above forecast, and whether the threshold was met. |

An alert is resolved when volume remains below the configured deviation threshold for the configured number of intervals.

Use the interval breakdown to evaluate the trend. A deviation that increases across consecutive intervals might require an immediate response, such as offering overtime, moving customer service representatives from a lower-priority queue, deferring nonurgent offline work, or rescheduling training and coaching. A deviation that is leveling off might resolve without intervention.

> [!NOTE]
> When forecast volume is zero and conversations arrive, the deviation is reported as +100 percent. Low forecast volumes can produce large percentage deviations from small absolute differences. For low-volume queues, consider using a higher **Above forecast (%)** value or a longer duration to reduce unnecessary alerts.

## Manage existing alerts

The **Intraday volume spike alerts** view lists created alerts and shows **Alert name**, **Shift plan**, and **Above forecast (%)**. By default, the view shows active alerts.

1. To review or change an alert, select the alert name.
1. To stop notifications without deleting the alert definition, deactivate the alert or set its expiration date to a past date.
1. To find alerts that are no longer running, clear or change the **Status** filter.

Review alert configurations after you change a shift plan or its linked forecast plan. The selected plan determines both the evaluated queues and the forecast baseline.

## Best practices

- Start with conservative thresholds. Use a higher deviation percentage and a duration of two or more intervals, and then adjust the values based on queue behavior.
- Create a separate alert for each operational scenario. For example, use a dedicated alert and expiration date for a peak-season campaign instead of using one permanent alert with compromise thresholds.
- Keep the recipient list focused. Notify people who can respond to staffing or routing needs for the affected queues.
- Set expiration dates for temporary alerts so that they don't continue after the related event.
- Review thresholds as forecast accuracy improves. More accurate forecasts might support a lower deviation percentage.

## Known limitations in preview

- Alerts are delivered only as in-app notifications in Copilot Service workspace. Recipients must be signed in to view them.
- The monitor evaluates alerts every five minutes, so detection isn't immediate.
- Volume spike alerts evaluate conversation volume only. They don't evaluate changes in handle time or staffing.

## Related information

- [Create and manage forecast scenarios](workforce-management-forecast-scenarios.md)  
- [Create and manage shift plans](workforce-management-shift-plan.md)  
- [Use the adherence history report](workforce-management-use-adherence-history-report.md)  
- [Use the adherence tracker](workforce-management-adherence-tracker.md)
