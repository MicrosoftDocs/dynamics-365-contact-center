---
title: Use /conversation/{conversationId}/messages endpoint
description: Learn how to retrieve messages from a conversation using the /conversation/{conversationId}/messages endpoint. Includes filtering, pagination, and response details.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---


# Use /conversation/{conversationId}/messages endpoint

Retrieve a list of all messages exchanged in an active conversation. The response is structured using the [Bot Framework Activity Schema](/javascript/api/botframework-schema/activity?view=botbuilder-ts-latest).

If there aren't any messages for the given conversation ID, the API returns an empty array.

> [!NOTE]
> Don't use the conversations endpoint as a polling mechanism. Conversation events are posted to Microsoft, and updates are posted back to your subscribed webhook.

## Method

`GET`

## Url

`/api/v1.0/consumer/conversation/{conversationId}/messages`


## Request parameters

| Parameter        | Description                   | Type     | Required |
|------------------|-------------------------------|----------|----------|
| conversationId | The unique ID of the conversation to retrieve messages. | GUID string | Yes |

---

## Query parameters (optional)

 Query parameters let you filter, limit, and paginate the messages returned by the API for efficient data retrieval.

| Parameter           | Description                                                                 | Type                      |
|---------------------|-----------------------------------------------------------------------------|---------------------------|
| StartTimeStamp      | Filters messages sent after the given timestamp. The timestamp must be in ISO 8601 format and URL-encoded. | datetimeoffset (ISO 8601) |
| PageSize            | Specifies the maximum number of messages to return. The default is 50, and the maximum is 100.                | integer                 |
| ContinuationToken   | Retrieves the next batch of results for pagination. The token must be URL-encoded.     | DatetimeOffset          |

---

## Response payload

```json
{
  "messages": [
    {
      "type": "message",
      "attachments": [],
      "text": "Message 1",
      "messageId": "12313",
      "timestamp": "2025-04-15T12:37:00+00:00",
      "from": {},
      "channelData": {}
    },
    {
      "type": "message",
      "attachments": [],
      "text": "Message 2",
      "messageId": "12314",
      "timestamp": "2025-04-15T12:38:00+00:00",
      "from": {},
      "channelData": {}
    }
  ],
  "continuationToken": "2025-04-15T12:38:00+00:00"
}
```

## Response parameters

| Tier 1 Key          | Tier 2 Key    | Tier 3 Key | Description                                   | Type             |
| ------------------- | ------------- | ---------- | --------------------------------------------- | ---------------- |
| messages          | [ ]         | —          | JSON array of Bot Framework activity objects  | array          |
|                     | type        | —          | Type of message (for example, message)             | string         |
|                     | attachments | [ ]      | Array of attachments (if any)                 | array          |
|                     | text        | —          | Message content                               | string         |
|                     | messageid   | —          | Unique ID of the message                      | string         |
|                     | timestamp   | —          | Timestamp when the message was sent           | DatetimeOffset |
|                     | from        | —          | Sender metadata                               | object         |
|                     | channelData | —          | Additional message metadata                   | object         |
| continuationtoken   | —             | —          | Token for retrieving the next page of results | DatetimeOffset |
