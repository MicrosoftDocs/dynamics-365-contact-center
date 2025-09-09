---
title: Use /consumer/conversations/create endpoint
description: Learn how to use the /consumer/conversations/create endpoint in Dynamics 365 Customer Service and Contact Center to start customer conversations with the Messaging API. Includes schema, payload, and response details.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---


# Use /consumer/conversations/create endpoint

The `create` endpoint starts a new customer conversation using the Messaging API. Conversations remain active until a customer service representative ends the conversation, the conversation enters a waiting state, or a timeout rule ends the conversation.

 To end a conversation early, such as when the customer ends it, close the conversation using the `POST /api/v1.0/consumer/conversation/{conversationId}` with the conversation-ending activity. 


## Method

`POST`

## Url

`/api/v1.0/consumer/conversations/create`

## Payload

The API expects the following in the body of the HTTP POST request: information about the customer and the conversation context.

```json

{
 "customercontext": {
    "customerid": "jdoe123",
    "firstname": "John",
    "lastname": "Doe",
    "preferredname": "John Doe", // This will be displayed to the customer service representative
    "email": "john.doe@email.com",
    "phonenumber": "1234567890"
  },
  "conversationcontext": {
    "productname": { "isDisplayable": true, "value": "XBox" },
    "issue": { "isDisplayable": true, "value": "installation" }
  },
  "conversationrequestid": "some unique id",
  "startmessage": {
    "message": "Some initial message",
    "displayname": "Sender name"
  },
  "skipdeflectionbot": true
}

```

### Request schema

The following sections describe the request schema in detail.

**customercontext**

Provides customer identity and relevant information for record identification and displaying information to the customer service representative.

| Field           | Description                              | Type             | Max Length | Required |
| --------------- | ---------------------------------------- | ---------------- | ---------- | -------- |
| customerid    | Unique ID assigned the customer conversation. If an active conversation already exists with the same ID, the existing conversation ID is returned instead of creating new conversation.      | string         | 200 chars  | Optional        |
| firstname     | Customer first name                      | string         | 200 chars  | Optional       |
| lastname      | Customer last name                       | string         | 200 chars  | Optional        |
| preferredname | Display name for the agent or customer service representative (service representative or representative)           | string         | 200 chars  | Optional        |
| email         | Email address (used for record matching) | string (email) | 200 chars  | Optional        |
| phonenumber   | Phone number (used for record matching)  | string         | 200 chars  | Optional        |
| startmessage   | This message is processed when a new conversation is initialized. The message is sent only to the service representative and isn't shared with the AI agent.  | string         | 27 Kb  | Optional        |
| skipdeflectionbot   | When set to True, the AI agent isn't engaged.  | boolean         |   | Optional       |



**conversationcontext**

 The `conversationcontext` object lets you pass up to 100 context variables. These variables contain a key name and object value. Set the `displayable flag` to indicate if the value appears to the service representative. Learn more in [setcontextprovider](/dynamics365/customer-service/develop/reference/methods/setcontextprovider). 


**Record identification**

 Customer service identifies records based on the email and phone number in the request body. If an existing record is found but fields like first name and last name don't match, the application uses the values from the existing record and ignores the information in the request body.

## Response

The API returns the following JSON response. 

```json
{
  "conversationId": "some unique GUID",
  "isNew": true or false,
  "messageId": "1234567890123"
}
```

**Field descriptions**

| Field | Description | Type |
|-------|-------------|------|
| conversationId | The conversationId is a GUID that should be used for subsequent API calls. | string |
| isNew | Indicates whether the conversation is new or continued. | Boolean |
| messageId | The messageId is a 13-digit string epoch timestamp used for message ordering to match the order displayed (only when the start message is used). | string |