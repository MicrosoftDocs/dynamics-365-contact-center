---
title: Use CCaaS_CreateProactiveDelivery API
description: Learn about the CCaaS_CreateProactiveDelivery API that enables organizations to initiate proactive outbound voice calls to customers in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.date: 03/31/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_CreateProactiveDelivery API

You can use the `CCaaS_CreateProactiveDelivery` API to initiate proactive outbound voice calls to customers through the Proactive Engagement Service.

> [!IMPORTANT]
>
> - If an organization is using the `CCaaS_CreateProactiveDelivery` API to initiate an outbound voice call, the organization is responsible for consent management, including the manual updating of "do not call lists" for setting quiet hours for customer contact. Make sure that the following conditions are met:
> - Consent is obtained before contacting customers.
> - Customers are contacted during permitted hours only.

## Prerequisites

- You must have the Omnichannel Agent or Omnichannel Supervisor role to call this API.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).

## Request details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CreateProactiveDelivery`
- **Method**: POST
- **Version**: 1.0
- **OData Operation**: Action
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Azure AD Bearer token for the user making the API call. This token must be issued from the same Azure AD tenant as the Customer Service instance.

## Request headers

| Key | Type | Description |
|-----|------|-------------|
| ApiVersion | String | The CCaaS API version. |
| ProactiveEngagementConfigId | String | ID of the Proactive Engagement Configuration to use. This specifies the dial mode type, workstream, and outbound profile to use. To get this ID, do the following: <ol><li>Go to [Power Apps](https://make.preview.powerapps.com) and select the required environment.</li><li>Select **Tables** > **Proactive Engagement Configuration**.</li><li>Select the ID of the required record.</li></ol> |
| RequestId | String | Optional. Attribute to pass to track the request from a source system. |
| Priority | String | Optional. Defines the priority value of the request. |
| Contacts | JSON array of Contact objects | Specifies one or more contacts (up to 5) on this request. At least one phone number per contact is required. |
| Windows | JSON array of Window objects | Specifies the valid time periods when the outbound call may be placed. If not provided, the system defaults to a 24-hour window starting immediately (from current time until 24 hours later). |

## Contact object

| Key | Type | Description |
|-----|------|-------------|
| uniqueIdentifier | String | Unique identifier of the contact. Can be a ContactId or an external ID. |
| firstName | String | First name of the contact. |
| lastName | String | Last name of the contact. |
| mobilePhoneNumber | String | Mobile phone number of the contact. |
| businessPhoneNumber | String | Business phone number of the contact. |
| homePhoneNumber | String | Home phone number of the contact. |
| email | String | Optional. Email address of the contact. |
| postalcode | String | Optional. Postal code of the contact. |
| state | String | Optional. State of the contact. |
| country | String | Optional. Country of the contact. |
| addressline | String | Optional. Address line of the contact. |
| city | String | Optional. City of the contact. |
| timezone | String | Optional. Time zone of the contact. Must be a value from the Dynamics-approved list. |
| inputAttributes | JSON object of key-value strings | Optional. Variables that can be referenced within Copilot agent flows to customize behavior, drive conditional logic, or retrieve personalized information from Dataverse records. |
| windows | JSON array of Window objects | Optional. Contact-level time windows that override the top-level Windows for this specific contact. |

> [!NOTE]
> At least one of `mobilePhoneNumber`, `businessPhoneNumber`, or `homePhoneNumber` is required per contact.

## Windows object

| Key | Type | Description |
|-----|------|-------------|
| Start | String | The beginning timestamp for this window. Must be specified in UTC in the `yyyy-MM-ddTHH:mm:ss.fffZ` format. |
| End | String | The end timestamp for this window. Must be specified in UTC in the `yyyy-MM-ddTHH:mm:ss.fffZ` format. |

## Sample request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "RequestId": "e1f2a3b4-c5d6-7890-abcd-ef1234567890",
  "Priority": "1",
  "Contacts": "[{\"uniqueIdentifier\":\"f47ac10b-58cc-4372-a567-0e02b2c3d479\",\"firstName\":\"John\",\"lastName\":\"Doe\",\"mobilePhoneNumber\":\"+15550100\",\"businessPhoneNumber\":\"+15550101\",\"homePhoneNumber\":\"+15550102\",\"email\":\"text@a.com\",\"postalcode\":\"25642\",\"state\":\"WA\",\"country\":\"USA\",\"addressline\":\"1234 227th PL SE\",\"city\":\"Seattle\",\"timezone\":\"(GMT-03:00) Brasilia\",\"inputAttributes\":{\"AppointmentTime\":\"10:00 AM\",\"CustomerNumber\":\"1234567\"},\"windows\":[{\"start\":\"2025-12-10T09:00:00Z\",\"end\":\"2025-12-10T17:00:00Z\"}]}]"
}
```

### Related information

[Use CCaaS_CreateProactiveVoiceDelivery API](ccaas_createproactivevoicedelivery.md)  
[Use CCaaS_CreateOperation API](ccaas_createoperation.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  
