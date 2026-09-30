---
title: Use the intraday performance report (preview)
description: Learn how to compare planned and actual intraday performance by interval, channel, and queue in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.topic: how-to
ms.date: 09/29/2026
ms.custom:
  - bap-template
---

# Use the intraday performance report (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

The intraday performance report shows how volume, average handle time, service level, and staffing are tracking against plan throughout the day. Supervisors and workforce managers can use the report to compare planned and actual performance interval by interval, broken out by channel and queue, and determine whether the representatives scheduled for each interval are enough to meet the service level target.

Use this report to find coverage gaps while there's still time to act on them, decide whether to move breaks, extend shifts, or offer voluntary time off, and review after the fact how closely the day matched the plan.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- Your administrator installed the Workforce Management for Customer Service package in the Power Platform admin center.
- Your administrator enabled **Intraday Performance** under **Workforce Management** in Copilot Service admin center.
- A shift plan with published shift bookings exists, with an associated capacity plan and forecast scenario.

## View the intraday performance report

1. In the Copilot Service workspace site map, select **Intraday Performance** under **Workforce management**.
1. Select a **Planning group**, and then select a **Shift Plan**.
1. Select the **Channels** and **Queues** that you want to review.
1. Use the date box or the arrows to select the day. The current day opens by default and updates in near real time.

The report displays a row for each interval in the shift, with planned and actual values side by side. The report uses the interval length configured for the selected planning group.

> [!NOTE]
> - Use the date picker to navigate to earlier dates and review past performance, but only for dates from the enablement of the intraday performance report. Dates before enablement aren't supported.
> - If there's no active planning group, the **Planning group** filter is hidden and you select the **Shift Plan** directly.

## Understand the report layout

The grid is organized into column groups. The first group summarizes staffing for the whole shift plan. Each remaining group covers one combination of a selected channel and a selected queue and is labeled **Channel - Queue**, such as **Live chat - Contoso Coffee Queue A**.

| Group | What it covers |
|---|---|
| **Overall Staffing** | Staffing for the shift plan as a whole. Required representatives are rolled up across every channel and queue combination and compared against the representatives scheduled. This is the group to read first when you want to know whether the interval is covered. |
| **Channel - Queue** | Demand and service performance for one channel and queue combination: forecast and actual volume, planned and actual handle time, service level, and speed of answer, plus the required representatives that this combination contributes to the overall total. |

Selecting two channels and two queues produces four channel and queue groups. Use the horizontal scroll bar under the grid to move across them, and the column count control to change how many columns display at a time.

### Interval rows

Each row is one interval, and intervals don't overlap. On the current day, the interval in progress is highlighted and marked with an indicator so that you can find it without scrolling.

| Row state | Description |
|---|---|
| **Completed interval** | Planned and actual values are both populated. |
| **Interval in progress** | The row is highlighted. Actual values reflect the records handled so far and continue to change until the interval closes. |
| **Future interval** | Planned values and required representatives are populated. Actual columns are blank because no records have arrived yet. |

## Use report controls

Use the controls at the top of the page to set the reporting context and control how much detail the grid displays.

| Control | Description |
|---|---|
| **Date** | Sets the day that the report covers. Select the date box to open the calendar, or use the arrows to move backward or forward by one day. |
| **Real-time indicator** | Shows that the report is displaying the current day and refreshing automatically. When you navigate to a past date, the report shows historical values for that day. |
| **Planning group** | Scopes the report to a single planning group. The filter is hidden when there's no active planning group. |
| **Shift Plan** | Sets the source data for the report. The selected shift plan determines the capacity plan that supplies the staffing parameters, the forecast scenario that supplies predicted volume and the list of available queues, and the published shift bookings that supply scheduled staffing. |
| **Channels** | Selects which channels to display. Each selected channel is combined with each selected queue to produce a column group. |
| **Queues** | Selects which of the queues associated with the forecast scenario to display. Deselecting a queue removes its column group and removes its contribution from the **Overall Staffing** totals. |
| **Columns** | Sets how many metric columns display in the grid at a time. Reduce the column count to focus on a smaller set of metrics. |
| **Updated** | Shows the time of the most recent data refresh. |
| **Refresh** | Retrieves the latest values without reloading the page. |
| **Export** | Exports the current grid, including your filter selections, to a Microsoft Excel workbook for offline analysis or distribution. |

## Understand where the report data comes from

The report resolves its data through a chain of related records. Understanding this chain explains why some columns change when you change the shift plan and others don't.

**Planning group → Shift plan → Capacity plan → Forecast scenario → Queues (x selected channels)**

