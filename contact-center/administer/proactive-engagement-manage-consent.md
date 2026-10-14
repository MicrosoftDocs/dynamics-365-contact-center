---
title: Manage consent for proactive engagement in Dynamics 365 Contact Center
description: Learn how to manage customer consent and opt-out preferences for proactive engagement campaigns in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 10/14/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Manage consent for proactive engagement

Consent management helps your organization track and honor customer opt-out preferences for proactive outbound voice calls and SMS/MMS messages. MMS uses the SMS channel's consent records; it doesn't have a separate MMS consent channel. During WhatsApp public preview, WhatsApp proactive messages use SMS/text consent records and opt-out status. Opt-out records apply to the corresponding contact point and consent channel.

The **PES** compliance profile treats these engagements as transactional with implicit opt-in. This technical setting isn't evidence that a customer has given legally required consent. Learn more about compliance profiles in [Manage consent for email and text messages in Customer Insights](/dynamics365/customer-insights/journeys/real-time-marketing-compliance-settings).

> [!IMPORTANT]
> Your organization is responsible for ensuring compliance with all applicable consent and opt-out regulations, including maintaining accurate do-not-call lists and honoring opt-out requests promptly. Learn more in [Best practices for proactive engagement campaigns](proactive-engagement-best-practices.md).

## Prerequisites

- You must have the Omnichannel administrator role.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](configure-proactive-engagement.md).

## Channel support

| Channel | Built-in proactive consent handling |
|---------|-------------------------------------|
| Voice | Voice consent records and the supported voice opt-out workflow. |
| SMS and MMS (preview) | Shared SMS/text consent records. An SMS opt-out applies to subsequent MMS deliveries to the same contact point through the SMS channel. |
| WhatsApp (preview) | Uses SMS/text consent records. An SMS/text opt-out applies to subsequent WhatsApp proactive deliveries to the same contact point. |

An approved WhatsApp message template doesn't establish customer consent. WhatsApp proactive deliveries are evaluated against the contact point's SMS/text consent record.


> [!IMPORTANT]
> - Proactive engagement in MMS and WhatsApp is a preview feature.
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://www.microsoft.com/en-us/business-applications/legal/supp-powerplatform-preview/), and are available before an official release so that customers can get early access and provide feedback.

## Navigate to consent management

1. In the Copilot Service admin center site map, go to **Productivity** > **Proactive engagement**.
1. Select **Manage** next to **Consent**.

## Automatic opt-out

The system automatically creates opt-out records for customers in the following scenarios:

- **SMS and MMS**: When the system receives an opt-out SMS message from the customer (for example, the customer replies STOP), it creates an opt-out record for the SMS channel. The same record applies to MMS.
- **Voice and SMS/MMS**: When a service representative marks a conversation with a disposition code of **Do not contact**, the system creates an opt-out record for the appropriate channel.

Provider-side opt-out handling can also apply. Follow your messaging provider's configuration requirements; adding "Reply STOP to opt out" to a message doesn't configure provider-side handling.

## Manually manage opt-outs

You can manually create, edit, and bulk upload opt-out records from the consent management page.

### Create an opt-out record

1. On the consent management page, select **Voice consent** for voice or **Text consent** for SMS, MMS, and WhatsApp.
1. Select the customer and set the opt-out status.

### Edit existing opt-out records

Go to the consent management page to view and edit opt-out records. You can update a customer's consent status, such as restoring consent when a customer requests to receive proactive engagements again.

### Bulk upload opt-outs

If you're migrating from another system, bulk upload opt-out records to import your existing do-not-call list. This process ensures that customers who previously opted out in your current system continue to be honored in Dynamics 365 Contact Center.

## How consent is enforced

The proactive delivery flow uses the corresponding consent records to evaluate eligibility for deliveries submitted through APIs, file upload, MCP, or a Customer Insights journey. Voice uses voice consent records. SMS and MMS use SMS/text consent records. During public preview, WhatsApp also uses SMS/text consent records. An opt-out excludes the corresponding contact point from delivery.

### Related information

[Overview of proactive engagement](overview-proactive-engagement.md)  
[Configure proactive engagement](configure-proactive-engagement.md)  
