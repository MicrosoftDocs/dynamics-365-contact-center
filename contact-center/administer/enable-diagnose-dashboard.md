---
title: Enable Diagnose dashboard
description: Learn how to enable the Diagnose dashboard that can help supervisors diagnose and debug issues in automatic routing assignments in Dynamics 365 Contact Center and Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot 
ms.date: 12/15/2025
ms.custom: bap-template
---

# Enable Diagnose dashboard

Supervisors and contact center operators can identify routing issues and uncover the underlying causes of declining performance metrics, such as a high queue backlog or service representatives not being assigned any work, despite having the required presence.

With the debug experience, organizations can access diagnostic telemetry for the full lifecycle of a conversation via Azure Application Insights to effectively troubleshoot runtime issues. This end-to-end data empowers teams to identify problems quickly, apply mitigations, and maintain seamless contact center operations.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature is not intended for use in making—and should not be used to make—decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This also includes adequately notifying end users that their communications with representatives may be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users may be monitored, recorded, or stored.

## Prerequisites

- The System administrator role.

- Application Insights is configured.
- [Conversation diagnostics](/dynamics365/customer-service/administer/configure-conversation-diagnostics) is configured for the environment. Learn more in [](/power-platform/admin/conversation-diagnostics-application-insights#set-up-a-connection-with-azure-application-insights)
- Assignment snapshots in conversation diagnostics is enabled for the environment.

## Pricing

The conversation diagnostics data is stored in Azure Application Insights database. For details on pricing for data storage, refer [Pricing](/dynamics365/customer-service/administer/configure-conversation-diagnostics#pricing).
There’s no additional cost for using Azure workbooks.

## Enable Debug tab experience

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

### I already have an Omnichannel Supervisor role assigned. What extra roles or permissions do I need to access these dashboards?

For accessing the out-of-the-box dashboards, the user must have access to Azure monitoring. Learn more in [Roles and permissions](/azure/azure-monitor/fundamentals/roles-permissions-security).

### How often is the data refreshed?

By default, the data in the dashboard isn't auto refreshed. However, you can set the auto-refresh interval for your workbook in Application Insights.

### Can I export dashboard data?

You can export the dashboard details as JSON from the **Advanced editor** option. However, the dashboard data can't be exported or imported.

### Related information

[Diagnose contact center health](../use/diagnose-dashboard.md)  
[Configure conversation diagnostics](/dynamics365/customer-service/administer/configure-conversation-diagnostics)  