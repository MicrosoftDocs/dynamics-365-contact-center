---
title: Use the adherence history report
description: Review historical adherence data to understand how customer service representative schedules align with actual work activity.
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.date: 06/15/2026
ms.topic: how-to
ms.custom: bap-template
---

# Use the adherence history report

The adherence history report shows how customer service representative schedules align with actual work activity over time. Supervisors can use the report to review historical adherence, identify trends, and understand when and why representatives were out of adherence during their shifts.

Use this report to analyze adherence data for individuals and teams, and to support staffing, scheduling, and coaching decisions.

## Prerequisites

- Your administrator installed the Workforce Management for Customer Service package in the Power Platform admin center.
- Your administrator enabled Workforce Management in Copilot Service admin center.

## View the adherence history report

1. In the **Copilot Service workspace** site map, select **Adherence historical analytics** under **Workforce management**.
1. Set the date range, and then select one or more customer service representatives.
1. Select **Apply**.

The report updates to display adherence data based on your selections.

## Use report filters

Use the filters at the top of the report to analyze adherence data for specific representatives, shift plans, time zones, and date ranges.

| Filter | Description |
|----------|----------|
| Duration | Sets the reporting period. Adjust the start and end dates or use the slider to change the range. The report supports up to two years of historical data, and the window can span any range within the last two years. |
| Time Zone | Aligns scheduled and actual times to a single time zone for consistent reporting across regions. |
| Shift Plan | Displays representatives associated with a specific shift plan. |
| Agent | Displays data for a specific representative or the entire team. |

> [!NOTE]
> The report supports up to two years of historical data. Data older than two years isn't available.

## Review summary metrics

The summary cards display adherence metrics for all representatives included in the current filter selection.

| Metric | Description |
|----------|----------|
| Adherence % | The percentage of tracked scheduled time during which the representative's actual state matched the scheduled state. This metric represents how closely the team followed its schedule. |
| Time Out of Adherence | The total tracked scheduled time during which the representative's actual state didn't match the scheduled state after tolerance is applied. Displayed as hrs:min:sec. |
| Total Schedule Time | The total duration of scheduled activities in the selected reporting period. |

## Review representative metrics

The representative grid provides adherence details for each representative included in the selected reporting period. Supervisors can use this information to compare adherence trends and identify coaching or scheduling opportunities.

| Column | Description |
|----------|----------|
| Agent | The customer service representative. |
| Adherence % | The representative's adherence percentage for the selected period. |
| Total Schedule Time | The total scheduled duration assigned to the representative. |
| Time Out of Adherence | The total tracked time during which the representative's actual state didn't match the scheduled state after tolerance is applied. |
| Total Time Worked | The total time the representative was signed in and working during the selected period, regardless of what was scheduled. Comparing this value with Total Schedule Time highlights overcoverage or undercoverage. |

> [!NOTE]
> If a representative has scheduled time but doesn't sign in during the selected period, the report displays **0.00%** adherence and **0** time worked.

## Review activity summary data

The Activity summary grid displays adherence details for each tracked interval and shows how actual activities compared to scheduled activities.

| Column | Description |
|----------|----------|
| Agent | The representative associated with the interval. |
| Actual activity | The representative's actual presence state during the interval, such as **Available**, **Away**, or **Offline**. |
| Scheduled activity | The activity scheduled for the interval, such as a call, conversation, training session, or break. |
| Start time | The time the interval began. |
| End time | The time the interval ended. |
| Total duration | The length of the interval. |
| Adherence status | Indicates whether the interval was **In Adherence**, **Out of Adherence**, or **Not Tracked**. |

## Understand adherence status values

| Status | Meaning |
|----------|----------|
| In Adherence | The actual state matched the expected state, or the deviation was within the configured tolerance. This time counts toward Adherence %.|
| Out of Adherence | The actual state didn't match the expected state and exceeded the configured tolerance. This time counts toward **Time out of Adherence** and lowers **Adherence %**.|
| Not Tracked | The scheduled activity isn't configured for adherence tracking and is excluded from calculations. |

## Understand how adherence is calculated

Adherence measures whether a representative's actual activity matched the scheduled activity during each tracked interval. Three factors affect the calculation.

### Scheduled state versus actual state

Each scheduled activity has an expected state. The system continuously captures the representative's actual presence state and compares it to the expected state.

### User state mapping

Scheduled activities and presence states don't necessarily use the same values. User state mapping defines which presence states satisfy each scheduled activity. For example, both **Available** and **Busy** might satisfy a scheduled call activity, while **Away** might satisfy a scheduled break.

### Tolerance

Tolerance provides a grace period that absorbs minor timing deviations. For example, if a scheduled activity has a five-minute tolerance and a representative signs in four minutes late, the interval remains in adherence. If they sign in 10 minutes late, they're considered out of adherence for five of those minutes.

### Tracked versus not tracked activities

