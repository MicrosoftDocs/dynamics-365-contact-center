---
title: Use webhook to receive messages and events
description: Learn how to use webhook to receive messages and events.
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use webhook to receive messages and events

When a conversation is active, events and messages from the customer service representative are sent to your configured webhook endpoint. The webhook is required for receiving real-time updates in your custom messaging channel.

The service is retried three times, with a 10-second timeout on each attempt. 

## Endpoint
 
 `{webhook_url}/v3/conversations/{conversationId}/activities`

 Where 

 
- `{webhook_url}` is the base URL you configured in your custom channel.
- `{conversationId}` with the GUID of the active conversation.



## Method

`POST`


## Request Headers

| Header        | Description                                             | 
|----------------|---------------------------------------------------------|
| `x-ms-token`   | Authorization token   

---

## Retry Policy

- The webhook service **retries up to three times**.
- Each retry allows a **10-second timeout**.
- After three failed attempts, no further retries are made.



## Request Payload

Payloads follow the [Bot Framework Activity Schema](/javascript/api/botframework-schema/activity?view=botbuilder-ts-latest). The structure includes message content, activity type, sender details, and optional attachments.

### Request Body Fields

| Tier 1 Key     | Tier 2 Key         | Tier 3 Key       | Description                            | Type                |
|----------------|--------------------|------------------|----------------------------------------|---------------------|
| `type`         |                    |                  | Type of activity (`message`, `event`, `typing`) | `string` (max 256)  |
| `channelId`    |                    |                  | Identifier of the channel (for example, `"MessagingApi"`) | `string` (max 256)  |
| `from`         |                    |                  | Sender object                          | `object`            |
|                | `id`               |                  | Sender ID                              | `string` (max 256)  |
|                | `name`             |                  | Sender display name                    | `string` (max 256)  |
| `conversation` | `id`               |                  | Conversation ID                        | `string` (max 256)  |
| `textFormat`   |                    |                  | Format of the message text (`markdown`) | `string` (max 256)  |
| `attachments`  | `[ ]`              |                  | List of attachments (if any)           | `array`             |
|                | `contentType`      |                  | MIME type of the attachment            | `string` (max 256)  |
|                | `contentUrl`       |                  | File URL                               | `string`            |
|                | `content`          |                  | Typically `null`                       | —                   |
|                | `name`             |                  | Name of the file                       | `string` (max 256)  |
|                | `thumbnailUrl`     |                  | Typically `null`                       | —                   |

---

## Supported activity types

| Type            | Description                               |
|------------------|-------------------------------------------|
| `message`        | Standard text or rich message from agent  |
| `typing`         | Indicates the agent is typing             |
| `event`          | System-level events like join/close       |

---

## 📘 Event Activity Names

The following values are sent in the **name** field of `event` activities:

- `AgentAccepted`
- `AgentClosed`
- `AgentDisconnected`
- `AgentEndedSession`
- `AgentJoinedConversation`
- `AgentTransferAcceptedSession`
- `AgentTransferFailed`
- `ConversationClosed`
- `OutOfOperatingHoursDueToHoliday`
- `OutOfOperatingHoursDueToNonWorkingHours`
- `QueueTransferFailed`



## Sample payloads

The example payloads represent different types of real-time activities, such as messages, typing indicators, agent events, and attachments that the application sends to your webhook during an active conversation.

### Agent Accepted

```json
{
  "type": "message",
  "channelId": "<custom channel Id GUID>",
  "conversation": {
    "id": "{conversation_id}"
  },
  "text": "EventName: **_AgentAccepted_**",
  "name": "AgentAccepted"
}

```

### Agent Typing

```json

{
  "type": "typing",
  "channelId": "MessagingApi",
  "conversation": {
    "id": "{conversation_id}"
  },
  "recipient": {
    "id": "{recipient_id}"
  }
}
```
### Agent Message

```json

{
  "type": "message",
  "channelId": "<custom channel Id GUID>",
  "from": {
    "id": "{sender_id}",
    "name": "{sender_name}"
  },
  "conversation": {
    "id": "{conversation_id}"
  },
  "textFormat": "markdown",
  "text": "hello"
}
```
### Agent Send Attachment
``` json

{
  "type": "message",
  "channelId": "<custom channel Id GUID>",
  "from": {
    "id": "{sender_id}",
    "name": "{sender_name}"
  },
  "conversation": {
    "id": "{conversation_id}"
  },
  "textFormat": "markdown",
  "attachments": [
    {
      "contentType": "image/jpeg",
      "contentUrl": "{attachment_url}",
      "content": null,
      "name": "issue (1).jpg",
      "thumbnailUrl": null
    }
  ]
}
```

### Agent Closed
``` json

{
  "type": "message",
  "channelId": "<custom channel Id GUID>",
  "from": {
    "id": "{sender_id}"
  },
  "conversation": {
    "id": "{conversation_id}"
  },
  "text": "EventName: **_AgentClosed_**",
  "name": "AgentClosed"
}
Conversation Closed
json
Copy
Edit
{
  "type": "message",
  "channelId": "<custom channel Id GUID>",
  "from": {
    "id": "{sender_id}"
  },
  "conversation": {
    "id": "{conversation_id}"
  },
  "text": "EventName: **_ConversationClosed_**",
  "name": "ConversationClosed"
}
```

## Response

200 HTTP Code 
  
