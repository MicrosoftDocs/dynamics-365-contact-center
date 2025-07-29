---
title: How-to topic template #Required; page title displayed in search results. Don't enclose in quotation marks.
description: How-to description #Required; article description that's displayed in search results. Don't enclose in quotation marks. Do end with a period.
author: rhanajoy #Required; your GitHub user alias, with correct capitalization.
ms.author: rhcassid #Required; your Microsoft alias; optional team alias.
ms.reviewer: kfend #Required; Microsoft alias of content publishing team member.
ms.topic: how-to #Required; don't change.
ms.collection: get-started #Required; If this isn't a getting started article, don't remove the attribute, but leave the value blank. The values for this attribute will be updated over time.
ms.date: 07/29/2025
ms.custom: bap-template #Required; don't change.
---


# Migrate Copilot Studio survey agents configurations


You can migrate Microsoft Copilot Studio survey agent configurations between Dataverse environments using the Application Lifecycle Management (ALM) framework. The ALM framework allows you to transfer survey agents, connection references, and related components while maintaining functionality across environments

You can migrate the agents in one of the following ways: 

- Migrating standalone survey configurations 
- complete workstream configurations with integrated surveys. 

## Prerequisites

Before you begin the migration process, ensure you have the following prerequisites in place:

1. Access to both the source and target Dataverse environments.
2. Appropriate permissions to create and manage solutions in both environments.
3. Familiarity with the ALM framework and its components.

## Migrate survey agent configurations

To migrate survey agent configurations, perform the following steps:

1. In Power Apps, create a new solution in the source environment where the survey agents are configured. Learn more in [Create a solution](/power-apps/maker/data-platform/create-solution).
1. In the solution, select **Add existing**> **More** > **Other** > **Customer feedback survey**. The **
Add existing Customer feedback survey** pane appears.
1. Select the survey agents you want to migrate. You can select multiple agents at once.
1. For the selected agents, select **Properties** for the **Conversation Start** topic. The **Managed Properties** pane appears. 
1. Turn on the **Allow customizations** toggle.
1. Publish the customizations and then [export the solution](/power-apps/maker/data-platform/export-solutions#export-from-power-apps). A .zip file is downloaded to your local machine.
1. In the target environment, import the solution you downloaded from the source environment. Learn more in [Import a solution](/power-apps/maker/data-platform/import-update-export-solutions).
1. Make sure you verify that the imported connection references are connected to Dataverse. If the references are missing, add a new connection to Microsoft Copilot Studio. Learn more in [Use a connection reference in a solution with Microsoft Dataverse](/power-apps/maker/data-platform/create-connection-reference).
1. In Microsoft Copilot Studio, make sure the survey agents are working as expected and that the connection references are properly configured.
1. Save and publish the agents.
1. In Copilot Service Admin center, verify that the agent is available and the status of the agent is set to Ready. Learn more in []

## Migrate chat, voice workstream and survey agent configurations

To migrate chat and voice workstream configurations along with survey agent configurations, perform the following steps. We recommend that you remove all the voice channel settings in the target environment before you start the migration.

1. In Power Apps, create a new solution in the source environment where the chat and voice workstream configurations are set up.
2. In the solution, select **Add existing** > **More** > **Other** > **msdyn_surveyconfig**. The **Add existing msdyn_surveyconfig** pane appears.
3. Select the required configurations you want to migrate. You can select multiple configurations at once.
4. For the selected configurations, select **Properties** for the **Conversation Start** topic. The **Managed Properties** pane appears.
5. Turn on the **Allow customizations** toggle.
6. Publish the customizations and then [export the solution as a managed solution](/power-apps/maker/data-platform/export-solutions#export-from-power-apps). A .zip file is downloaded to your local machine.
7. In the target environment, import the solution you downloaded from the source environment. Learn more in [Import a solution](/power-apps/maker/data-platform/import-update-export-solutions).
1. 
1. Make sure you verify that the imported connection references are connected to Dataverse. If the references are missing, add a new connection to Microsoft Copilot Studio. Learn more in [Use a connection reference in a solution with Microsoft Dataverse](/power-apps/maker/data-platform/create-connection-reference). Make sure the Dataverse connection is present in the target organization.
1. In Microsoft Copilot Studio, make sure the chat and voice workstream configurations are working as expected and that the connection references are properly configured.
1. Save and publish the configurations.
1. In Copilot Service Admin center, verify the following:
    - Chat and voice workstreams are available.
    -  The survey agent is available with the status set to Ready.

## Next steps

<!--Remove all the comments in this template before you sign-off or merge to the main branch.-->
