---
title: Create a Dataverse shortcut in Microsoft Fabric by using a service principal
description: Configure a service principal and use it to create a Dataverse shortcut in Microsoft Fabric.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection: 
ms.date: 10/30/2026
ms.custom: bap-template 
ai-usage: ai-assisted
---

# Create a Dataverse shortcut in Microsoft Fabric by using a service principal

Dynamics 365 Contact Center uses the Shared Analytics Platform data model to provide reporting-ready metrics for analyzing customer experience, representative performance, and operational efficiency.

To use this data for custom reporting, advanced analytics, or data engineering in Microsoft Fabric, create a Dataverse shortcut in a Fabric lakehouse. The shortcut makes the required Dataverse tables available in the lakehouse, where you can use them with Fabric capabilities.

This article explains how to configure a service principal and use its credentials to create the shortcut. A service principal provides an application identity for the connection instead of using an individual user's identity.

Before you create a shortcut, use **Link to Fabric** to make the source Dataverse tables available in Dataverse Managed Lake. Access to processed Contact Center analytics tables requires separate enablement and access; creating a source Dataverse shortcut doesn't provision those tables.

## How the connection works

The setup has two layers:

| Layer | Configuration | Purpose |
|---|---|---|
| Microsoft Entra ID | An app registration with a tenant ID, client ID, and client secret | Provides the application identity and credentials used by the connection. |
| Dataverse environment | An application user with assigned security roles | Authorizes the application in the Dataverse environment. |

Create the app registration once in the tenant. Create and authorize an application user separately in each Dataverse environment that the service principal must access.

**Link to Fabric** synchronizes selected source tables from Dataverse to Microsoft-managed lake storage and creates a lakehouse with shortcuts in your Fabric workspace. You can also create shortcuts from Fabric to tables that are already available in Dataverse Managed Lake. Dataverse shortcuts are read-only.

> [!TIP]
> Workspace identity is the recommended authentication option for **Link to Fabric** because it doesn't require you to manage a client secret. This article covers the service principal alternative. Learn more in [Configure your environment and link to Microsoft Fabric](/power-apps/maker/data-platform/fabric-link-to-data-platform).

## Prerequisites

Before you begin, ensure that you have:

- Permission to create app registrations in Microsoft Entra ID for the target tenant.
- The **System Administrator** security role in the target Dataverse environment to enable **Link to Fabric** and configure the application user.
- Access to the Power Platform admin center.
- Access to the Microsoft Fabric workspace where you want to create the shortcut.
- The required Dataverse tables available in Dataverse Managed Lake.

To enable **Link to Fabric**, you also need:

- Administrator access to the target Power BI workspace.
- Power BI Premium or Fabric capacity in the same Azure geographical region as your Dataverse environment.
- Permission to manage Fabric connections through **Settings** > **Manage connections and gateways**.
- The following tenant settings enabled by your administrator:
  - **Tenant settings** > **Microsoft Fabric** > **Users can create Fabric items**.
  - **Tenant settings** > **Workspace settings** > **Create workspaces**.
  - **Tenant settings** > **OneLake settings** > **Users can access data stored in OneLake with apps external to Fabric**.

