---
title: Use /conversations endpoint
description: Learn how to use the /conversations endpoint.
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use /conversations endpoint


Retrieves a list of all the active conversations created through the custom channel created using the Messaging APIs. Conversations created for other messaging channels aren't retrieved.

Conversations that are in **Wrap-Up** or **Closed** states aren't included in the response. If no active conversations exist, the response returns an empty array.

> [!NOTE]
> The conversations endpoint mustn't be used as a polling mechanism. Conversation events are posted to Microsoft and updates posted back to your subscribed webhook. 


## Method

`GET`


## URL

`/api/v1.0/consumer/conversations`

## Query parameters 

Query parameters allow you to filter, limit, and paginate the list of active conversations returned by the API for more efficient data retrieval.

| Parameter         | Description                                                                 | Type                      |
|-------------------|-----------------------------------------------------------------------------|---------------------------|
| `StartTimeStamp`  | Filters conversations created **after** this timestamp (ISO 8601 format).   | `string` (DatetimeOffset) |
| `PageSize`        | Maximum number of conversations to return. Default: `50`, Max: `250`.       | `integer`                 |
| `ContinuationToken`| Used for pagination to avoid duplicates in large result sets.             | `GUID` string             |



## Response payload

```json
{
    "conversations": [
        {
            "conversationid": "debd3f0d-90d4-47fc-b30c-d5ffbe31c851",
            "timestamp": "2025-04-15T12:36:40.9049594Z"
        },
        {
            "conversationid": "b816977f-7c80-46a1-9062-404665987430",
            "timestamp": "2025-04-16T14:25:19.9245078Z"
        },
        {
            "conversationid": "94edeca2-5563-46fb-9ab5-b9b4ce85e0b2",
            "timestamp": "2025-04-16T14:25:29.0700838Z"
        }
    ],
    "continuationtoken": "string"
}


```

### Response fields

| Tier 1 Key          | Tier 2 Key       | Description                                                   | Type       |
| ------------------- | ---------------- | ------------------------------------------------------------- | ---------- |
| `conversations`     | `[ ]`            | JSON array of active conversation records                     | `array`    |
|                     | `conversationid` | Unique ID of the conversation                                 | `GUID`     |
|                     | `timestamp`      | Creation timestamp in ISO 8601 format                         | `Datetime` |
| `continuationtoken` |                  | Token used for fetching the next page of results, if necessary | `GUID`     |
