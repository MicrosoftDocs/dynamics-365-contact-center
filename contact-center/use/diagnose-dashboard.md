---
title: Diagnose contact center health
description: Know how the Diagnose dashboard can help you, as a supervisor, why the automatic routing assignments are failing or high queue backlogs are affecting service SLAs in Dynamics 365 Contact Center and Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot 
ms.date: 11/19/2025
ms.custom: bap-template
---

# Diagnose contact center health

Supervisors and contact center operators can identify routing issues and uncover the underlying causes of declining performance metrics—such as a high queue backlog or service representatives not being assigned any work, despite having the available presence.

The system provides visibility into operational challenges that contribute to the degrading metrics and offers actionable recommendations to resolve them. Supervisors can further explore these insights, take immediate corrective actions, and quickly restore degrading contact centre metrics. This empowers them to self-serve and address issues efficiently, enhancing overall contact center responsiveness.

With debug experience, organizations can access diagnostic telemetry for the full lifecycle of a conversation via Application Insights to effectively troubleshoot runtime issues. This end-to-end data empowers teams to identify problems quickly, apply mitigations, and maintain seamless contact center operations.

## Prerequisites

- The user must have the **Omnichannel supervisor privileges** to access the Diagnose dashboard. [Learn how to configure user roles to access analytics and dashboards.](https://learn.microsoft.com/en-gb/dynamics365/customer-service/administer/configure-customer-service-analytics-insights-csh#configure-user-access-to-analytics-and-dashboards)

- To access App Insights dashboards embedded in Debug tab:

  - [Conversation diagnostics](https://learn.microsoft.com/dynamics365/customer-service/administer/configure-conversation-diagnostics) must be configured for the environment.

  - Assignment snapshots in conversation diagnostics must be enabled for the environment.
    > [!NOTE]
    > It takes approximately 24 hours to sync the data completely.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature is not intended for use in making—and should not be used to make—decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This also includes adequately notifying end users that their communications with representatives may be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users may be monitored, recorded, or stored.

## Things to keep in mind

- Diagnostics insights is supported for out-of-the-box assignment methods only and considers presence, capacity, and skills check to diagnose the assignment issues.

- The feature currently supports live chat, voice, and asynchronous messaging channels only.

- The data in the App Insights out-of-the-box dashboards tab might have a delay of up to 15 minutes.

- Diagnostics to view data related to transfer and consult conversations aren’t supported in App Insights OOB dashboards.

## Key scenarios for Analyze

The feature offers the following diagnostics scenarios. The information displayed is dependent on the operational issues that affect the scenario. You might see one or more of the line items explained here.

### How do I reduce queue backlog

This diagnostic scenario enables supervisors identify the top 10 queues that currently have the highest number of conversations awaiting automatic assignment.

By default, the queue with the highest number of unassigned conversations is displayed with the following information:

- **Details**: Displays information, such as conversation metrics and assignment attempts. For the selected queue, the supervisor can view:

  - Conversation details

    - Total conversations in the queue

    - Conversations awaiting automatic assignment

    - Conversations awaiting manual assignment

    - Oldest conversation waiting since

  - Time when latest assignment was attempted

  - Conversations assigned in last 15 minutes

  - Number of members

- **Analysis**: Displays insights into the operational challenges that contribute to the metrics degradation. The supervisor can view the following issues:

  - Number of distinct conversations rejected by service representatives at least once if any out of the total number of conversations awaiting automatic assignments.

  - Number of distinct conversations that aren’t accepted and timed out by representatives at least once if any out of the total number of conversations awaiting automatic assignments.

  - Number of representatives who have presence states like Busy-DND, Away, or offline that aren't allowed and the number of representatives who set themselves to those presence states manually.

  - Number of representatives who currently don’t have any available capacity or are on a blocking capacity.

  - Top 3 capacity profiles needed by the conversations waiting to be automatically assigned in the queue and the number of service representatives who lack the required capacity profiles.

  - Top 3 skills needed by the conversations waiting to be automatically assigned in the queue and the number of service representatives who lack those skills

- **Suggestions**: Supervisors can drill down to know more details about the insights provided with recommended actions to reduce the queue backlog. These include:

  - Representatives who rejected or didn’t accept conversations offered to them and the count of distinct conversations rejected out of total conversations awaiting assignment from the selected queue. Any conversation that was rejected or not accepted at least once and is still awaiting automatic assignment is counted.

  > [!NOTE]
  > The system doesn’t show the number of times the conversations are rejected or aren’t accepted by the representative.

- Representatives who have marked themselves with presence status like Busy-DND, Away, or Offline that might be preventing work assignments to them. The supervisor can view recommendations to reset their presence status as a corrective action.

- Representatives who don’t have available capacity as follows:

  - Have zero or negative capacity if unit-based capacity is configured for the workstream that's landing the conversations to this queue.

  - Have zero or negative capacity for any of the top 3 identified capacity profiles (if capacity profile is configured for the workstreams landing the conversations to this queue) needed by the conversations awaiting assignment from the queue

  - Name of the blocking capacity profile, if the user is blocked on a capacity profile. For example, the user is on a call and hence their capacity is blocked for new assignments.

- Representatives who don’t have top 3 identified capacity profiles or skills needed by the conversations awaiting assignment. By following the recommended actions, supervisor can work with their business administrators to ensure the relevant capacity profiles or skills are added to the service representatives.

- Representatives whose available capacity isn’t zero (for any of the top 3 capacity profiles needed by the conversations if capacity profile is configured for the workstreams) with their presence details that might be contributing to assignments not happening for those representatives.

- Representatives whose presence status is set to Busy-DND automatically by the system because they have 10 session tabs open and therefore they aren’t receiving assignments. By following recommended actions, supervisors can ensure that the representatives close the wrapped up sessions. Also, if representatives need more than 10 session tabs opened, supervisors can receive in-product guidance to configure Inbox view for them.

### How do I optimize representative’s task assignments

This diagnostic scenario enables supervisors understand why some representatives weren’t assigned any work in a while. Supervisors can filter on time as per their business needs. The duration available for selection in the filter is from more than 5 minutes to up to more than 12 hours. The default duration is set to greater than 30 minutes. When the supervisor selects the option to optimize representative’s task assignments, the system automatically pre-selects the queue that has the highest number of representatives with no assignments for more than 30 minutes. It considers representatives only up till last 24 hours from the current time. Supervisor can change the queue selection. The following information is available:

- **Details**: For the queue that’s selected by default, the supervisor can view the following:

  - Number of service representatives who are a member of the queue.

  - Number of service representatives who haven’t been assigned conversations in the last 30 minutes or more.

  - Number of conversations awaiting automatic assignment in the selected queue.

  - Top 3 capacity profiles or skills needed by the conversations with the number of conversations that need each of them

  - The time stamp when the last automatic assignment was attempted

  - How many conversations are assigned in the last 15 minutes

- **Analysis**: Lists the names of top 10 representatives who haven’t been assigned work items for the last 30 minutes or more with the time passed since the last assignment.

- **Suggestions**: Supervisors can drill down to know more details of:

  - Why a representative wasn't assigned any work in the last 30 minutes or more. They can dive deeper to get insights as follows:

    - The number of times representative rejected or didn’t accept (time out) one or more conversations that were offered

    - Current and default presence of the representative, and how long they are offline/on Busy DND, or away out of the total time for which no conversation was assigned to them.

    - Current available capacity for the top 3 capacity profiles needed by the waiting conversations in the queue

    - Duration when the representative had zero or negative available capacity (for any of the top 3 capacity profiles identified if using capacity profile) out of the total time for which no conversation was assigned to them

    - Duration when the representative was on a blocking capacity profile, out of the total time for which no conversation was assigned to them

    - Current skills of the representative

  - View the list of all representatives who haven’t been assigned any work in the last 30 minutes or more

  - View details of representatives who rejected or didn’t accept conversations, when offered out of the total number of representatives who weren’t assigned any work during the selected time frame

## Key capabilities for Debug

The Debug experience offers the following diagnostic capabilities:

- **Conversation trend analysis**: Visualize trends over the last 24 hours or a custom time range, filtered by channel and queue.

- **Assignment performance**: Analyze time to assign and assignment events to identify bottlenecks.

- **Non-assignment reasons**: View top non-assignment reasons and drill into specific cases.

- **Conversation timeline**: Inspect the full lifecycle of a conversation, including assignment events.

- **Service representative details**: Get detailed service representative view including configured parameters like skills, capacity, presence and all conversations handled by the service representative.

- **Raw event access**: Access raw conversation telemetry from Application Insights for deep-dive analysis of specific work items.

- **Assignment events**: Analyze both the demand (work item) and supply (CSR) view for an assignment event at one place. In addition, get more details on each assignment event for a work item including why a CSR was not found during an assignment run.

## Access the Diagnose dashboard

Supervisor can access this capability from Omnichannel real time analytics dashboard. The **Diagnose** page offers two tabs – *Analyze* that lists the scenarios that supervisors can analyse and get recommendations to resolve issues and *Debug* that presents a visual representation of the conversation lifecycle to debug issues in a particular conversation.

1. Go to Copilot Service workspace and select **Omnichannel real-time analytics**.

    :::image type="content" source="media/debug-dashboard/image1.png" alt-text="Navigation to Omnichannel real-time analytics":::

1. On the command bar, select **Diagnose**.

    :::image type="content" source="media/debug-dashboard/image2.png" alt-text="":::

    A new session tab opens and the user lands on the **Analyze** tab that displays the following scenarios:

    - **How do I reduce queue backlog**

        :::image type="content" source="media/debug-dashboard/image3.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

    - **How do I optimize representative’s task assignments**

        > :::image type="content" source="media/debug-dashboard/image4.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

1. Select **Debug**. A Visual representation of conversation lifecycle and other Application Insights data is displayed.

    :::image type="content" source="media/debug-dashboard/image5.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

## Use the Debug tab

Do the following steps for debugging issues:

- Use the top-level filters to select a period for analysis, the channel type, organization ID, and queue name.

    :::image type="content" source="media/debug-dashboard/image19.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- View the conversations in different states over time. You can use this to look at trends of open conversations over time and select a specific period for further analysis from top-level filters mentioned in the preceding paragraph.

    :::image type="content" source="media/debug-dashboard/image20.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- View the **Total processed conversations** and **Assignment time (P95)** for more details on the overall health for routing. The **Total processed conversations** are the number of conversations that are processed by contact center during the selected period. The **Assignment time (P95)** here is P95 of the time taken for first successful assignment of a conversation to service representative.

    :::image type="content" source="media/debug-dashboard/image21.png" alt-text="A close up of text AI-generated content may be incorrect.":::

- Select **View by time to assign** to understand the distribution of conversations by time for first successful assignment to representative.

    :::image type="content" source="media/debug-dashboard/image22.png" alt-text="A screenshot of a graph AI-generated content may be incorrect.":::

- Select **View by assignment events** to understand distribution of conversations by total assignment events. An assignment event is defined as an event when the assignment engine tried to assign a conversation to a service representative.

    :::image type="content" source="media/debug-dashboard/image23.png" alt-text="A screenshot of a graph AI-generated content may be incorrect.":::

- View **Conversations with non-assignment reasons** to understand why a conversation wasn’t assigned during the assignment flow.

   > [!Note]
   > During a conversation assignment, if the conversation is rejected by the service representative and the next time the assignment engine doesn’t find any eligible service representatives for the conversation, it's counted in both **No eligible CSRs found** and **CSR reject**.

    :::image type="content" source="media/debug-dashboard/image24.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- Use the **All Conversations** table to get details on the conversation state, time to assign the conversation, number of assignment events, when the conversation was initiated and the queue and workstream the conversation was routed to, for different conversations during a defined time period. You can also use the filters for **Assignment events**, **Conversation state**, and **Time to assign** to select precise conversations for analysis.

    :::image type="content" source="media/debug-dashboard/image25.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- Select an individual conversation to view **Conversation details**. Use this page to view details like the conversation ID, assignment duration,  channel name, required capacity, presence, and skills for the selected conversation. You can also view the conversation timeline to understand all the events that occurred for a conversation in a chronological order.

    :::image type="content" source="media/debug-dashboard/image26.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- For a detailed analysis of individual events, select the **View all events** link in the Information section.

  The **View all events** link provides details on each conversation stage with the full details of the stage.

    :::image type="content" source="media/debug-dashboard/image27.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- Select **Custom Dimensions** to get details on the individual conversation event. This is helpful when you want to view the output and other details for a conversation event. For example, for Route To Queue event, you can view what rulesets or rules were applied for a conversation, the conditions defined in the rules and what is the final queue that the conversation was routed to.

    :::image type="content" source="media/debug-dashboard/image28.png" alt-text="":::

- For analysis of assignment related issues, you can go to **All conversations** list and select an individual assignment event to get details on the assignment event. You can also sort the list based on Assignment events to view the conversations that involved the assignment engine multiple times. You can also sort the list on **Time to assign** to view the conversations that have taken the maximum time to be assigned to service representative.

    :::image type="content" source="media/debug-dashboard/image29.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- The **Assignment events** page for a conversation has details on conversation with information specific to the assignment, assignment method used, and ruleset information for the assignment step. The **Timeline** section has details on different assignment events, the run result, representative name, and other details like presence, available capacity, and capacity profiles after the assignment event that are sorted in a chronological order for easier readability.

    :::image type="content" source="media/debug-dashboard/image30.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- Select a representative name to go to the CSR details view. The CSR details view shows information like service representative name, ID, capacity units, capacity profiles assigned to service representative, skills assigned to service representative, and queues that service representative is part of. The **Timeline** section shows events from +/- 2 hours from the assignment event and has details on the individual conversations that service representative interacted with, the action and result and the change in capacity, presence and capacity profile for the service representative due to the action.

    :::image type="content" source="media/debug-dashboard/image31.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

  If the assignment engine is unable to find any eligible service representative, the CSR column shows **No eligible CSR found**. Select **No eligible CSR found** that takes you to **Assignment event** **details**.

    :::image type="content" source="media/debug-dashboard/image32.png" alt-text="A screenshot of a computer screen AI-generated content may be incorrect.":::

- The **Assignment event details** view is especially helpful if you want to validate why a particular representative wasn’t eligible during a particular assignment run. There is information around the conversation to help provide the requirements for a conversation in terms of presence, skills and capacity. The Timeline section has a search bar for service representatives. You can enter the representative name in the search bar to view the presence, skills, capacity and capacity profile during the assignment event. You can then compare it with the required capacity, required capacity profile, required skills and allowed presence from the Information section to understand why the representative was not selected during the assignment run.

    :::image type="content" source="media/debug-dashboard/image33.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

## FAQs

### I am using an unmanaged environment for Dynamics 365 Customer Service and Dynamics 365 Contact Center. Can I use these out-of-the-box dashboards?

No. To set up the out-of-the-box dashboards for Application Insights, you need a managed environment. Learn more in [Prerequisites](/dynamics365/customer-service/administer/configure-conversation-diagnostics)

### Does my organization need any extra licenses for accessing these dashboards?

Your organization doesn't need any extra licenses for Dynamics 365 Contact Center or Customer Service. However, you need an active Azure Monitor subscription for using the out-of-the-box dashboards. More details: [Pricing](https://learn.microsoft.com/dynamics365/customer-service/administer/configure-conversation-diagnostics#pricing)

### I already have an Omnichannel supervisor role assigned. What extra roles or permissions do I need to access these dashboards?

For accessing the out-of-the-box dashboards, the user must have access to Azure monitoring. More details: [Roles and permissions](https://learn.microsoft.com/azure/azure-monitor/fundamentals/roles-permissions-security)

### How often is the data refreshed?

By default, the data is dashboard is not auto refreshed. However, you can set the auto-refresh interval for your workbook.

:::image type="content" source="media/debug-dashboard/image34.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

### Can I export dashboard data?

You can export the dashboard details as JSON from the Advanced editor option. However, the dashboard data cannot be exported or imported.

### What happens when there is solution update?

You will need to bind the Managed Identity with Plugin Assembly again. Perform **Bind managed identity with plugin assembly** step from this document.

Open newly created 3P app from App registration  
Click **Certificates and secrets  
  **

8.  **Create Managed Identity record:  **
    Logged into the Dynamics organization.  
    Go to the **Copilot Service Workspace** (CSW)  
    **Click on**

