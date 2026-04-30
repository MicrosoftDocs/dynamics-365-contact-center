---
title: Use service representative availability APIs
description: Learn how to use the representative availability APIs in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
ms.date: 04/30/2026
ms.topic: conceptual
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---
# Use representative availability APIs

Use the representative availability APIs to retrieve information about queue and customer service representative availability in Dynamics 365 Contact Center.

You can use these APIs in scenarios such as:

- When AI agents have to escalate ongoing conversations only to queues where service representatives are available.
- You want customers to initiate conversations only when relevant queues are within operating hours or have available representatives.

The representative availability APIs are applicable for all channels, including voice, live chat, and digital messaging.

## Prerequisites

- You have the Omnichannel administrator role assigned.

### Set up token for API authorization

To use the representative availability APIs, you must generate an access token. This token acts as a secure credential to authenticate your application's identity and authorize it to access specific service resources.

Do the following steps in the [Azure portal](https://portal.azure.com):
1. [Register your application](/entra/identity-platform/quickstart-register-app#register-an-application) or go to **Entra ID** > **App registrations**, and then select your client application. Copy the following values:

   - **Application (client) ID**
   - **Directory (tenant) ID** 
1. In your app registration, select **API permissions** > **Add a permission**.
2. In **Request API permissions**, select **Microsoft APIs** tab and then select **Dynamics CRM**.
3. Select **Delegated permissions**, and then select the `user_impersonation` scope.
1. Select **Add permissions**.
1. [Add a client secret for your application](/entra/identity-platform/how-to-add-credentials?tabs=client-secret#add-a-credential-to-your-application). 
 > [!IMPORTANT]
 > Copy the secret **Value** immediately. This value is encrypted and isn't displayed again once you leave the page.

To generate the token, run the following `POST` request. Replace the following values:

| Value | Description |
| :--- | :--- |
| `tenant-Id` | The **Directory (tenant) ID** of the app.|
| `client_id` | The Application (client) ID assigned to your app in Microsoft Entra ID. |
| `client_secret` | The secret string generated during app registration. |
| `resource` | The URL of your Dynamics 365 environment, defining the requested permissions. |

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

The response returns a JSON object with the token that you can use in the Authorization Header of your representative availability API calls as a Bearer token.

## Representative availability APIs

The following representative availability APIs are available:

- **CCaaS_GetRepresentativeAvailabilityForConversation**: Returns the queue and service representative availability during an active omnichannel conversation with a valid conversation ID. Learn more in [CCaaS_GetRepresentativeAvailabilityForConversation](./api/ccaas-getrepresentativeavailabilityconversation.md)
- **CCaaS_GetRepresentativeAvailabilityBeforeConversation**: Returns the queue and service representative availability before an omnichannel conversation with the customer starts. Learn more in [CCaaS_GetRepresentativeAvailabilityBeforeConversation](./api/ccaas-getrepresentativeavailabilitybeforeconversation.md)

## Related information
 
[CCaaS_GetRepresentativeAvailabilityForConversation](./api/ccaas-get-representative-availability-conversation.md)  
[CCaaS_GetRepresentativeAvailabilityBeforeConversation](./api/ccaas-get-representative-availability-before-conversation.md)  