| Record | What it supplies to the report |
|---|---|
| **Planning group** | Scopes the report and defines the interval length used for the grid rows. |
| **Shift plan** | Supplies the published shift bookings that produce **Reps Scheduled**, and points to the capacity plan that supplies everything else. |
| **Capacity plan** | Supplies the planning parameters used to calculate the requirement: average handle time, service level target, target time to answer, maximum occupancy, and shrinkage percentage. |
| **Forecast scenario** | Supplies the predicted volume for each interval, the record type being forecast, and the list of queues that the volume is forecast for. |
| **Queues and channels** | Determine which records count toward the actual metrics and which column groups appear in the grid. |

## Review the Overall Staffing columns

The **Overall Staffing** group answers a single question: Is this interval covered? It compares the total representatives required across every displayed channel and queue combination against the representatives actually scheduled.

| Column | Description |
|---|---|
| **Req. Reps (including shrinkage)** | The total number of representatives required for the interval across all displayed channel and queue combinations, after applying the shrinkage percentage configured in the capacity plan. **Over/Under** is calculated against this value. |
| **Req. Reps (excluding shrinkage)** | The same total before shrinkage is applied. Compare the two values to see how much of the requirement is attributable to shrinkage. |
| **Reps Scheduled** | The number of representatives who have a published shift booking covering the interval in the selected shift plan. |
| **Over/Under** | The difference between the representatives scheduled and the representatives required, including shrinkage. See [Understand the Over/Under indicator](#understand-the-overunder-indicator). |

## Review the channel and queue columns

Each channel and queue group describes demand and service performance for one combination. Planned columns come from the capacity plan, forecast volume comes from the forecast scenario, and actual columns come from operational records.

| Column | Description |
|---|---|
| **Fcst. Vol.** | The number of records that the forecast scenario predicts will arrive in this queue and channel during the interval. This column is the only genuine forecast column; the planned columns that follow are configured values, not predictions. |
| **Act. Vol.** | The number of records that actually arrived during the interval. Blank for intervals that haven't started. |
| **Planned AHT** | The average handle time configured in the capacity plan and used to calculate the staffing requirement for the interval. |
| **Act. AHT** | The average handle time actually recorded for the records handled in the interval. |
| **Planned SL %** | The service level target configured in the capacity plan, such as 75%. |
| **Act. SL %** | The percentage of records actually answered within the planned target time to answer. Compare this value with **Planned SL %** to see whether the interval met its service level target. |
| **Planned TTA** | The target time to answer that pairs with the service level target, shown in seconds. A value of 90 seconds with a service level of 75% means the plan is to answer 75 percent of records within 90 seconds. |
| **Act. TTA** | The average time that records waited before a representative picked them up. |
| **Planned Occupancy** | The maximum occupancy configured in the capacity plan as a ceiling for the interval. |
| **Req. Reps (including shrinkage)** | The representatives required for this channel and queue combination after shrinkage is applied. This value contributes to the **Overall Staffing** total. |
| **Req. Reps (excluding shrinkage)** | The representatives required for this combination before shrinkage is applied. |

> [!NOTE]
> - **Planned TTA**, **Act. TTA**, **Planned SL %**, and **Act. SL %** aren't available for case records.
> - Because the report breaks performance out per channel and queue, planned handle time is shown as configured for each combination rather than blended. You don't need to interpret a weighted average across queues.

## Understand the Over/Under indicator

The **Over/Under** column summarizes coverage for each interval in a single number.

**Over/Under = Reps Scheduled - Overall Req. Reps (including shrinkage)**

| Value | Meaning |
|---|---|
| **Negative** | Fewer representatives are scheduled than the interval requires. The interval is at risk of missing the service level target. |
| **Zero** | Scheduled coverage matches the requirement. |
| **Positive** | More representatives are scheduled than the interval requires. |
| **Dash** | There's no requirement for the interval, usually because it falls outside the hours the shift plan covers. |

Negative values display with a red indicator so that understaffed intervals are easy to scan for. A large negative value that repeats across consecutive intervals usually points to a schedule that doesn't match the shape of the forecast, rather than to a problem in a single interval.

## Understand how often data refreshes

Actual values and planning values refresh on different cadences because they come from different sources.

| Refresh frequency | Columns |
|---|---|
| **Every 10 seconds** | **Act. Vol.**, **Act. AHT**, **Act. SL %**, **Act. TTA** |
| **Every 5 minutes** | **Fcst. Vol.**, **Planned AHT**, **Planned SL %**, **Planned TTA**, **Planned Occupancy**, **Req. Reps (including shrinkage)**, **Req. Reps (excluding shrinkage)**, **Reps Scheduled**, **Over/Under** |

Select **Refresh** to retrieve the latest values immediately. The **Updated** timestamp shows when the data was last retrieved.

## Understand how actual metrics are calculated

The actual columns are calculated from operational records rather than from planning data. Each actual metric is scoped to one channel and queue combination, and each record is attributed to the interval in which it arrived in the queue.

### Sample data set

The following conversation records arrived in the **Live chat - Queue A** group during a single interval. The capacity plan for this combination sets **Planned AHT** to 4:00, **Planned SL %** to 80 percent, and **Planned TTA** to 20 seconds.

**Interval: 14:00 to 14:30**

| ID | Arrived | Wait time | Handle time | Outcome |
|---|---|---:|---:|---|
| R1 | 14:02:00 | 8s | 3:40 | Handled |
| R2 | 14:05:00 | 15s | 4:20 | Handled |
| R3 | 14:08:00 | 4s | 5:10 | Handled |
| R4 | 14:12:00 | 45s | — | Abandoned |
| R5 | 14:16:00 | 30s | 2:50 | Handled |
| R6 | 14:21:00 | 10s | 6:00 | Handled |
| R7 | 14:25:00 | 20s | 4:00 | Handled |
| R8 | 14:28:00 | 53s | 3:20 | Handled |

For a conversation record, wait time is the interval between arrival in the queue and the moment a representative answered. If the shift plan instead resolved to a case forecast scenario, volume and handle time would be calculated the same way, but arrival would be the moment the case entered the queue.

### Act. Vol.

**Act. Vol.** counts every record that arrives in the interval for this channel and queue combination. It includes abandoned records because the record arrives and represents demand on the queue even if no representative handles it.

**Act. Vol. = all records that arrive in the interval = 8**

Key things to note:

- The system attributes records by arrival time, not by the time they're answered or completed. A record that arrives at 14:28 and finishes at 14:35 still counts toward the 14:00 interval.
- The value is scoped to one channel and queue combination. To determine total demand across the shift plan, add the **Act. Vol.** values across the displayed groups.
- Compare **Act. Vol.** with **Fcst. Vol.** to determine forecast accuracy. A persistent gap in the same direction across many intervals suggests the forecast scenario needs revisiting, not that the schedule was wrong.

### Act. AHT

**Act. AHT** is the average handle time across the records that were actually handled in the interval. Abandoned records have no handle time and are excluded from both the numerator and the denominator.

**Total handle time = 3:40 + 4:20 + 5:10 + 2:50 + 6:00 + 4:00 + 3:20**

**= 220 + 260 + 310 + 170 + 360 + 240 + 200 seconds**

**= 1,760 seconds**

**Act. AHT = 1,760 / 7 handled records**

**= 251 seconds**

**= 4:11**

Key things to note:

- The denominator is records handled, not records that arrived. In this example, the denominator is 7, not the **Act. Vol.** figure of 8.
- **Act. AHT** running above **Planned AHT** means the interval consumed more capacity than planned.

### Act. TTA

**Act. TTA** is the average time that records waited before a representative picked them up. Only answered records contribute, so abandoned records are excluded.

**Total wait time = 8 + 15 + 4 + 30 + 10 + 20 + 53 seconds**

**= 140 seconds**

**Act. TTA = 140 / 7 answered records**

**= 20 seconds**

### Act. SL %

**Act. SL %** is the percentage of records answered within **Planned TTA**. It's the metric to compare against **Planned SL %**, and it tells you whether the interval met its service level commitment.

Records answered within 20 seconds:

- R1 (8s)
- R2 (15s)
- R3 (4s)
- R6 (10s)
- R7 (20s)

**Act. SL % = 5 / 8 records that arrived**

**= 62.5%**

**= 63%**

Key things to note:

- The threshold comes from **Planned TTA**. Changing the target time to answer in the capacity plan changes **Act. SL %** for the same underlying records.
- The denominator includes abandoned records, so an abandon counts as a service level failure.
- This example shows why the average and the percentage disagree. **Act. TTA** is exactly 20 seconds, matching **Planned TTA** precisely, yet **Act. SL %** is 63 percent against an 80 percent target. Two slow records and one abandon pulled the percentage down while the average looked healthy.

## Related information

[Create and manage shift plans](workforce-management-shift-plan.md)  
[Create and manage capacity plans](workforce-management-capacity-planning.md)  
[Create and manage forecast scenarios](workforce-management-forecast-scenarios.md)  
[Use the adherence tracker](workforce-management-adherence-tracker.md)
