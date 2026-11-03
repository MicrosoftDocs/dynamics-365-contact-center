---
title: Use CCaaS_CancelProactiveEngagement API
description: Learn about the CCaaS_CancelProactiveEngagement API that enables organizations to cancel pending proactive deliveries by configuration, contact, delivery task, or callback in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: alialtunsu
ms.topic: reference
ms.date: 10/30/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
ai-usage: ai-assisted
---

# Use CCaaS_CancelProactiveEngagement API

Use the `CCaaS_CancelProactiveEngagement` API to cancel proactive outreach that hasn't started. You can cancel pending outreach for a proactive engagement configuration, a specific contact, or an individual delivery task or callback.

The API cancels the following tasks:

- **Delivery tasks** that aren't completed yet (status `Queued` or `Sent`), and the deliveries of those tasks that haven't started. A canceled delivery task makes no further attempts, including retries and calls or messages to the next contacts in the chain. Delivery tasks are created by the [CCaaS_CreateProactiveDelivery](ccaas_createproactivedelivery.md), [CCaaS_CreateSimpleProactiveDelivery](ccaas_createsimpleproactivedelivery.md), and [CCaaS_CreateProactiveBulkDelivery](ccaas_createproactivebulkdelivery.md) APIs.
- **Pending deliveries created by Customer Insights - Journeys** for the contact or configuration in the request.

The API doesn't cancel the following tasks:

- **Deliveries that already started.** A call that's being dialed, or that was offered to a representative, isn't stopped.
- **Deliveries created after the request.** The API cancels what exists when you call it. It doesn't prevent new deliveries from being created for the same contact later.
- **Deliveries created by [CCaaS_CreateProactiveVoiceDelivery](ccaas_createproactivevoicedelivery.md) or [CCaaS_CreateProactiveSMSDelivery](ccaas_createproactivesmsdelivery.md).** These deliveries aren't linked to a delivery task or a journey. Use [CCaaS_CreateOperation](ccaas_createoperation.md) with the `Cancel` operation to cancel them.

## Prerequisites

