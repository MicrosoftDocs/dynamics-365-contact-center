---
title: Set up the embedded experience in ServiceNow for Dynamics 365 Contact Center 
description: Learn how to set up the embedded experience in ServiceNow for Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection:
ms.date: 05/21/2025
ms.custom: bap-template
---

# Set up the embedded experience in ServiceNow

The embedded conversation widget is a feature of Dynamics 365 Contact Center that allows customer service representatives (service representatives or representatives) to chat or have voice conversations with customers directly from any non-Microsoft customer relationship management (CRM) system. You can embed the widget into a web page or application that supports HTML and JavaScript. Representatives have seamless and consistent conversation experience across different platforms.

## Prerequisites

- The prerequisites mentioned in the system requirements are set up. Learn more in [Prerequisites](../implement/system-requirements-contact-center.md#prerequisites).
- Omnichannel capabilities are enabled in your org. Learn more in [Provision channels](../implement/provision-channels.md).
- The provisioning user has System Administrator permissions in ServiceNow.
- The OpenFrame plugin is installed in your Service now instance. To install it, sign in to ServiceNow, and then search for OpenFrame in **System Definition** > **Plugins**.
- You have the widget URL. To find the embedded widget URL, go to the welcome page of Dynamics 365 Contact Center admin center. Select **Open** under **Your default contact center** and then navigate to the **Conversation widget** tab. The URL is listed under **Integration into third-party systems**.

## Set up the call center in ServiceNow

1. Sign in to ServiceNow.
1. To display the OpenFrame configurations list, navigate to **All** > **OpenFrame** > **Configurations**. 
1. Select **New**.
1. Add the following details to the OpenFrame configuration record:
   - **Name**: Dynamics 365 Contact Center.
   - **Title**: Dynamics 365 Contact Center. 
   - **Width**: 400 
   - **Height**: 700 
   - **URL**: The widget URL that needs to be embedded.

### Related information

[View communication panel](/dynamics365/customer-service/use/oc-conversation-control?context=/dynamics365/contact-center/context/use-context)  
