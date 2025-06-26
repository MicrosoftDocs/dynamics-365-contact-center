---
title: Use /conversation/{conversationId}/contexts endpoint
description: Learn how to use the /conversation/{conversationId}/contexts endpoint.
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use /conversation/{conversationId}/contexts endpoint

Retrieves an array of context variables associated with an ongoing conversation. These context variables help enrich the conversation with additional metadata (for example, product details, browser info, locale) and are visible to the customer service representative.

If the conversation has no context variables, the API returns an empty array.

## Method

`GET`

## URL

`/api/v1.0/consumer/conversation/{conversationId}/context`



## Route Parameters

| Parameter        | Description                                             | Type     | Required |
|------------------|---------------------------------------------------------|----------|----------|
| `conversationId` | The unique ID of the conversation to retrieve context for | `GUID` string | Yes |



## Response payload

```json
{
  "context": [
    {
      "name": "contextname1",
      "value": "value 1"
    },
    {
      "name": "contextname2",
      "value": "value 2"
    }
  ]
}

```
## Response parameters

| Tier 1 Key | Tier 2 Key | Tier 3 Key | Description                           | Type                |
| ---------- | ---------- | ---------- | ------------------------------------- | ------------------- |
| `context`  | `[ ]`      | —          | JSON array of context key-value pairs | `array`             |
|            | `name`     | —          | Name of the context variable          | `string`            |
|            | `value`    | —          | Value of the context variable         | `string` / `object` |