- Proactive engagement is configured. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).
- Your security role grants read access to proactive engagement configurations. The API also checks your access to the configuration that the request targets. Learn more in [Permissions](#permissions).

## Request details

- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_CancelProactiveEngagement`
- **Method**: POST
- **Version**: 1.0
- **OData Operation**: Action
- **OData Type**: Unbounded
- **Request Authorization**: Required. Must contain a valid Microsoft Entra ID Bearer token for the user making the API call. This token must be issued from the same Microsoft Entra ID tenant as the contact center instance.

## Request parameters

| Key | Type | Required | Description |
|-----|------|----------|-------------|
| ApiVersion | String | Yes | The CCaaS API version. Must be set to `1.0`. |
| ProactiveEngagementConfigId | String (GUID) | No |The proactive engagement configuration whose deliveries you want to cancel. Combine it with `ContactId` or `ExternalContactId` to limit the cancellation to one contact in this configuration. |
| ContactId | String (GUID) | No | The Dataverse contact ID of the contact whose deliveries to cancel. |
| ExternalContactId | String | No | The value of the contact's unique identifier column, as configured for the proactive engagement. Learn more about the unique identifier column in the **Details** step for [voice](../../administer/configure-proactive-engagement-voice.md#details) or [messaging](../../administer/configure-proactive-engagement-messaging.md#details). Requires `ProactiveEngagementConfigId`. |
| DeliveryTaskId | String (GUID) | No | The delivery task to cancel. This value is returned in the response of the [CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md). |
| CallbackConversationId | String (GUID) | No | The ID of the conversation in which the customer requested a callback. Cancels the scheduled callback. |

Provide at least one of `ProactiveEngagementConfigId`, `ContactId`, `ExternalContactId`, `DeliveryTaskId`, or `CallbackConversationId`.

## Supported combinations

| Parameters | What's canceled |
|------------|-----------------|
| `ProactiveEngagementConfigId` | All delivery tasks of the configuration, and the configuration's pending journey deliveries that were created before the request. Journey deliveries are canceled in the background, shortly after the API returns. |
| `ProactiveEngagementConfigId` and `ContactId` | The contact's delivery tasks in the configuration, and the contact's pending journey deliveries in the configuration. A delivery task is canceled when the contact is any contact in its chain. |
| `ContactId` | The contact's delivery tasks and pending journey deliveries in every configuration. Requires read access to all proactive engagement configurations in the organization. |
| `ProactiveEngagementConfigId` and `ExternalContactId` | The delivery tasks and pending journey deliveries in the configuration of every contact whose unique identifier column matches `ExternalContactId`. |
| `DeliveryTaskId` | The delivery task and its pending deliveries. The task must have the status `Queued` or `Sent`. To cancel a callback, use `CallbackConversationId` instead. |
| `CallbackConversationId` | The scheduled callback that was requested in the conversation. The pending callback conversation is closed. |

Callbacks aren't canceled by the configuration or contact parameters. The API rejects these combinations with `400 Bad Request`:

- `DeliveryTaskId` or `CallbackConversationId` together with any other scope parameter. Send each of them on its own.
- `ContactId` together with `ExternalContactId`.
- `ExternalContactId` without `ProactiveEngagementConfigId`.
- A GUID parameter that's empty (`00000000-0000-0000-0000-000000000000`) or isn't a valid GUID.

## Permissions

The API checks your access to the target of each request:

| Request | Required access |
|---------|-----------------|
| `ProactiveEngagementConfigId`, with or without `ContactId` or `ExternalContactId` | Read access to that proactive engagement configuration. |
| `ContactId` without `ProactiveEngagementConfigId` | Read access to every proactive engagement configuration in the organization. If you don't have it, include `ProactiveEngagementConfigId` to limit the request to one configuration. |
| `DeliveryTaskId` | Read access to the proactive engagement configuration that owns the delivery task. |
| `CallbackConversationId` | Permission to call the API. |

If the access check fails, the API returns `403 Forbidden` and cancels nothing.

## Sample requests

Cancel everything that's pending for one contact in a proactive engagement configuration:

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "47089bbe-deb7-ef11-b8e6-000d3a36a6b3",
  "ContactId": "f47ac10b-58cc-4372-a567-0e02b2c3d479"
}
```

Cancel everything that's pending for a proactive engagement configuration:

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "47089bbe-deb7-ef11-b8e6-000d3a36a6b3"
}
```

Cancel deliveries for a contact identified by an external ID:

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "47089bbe-deb7-ef11-b8e6-000d3a36a6b3",
  "ExternalContactId": "CUST-000123"
}
```

Cancel a single delivery task:

```json
{
  "ApiVersion": "1.0",
  "DeliveryTaskId": "06c94046-c18d-4f4b-9770-e43116f96461"
}
```

Cancel a scheduled callback:

```json
{
  "ApiVersion": "1.0",
  "CallbackConversationId": "9c2b6f3e-4a1d-4f7b-8e2a-1d5c3b7a9e40"
}
```

## Response

The API doesn't return a response body. A successful request returns `204 No Content`, including when nothing matched the request. The response doesn't report how many delivery tasks or deliveries were canceled.

Canceled deliveries get the status `Cancelled`. The [msdyn_proactive_delivery](../proactive-engagement-tables.md#msdyn_proactive_delivery) table is updated by a periodic synchronization, so the new status can take several minutes to appear there.

| HTTP status | Description |
|-------------|-------------|
| `204 No Content` | The request was processed. |
| `400 Bad Request` | The parameters or their combination aren't valid, the delivery task isn't in a state that can be canceled, or `ExternalContactId` isn't compatible with the configured unique identifier column. Review the returned error message. |
| `401 Unauthorized` | The request doesn't contain a valid bearer token. |
| `403 Forbidden` | You don't have access to the configuration that the request targets. Learn more in [Permissions](#permissions). |
| `404 Not Found` | The delivery task or callback wasn't found. |
| `429 Too Many Requests` | The rate limit was exceeded. Retry the request later. |
| `500 Internal Server Error` | The service couldn't complete the request. You can safely retry the request. |

### Related information

[Use CCaaS_CreateProactiveDelivery API](ccaas_createproactivedelivery.md)  
[Use CCaaS_GetDeliveryTasks API](ccaas_getdeliverytasks.md)  
[Use CCaaS_CancelDeliveryTask API](ccaas_canceldeliverytask.md)  
[Use CCaaS_CreateOperation API](ccaas_createoperation.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)  
