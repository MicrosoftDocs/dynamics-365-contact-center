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

- Channels are provisioned in your environment. Learn more in [provision channels](../implement/provision-channels.md).
- You have an Azure account with an active subscription. Make sure that the Azure subscription and Dynamics 365 account are in the same tenant. Learn more at [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account).
   - Create or use an existing Azure Communication Services resource. Learn more in [Create and manage Communication Services resources](/azure/communication-services/quickstarts/create-communication-resource).
    - Obtain a phone number that can send and receive SMS. You have several options:
       - Purchase a phone number or import one from Azure Communication Services. Learn more in [Get and manage phone number](/azure/communication-services/quickstarts/telephony/get-phone-number) or [import phone numbers](/dynamics365/customer-service/administer/voice-channel-sync-from-acs?context=/dynamics365/contact-center/context/administer-context).
       - Bring a phone number from your provider. Learn more in [Bring your own carrier](/dynamics365/customer-service/administer/voice-channel-bring-your-own-number?context=/dynamics365/contact-center/context/administer-context).
       -    Migrate your existing WhatsApp business accounts with phone number.
   - Set up Advanced Messaging for WhatsApp. Learn more in [Advanced Messaging for WhatsApp in Azure Communication Services](/azure/communication-services/concepts/advanced-messaging/whatsapp/whatsapp-overview) and [Register WhatsApp business account](/azure/communication-services/quickstarts/advanced-messaging/whatsapp/connect-whatsapp-business-account).
   - Set up Event Grid with Microsoft Entra app authentication. Learn more in [Handle Advanced Messaging events](/azure/communication-services/quickstarts/advanced-messaging/whatsapp/handle-advanced-messaging-events) and [Deliver events to Microsoft Entra protected endpoints](/azure/event-grid/secure-webhook-delivery).

## End-to-end walkthrough

