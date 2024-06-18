---
title: Configure the connector for Salesforce
description: Learn how to configure the connector for Salesforce in Dynamics 365 Contact Center to bring the data into Dataverse.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection:
ms.date: 07/01/2024
ms.custom: bap-template
---

# Configure the connector for Salesforce

The connector for Salesforce in Dynamics 365 Contact Center allows organizations to engage with their customers using omnichannel capabilities like voice, video, SMS, live chat, and social messaging while keeping their current investments in third-party CRMs. The omnichannel add-in will work with third-party CRMs through data connectors. These connectors will help bring the contacts and accounts data from Salesforce into Dataverse. 

## Prerequisites

- Access to Salesforce instance.
- System administrator role.
- License for Dynamics 365 Contact Center.

> [!NOTE]
> We recommend the following:
> - Back up the existing data in the Contact and Account tables in Dataverse before you set up the connector to rollback if any data issues occur.
> - For optimal performance, sync a small set of 10,000-20,000 records for trial or demo purposes.

## Configure the data connector

1. In the site map of Contact Center admin center, go to **Workspaces** under **Agent experience**, and select **Manage** for **Data synchronization from external CRMs**.
1. On the **Data synchronization from external CRMs** page, select **New**.
1. On **Add Third party CRM connector**, select **Salesforce**, and select **Next**.
    1. On the **Connection Setup** dialog, select the ellipses for Salesforce, and select **Add new connection**. 
    1. On the dialog that appears, select the Salesforce environment and Salesforce API version, and select **Sign in**.
    1. On the Salesforce sign in page, sign in with the Salesforce user credentials. Complete the multifactor authentication if it's configured. The **Allow Access** dialog appears.
    1. Select **Allow**. A green tick mark on the **Connection Setup** dialog indicates a successful connection to the Salesforce instance.
    1. Select **Create**. 
1. On the **Add Third party CRM connector**, select **I agree to share connector permissions**, and select **Next**.
    1. On the **Enable salesforce permissions** page, complete the steps listed on the page by signing into the Salesforce instance that opens on a new tab.
    1. Go to the setup page in Contact Center admin center, and select the checkbox that indicates you have completed the steps in Salesforce.
1. Select **Next**.
1. On the **Choose tables to sync** page, select the **Accounts** and **Contacts** tables. To maintain the relationship about the linked data between the records, we recommend that you select both the tables.
1. Select **Next**, and in the **Column mapping** section, map the source and destination columns according to your business needs.
1. Select **Next**, and on the Teams permissions page, select the Teams permission.
1. On the next page, review the mappings for each of the tables that you have selected. You have the option to go back and change a setting.
1. Select **Create**.

## Next steps

