---
title: Capacity metrics in Contact Center historical analytics
description: Explore capacity metric definitions and DAX measures for Shared Analytics Platform in Dynamics 365 Contact Center, including availability and utilization.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---
# Capacity metrics in Contact Center historical analytics

Use capacity metrics to review service representative capacity over time. Time-weighted values show total capacity, available capacity, capacity in use, blocked assignment time, and capacity-state changes.

Use capacity metrics to answer workforce planning and utilization questions such as:

- How much total and available capacity was present during each reporting window?
- How much capacity was in use, and what percentage of total capacity did it represent?
- When and for how long was assignment blocked because capacity was unavailable?
- How often did capacity state change?
- Is the capacity profile unit based?

## Metrics

All metrics use `AggAgentCapacity`, sourced from `FactAgentCapacityHistory` with `DimCapacityProfile` and agent and business unit dimensions. Each row represents one agent, capacity profile, 30-minute UTC window, and business unit.

### Total capacity units

Measures the time-weighted average maximum capacity in a 30-minute window. Use it to assess capacity by agent and capacity profile.
<br>

- **Appears on:** Agent capacity and custom reports.
- **Calculation:** `Time-weighted SUM(EffectiveMaxUnits * duration) / SUM(duration).`
- **Source:** `AggAgentCapacity`. `EffectiveMaxUnits` uses `COALESCE(agent_override, history.msdyn_defaultmaxunits)`.
- **Related metrics:** [Available capacity units](#available-capacity-units), [In-use capacity](#in-use-capacity), [Capacity utilization %](#capacity-utilization-).

### Available capacity units

Measures the time-weighted average available capacity units in a 30-minute window. Use it to assess remaining capacity.
<br>

- **Appears on:** Agent capacity and custom reports.
- **Calculation:** `Time-weighted SUM(AvailableCapacityUnits * duration) / SUM(duration).`
- **Source:** `AggAgentCapacity`.
- **Related metrics:** [Total capacity units](#total-capacity-units), [In-use capacity](#in-use-capacity), [Capacity utilization %](#capacity-utilization-).

### Blocked assignment duration

Totals the time assignment was blocked by capacity constraints. Use it to identify periods when unavailable capacity prevented work assignments.
<br>

- **Appears on:** Agent capacity and custom reports.
- **Calculation:** `SUM(AggAgentCapacity[BlockedAssignmentDurationInSeconds]).`
- **Source:** `AggAgentCapacity`.
- **Related metrics:** [Blocked assignment time](#blocked-assignment-time), [Capacity utilization %](#capacity-utilization-).

### Blocked assignment time

Displays blocked assignment duration as HH:MM:SS. Use it when you need a readable duration.
<br>

- **Appears on:** Agent capacity and custom reports.
- **Calculation:** `Formats SUM(AggAgentCapacity[BlockedAssignmentDurationInSeconds]) as HH:MM:SS.`
- **Source:** `AggAgentCapacity`.
- **Related metrics:** [Blocked assignment duration](#blocked-assignment-duration), [Capacity utilization %](#capacity-utilization-).

### Capacity utilization %

Shows the percentage of total capacity in use. Use it to assess capacity consumption. The calculation returns blank unless total capacity is greater than zero.
<br>

- **Appears on:** Agent capacity and custom reports.
- **Calculation:** `VAR TotalCap = SUM(AggAgentCapacity[TotalCapacityUnits]); VAR AvailCap = SUM(AggAgentCapacity[AvailableCapacityUnits]); RETURN IF(TotalCap > 0, 1 - DIVIDE(AvailCap, TotalCap, 0), BLANK()).`
- **Source:** `AggAgentCapacity`.
- **Related metrics:** [Total capacity units](#total-capacity-units), [Available capacity units](#available-capacity-units), [In-use capacity](#in-use-capacity).

### In-use capacity

The difference between total capacity units and available capacity units. Use this metric to understand current capacity consumption.
<br>

- **Appears on:** Agent capacity and custom reports.
- **Calculation:** `SUM(AggAgentCapacity[TotalCapacityUnits]) - SUM(AggAgentCapacity[AvailableCapacityUnits]).`
- **Source:** `AggAgentCapacity`.
- **Related metrics:** [Capacity utilization %](#capacity-utilization-), [Total capacity units](#total-capacity-units), [Available capacity units](#available-capacity-units).

### Capacity update count

Counts capacity update events in a 30-minute window. Use it to assess how often capacity state changed.
<br>

- **Appears on:** Agent capacity and custom reports.
- **Calculation:** `COUNT(*) or SUM(AggAgentCapacity[CapacityUpdateCount]) depending on model exposure.`
- **Source:** `AggAgentCapacity`.
- **Related metrics:** [Total capacity units](#total-capacity-units), [Available capacity units](#available-capacity-units).

### Is unit based

A true-or-false field that identifies whether the capacity profile is unit based. Use it to filter or group capacity results by profile type.
<br>

- **Appears on:** Agent capacity and custom reports.
- **Calculation:** No calculation is needed. Use the `AggAgentCapacity[IsUnitBased]` column to filter or group results.
- **Source:** `AggAgentCapacity`.
- **Related metrics:** [Total capacity units](#total-capacity-units), [Available capacity units](#available-capacity-units).
