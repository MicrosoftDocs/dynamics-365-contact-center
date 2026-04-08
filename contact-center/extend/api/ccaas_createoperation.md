---
title: Use CCaaS_CreateOperation API
description: Learn about the CCaaS_CreateOperation API that enables you to suspend, resume, or cancel proactive engagement operations in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.date: 04/06/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_CreateOperation API

Use the `CCaaS_CreateOperation` API to request a cancel, suspend, or resume operation on the Proactive Engagement Service.

|  Property              | Value                                       |
|------------------------|---------------------------------------------|
| URL                    | `https://<orgurl>/api/data/v9.2/CCaaS_CreateOperation` |
| Version                | 1.0                                         |
| OData Operation        | Action                                      |
| OData Type             | Bounded                                     |
| HTTP Verb              | POST                                        |
| Authorization          | Required. Must contain a valid Microsoft Entra Bearer token for the user making the API call. |

## Request parameters

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| ApiVersion | string | Yes | Must be set to `1.0`. |
| ProactiveEngagementConfigId | string | No | The proactive engagement configuration ID. |
| DeliveryId | string | No | For cancel operations, the ID of the delivery to cancel. |
| Operation | string | Yes | The operation to perform: `Suspend`, `Resume`, or `Cancel`. |

## Sample request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "47089bbe-deb7-ef11-b8e6-000d3a36a6b3",
  "Operation": "Resume"
}
```

## Response status codes

| HTTP status | Description |
|-------------|-------------|
| 202 | Accepted |
| 400 | Bad Request (wrong input parameters) |
| 401 | Unauthorized |
| 404 | Resource not found |
| 429 | Rate limit (too many requests) |
| 405 | API not allowed |

### Related information

[Use CCaaS_CreateProactiveVoiceDelivery API](ccaas_createproactivevoicedelivery.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  