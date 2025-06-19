---
title: Configure a custom messaging channel using messaging APIs
description: Learn how to configure a custom messaging channel using messaging APIs.
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Configure a custom messaging channel using messaging APIs

You must register your custom messaging channel in Dynamics 365 before it can communicate with the Omnichannel platform using the Messaging API. This registration links your Azure AD app, tenant, and webhook endpoint to a new channel record that the system can route messages through.

## Prerequisites

- The System Administrator role assigned to an account to set up Messaging API.
- Create a messaging workstream and configure routing rules. Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams).
- An active Azure subscription.

## Set up authentication

To enable secure, authenticated access to the Messaging APIs, you must register a **confidential client application** in **Azure Active Directory (AAD)** for your tenant. This app will be used to acquire OAuth 2.0 tokens that authorize API requests. Perform the following steps:

1. Go to the [Azure portal](https://portal.azure.com/) and navigate to **Azure Active Directory** > **App registrations**.
2. Select **New registration** to register a new application (or use an existing one).
3. Once registered, go to the **Overview** page of your app registration.
4. Copy the **Application (client) ID**.  
   You will use this value in your custom messaging channel record in Dataverse as the value for `msdyn_appid`.

> [!NOTE] 
> Creating a new app from the **Power Platform admin center** is optional. You can use an existing Azure AD app if it meets the authentication requirements.


Here’s a sample of the code that uses the app registration: [A quick start to Dataverse Web API](https://github.com/microsoft/PowerApps-Samples/tree/master/dataverse/webapi/CSharp-NETx/QuickStart).

The scope required for the token is in the format: `https://{organization_id_without_dash}-c.{zone}.dynamics.com /.default.`

 Zone mapping is based on organization region found in [Datacenter regions](/power-platform/admin/new-datacenter-regions)

**Example of token retrieval using Post request**

```
curl --request POST \
  --url https://login.microsoftonline.com/{tenantId} /oauth2/v2.0/token \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=client_credentials \
  --data 'client_secret=***' \
  --data client_id={appId} \
  --data scope=https://{organization_id_without_dash}-c.{zone}.dynamics.com/.default
```

## Setup webhook

To receive real-time updates, you must implement and host a secure webhook endpoint. This endpoint will receive events such as agent messages, typing indicators, and conversation state changes from the Messaging API channel.

the URL path the webhook is as follows: `{webhook_url}/v3/conversations/{conversationId}/activities`. 

Once configured in the custom messaging channel, the application delivers activity payloads to your webhook as POST requests. These payloads follow the Bot Framework Activity Schema.

Learn more about the structure and examples of payloads delivered to your webhook in [Use webhook to receive messages and events](/api/intro-messaging-apis.md).

## Add and manage channels

To enable a custom messaging channel using the Messaging API, you must create a corresponding record in Dataverse. This record defines the key connection settings—such as the Azure app ID and webhook URL—that the system uses to authenticate and communicate with your channel.

Perform the following steps to create, update, or delete a custom messaging channel record:

1. In your environment Copilot Service admin center navigate to **Customer Service** > **Workstreams**.
1. Press **F12** to open your browser's developer tools and then select the **Console** tab.
1. Copy and paste the following code into the browser console to do the following:

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
     Where you must specify the following parameters: <br>
    
      | Field              | Description                                                                 | Example Value                                                  |
      |--------------------|-----------------------------------------------------------------------------|----------------------------------------------------------------|----------|
      | `msdyn_appid`      | The **Application (client) ID** of the Azure AD app used to authenticate Messaging API requests. This is the value you've copied in the [Setup authentication](#set-up-authentication) section. | `9f6c021d-1234-4abc-8df7-123456789abc`                         | 
      | `msdyn_tenantid`   | The **Tenant (Directory) ID** of your organization's Azure Active Directory. | `b5122edb-5678-4def-99e2-abcdef123456`                         | 
      | `msdyn_webhookurl` | The **HTTPS endpoint** that receives messages and events from the application. Must use a valid, non-self-signed certificate. This is the value you configured in [Setup webhook](#setup-webhook) section. | `https://contoso-bot.example.com`                              | <br>

      Replace `{channel_id}` with the ID of the channel you want to delete. You can find this ID in the URL of the channel record in the admin center or by querying the API. <br>

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

1. Perform the steps to add the [custom channel](/dynamics365/customer-service/administer/configure-custom-channel) to the workstream. In the **Channel** field, specify the Messaging API channel you created in the section above.
