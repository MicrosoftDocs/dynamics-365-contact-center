---
title: Set up embedded experience for Dynamics 365 Contact Center
description: Learn about how to set up the embedded experience for Dynamics 365 Contact Center.
author: shwetamurkute
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: get-started
ms.date: 07/01/2024
ms.custom: bap-template
---

# Set up embedded experience for Dynamics 365 Contact Center

The Embeddable Conversation Widget is a feature of the Dynamics 365 Contact Center that allows agents to chat with customers directly from any third-party customer relationship management (CRM) system. The widget can be embedded into any web page or application that supports HTML and JavaScript, and it provides a seamless and consistent chat experience across different platforms.

## Prerequisites

- Set up the prerequisites mentioned in the system requirements. More information: [Prerequisites](../implement/system-requirements-contact-center.md#prerequisites).

- Ensure that the provisioning user has the following permissions:
  - Microsoft 365 Global admin role. More information: [Assign admin roles to user in Microsoft Office 365](https://learn.microsoft.com/microsoft-365/admin/add-users/assign-admin-roles?view=o365-worldwide)
  - Dynamics 365 System Administrator role on the root business unit for your organization. More information: [Assign security roles to a user in Power Platform](https://learn.microsoft.com/power-platform/admin/assign-security-roles) and [Create or edit business units](https://learn.microsoft.com/power-platform/admin/create-edit-business-units)
  - Read-Write access in the Client Access License Information (CAL). More information: [Create a Read-Write user account in Power Platform](https://learn.microsoft.com/power-platform/admin/create-users#create-a-read-write-user-account)
  
- [Set up Omnichannel for Customer Service](https://learn.microsoft.com/dynamics365/customer-service/implement/omnichannel-provision-license#set-up-omnichannel-for-customer-service-)

- Ensure you have CTI Adapter URL, which is available on the Contact Center admin center's welcome page. Alternatively, you can create your embedded widget URL using this template: `https://ccaas-embed-prod.azureedge.net/widget/index.html?dynamicsUrl=https://[ORG_URL]&tenantId=[TENANT_ID]&msdynembedmode=3`. Replace `[ORG_URL]` with your organization's URL (for example, `msdynccaas.crm.dynamics.com`) and `[TENANT_ID]` with your tenant ID (for example, `8cd46c97-38dd-4560-9228-3df8a717a198`).
> [!NOTE]
> If the URL ends with the number 3, it will display the CCaaS widget. If it ends with the number 1, it will display the Copilot for service widget.

## Set up Call Center in Salesforce

1. Sign in to Salesforce.

2. Download the Salesforce installation package by using the following URL template: `https://<sfdc-org-url>/packaging/installPackage.apexp?p0=04t8b000001BV5mAAG`, replacing `<sfdc-org-url>` with your specific Salesforce Org URL. For instance, your Salesforce Org URL might be `flow-power-1788--dev3.sandbox.lightning.force.com`.

3. Select **Install for All Users** and Click **Install**.

4. After the installation is complete, a confirmation screen appears. Click **Done** to continue. A successful installation will display a screen listing **CCaaSforSF** as an installed package.

5. Navigate to the **Setup** by clicking the gear icon in the top right corner.

6. In the **Quick Find** box, search for **Call Center**.

7. Click **Continue** if this is your first time setting up this feature.

8. Edit the call center file by updating the CTI Adapter URL and save your changes.

10. Go to **Manage Call Center Users** > **Add more users**, select the user record that you're currently logged in with and select **Save**.

## Set up Softphone in Salesforce

1. To create a softphone layout:
    1. In the **Quick Find** box, search for **Softphone Layouts**.
    2. Create a new softphone layout or edit an existing one.
    3. Verify that **Is Default Layout** is checked and then select **Save**.

2. To set up the softphone utility for your application, navigate to the **App Manager** in setup and edit the **Service Console** application.

3. Add the softphone utility by going to **Utility Items** and choosing **Open CTI Softphone**.

4. Name your softphone appropriately (for example, "MSFT Omnichannel"), set the width to 400, and the height to 600, then select **Save**.

5. Navigate to the **Service Console** from the **Apps** page.

6. Refresh your browser. You should start seeing the Omnichannel Add-on in your application.

7. To connect Copilot to the CRM system, select "Sandbox" as the Login URI and v58.0 as the Salesforce API Version to set up the third-party CRM connection.

### See also