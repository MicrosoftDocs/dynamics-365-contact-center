---
title: Use CCaaS_GetDeliveryTasks API
description: Learn about the CCaaS_GetDeliveryTasks API that enables organizations to retrieve the status and details of a proactive delivery task in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.date: 07/01/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_GetDeliveryTasks API

You can use the `CCaaS_GetDeliveryTasks` API to retrieve the status and details of a proactive delivery task created through the Proactive Engagement service. It returns the current status, retry information, [contact chaining](../../administer/configure-proactive-engagement.md#configure-multiparty-account-engagements) state, and the individual deliveries associated with the task.

## Prerequisites

- You must have the Omnichannel agent or Omnichannel supervisor role to call this API.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).
- A delivery task must have been created using the [CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md).

## Request details

- **URL**: `https://<orgurl>/api/data/v9.0/CCaaS_GetDeliveryTasks(DeliveryTaskId=<deliveryTaskId>)`
- **Method**: GET
- **OData Operation**: Function
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Microsoft Entra ID Bearer token for the user making the API call. This token must be issued from the same Microsoft Entra ID tenant as the Customer Service instance.

## Request parameters

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| DeliveryTaskId | String (GUID) | Yes | The unique identifier of the delivery task to retrieve. This value is returned in the response of the [CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md). |

## Sample request

```http
GET /api/data/v9.0/CCaaS_GetDeliveryTasks(DeliveryTaskId=68b36193-49cc-4749-8118-433a0e8c4b9a)
```

## Sample response

```json
{
  "@odata.context": "https://<orgurl>/api/data/v9.0/$metadata#expando",
  "value": [
    {
      "@odata.type": "#Microsoft.Dynamics.CRM.expando",
      "deliveryTaskId": "68b36193-49cc-4749-8118-433a0e8c4b9a",
      "organizationId": "cc9d14e1-1860-f111-ab00-70a8a59ac3af",
      "status": "Expired",
      "retryCount": 1,
      "maxRetryCount": 1,
      "whenCreated": "2026-06-05T11:57:26.778Z",
      "nextScheduledTime": "2026-06-05T11:57:26.778Z",
      "lastAttemptedTime": "2026-06-05T11:57:26.778Z",
      "fallbackAttempted": false,
      "channelType": "Voice",
      "proactiveEngagementConfigId": "6da5cb99-c060-f111-ab0c-70a8a5afa55c",
      "expirationDate": "2026-06-06T11:57:21.892Z",
      "reattemptDelay": 2,
      "reattemptSettings@odata.type": "#Collection(Int32)",
      "reattemptSettings": [192360001],
      "contactIds@odata.type": "#Collection(String)",
      "contactIds": [
        "428777f8-2705-4787-893b-1fb2834edf29"
      ],
      "requestId": "895f304d-4eec-4f7e-8bc1-2d6317dae469",
      "customerReached": false,
      "callbackAttemptCount": 0,
      "contactChainingStatus": {
        "@odata.type": "#Microsoft.Dynamics.CRM.expando",
        "currentLoopNumber": 1,
        "currentContactIndexAttempted": 0,
        "currentContactIdAttempted": "428777f8-2705-4787-893b-1fb2834edf29",
        "currentPhoneIndexAttempted": 0,
        "currentPhoneNumberTypeIdAttempted": "MobilePhoneNumber",
        "totalContactsInChain": 1,
        "totalPhonesInCurrentContact": 2,
        "totalPhonesInChain": 2,
        "totalEligiblePhonesInChain": 2,
        "totalEligiblePhonesInCurrentContact": 2,
        "areLoopsExhausted": false,
        "isChainExhausted": false,
        "seqNo": 1,
        "lastDeliveryResult": "Expired"
      },
      "deliveries@odata.type": "#Collection(Microsoft.Dynamics.CRM.crmbaseentity)",
      "deliveries": [
        {
          "@odata.type": "#Microsoft.Dynamics.CRM.expando",
          "id": "c776a9c2-623c-4f6e-ab6e-0ba3f3b4c317",
          "status": "Expired",
          "result": "Expired"
        }
      ]
    }
  ]
}
```

## Response properties

| Property | Type | Description |
|----------|------|-------------|
| deliveryTaskId | String (GUID) | The unique identifier of the delivery task. |
| organizationId | String (GUID) | The organization that owns the delivery task. |
| status | String | Current status of the delivery task, for example, `Expired`. |
| retryCount | Integer | Number of retry attempts that were made. |
| maxRetryCount | Integer | Maximum number of retry attempts allowed. |
| whenCreated | String | Timestamp when the task was created. |
| nextScheduledTime | String | Timestamp for the next scheduled attempt. |
| lastAttemptedTime | String | Timestamp of the most recent attempt. |
| fallbackAttempted | Boolean | Indicates whether a fallback delivery was attempted. |
| channelType | String | Channel used for the delivery, for example, `Voice`. |
| proactiveEngagementConfigId | String (GUID) | The proactive engagement configuration associated with the task. |
| expirationDate | String | Timestamp when the task expires. |
| reattemptDelay | Integer | Delay between reattempts. |
| reattemptSettings | Collection (Int32) | Configured reattempt settings. |
| contactIds | Collection (String) | The contacts associated with the task. |
| requestId | String | Identifier used to track the request from the source system. |
| customerReached | Boolean | Indicates whether the customer was reached. |
| callbackAttemptCount | Integer | Number of callback attempts. |
| contactChainingStatus | Object | Current state of the contact chaining loop, including contacts and phone numbers attempted. |
| deliveries | Collection | The individual deliveries created for the task, each with an `id`, `status`, and `result`. |

### Related information

[Use CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md)  
[Use CCaaS_CancelDeliveryTask API](ccaas_canceldeliverytask.md)  
[Use CCaaS_CreateOperation API](ccaas_createoperation.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  
