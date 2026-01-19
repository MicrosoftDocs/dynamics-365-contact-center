---
title: Enable Diagnose dashboard
description: Learn how to enable the Diagnose dashboard that can help supervisors diagnose and debug issues in automatic routing assignments in Dynamics 365 Contact Center and Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot 
ms.date: 01/19/2026
ms.custom: bap-template
---

# Enable Diagnose dashboard

Supervisors and contact center operators can identify routing issues and uncover the underlying causes of declining performance metrics, such as a high queue backlog or service representatives not being assigned any work, despite having the required presence.

With the debug experience, organizations can access diagnostic telemetry for the full lifecycle of a conversation via Azure Application Insights to effectively troubleshoot runtime issues. This end-to-end data empowers teams to identify problems quickly, apply mitigations, and maintain seamless contact center operations.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature is not intended for use in making—and should not be used to make—decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This also includes adequately notifying end users that their communications with representatives may be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users may be monitored, recorded, or stored.

## Prerequisites

- The System administrator role.

- Configure the prerequisite settings mentioned in the subsections.

### Configure Application Insights

Configure an [Application Insights resource](/azure/azure-monitor/app/create-workspace-resource?tabs=portal#create-an-application-insights-resource) where the Dynamics 365 Contact Center telemetry data can be saved.

### Configure conversation diagnostics and connection

Configure [conversation diagnostics](/dynamics365/customer-service/administer/configure-conversation-diagnostics) for the environment and [set up a connection with Azure Application Insights](/power-platform/admin/conversation-diagnostics-application-insights#set-up-a-connection-with-azure-application-insights). This connection is used by Dynamics 365 Contact Center to connect with the Application Insights instance and push data from the Dynamics instance into Application Insights.

### Update Application Insights ID in environment variable

Update the Application insights ID in the **Default Value** and **Current Value** fields of the environment variable. This is required by Dataverse to access the Dynamics 365 Contact Center telemetry data from the Application Insights instance. Learn more in [Environment variables for Power Platform](/power-apps/maker/data-platform/environmentvariables#manually-create-an-environment-variable-in-a-solution).

### Create and register an app

1. Create and register an app for your tenant. The app is required to authorize Dataverse to access the telemetry data in Application Insights. Learn more in [Register an application](/entra/identity-platform/quickstart-register-app#register-an-application).

1. Copy the **Application (client) ID** and **Directory (tenant) ID**, and save them in a secure location like a Notepad file to update the managed identity record.

**Configure federated identity credentials**

[Configure federated identity credentials](/power-platform/admin/set-up-managed-identity#configure-federated-identity-credentials) with the following details:

- **Issuer**: `https://login.microsoftonline.com/{tenant_id}/v2.0`. Replace {tenant_id} with your Tenant ID.

- **Type**: Explicit subject identifier
- **Value**: `/eid1/c/pub/t/urwIj5vn7Eq6VeRuc0PF9Q/a/CQSGf3JJtEi27nY2ePL7UQ/n/plugin/e/137c15c0-84b4-ec8f-9666-012432c11550/i/Microsoft Code Signing PCA 2011/s/Microsoft Corporation`. You'll update the value in a subsequent step.
- **Name**: App name
- **Audience**: `api://AzureADTokenExchange`

**Assign Monitoring Reader role**

Assign the **Monitoring Reader** role to your app to access App insights data. Learn about assigning roles in [Assign Azure roles using the Azure portal](/azure/role-based-access-control/role-assignments-portal) and about roles in [Roles, permissions, and security in Azure Monitor](/azure/azure-monitor/fundamentals/roles-permissions-security#monitoring-reader).

**Update managed identity record**

Run the following script in your browser console after you sign in to your Dynamics 365 environment.

```javascript
var globalContext = Xrm.Utility.getGlobalContext();
var OrgURL = globalContext.getClientUrl();
var ocConfigAPIURL = OrgURL + "/api/data/v9.0/managedidentities(c9c8f1ca-075c-4ffa-92ce-f4bc1a8a7101)";     
fetch(ocConfigAPIURL, {
    method: 'PATCH',
    body: JSON.stringify({
        "applicationid": "Cx 3P app id", // Replace with actual Application ID that you copied when you registered the app.
        "tenantid": "Cx 3P tenant id"    // Replace with actual Tenant ID that you copied when you registered the app.
    }),
    headers: {
       'Content-type': 'application/json; charset=UTF-8'
    }
})
.then(res => {
    if (res.status === 204) {
        console.log('PATCH successful!');
    } else {
        console.log('PATCH error!');
    }
});
```

**Fix federated identity credentials path**

1. In Copilot Service workspace, open the browser console, go to the **Network** tab, search for `msdyn_GetAppInsightsTelemetry`, and select a failed request call.

1. Select the **Debug** tab on the **Diagnose** dashboard.
1. On the **Network** tab, go to **Preview**, copy the message contents and paste in a Notepad.
1. Check for any missing configuration value. Paste the value in the federated credentials > **Value** field. Make sure that there are no special characters or spaces in the value.

## Pricing

The conversation diagnostics data is stored in Azure Application Insights database. For details on pricing for data storage, refer [Pricing](/dynamics365/customer-service/administer/configure-conversation-diagnostics#pricing).

There’s no additional cost for using Azure workbooks.

## Enable Debug tab experience for Diagnose dashboard

1. In Power Apps, go to the Default Solution or the solution in which you want to enable the dashboard.
1. In **Objects**, go to **Setting** > **Setting definition**.
1. Search for **Enable Application Insights Dashboard** app setting.
1. Select **Yes** in the **Default value** and **Setting environment value** fields.
1. Save and close.

## FAQ

### I am using an unmanaged environment for Dynamics 365 Customer Service and Dynamics 365 Contact Center. Can I use these out-of-the-box dashboards?

No. To set up the out-of-the-box dashboards for Application Insights, you need a managed environment. Learn more in [Prerequisites](/dynamics365/customer-service/administer/configure-conversation-diagnostics)

### Does my organization need any extra licenses for accessing these dashboards?

Your organization doesn't need any extra licenses for Dynamics 365 Contact Center or Customer Service. However, you need an active Azure Monitor subscription for using the out-of-the-box dashboards. learn more in **Pricing**.

### How often is the data refreshed?

By default, the data in the dashboard isn't auto refreshed. Use the **Refresh** button for a manual refresh.

### Related information

[Diagnose contact center health](../use/diagnose-dashboard.md)  
[Configure conversation diagnostics](/dynamics365/customer-service/administer/configure-conversation-diagnostics)  