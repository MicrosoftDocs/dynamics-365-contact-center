---
title: Enable Diagnose dashboard
description: Learn how to enable the Diagnose dashboard that can help supervisors diagnose and debug issues in automatic routing assignments in Dynamics 365 Contact Center and Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot 
ms.date: 11/19/2025
ms.custom: bap-template
---

# Enable Diagnose dashboard

Supervisors and contact center operators can identify routing issues and uncover the underlying causes of declining performance metrics—such as a high queue backlog or service representatives not being assigned any work, despite having the available presence.

With the debug experience, organizations can access diagnostic telemetry for the full lifecycle of a conversation via Application Insights to effectively troubleshoot runtime issues. This end-to-end data empowers teams to identify problems quickly, apply mitigations, and maintain seamless contact center operations.

## Prerequisites

- The System administrator role.

- Assignment snapshots in conversation diagnostics must be enabled for the environment.

## Pricing

The conversation diagnostics data is stored in Azure Application Insights database. For details on pricing for data storage, refer [Pricing](https://learn.microsoft.com/en-us/dynamics365/customer-service/administer/configure-conversation-diagnostics#pricing).
There’s no additional cost for using Azure workbooks.


This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature is not intended for use in making—and should not be used to make—decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This also includes adequately notifying end users that their communications with representatives may be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users may be monitored, recorded, or stored.

## Things to keep in mind

- Diagnostics insights is supported for out-of-the-box assignment methods only and considers presence, capacity, and skills check to diagnose the assignment issues.

- The feature currently supports live chat, voice, and asynchronous messaging channels only.

- As a supervisor, you can view the **Diagnose** button on the **Omnichannel real-time analytics** dashboard in Copilot Service workspace.

- The data in the App Insights OOB dashboards tab might have a delay of up to 15 minutes.

- Diagnostics to view data related to transfer and consult conversations aren’t supported in App Insights OOB dashboards.

## Key capabilities for Analyze

The feature offers the following diagnostics scenarios. The information displayed is dependent on the operational issues that affect the scenario. You might see one or more of the line items explained here.

### Key scenarios for Analyze

#### How do I reduce queue backlog

This diagnostic scenario enables supervisors to identify the top 10 queues that currently have the highest number of conversations awaiting automatic assignment.

By default, the queue with the highest number of unassigned conversations is displayed with the following information:

- **Details**: Displays information, such as conversation metrics and assignment attempts. For the selected queue, the supervisor can view the following:

  - Conversation details

    - Total conversations in the queue

    - Conversations awaiting automatic assignment

    - Conversations awaiting manual assignment

    - Oldest conversation waiting since

  - Time when latest assignment was attempted

  - Conversations assigned in last 15 minutes

  - Number of members

- **Analysis**: Displays insights into the operational challenges contributing to the metrics degradation. The supervisor can view the following issues:

  - Number of distinct conversations that were rejected by service representatives at least once (if any) out of total number of conversations awaiting automatic assignment currently

  - Number of distinct conversations that weren’t accepted (timed out) by service representatives at least once (if any) out of total number of conversations awaiting automatic assignment currently

  - Number of representatives who are in not allowed presence states like Busy-DND, Away, or offline and how many of them set themselves to such “not allowed” presence states manually

  - Number of representatives who currently don’t have any available capacity or are on a blocking capacity

  - Top 3 capacity profiles needed by the conversations waiting to be automatically assigned from the queue and how many service representatives lack those capacity profiles

  - Top 3 skills needed by the conversations waiting to be automatically assigned from the queue and how many service representatives lack those skills

- **Suggestions**: Supervisors can drill down to know more details about the insights provided with recommended actions to reduce the queue backlog. These include:

  - Representatives who rejected or didn’t accept conversations offered to them and the count of distinct conversations rejected out of total conversations awaiting assignment from the selected queue. Any conversation that was rejected or not accepted at least once and is still awaiting automatic assignment is counted.

> **NOTE**
>
> The system doesn’t show the number of times the conversations were rejected or weren’t accepted by the representative.

- Representatives who have marked themselves with presence status like Busy-DND, Away, or Offline that might be preventing work assignments to them. The supervisor can view recommendations to reset their presence status as a corrective action.

- Representatives who don’t have available capacity. This could be

  - Have zero or negative available capacity if unit-based capacity is configured for the workstream which is landing the conversations to this queue

  - Have zero or negative available capacity for any of the top 3 identified capacity profiles (if capacity profile is configured for the workstreams landing the conversations to this queue) needed by the conversations awaiting assignment from the queue

  - Name of the blocking capacity profile, if the user is blocked on a capacity profile (for example, the user is on a call and hence their capacity is blocked for assignment)

- Representatives who don’t have top 3 identified capacity profiles or skills needed by the conversations awaiting assignment. By following the recommended actions, supervisor can work with their business administrators to ensure the relevant capacity profiles or skills are added to the service representatives.

- Representatives whose available capacity isn’t zero (for any of the top 3 capacity profiles needed by the conversations if capacity profile is configured for the workstreams) along with their presence details that might be contributing to assignments not happening for those representatives.

- Representatives whose presence status is set to Busy-DND automatically by the system because they have 10 session tabs open and therefore they aren’t receiving assignments. By following recommended actions, supervisors can ensure that the representatives close the wrapped up sessions. Also, if representatives need more than 10 session tabs opened, supervisors can receive in-product guidance to configure Inbox view for them.

#### How do I optimize representative’s task assignments

This diagnostic scenario enables supervisors understand why some representatives weren’t assigned any work in a while. Supervisors can filter on time as per their business needs. The duration available for selection in the filter is from more than 5 minutes to up to more than 12 hours. The default duration is set to \> 30 minutes. When the supervisor selects the option to optimize representative’s task assignments, the system automatically pre-selects the queue that has the highest number of representatives with no assignments for more than 30 minutes. It considers representatives only up till last 24 hours from the current time. Supervisor can change the queue selection. The following information is available:

- **Details**: For the queue that’s selected by default, the supervisor can view the following:

  - Number of service representatives who are a member of the queue

  - Number of service representatives who haven’t been assigned conversations in the last 30 minutes or more

  - Number of conversations awaiting automatic assignment in the selected queue

  - Top 3 capacity profiles or skills needed by the conversations along with how many conversations need each of those top 3 capacity profiles or skills

  - When was the last time automatic assignment was attempted

  - How many conversations were assigned in the last 15 minutes

- **Analysis**: Lists the names of top 10 representatives who haven’t been assigned work items for the last 30 minutes or more with the time passed since the last assignment

- **Suggestions**: Supervisors can drill down to know more details of:

  - Why a representative couldn’t get any work assigned in the last 30 minutes or more. They can dive deeper to get insights about the following:

    - Number of times representative rejected or didn’t accept (time out) one or more conversations when offered

    - Current presence, default presence of the representative, and how long they are offline/on Busy DND, away. out of the total time for which no conversation was assigned to them.

    - Current available capacity for the top 3 capacity profiles needed by the waiting conversations in the queue

    - For how long the representative had zero or negative available capacity (for any of the top 3 capacity profiles identified if using capacity profile) out of the total time for which no conversation was assigned to them

    - For how long the representative was on a blocking capacity profile, out of the total time for which no conversation was assigned to them

    - Current skills of the representative

  - View the list of all representatives who haven’t been assigned any work in the last 30 minutes or more

  - View details of representatives who rejected or didn’t accept conversations, when offered out of the total number of representatives who weren’t assigned any work during the selected time frame

## Key capabilities for Debug

The Debug experience offers the following diagnostic capabilities:

- **Conversation trend analysis**: Visualize trends over the last 24 hours or a custom time range, filtered by channel and queue.

- **Assignment performance**: Analyze time to assign and assignment events to identify bottlenecks.

- **Non-assignment reasons**: View top non-assignment reasons and drill into specific cases.

- **Conversation timeline**: Inspect the full lifecycle of a conversation, including assignment events.

- **CSR details**: Get detailed service representative view including configured parameters like skills, capacity, presence and all conversations handled by the service representative.

- **Raw event access**: Access raw conversation telemetry from Application Insights for deep-dive analysis of specific work items.

- **Assignment events**: Analyze both the demand (work item) and supply (CSR) view for an assignment event at one place. In addition, get more details on each assignment event for a work item including why a CSR was not found during an assignment run.

## Access the Diagnose dashboard

Supervisor can access this capability from Omnichannel real time analytics dashboard. The **Diagnose** page offers two tabs – *Analyze* that lists the scenarios that supervisors can analyse and get recommendations to resolve issues and *Debug* that presents a visual representation of the conversation lifecycle to debug issues in a particular conversation.

1.  Go to Copilot Service workspace and select **Omnichannel real-time analytics**.

:::image type="content" source="media/debug-dashboard/image1.png" alt-text="Navigation to Omnichannel real-time analytics":::

2.  On the command bar, select **Diagnose**.

> :::image type="content" source="media/debug-dashboard/image2.png" alt-text="":::
>
> A new session tab opens and the user lands on the **Analyze** tab that displays the following scenarios:

- **How do I reduce queue backlog**

> :::image type="content" source="media/debug-dashboard/image3.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

- **How do I optimize representative’s task assignments**

> :::image type="content" source="media/debug-dashboard/image4.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

3.  Select **Debug**. A Visual representation of conversation lifecycle and other Application Insights data is displayed.

> :::image type="content" source="media/debug-dashboard/image5.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

## Enable Debug tab experience

1.  **Create App-insights app (If not already created):**

    1.  Go to <https://portal.azure.com/>

    2.  Search for Application insights, if not already created create new one.  
        After creation you will be able to see the details like:


3.  Get the **Application insights app id**, which is appended at the end of the connection string:

> InstrumentationKey=18c052c7-25g2-6a38-9b81-efadc26ed188;IngestionEndpoint=https://westus2-2.in.applicationinsights.azure.com/;LiveEndpoint=https://test.livediagnostics.monitor.azure.com/;ApplicationId=80ddd645-54e4-4014-ba39-29c9bb549c68  


2.  **Enter AppInsights Id when importing the solution:**

When importing the solution, you will get new field to enter AppInsights id in environment variable.

Enter an Id of AppInsights app from the previous step and import the solution. 

If it’s not available, you can skip and add it later from environment variables screen.

3.  Select the variable name, enter your application insights id and save it.



4.  **Create 3P app in your tenant**

    1.  Sign in to <https://portal.azure.com/> using credentials.

    2.  Go to **App registrations**.



3.  Select **New registration.**

4.  Enter your app name (a name for identifying your app)

5.  Select **Register**.



6.  Open newly created app from App registration

7.  Copy the **Application (Client) ID** and **Directory (Tenant) ID**, and save them in a secure location (e.g., a Notepad file) for future references.

8.  Select **Certificates and secrets  **


9.  Select **Federated credentials**

10. Select\* **Add credential.**:::image type="content" source="media/debug-dashboard/image14.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

11. Select **Other issuer.**

> **Issuer:** [https://login.microsoftonline.com/{tenant-id}/v2.0](https://login.microsoftonline.com/%7btenant-id%7d/v2.0)  
> **Type:** Explicit subject identifier  
> **Value:** /eid1/c/pub/t/urwIj5vn7Eq6VeRuc0PF9Q/a/CQSGf3JJtEi27nY2ePL7UQ/n/plugin/e/137c15c0-84b4-ec8f-9666-012432c11550/i/Microsoft Code Signing PCA 2011/s/Microsoft Corporation  
> (need to change it later after below steps)  
> **Name:** Any app name
>
> **Audience:** api://AzureADTokenExchange (keep it as is)

12. Select **Add**.

<!-- -->

5.  **Provide Monitoring Reader role to your 3P app to access App insights data:  **
    Go to your application insights app, the one you have created in first step.  
    Click on “Access Control (IAM)” tab.  
    Click on “+ Add” button.  
    Search for “Monitoring Reader” role, click on it.  
    then select your 3P app name from search box and click Add.  
   

6.  **PATCH Managed** **Identity record**

To update the **applicationId** and **tenantId** fields on the Managed Identity record, run the following script in your browser console while logged into your D365 environment:

var globalContext = Xrm.Utility.getGlobalContext();

var OrgURL = globalContext.getClientUrl();

var ocConfigAPIURL = OrgURL + "/api/data/v9.0/managedidentities(c9c8f1ca-075c-4ffa-92ce-f4bc1a8a7101)";

fetch(ocConfigAPIURL, {

method: 'PATCH',

body: JSON.stringify({

"applicationid": "Cx 3P app id", // Replace with actual Application ID

"tenantid": "Cx 3P tenant id" // Replace with actual Tenant ID

}),

headers: {

'Content-type': 'application/json; charset=UTF-8'

}

})

.then(res =\> {

if (res.status === 204) {

console.log('PATCH successful!');

} else {

console.log('PATCH error!');

}

});

**Ensure you replace "Cx 3P app id" and "Cx 3P tenant id" with your actual values.**

:::image type="content" source="media/debug-dashboard/image16.png" alt-text="A screenshot of a computer AI-generated content may be incorrect.":::

7.  **Fix FIC path:  **
    Once done with all the above steps, click on Debug tab.  
    Open network tab, search for api name: **msdyn_GetAppInsightsTelemetry** and click on any failed request call.  
    Go to Review and copy the message contents.  
    :::image type="content" source="media/debug-dashboard/image17.png" alt-text="":::  
      
    Now, paste this content in notepad or any text editor and check missing configuration value. You can take a reference from below screenshot:  
    :::image type="content" source="media/debug-dashboard/image18.png" alt-text="":::  
      
    Paste this value in your 3P apps (created in step 3) federated credentials.  
      
    **Done!**

## FAQs

### I am using an unmanaged environment for Dynamics 365 Customer Service and Dynamics 365 Contact Center. Can I use these out-of-the-box dashboards?

No, to set up the out-of-the-box dashboards for Application Insights, you will need a managed environment. More details: [Prerequisites](https://learn.microsoft.com/dynamics365/customer-service/administer/configure-conversation-diagnostics)

### Does my organization need any extra licenses for accessing these dashboards?

Your organization will not need any additional licenses for Dynamics 365 Contact Center or Customer Service. However, you will need an active Azure Monitor subscription for using the out-of-the-box dashboards. More details: [Pricing](https://learn.microsoft.com/dynamics365/customer-service/administer/configure-conversation-diagnostics#pricing)

### I already have an Omnichannel supervisor role assigned. What extra roles or permissions do I need to access these dashboards?

For accessing the out-of-the-box dashboards, the user must have access to Azure monitoring. More details: [Roles and permissions](https://learn.microsoft.com/azure/azure-monitor/fundamentals/roles-permissions-security)

### How often is the data refreshed?

By default, the data is dashboard isn't auto refreshed. However, you can set the auto-refresh interval for your workbook in Application Insights.

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