Activities that you configure as **Not Tracked** are excluded from adherence calculations. Representatives don't get rewards or penalties for time associated with these activities.

After you apply state mapping and tolerance, the system calculates adherence metrics as follows:

```text
Tracked Schedule Time = Total Schedule Time - Not Tracked Time

Time In Adherence = Tracked Schedule Time - Time Out of Adherence

Adherence % =
(Time In Adherence / Tracked Schedule Time) × 100
```

## Example

The following example demonstrates how the system calculates adherence for a representative working a single shift.

### Setup

- Representative: Maria
- Shift: 9:00 AM–5:00 PM (480 minutes)
- Call activity tolerance: 5 minutes

### User state mapping

| Activity | Allowed presence state | Tolerance | Tracked |
|----------|----------|----------|----------|
| Call | Available, Busy | 5 min | Yes |
| Conversation | Available, Busy | None | Yes |
| Break and Lunch | Away | None | Yes |
| Training | Away | N/A | No |

### Activity log

The following example shows how adherence is calculated for a single shift. Each row represents a continuous interval with a single adherence status. When a deviation occurs, the scheduled activity splits into separate intervals so the report can accurately track adherence time.

| Scheduled activity | Time block | Expected state | Actual state | Status | In Adherence (min) | Out of Adherence (min) | Comments |
|----------|----------|----------|----------|----------|----------|----------|----------|
| Call | 9:00 to 9:05 | Available | Offline | In Adherence | 5 | 0 | First five minutes absorbed by the configured call tolerance. |
| Call | 9:05 to 9:10 | Available | Offline | Out of Adherence | 0 | 5 | Sign-in delay exceeded the configured tolerance. |
| Call | 9:10 to 11:00 | Available | Available | In Adherence | 110 | 0 | Representative handled calls as scheduled. |
| Break | 11:00 to 11:15 | Away | Away | In Adherence | 15 | 0 | Break occurred as scheduled. |
| Conversation | 11:15 to 12:00 | Available | Available | In Adherence | 45 | 0 | Representative handled conversations as scheduled. |
| Conversation | 12:00 to 12:25 | Available | Away | Out of Adherence | 0 | 25 | Unscheduled away time. |
| Conversation | 12:25 to 1:00 | Available | Available | In Adherence | 35 | 0 | Representative returned to scheduled work. |
| Lunch | 1:00 to 1:30 | Away | Away | In Adherence | 30 | 0 | Lunch occurred as scheduled. |
| Call | 1:30 to 3:30 | Available | Available | In Adherence | 120 | 0 | Representative handled calls as scheduled. |
| Training | 3:30 to 4:00 | Away | Away | Not Tracked | 0 | 0 | Training is excluded from adherence calculations. |
| Call | 4:00 to 4:40 | Available | Available | In Adherence | 40 | 0 | Representative handled calls as scheduled. |
| Call | 4:40 to 4:45 | Available | Offline | In Adherence | 5 | 0 | First five minutes absorbed by the configured call tolerance. |
| Call | 4:45 to 5:00 | Available | Offline | Out of Adherence | 0 | 15 | Sign-out occurred outside the configured tolerance. |

### Roll up the totals

The report aggregates individual intervals into summary metrics. In this example:

```text
Time In Adherence = 405 min

Time Out of Adherence = 45 min

Not Tracked Time = 30 min
```

### Calculate each metric

**Total Schedule Time**

```text
480 min = 8 hrs 00 min
```

**Tracked Schedule Time**

```text
480 - 30 = 450 min
```

**Time Out of Adherence**

```text
45 min = 00 hrs 45 min 00 sec
```

**Time In Adherence**

```text
450 - 45 = 405 min = 6 hrs 45 min
```

**Adherence Percentage**

```text
(450 - 45) / 450 × 100

= 405 / 450 × 100

= 90.00%
```

### Results

| Metric | Value |
|----------|----------|
| Total Schedule Time | 8 hrs 00 min |
| Time In Adherence | 6 hrs 45 min |
| Time Out of Adherence | 0 hrs 45 min 00 sec |
| Adherence % | 90.00% |

The 45 minutes out of adherence comes from three deviations. The late sign-in and early sign-out deviations are both measured against the five-minute tolerance configured for the **Call** activity. As a result, only the time beyond the tolerance counts as out of adherence (5 minutes and 15 minutes, respectively). The unscheduled away time during the **Conversation** activity has no configured tolerance, so all 25 minutes count as out of adherence.

The 30 minutes of training doesn't affect the adherence score because the activity is configured as **Not Tracked**.

The report records each adherence status change as a separate interval. This approach ensures that the values shown in the **Activity summary** grid align with the summary metrics and provides a detailed record of how the adherence percentage was calculated.

### Related information

[Use the adherence tracker](workforce-management-adherence-tracker.md)  
[Configure shift activity types](../administer/workforce-management-shift-activity-types.md)  
[Enable adherence historical analytics](../administer/workforce-management-enable-adherence-historical-analytics.md)

