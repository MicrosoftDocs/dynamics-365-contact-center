---
title: Use /conversation/{conversationId}/messages endpoint
description: Learn how to use the conversation/{conversationId}/messages endpoint.
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use /conversation/{conversationId}/messages endpoint

Retrieves a list of all messages exchanged in an active conversation. The response is structured using the [Bot Framework Activity Schema](https://learn.microsoft.com/en-us/javascript/api/botframework-schema/activity?view=botbuilder-ts-latest).

If there are no messages for the given conversation ID, the API returns an empty array.

---

## Method

`GET`

## URL

`/api/v1.0/consumer/conversation/{conversationId}/messages`


##  Route Parameters

| Parameter        | Description                   | Type     | Required |
|------------------|-------------------------------|----------|----------|
| `conversationId` | The unique ID of the conversation to retrieve messages for | `GUID` string | Yes |

---

## Query Parameters (Optional)

 Query parameters allow you to filter, limit, and paginate the messages returned by the API for more efficient data retrieval.

| Parameter           | Description                                                                 | Type                      |
|---------------------|-----------------------------------------------------------------------------|---------------------------|
| `StartTimeStamp`    | Filters messages sent **after** the given timestamp. Must be ISO 8601 and URL-encoded. | `DatetimeOffset (ISO 8601)` |
| `PageSize`          | Maximum number of messages to return. Default: 50, Max: 100.                | `integer`                 |
| `ContinuationToken` | Used to retrieve the next batch of results for pagination. URL-encoded.     | `DatetimeOffset`          |

---

##  Response Payload

```json
{
  "messages": [
    {
      "type": "message",
      "attachments": [],
      "text": "Message 1",
      "messageid": "12313",
      "timestamp": "2025-04-15T12:37:00+00:00",
      "from": {},
      "channelData": {}
    },
    {
      "type": "message",
      "attachments": [],
      "text": "Message 2",
      "messageid": "12314",
      "timestamp": "2025-04-15T12:38:00+00:00",
      "from": {},
      "channelData": {}
    }
  ],
  "continuationtoken": "2025-04-15T12:38:00+00:00"
}
```

## Response parameters

| Tier 1 Key          | Tier 2 Key    | Tier 3 Key | Description                                   | Type             |
| ------------------- | ------------- | ---------- | --------------------------------------------- | ---------------- |
| `messages`          | `[ ]`         | —          | JSON array of Bot Framework activity objects  | `array`          |
|                     | `type`        | —          | Type of message (e.g., `message`)             | `string`         |
|                     | `attachments` | `[ ]`      | Array of attachments (if any)                 | `array`          |
|                     | `text`        | —          | Message content                               | `string`         |
|                     | `messageid`   | —          | Unique ID of the message                      | `string`         |
|                     | `timestamp`   | —          | Timestamp when the message was sent           | `DatetimeOffset` |
|                     | `from`        | —          | Sender metadata                               | `object`         |
|                     | `channelData` | —          | Additional message metadata                   | `object`         |
| `continuationtoken` | —             | —          | Token for retrieving the next page of results | `DatetimeOffset` |
