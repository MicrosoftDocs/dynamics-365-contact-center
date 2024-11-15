---
title: Configure the connector for Salesforce
description: Learn how to configure the connector for Salesforce in Dynamics 365 Contact Center to bring Salesforce data into Dataverse.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection:
ms.date: 08/01/2024
ms.custom: bap-template
---

# Configure the connector for Salesforce

With the connector for Salesforce in Dynamics 365 Contact Center, organizations can use omnichannel capabilities to engage with customers without having to give up their investments in non-Microsoft customer relationship management (CRM) solutions.

The omnichannel add-in uses data connectors to work with non-Microsoft CRM solutions. The connector for Salesforce helps bring contact and account data from Salesforce into Dataverse.

## Prerequisites

- Access to the Salesforce instance
- System administrator role for Dynamics 365 Contact Center and Salesforce
- License for Dynamics 365 Contact Center
- Salesforce license to access change data capture

> [!NOTE]
> We also recommend that you complete the following steps:
>
> - Before you set up the connector, back up the existing data in the `Contact` and `Account` tables in Dataverse. In this way, you can do a rollback if any data issues occur.
> - For optimal performance, limit the data size to 10 gigabytes (GB). In addition, make sure that your limit on Salesforce API requests is sufficient to support your data synchronization needs.

## Configure the data connector

> [!IMPORTANT]
> After you configure the data connector and sync it from the Salesforce instance, we recommend that you don't make any changes to the synced data in Dataverse, because those changes aren't synced back to Salesforce. If you must update the data, update it only in Salesforce.

1. In Contact Center admin center, in the site map, under **Agent experience**, go to **Workspaces**. Then, for **Data synchronization from external CRMs**, select **Manage**. Alternatively, on the home page, under **CRM connection wizard**, select **Open**.
1. On the **Data synchronization from external CRMs** page, select **New**.
1. On the **Create a CRM connector** page, select **Salesforce**, and then select **Next**. If you're connecting to Salesforce for the first time, the **Connection Setup** dialog displays a **Sign in** button. Otherwise, the dialog displays an ellipsis (**&hellip;**) button that you can use to sign in.

    > [!NOTE]
    > The system redirects you to Power Apps to connect to your Salesforce instance. Dynamics 365 uses the connection to sync data.

1. Follow these steps:

    1. Select the option that is shown, and then select **Add new connection**.
    1. In the dialog box that appears, select the Salesforce environment and Salesforce API version, and then select **Sign in**.
    1. On the Salesforce sign-in page, use the Salesforce user credentials to sign in. Complete the multifactor authentication if it's required.
    1. In the **Allow Access** dialog box that appears, select **Allow**.

        In the **Connection Setup** dialog box, a green check mark indicates a successful connection to the Salesforce instance.

    1. Select **Create**.

1. On the **Add Third party CRM connector** page, select **I agree to share connector permissions**, and then select **Next**.
1. The **Enable salesforce permissions** page lists steps that you must complete in Salesforce. Sign in to the Salesforce instance that opens on a new tab, and then complete the steps that are listed. When you're finished, go to the setup page in Contact Center admin center, and select the checkbox that indicates that you completed the steps in Salesforce.
1. Select **Next**.
1. On the **Choose tables to sync** page, select the `Contacts` and `Accounts` tables that you want to sync. To maintain the relationship about the linked data between the records, we recommend that you select both tables.
1. Select **Next**.
1. For each table that you selected, in the **Column mapping** section, map the source and destination columns. You can also update the predefined mappings according to your business needs. The source column shows only fields that have a [compatible data type](#data-types-supported-in-dataverse).
1. Select **Next**.
1. On the **Teams permissions** page, select the Teams permission. The Team ID is used to write data to Dataverse. Therefore, it must have read and write permissions on the selected tables. Otherwise, data synchronization fails. Learn more in [Teams in Dataverse](/power-platform/admin/manage-teams).
1. On the next page, review the mappings for each table that you selected. You can go back and change settings as you require.
1. Select **Create**.

    If the connection is successful, a message appears on the **Summary** page.

1. Select the checkbox to activate the connector and data synchronization, and then select **Done**. You can view the synchronization status on the **Data synchronization from external CRMs** page.

### Data types supported in Dataverse

Dataverse supports the following data types. It doesn't support the *Virtual* and *EntityName* data types.

| Dataverse columns of attribute type | Salesforce columns of data type type |
|---|---|
| Boolean | boolean |
| Integer, BigInt | integer |
| Integer, BigInt, Decimal, Double, Number | number |
| String/Memo | <p>string: date. datetime</p><p><strong>Note:</strong> ID and reference aren't accepted.</p> |
| Uniqueidentifier, Lookup, Owner, Customer | string with data type: ID, reference |
| DateTime | string with data type: date, datetime |

### Predefined data mappings

The following table shows the predefined data mappings for the `Contact` table.

| Salesforce field name | Dataverse field name |
|---|---|
| AssistantName | AssistantName |
| AssistantPhone | AssistantPhone |
| Birthdate | BirthDate |
| GUID from SF Id (transformed data) | ContactId |
| Department | Department |
| Description | Description |
| Email | EMailAddress1 |
| Fax | Fax |
| FirstName | FirstName |
| LastName | LastName |
| MobilePhone | MobilePhone |
| Salutation | Salutation |
| Phone | Telephone1 |

The following table shows the predefined data mappings for the `Account` table.

| Salesforce field name | Dataverse field name |
|---|---|
| GUID from SF AccountId (transformed data) | AccountId |
| AccountNumber | AccountNumber |
| Description | Description |
| Fax | Fax |
| Name | Name |
| NumberOfEmployees | NumberOfEmployees |
| Sic | SIC |
| Phone | Telephone1 |
| TickerSymbol | TickerSymbol |

## Manage the data connector

This section lists the actions that you can perform by using the selected connector.

- Activate or deactivate the connector.
- View diagnostic details.
- Edit the details of the connector:

    - **Data tables:** Update the tables that you want to sync.
    - **Field mappings:** Update the column mappings. Use the **Reset** option to reset the mappings to the out-of-box defined mappings.
    - **Data access permissions:** Update the Teams ID that is used to write the data to Dataverse.

    > [!NOTE]
    > If you add new tables or mappings, the data for the existing tables and mappings is also synced. If a table or mapped field is removed, the data remains in Dataverse, and only new data isn't synced.

:::image type="content" source="../media/connector-salesforce.png" alt-text="Screenshot of the connector page in Dynamics 365 Contact Center, showing the buttons and links for the actions that you can perform.":::

## Next steps

[Configure a workstream](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context)

## Related information

[Single sign-on SAML protocol](/entra/identity-platform/single-sign-on-saml-protocol)
