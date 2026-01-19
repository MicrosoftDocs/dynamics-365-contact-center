---
title: Diagnose contact center health with the Application Insights dashboard
description: Know how the Diagnose dashboard can help you, as a supervisor, and why the automatic routing assignments are failing or high queue backlogs are affecting service SLAs in Dynamics 365 Contact Center and Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot 
ms.date: 01/19/2026
ms.custom: bap-template
---

# Diagnose contact center health using Application Insights dashboard

Supervisors and contact center operators can identify routing issues and uncover the underlying causes of declining performance metrics, such as a high queue backlog or service representatives not being assigned any work, despite having the required presence.

With debug experience, organizations can access diagnostic telemetry for the full lifecycle of a conversation via Application Insights to effectively troubleshoot runtime issues. This end-to-end data empowers teams to identify problems quickly, apply mitigations, and maintain seamless contact center operations.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature is not intended for use in making—and should not be used to make—decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This also includes adequately notifying end users that their communications with representatives may be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users may be monitored, recorded, or stored.

## Prerequisites

- You have the **Omnichannel supervisor privileges** to access the diagnostics dashboard. [Learn how to configure user roles to access analytics and dashboards](/dynamics365/customer-service/administer/configure-customer-service-analytics-insights-csh#configure-user-access-to-analytics-and-dashboards).

- [Omnichannel real-time dashboards are enabled](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator).

- [Application Insights](/azure/azure-monitor/app/create-workspace-resource?tabs=portal#create-an-application-insights-resource) is configured.

    > [!NOTE]
    > It takes approximately 24 hours to sync the data completely.

## Things to keep in mind

- Diagnostics insights is supported for out-of-the-box assignment methods only and considers presence, capacity, and skills check to diagnose the assignment issues.

- The data in the Application Insights out-of-the-box dashboards tab might have a delay of up to 15 minutes.

- Diagnostics to view data related to transfer and consult conversations aren’t supported.

## Key debug capabilities

The debug experience offers the following diagnostic capabilities:

- **Conversation trend analysis**: Visualize trends over the last 24 hours or a custom time range, filtered by channel and queue.

- **Assignment performance**: Analyze time to assign and assignment events to identify bottlenecks.

- **Non-assignment reasons**: View top non-assignment reasons and drill into specific cases.

- **Conversation timeline**: Inspect the full lifecycle of a conversation, including assignment events.

- **Service representative details**: Get detailed service representative view including configured parameters like skills, capacity, presence and all conversations handled by the service representative.

- **Raw event access**: Access raw conversation telemetry from Application Insights for deep-dive analysis of specific work items.

- **Assignment events**: Analyze the work item and service representative view for an assignment event. Event‑level details that explain why a representative was or wasn’t identified during an assignment run.

## Access the Diagnose dashboard

Supervisors can access the **Diagnose** dashboard in Omnichannel real-time analytics dashboard.

1. In the site map of Copilot Service workspace, select **Omnichannel Realtime analytics**.

1. On the command bar, select **Diagnose**. A new session tab displays the **Debug** page with conversation lifecycle and other Application Insights data.

    :::image type="content" source="../media/debug-dashboard.png" alt-text="A screenshot of the Debug page with conversation lifecycle and Application Insights data.":::

## Use the Debug tab to view assignment data

Perform the following steps to debug issues:

- Use the top-level filters to select a period for analysis, the channel type, organization ID, and queue name.

- View the conversations in different states over time. You can use this to look at trends of open conversations and select a specific period for further analysis from top-level filters.

    - **Total processed conversations**: The number of conversations processed by the contact center during the selected period.
    - **Assignment time (P95)**: The time taken for first successful assignment of a conversation to a service representative.

        :::image type="content" source="../media/debug-metrics.png" alt-text="A screenshot of assignment time and total processed conversations metrics.":::

- Select **View by time to assign** to understand the distribution of conversations by time for first successful assignment to representative.

    :::image type="content" source="../media/view-by-time-to-assign.png" alt-text="A screenshot of view by time to assign.":::

- Select **View by assignment events** to understand distribution of conversations by total assignment events. An assignment event is defined as an event when the assignment engine tries to assign a conversation to a service representative.

    :::image type="content" source="../media/view-by-assignment-events.png" alt-text="A screenshot of view by assignment events.":::

- View **Conversations with non-assignment reasons** to understand why a conversation wasn’t assigned during the assignment flow.

   > [!NOTE]
   > During a conversation assignment, if the conversation is rejected by the service representative and the next time the assignment engine doesn’t find any eligible service representatives for the conversation, it's counted in both **No eligible CSRs found** and **CSR reject**.

    :::image type="content" source="../media/conversations-by-non-assignment-reasons.png" alt-text="A screenshot of conversations by non assignment reasons.":::

- Use the **All Conversations** table to get details on the conversation state, time to assign the conversation, number of assignment events, when the conversation was initiated and the queue and workstream the conversation was routed to, for different conversations during a defined time period. You can also use the filters for **Assignment events**, **Conversation state**, and **Time to assign** to select precise conversations for analysis.

    :::image type="content" source="../media/debug-all-conversations.png" alt-text="A screenshot of all conversations.":::

- Select an individual conversation to view **Conversation details**. Use this page to view details like the conversation ID, assignment duration,  channel name, required capacity, presence, and skills for the selected conversation. You can also view the conversation timeline to understand all the events that occurred for a conversation in a chronological order.

    :::image type="content" source="../media/debug-conversation-details.png" alt-text="A screenshot of details of a conversation.":::

- For a detailed analysis of individual events, select the **View all events** link in the **Information** section.

  The **View all events** link provides details on each conversation stage with the full details of the stage.

- Select **Custom Dimensions** to get details on the individual conversation event. This is helpful when you want to view the output and other details for a conversation event. For example, for Route To Queue event, you can view what rulesets or rules were applied for a conversation, the conditions defined in the rules and what is the final queue that the conversation was routed to.

- For analysis of assignment related issues, you can go to **All conversations** list and select an individual assignment event to get details on the assignment event. You can also sort the list based on Assignment events to view the conversations that involved the assignment engine multiple times. You can also sort the list on **Time to assign** to view the conversations that have taken the maximum time to be assigned to service representative.

- The **Assignment events** page for a conversation has details on conversation with information specific to the assignment, assignment method used, and ruleset information for the assignment step. The **Timeline** section has details on different assignment events, the run result, representative name, and other details like presence, available capacity, and capacity profiles they had during the assignment event are sorted in a chronological order for easier readability.

    :::image type="content" source="../media/assignment-events.png" alt-text="A screenshot of the assignment events.":::

- Select a representative name to go to the **CSR details** view. The **CSR details** view shows information like service representative name, ID, capacity units, capacity profiles assigned to service representative, skills assigned to service representative, and queues that service representative is part of. The **Timeline** section shows events from +/- 2 hours from the assignment event and has details on the individual conversations that service representative interacted with, the action and result and the change in capacity, presence and capacity profile for the service representative due to the action.

    :::image type="content" source="../media/csr-details.png" alt-text="A screenshot of the representative details.":::

  If the assignment engine is unable to find any eligible service representative, the CSR column shows **No eligible CSR found**. Select **No eligible CSR found** that takes you to **Assignment event details**.

- The **Assignment event details** view is helpful if you want to validate why a representative wasn’t eligible during a particular assignment run. There is information around the conversation to help provide the requirements for a conversation in terms of presence, skills and capacity. The **Timeline** section has a search bar for service representatives. You can search for the representative to view the presence, skills, capacity and capacity profile during the assignment event. You can then compare it with the required capacity, required capacity profile, required skills and allowed presence from the **Information** section to understand why the representative wasn't selected during the assignment run.

### Related information

[Enable Diagnose dashboard](../administer/enable-diagnose-dashboard.md)  
[Configure conversation diagnostics](/dynamics365/customer-service/administer/configure-conversation-diagnostics)  