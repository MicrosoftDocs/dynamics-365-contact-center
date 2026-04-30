---
title: Use CCaaS_GetRepresentativeAvailabilityBeforeConversation
description: Learn how to use the CCaaS_GetRepresentativeAvailabilityBeforeConversation API in Dynamics 365 Contact Center.
ms.date: 04/30/2026
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---


# Use CCaaS_GetRepresentativeAvailabilityBeforeConversation

Use the **CCaaS_GetRepresentativeAvailabilityBeforeConversation** to get the queue and service representative availability before an conversation with the customer starts.

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

[!INCLUDE [cc-availability-response](../../includes/cc-availability-response.md)]

## Related information
 
[Use representative availability APIs](../representative-availability-overview.md)    
[CCaaS_GetRepresentativeAvailabilityForConversation](ccaas-get-representative-availability-conversation.md)  

