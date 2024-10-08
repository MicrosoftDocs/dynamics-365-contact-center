---
title: Set up embedded experience for Dynamics 365 Contact Center
description: Learn about how to set up the embedded experience for Dynamics 365 Contact Center.
author: shwetamurkute
ms.author: smurkute
ms.reviewer: smurkute
ms.topic: how-to
ms.collection:
ms.date: 07/01/2024
ms.custom: bap-template
---

# Set up embedded experience for Dynamics 365 Contact Center

The embedded conversation widget is a feature of Dynamics 365 Contact Center that allows agents to chat with customers directly from any non-Microsoft customer relationship management (CRM) system. You can embed the widget into any web page or application that supports HTML and JavaScript, and it provides a seamless and consistent chat experience across different platforms.

## Prerequisites

- Set up the prerequisites mentioned in the system requirements. More information: [Prerequisites](../implement/system-requirements-contact-center.md#prerequisites).
  
- Make sure that the omnichannel capabilities are enabled in your org, see [Provision channels](../implement/provision-channels.md).

- Make sure that the provisioning user has permission to the System Administrator role in Salesforce.

- Make sure that you have the embedded widget URL. To find the embedded widget URL, go to the welcome page of Contact Center admin center. Select **Open** under **Your default contact center**, then navigate to the **Conversation widget** tab. The URL is listed under **Integration into third-party systems**.

## Set up the call center in Salesforce

1. Download the call center definition file from the following location: `https://github.com/microsoft/dynamics-365-contact-center/blob/main/configuration/SFCallCenter/Dynamics365CallCenter.xml`. Make sure that you sign into GitHub to access the file.

1. Open the file, replace the "CTI Adapter URL" with the embedded widget URL, and then save your changes.

1. Sign in to Salesforce.

1. Navigate to the **Setup** by selecting the gear icon in the top-right corner.

1. In the **Quick Find** box, search for **Call Center**.

1. Select **Continue** if you are setting up the feature for the first time.

1. Select **Import** and select the call center definition file.

1. Go to **Manage Call Center Users** > **Add more users**, select the user record that you are currently signed in with and select **Save**.

## Set up a softphone in Salesforce

1. To create a softphone layout:
    1. In the **Quick Find** box, search for **Softphone Layouts**.
    2. Create a new softphone layout or edit an existing one.
    3. Verify that **Is Default Layout** is selected and then select **Save**.
    
1. To set up the softphone utility for your application, navigate to the **App Manager** in setup and edit the **Service Console** application.

1. Go to **Utility Items** and select **Open CTI Softphone** to add the softphone utility.

1. Name your softphone appropriately (for example, "MSFT Omnichannel"), set the width to 400, and height to 600, then select **Save**.

1. Navigate to the **Service Console** from the **Apps** page.

1. Refresh your browser. The embedded widget appears in your application.

1. To connect Copilot to the CRM system, select the required sign in URI and v58.0 as the Salesforce API Version to set up the non-Microsoft CRM connection.

### Related information

[View communication panel](/dynamics365/customer-service/use/oc-conversation-control?context=/dynamics365/contact-center/context/use-context)  