1. [Get Azure Communication Services details](#get-azure-communication-services-details).
1. [Create a WhatsApp channel in Dynamics 365 Contact Center](#create-a-whatsapp-channel).
1. [Create a workstream for the WhatsApp channel](#create-a-workstream-for-the-whatsapp-channel).
1. [Set up WhatsApp message templates](#set-up-whatsapp-message-templates).


## Get Azure Communication Services details

You'll need these details when you create the WhatsApp channel in [the following section](#create-a-whatsapp-channel). You might find it helpful to have the Azure portal and the Contact Center admin center or Customer Service admin center open in separate browser tabs and switch back and forth as required.
   
1. Sign in to the [Azure portal](https://ms.portal.azure.com/).

1. Search for and select the Azure Communication Services resource that you created in [Prerequisites](#prerequisites).
 
1. Copy the name of the resource. You'll paste this value in the **ACS resource name** field when you create the WhatsApp channel in the admin center.

1. Select **Events**. Select the event subscription that you created when you set up Advanced Messaging for WhatsApp in [Prerequisites](#prerequisites).

1. Select **Additional features**, and then scroll down to **MICROSOFT ENTRA AUTHENTICATION**.

1. Copy the value of **Microsoft Entra Application ID or URI**. You'll paste this value in the **Event grid app ID** field in the WhatsApp channel settings.

1. Copy the value of **Microsoft Entra Tenant ID**. You'll paste this value in the **Event grid app tenant ID** field in the WhatsApp channel settings.

1. Select **Settings**, and then select **Keys**. Under **Primary key**, select the copy icon to the right of **Connection string**. You'll paste this value in the **ACS connecting string** field in the WhatsApp channel settings.

1. Under **Advanced Messaging**, select **Channels**. Select the copy icon to the right of the **Channel ID** of the channel that you created when you set up Advanced Messaging for WhatsApp in [Prerequisites](#prerequisites). You'll paste this value in the **Channel ID** field in the WhatsApp channel settings.

## Create a WhatsApp channel

You can create a WhatsApp channel in either the Contact Center admin center or the Customer Service admin center.

1. In **Customer support**, select **Channels**.

1. In **Accounts**, select **Manage** for **Messaging accounts**.

1. Select **Add account**.

1. On the **Add account** page, enter a **Name** for your channel, and then in the **Channel** list, select **WhatsApp**.

1. Select the data sharing consent message, and then select **Next**.

1. In the **Provider** list, select **Azure Communication Services (Preview)**.

In the following instructions, you'll provide the information from the Azure portal in [the previous section](#get-azure-communication-services-details).

1. On the **Channel settings** page:

   - **ACS resource name**: Paste the name of the resource.
   - **Event grid app ID**: Paste the **Microsoft Entra Tenant ID**.
   - **Event grid app tenant ID**: Paste the **Microsoft Entra Application or URI**.
   - **ACS connecting string**: Paste the primary key **Connection string**.

1. Select the checkbox to confirm that the Azure Communication Services resource is connected to only one organization, and then select **Next**.

1. Select **Add**, and then enter the following information:

   - **Name**: Enter a name for the channel.
   - **Channel ID**: Paste the **Channel ID** that you copied from the Azure portal.

1. Select **Add**, and then select **Next**.

1. Select **Copy** next to the **Whatsapp webhook URL** box.

1. In the Azure portal, select **Events**. Select the event subscription that you created when you set up Advanced Messaging for WhatsApp in [Prerequisites](#prerequisites).

1. Next to **ENDPOINT**, select **Change**. Paste the **Whatsapp webhook URL** that you copied from the **Callback information** page in the WhatsApp channel settings.

1. Select the **Web Hook** URL, and then select the **Filters** tab.

1. Under **ADVANCED FILTERS**, enter the following information:

   - **Key**: `data.to`
   - **Operator**: **String is in**
   - **Value**: Paste the **Channel ID** from the Azure portal.

1. Select the checkbox to confirm that the WhatsApp channel is set up correctly, and then select **Done**.
               
## Create a workstream for the WhatsApp channel

To configure routing and work distribution, you can create a [workstream](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context) with the **Channel** set to **WhatsApp** or select an existing one.

### Set up WhatsApp message templates

WhatsApp has a constraint known as the 24-hour window. If a WhatsApp user has sent a message, whether it's a communication they initiated or a reply to one of your messages, you have a 24-hour window to send that user messages that don't need to use a template. After the 24-hour window closes, your messages must use an approved template.

You must create WhatsApp message templates before you can add them to your WhatsApp workstream. Learn more in [Send WhatsApp template messages](/azure/communication-services/concepts/advanced-messaging/whatsapp/template-messages). Only text-based message templates can be added to your workstream.

1. In the admin center, edit the WhatsApp workstream.

1. On the **Behaviors** page, under **WhatsApp message templates**, select **Add**.

1. Enter a **Name** for the template.

1. Select the **Default language** from the list.

1. Copy the text from the template that you created in WhatsApp and paste it in **WhatsApp approved text**.

1. Select **Save**.

You can create as many templates as you require.

### Related information

[Configure automated messages](/dynamics365/customer-service/administer/configure-automated-message?context=/dynamics365/contact-center/context/administer-context)   
[Configure a post-conversation survey](/dynamics365/customer-service/administer/configure-post-conversation-survey?context=/dynamics365/contact-center/context/administer-context)  
[Skill-based routing](/dynamics365/customer-service/administer/overview-skill-work-distribution?context=/dynamics365/contact-center/context/administer-context)   
[Create message templates](/dynamics365/customer-service/administer/create-message-templates?context=/dynamics365/contact-center/context/administer-context)   
[Delete a configured channel](/dynamics365/customer-service/administer/delete-channel?context=/dynamics365/contact-center/context/administer-context)   
[Support for live chat and asynchronous channels](/dynamics365/customer-service/administer/card-support-in-channels?context=/dynamics365/card-support-in-channels/context/administer-context)   


