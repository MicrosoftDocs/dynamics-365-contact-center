---
title: CCaaS_GetPresence 
description: Get an agent's presence information at runtime.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: conceptual 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---


# CCaaS_GetPresence 
Get an agent's [presence](/dynamics365/customer-service/use/oc-manage-presence-status?context=/dynamics365/contact-center/context/use-context) information at runtime.

## Prerequisites

You must have the Omnichannel Agent or Omnichannel Supervisor role to call this API.

## Request Details
- **URL**: `https://<orgurl>/api/data/v9.2/CCaaS_GetPresence`
- **Method**: GET
- **Version**: 1.0

## Request Headers

| Name           | Description                                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------------------------|
| Authorization     | Mandatory. Bearer token from Azure AD for the API caller user in CCaaS instance's tenant.                        |
| MSCRMCallerID     | To get the presence for an agent, provide the AgentID of the user you want to impersonate. Calls will be charged against that agent's quota. |


## Response

If successful, this method returns a 200 OK response code and a presence object in the response body. The method returns the following status codes as well.

| HTTP Status | Description                        |
|-------------|---------------------------------------|
| 400         | Bad Request (Wrong input parameters)  |
| 401         | Unauthorized                          |
| 404         | Resource not found                    |
| 429         | Rate limit (Too many requests)        |
| 405         | API not allowed                       |
| 500         | Internal Server Error                 |

## Response Keys

| Key                        | Type          | Description                                                                 |
|----------------------------|---------------|-----------------------------------------------------------------------------|
| ActiveBrowserSessions      | Integer       | The number of browsers or tabs that the agent is logged into.      |
| AgentId                    | GUID          | The ID of the agent in the systemusers entity.                           |
| AgentName                  | String        |  The name of the agent in the systemusers entity.                        |
| Timestamp                  | Integer       |  The login time in seconds from epoch.                                           |
| AllowedChannels            | String array  |  The channels that the agent can use.                              |
| CurrentPresenceStatusInfo  | String        | The name of the current presence status for the agent.                   |
| DisabledChannels           | String array  | The channels that the agent cannot use.                               |
| PresenceId                 | GUID          | The ID of the presence status for the agent. You can use this ID to query more details from the Presence entity by using OData calls. |

## Sample cURL Request

```bash
curl -X GET \
  'https://presencesqlorg.crmtest.Dynamics.com/api/presence/GetAgentPresence/394382b6-a4d4-ee11-904c-00224808a166' \
  --header 'Accept: */*' \
  --header 'OrganizationId: 1e97a1fa-ebd3-ee11-9048-000d3a3501e9' \
  --header 'Content-Type: application/json' \
  --header 'x-ms-organization-id: 1e97a1fa-ebd3-ee11-9048-000d3a3501e9' \
  --header 'tenantId: 8cd46c97-38dd-4560-9228-3df8a717a140' \
  --header 'MSCRMCallerID: cc05cf62-6242-ee11-be6e-6045bdd7ac2c' \
  --header 'Authorization: Bearer Token'
```