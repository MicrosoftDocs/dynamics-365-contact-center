---
title: Configure a custom messaging channel using messaging APIs
description: Learn how to configure a custom messaging channel in Dynamics 365 using Messaging APIs, including authentication, webhook setup, and managed identity configuration.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---


# Configure a custom messaging channel using messaging APIs

Register your custom messaging channel in Dynamics 365 so it communicates with the omnichannel platform using the Messaging API. This registration links your Microsoft Entra app, tenant, and webhook endpoint to a new channel record that the system routes messages through.

## Prerequisites

- The System Administrator role assigned to an account to set up Messaging API.
- Create a messaging workstream and set up routing rules. Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams).
- An active Azure subscription

## Set up authentication

To enable secure, authenticated access to the Messaging APIs, register a **confidential client application** in **Azure Active Directory (AAD)** for your tenant. This app is used to acquire OAuth 2.0 tokens that authorize API requests. Perform the following steps:

1. Go to the [Azure portal](https://portal.azure.com/) and navigate to **Azure Active Directory** > **App registrations**.
2. Use an existing app or select **New registration** to register a new application.
3. Once registered, go to the **Overview** page of your app registration.
4. Copy the **Application (client) ID**.  
   You use this value in your custom messaging channel record in Dataverse as the value for `msdyn_appid`.

Learn more in [confidential client app registration](/power-apps/developer/data-platform/walkthrough-register-app-azure-active-directory#confidential-client-app-registration).

> [!NOTE] 
> Creating a new Microsoft Entra app registration is optional. Use an existing Microsoft Entra app registration if it meets the authentication requirements.


Here’s a sample of code that uses the app registration: [A quick start to Dataverse Web API](https://github.com/microsoft/PowerApps-Samples/tree/master/dataverse/webapi/CSharp-NETx/QuickStart).

The scope required for the token is in the format: `https://{organization_id_without_dash}-c.{zone}.dynamics.com/.default`.

Zone mapping is based on the organization region found in [Datacenter regions](/power-platform/admin/new-datacenter-regions).

**Example of token retrieval using POST request**

```
curl --request POST \
  --url https://login.microsoftonline.com/{tenantId} /oauth2/v2.0/token \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=client_credentials \
  --data 'client_secret=***' \
  --data client_id={appId} \
  --data scope=https://{organization_id_without_dash}-c.{zone}.dynamics.com/.default
```

## Set up webhook

To receive real-time updates, you must implement and host a secure webhook endpoint. This endpoint receives events such as agent messages, typing indicators, and conversation state changes from the Messaging API channel.

The URL path for the webhook is: `{webhook_url}/v3/conversations/{conversationId}/activities`. 

After you configure the webhook in the custom messaging channel, the application delivers activity payloads to your webhook as POST requests. These payloads follow the Bot Framework Activity Schema.

Learn more about the structure and examples of payloads delivered to your webhook in [use webhook to receive messages and events](./api/api-conversation-webhook.md).

## Set up managed identity for webhook authentication

To enable webhook authentication using [Power Platforms managed identity](/power-platform/admin/managed-identity-overview), you must create a managed identity record in Dataverse. This record defines the credential settings that generate authentication tokens for webhook requests.

The process involves these steps:

1. Create the managed identity record to establish the authentication configuration in Dataverse.
2. Link the identity to your messaging channel. Update the custom messaging channel (created in the add and manage channel process) with the new managed identity record ID.
3. Configure Microsoft Entra App credentials. Use the [GetComponentManagedIdentityFIC](/power-apps/developer/data-platform/webapi/reference/getcomponentmanagedidentityfic) service to obtain the FICSubject, then update your Microsoft Entra App registration with the [federated identity credentials](/graph/api/resources/federatedidentitycredentials-overview).

### Create managed identity record

```javascript
// Define the data to create a record
var data = {
    "applicationid": "REPLACE_WITH_app_id",
    "credentialsource": 2,
    "subjectscope": 1,
    "tenantid": "REPLACE_WITH_tenant_id"
};

// create the record
Xrm.WebApi.createRecord("managedidentity", data).then(
    function success(result) {
        console.log("managedidentity created with ID:" + result.id);
        // perform operations on record update
    },
    function (error) {
        console.log(error.message);
        // handle error conditions
    }
);
```

**Parameters**


| Field | Description | Example  |
|-------|-------------|---------------|
| applicationid | The **Application (client) ID** of the Microsoft Entra app used to authenticate messaging API requests. This is the value you copied in the [Setup authentication](#set-up-authentication) section. | `9f6c021d-1234-4abc-8df7-123456789abc` |
| credentialsource | The value should always be set to two.| 2 |
| subjectscope | The value should always be set to one. | 1 |
| tenantid | The **Tenant (Directory) ID** of your organization's Microsoft Entra ID | `b5122edb-5678-4def-99e2-abcdef123456` |

### Update custom messaging channel

```javascript
// define the data to update a msdyn_occustommessagingchannel record
var data = {
    "managedidentityid@odata.bind": "/managedidentities(REPLACE_WITH_managed_identity_id)"
};

// update the record
Xrm.WebApi.updateRecord("msdyn_occustommessagingchannel", "REPLACE_WITH_custom_channel_id", data).then(
    function success(result) {
        console.log("msdyn_occustommessagingchannel updated");
    },
    function (error) {
        console.log(error.message);
    }
);
```

### Obtain FICSubject

Run the following URL in a new browser tab where you're signed in to the Copilot Service admin center:

```
https://{org_url}/api/data/v9.2/GetComponentManagedIdentityFIC(ComponentName='msdyn_occustommessagingchannel',ComponentId={custom_channel_id})
```

- Copy the FICSubject value. You add it as the new credential to the Microsoft Entra App registration.
- Go to Azure portal > **Entra ID** > **Manage** > **App Registrations**, and select the Microsoft Entra app registration you created earlier. 
- Under **Manage**, select **Certificates & secrets** > **Federated credentials** > **Add credential** and specify the following details: 

**Federated credential scenario**: Other issuer
**Issuer**: `https://login.microsoftonline.com/{tenant_id}/v2.0`  
**Type**: Explicit subject identifier  
**Value**: `{FICSubject}` copied from GetComponentManagedIdentityFIC

## Manage channels

To enable a custom messaging channel using the Messaging API, you must create a corresponding record in Dataverse. This record defines the key connection settings—such as the Azure app ID and webhook URL—that the system uses to authenticate and communicate with your channel.

Perform the following steps to create, update, or delete a custom messaging channel record:

1. In Copilot Service admin center, go to **Customer Service** > **Workstreams**.
1. Press **F12** to open your browser's developer tools, and then select the **Console** tab.
1. Copy and paste the following code into the browser console to do the following actions:

  - **Create a new custom messaging channel**
     ```js
      // Define the data to create a record
       var data = {
        "msdyn_occustomchannelid": 192350005, // MessagingAPI
        "msdyn_name": "{display_name}",
        "msdyn_appid": "{azure_app_id_guid}",
        "msdyn_tenantid": "{azure_tenant_id_guid}",
         "msdyn_webhookurl": "{base_webhook_url}" // e.g., https://company.webhook
       };

     // Create the record
       Xrm.WebApi.createRecord("msdyn_occustommessagingchannel", data).then(
        function success(result) {
        console.log("msdyn_occustommessagingchannel created with ID: " + result.id);
        console.log(result);
       },
       function (error) {
        console.log(error.message);
       }
      );
    ```
     You can specify the following parameters in the request body:

      | **Field**              | **Description**   | **Example Value**                                                  |
      |--------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------|----------|
      | `msdyn_appid`      | The **Application (client) ID** of the Microsoft Entra ID app used to authenticate Messaging API requests. This is the value you copied in the [Setup authentication](#set-up-authentication) section. | `9f6c021d-1234-4abc-8df7-123456789abc` | 
      | `msdyn_tenantid`   | The **Tenant (Directory) ID** of your organization's Microsoft Entra ID. | `b5122edb-5678-4def-99e2-abcdef123456`  | 
      | `msdyn_webhookurl` | The **HTTPS endpoint** that receives messages and events from the application. Must use a valid, non-self-signed certificate. This is the value you configured in [Setup webhook](#setup-webhook) section. | `https://contoso-bot.example.com`                              | <br>

      Replace `{channel_id}` with the ID of the channel to delete. Find this ID in the URL of the channel record in the admin center or by querying the API. <br>

  - **Update an existing record.**
  
      ```js
      // Define the data to update
      var data = {
      "msdyn_tenantid": "{azure_tenant_id_guid}",
      "msdyn_webhookurl": "{base_webhook_url}"
       };

       // Update the record
      Xrm.WebApi.updateRecord("msdyn_occustommessagingchannel", "{msdyn_occustommessagingchannelid}", data).then(
      function success(result) {
        console.log("msdyn_occustommessagingchannel updated");
      },
       function (error) {
        console.log(error.message);
      }
     );

       ```
  - **Delete an existing record**
  
      ```js

        // Delete the record
         Xrm.WebApi.deleteRecord("msdyn_occustommessagingchannel", "{channel_id}").then(
         function success(result) {
        console.log("msdyn_occustommessagingchannel deleted");
        },
        function (error) {
         console.log(error.message);
        }
        );

      ```
 - **View all the custom messaging channel records that are created in the organization** 

     `{org_url}/api/data/v9.2/msdyn_occustommessagingchannels`

4. Follow the steps to add the [custom channel](/dynamics365/customer-service/administer/configure-custom-channel) to the workstream. In the **Channel** field, specify the Messaging API channel created in the **Create a new custom messaging channel** section.

