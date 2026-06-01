---
title: Manage consent for proactive engagement in Dynamics 365 Contact Center
description: Learn how to manage customer consent and opt-out preferences for proactive engagement campaigns in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 06/01/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Manage consent for proactive engagement

Consent management helps your organization maintain compliance with telecommunications regulations by tracking and honoring customer opt-out preferences for proactive outbound voice calls and SMS messages. When a customer opts out, the system prevents future proactive engagements from being initiated to that customer until consent is restored.

All consent records created by proactive engagement use the **PES** compliance profile. These engagements are considered transactional with implicit opt-in, meaning customers are assumed to have consented unless they explicitly opt out. Learn more about compliance profiles in [Manage consent for email and text messages in Customer Insights](/dynamics365/customer-insights/journeys/real-time-marketing-compliance-settings).

> [!IMPORTANT]
> Your organization is responsible for ensuring compliance with all applicable consent and opt-out regulations, including maintaining accurate do-not-call lists and honoring opt-out requests promptly. Learn more in [Best practices for proactive engagement campaigns](proactive-engagement-best-practices.md).

## Prerequisites

- You must have the Omnichannel administrator role.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](configure-proactive-engagement.md).

## Navigate to consent management

1. In the Contact Center admin center, go to **Productivity** > **Proactive engagement**.
1. Select **Manage** next to **Consent**.

## Automatic opt-out

The system automatically creates opt-out records for customers in the following scenarios:

- **SMS**: When the system receives an opt-out SMS message from the customer (for example, the customer replies STOP), an opt-out record is automatically created for the SMS channel.
- **Voice and SMS**: When a service representative marks a conversation with a disposition code of **Do not contact**, an opt-out record is automatically created for the appropriate channel.

## Manually manage opt-outs

You can manually create, edit, and bulk upload opt-out records from the consent management page.

### Create an opt-out record

1. In the consent management page, select **Voice consent** or **SMS consent** as appropriate.
1. Select the customer and set the opt-out status.

### Edit existing opt-out records

Navigate to the consent management page to view and edit opt-out records that are already created. You can update a customer's consent status—for example, to restore consent when a customer requests to receive proactive engagements again.

### Bulk upload opt-outs

If you're migrating from another system, you can do a bulk upload of opt-out records to import your existing do-not-call list. This ensures that customers who have previously opted out in your current system continue to be honored in Dynamics 365 Contact Center.

## How consent is enforced

When a proactive delivery is initiated through any of the proactive engagement APIs, file upload or MCP end points or through a Customer Insights journey, the system checks the customer's consent status before placing the call or sending the SMS message. If the customer has opted out, the delivery isn't initiated and the request is marked accordingly.
