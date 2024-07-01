---
title: Configure the connector for ServiceNow
description: Learn how to use the connector for ServiceNow CRM solution to fetch data into Dataverse and use in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.date: 06/25/2024
ms.custom: bap-template 
---

# Configure the connector for ServiceNow

The Microsoft Contact Center — Power Automate solution for ServiceNow connector allows organizations to engage with their customers using capabilities such as voice, video, SMS, live chat, and social messaging from their third-party CRM solutions. You can use Power Automate data connectors to sync the contacts and accounts data from the ServiceNow CRM solution into Dataverse.

## Prerequisites
-  A ServiceNow instance. For example, `https://[your-instance-name].service-now.com/`
- License for Dynamic 365 Contact Center, that include the Power Automate and Power Apps subscriptions.
- Power Platform System administrator permissions
- Basic understanding of how to use Power Automate flows or Power Apps
- Ensure that the Power Apps and Power Automate environments are the same.
- The Dynamics 365 CCaaS CRM Connector, **msdyn_ContactCenterCRMConnector**, is available is available in the Power Apps environment and the Account and Contact tables have the following columns:
    - Source CRM
    - Source CRM ID
    - Source CRM URL

## Use Power Automate Flow to sync Account and Contact records

The process for using the Power Automate flow is as follows:

1. Configure the View-In-CRM functionality
1. Import Power Automate flows
1. Configure Incremental Data Sync (Create, Update and Delete)
1. Run the power automate flow

## Configure View-In-CRM functionality

ServiceNow uses calculated field feature to create a special field to store the `subdomain/baseUrl /InstanceName` in **Account** and **Contact** tables. The **Source CRM URL** column in **Account** and **Contact** tables stores the full URL of the Account or Contact record, which can be accessed by selecting the URL.

To create the custom field in ServiceNow, perform the following steps:

