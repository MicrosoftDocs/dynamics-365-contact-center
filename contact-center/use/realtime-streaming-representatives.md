---
title: Monitor representatives in real time (preview)
description: Use the Representatives view in Dynamics 365 Contact Center to monitor representative activity, availability, and workload in real time.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.date: 06/23/2026
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

The **Representatives** view enables supervisors to:

- Monitor representative availability in real time.
- Understand how representatives are distributed across presence statuses and how long they have been in that presence status.
- View assigned queues and adjust queue membership.
- Reset representative status and modify representative attributes such as skills and capacity profiles.
- Analyze how representative presence status changed during the last 24 hours.
- Analyze representative performance over the selected time period, such as conversation assignments answered compared to the total number offered.

In **Real-time streaming analytics**, select the **Representatives** tab.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements.
>
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

### Representative performance

The representative performance section provides insights into the following areas:

- **Online Representatives**: Shows the number of representatives who are currently available and connected to the system.

- **Offline Representatives**: Shows the number of representatives who are currently offline or unavailable to receive work.

- **Representatives in active conversations**: Shows the number of representatives who are currently engaged in customer conversations.

- **Representative presence**: Displays the distribution of representatives across presence states, such as Available, Busy, Busy - DND, Away, Offline, and custom presence statuses. Each status includes a count and a visual bar representation. A live indicator shows real-time data.

## Use with the Representatives grid

- Use the search box to search representatives by name or attributes.

- Perform actions on representatives with the following options:

   - **Update queues**:
    1. Select one or more representatives using the checkbox.
    1. Select **Update queues**.
    1. Assign, modify, or remove queue memberships for the selected representatives.

   - **Update presence**:
    1. Select one or more representatives using the checkbox.
    1. Select **Update presence**.
    1. Set a new presence state from the available options.

 In the grid, each row represents a single representative. You see the corresponding details:

- **Representative name**: Name of the representative.

- **Presence status**: Includes a colored status indicator with **Set by** information that indicates whether the system or the person updated status.

- **Duration**: Time spent in the current presence status in hh:mm.

- **Availability (Capacity Profiles)**: Numeric value representing assigned capacity profile. Select this value to view available and consumed capacity for each capacity profile assigned to the representative.

- **Availability (Capacity Units)**: Indicates consumed versus total capacity, with a visual bar and numbers (for example, 6/15).
- **Conv. Assignments (Answered/Offered)**: Ratio of answered conversation assignments to offered conversations assignments. For example: 12/18.

- **Active conversations**: Number of currently active conversations.

- **Assignment – Unanswered**: Number of conversation assignments that aren't accepted. Visual bar representation includes classification of how many of these are explicitly rejected by representatives versus how many aren't accepted leading to timeout.

- **Queues**: Number of queues assigned to the representative. Selecting the value opens the right side pane that shows the queues to which the representative has been added.

- **Skills**: Indicates the count of assigned skills. Selecting the value opens the right side pane that shows the skills assigned to the representative.

Use filters and search to identify representatives with low answer rates and take corrective action.

## Related information

[Overview of real-time streaming analytics (preview)](realtime-streaming.md)
[Real-time streaming analytics (preview)](realtime-streaming.md)
[Wallboard](realtime-streaming-wallboard.md)  
[Assisted Service](realtime-streaming-assisted-service.md)  
[Queues](realtime-streaming-queues.md)   
[Conversations](realtime-streaming-conversations.md)