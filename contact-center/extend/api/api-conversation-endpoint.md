---
title: Use /conversation/{id} endpoint
description: Learn how to use the /conversation/{id} endpoint in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use /conversation/{id} endpoint

This endpoint lets you send an activity to an ongoing conversation. The request follows the [Bot Framework Activity Schema](https://github.com/microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md).

Send various types of activities, such as messages, typing indicators, or conversation closure events.

---

## Method

`POST`

## URL

`/api/v1.0/consumer/conversation/{conversationId}`

## Supported activity types

- `message`: Sends a message (optionally with attachments)
- `typing`: Indicates the user is typing
- `endOfConversation`: Ends the conversation
- `event`: Custom events inform the system of an event without needing to send a message and support sending metadata  

If you pass an unsupported event name in an `event` type, the API returns a 400 error.

---

## Message payload

The payload for this API is a JSON-formatted object that defines the activity being sent to the conversation—such as a message, typing indicator, or end-of-conversation event—based on the Bot Framework activity schema.


### Payload for message, automated message, and attachment

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

### Message payload field reference

| Tier 1 Key              | Tier 2 Key           | Description                                                                 | Type                      | Max Length              |
|-------------------------|----------------------|-----------------------------------------------------------------------------|---------------------------|--------------------------|
| type                  |                      | Type of activity being sent. For messages, use "message".                | string                  | 256 characters           |
| id                    |                      | An optional identifier for the message.                                       | string                  | —                        |
| channelId             |                      | The GUID of the messaging channel. It must match the channel used in headers.     | GUID                     | —                        |
| from                  |                      | Object containing sender info. Optional.                                   | object                   | —                        |
|                         | id                   | ID of the sender. Optional.                                                | string                   | 256 characters           |
|                         | name                 | Display name of the sender.                             | string                   | 256 characters           |
| text                   |                      | Text content of the message. Required if no attachments are present.       | string                   | 6,000 characters           |
| attachments           |                      | Array of attachment objects. Required if no text is provided. Learn more in [Configure file attachment capability](/dynamics365/customer-service/administer/configure-file-attachment).           | array of objects        | —                        |
|                         | contentType        | MIME type of the attachment. For example, image/png, application/pdf.        | string                  | 256 characters           |
|                         | contentUrl         | URL or embedded base64 content for the file.                               | string                  | —                        |
|                         | name               | Name of the file including extension.                                      | string                  | 256 characters           |
| channelData.messagingapi-oc | type        | Optional. If "AutomatedMessage", marks the message as automated.         | string                  | 256 characters           |

> [!NOTE] 
> Either `text` or `attachments` must be provided. If both are missing, the request is rejected.

### End-of-conversation payload

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
| type           | endOfConversation  | string |
| channelId      | Channel GUID           | GUID   |
| conversation   | Object containing id | object |
| id             | Conversation ID        | GUID   |

### Typing indicator

```json
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
| type            | typing                 | string |
| channelId       | Channel GUID               | GUID   |
| from.name       | Display name of the sender | string |
| conversation.id | Conversation ID            | GUID   |

## Custom events

Custom events let you send structured data and trigger system processes in ongoing conversations without showing messages to customer service representatives.

### Request payload

```json
{
  "conversation": {
    "id": "{conversation-id-guid}"
  },
  "type": "event",
  "channelData": {
    "customEvent": true,
    "customEventName": "TestEvent",
    "customEventValue": "{ \"stringVar\": \"Hello world! 123456\", \"numberVar\": -10.5, \"boolVar\": true, \"displayableVar\": { \"isDisplayable\": true, \"value\": \"Hello again!\" } }"
  },
  "name": "TestEvent"
}
```

**Payload schema**

| Tier 1 Key | Tier 2 Key | Description | Type | Max Length |
|------------|------------|-------------|------|------------|
| type | | Type of activity being sent. For events, use "event". | string | 256 characters |
| id | | Optional identifier for the message. | string | — |
| channelId | | GUID of the messaging channel. This must match the channel used in headers. | GUID | — |
| from | | Object containing sender info. Optional. | object | — |
| | id | ID of the sender. This is optional. | string | 256 characters |
| | name | Display name of the sender that appears to the service representative. | string | 256 characters |
| name | | Name of the event | string | 256 characters |
| channelData | | | object | — |
| | customEvent | True when sending event | Boolean | — |
| | customEventName | Name of the event | string | — |
| | customEventValue | JSON-encoded string containing variables as objects with key names and values. Use the displayable flag to control whether specific values are visible to service representatives. For more information, see [setcontextprovider](/dynamics365/customer-service/develop/reference/methods/setcontextprovider). | string | — |

> [!NOTE] 
> Learn more in [Configure Copilot Studio agent custom events](../configure-custom-messaging-channel.md).

### Response

The API shows the following response.

```json
{
  "messageId": "1234567890123"
}
```

**Field Descriptions**

| Field | Description | Type |
|-------|-------------|------|
| messageId | The messageId is a 13-digit string epoch timestamp that you can use for message ordering to match the message order. | string |