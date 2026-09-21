---
title: Configure an SMS channel for Infobip in Dynamics 365 Contact Center
description: Learn how to configure an SMS channel for Infobip in Dynamics 365 Contact Center to connect with customers using text messages.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.date: 09/21/2026
ms.custom: bap-template
---

# Configure an SMS channel for Infobip

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]  

The SMS channel through Infobip allows your organization to connect with your customers by using text messages. Your customers can send text messages through Infobip and connect with a customer service representative (service representative or representative). Service representatives can view incoming SMS requests on their dashboard and respond accordingly.

## Prerequisites

Make sure that the following prerequisites are met:

- SMS for Infobip is provisioned in Copilot Service admin center. Learn more in [Provision channels](../implement/provision-channels.md).
- An active Infobip account with a provisioned SMS phone number is available. To request access or acquire a phone number, contact the Infobip account owner.
- Permissions on the secure columns are configured. Learn more in [Configure permissions to access secure columns](/dynamics365/customer-service/implement/add-users-assign-roles#configure-permissions-to-access-secure-columns).
- The **Organization ID** of the Dynamics 365 environment where you want to configure the SMS channel. Learn more in [Find your environment and organization IDs](/power-platform/admin/determine-org-id-name). Use the organization ID, not the environment ID, tenant ID, or Microsoft Entra application ID.

## Get Infobip account details

You enable an SMS channel within the application that's integrated with Infobip. This integration uses the API Base URL to send and receive text messages. Complete the following steps in the Infobip portal.

1. Sign in to the [Infobip portal](https://portal.infobip.com/) and note the **API Base URL**.

1. Go to **Developer tools** > **Applications and entities** > **Applications**, and select **Create application**. Set **Application ID** to the organization ID from the first step, and create the application.
1. Go to **Channels and numbers** > **Numbers** > **My numbers**, and select your SMS phone number. In its general settings, associate the number with the application you created, and save the changes.
1. Create an API key with the `message:send` scope, and save it securely. Use this key and the **API Base URL** to configure the messaging account in Copilot Service admin center. You also use the same key for HMAC authentication in the following connection setup.

> [!NOTE]
> To make sure that non-Microsoft SMS providers handle opt-out commands properly, you must configure your consent settings with the provider directly.

## Set up the SMS channel for Infobip

In Copilot Service admin center, complete the following tasks to configure the SMS channel:

- Configure SMS via Infobip account
- Configure workstream for the SMS channel

### Configure the SMS number via Infobip account

1. In the site map of Copilot Service admin center, go to **Customer support**, and then select **Channels**.
1. In **Accounts**, for **Messaging accounts**, select **Manage**.
1. On the **Accounts and channels** page, select **New account**.
1. Enter the following details:
   1. In **Channel details**, enter a name, and select **SMS** in **Channel**.
   1. In **Account details**, select **Infobip** in **Provider**, and then enter the following details:
      - **API Base URL**: Enter the base URL from your Infobip account.
      - **API Key**: Enter the API key from your Infobip account.
   1. In **SMS phone numbers**, select **Add**, and enter the following details in **Add SMS number**:
      - **Number**: Specify the SMS phone number provisioned in your Infobip account in the `<country_code><phone_number>` format, such as `14252306549`. Make sure that you don't enter blank spaces or special characters.
      - **Type**: Select **Long code**, **Short code**, or **Toll free**.
      - **Description**: Specify a description for the number. (Optional)
   1. In **Callback information**, copy the callback URL. The copied URL is used in the Infobip notification profile.
1. Select **Done**. The account is configured.

### Configure workstream for the SMS channel

To configure the workstream, make sure you perform the steps to create a workstream for the SMS channel. Learn more in [Create workstreams](/dynamics365/customer-service/administer/create-workstreams).

1. Go to the workstreams page and open the workstream you created for the channel.
1. In the **Set up your SMS channel** section, select **Set up SMS**, and then configure the following options:
   1. On the **SMS setup** page, select a number from the list.
   1. On the **Language** page, select the language that you want to set as the default.
   1. On the **Behaviors** page, configure the following options:
      - **Channel operation hours**: Set the toggle to **On**, and then select an operating hour record. Learn more in [Configure operating hours](/dynamics365/customer-service/administer/create-operating-hours).
      - **Custom automated messages**
      - **Post-conversation survey**
   1. In **User features**, set the toggle for **File attachments** to **On** and select the following options if you want both representatives and customers to exchange files. Learn more in [Enable file attachments](/dynamics365/customer-service/administer/enable-file-attachments).
      - **Customers can send file attachments**
      - **Representatives can send file attachments**
   1. Verify the settings on the **Summary** page, and then select **Finish**. The SMS for Infobip channel is configured.
1. Configure routing rules. Learn more in [Configure work classification](/dynamics365/customer-service/administer/configure-work-classification).
1. Configure work distribution. Learn more in [Work distribution settings](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution).
1. Add an AI agent. Learn more in [Configure an agent](/dynamics365/customer-service/administer/create-workstreams#add-an-agent-to-a-workstream).
1. In **Advanced settings**, configure the following options based on your business needs:
   - Sessions
   - [Representative notifications](/dynamics365/customer-service/administer/notification-templates#out-of-the-box-notification-templates)
   - [Context variables](/dynamics365/customer-service/administer/manage-context-variables)  
   - [Smart assist agents](/dynamics365/customer-service/develop/smart-assist-bot)  
   - [Quick replies](/dynamics365/customer-service/administer/create-quick-replies)

## Establish a connection between the omnichannel application and Infobip

After you configure the messaging account, complete the following steps to receive incoming messages and delivery notifications.

### Configure HMAC authentication

1. In the Infobip portal, go to **Developer tools** > **Subscriptions Management** > **Authentication settings**.
1. Select **Create authentication settings**, enter a name, and select **HMAC** as the authentication type.
1. Use the same API key that you entered in Copilot Service admin center as the secret key.
1. Select `HMAC_SHA_512` (recommended) as the algorithm. `HMAC_SHA_384` and `HMAC_SHA_256` are also supported.
1. Save the authentication settings.

### Configure the notification profile

1. In Copilot Service admin center, copy the callback URL from **Callback information** in the messaging account setup.
1. In the Infobip portal, go to **Subscriptions Management** > **Notification profiles**, select **Create notification profile**, and enter a name.
1. In the **Webhook URL** field of the notification profile, paste the callback URL copied in step 1.
1. Under **Security settings**, select the HMAC authentication settings you created, and save the profile.

### Configure the SMS subscription

1. In the Infobip portal, go to **Developer tools** > **Subscriptions Management** > **Subscriptions**, select **Create subscription**, choose **SMS** under **Channels**, and enter a subscription name and ID.
1. Select the following events and formats:
   - **Inbound message**: `inbound-message.sms.v2.json`
   - **Delivery**: `delivery.sms.v5.json`
1. In the application filter, select the application whose **Application ID** matches your Dynamics 365 organization ID.
1. Select the notification profile you created, and save the subscription.
1. Return to **Channels and numbers** > **Numbers** > **My numbers**, and select your SMS number. Verify that its general settings reference the same application.
1. On the **SMS** tab, set the default inbound forwarding action to **Apply subscription** so that incoming messages use the subscription. Learn more in [Manage numbers](https://www.infobip.com/docs/resources-and-numbers/manage-resources).

To verify the setup, send an SMS to the configured number, confirm that it reaches a service representative, and reply from the conversation. If messages don't arrive, check the number's application assignment, the subscription's application filter and events, the default inbound forwarding action, and that the HMAC secret matches the API key in the messaging account.

## Flow of data between the omnichannel application and Infobip

### Incoming text messages

For an incoming text message sent by a customer to the SMS phone number, the message is first sent to the Infobip messaging service. Infobip then pushes it to the omnichannel application by using the configured webhook URL. The message is then routed and associated to either a new or an existing conversation by the application.

### Outgoing text messages

For an outgoing message sent by the contact center from within the application, the message is first sent to the Infobip service and then Infobip sends it to the customer. Apart from the text message, the application uses the APIs provided by Infobip to send the customer's phone number, SMS phone number, and the Infobip account information (API Base URL and API Key) to the Infobip service.

## Related information

[Overview of SMS channels](/dynamics365/customer-service/administer/sms-channel-overview)  
[Configure an SMS channel using Azure Communication Services](/dynamics365/customer-service/administer/configure-sms-channel-acs)  
[Infobip messaging API documentation](https://www.infobip.com/docs/api)  
[Delete a configured channel](/dynamics365/customer-service/administer/delete-channel)  
[SMS FAQ](/dynamics365/customer-service/administer/faqs#sms)  
