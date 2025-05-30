---
title: Use shift-based routing
description: Learn how to use shift-based routing for representative work items to help you manage your workforce.
author: lalexms  
ms.author: laalexan
ms.reviewer: lalexan
ms.topic: how-to
ms.collection: 
ms.date: 05/29/2025
ms.custom: bap-template
---

# Use shift-based routing for work items

You can use assignment rules to route and assign cases and conversations based on your customer service representatives' (service representative or representative) shift schedules. By verifying representatives' schedules in advance, you can avoid routing tasks to off-duty service representatives, which helps reduce the risk of assignment delays. 

You can incorporate shift assignments and time-off considerations into the routing process to foster an employee-centric approach, and streamline operational workflows for productivity and improved retention rates.

## Prerequisites

- Your administrator installed the [Workforce Management for Customer Service package](../administer/wfm-package-installation.md).
- [Shift-based routing is enabled](wfm-enable-shift-based-routing.md).
- [Unified routing](/dynamics365/customer-service/administer/provision-unified-routing) is provisioned and set up.
- [Workstreams](/customer-service/administer/create-workstreams) and [advanced queues](/dynamics365/customer-service/administer/queues-omnichannel) are set up.
- [Custom assignment method](/dynamics365/customer-service/administer/configure-assignment-rules) is configured for the queue.

## Configure an assignment rule

1. In the Copilot Service admin center site map, select **Queues**, and then select **Manage** in the **Advanced queues** area.
1. Select the queue that you want to configure the assignment rule for, select the [custom assignment](/customer-service/administer/configure-assignment-rules) method, and select **Edit**.
1. Create a rule or modify an existing rule, and do the following steps:
    1. In **Conditions**, select **Add row**, and then select **Calendar schedule**. The **Is working** value is automatically selected.
    1. Save and close.

       :::image type="content" source="../media/calendar-schedule-condition.png" alt-text="Screenshot of assignment rule configured on calendar schedule.":::

## View routing diagnostics records

View the [routing diagnostics record](/customer-service/administer/unified-routing-diagnostics) to understand how a work item is routed when routing is configured based on representative calendar attribute.

## How shift-based routing works

The imported schedules from external systems are represented in Dynamics 365 as "bookings". The [bookableresourcebooking](customer-service/develop/reference/entities/bookableresourcebooking) entity stores this information. Each booking is assigned to a representative. The representative is recorded as a bookable resource and each of them with one or more bookings has a corresponding entry in the [bookableresource](/customer-service/develop/reference/entities/bookableresource) entity.

An automated process synchronizes the representative's imported schedules with the representative's work hour calendar. The following rules apply for the automatic synchronization:

- After you opt in the representative for shift-based routing, the first automated sync occurs after **180 minutes** to allow the external schedules to be imported for the representative.
- After the first automated sync, the representative's bookings are synchronized with their work hour calendar every **180 minutes**.
- Each automated run synchronizes the representative's bookings for the next **28 days**, starting from the time of the automated sync. Bookings beyond 28 days aren't synchronized.
- Any updates to the booking, including deletion of the booking, are immediately reflected in the corresponding work hour entry for the booking. For example, if the end time for a synchronized booking is updated, then the end time of the corresponding work hour calendar entry is also updated immediately. Similarly, if a synchronized booking is deleted, then the corresponding work hour calendar entry is also removed.

After the representative's bookings are synchronized with their work hour calendar, unified routing routes work items based on the work hour calendar entries.

## Next steps

[Use Copilot Service workspace](/customer-service/implement/csw-overview)  
[View the representative calendar](use-agent-calendar.md)  
