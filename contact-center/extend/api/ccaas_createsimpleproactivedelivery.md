---
title: Use CCaaS_CreateSimpleProactiveDelivery API
description: Learn about the CCaaS_CreateSimpleProactiveDelivery API that enables organizations to initiate a single proactive outbound delivery to a customer in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.date: 07/01/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_CreateSimpleProactiveDelivery API

You can use the `CCaaS_CreateSimpleProactiveDelivery` API to initiate a single proactive outbound delivery to a customer through the Proactive Engagement service. It provides a simplified, flattened set of contact attributes for a single recipient.

[!INCLUDE [proactive-api-guidance](../../includes/proactive/cc-proactive-api-guidance.md)]

> [!IMPORTANT]
>
> - If an organization is using the `CCaaS_CreateSimpleProactiveDelivery` API to initiate an outbound voice call or SMS message, the organization is responsible for consent management, including the manual updating of "don't call lists" for setting quiet hours for customer contact. Make sure that the following conditions are met:
>   - Consent is obtained before contacting customers.
>   - Customers are contacted during permitted hours only.

## Prerequisites

- You must have the Omnichannel agent or Omnichannel supervisor role to call this API.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).

## Request details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CreateSimpleProactiveDelivery`
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
| UniqueIdentifier | String | Yes | Unique identifier of the contact. Can be a ContactId or an external ID. |
| FirstName | String | Yes | First name of the contact. |
| LastName | String | Yes | Last name of the contact. |
| Email | String | No | Email address of the contact. |
| MobilePhoneNumber | String | Yes | Mobile phone number of the contact. |
| BusinessPhoneNumber | String | No | Business phone number of the contact. |
| HomePhoneNumber | String | No | Home phone number of the contact. |
| Country | String | No | Country/Region of the contact. |
| City | String | No | City of the contact. |
| AddressLine | String | No | Address line of the contact. |
| PostalCode | String | No | Postal code of the contact. |
| State | String | No | State of the contact. |
| TimeZone | String | No | Time zone of the contact. Must be a value from the Dynamics 365-approved list. |
| Priority | String | No | Defines the priority value of the request. |
| InputAttributes | JSON object of key-value strings | No | Variables that can be referenced within Copilot agent flows to customize behavior, drive conditional logic, or retrieve personalized information from Dataverse records. |
| Windows | JSON array of Window objects | No | Specifies the valid time periods when the outbound call or SMS can be placed. If not provided, the system defaults to a 24-hour window starting immediately. |

## Windows object

| Key | Type | Description |
|-----|------|-------------|
| Start | String | The beginning timestamp for this window. |
| End | String | The end timestamp for this window. |

## Sample request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "36ebcd69-574d-f111-bec5-70a8a5b0f6fd",
  "UniqueIdentifier": "36ebcd69-574d-f111-bec5-10a8a5b0f6fb",
  "FirstName": "John",
  "LastName": "Doe",
  "Email": "john.doe@contoso.com",
  "MobilePhoneNumber": "+18666316096",
  "BusinessPhoneNumber": "+18666316096",
  "HomePhoneNumber": "+18666316096",
  "Country": "United States",
  "City": "Seattle",
  "AddressLine": "123 Main Street",
  "PostalCode": "98101",
  "State": "WA",
  "TimeZone": "Central European Standard Time",
  "Priority": "1",
  "InputAttributes": "{\"CustomerTier\":\"Gold\",\"AccountNumber\":\"ACC-12345\",\"PreferredLanguage\":\"en-US\"}",
  "Windows": "[{\"Start\":\"2026-06-06T09:00:00\",\"End\":\"2026-06-06T12:00:00\"},{\"Start\":\"2026-06-06T14:00:00\",\"End\":\"2026-06-06T17:00:00\"}]"
}
```

### Related information

[Use CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md)  
[Use CCaaS_CreateProactiveBulkDelivery API](ccaas_createproactivebulkdelivery.md)  
[Use CCaaS_CreateOperation API](ccaas_createoperation.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  
