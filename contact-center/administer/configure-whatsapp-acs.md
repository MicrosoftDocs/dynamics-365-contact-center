---
title: Configure a WhatsApp channel through Azure Communication Services 
description: Use this article to learn how to configure the WhatsApp channel through Azure Communication Services.
ms.date: 10/14/2026
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.collection:
ms.custom: bap-template
---

# Configure a WhatsApp channel through Azure Communication Services 

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

The success of social media customer service, like all other customer services, depends on the quality of customer care provided. Communications from customer service representatives should be timely, accurate, sensitive, brief, and friendly, which ultimately improves customer satisfaction and brand loyalty. 

To enhance customer satisfaction and improve communications, the omnichannel capability in the application enables you to send and receive WhatsApp messages using [Azure Communication Services](/azure/communication-services). You can use the WhatsApp channel feature to engage in conversations with customers for product inquiry and customer service scenarios with those who prefer to communicate using WhatsApp. 

> [!IMPORTANT]
> - [!INCLUDE[Deprecation of Azure Communication Services](../includes/cc-acs-deprecation.md)]
> - From June 2026, usernames and a new customer identifier called the Business-Scoped User ID are being released for WhatsApp. For updates on the timeline for this change, refer to [WhatsApp Business-Scoped User IDs](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids/) in the Meta documentation.
> - A Business-Scoped User ID will be assigned to every WhatsApp user that interacts with your organization. When a user adopts a WhatsApp username, their phone number is no longer be sent, and their Business-Scoped User ID becomes the primary identifier.
> - With this change, the Contact Book is enabled by default for your business WhatsApp account. By keeping your Contact Book enabled, you preserve your ability to identify customers by phone number even after they adopt a username. If you disable the Contact Book, the phone number is permanently lost as an identifier for the WhatsApp customer.
> - After a customer’s phone number is no longer available, the system displays their first and last name if linked to a contact record. Otherwise, the customer shows "Visitor."
> - **What action do I need to take?**
>   - Review your routing rules. Any custom routing rules that have conditions on phone number patterns like country/region code–based routing don't match Business-Scoped User ID-only conversations. Add a fallback rule to route these conversations correctly. Business-Scoped User ID is prefixed with a two-letter country code and a period, followed by up to 128 alphanumeric characters (for example, US.13491208655302741918).
>   - Review any integrations or automation workflows, such as like Power Automate flows, that rely on phone numbers for customer identification and update them to handle Business-Scoped User ID. 
>   - Review context variables in your AI agents. If you use msdyn_CustomerPhoneNumber in your AI agent configuration, update your logic to also handle scenarios where only the Business-Scoped User ID is available.<br>
> Learn more in [WhatsApp usernames and business-scoped user IDs (BSUID)](/azure/communication-services/concepts/advanced-messaging/whatsapp/whatsapp-username-support-overview).

## Prerequisites

- Channels are provisioned in your environment. Learn more in [provision channels](../implement/provision-channels.md).
- Make sure that the Azure subscription and Dynamics 365 account are in the same tenant.

### Setup advanced messaging for WhatsApp

- Register and connect your [WhatsApp Business Account through Azure Communication Services](/azure/communication-services/quickstarts/advanced-messaging/whatsapp/connect-whatsapp-business-account) in the Azure portal.

### Setup Event Grid

Complete the following checklist before connecting Event Grid to Contact Center:

