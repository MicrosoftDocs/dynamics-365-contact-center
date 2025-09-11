---
title: Configure Copilot Studio agent custom events
description: Learn how to configure custom events for Microsoft Copilot Studio agents to send and receive contextual data without interrupting user conversations.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---


# Configure Copilot Studio agent custom events

Use Microsoft Copilot Studio agents to send and receive events containing custom data. These events work independently of standard message flows and don't appear in responses from `/api/v1.0/consumer/conversation/{conversationId}/messages`.

This helps the agent understand what the customer does without cluttering the conversation with technical details.

## Receive custom events

You can send custom events from your external systems to trigger specific AI agent behaviors, pass contextual data, or initiate workflows without interrupting the user's conversation flow.

Handle inbound events as activities of type **Message** in Copilot Studio. Use the `Activity.ChannelData.customEvent` flag and the `Activity.ChannelData.customEventName` condition. 

### Example of custom event handling

This example shows a Copilot Studio bot agent topic that parses a JSON string from `Activity.ChannelData.customEventValue` and sends a message using the `stringVar` value:

```yaml
kind: AdaptiveDialog
beginDialog:
  kind: OnActivity
  id: main
  condition: =System.Activity.ChannelData.customEvent = true && System.Activity.ChannelData.customEventName = "TestEvent"
  type: Message
  actions:
    - kind: ParseValue
      id: 6Lq0pb
      variable: Topic.Var1
      valueType:
        kind: Record
        properties:
          boolVar: Boolean
          displayableVar:
            type:
              kind: Record
              properties:
                isDisplayable: Boolean
                value: String
          numberVar: Number
          stringVar: String
      value: =System.Activity.ChannelData.customEventValue

    - kind: SendActivity
      id: sendActivity_5z8cZN
      activity: "{Topic.Var1.stringVar}"

inputType: {}
outputType: {}
```

### API payload example 

Send the following payload to `/api/v1.0/consumer/conversation/{conversationId}` to trigger the example above:

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

## Send custom events

You can configure your Copilot Studio agent to send data back to your external systems when certain conditions are met. Use this to trigger actions in your application, update databases, or notify other services based on conversation events.

Set up the `SendActivity` node in Copilot Studio with the following specifications:

- **Activity Type**: Event
- **Channel Data Requirements**:
  - `customEvent: true`
  - `deliveryMode: "bridged"`

Learn more in [Send an event or activity](/microsoft-copilot-studio/authoring-send-event-activities).

### Example

This example is a Copilot Studio agent topic that triggers an outbound event when it receives a message with the text "outbound event":

```yaml
kind: AdaptiveDialog
beginDialog:
  kind: OnRecognizedIntent
  id: main
  intent:
    triggerQueries:
      - outbound event

  actions:
    - kind: SetVariable
      id: setVariable_OYEivZ
      variable: Topic.Context
      value: "={ stringVar: \"Hello world!\", numberVar: -10.5, boolVar: true, displayableVar: { isDisplayable: true, value: \"Hello again!\" } }"

    - kind: SendActivity
      id: sendActivity_HWCvZ6
      activity:
        kind: Activity
        channelData: "={ customEvent: true, customEventName: \"CustomTest\", customEventValue: JSON(Topic.Context), deliveryMode: \"bridged\" }"
        activityType: Event

    - kind: CancelAllDialogs
      id: L4rn5o

inputType: {}
outputType: {}
```

### Webhook payload

Copilot Studio sends this payload to your webhook:

```json
{
  "Type": "event",
  "Id": "1756399395730",
  "ServiceUrl": "https://webhook.com/",
  "ChannelId": "{channel-id-guid}",
  "Conversation": {
    "Id": "{conversation-id-guid}"
  },
  "ChannelData": {
    "customEvent": true,
    "customEventName": "CustomTest",
    "customEventValue": "{\"boolVar\":true,\"displayableVar\":{\"isDisplayable\":true,\"value\":\"Hello again!\"},\"numberVar\":-10.5,\"stringVar\":\"Hello world!\"}"
  },
  "Name": "CustomTest"
}
```