Review the complete [Link to Fabric prerequisites](/power-apps/maker/data-platform/fabric-link-to-data-platform#prerequisites), including the additional capacity administrator requirement if you want the setup to create a workspace.

For processed analytics tables, confirm that your environment has modern historical analytics enabled and that your organization has the required access to those tables. Learn more in [Enable historical analytics reports](../administer/enable-contact-center-analytics.md) and [Connect to processed Contact Center analytics tables](../administer/modern-contact-center-analytics-journey.md#connect-to-processed-contact-center-analytics-tables).

## Configure the service principal

Complete the following procedures in order:

1. [Register an application in Microsoft Entra ID](/entra/identity-platform/quickstart-register-app). For an application that accesses resources only in your organization, use a single-tenant registration. After registering the application, copy the following values from its overview page:

   - **Application (client) ID**.
   - **Directory (tenant) ID**.

2. [Create a client secret](/entra/identity-platform/how-to-add-credentials#add-a-client-secret). Copy the secret **Value** when you create it. The value is displayed only once.

   > [!IMPORTANT]
   > Store the client secret securely. Don't include it in source code or share it through email or chat.

3. [Create an application user in the Dataverse environment](/power-platform/admin/manage-application-users#create-an-application-user). Select the Microsoft Entra application that you registered and the appropriate business unit.

4. As part of creating the application user, assign the **System Administrator** security role required to access data in Dataverse Managed Lake. Learn more in [Dataverse shortcut authorization](/fabric/onelake/create-dataverse-shortcut#authorization).

Repeat the Dataverse application-user configuration for each additional environment that the service principal must access.

## Enable Link to Fabric

If the source tables are already available in Dataverse Managed Lake, you can proceed to [Create the Dataverse shortcut](#create-the-dataverse-shortcut).

1. Prepare a Fabric-enabled workspace that meets the prerequisites.
2. Sign in to [Power Apps](https://make.powerapps.com) and select the Dataverse environment whose data you want to access.
3. Follow [Create a link to Fabric](/power-apps/maker/data-platform/fabric-link-to-data-platform#create-a-link-to-fabric). In **Link data**, select **+ New link**, and then select **Link data via Fabric**.
4. Select the target workspace and configure the connection. To use the service principal configured earlier, select **Service Principal** authentication and provide its tenant ID, client ID, and client secret.
5. Select the source tables to synchronize, review your selections, and finish creating the link. Wait for the initial synchronization to complete before using the data.

Link to Fabric creates a lakehouse and shortcuts for the selected tables. If these shortcuts meet your needs, you don't need to create them again. Use the following section when you want to create shortcuts in another lakehouse or select from tables already available in Dataverse Managed Lake.

To change the source tables later, use **Manage tables** on the Fabric link. Learn more in [Add or remove tables linked to Fabric](/power-apps/maker/data-platform/fabric-link-to-data-platform#add-or-remove-tables-linked-to-fabric).

## Create the Dataverse shortcut

Follow the instructions in [Create shortcuts through Fabric](/fabric/onelake/create-dataverse-shortcut#create-shortcuts-through-fabric). When you create the connection, select **Service Principal** as the authentication method and provide the following values:

| Field | Value |
|---|---|
| Environment domain | The Dataverse environment domain, such as `yourorg.crm.dynamics.com`. Don't include `https://`. |
| Authentication kind | **Service principal** |
| Tenant ID | The directory (tenant) ID from the Microsoft Entra app registration. |
| Service principal client ID | The application (client) ID from the Microsoft Entra app registration. |
| Service principal key | The client secret value. |

After you create the connection, select the Dataverse tables to make available in the Fabric lakehouse.

If the source tables aren't visible, confirm that they're selected in **Link to Fabric** and that their initial synchronization is complete.

## Choose source and analytics tables

Source Dataverse tables and processed analytics tables serve different purposes:

| Data | Purpose | Examples |
|---|---|---|
| Source Dataverse tables | Build custom analytics from operational records selected through Link to Fabric. | `account`, `contact`, `incident`, and `msdyn_agentstatushistory`. |
| Processed analytics tables | Use reporting-ready aggregates, facts, and dimensions used by built-in historical analytics, and combine them with source data when needed. | `AggConversation`, `AggAgentPerformance`, `AggQueuePerformance`, and `DimChannel`. |

When you enable Shared Analytics Platform (also referred to as analytics v2) and have access, analytics tables appear under `DIA_Workspace`. 

Use only customer-visible tables exposed through your supported data access experience. Enabling Link to Fabric for source tables doesn't by itself enable access to processed analytics tables. Learn more in [Connect to processed Contact Center analytics tables](../administer/modern-contact-center-analytics-journey.md#connect-to-processed-contact-center-analytics-tables).

Learn more about table definitions and relationships in [Understand the Contact Center data model](overview-data-model.md).

## Plan for data freshness and storage

Data availability isn't real-time. Link to Fabric synchronization latency varies with table size, number of columns, change volume, and workload. The initial synchronization can take longer for large tables, and bursts of changes can delay later updates. Published latency measurements are planning examples, not a service-level agreement. Learn more in [Plan your latency for Link to Fabric](/power-apps/maker/data-platform/fabric-link-plan-latency).

These measurements describe source Dataverse synchronization, not a guarantee of end-to-end freshness for processed analytics tables. Check the freshness of the tables used by your reports before publishing them.

Enabling Link to Fabric consumes Dataverse storage. In the environment's storage capacity details, synchronized tables can appear as `entityName-Analytics`. Select only the source tables you need, and monitor capacity as data grows. Learn more in [Dataverse capacity-based storage details](/power-platform/admin/capacity-storage).

## Maintain the connection

- Store the client secret in a secure credential store, such as Azure Key Vault.
- Track the client secret expiration date and rotate it before it expires.
- Review the Dataverse security roles periodically and retain the permissions required by the selected connection method.
- Remove the application user from each Dataverse environment when the identity is no longer required.

> [!NOTE]
> Removing the app registration from Microsoft Entra ID doesn't automatically remove the corresponding application user from Dataverse.
