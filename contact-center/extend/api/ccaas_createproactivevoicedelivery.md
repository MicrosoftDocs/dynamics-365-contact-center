---
title: Use CCaaS_CreateProactiveVoiceDelivery API
description: Learn about the CCaaS_CreateProactiveVoiceDelivery API that enables organizations to initiate proactive outbound voice calls to customers.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: reference
ms.date: 06/05/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_CreateProactiveVoiceDelivery API

You can use the `CCaaS_CreateProactiveVoiceDelivery` API to initiate proactive outbound voice calls to customers or allow customers to schedule callbacks through the Proactive Engagement Service.

> [!NOTE]
> This API doesn't support proactive engagement features like reattempts, contact windows, custom priority, and frequency capping. Use the [CCaaS_CreateProactiveDelivery](ccaas_createproactivedelivery.md) API if you want to leverage these features.

> [!IMPORTANT]
> If an organization is using the `CCaaS_CreateProactiveVoiceDelivery` API to initiate an outbound voice call, the organization is responsible for consent management, including the manual updating of "do not call lists" for setting quiet hours for customer contact. Make sure that the following conditions are met:
> - Consent is obtained before customers are contacted.
> - Customers are contacted during permitted hours only.

## Prerequisites

- You must have the Omnichannel agent or Omnichannel supervisor role to call this API.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).

### Request Details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CreateProactiveVoiceDelivery`
- **Method**: POST
- **Version**: 1.0
- **OData Operation**: Action
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Azure AD Bearer token for the user making the API call. This token must be issued from the same Azure AD tenant as the Customer Service instance.

### Request headers

| Key                          | Type                              | Description                                                                                                                                                                                                 |
|------------------------------|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ApiVersion                   | String                           | The CCaaS API version.                                                                                                                                                                         |
| ProactiveEngagementConfigId  | String                           | Id of the Proactive Engagement Configuration to use. This specifies dial mode type, workstream, and outbound profile to use. To get this ID, do the following: <ol><li> Go to [Power Apps](https://make.preview.powerapps.com) and select the required environment.</li><li> Select **Tables** > **Proactive Engagement Configuration**</li><li> Select the ID of the required record.</li></ul>       |
| DestinationPhoneNumber       | String                           | Phone number of the customer to call.|
| ContactId                    | String                           |  Id of the customer contact in Dynamics CRM.|
| Windows                      | JSON array of Window objects     | Specifies the valid time periods when the outbound call may be placed. If not provided, the system defaults to a 24-hour window starting immediately (from current time until 24 hours later).                           |
| InputAttributes              | JSON object of key-value strings | Optional. Variables that can be referenced within Copilot agent flows to customize behavior, drive conditional logic, or retrieve personalized information from Dataverse records. |

### Windows object

| Key   | Type   | Description                                                                                   |
|-------|--------|-----------------------------------------------------------------------------------------------|
| Start | String | The beginning timestamp for this window. Must be specified in UTC in the `yyyy-MM-ddTHH:mm:ss.fffZ` format.           |
| End   | String | The end timestamp for this window. Must be specified in UTC in the `yyyy-MM-ddTHH:mm:ss.fffZ` format.                |
> [!IMPORTANT]
> Some clients require a specific format such as `"Windows": "[{\"Start\":\"2025-01-30T16:32:45.930Z\",\"End\":\"2025-06-25T16:32:45.930Z\"}]"`. We recommend that you test accordingly.

### Sample request

```
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "cbbac510-3e66-ef11-a671-6045bd03d9d8",
  "DestinationPhoneNumber": "+123456798",
  "ContactId": "761e062f-c734-ef11-8e4f-00224808a166",
  "Windows": [
    {
      "Start": "2024-09-10T13:00:00.000Z",
      "End": "2024-09-10T15:59:59.999Z"
    },
    {
      "Start": "2024-09-11T13:00:00.000Z",
      "End": "2024-09-11T15:59:59.999Z"
    }
  ],
  "InputAttributes": {
    "orderNumber": "ORD123456789",
    "type": "callback",
    "isFinalAttempt": "false"
  }
}

```

### Response details

If successful, this method returns `DeliveryId`. Delivery ID is a unique identifier assigned to each proactive engagement request that is accepted through the API and is stored in the msdyn_proactive_delivery table.

The sample response is as follows:

```
{
  "@odata.context": "[Organization URI]api/data/v9.2/$metadata#Microsoft.Dynamics.CRM.CCaaS_CreateProactiveVoiceDeliveryResponse",
  "DeliveryId": "9838deee-0b4e-4116-bf73-ecb80474568d"
}
```

### Related information

[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  
