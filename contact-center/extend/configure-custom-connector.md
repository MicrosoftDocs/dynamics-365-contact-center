---
title: Configure the connector for any CRM solution
description: Learn how to use the connector for any CRM solution to fetch data into Dataverse and use in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection:
ms.date: 07/01/2024
ms.custom: bap-template
---

# Configure the connector for any CRM solution

The Microsoft Contact Center&mdash;Power Automate solution for any CRM connector allows organizations to engage with their customers using capabilities such as voice, video, SMS, live chat, and social messaging from their third-party CRM solutions. You can use Power Automate data connectors to sync the contacts and accounts data from the  CRM solution into Dataverse.

## Prerequisites 

-  A CRM instance
- License for Dynamic 365 Contact Center, that include the Power Automate and Power Apps subscriptions.
- Power Platform System administrator permissions
- Basic understanding of how to use Power Automate flows or Power Apps
- Ensure that the Power Apps and Power Automate environments are the same.
- The Dynamics 365 CCaaS CRM Connector, **msdyn_ContactCenterCRMConnector**, is available in the Power Apps environment and the Account and Contact [tables](/power-apps/maker/data-platform/entity-overview) have the following columns:
    - Source CRM
    - Source CRM ID
    - Source CRM URL

## Copy data

You can copy data from your CRM instance to Dataverse in one of the following ways:

- **Initial sync**: Copy data from CRM to Dataverse through manual triggers. We recommend that you use [pagination](/power-automate/dataverse/list-rows?tabs=classic-designer) as Power Automate connectors have a limit on the number of records that can be fetched at a time.
- **Incremental sync**: Copy data through automated triggers.

## Import Power Automate flows to sync Account and Contact records

Perform the steps outlined in the sections that follow.

### Add a Dataverse connector

1. Follow the steps in [Add a connection](/power-automate/add-manage-connections#add-a-connection) to add a Dataverse connection, and then select **Create**.
1. In the pop-up window that appears, select your account. A connection is created.

You can establish a connection to your CRM instance using the following methods.

### Add any CRM connector

Add a connector in one of the following ways:

**Power Automate**    

1. Follow the steps in [Add a connection](/power-automate/add-manage-connections#add-a-connection) to find and add the CRM connector.
1. Specify the required information. A connection is created.

**Add a CRM using API calls**      

1. Create a new [flow](/power-automate/get-started-logic-flow) in Power Automate.
1. Add the HTTP action and specify the required parameters such as the URL, method, and headers. In **Parameters** > **Authentication** set the **Authentication Type** to **Basic** and specify the **Username** and **Password**.

Your HTTP action can send and receive JSON requests and responses.

**Add a CRM using webhooks**    

Set up webhooks in your CRM to facilitate incremental data synchronization. Webhooks trigger notifications upon the creation, update, or deletion of a record. 

To create webhooks, ensure you have the HTTP endpoint for the Power Automate flow. Perform the following steps to get the endpoint in Power Automate: 

1. Select the required flow and then select **Edit**. 
1. Select **Manual** in the flow, and then copy the HTTP URL. Repeat the steps for the organization and user flows for all the create, update, and delete operations.

You can use this URL as the webhook endpoint in your CRM.

**Add a CRM using Business rules**     

You can use trigger notifications when a record is created, updated, and deleted. You must use the Customer Service Plugin to trigger these notifications. You must create the script in the following order:

1. Create REST Message
2. Create Business Rule

For more information, see: [Configure incremental data sync](configure-servicenow-connector.md)

 **Use Apex triggers**    

Use [Apex triggers](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_dev_guide.htm). Ensure that your CRM instance has the required privileges to create the triggers.

## Run the Power Automate Flow 

In Power Automate, select the required flow and then select **Run**. 

> [!NOTE]
> The create, update, and delete events automatically trigger the flows.

### See also

[Configure a connector for ServiceNow](configure-servicenow-connector.md)  



