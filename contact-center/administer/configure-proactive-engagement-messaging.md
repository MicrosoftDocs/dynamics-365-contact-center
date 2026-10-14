---
title: Configure proactive engagement for messaging
description: Configure proactive SMS, MMS (preview), and WhatsApp (preview) engagements in Dynamics 365 Contact Center, including outbound workstreams, message content, and templates.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 10/14/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Configure proactive engagement for messaging

Use this article to configure proactive SMS, MMS (preview), or WhatsApp (preview) engagements. Complete the shared messaging setup, and then follow the [SMS](#sms), [MMS (preview)](#mms-preview), or [WhatsApp (preview)](#whatsapp-preview) instructions for your message content.

> [!IMPORTANT]
> - Proactive engagement in MMS and WhatsApp is a preview feature.
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://www.microsoft.com/en-us/business-applications/legal/supp-powerplatform-preview/), and are available before an official release so that customers can get early access and provide feedback.

## Prerequisites

Review the shared prerequisites, consent requirements, and audience options in [Set up proactive engagement](configure-proactive-engagement.md). Then complete the required setup for the required channel:

- **SMS:** [Configure an SMS channel](/dynamics365/customer-service/administer/configure-sms-channel?context=/dynamics365/contact-center/context/administer-context) or [Configure an SMS channel for Infobip](configure-sms-channel-infobip.md).
- **MMS (preview):** Configure an SMS channel with an MMS-capable Twilio or Infobip number. Azure Communication Services doesn't support MMS. MMS uses an SMS workstream and doesn't require a separate MMS workstream.
- **WhatsApp (preview):** [Configure a WhatsApp channel through Azure Communication Services](configure-whatsapp-acs.md) and prepare approved message templates. Complete the [channel verification steps](configure-whatsapp-acs.md#verify-your-whatsapp-channel) before testing proactive engagement. Verify delivery-status updates are received. If delivery-status updates are missing, see [Troubleshoot missing messages or status updates](configure-whatsapp-acs.md#troubleshoot-missing-messages-or-status-updates). The Event Grid guidance applies to WhatsApp through Azure Communication Services, not MMS.

Review [consent support by channel](proactive-engagement-manage-consent.md#channel-support) before configuring proactive engagement. 
## Set up an outbound workstream

1. Create a workstream by selecting the **Outbound** option and setting the type to **Messaging**. Then, select the channel:
   - For SMS and MMS, select **SMS**.
   - For WhatsApp, select **WhatsApp**.

   Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context).

1. Set up the outbound channel in the workstream:

   - **SMS and MMS**: In the **Set up your SMS channel** section, select **Setup**, and then select an SMS number. To send MMS, select a Twilio or Infobip number that supports MMS. For provider setup, see [Configure an SMS channel](/dynamics365/customer-service/administer/configure-sms-channel?context=/dynamics365/contact-center/context/administer-context) or [Configure an SMS channel for Infobip](configure-sms-channel-infobip.md).
   - **WhatsApp**: Select the WhatsApp account and number that you configured. For account and channel setup, see [Configure a WhatsApp channel through Azure Communication Services](configure-whatsapp-acs.md).

1. Set up the outbound behaviors for the selected channel.

1. Configure [work distribution](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution), optionally add an [AI agent](/dynamics365/customer-service/administer/create-workstreams#add-an-agent-to-a-workstream) to the workstream, and configure representative notifications. Ensure that the workstream has a default queue.

The system automatically configures the routing rules based on the proactive engagement settings. These rules appear under the **Auto generated rules (advanced)** section of the workstream.

To have an AI agent handle customer responses, add and configure the agent on the messaging workstream. The messaging engagement wizard doesn't provide a separate AI-agent selection or the voice **Engagement type** and **Dialing modes** controls.

## Create a messaging proactive engagement

[!INCLUDE [proactive-setup](../includes/proactive/cc-proactive-setup.md)]


The **Create new proactive engagement** wizard guides you through the steps outlined in the following sections:

- Audience
- Details
- Preferences
- Message template configuration
- Frequency limits
- Summary

If you select **Upload a file** as the intake method, **File upload** follows **Summary**.

> [!NOTE]
> Delivery windows and expiration dates can't extend more than 30 days into the future. If a request or uploaded record doesn't specify a delivery window, the system uses a 24-hour window that starts immediately, or at the requested earliest schedule date when it's a future date.

## Audience

[!INCLUDE [proactive-audience](../includes/proactive/cc-proactive-audience.md)]

2. Select **Next**.

## Details

[!INCLUDE [proactive-details](../includes/proactive/cc-proactive-details.md)]

## Preferences

On the **Preferences** page, configure channel behaviors and throttling rules for the messaging engagement.

1. Under **Channel behaviors**, configure the following settings:

   - **First response timeout**: Set how long to wait for the customer's first reply, in minutes, hours, or days. The default is 5 minutes. A reply received after this period might be handled as an inbound message without the original proactive engagement context.
   - **Priority level**: Select the priority for the engagement — **Normal**, **High**, or **Critical**. Priority determines which proactive engagement is processed first when multiple engagements compete for the same queue and skillset.
   - **Message order**: Select how messages within the engagement are processed:
     - **Earliest Scheduled Date**: Processes records that are close to the end of the messaging window first.
     - **Last in First Out**: Processes the most recent records first.
     - **First in, First Out**: Processes older records first.
     - **Custom priority ascending**: Processes records in ascending order based on a priority attribute specified in the contact list or API payload.
     - **Custom priority descending**: Processes records in descending order based on the priority attribute.

1. Under **Rules**, select **Use rules** to set throttling and pacing rules for the engagement. Configure conditions based on the following parameters:

   - **Average wait time**: The average amount of time it takes for customers to connect to representatives.
   - **Escalation count**: The total number of escalations made from the AI agent.
   - **Open concurrent escalations**: The total number of open escalations that aren't resolved.

   For each rule, specify the threshold value, the time window (**In the last**), and the **Decrease concurrent calls by** percentage. In a messaging engagement, this setting controls the number of concurrent messages when the condition is met.

1. Select **Next**.

## Message template configuration

On the **Message template configuration** page, configure the content for the channel selected by the messaging workstream. 

For SMS and MMS text, use the personalization menu to insert contact details, such as first and last names, phone number, email, postal code, country/region, city, and street.

Use the **Preview** pane to view how the message might appear on a mobile device. The actual appearance can vary by channel, provider, and device.

### SMS

1. Under **Templates**, turn on **Enable message templates for this workflow**. This setting is on by default when you use **Upload a file** as the intake method.

   For engagements triggered through the **CCaaS API** or **MCP**, you must configure a template. The `Message` parameter can override the rendered template text, but a template is still required.

1. In **Message**, compose the message to send to customers. You can enter up to 1,000 characters and use personalization to add contact details.

1. Review the preview, and then select **Next** to configure [frequency limits](#frequency-limits).

### MMS (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

The selected provider and phone number must support MMS. You can send a message with text and media attachments or with media only.

1. Under **Templates**, turn on **Enable message templates for this workflow**. This setting is on by default when you use **Upload a file** as the intake method.

   For API requests that provide content and attachments through `MessageAttributes`, you don't need to configure an SMS template. Learn more in [CCaaS_CreateProactiveDelivery API](../extend/api/ccaas_createproactivedelivery.md).

1. Under **Message type**, select **MMS**.

1. Optionally, compose a message of up to 1,600 characters. You can use personalization to add contact details.

1. Under **Multimedia**, select **Add media**. Select an existing asset from the media library, or select **Add file** to upload an asset. You can add up to 10 attachments.

   > [!IMPORTANT]
   > Media files uploaded for MMS are publicly accessible through a content delivery network (CDN). Don't upload confidential or sensitive files.

   The editor uses the Dataverse file records for the selected assets. You don't need to enter the record IDs. Learn more in [Get a media attachment ID](../extend/api/ccaas_createproactivedelivery.md#get-a-media-attachment-id).

   For supported formats, text-length counting, and Twilio and Infobip media size limits, learn more in [MMS limits](../extend/api/ccaas_createproactivedelivery.md#mms-limits).

1. Review the preview, and then select **Next** to configure [frequency limits](#frequency-limits).

### WhatsApp (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]
Use an approved WhatsApp message template for proactive engagements. Free-form outbound WhatsApp messages aren't supported.

Before you configure the engagement, prepare an approved template in WhatsApp Manager for the account associated with the workstream. Learn more in [WhatsApp template messages](/azure/communication-services/concepts/advanced-messaging/whatsapp/template-messages).

The proactive engagement editor defines the message content inline and doesn't use templates configured in the workstream **Behaviors** settings. You don't need to complete the [workstream template setup](configure-whatsapp-acs.md#set-up-whatsapp-message-templates) for this editor.

[!NOTE] Saving the proactive engagement doesn't submit the WhatsApp template for approval or change its approval status in WhatsApp Manager.

1. Enter the approved template name, select the language, and define the content to match the template in WhatsApp Manager.

1. If the template contains placeholders, specify a value for each required parameter.

1. Review the preview, and then select **Next** to configure [frequency limits](#frequency-limits).

## Frequency limits

On the **Frequency limits** page, complete the following steps:

1. Select **Use frequency limits** to turn on frequency controls, and then enter values for:
   - **Maximum engagements per day**: The maximum number of times you can reach a contact in a day across all channels.
   - **Maximum engagements per week**: The maximum number of times you can reach a contact in a week across all channels.

1. Under **Time zones**, choose the time-zone basis for the schedule:
   - **Use customer's local time zone when available (defaults to UTC if not available)**: Use the customer's time zone, with UTC as the fallback when it isn't available.
   - **Use Coordinated Universal Time (UTC)**: Use UTC regardless of the customer's time zone.

   If you provide contact time-zone values, supply them explicitly in the uploaded file or API payload. The system doesn't auto-detect or geo-infer time zones. In an API payload, use a Windows standard time-zone name, such as `Pacific Standard Time`, or a Dataverse time-zone code as a string, such as `"35"`. Display names and IANA time-zone names aren't accepted. See the [Contact object](../extend/api/ccaas_createproactivedelivery.md#contact-object).

1. Select **Next**.

## Summary

Review all settings on the **Summary** page, and select **Create**.

## File upload

[!INCLUDE [proactive-file-upload](../includes/proactive/cc-proactive-file-upload.md)]

## Manage messaging engagements

Messaging engagements support one contact per request. Contact chaining and configurable reattempts are available for voice engagements only. Automatic service retries for messaging are separate from configurable reattempts.

To cancel messaging engagements through the CCaaS APIs:

- To cancel a pending delivery, use [CCaaS_CreateOperation](../extend/api/ccaas_createoperation.md) with the `Cancel` operation and `DeliveryId`.
- To stop future attempts for a delivery task, use [CCaaS_CancelDeliveryTask](../extend/api/ccaas_canceldeliverytask.md) with `DeliveryTaskId`.

Cancellation doesn't recall messages that are already sent, and work that already started might continue.

To monitor delivery results, see [Outcomes for proactive engagement](proactive-engagement-outcomes.md) and [Proactive engagement tables](../extend/proactive-engagement-tables.md).

## Related information

[Set up proactive engagement](configure-proactive-engagement.md)  
[Configure proactive engagement for voice](configure-proactive-engagement-voice.md)  
[Configure a WhatsApp channel through Azure Communication Services](configure-whatsapp-acs.md)  
[Configure an SMS channel for Infobip](configure-sms-channel-infobip.md)  
[Manage consent for proactive engagement](proactive-engagement-manage-consent.md)  
[Use CCaaS_CreateProactiveDelivery API](../extend/api/ccaas_createproactivedelivery.md)  
[Best practices for proactive engagement campaigns](proactive-engagement-best-practices.md)  
[Proactive Outbound dashboard](../use/proactive-outbound-dashboard.md#proactive-outbound-dashboard)