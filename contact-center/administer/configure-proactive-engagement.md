---
title: How to set up proactive engagement
description: Prepare shared prerequisites, choose an audience, and find the voice or messaging setup guide for proactive engagement in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 10/14/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# How to set up proactive engagement

This article describes how to set up proactive engagement for voice or messaging. Learn more about proactive engagement and supported scenarios in [Overview of proactive engagement](overview-proactive-engagement.md).

## Prerequisites

- [Provision the required channels](../implement/provision-channels.md).
- Dynamics 365 Customer Insights if you want to use journey for your customer journey authoring.
- Microsoft Copilot Studio to use Copilot agents.
- For voice engagements that use direct routing, review the [requirements for direct routing](configure-proactive-engagement-voice.md#requirements-for-direct-routing).

> [!NOTE]
> Your organization is responsible for honoring customer consent and opt-out preferences. To learn how to view and manage opt-out records, see [Manage consent for proactive engagement](proactive-engagement-manage-consent.md).


## Set up proactive engagement

Complete the following steps:

1. Choose an audience and intake method. Define the audience and how customer contact information is provided:

   - Contact Center: Use file upload, the CCaaS API, or MCP (preview).
   - Conversational Journeys in Customer Insights: Use a customer journey when Dynamics 365 Customer Insights - Journeys is enabled.

    Then configure the required customer identification and routing details for your channel.
1. Set up an outbound workstream. Configure an outbound workstream for [voice](configure-proactive-engagement-voice.md#set-up-an-outbound-workstream) or [messaging](configure-proactive-engagement-messaging.md#set-up-an-outbound-workstream). 

1. Complete the configuration steps for the required channel in the **Create new proactive engagement** pane in  Copilot Service admin center.

> [!NOTE]
> Delivery windows and expiration dates can extend up to 30 days into the future. If you don't specify a delivery window, the system uses a 24-hour window starting immediately or on the earliest scheduled date, if it's in the future.

   - **Voice**: [Configure proactive engagement for voice](configure-proactive-engagement-voice.md).
   - **SMS**: [Configure proactive engagement for messaging](configure-proactive-engagement-messaging.md), including [SMS content](configure-proactive-engagement-messaging.md#sms).
   - **MMS (preview)**: [Configure proactive engagement for messaging](configure-proactive-engagement-messaging.md), including [MMS content and attachments](configure-proactive-engagement-messaging.md#mms-preview). MMS uses an SMS workstream with an MMS-capable provider and number. It doesn't use a separate MMS workstream.
   - **WhatsApp (preview)**: [Configure proactive engagement for messaging](configure-proactive-engagement-messaging.md), including [WhatsApp templates](configure-proactive-engagement-messaging.md#whatsapp-preview).

> [!IMPORTANT]
> - Proactive engagement in WhatsApp and MMS is a preview feature.
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://www.microsoft.com/en-us/business-applications/legal/supp-powerplatform-preview/), and are available before an official release so that customers can get early access and provide feedback.


## Manage proactive engagements

Use the following options to manage proactive engagements for voice and messaging:

   - **Voice**:
     - For contact chaining, phone number order, and retry behavior across related contacts, see [Configure multiparty (account) engagements](configure-proactive-engagement-voice.md#configure-multiparty-account-engagements).
     - For cancellation policies and suppressing future calls, see [Configure voice call cancellation and suppression](configure-proactive-engagement-voice.md#configure-voice-call-cancellation-and-suppression).
   - **Messaging**: For cancellation and reporting, see [Manage messaging engagements](configure-proactive-engagement-messaging.md#manage-messaging-engagements).

## Related information

[Overview of proactive engagement](overview-proactive-engagement.md)  
[Configure proactive engagement for voice](configure-proactive-engagement-voice.md)  
[Configure proactive engagement for messaging](configure-proactive-engagement-messaging.md)  
[Dial modes for proactive engagement](proactive-engagement-dial-modes.md)  
[Manage consent for proactive engagement](proactive-engagement-manage-consent.md)  
[Outcomes for proactive engagement](proactive-engagement-outcomes.md)  
[Best practices for proactive engagement campaigns](proactive-engagement-best-practices.md)  
[How proactive engagement works](../use/how-proactive-engagement-works.md)  
[Overview of conversational journeys](/dynamics365/customer-insights/journeys/conversational-journeys-overview)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
[Use CCaaS_CreateProactiveVoiceDelivery API](../extend/api/ccaas_createproactivevoicedelivery.md)  
[Use CCaaS_CreateOperation API](../extend/api/ccaas_createoperation.md)  
[Use CCaaS_CreateProactiveDelivery API](../extend/api/ccaas_createproactivedelivery.md)  
[Proactive Outbound dashboard](../use/proactive-outbound-dashboard.md#proactive-outbound-dashboard)
