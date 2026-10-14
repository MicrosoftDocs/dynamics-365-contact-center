---
title: Use CCaaS_CreateProactiveDelivery API
description: Learn how to initiate proactive outbound voice, SMS, MMS, and WhatsApp communications in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.date: 10/14/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template
---

# Use CCaaS_CreateProactiveDelivery API

Use the `CCaaS_CreateProactiveDelivery` API to initiate proactive outbound voice calls and SMS, MMS (preview), and WhatsApp (preview) messages through the Proactive Engagement service.

> [!IMPORTANT]
> - Proactive engagement features in MMS and WhatsApp are in public preview.
> - Public preview features are subject to [supplemental terms of use](https://www.microsoft.com/en-us/business-applications/legal/supp-powerplatform-preview/).

[!INCLUDE [proactive-api-guidance](../../includes/proactive/cc-proactive-api-guidance.md)]

> [!IMPORTANT]
> If your organization uses the `CCaaS_CreateProactiveDelivery` API to initiate an outbound voice call or message, your organization is responsible for managing consent and opt-out preferences, maintaining do-not-contact lists, and setting quiet hours. Make sure that you:
>
> - Obtain consent before contacting customers.
> - Contact customers only during permitted hours.

Learn more about channel-specific consent support in [Manage consent for proactive engagement](../../administer/proactive-engagement-manage-consent.md). MMS uses SMS consent handling. During public preview, WhatsApp proactive deliveries use SMS/text consent records and opt-out status.

## Prerequisites

- You must have the Omnichannel agent or Omnichannel supervisor role to call this API.
- Configure proactive engagement. Learn more in [Configure proactive engagement](../../administer/configure-proactive-engagement.md).

## Request details

- **URL:** `https://<orgurl>/api/data/v9.2/CCaaS_CreateProactiveDelivery`
- **Method:** POST
- **Version:** 1.0
- **OData operation:** Action
- **OData type:** Unbounded
- **Request authorization:** Required. Include a valid Microsoft Entra access token in the `Authorization: Bearer <access-token>` header. The token must be issued for your Dataverse environment and from the same Microsoft Entra tenant as that environment.

## Request body properties

| Key | Type | Required | Applicable channels | Description |
|---|---|---|---|---|
| `ApiVersion` | String | Yes | All | The CCaaS API version. The current value is `1.0`. |
| `ProactiveEngagementConfigId` | String | Yes | All | The ID of the Proactive Engagement Configuration to use. The configuration determines the channel, dial mode, workstream, outbound profile, and configured message template. To get the ID, go to [Power Apps](https://make.preview.powerapps.com), select the required environment, select **Tables** > **Proactive Engagement Configuration**, and then select the ID of the required record. |
| `RequestId` | String | No | All | A client-supplied idempotency key. Use a new value, such as a GUID, for each logical request. If you retry a request after a network failure, reuse the same value so that the service returns the existing delivery instead of creating a duplicate. You can also use this value to correlate the request with your source system. Requests without a value don't receive idempotency protection. |
| `Priority` | String | No | All | A custom sort value used to order records within an engagement. The value must be a non-negative number or a date in `yyyy-MM-dd` format. The value is used only when **Call order** or **Message order** is set to **Custom priority ascending** or **Custom priority descending**. Otherwise, it's ignored. This value is separate from the engagement-level **Normal**, **High**, or **Critical** priority. |
| `Contacts` | String containing a JSON array of Contact objects | Yes | All | The contacts included in the request. Voice supports up to five contacts for contact chaining. SMS, MMS, and WhatsApp support one contact per request. At least one phone number is required for each contact. |
| `EarliestScheduleDate` | String | No | All | An ISO 8601 UTC timestamp before which the engagement must not start. If omitted, processing can start immediately. |
| `ExpirationDate` | String | No | All | An ISO 8601 UTC timestamp after which the request is no longer attempted. The value must be in the future, no more than 30 days from the current time, later than `EarliestScheduleDate`, and at or after the latest contact window end. |
| `Message` | String | No | SMS (text-only) | The message content to deliver to the contact. For an SMS proactive configuration, this value overrides the configured template text. The engagement must still have a message template configured. Don't use this parameter for MMS or WhatsApp. |
| `MessageAttributes` | String containing a JSON object | No | MMS | Delivery-type-specific message content and attributes. For MMS, a configured message template isn't required. `MessageAttributes` overrides the value configured for the proactive engagement. Learn more in [MessageAttributes object](#messageattributes-object). |

## Contact object

| Key | Type | Required | Applicable channels | Description |
|---|---|---|---|---|
| `uniqueIdentifier` | String | Yes | All | The unique identifier of the contact. The value can be a ContactId or an external ID. |
| `firstName` | String | No | All | The contact's first name. |
| `lastName` | String | No | All | The contact's last name. |
| `mobilePhoneNumber` | String | Yes for messaging; conditionally required for voice | All | The contact's mobile phone number in E.164 format, such as `+12025550100`. SMS, MMS, and WhatsApp require this value. For voice, provide at least one mobile, business, or home phone number. |
| `businessPhoneNumber` | String | No | Voice | The contact's business phone number. |
| `homePhoneNumber` | String | No | Voice | The contact's home phone number. |
| `email` | String | No | All | The contact's email address. |
| `postalCode` | String | No | All | The contact's postal code. |
| `state` | String | No | All | The contact's state. |
| `country` | String | No | All | The contact's country or region. `country` is the API property name, not a display label. |
| `addressLine` | String | No | All | The contact's address line. |
| `city` | String | No | All | The contact's city. |
| `timeZone` | String | No | All | The contact's time zone. Use a Windows standard time-zone name, such as `Pacific Standard Time` or `Eastern Standard Time`, or a Dataverse time-zone code as a string, such as `"35"`. Display names such as `(GMT-08:00) Pacific Time` and IANA names such as `America/Los_Angeles` aren't accepted. |
| `inputAttributes` | JSON object of key-value strings | No | All | Variables that can be referenced in Copilot agent flows or message templates. Use this object to provide values for template tokens that aren't contact fields. Token matching is case-insensitive. |
| `windows` | JSON array of Window objects | No | All | Contact-specific delivery windows interpreted in the contact's time zone. Learn more in [Windows object](#windows-object). If omitted, the system uses a 24-hour window that begins immediately or at `EarliestScheduleDate` when that value is in the future. |

> [!NOTE]
> - Contact property-name matching is case-insensitive. This article uses the canonical camelCase names defined by the contact request contract.
> - Phone numbers must use E.164 format and include the leading plus sign (`+`).
> - For voice, each contact must have at least one `mobilePhoneNumber`, `businessPhoneNumber`, or `homePhoneNumber`. For SMS, MMS, and WhatsApp, `mobilePhoneNumber` is required.

## MessageAttributes object

Pass `MessageAttributes` as a JSON-serialized object. Its properties depend on the delivery type specified by `Type`. Currently, `MMS` is the only supported delivery type.

### MMS

An MMS request that supplies content through `MessageAttributes` doesn't require a configured message template. Use the following properties:

| Key | Type | Required | Description |
|---|---|---|---|
| `Type` | String | Yes | Must be `MMS`. The proactive engagement configuration must use the SMS channel. |
| `Body` | String | No | The MMS text body. It can contain contact-field or `inputAttributes` tokens, such as `{{firstName}}`. The maximum length before personalization is 1,600 UTF-16 code units. A media-only MMS can omit this value. |
| `Attachments` | JSON array of Attachment objects | Yes | Dataverse media attachments. Specify between one and 10 attachments. |

#### Attachment object

| Key | Type | Required | Description |
|---|---|---|---|
| `Source` | String | Yes | Must be `entity`. |
| `EntityId` | String (GUID) | Yes | The `msdyncrm_fileid` of an active Dataverse File (`msdyncrm_file`) row that contains the uploaded media. Learn more in [Get a media attachment ID](#get-a-media-attachment-id). |

#### Get a media attachment ID

`EntityId` identifies a row in the [Dataverse File table](/dynamics365/developer/reference/entities/msdyncrm_file). It isn't a file name, file-column identifier, media URL, or shared access signature (SAS).

To find an existing media row:

1. In [Power Apps](https://make.powerapps.com), select the same environment as the proactive engagement configuration.
1. Select **Tables**, locate **File** (logical name `msdyncrm_file`), and inspect the row for the media that you want to use. The primary key is `msdyncrm_fileid`.
1. If the row ID isn't visible in the table view, retrieve it through the Dataverse Web API. For example, the following query lists active file rows:

   ```http
   GET https://<orgurl>/api/data/v9.2/msdyncrm_files?$select=msdyncrm_fileid,msdyncrm_name,statecode&$filter=statecode%20eq%200
   Authorization: Bearer <access-token>
   Accept: application/json
   ```

1. Match the intended file and copy its `msdyncrm_fileid` value to `Attachments[].EntityId`. Use `"Source": "entity"`.

The caller must have permission to read these Dataverse records. Creating the row or setting its name doesn't upload the media. Before you submit the delivery, make sure that the file upload is complete, the row is active, and the media remains available for dispatch. Learn more in [Configure MMS content](../../administer/configure-proactive-engagement-messaging.md#mms-preview).

#### MMS limits

The following limits apply to MMS content:

- **Attachments:** One through 10 attachments per request.
- **`MessageAttributes` string:** Up to 32,768 UTF-16 code units. This limit applies to the JSON string supplied as the value of `MessageAttributes`, not the entire HTTP request, its UTF-8 byte length, or the media files.
- **Body length:** Up to 1,600 UTF-16 code units before personalization.
- **JSON nesting:** A maximum depth of eight within `MessageAttributes`.
- **Supported media file extensions:** `.jpeg`, `.jpg`, `.png`, `.gif`, `.mp3`, `.mp4`, `.mpeg`, `.mpg`, `.pdf`, and `.vcf`.

Most common characters use one UTF-16 code unit. Some characters, including many emoji, use two. Media must have a supported content type. Changing a file extension doesn't change the file format.

The following media size budgets apply to Dataverse-backed MMS attachments:

| Sending provider | Maximum per attachment | Maximum total attachment size | Additional limit |
|---|---|---|---|
| Twilio | 5 MiB (5,242,880 bytes) | 5 MiB (5,242,880 bytes) | All non-image attachments combined: 500 KiB (512,000 bytes). |
| Infobip | 500 KiB (512,000 bytes) | 850 KiB (870,400 bytes) | Both the per-attachment and total limits apply. |

These media budgets don't guarantee that a provider or carrier accepts the message. Provider and carrier restrictions can be more restrictive. Media checks can occur during dispatch by using the sending provider, so an accepted create request can still fail because the media is invalid, unavailable, or oversized. Check the delivery result in addition to the create response.

> [!IMPORTANT]
> Media files uploaded for MMS are publicly accessible through a content delivery network (CDN). Don't upload confidential or sensitive files.

> [!NOTE]
> MMS is a capability of the SMS channel. Don't create a separate MMS channel configuration.

## WhatsApp message content

WhatsApp proactive deliveries use the message template defined in the proactive engagement configuration. The template name, language, and content must match an approved WhatsApp template. Learn more in [Configure WhatsApp content](../../administer/configure-proactive-engagement-messaging.md#whatsapp-preview).

The request doesn't accept a WhatsApp template or free-form WhatsApp message. Add values required by template placeholders to the contact's `inputAttributes` object. Contact fields, such as `firstName`, can also supply template values.

## Windows object

| Key | Type | Required | Description |
|---|---|---|---|
| `start` | String | Yes | The beginning of the window as an ISO 8601 date and time, interpreted in the contact's time zone. |
| `end` | String | Yes | The end of the window as an ISO 8601 date and time, interpreted in the contact's time zone. |

> [!NOTE]
> Window property-name matching is case-insensitive for this API. This article uses the canonical lowercase `start` and `end` names.

For contact windows, the service interprets the supplied date and clock time in the contact's `timeZone` and converts it to UTC for scheduling. A `Z` suffix doesn't override the contact's time zone on this path. If the contact doesn't have a time zone, the service uses UTC.

For example, `2026-09-18T09:00:00Z` with `timeZone` set to `Pacific Standard Time` means 9:00 AM Pacific time (16:00 UTC on that date), not 9:00 AM UTC. To express a contact window in UTC, set the contact's time zone to `UTC`.

The top-level `EarliestScheduleDate` and `ExpirationDate` are separate UTC timestamps. When you combine them with contact windows, account for the windows' UTC equivalents.

## Validation rules

- Each contact must have a `uniqueIdentifier`, and the value must be unique within the request.
- When the proactive engagement configuration uses the default `contactid` unique identifier column, each `uniqueIdentifier` must be a valid GUID. A custom external ID column can accept values in the format required by that column. Learn more about the unique identifier column in the **Details** step for [voice](../../administer/configure-proactive-engagement-voice.md#details) or [messaging](../../administer/configure-proactive-engagement-messaging.md#details).
- Every phone number must use E.164 format, such as `+12025550123`. A malformed number is rejected even if the same contact has another valid number.
- Voice requests can contain one to five contacts. SMS, MMS, and WhatsApp requests must contain exactly one contact.
- For each window, `start` must be the current time or later and earlier than `end`. At least one window must end in the future, and no window can end more than 30 days in the future.
- `ExpirationDate` must be in the future and no more than 30 days ahead. It must be later than `EarliestScheduleDate` and at or after the latest `end` value across all contact windows.

## Sample requests

Replace the sample identifiers and dates with values for your environment. Use future delivery dates within the 30-day limit. Property names such as `country` in these JSON examples are API identifiers and must not be replaced with display labels.

### Voice request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "RequestId": "e1f2a3b4-c5d6-7890-abcd-ef1234567890",
  "Priority": "1",
  "Contacts": "[{\"uniqueIdentifier\":\"f47ac10b-58cc-4372-a567-0e02b2c3d479\",\"firstName\":\"John\",\"lastName\":\"Doe\",\"mobilePhoneNumber\":\"+12025550100\",\"businessPhoneNumber\":\"+12025550101\",\"homePhoneNumber\":\"+12025550102\",\"email\":\"text@a.com\",\"postalCode\":\"25642\",\"state\":\"WA\",\"country\":\"USA\",\"addressLine\":\"1234 227th PL SE\",\"city\":\"Seattle\",\"timeZone\":\"Pacific Standard Time\",\"inputAttributes\":{\"AppointmentTime\":\"10:00 AM\",\"CustomerNumber\":\"1234567\"},\"windows\":[{\"start\":\"2026-12-10T09:00:00.000Z\",\"end\":\"2026-12-10T17:00:00.000Z\"}]}]"
}
```

### SMS request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
  "RequestId": "d3e4f5a6-b7c8-9012-cdef-a12345678901",
  "Priority": "1",
  "Message": "Your appointment is confirmed for tomorrow at 10:00 AM. Reply STOP to opt out.",
  "Contacts": "[{\"uniqueIdentifier\":\"a58bc20c-69dd-5483-b678-1f13c3d4e580\",\"firstName\":\"Jane\",\"lastName\":\"Smith\",\"mobilePhoneNumber\":\"+12025550103\",\"email\":\"jane.smith@example.com\",\"postalCode\":\"98101\",\"state\":\"WA\",\"country\":\"USA\",\"addressLine\":\"5678 Main St\",\"city\":\"Seattle\",\"timeZone\":\"Pacific Standard Time\",\"inputAttributes\":{\"AppointmentTime\":\"10:00 AM\",\"CustomerNumber\":\"7654321\"},\"windows\":[{\"start\":\"2026-12-10T09:00:00.000Z\",\"end\":\"2026-12-10T17:00:00.000Z\"}]}]"
}
```

### MMS request

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "c3d4e5f6-a7b8-9012-cdef-123456789012",
  "RequestId": "e4f5a6b7-c8d9-0123-defa-234567890123",
  "Priority": "1",
  "Contacts": "[{\"uniqueIdentifier\":\"b69cd31d-70ee-6594-c789-2f24d4e5f691\",\"firstName\":\"Alex\",\"lastName\":\"Taylor\",\"mobilePhoneNumber\":\"+12025550104\",\"inputAttributes\":{\"OrderNumber\":\"12345\"}}]",
  "MessageAttributes": "{\"Type\":\"MMS\",\"Body\":\"Hello {{firstName}}, your order {{OrderNumber}} is ready.\",\"Attachments\":[{\"Source\":\"entity\",\"EntityId\":\"f5a6b7c8-d9e0-1234-efab-345678901234\"}]}"
}
```

### WhatsApp request

The following request uses the WhatsApp template and language selected in the proactive engagement configuration. The `OrderNumber` value is available to a matching template placeholder.

```json
{
  "ApiVersion": "1.0",
  "ProactiveEngagementConfigId": "d4e5f6a7-b8c9-0123-defa-234567890123",
  "RequestId": "f5a6b7c8-d9e0-1234-efab-345678901234",
  "Priority": "1",
  "Contacts": "[{\"uniqueIdentifier\":\"c70de42e-81ff-7605-d89a-3f35e5f6a702\",\"firstName\":\"Sam\",\"lastName\":\"Lee\",\"mobilePhoneNumber\":\"+12025550105\",\"inputAttributes\":{\"OrderNumber\":\"98765\"}}]"
}
```

## Response

The API can return the following HTTP status codes:

| Status code | Description |
|---|---|
| `200 OK` | The request was accepted. The response contains `DeliveryTaskId` and `DeliveryId`. Acceptance doesn't confirm that the call or message was delivered. |
| `400 Bad Request` | Request validation failed, such as when an identifier or the serialized contact data is invalid. Review the returned error message. |
| `401 Unauthorized` | Dataverse couldn't authenticate the request. Check the access token and its intended environment. |
| `403 Forbidden` | The caller doesn't have permission to perform the operation or access the target configuration. |
| `404 Not Found` | The organization or proactive engagement configuration wasn't found. |
| `429 Too Many Requests` | Dataverse service protection or proactive request throttling rejected the request. Learn more in [Handle throttling](#handle-throttling). |
| `500 Internal Server Error` | The service couldn't complete the request because of an internal error. Retain the error and request identifiers for troubleshooting. |

Errors can originate from Dataverse authentication, authorization, or the proactive service. Don't assume that every error has the same validation-detail structure, and don't retry invalid requests without changes.

### Sample success response

```json
{
  "DeliveryTaskId": "06c94046-c18d-4f4b-9770-e43116f96461",
  "DeliveryId": "44bca794-ead0-46ab-89ad-b9a634fc654c"
}
```

The identifiers are GUID strings. Dataverse can also include OData annotations, which are omitted from this example. Use [CCaaS_GetDeliveryTasks](ccaas_getdeliverytasks.md) to retrieve task and delivery results.

### Response properties

| Property | Type | Description |
|---|---|---|
| `DeliveryId` | String (GUID) | The unique identifier of the first individual dial or message delivery. Use this value with [CCaaS_CreateOperation](ccaas_createoperation.md) and the `Cancel` operation to cancel that delivery. |
| `DeliveryTaskId` | String (GUID) | The unique identifier of the task that manages the contact chain and all reattempts. Use this value with [CCaaS_CancelDeliveryTask](ccaas_canceldeliverytask.md) to cancel pending and future attempts for the task. |

### Handle throttling

Dataverse service protection, proactive request admission, and outbound message pacing are separate controls. The rate at which create requests are accepted doesn't guarantee the sending rate. Learn more in [Dataverse service protection API limits](/power-apps/developer/data-platform/api-limits).

For HTTP 429 responses:

1. Honor `Retry-After` when the response provides it. Don't assume that every throttling response includes this header.
1. Otherwise, use bounded exponential backoff with jitter and reduce concurrent requests. Stop or defer work when the retry budget is exhausted.
1. Reuse the same `RequestId` when retrying the same logical request to preserve idempotency.

For contact-list intake scenarios, review [CCaaS_CreateProactiveBulkDelivery](ccaas_createproactivebulkdelivery.md) instead of assuming that individual create calls provide unlimited throughput. Bulk intake doesn't bypass consent, delivery scheduling, or channel sending limits.

## Related information

[Use CCaaS_CreateProactiveVoiceDelivery API](ccaas_createproactivevoicedelivery.md)  
[Use CCaaS_CreateOperation API](ccaas_createoperation.md)  
[Use CCaaS_CancelDeliveryTask API](ccaas_canceldeliverytask.md)  
[Configure proactive engagement](../../administer/configure-proactive-engagement.md)  
[Use proactive engagement tables for reporting](../proactive-engagement-tables.md)
