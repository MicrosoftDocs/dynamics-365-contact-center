---
title: Use CCaaS_CreateProactiveBulkDelivery API
description: Learn about the CCaaS_CreateProactiveBulkDelivery and CCaaS_CreateProactiveDeliveryBulkV2 APIs that enable organizations to initiate proactive outbound deliveries to multiple customers in a single request in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.date: 08/24/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_CreateProactiveBulkDelivery API

Use the `CCaaS_CreateProactiveBulkDelivery` API to initiate proactive outbound deliveries to multiple customers in a single request through the proactive engagement service. Use it to submit a batch of contacts for a workstream rather than creating each delivery individually.

[!INCLUDE [proactive-api-guidance](../../includes/proactive/cc-proactive-api-guidance.md)]

> [!IMPORTANT]
>
> - If an organization is using the `CCaaS_CreateProactiveBulkDelivery` API to initiate outbound voice calls or SMS messages, the organization is responsible for consent management, including the manual updating of "don't call lists" for setting quiet hours for customer contact. Make sure that the following conditions are met:
>   - Consent is obtained before contacting customers.
>   - Customers are contacted during permitted hours only.

## Prerequisites

- You must have the Omnichannel agent or Omnichannel supervisor role to call this API.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).

## Request details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CreateProactiveBulkDelivery`
- **Method**: POST
- **Version**: 1.0
- **OData Operation**: Action
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Microsoft Entra ID Bearer token for the user making the API call. This token must be issued from the same Microsoft Entra ID tenant as the Customer Service instance.

## Request parameters

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| ApiVersion | String | Yes | The CCaaS API version. |
| ProactiveEngagementConfigId | String | Yes | ID of the Proactive Engagement Configuration to use. It also specifies the dial mode type, workstream, and outbound profile to use. To get this ID, do the following steps: <ol><li>Go to [Power Apps](https://make.preview.powerapps.com) and select the required environment.</li><li>Select **Tables** > **Proactive Engagement Configuration**.</li><li>Select the ID of the required record.</li></ol> |
| ProactiveDeliveries | JSON array of delivery objects | Yes | A serialized JSON array that specifies the contacts for the delivery. Each object includes the contact details and at least one phone number. |
| RequestId | String | No | Identifier used to track the request from a source system. |
| ProactiveEngagements | String | No | Optional engagement details to associate with the deliveries. |

## ProactiveDeliveries object

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| uniqueIdentifier | String | Yes | Unique identifier of the contact. Can be a ContactId or an external ID. |
| firstName | String | Yes | First name of the contact. |
| lastName | String | Yes | Last name of the contact. |
| mobilePhoneNumber | String | Yes | Mobile phone number of the contact. |
| businessPhoneNumber | String | No | Business phone number of the contact. |
| state | String | No | State of the contact. |
| city | String | No | City of the contact. |
| zipCode | String | No | Postal code of the contact. |
| timeZone | String | No | Time zone of the contact. Must be a value from the Dynamics 365-approved list. |

## Sample request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "36ebcd69-574d-f111-bec5-70a8a5b0f6fd",
  "ProactiveDeliveries": "[{\"firstName\":\"John\",\"lastName\":\"Doe\",\"businessPhoneNumber\":\"+18666316096\",\"mobilePhoneNumber\":\"+18666316096\",\"state\":\"CA\",\"city\":\"San Francisco\",\"zipCode\":\"94105\",\"timeZone\":\"Pacific Standard Time\",\"uniqueIdentifier\":\"00de1776-7c59-44ec-4060-3f9184bb5958\"}]",
  "RequestId": "06228731-fab7-45f8-9f2f-a9daecef99d2",
  "ProactiveEngagements": ""
}
```

## Use CCaaS_CreateProactiveDeliveryBulkV2 API

The `CCaaS_CreateProactiveDeliveryBulkV2` API provides the same bulk delivery capability as `CCaaS_CreateProactiveBulkDelivery`, with `RequestId` optional and `ProactiveEngagements` no longer required.

### Request details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CreateProactiveDeliveryBulkV2`
- **Method**: POST
- **Version**: 1.0
- **OData Operation**: Action
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Microsoft Entra ID Bearer token for the user making the API call. This token must be issued from the same Microsoft Entra ID tenant as the Customer Service instance.

### Request parameters

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| ApiVersion | String | Yes | The CCaaS API version. |
| ProactiveEngagementConfigId | String | Yes | ID of the Proactive Engagement Configuration to use. It also specifies the dial mode type, workstream, and outbound profile to use. |
| ProactiveDeliveries | JSON array of delivery objects | Yes |A serialized JSON array that specifies the contacts for the delivery. Each object includes the contact details and at least one phone number. |
| RequestId | String | No | Identifier used to track the request from a source system. |

### Sample request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "36ebcd69-574d-f111-bec5-70a8a5b0f6fd",
  "ProactiveDeliveries": "[{\"firstName\":\"John\",\"lastName\":\"Doe\",\"businessPhoneNumber\":\"+18666316096\",\"mobilePhoneNumber\":\"+18666316096\",\"state\":\"CA\",\"city\":\"San Francisco\",\"zipCode\":\"94105\",\"timeZone\":\"Pacific Standard Time\",\"uniqueIdentifier\":\"00de1776-7c59-44ec-4060-3f9184bb5958\"}]",
  "RequestId": "06228731-fab7-45f8-9f2f-a9daecef99d2"
}
```

### Related information

[Use CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md)  
[Use CCaaS_CreateSimpleProactiveDelivery API](ccaas_createsimpleproactivedelivery.md)  
[Use CCaaS_CreateOperation API](ccaas_createoperation.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  
