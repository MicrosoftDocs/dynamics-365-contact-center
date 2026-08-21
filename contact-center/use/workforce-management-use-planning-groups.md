---
title: Set up and manage planning groups
description: Learn how to create and manage planning groups, configure service objectives, and associate workforce management plans in Dynamics 365.
ms.date: 08/20/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.custom: bap-template
---

# Set up and manage planning groups

A planning group is the foundational planning unit in workforce management. It groups the queue and channel combinations that generate work for a team and defines the time zone and service objectives applied to that work. Forecasts, capacity plans, schedules, and performance reports created for the group inherit these settings. This shared configuration helps keep demand, staffing requirements, and published schedules aligned.

Use planning groups to:

- Define which queue and channel combinations drive demand for a team or business unit.
- Set service objectives used to calculate capacity and scheduling targets.
- Associate forecast scenarios, capacity plans, and shift plans so that they share the same demand scope.
- Scope intraday performance, adherence tracking, and historical reporting to the appropriate team and compare groups consistently.
- Forecast multiple queues as one unit, reducing the number of scenarios to maintain and helping prevent aggregation errors.

## Prerequisites

Before you create a planning group, make sure that:

- Your administrator installed the Workforce Management for Customer Service package in the Power Platform admin center.
- The channels and queues that you want to plan together are configured in Customer Service admin center or Copilot Service admin center.

## How planning groups work

A planning group defines the boundaries for demand, scheduling, and service objectives for the service representatives assigned to it.

Each planning group includes the following configuration:

- A name and description that identify the group.
- A time zone that governs scheduling and forecasting intervals.
- A demand scope that consists of one or more queue and channel combinations. These combinations determine which interaction volumes are included in the forecast.
- Service objectives that define the group’s performance targets.
- Associated shift plans, forecast scenarios, and capacity plans.

> [!IMPORTANT]
> A queue and channel combination can belong to only one planning group at a time. This restriction prevents the same interaction volume from being included in multiple forecasts.

## Benefits of planning groups

### Accurate forecasting

By scoping demand to specific queue and channel combinations, planning groups help ensure that staffing projections include only the interactions that the group is responsible for handling.

### Consistent service objectives

Service objectives configured for a planning group are available to the capacity plans associated with that group. Administrators can configure the objectives once and use them consistently across related planning activities.

### Supervisor-scoped visibility

Supervisors work with the service representatives, schedules, and requests within their authorized planning group. This scope keeps request management, adherence monitoring, and intraday oversight aligned with the appropriate team.

### Aligned workforce management artifacts

Shift plans, forecast scenarios, and capacity plans use configuration from their associated planning group. This shared context helps keep workforce planning artifacts aligned with the operational team they support.

## Create a planning group

1. In the site map of Copilot Service workspace, under **Workforce Management**, select **Planning Groups**. The **Active Planning Groups** page opens.
1. Select **New**.
1. On the **Details** card, enter the following information:

   - **Name**: Enter a name that identifies the group, such as `Voice Tier 1 - East`.
   - **Description**: Enter an optional description of the group’s scope or purpose.
   - **Time Zone**: Select the time zone that governs scheduling and forecasting intervals for the group. Associated shift plans, forecast scenarios, and capacity plans use this time zone.

1. In the **Demand Scope** view, select **Add Demand Scope**, and then add one or more queue and channel combinations:

   - **Queue**: Select a queue.
   - **Channel**: Select the channel that the queue handles, such as Voice, Chat, or Email.

   Repeat these steps for each queue and channel combination that drives demand for the group.

1. Select **Save**.

The planning group is available for association with shift plans, forecast scenarios, and capacity plans.

> [!NOTE]
> If a queue and channel combination is already associated with another planning group, you can’t add it to a second group. A validation error appears when you save the record.

## Configure service objectives

Service objectives define the performance targets for a planning group. Capacity planning uses these values to align staffing projections with your organization’s service commitments.

### Service objective settings

Service objectives include the following settings:

- **Service Level (%)**: The percentage of interactions that must be answered within the target answer time. For example, you might set a target of 80 percent within 20 seconds.
- **Target Answer Time (seconds)**: The maximum response time used with the service-level target.
- **Shrinkage (%)**: The percentage of scheduled time when service representatives are unavailable because of activities such as breaks, training, coaching, meetings, or unplanned absences.
- **Concurrency**: The number of interactions that a service representative is expected to handle at the same time. Use `1` for voice, and configure other channels according to your operating model.
- **Occupancy (%)**: The percentage of logged-in time that service representatives are expected to spend handling interactions, including related after-interaction work.

### Associate a service objective with a planning group

1. Open the planning group that you want to configure.
1. Select the **Service Objectives** lookup field.
1. Select **Add New Service Objective**.
1. Enter values for **Service Level (%)**, **Target Answer Time (seconds)**, **Shrinkage (%)**, **Occupancy (%)**, and **Concurrency**.
1. Select **Save**.

When you create a capacity plan for the planning group, the service objective values are prepopulated in the plan. You can change individual values to model a specific scenario.

> [!NOTE]
> Service objectives apply to all capacity plans associated with the planning group. If channels require different service-level targets, create separate planning groups for those channel scopes.

## Associate workforce management artifacts

A planning group provides shared context for shift plans, forecast scenarios, and capacity plans.

### Shift plans

A shift plan defines shifts, activities, and coverage windows for service representatives. When you associate a shift plan with a planning group, the plan uses the group’s time zone and representative scope.

1. In the planning group, select **Add New Shift Plan** or **Add Existing Shift Plan**.
1. On the **Details** card, select the **Planning Group** lookup field.
1. Search for and select the planning group.
1. Select **Save**.

### Forecast scenarios

A forecast scenario models expected interaction volume over a defined period. It uses the planning group’s demand scope and time zone to generate volume projections and staffing requirements.

1. In the site map, under **Workforce Management**, select **Forecast Scenarios**.
1. Open a forecast scenario, or select **New**.
1. On the **Details** card, select the **Planning Group** lookup field.
1. Search for and select the planning group.
1. Select **Save**.

### Capacity plans

A capacity plan converts a forecast scenario into a staffing projection. It uses the service objectives associated with the planning group to calculate the number of service representatives required for each interval.

1. In the site map, under **Workforce Management**, select **Capacity Planning**.
1. Select **New**, and then select **Short-term** or **Long-term**.
1. On the **Details** card, select the **Planning Group** lookup field.
1. Search for and select the planning group. The **Forecast Scenario** lookup displays scenarios associated with that planning group.
1. Select the forecast scenario that you want to use.
1. Select **Save**. The service objective values from the planning group are prepopulated in the capacity plan.

## Related information

- [Create and manage capacity plans](workforce-management-capacity-planning.md)  
- [Create and manage forecast scenarios](workforce-management-forecast-scenarios.md)  
- [Use shift bidding to select shifts](workforce-management-representative-shift-bidding.md)
