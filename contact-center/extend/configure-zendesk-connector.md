---
title: Configure the connector for Zendesk
description: Learn how to use the connector for Zendesk CRM solution to fetch data into Dataverse and use in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection:
ms.date: 07/01/2024
ms.custom: bap-template
---

# Configure the connector for Zendesk

The Zendesk connector allows organizations to engage with their customers using omnichannel capabilities like voice, video, SMS, live chat, and social messaging while keeping their current investments in third-party CRM solutions. The omnichannel add-in works with third-party CRM solutions through data connectors. These connectors help bring the contacts and accounts data from the Zendesk CRM solution into Dataverse.

## Prerequisites 

- [Zendesk](https://[your_subdomain].zendesk.com) instance
- License for Dynamic 365 Contact Center
- Power Platform System administrator permissions
- Basic understanding of how to use Power Automate flows or Power Apps
- The following subscriptions that are a part of the license for Dynamics 365 Contact Center:
    - Power Automate
    - Power Apps 
- Ensure that the Power Apps and Power Automate environments are the same.
- Check if the Dynamics 365 CCaaS CRM Connector is available.
- In Power Apps > **Tables**, verify if the Account and Contact tables have the following columns:
    - Source CRM
    - Source CRM ID
    - Source CRM URL

## Add a Zendesk connection

1. In Power Automate, follow the steps in [Add a connection](/power-automate/add-manage-connections#add-a-connection) to add a Zendesk connection.
1. Specify your Zendesk domain, and then select **Create**.
1. In the pop-up window, sign in with your Zendesk credentials.
1. In the pop-up window that appears, select **Allow** to Power Platform to access your Zendesk account. A connection is created.
1. Follow the steps in [Add a connection](/power-automate/add-manage-connections#add-a-connection) to add a Dataverse connection, and then select **Create**.
1. In the pop-up window that appears, select your account. A connection is created.
1. Download all the Power Automate flows from the [Zendesk](https://github.com/microsoft/copilot-for-service/tree/CCaaS-3P-CRM-Connector/flows/Zendesk) repository.

1. In Power Automate, select **My flows**.
1. In **Import**, select **Import** and then select **Import Package (legacy)**.  
1. Select the downloaded flows and then select **Upload**.
1. In the **Import package** window, for the Microsoft Dataverse resource type, select **Select during import** and then select the Dataverse connection that you created and then select **Save**.
1. The connection is displayed on the Import page. Select **Import**.
1. The imported flows are displayed in the **My flows** page. The flows are disabled by default. For the flow you want to enables, select the more items (ellipsis) and then select **Turn on** to enable them.

## Edit flows and field mappings (Optional) 

1. If you want to edit the dlow or field mappings, select the flow that you want to edit. 
1. Select **Edit**.
1. You can use outputs from previous triggers and actions in the Dynamic content selector, or modify them by building an expression. See: [Use expressions in flow actions](/power-platform/blog/power-automate/use-expressions-in-actions/).

### Predefined column mapping

 The following table describes the predefined column mapping for the Zendesk and Dataverse connectors for Contact and Account.

**Contact**

| Zendesk | Dataverse |
|---------|-----------|
| id    | contactid |
| name  | lastname  |
|email  | emailaddress1 |
| phone  | mobilephone |
|organization_id | parentcustomerid |
|id      | msdyn_source_crm_id |
| Static Value: Zendesk  | msdyn_source_crm |
|Calculated Value | msdyn_source_crm_url |
| Created_at | createddate |

**Account**

| Zendesk | Dataverse |
|---------|-----------|
| name   | name |
| id  | accountid  |
|id  | msdyn_source_crm_id |
| Static Value: Zendesk  | msdyn_source_crm |
|Calculated Value | msdyn_source_crm_url |
| Created_at | createddate |

## Configure incremental data sync

We need to update the credentials in the Power Automate flows to connect the incremental flows to your Zendesk account. For all the incremental automated-triggered flows, please follow the steps below. 
1. Select the ZendeskCreateUserAPICall, ZendeskUpdateUserAPICall, and ZendeskCreateOrgHttp flows and then select **Edit**:    
  - Update the subdomain in the **URI** section with your subdomain.
  - Update the **Method** to **GET**
1. Select **Authentication** in **Advanced parameters**, and specify the following:

   - Authentication Type: **Basic**
   - Specify your Zendesk credentials in the **Username** and **Password** fields.
1. Login to the Zendesk account.
1. In the Zendesk Admin Center page, select Apps and integration. Select the Zendesk API option and then enable the Password access toggle.

## Configure Webhooks 

Set up webhooks in Zendesk to facilitate incremental data synchronization. Webhooks trigger notifications upon the creation, update, or deletion of a record. Name the flows to reflect the operation (Create, Update, Delete) and the entity involved (Org, User), for example, `ZendeskCreateOrgHttp`. 

To create webhooks, ensure you have the HTTP endpoint for the Power Automate flow. Perform the following steps: 

1. Select the required flow and then select **Edit**. 
1. Select **Manual** in the flow, and then copy the HTTP URL. Repeat the steps for the organization and user flows for all the create, update, and delete operations.

1. Sign in to your Zendesk instance and then select Admin center. 
1. Select **Apps and Integrations** > **Webhooks**. Perform the steps in [create a webhook](https://support.zendesk.com/hc/en-us/articles/4408839108378-Creating-webhooks-to-interact-with-third-party-systems#:~:text=To%20create%20a%20webhook,event%20types%20from%20the%20dropdown) to create a webhook.
1. Select **Create webhook**.
1. In the Create webhook page, select the following options in **Organization events**:
    -  **Support Organization Created** to create an organization, and then select **Next**.
    - **Support Organization name changed** to update the organization, and then select **Next**. 
    - **Support Organization deleted** to delete the organization, and then select **Next**. 
1. In the Create webhook page, select the following options in **User events**:
    -  **Support user Created** to create a user, and then select **Next**. 
    - **Any user events** to update a user, and then select **Next**. 
    - **Support user deleted** to delete users, and then select **Next**. 
1. Specify a name and update the Endpoint URL field with the endpoint copied from Power Automate flow.
1. Select **Test Webhook**, and then select **Send Test**. If you get a 202 Accepted response, the test has succeeded. 

## Run The Power Automate Flow 

In Power Automate https://make.powerautomate.com/environments/[environmentId], select the required flow and then select **Run**.

> [!NOTE]
> Automated flows are automatically triggered by create, update, and delete events.
Considerations 