- Register a single-tenant Microsoft Entra application for the webhook, or identify the existing webhook application that you plan to use. See [Register an application](/entra/identity-platform/quickstart-register-app).
- Record the webhook application's **Application (client) ID** and **Directory (tenant) ID**. Use these same values in Contact Center and both event subscriptions, as described in [Get Azure Communication Services details](#get-azure-communication-services-details).
- Complete the application permissions and role assignments in [Deliver events to a webhook in the same Microsoft Entra tenant](/azure/event-grid/secure-webhook-delivery#deliver-events-to-a-webhook-in-the-same-microsoft-entra-tenant). Follow the instructions for the identity that creates the subscriptions: a user or an application. The webhook application and the subscription writer have different roles; don't substitute the writer's application ID for the webhook application's ID.
- Review the [Advanced Messaging event setup](/azure/communication-services/quickstarts/advanced-messaging/whatsapp/handle-advanced-messaging-events). Configure both inbound-message and outbound delivery-status subscriptions by using the Contact Center webhook URL you get during [channel creation](#create-a-whatsapp-channel), not the sample Event Grid Viewer endpoint.
- If your webhook authentication requires the app-only token type claim, configure the webhook application's access tokens to include `idtyp`. See [Check the app-only access-token claim](#check-the-app-only-access-token-claim).

> [!IMPORTANT]
> Creating an event subscription or passing endpoint validation doesn't prove that message events authenticate and get processed. Complete the [channel verification steps](#verify-your-whatsapp-channel) after setup.

## End-to-end walkthrough

1. [Get Azure Communication Services details](#get-azure-communication-services-details).
1. [Create a WhatsApp channel in Dynamics 365 Contact Center](#create-a-whatsapp-channel).
1. [Create a workstream for the WhatsApp channel](#create-a-workstream-for-the-whatsapp-channel).
1. [Set up WhatsApp message templates](#set-up-whatsapp-message-templates).
1. [Verify your WhatsApp channel](#verify-your-whatsapp-channel).

## Get Azure Communication Services details

Gather the following details before you create the WhatsApp channel in [the following section](#create-a-whatsapp-channel). You might find it helpful to have the Azure portal and the Copilot Service admin center open in separate browser tabs.

1. Sign in to the [Azure portal](https://ms.portal.azure.com/).

1. Search for and select the Azure Communication Services resource that you created in [Prerequisites](#prerequisites).

1. Copy the name of the resource. You'll paste this value in the **ACS resource name** field when you create the WhatsApp channel in the admin center.

1. Open the webhook application’s registration in Microsoft Entra ID. Copy its **Application (client) ID** and **Directory (tenant) ID**. Use these values in the WhatsApp channel settings and in **Additional features** > **Microsoft Entra authentication** for both Event Grid subscriptions.

1. Return to the Communication Services resource. Select **Settings**, and then select **Keys**. Under **Primary key**, select the copy icon to the right of **Connection string**. Paste this value in the **ACS connecting string** field in the WhatsApp channel settings.

1. Under **Advanced Messaging**, select **Channels**. Select the copy icon to the right of the **Channel ID** of the channel that you created when you set up Advanced Messaging for WhatsApp in [Prerequisites](#prerequisites). Paste this value in the **Channel ID** field in the WhatsApp channel settings.

## Create a WhatsApp channel

Use the following mapping when you configure the channel and its event subscriptions. For this setup, use the webhook application's client ID GUID in the Event Grid field, even though the field also allows an application ID URI.

| Value | Contact Center channel setting | Setting in both Event Grid subscriptions |
|-------|--------------------------------|-----------------------------------------|
| Webhook application's **Application (client) ID** | **Event grid app ID** | **Microsoft Entra Application ID or URI** |
| Webhook application's **Directory (tenant) ID** | **Event grid app tenant ID** | **Microsoft Entra Tenant ID** |
| Contact Center **Whatsapp webhook URL** | Copy from **Callback information** | **Web Hook** endpoint URL |

The application ID identifies the intended audience of the webhook access token. It isn't the application object's **Object ID**, the subscription writer's application ID, or the Azure Event Grid service application's ID. The WhatsApp **Channel ID** is a separate value used for channel selection and event filtering.

> [!IMPORTANT]
> Before you create a WhatsApp channel in Dynamics 365 Contact Center, make sure your [WhatsApp business account is registered](#setup-advanced-messaging-for-whatsapp) and connected through Azure Communication Services in the Azure portal.


Create a WhatsApp channel in Copilot Service admin center.

1. In **Customer support**, select **Channels**.

1. In **Accounts**, select **Manage** for **Messaging accounts**.

1. Select **Add account**.

1. On the **Add account** page, enter a **Name** for your channel, and then in the **Channel** list, select **WhatsApp**.

1. Select the data sharing consent message, and then select **Next**.

1. In the **Provider** list, select **Azure Communication Services**.

In the following instructions, you provide the information from the Azure portal in [the previous section](#get-azure-communication-services-details).

1. On the **Channel settings** page:

   - **ACS resource name**: Paste the name of the resource.
   - **Event grid app ID**: Paste the webhook application's **Application (client) ID**.
   - **Event grid app tenant ID**: Paste the webhook application's **Directory (tenant) ID**.
   - **ACS connecting string**: Paste the primary key **Connection string**.

1. Select the checkbox to confirm that the Azure Communication Services resource is connected to only one organization, and then select **Next**.

1. Select **Add**, and then enter the following information:

   - **Name**: Enter a name for the channel.
   - **Channel ID**: Paste the **Channel ID** that you copied from the Azure portal.

1. Select **Add**, and then select **Next**.

1. Select **Copy** next to the **Whatsapp webhook URL** box.

1. In the Azure portal, open the Communication Services resource and select **Events**. Select an existing inbound-message event subscription, or create one on the resource's Event Grid system topic.

1. Set the endpoint type to **Web Hook** and paste the **Whatsapp webhook URL** that you copied from **Callback information**. For an existing subscription, select **Change** next to **ENDPOINT**. Under **Additional features**, enable **Microsoft Entra authentication** and enter the webhook application's client ID and tenant ID from the mapping table.

1. Select only **Microsoft.Communication.AdvancedMessageReceived** as the inbound subscription's event type. On the **Filters** tab, configure the channel filter shown in the following table, and save the subscription.

1. On the same Event Grid system topic, create a second subscription for outbound delivery-status updates. Give it a distinct name, such as `whatsapp-<channel-name>-delivery-status`. Enable Microsoft Entra authentication and use the same webhook URL, webhook application client ID, and tenant ID as the inbound subscription. Select only **Microsoft.Communication.AdvancedMessageDeliveryStatusUpdated** as its event type. Configure its channel filter using the following table, and save the subscription.

1. Compare the channel filters for both subscriptions with the following table. Keep the event types specified in the preceding steps. For each channel filter, use **Advanced filters** on the **Filters** tab and select the **String is in** operator:

   | Subscription | Channel filter key | Filter value |
   |--------------|--------------------|--------------|
   | Inbound messages | `data.to` | WhatsApp **Channel ID** |
   | Outbound delivery status | `data.from` | The same WhatsApp **Channel ID** |

   Don't copy the inbound `data.to` filter into the delivery-status subscription. In a delivery-status event, `data.from` identifies the sending channel; `data.to` identifies the recipient. See [Advanced Messaging event schemas](/azure/event-grid/communication-services-advanced-messaging-events).

   > [!IMPORTANT]
   > - Both subscriptions are required. Without the outbound delivery-status subscription, the application won't receive delivery, read, or failure updates for outbound WhatsApp messages, and representatives won't see delivery failure notifications in the conversation.
   > - If your Azure Communication Services resource contains only one WhatsApp channel that isn't shared with other channels or workloads, you can skip configuring the advanced filters for both subscriptions. You can filter by event type. Use the `data.to` and `data.from` filters only when the same ACS resource is shared across multiple channels or workloads.

1. Return to Contact Center, select the checkbox to confirm that the WhatsApp channel is set up correctly, and then select **Done**.

## Create a workstream for the WhatsApp channel

To configure routing and work distribution, create a [workstream](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context) with the **Channel** set to **WhatsApp** or select an existing one.

## Set up WhatsApp message templates

WhatsApp uses a 24-hour messaging window. If a WhatsApp user has sent a message, whether it's a communication they initiated or a reply to one of your messages, you have a 24-hour window to send that user messages that don't need to use a template. After the 24-hour window closes, you can only send messages by using an approved template.

You must create WhatsApp message templates before you can add them to your WhatsApp workstream. Learn more in [Send WhatsApp template messages](/azure/communication-services/concepts/advanced-messaging/whatsapp/template-messages). Only text-based message templates can be added to your workstream.

1. In the admin center, edit the WhatsApp workstream.

1. On the **Behaviors** page, under **WhatsApp message templates**, select **Add**.

1. Enter a **Name** for the template.

1. Select the **Default language** from the list.

1. Copy the text from the template that you created in WhatsApp and paste it in **WhatsApp approved text**.

1. Select **Save**.

Create as many templates as you require.

## Verify your WhatsApp channel

Use a test recipient who agrees to receive your test messages. Verify inbound messages, outbound messages, and delivery-status processing separately.

1. **Check both subscriptions.** Confirm that they use the same system topic, Contact Center webhook URL, webhook application client ID, and tenant ID. Check the event types and channel filters against the table in [Create a WhatsApp channel](#create-a-whatsapp-channel).
1. **Test an inbound message.** Send a WhatsApp message from the test recipient to the connected business number. Confirm that the inbound subscription receives activity and that the conversation appears in Contact Center.
1. **Test an outbound message.** Send a message from Contact Center to the test recipient, using an approved template when required. Confirm whether the recipient receives it.
1. **Check delivery-status processing.** Check activity and delivery failures on the outbound delivery-status subscription, separately from the inbound subscription. Confirm that the corresponding message status is reflected in Contact Center. When examining a status receipt, correlate its `data.messageId` with the sent message and inspect `data.status` and any `data.error` details. See [Advanced Messaging event schemas](/azure/event-grid/communication-services-advanced-messaging-events).

Use [Event Grid subscription metrics](/azure/event-grid/monitor-event-delivery#view-subscription-metrics) to check event delivery activity. If you need event-delivery failure details, configure [Event Grid diagnostic logs](/azure/event-grid/enable-diagnostic-logs-topic).

> [!IMPORTANT]
> Event Grid reporting an event as **Delivered** means that the webhook acknowledged receipt of the event. It doesn't prove that Contact Center finished processing it or that the WhatsApp message reached the recipient's device. Check the message-status receipt separately: `data.status` can be `Sent`, `Delivered`, `Read`, or `Failed`. An Event Grid delivery success and a WhatsApp message status are different signals.

## Troubleshoot missing messages or status updates

Outbound sending and receipt processing are separate operations. A customer can receive your outbound WhatsApp message even when the delivery-status subscription is missing, filters out the receipt, or fails webhook authentication.

| Symptom | What to check |
|---------|---------------|
| A subscription can't be created or its endpoint can't be validated | Confirm the Contact Center webhook URL and complete the webhook application and subscription-writer permissions in [Secure webhook delivery](/azure/event-grid/secure-webhook-delivery). |
| Inbound messages don't appear | Check the inbound event type, the `data.to` channel filter when used, and the webhook authentication settings. If Event Grid delivery succeeds, also check workstream routing and assignment. |
| Customers receive outbound messages, but statuses are missing or don't change | Check the separate delivery-status subscription, its `AdvancedMessageDeliveryStatusUpdated` event type, and its `data.from` channel filter when used. Verify its authentication settings independently of the inbound subscription. |
| Webhook delivery reports HTTP 401 or 403 | Check the tenant and application ID mapping, required role assignments, and access-token validation. If the failure concerns the app-only token type, follow [Check the app-only access-token claim](#check-the-app-only-access-token-claim). |
| Event Grid reports successful delivery, but Contact Center still doesn't show the expected result | Verify which subscription delivered the event and inspect the corresponding message-status receipt. Record the test time, channel ID, and message ID for support; event acknowledgement alone doesn't prove successful application processing. |

After correcting the configuration, send a new test message. Don't assume that old failed receipts will be replayed: Event Grid doesn't retry webhook responses such as HTTP 401 or 403. See [Event delivery and retry](/azure/event-grid/delivery-and-retry).

### Check the app-only access token claim

For webhook authentication that requires an app-only access token, the `idtyp` claim identifies the token type. Microsoft Entra emits `idtyp` with the value `app` in app-only access tokens when you configure this optional claim. This claim isn't a universal requirement for every Event Grid endpoint.

If authentication diagnostics indicate a missing app-only token type claim:

1. In Microsoft Entra ID, open **App registrations** and select the webhook application whose **Application (client) ID** you configured in Contact Center and both subscriptions.
1. Under **Token configuration**, select **Add optional claim**, select the **Access** token type, and add `idtyp`. If you use the application manifest instead, add `idtyp` to `optionalClaims.accessToken` without replacing existing claims. See [Configure optional claims](/entra/identity-platform/optional-claims) and the [`idtyp` reference](/entra/identity-platform/optional-claims-reference).
1. Save the configuration and verify event delivery again with a newly issued token. Configuring an ID-token claim doesn't change the access token delivered to the webhook.

Configure this claim on the **webhook resource application**, not on the subscription-writer application or the Azure Event Grid service application. The resource application's registration controls access-token claims.

Don't disable token validation to work around authentication failures, and don't paste bearer tokens into tickets or public token-decoding tools.

## Related information

[Configure proactive engagement for messaging](configure-proactive-engagement-messaging.md#whatsapp-preview)

[Plan migration from Azure Communication Services](migrate-from-azure-communication-services.md)

[Configure automated messages](/dynamics365/customer-service/administer/configure-automated-message?context=/dynamics365/contact-center/context/administer-context)   
[Configure a post-conversation survey](/dynamics365/customer-service/administer/configure-post-conversation-survey?context=/dynamics365/contact-center/context/administer-context)  
[Skill-based routing](/dynamics365/customer-service/administer/overview-skill-work-distribution?context=/dynamics365/contact-center/context/administer-context)   
[Create message templates](/dynamics365/customer-service/administer/create-message-templates?context=/dynamics365/contact-center/context/administer-context)   
[Delete a configured channel](/dynamics365/customer-service/administer/delete-channel?context=/dynamics365/contact-center/context/administer-context)   
[Support for live chat and asynchronous channels](/dynamics365/customer-service/administer/card-support-in-channels?context=/dynamics365/card-support-in-channels/context/administer-context)   
