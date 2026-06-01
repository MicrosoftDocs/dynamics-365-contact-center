---
title: Use CCaaS_CreateProactiveSMSDelivery API
description: Learn about the CCaaS_CreateProactiveSMSDelivery API that enables organizations to initiate proactive outbound SMS messages to customers in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.date: 06/01/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_CreateProactiveSMSDelivery API

You can use the `CCaaS_CreateProactiveSMSDelivery` API to create a proactive outbound SMS delivery by invoking the appropriate API within the Proactive Engagement service. It initiates an SMS outbound message via Messaging Runtime.

> [!IMPORTANT]
>
> - If an organization is using the `CCaaS_CreateProactiveSMSDelivery` API to initiate an outbound SMS message, the organization is responsible for consent management. Make sure that the following conditions are met:
>   - Consent is obtained before contacting customers.
>   - Customers are contacted during permitted hours only.

> [!NOTE]
> This API doesn't support proactive engagement features like re-attempts, contact windows, custom priority, and frequency capping. Use the [CCaaS_CreateProactiveDelivery](ccaas_createproactivedelivery.md) API if you want to leverage these features.

## Prerequisites

- You must have the Omnichannel agent or Omnichannel supervisor role to call this API.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).

## Request details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CreateProactiveSMSDelivery`
- **Method**: POST
- **Version**: 1.0
- **OData Operation**: Action
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Microsoft Entra ID Bearer token for the user making the API call. This token must be issued from the same Microsoft Entra ID tenant as the Customer Service instance.

## Request parameters

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| ApiVersion | String | Yes | The Omnichannel CCaaS API version. |
| ProactiveEngagementConfigId | String | Yes | ID of the Proactive Engagement Configuration to use. This specifies the workstream to use. To get this ID, do the following steps: <ol><li>Go to [Power Apps](https://make.preview.powerapps.com) and select the required environment.</li><li>Select **Tables** > **Proactive Engagement Configuration**.</li><li>Select the ID of the required record.</li></ol> |
| DestinationPhoneNumber | String | Yes | Phone number of the customer to send the SMS message. |
| Message | String | Yes | SMS message content to be sent to the recipient. |
| InputAttributes | JSON object of key-value strings | No | Variables that can be referenced within Copilot agent flows to drive behavior changes or to look up information from Dataverse for personalization purposes. |

## Sample request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "DestinationPhoneNumber": "+15550200",
  "Message": "Your appointment is confirmed for tomorrow at 10:00 AM. Reply STOP to opt out.",
  "InputAttributes": "{\"AppointmentTime\":\"10:00 AM\",\"CustomerNumber\":\"1234567\"}"
}
```

### Related information

[Use CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md)  
[Use CCaaS_CancelDeliveryTask API](ccaas_canceldeliverytask.md)  
[Use CCaaS_CreateProactiveVoiceDelivery API](ccaas_createproactivevoicedelivery.md)  
[Use CCaaS_CreateOperation API](ccaas_createoperation.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  
