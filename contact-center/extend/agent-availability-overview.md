---
title: Use availabilty APIs
description: Learn how to use the availabilty APIs in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---
# Use availabilty APIs

Use the availability APIs to retrieve information about queue availability and customer service representative availability in Dynamics 365 Contact Center.
You can use these APIs in scenarios such as:

- Escalating ongoing conversations only to queues where service representatives are available.
- Initiating conversations only when relevant queues are within operating hours or have available representatives

The Availability APIs are channel‑agnostic and work consistently across all Dynamics 365 Contact Center channels, including voice, live chat, and digital messaging.

## Prerequisites

- A license for Dynamics 365 Contact Center.

## Setup token for API authorization

Do the following steps to setup a token to authorize API calls from you application to the APIs:

1. In the Azure portal, [register your application](/entra/identity-platform/quickstart-register-app#register-an-application) or go to **Entra ID** > **App registrations**, and then select your client application. Copy the tenant-id and the appid of the application.
1. Select **API permissions**, then **Add a permission**. 
1. In **Request API permissions**, select **Microsoft APIs** tab and then select **Dynamics CRM**.
1. Select **Delegated permissions**. 
1. Under **Select permissions**, select `user.impersonation`.
1. Select **Add permissions**.
1. [Add a client secret for your application](/entra/identity-platform/how-to-add-credentials?tabs=client-secret#add-a-credential-to-your-application). Copy the client secret value. The value isn't displayed again once you leave the page.
1. In Power Platform admin center, [create an application user](/power-platform/admin/manage-application-users?WT.mc_id=ppac_inproduct_settings#create-an-application-user) for your application and assign the Omnichannel administrator role.
1. Run the following POST request generate a token. where tenant-ID is the Azure tenant-ID, client_id values are the values from the app registration and client secret is the appid that you copy from app registration. orgurl is the dynamics org.

  ```bash
   
     curl --request POST \
     --url https://login.windows.net/{tenant-Id}/oauth2/token \
     --header 'Content-Type: multipart/form-data' \

     --header 'User-Agent: insomnia/10.1.0' \
     --cookie 'fpc=ApQqO0OrCftGhsPOawVKHv6SxOiUAgAAHN3YN8OAAAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd' \
     --form grant_type=client_credentials \
     --form client_id={ApplicationIdFromAppRegistration} \
     --form 'client_secret={secretSavedInPreviousStep}' \
     --form resource={OrgUrl}

  ```
Microsoft Entra ID generates a token that you can use in the APIs.

## Availability APIs

The following APIs are available:

- CCaaS_GetRepresentativeAvailabilityForConversation: Returns the queue and service representative availability during an active omnichannel conversation with a valid conversation ID. Learn more in [CCaaS_GetRepresentativeAvailabilityForConversation](./api/ccaas_getrepresentativeavailabilityconversation.md)
- CCaaS_GetRepresentativeAvailabilityBeforeConversation: get the queue and service representative availability when the conversation with the customer hasn’t started. Learn more in [CCaaS_GetRepresentativeAvailabilityBeforeConversation](./api/ccaas_getrepresentativeavailabilitybeforeconversation.md)


## Make ca availability APIs Copilot Studio

This procedure describes how to configure a Copilot Studio agent to call the **CCaaS Representative Availability APIs**. These APIs allow the Copilot agent to retrieve availability information from Dynamics 365 Contact Center.

Before configuring the APIs, ensure that the Copilot Studio agent has been assigned the **Omnichannel Administrator** role. This role is required to successfully invoke the CCaaS Representative Availability APIs.

Do the following the steps in Copilot Studio for the required agent:


1. Go to **Topics** and then select **Escalate** action.
1. Add a new node to the topic.
1. Select **Add a tool** and then select **Perform an unbound action in selected environment**. If no connections are available, do the following:
   - Create a new connection.
   - Select the authentication type as **OAuth**.
   - Select **Create**.
1. Set the **Environment** to **Current**.
2. Select one of the following action names, as required:
   - `CCaaS_GetRepresentativeAvailabilityForConversation`
   - `CCaaS_GetRepresentativeAvailabilityBeforeConversation`
1. After selecting the action, update the **Advanced Parameters** as required.
2. Add the rules for the agent based on the API response.
1. Save and publish.






