---
title: Monitor representatives in real time (preview)
description: Use the Representatives view in Dynamics 365 Contact Center to monitor representative activity, availability, and workload in real time.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.date: 09/29/2026
ms.topic: concept-article
ms.custom: bap-template
---

# Monitor representatives in real time (preview)

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

[This article is prerelease documentation and is subject to change.]

The **Representatives** view provides real-time visibility into individual representative activity, availability, and workload. Supervisors can monitor representative metrics, review presence status, update queues, and reset presence directly from the grid.

> [!IMPORTANT]
>
> - This is a production-ready preview feature.
> - Production-ready previews are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520).

Supervisors can use the **Representatives** view to:

- Monitor representative availability in real time.
- Review the distribution of representatives across presence statuses and how long each representative has been in their current status.
- View assigned queues and adjust queue membership.
- Reset representative presence status.
- Analyze how representative presence status changed during the last 24 hours.
- Analyze representative performance over the selected time period, such as the number of conversation assignments answered compared with the number offered.

In **Real-time streaming analytics**, select the **Representatives** tab.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Filter representative performance data

Use the **Representative** filter to view performance metrics for a specific representative. Enter all or part of a representative's name in the search box, and then select the representative from the results. The dashboard updates to display performance metrics for the selected representative.

### Representative performance

The representative performance section displays the following metrics:

- **Online Representatives**: Shows the number of representatives who are available and connected to the system.

- **Offline Representatives**: Shows the number of representatives who are offline or unavailable to receive work.

- **Representatives in active conversations**: Shows the number of representatives who are engaged in customer conversations.

- **Representative presence**: Displays the distribution of representatives across presence states, such as Available, Busy, Busy - DND, Away, Offline, and custom presence statuses. Each status includes a count and a bar that represents that count. A live indicator shows real-time data.

## Use the Representatives grid

- Use the search box to search for representatives by name or attributes.

- Perform actions on representatives with the following options:

   - **Update queues**:
    1. Select one or more representatives using the checkbox.
    1. Select **Update queues**.
    1. Assign, modify, or remove queue memberships for the selected representatives.

   - **Update presence**:
    1. Select one or more representatives using the checkbox.
    1. Select **Update presence**.
    1. Set a new presence state from the available options.
    
   - **Update user attributes**
   1. Select one or more representatives by using the checkbox.
   1. Select one of the following options:
   - **Update skills**: Add, remove, or replace skills and update proficiency levels for the selected representatives.
   - **Update capacity profiles**: Add, remove, or replace capacity profiles.
   - **Update capacity units**: Update the default capacity units for the selected representatives.
- Save the changes.

Each row in the grid represents one representative and displays the following information:

- **Representative name**: Name of the representative.

- **Presence status**: Includes a colored status indicator and **Set by** information that identifies whether the system or a user changed the presence status.

- **Duration**: Time spent in the current presence status, displayed as hours and minutes (hh:mm).

- **Availability (Capacity Profiles)**: Numeric value representing assigned capacity profile. Select this value to view available and consumed capacity for each capacity profile assigned to the representative.

- **Availability (Capacity Units)**: Indicates consumed versus total capacity, with a visual bar and numbers (for example, 6/15).
  
- **Conv. Assignments (Answered/Offered)**: Ratio of answered conversation assignments to offered conversations assignments, such as 12/18.

- **Active conversations**: Number of currently active conversations.

- **Assignment – Unanswered**: Number of conversation assignments that aren't accepted. A bar shows how many assignments representatives explicitly reject and how many time out before representatives accept them.

- **Queues**: Number of queues assigned to the representative. Select the value to open a pane that lists the queues assigned to the representative.

- **Skills**: Number of skills assigned to the representative. Select the value to open a pane that lists those skills.

## Related information

[Overview of real-time streaming analytics (preview)](realtime-streaming.md)  
[Wallboard](realtime-streaming-wallboard.md)  
[Assisted Service](realtime-streaming-assisted-service.md)  
[Queues](realtime-streaming-queues.md)  
[Conversations](realtime-streaming-conversations.md)