1. Sign in to ServiceNow instance (https://[your-instance-name].service-now.com/), select **All** and then search for table.
1. Select **Tables** in **System Definition** and then select **Account** and **Contact** table to create a custom field. 
1. Select **New** and then specify the following:
    - Table: Account[customer_account]
    - Type: String
    - Column label: Base URL
    - Column name: u_base_url
    - Application: Global
    - Select the Active check box.
1. Select the **CalculatedValue** tab and then select the **Calculated** checkbox. Add return `gs.getProperty('instance_name');` in **Calculation** textbox.
1. Select **Save** and then select **Update**.

Repeat the same configuration for the Contact table.

## Import the Power Automate flow

**Add a ServiceNow connector**
1. In Power Automate, follow the steps in [Add a connection](/power-automate/add-manage-connections#add-a-connection) to add a ServiceNow connection.
1. Specify your ServiceNow instance and credentials, and then select **Create**.

**Add a Dataverse Connector**

1. In Power Automate, follow the steps in [Add a connection](/power-automate/add-manage-connections#add-a-connection) to add a Dataverse connection, and then select **Create**.
1. In the pop-up window that appears, select your account. A connection is created.

**Download flows from GitHub**

1. Download all the Power Automate flows from the [ServiceNow](https://github.com/microsoft/copilot-for-service/tree/CCaaS-3P-CRM-Connector/flows/ServiceNow) repository.


**Import flows to Power Automate**

1. In Power Automate, select **My flows**.
1. In **Import**, select **Import** and then select **Import Package (legacy)**.  
1. Select the downloaded flows and then select **Upload**.
1. In the **Import package** window, for the Dataverse resource type, select **Select during import** and then select the Dataverse connection that you created and then select **Save**.
1. The connection is displayed on the Import page. Select **Import**.
1. The imported flows are displayed in the **My flows** page. The flows are disabled by default. For the flow you want to enables, select the more items (ellipsis) and then select **Turn on** to enable them.

## Configure incremental data sync


Incremental data sync updates the ServiceNow data to Dataverse in realtime through automated triggers.
ServiceNow uses scripts to trigger notifications when a record is created, updated, and deleted. You must use the Customer Service Plugin to trigger these notifications. You must create the script in the following order:

1. Create REST Message
2. Create Business Rule

> [!NOTE]
> The following steps must be performed for both Account and Contact tables.

### Create REST message

1. Login to the ServiceNow instance, select **All** and search for rest message in the search bar.
1. Select **Outbound** > **Rest Message**.
1. Select **New** to create a new REST message.
1. In the **Rest Message** page, specify the required fields. See: [Create a REST message](https://docs.servicenow.com/bundle/tokyo-application-development/page/integrate/outbound-rest/task/t_ConfiguringARESTMessage.html).
   - Create individual REST Messages for create, update, and delete. Update the **Endpoint** field in **REST Messages** with the Power Automate flow. Perform the following steps to get the URL:

     1. Select the required flow and then select **Edit**. 
     1. Select **Manual** in the flow, and then copy the HTTP URL. Repeat the steps for the organization and user flows for all the create, update, and delete operations
     1. Select **New** in **Authentication** tab to create a new HTTP method.
     1. Specify the same endpoint from Power Automate flow as the endpoint for the HTTP Method for the respective operation.
     1. Copy the  **REST Message** and **Name** fields on this page, which are required in **Business Rules** script. 
   - Create a new variable, **baseURL**. The value of this variable is the initial part of the same endpoint that contains hostname/IP and port number.  

### Create Business Rule

1. Login to the ServiceNow instance, select **All** and search for business rules in the search bar.
1. Select **System Definition** > **Business Rule**.
1. Select **New** to create a new REST message.
1. In the **Business Rule** page, specify the required information. See: [Business Rules](https://developer.servicenow.com/dev.do#!/learn/courses/washingtondc/app_store_learnv2_scripting_washingtondc_scripting_in_servicenow/app_store_learnv2_scripting_washingtondc_server_side_scripting/app_store_learnv2_scripting_washingtondc_business_rules).
   - In the **When to run** tab, add the required conditions to trigger the business rule for create, update, and delete record operations.
   - Download the scripts from [ServiceNow scripts](https://github.com/microsoft/copilot-for-service/tree/CCaaS-3P-CRM-Connector/flows/ServiceNow/Scripts) for the required operations for the Contact and Account tables.
   - Update the **Script** field in **Advanced** tab with the downloaded scripts for the specific operation.
   - For the script, update the baseURL with the corresponding values from the HTTP method in the REST Message.

## Run The Power Automate Flow 

In Power Automate https://make.powerautomate.com/environments/[environmentId], select the required flow from **Cloud flows** and then select **Run**.

## Edit flows and field mappings (Optional) 

1. If you want to edit the flow or field mappings, select the flow that you want to edit. 
1. Select **Edit**.
1. You can use outputs from previous triggers and actions in the Dynamic content selector, or modify them using [expressions](/power-platform/blog/power-automate/use-expressions-in-actions/).

For example, the **Account Name** field in Dataverse can be mapped to the **Name** field in ServiceNow with the `‘triggerBody()?['name']’` expression. See: [ServiceNow REST API reference](https://docs.servicenow.com/bundle/washingtondc-api-reference/page/build/applications/concept/api-rest.html)

### Predefined column mapping

 The following table describes the predefined column mapping for the ServiceNow and Dataverse connectors for Contact and Account.

**Contact**

| ServiceNow | Dataverse |
|---------|-----------|
| sys_id    | contactid |
| last_name | lastname  |
| first_name| firstname |
|email  | emailaddress1 |
| mobile_phone  | mobilephone |
|phone|telephone1 |
|account| parentcustomerid |
|sys_id     | msdyn_source_crm_id |
| Static Value: ServiceNow  | msdyn_source_crm |
|u_base_url | msdyn_source_crm_url |
| sys_created_on | createddate |

**Account**

| ServiceNow | Dataverse |
|---------|-----------|
| name   | name |
|phone|telephone1 |
| sys_id  | accountid  |
|city| address1_city |
|zip|address1_postalcode|
|NumberOfEmployees|numberofemployees|
|id  | msdyn_source_crm_id |
| Static Value: ServiceNow  | msdyn_source_crm |
|u_base_url | msdyn_source_crm_url |
| sys_created_on | createddate |