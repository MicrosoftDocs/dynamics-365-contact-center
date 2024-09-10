---
title: Configure a WhatsApp channel through Azure Communication Services (preview)
description: Use this article to learn how to configure the WhatsApp channel through Azure Communication Services.
ms.date: 09/10/2024
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.collection:
ms.custom: bap-template
---

# Configure a WhatsApp channel through Azure Communication Services (preview)

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

> [!IMPORTANT]
> This is a preview feature.
> Preview features aren’t meant for production use and might have restricted functionality. To sign up to use this feature, fill out [this](https://forms.office.com/r/xu3K2hDic1) form.

The success of social media customer service, like all other customer services, depends on the quality of customer care provided. Communications from agents should be timely, accurate, sensitive, brief, and friendly, which ultimately improves customer satisfaction and brand loyalty. To enhance customer satisfaction and improve communications, the omnichannel capability in the application enables you to send and receive WhatsApp messages using [Azure Communication Services](/azure/communication-services). You can use the WhatsApp channel feature to engage in conversations with customers for product inquiry and customer service scenarios with those who prefer to communicate using WhatsApp. 


## Prerequisites

- Make sure channels are provisioned in your environment. Learn more in [provision channels](../implement/provision-channels.md).
- Have an Azure account with an active subscription. Make sure that the Azure subscription and Dynamics 365 account are in the same tenant. Learn more at [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account).
   - Create or use an existing Azure Communication Services resource. Learn more at [Create and manage Communication Services resources](/azure/communication-services/quickstarts/create-communication-resource).
    - Obtain a phone number that can send and receive SMS. The following are supported:
       - Purchase a [phone number](/azure/communication-services/quickstarts/telephony/get-phone-number) or [import phone numbers](/dynamics365/customer-service/administer/voice-channel-sync-from-acs?context=/dynamics365/contact-center/context/administer-context)
       - [Bring your own phone number from existing providers](/dynamics365/customer-service/administer/voice-channel-bring-your-own-number?context=/dynamics365/contact-center/context/administer-context) or migrate your existing WhatsApp business accounts with phone number.
   - [Advanced Messaging for WhatsApp](/azure/communication-services/concepts/advanced-messaging/whatsapp/whatsapp-overview) is set up in Azure Communication Services. Perform the steps in [register WhatsApp business account](/azure/communication-services/quickstarts/advanced-messaging/whatsapp/connect-whatsapp-business-account).
   - Configure [Event Grid](/azure/communication-services/quickstarts/advanced-messaging/whatsapp/handle-advanced-messaging-events) with Microsoft Entra app authentication. Learn more at [Secure WebHook delivery with Microsoft Entra ID in Azure Event Grid](/azure/event-grid/secure-webhook-delivery).

## End-to-end walkthrough

1. Get Azure Communication Services details to connect.
2. Create a WhatsApp channel.
3. Create routing rules.
4. Modify settings for a specific WhatsApp phone number.<br>


> [!VIDEO https://www.youtube.com/embed/tYS0qcv-8Jc]


## Fetch Azure Communication Services details

Copy the following information from the [Azure portal](https://ms.portal.azure.com/). You need these details to configure the WhatsApp channel through Contact Center admin center or Customer Service admin center.
   
   1. Go to **Resource groups** and select the required resource group. 
   1. Select the required **Resource** from the resource group.
   1. Select **Properties** in **Settings**. 
   1. On the **Properties** page, copy the **Name**. 
   1. Select **Keys** in **Settings**. On the **Keys** page, copy **Connection string** in **Primary key**.
   1. Select **Events**. Select the event subscription you created as a part of setting up advanced messaging for WhatsApp in [Prerequisites](#prerequisites).
   1. Select **Additional features** in the **Event Subscription** page. 
   1. In **MICROSOFT ENTRA AUTHENTICATION**, copy the **Microsoft Entra Tenant ID** and **Microsoft Entra Application ID or URI** values.
   1. Select **Channels** in **Advanced Messaging**. Copy the **Channel ID** corresponding to the channel you created as a part of setting up advanced messaging for WhatsApp in [Prerequisites](#prerequisites).

## Create a WhatsApp channel

1. In the site map of Contact Center admin center or Customer Service admin center, select **Channels** in **Customer support**. The **Channels** page appears.
    
1. Select **Manage** for **Messaging accounts**. The **Accounts and channels** page appears.
   
1. Select the required **Provider**. Based on your selection, specify the following details.
 
    You must specify the information you copied from [Fetch Azure Communication Services details](#fetch-azure-communication-services-details).
    
     1. In the **Channel settings** page, specify the following. 
         - **ACS resource name**: The **Name** of the resource.
         - **ACS connection string**: The **Connection string** corresponding to the resource.
         - **Event grid app ID**: **Microsoft Entra Tenant ID**.
         - **Event grid app tenant ID**:  **Microsoft Entra Application  or URI**.
         - Select the check box to confirm that the Azure Communication Services resource is connected only to one organization.
     1. In the **WhatsApp channel ID**, select **Add**, and on the page that appears, enter the following information:
         - **Name**: Specify a name.
         - **Channel ID**: Specify the **Channel ID** for the WhatsApp channel you created in Azure Communication Services.
     1. On the **Callback information** page, copy the value in the **WhatsApp inbound URL** box to use in the Azure Communication Services event grid.
     1. Perform the following steps in Azure portal to add the webhook information and configure filters based on the channel id:
        1. In the **Events** page, select the event subscription that you created as a part of the [Advanced Messaging for WhatsApp](/azure/communication-services/concepts/advanced-messaging/whatsapp/whatsapp-overview) setup in Azure Communication Services.
        1. In the Event Subscription page > **Endpoint** select **Change** for the endpoint and add the **WhatsApp inbound URL** that you copied from the **Callback information** page in the WhatsApp channel setup.
        1. Select the webhook URL and then select **Filters**.
        1. In the **ADVANCED FILTERS** section, specify the following:
           - **Key**: data.to
           - **Operator**: String is in
           - **Value**:  Specify the **Channel ID** for the WhatsApp channel you created in Azure Communication Services.
     1. Select the check box to confirm that the WhatsApp channel is set up correctly and then select **Done**.
               
## Configure a workstream for the WhatsApp channel

To configure routing and work distribution, you can create a [workstream](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context) with the **Channel** set to **WhatsApp** or select an existing one.

### Configure WhatsApp message templates

You can configure the option for agents to send WhatsApp-approved messages. If 24 hours pass after a customer's last message, agents will only be able to send messages from WhatsApp-approved templates until the customer responds. You must perform the steps in Send WhatsApp template messages to send WhatsApp Template messages using Advanced Communication Messages SDK before you add them in the application.

> [!NOTE]
> Text-based message templates only are supported.

Perform the following steps:

1. For the selected workstream for WhatsApp, edit the WhatsApp account.
2. On the **Behaviors** tab, in **WhatsApp message templates**, select **Add**.
3. On the **Add message template** dialog box, do the following:
   - **Name:** Specify a name for the template.
   - **Default language:** Select the language from the list.
   - **WhatsApp approved text:** Copy and paste the approved text from the template that you created in WhatsApp.
4. Select **Save**.
5. Create as many templates as required.


### Related information

[Configure automated messages](/dynamics365/customer-service/administer/configure-automated-message?context=/dynamics365/contact-center/context/administer-context)   
[Configure a post-conversation survey](/dynamics365/customer-service/administer/configure-post-conversation-survey?context=/dynamics365/contact-center/context/administer-context)  
[Skill-based routing](/dynamics365/customer-service/administer/overview-skill-work-distribution?context=/dynamics365/contact-center/context/administer-context)   
[Create message templates](/dynamics365/customer-service/administer/create-message-templates?context=/dynamics365/contact-center/context/administer-context)   
[Delete a configured channel](/dynamics365/customer-service/administer/delete-channel?context=/dynamics365/contact-center/context/administer-context)   
[Support for live chat and asynchronous channels](/dynamics365/customer-service/administer/card-support-in-channels?context=/dynamics365/card-support-in-channels/context/administer-context)   


