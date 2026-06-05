---
title: Use CCaaS_CancelDeliveryTask API
description: Learn about the CCaaS_CancelDeliveryTask API that enables organizations to cancel pending and future proactive delivery attempts in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.date: 06/05/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_CancelDeliveryTask API

You can use the `CCaaS_CancelDeliveryTask` API to cancel all pending and future delivery attempts for a contact or an account. When a delivery task is canceled, no further attempts are made for the associated contact(s).

## Prerequisites

- You must have the Omnichannel agent or Omnichannel supervisor role.
- Proactive engagement is configured. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).
- A delivery task must have been created using the [CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md).

## Request details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CancelDeliveryTask`
- **Method**: POST
- **Version**: 1.0
- **OData Operation**: Action
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Microsoft Entra ID Bearer token for the user making the API call. This token must be issued from the same Microsoft Entra ID tenant as the contact center instance.

## Request parameters

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| ApiVersion | String | Yes | The CCaaS API version. |
| DeliveryTaskId | String (GUID) | Yes | The unique identifier of the delivery task to cancel. This value is returned in the response of the [CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md). |

## Sample request

```json
{
  "ApiVersion": "1.0",
  "DeliveryTaskId": "f47ac10b-58cc-4372-a567-0e02b2c3d479"
}
```

### Related information

[Use CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md)  
[Use CCaaS_CreateProactiveVoiceDelivery API](ccaas_createproactivevoicedelivery.md)  
[Use CCaaS_CreateOperation API](ccaas_createoperation.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  
