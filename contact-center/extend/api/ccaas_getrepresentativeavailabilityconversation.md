---
title: Use CCaaS_GetRepresentativeAvailabilityForConversation
description: Learn how to use the CCaaS_GetRepresentativeAvailabilityForConversation API in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# CCaaS_GetRepresentativeAvailabilityForConversation

Use the **CCaaS_GetRepresentativeAvailabilityForConversation** *API* to get the queue and service representative availability during an active omnichannel conversation with a valid conversation ID.

For example, when a customer chatting with an IVR or chat agent requests escalation to a service representative, the agent can call this API to determine the service representative’s availability and route the conversation appropriately based on the response.

## Request details

### URL
`/\<orgurl\>/api/data/v9.2/CCaaS\_ GetRepresentativeAvailabilityForConversation`

### Method
`POST`

### Version
1.0

## Request headers

| **Name** | **Description** |
|----|----|
| Authorization | Mandatory. Microsoft Entra ID bearer token for the API caller in the Contact Center instance's tenant. Learn more in [Setup token for API authorization](../agent-availability-overview.md)|


## Response

If successful, this method returns a 200 OK response code. The method returns the following status codes:

| **HTTP Status** | **Description**                      |
|-----------------|--------------------------------------|
| 400             | Bad Request (Wrong input parameters) |
| 401             | Unauthorized                         |
| 404             | Resource not found                   |
| 429             | Rate limit (Too many requests)       |
| 405             | API not allowed                      |
| 500             | Internal Server Error                |

## Response values

| **Name** | **Type** | **Description** |
|---|---|---|
| queueId | String | The target queue where the request is routed based on routing rule configuration and input data such as the entity values and context that are part of routing rule. |
| isQueueAvailable | Boolean | Displays:- TRUE if the queue is within operating hours.- FALSE if the queue is outside operating hours. |
| StartTimeOfNextOperatingHour | DateTime | The start time (UTC) of operating hours for the queue if it’s currently outside operating hours. Returns 01-01-0001 during operating hours. |
| EndTimeOfNextOperatingHour | DateTime | The time (UTC) when operating hours end for the queue, if it’s currently outside operating hours. Returns 01-01-0001 during operating hours. |
| nexttransitiontime | DateTime | The time (UTC) when the queue is operational again if it's outside operating hours. During operating hours, displays when the queue becomes non-operational. |
| positionInQueue | Number | Position in queue for a customer waiting behind others in the same queue. |
| isAgentAvailable | Boolean | Displays:- TRUE if service representatives in the queue are currently available to take requests based on the routing and assignment rules for workstream. The API also returns true if an agent is linked to the workstream or queue. We recommend that you don’t use this API when an agent is added to the workstream or queue.- FALSE if service representatives aren't available to take requests. |
| averageWaitTime | Number | Average wait time in minutes for customers in the target queue. |
| AverageWaitTimeInSeconds | Numbers | Average wait time in seconds for customers in the target queue. |



## Sample request body

| **Description** | **Sample request** |
|---|---|
| When a response is required only for the conversation | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityForConversation \ --header 'Authorization: Bearer token' \ --data '{ "ApiVersion": "1.0", "ConversationId": "2f2508bd-b58e-4982-b142-651e36dc8df3" }'` |
| The customer has started a conversation, and the route-to-queue rules need additional context items. So, the request body must pass the omnichannel conversation ID along with the context items that get updated after the conversation is initiated. | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityForConversation \ --header 'Authorization: Bearer token' \ --data '{ "ApiVersion": "1.0", "ConversationId": "cf21df54-6d64-4aea-b668-405b8aa42b07", "CustomContextItems": "{\"contextItem1\": {\"value\": \"contextItemValue1\", \"isDisplayable\": true, \"datatype\": \"DataType1\"}, \"contextItem2\": {\"value\": \"contextItemValue2\", \"isDisplayable\": true, \"datatype\": \"DataType2\"}}" }'` |
| When the rule is on context item Survey (type: Text, value: India) | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityForConversation \ --header 'Authorization: Bearer <Token>' \ --header 'Content-Type: application/json' \ --data '{ "ApiVersion": "1.0", "ConversationId": "94c002c8-b14e-4a0e-8069-78dcf0d6c208", "CustomContextItems": "{\"Survey\": {\"value\": \"India\", \"isDisplayable\": true, \"datatype\": \"192350000\"}}" }'` |

In the request body, `CustomContextItems` is a string with the context items used in route-to-queue rules. The sample list of context items:

```json
{
  "contextItemName1": {
    "value": "contextItemValue1",
    "isDisplayable": true,
    "datatype": "DataType1"
  },
  "contextItemName2": {
    "value": "contextItemValue2",
    "isDisplayable": true,
    "datatype": "DataType2"
  }
}
```

> [!NOTE]
> - `isDisplayable` indicates if the context item is displayed on the screen. This value is either True or False.
> - `datatype` can only be Text = 192350000 or Integer = 192350001.

## Sample Response Body

```json
{
  "@odata.context": "https://<OrgUrl>/api/data/v9.2/$metadata#Microsoft.Dynamics.CRM.CCaaS_GetRepresentativeAvailabilityForConversationResponse",
  "NextTransitionTime": "9999-12-31T23:59:59Z",
  "AverageWaitTimeInSeconds": 54,
  "PositionInQueue": 1,
  "AverageWaitTime": null,
  "StartTimeOfNextOperatingHour": "0001-01-01T00:00:00Z",
  "EndTimeOfNextOperatingHour": "0001-01-01T00:00:00Z",
  "QueueId": "85e55877-f27a-e911-a81a-000d3a1ca610",
  "IsAgentAvailable": true,
  "IsQueueAvailable": true
}
```

