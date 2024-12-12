---
title: CCaaS_ModifyAgentPresence
description: Modify an agent's presence information at runtime.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: conceptual 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---


# CCaaS_ModifyAgentPresence

Modify an agent's [presence](/dynamics365/customer-service/use/oc-manage-presence-status?context=/dynamics365/contact-center/context/use-context) information at runtime.

## Prerequisites

You must have the Omnichannel Agent or Omnichannel Supervisor role to call this API.

## Request details
- **URL**: `//<orgurl>/api/data/v9.2/CCaaS_ModifyAgentPresence`
- **Method**: POST
- **Version**: 1.0

## Request headers

| Name           | Description                                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------------------------|
| Authorization     | Mandatory. Bearer token from Azure AD for the API caller user in CCaaS instance's tenant.                        |
| MSCRMCallerID     | To get the presence for an agent, provide the AgentID of the user you want to impersonate. Calls will be charged against that agent's quota. |


## Response

If successful, this method returns a 200 OK response code. The method returns the following status codes as well.

| HTTP Status | Description                        |
|-------------|---------------------------------------|
| 400         | Bad Request (Wrong input parameters)  |
| 401         | Unauthorized                          |
| 404         | Resource not found                    |
| 429         | Rate limit (Too many requests)        |
| 405         | API not allowed                       |
| 500         | Internal Server Error                 |

## Response keys

None

## Sample cURL Request

```bash
curl --location 
 'https://presencesqlorg.crmtest.Dynamics.com/api/data/v9.2/CCaaS_ModifyAgentPresence' \
 --header 'MSCRMCallerID: cc05cf62-6242-ee11-be6e-6045bdd7ac2c' \
 --header 'Content-Type: application/json' \
 --header 'Authorization: Bearer Token' \
 --header 'Cookie: ReqClientId=00001111-aaaa-2222-bbbb-3333cccc4444; orgId=33dd33dd-ee44-ff55-aa66-77bb77bb77bb' \
 --data '{
   "ApiVersion": "1.0",
   "AgentId": "33dd33dd-ee44-ff55-aa66-77bb77bb77bb",
   "PresenceId": "55ff55ff-aa66-bb77-cc88-99dd99dd99dd"
}'
```