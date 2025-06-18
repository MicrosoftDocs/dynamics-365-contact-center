---
title: Use /consumer/conversations/create endpoin
description: Learn how to use the /consumer/conversations/create endpoint.
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use /consumer/conversations/create endpoint

The `create` endpoint is used to start a new customer conversation using the Messaging API. Conversations are considered to be active throughout the lifetime of the conversation until a customer service representative (service representative or representative) ends the conversation, or the conversation is in waiting state, or a timeout rule ends the conversation.

 If you must end a conversation early, for example, if the customer ends the conversation, you must close the conversation using the `POST /api/v1.0/consumer/conversation/{conversationId}` with the conversation ending activity. 


## Method

`POST`

## URL

`/api/v1.0/consumer/conversations/create`

## Payload

The API expects the following in the body of the HTTP POST request. The payload contains information about the customer and the conversation context.

```json

{
 "customercontext": {
    " customerid": "jdoe123",
    "firstname": "John",
    "lastname": "Doe",
    "preferredname": "John Doe", // This will be displayed to the customer service representative
    "email": "john.doe@email.com",
    "phonenumber": "1234567890"
  },
  "conversationcontext": {
    "productname": { "isDisplayable": true, "value": “XBox" },
    "issue": { "isDisplayable": true, "value": "installation" }
   }
}

```

## Request schema

### customercontext

Provides customer identity and other relevant information that can be used for record identification and to display the information to the customer service representative.

| Field           | Description                              | Type             | Max Length | Required |
| --------------- | ---------------------------------------- | ---------------- | ---------- | -------- |
| `customerid`    | Unique ID assigned the customer conversation. If an active conversation already exists with the same ID, the existing conversation ID is returned instead of creating new conversation.      | `string`         | 200 chars  | Optional        |
| `firstname`     | Customer first name                      | `string`         | 200 chars  | Optional       |
| `lastname`      | Customer last name                       | `string`         | 200 chars  | Optional        |
| `preferredname` | Display name for the agent UI            | `string`         | 200 chars  | Optional       |
| `email`         | Email address (used for record matching) | `string` (email) | 200 chars  | Optional        |
| `phonenumber`   | Phone number (used for record matching)  | `string`         | 200 chars  | Optional        |

### conversationontext

 The conversationcontext object allows you to pass up to 100 context variables. The variables are objects that contain a key name and object value. You can set the `displayable flag` to indicate if the value appears to the service representative. Learn more in [setcontextprovider](/dynamics365/customer-service/develop/reference/methods/setcontextprovider). 

## Record identification

 Record identification in customer service is based on the email and phone number provided in the request body. If an existing record is identified, but other fields such as first name and last name don't match the values in the body, the application uses the values in the existing identified record and ignores the values in the request body.
