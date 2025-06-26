---
title: Use /conversation/{id} endpoint
description: Learn how to use the /conversation/{id} endpoint.
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use /conversation/{id} endpoint

This endpoint allows you to send an activity to an ongoing conversation. The request must follow the [Bot Framework Activity Schema](https://github.com/microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md).

You can send various types of activities such as messages, typing indicators, or conversation closure events.

---

## Method

`POST`

## URL

`/api/v1.0/consumer/conversation/{conversationId}`

## Supported Activity Types

- `message` – Send a message (optionally with attachments)
- `typing` – Indicate the user is typing
- `endOfConversation` – End the conversation

If an unsupported event name is passed in an `event` type, the API returns a 400 error.

---

## Message payload

The payload for this API is a JSON-formatted object that defines the activity being sent to the conversation—such as a message, typing indicator, or end-of-conversation event—based on the Bot Framework activity schema.


### Payload for message, automated message, attachment

```json
{
  "type": "message",
  "id": "messageId",
  "channelId": "GUID",
  "from": {
    "id": "FromId",
    "name": "FromDisplayName"
  },
  "conversation": {
    "id": "GUID"
  },
  "text": "Sample message text",
  "attachments": [
    {
      "contentType": "MIME type",
      "contentUrl": "",
      "name": "file name incl. extension"
    }
  ],
  "channelData": {
    "messagingapi-oc": {
      "type": "AutomatedMessage"
    }
  }
}
```

**Payload schema**

### Message payload field reference

| Tier 1 Key              | Tier 2 Key           | Description                                                                 | Type                      | Max Length              |
|-------------------------|----------------------|-----------------------------------------------------------------------------|---------------------------|--------------------------|
| `type`                  |                      | Type of activity being sent. For messages, use `"message"`.                | `string`                  | 256 characters           |
| `id`                    |                      | Optional identifier for the message.                                       | `string`                  | —                        |
| `channelId`             |                      | GUID of the messaging channel. Must match the channel used in headers.     | `GUID`                    | —                        |
| `from`                 |                      | Object containing sender info. Optional.                                   | `object`                  | —                        |
|                         | `id`                 | ID of the sender. Optional.                                                | `string`                  | 256 characters           |
|                         | `name`               | Display name of the sender shown to the agent.                             | `string`                  | 256 characters           |
| `text`                  |                      | Text content of the message. Required if no attachments are present.       | `string`                  | 6,000 characters           |
| `attachments`           |                      | Array of attachment objects. Required if no `text` is provided.            | `array` of objects        | —                        |
|                         | `contentType`        | MIME type of the attachment (for example, `image/png`, `application/pdf`).        | `string`                  | 256 characters           |
|                         | `contentUrl`         | URL or embedded base64 content for the file.                               | `string`                  | —                        |
|                         | `name`               | Name of the file including extension.                                      | `string`                  | 256 characters           |
| `channelData.messagingapi-oc` | `type`        | Optional. If `"AutomatedMessage"`, marks the message as automated.         | `string`                  | 256 characters           |

> [!NOTE] 
> Either `text` or `attachments` must be provided. If both are missing, the request is rejected.

### End of conversation payload

```json
{
  "type": "endOfConversation",
  "channelId": "GUID",
  "conversation": {
    "id": "GUID"
  }
}

```

**Payload schema**


| Key            | Description            | Type     |
| -------------- | ---------------------- | -------- |
| `type`         | `"endOfConversation"`  | `string` |
| `channelId`    | Channel GUID           | `GUID`   |
| `conversation` | Object containing `id` | `object` |
| `id`           | Conversation ID        | `GUID`   |

### Typing indicator

```JSON
{
  "type": "typing",
  "channelId": GUID,
  "from": {
    "name": "FromDisplayName",
  },
  "conversation": {
    "id": GUID
  }
}

```
**Payload schema**

| Key               | Description                | Type     |
| ----------------- | -------------------------- | -------- |
| `type`            | `"typing"`                 | `string` |
| `channelId`       | Channel GUID               | `GUID`   |
| `from.name`       | Display name of the sender | `string` |
| `conversation.id` | Conversation ID            | `GUID`   |
