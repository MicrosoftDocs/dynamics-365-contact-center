---
title: Use CCaaS_GetRepresentativeAvailabilityForConversation
description: Learn how to use the CCaaS_GetRepresentativeAvailabilityForConversation API in Dynamics 365 Contact Center.
ms.date: 04/30/2026
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# CCaaS_GetRepresentativeAvailabilityForConversation

Use the **CCaaS_GetRepresentativeAvailabilityForConversation** API to get the queue and service representative availability during an active conversation with a valid conversation ID.

For example, when a customer who's chatting with an IVR or AI agent requests escalation to a service representative, the AI agent calls this API to determine service representative’s availability and route the conversation based on the response.

## Request details

### URL
`/\<orgurl\>/api/data/v9.2/CCaaS\_ GetRepresentativeAvailabilityForConversation`

### Method
`POST`

### Version
1.0

### Request headers

| **Name** | **Description** |
|----|----|
| Authorization | Mandatory. Microsoft Entra ID bearer token for the API caller in the Contact Center instance. Learn more in [Setup token for API authorization](../representative-availability-overview.md)|

### Sample request body

| **Description** | **Sample request** |
|---|---|
| Determines queue and representative availability for an active conversation. | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityForConversation \ --header 'Authorization: Bearer token' \ --data '{ "ApiVersion": "1.0", "ConversationId": "2f2508bd-b58e-4982-b142-651e36dc8df3" }'` |
| Determine queue and representative availability for a conversation where the route-to-queue rules need more context items. | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityForConversation \ --header 'Authorization: Bearer token' \ --data '{ "ApiVersion": "1.0", "ConversationId": "cf21df54-6d64-4aea-b668-405b8aa42b07", "CustomContextItems": "{\"contextItem1\": {\"value\": \"contextItemValue1\", \"isDisplayable\": true, \"datatype\": \"DataType1\"}, \"contextItem2\": {\"value\": \"contextItemValue2\", \"isDisplayable\": true, \"datatype\": \"DataType2\"}}" }'` |
| The rule is on context item Survey (type: Text, value: India) | `curl --request POST \ --url https://<org-url>/api/data/v9.2/CCaaS_GetRepresentativeAvailabilityForConversation \ --header 'Authorization: Bearer <Token>' \ --header 'Content-Type: application/json' \ --data '{ "ApiVersion": "1.0", "ConversationId": "94c002c8-b14e-4a0e-8069-78dcf0d6c208", "CustomContextItems": "{\"Survey\": {\"value\": \"India\", \"isDisplayable\": true, \"datatype\": \"192350000\"}}" }'` |


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

[!INCLUDE [cc-availability-response](../../includes/cc-availability-response.md)]

## Related information

[Use representative availability APIs](../representative-availability-overview.md)   
[CCaaS_GetRepresentativeAvailabilityBeforeConversation](ccaas-get-representative-availability-before-conversation.md)  