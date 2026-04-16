---
title: Use CCaaS_GetRepresentativeAvailabilityBeforeConversation
description: Learn how to use the CCaaS_GetRepresentativeAvailabilityBeforeConversation API in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---


# Use CCaaS_GetRepresentativeAvailabilityBeforeConversation

Use the **CCaaS_GetRepresentativeAvailabilityBeforeConversation** to get the queue and service representative availability when an omnichannel conversation with the customer hasn’t started

For example, you can display a chat widget on your website only when relevant queues are within operating hours by calling this API to verify service representative availability.

You can also use this API when external systems need to proactively query service representative availability, helping supervisors make staffing optimization decisions for their queues.

## Request details

### URL
`/\<orgurl\>/api/data/v9.2/CCaaS\_ GetRepresentativeAvailabilityBeforeConversation`

### Method
`POST`

### Version
1.0

### Request headers

| **Name** | **Description** |
|----|----|
| Authorization | Mandatory. Microsoft Entra ID bearer token for the API caller in the Contact Center instance's tenant. Learn more in [Setup token for API authorization](../representative-availability-overview.md)|

### Sample request 


| **Scenario** | **Sample code** |
|---|---|
| Check service representative availability for a workstream with a single default queue. | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityBeforeConversation \ --header 'Authorization: Bearer token' \ --header 'Content-Type: application/json' \ --data '{ "ApiVersion": "1.0", "LiveWorkStreamId": "8a581641-291b-2002-5b86-55e0cfa0fc63" }'` |
| Determine relevant queue availability for a workstream where context variables are used in route-to-queue rules. | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityBeforeConversation \ --header 'Authorization: Bearer token' \ --header 'Content-Type: application/json' \ --data '{ "ApiVersion": "1.0", "LiveWorkStreamId": "cf21df54-6d64-4aea-b668-405b8aa42b07", "CustomContextItems": "{\"contextItem1\": {\"value\": \"contextItemValue1\", \"isDisplayable\": true, \"datatype\": \"DataType1\"}, \"contextItem2\": {\"value\": \"contextItemValue2\", \"isDisplayable\": true, \"datatype\": \"DataType2\"}}" }'` |
| Add or override context items. For example, survey. | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityBeforeConversation \ --header 'Authorization: Bearer <Token>' \ --header 'Content-Type: application/json' \ --data '{ "ApiVersion": "1.0", "LiveWorkStreamId": "8a581641-291b-2002-5b86-55e0cfa0fc63", "CustomContextItems": "{\"Survey\": {\"value\": \"India\", \"isDisplayable\": true, \"datatype\": \"192350000\"}}" }'` |
| Determine service representative availability when a conversation has rules over engagement context entity. | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityBeforeConversation \ --header 'Authorization: Bearer token' \ --header 'Content-Type: application/json' \ --data '{ "ApiVersion": "1.0", "LiveWorkStreamId": "8a581641-291b-2002-5b86-55e0cfa0fc63", "ChannelEngagementContext": "{"msdyn_browser": "Edge",\n "msdyn_city": "florida"\n}"" '` |
| Determine service representative availability when rules are present over both context items and engagement context | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityBeforeConversation \ --header 'Authorization: Bearer token' \ --header 'Content-Type: application/json' \ --data '{ "ApiVersion": "1.0", "LiveWorkStreamId": "8a581641-291b-2002-5b86-55e0cfa0fc63", "ChannelEngagementContext": "{"msdyn_browser": "Edge", \n "msdyn_city": "florida"\n}", "CustomContextItems": "{\"contextItem1\": {\n    \"value\": \"contextItemValue1\",\n    \"isDisplayable\": true,\n    \"datatype\": \"DataType1\"\n  },\"contextItem12\": {\n    \"value\": \"contextItemValue2\",\n    \"isDisplayable\": true,\n    \"datatype\": \"DataType2\"\n  }}" }'` |

> [!NOTE]
> - In the request body, `CustomContextItems` is a string with the context items used in route-to-queue rules. The sample list of context items:
>
>   ```json
>   {
>     "contextItemName1": {
>       "value": "contextItemValue1",
>       "isDisplayable": true,
>       "datatype": "DataType1"
>     },
>     "contextItemName2": {
>       "value": "contextItemValue2",
>       "isDisplayable": true,
>       "datatype": "DataType2"
>     }
>   }
>   ```
>
> - `isDisplayable` indicates if the context item is displayed on the screen. This value is either True or False.
> - `datatype` can only be Text = 192350000 or Integer = 192350001

## Response

If successful, this method returns a 200 OK response code. The method also returns the following status codes.

| **HTTP Status** | **Description**                      |
|-----------------|--------------------------------------|
| 400             | Bad Request (Wrong input parameters) |
| 401             | Unauthorized                         |
| 404             | Resource not found                   |
| 429             | Rate limit (Too many requests)       |
| 405             | API not allowed                      |
| 500             | Internal Server Error                |

### Response values

| **Name** | **Type** | **Description** |
|---|---|---|
| queueId | String | The target queue where the request is routed based on routing rule configurations and input data such as entity values and context that are part of the routing rule. |
| isQueueAvailable | Boolean | Displays TRUE if the queue is within operating hours. FALSE if the queue is outside operating hours. |
| StartTimeOfNextOperatingHour | DateTime | The start time (UTC) of operating hours for the queue if it’s currently outside operating hours. Returns 01-01-0001 during operating hours. |
| EndTimeOfNextOperatingHour | DateTime | The time (UTC) when operating hours end for the queue, if it’s currently outside operating hours. Returns 01-01-0001 during operating hours. |
| nexttransitiontime | DateTime | The time (UTC) when the queue is operational again if it's outside operating hours. During operating hours, displays when the queue becomes non-operational. |
| positionInQueue | Number | Position in queue for a customer waiting behind others in the same queue. |
| isAgentAvailable | Boolean | Displays TRUE if service representatives in the queue are currently available to take requests based on the routing and assignment rules for workstream. The API also returns true if an AI agent is linked to the workstream or queue. We recommend that you don't use this API when an AI agent is added to the workstream or queue. FALSE if service representatives aren't available to take requests. |
| averageWaitTime | Number | Average wait time in minutes for customers in the target queue. |
| AverageWaitTimeInSeconds | Numbers | Average wait time in seconds for customers in the target queue. |
|NumberOfExpertsAvailableInQueue|Numbers|The number of service representatives currently available to accept conversations in the target queue. |

### Sample response 

```JSON
{  
"@odata.context": "https://aurorabapenv292a1.crm10.dynamics.com/api/data/v9.2/\$metadata#Microsoft.Dynamics.CRM.CCaaS_GetRepresentativeAvailabilityForConversationResponse",  
"NextTransitionTime": "9999-12-31T23:59:59Z",
"NumberOfExpertsAvailableInQueue": 5,
“AverageWaitTimeInSeconds”: 45  
"PositionInQueue": 1,  
"AverageWaitTime": null,  
"StartTimeOfNextOperatingHour": "0001-01-01T00:00:00Z",  
"EndTimeOfNextOperatingHour": "0001-01-01T00:00:00Z",  
"QueueId": "85e55877-f27a-e911-a81a-000d3a1ca610",  
"IsAgentAvailable": true,  
"IsQueueAvailable": true  
}
```