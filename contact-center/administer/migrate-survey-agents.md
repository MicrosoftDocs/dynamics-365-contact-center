---
title: Migrate Copilot Studio survey agents configurations
description: Learn how to migrate Copilot Studio survey agents configurations using Application Lifecycle Management.
author: gandhamm
ms.author: mgandham
ms.reviewer: gandhamm
ms.topic: how-to 
ms.custom: 
ms.date: 08/19/2025
ms.collection: bap-ai-copilot
---


# Migrate Copilot Studio survey agents configurations


You can migrate Microsoft Copilot Studio survey agent configurations between Dataverse environments using the application lifecycle management (ALM) framework. The ALM framework allows you to transfer survey agents, connection references, and related components while maintaining functionality across environments.

You can use one of the following options: 

- migrate the survey agent configuration only.
- migrate the survey agent and corresponding workstream configurations. 

## Prerequisites

- Access to both the source and target Dataverse environments.
- Appropriate permissions to create and manage solutions in both environments.
- Familiarity with the ALM framework and its components.

## Migrate survey agent configuration

1. In Power Apps, create a solution in the source environment where the survey agents are configured. Learn more in [Create a solution](/power-apps/maker/data-platform/create-solution).
1. In the solution, select **Add existing**> **More** > **Other** > **Customer feedback survey**. The **Add existing Customer feedback survey** pane appears.
1. Select the survey agents you want to migrate. You can select multiple agents at once.
1. For the selected agents, select **Properties** for the **Conversation Start** topic. The **Managed Properties** pane appears. 
1. Turn on the **Allow customizations** toggle.
1. Publish the customizations and then [export the solution](/power-apps/maker/data-platform/export-solutions#export-from-power-apps). A .zip file is downloaded to your local computer.
1. In the target environment, import the solution you downloaded from the source environment. Learn more in [Import a solution](/power-apps/maker/data-platform/import-update-export-solutions).
1. In Copilot Service admin center, verify that the AI agent is available and the status is Ready. Learn more in [Configure feedback surveys using Copilot Studio](../administer/configure-surveys.md). 
1. In Power Apps, verify that the imported connection references are connected to Dataverse. Make sure the Dataverse connection is present in the destination environment. If the references are missing, add a new connection to Copilot Studio. Learn more in [Use a connection reference in a solution with Microsoft Dataverse](/power-apps/maker/data-platform/create-connection-reference).
1. In Copilot Studio, make sure the survey agents are working as expected and that the connection references are properly configured to point to the current organization. Learn more in [Configure and manage connections](/microsoft-copilot-studio/authoring-connections).
1. Save and publish the agents.

## Migrate chat, voice workstream, and survey agent configuration

To migrate chat and voice workstream configurations along with survey agent configurations, perform the following steps. We recommend that you remove all the voice channel settings in the target environment before you start the migration.

1. In Power Apps, create a new solution in the source environment where the chat and voice workstream configurations are set up.
2. In the solution, select **Add existing** > **More** > **Other** > **msdyn_surveyconfig**. The **Add existing msdyn_surveyconfig** pane appears.
3. Select the required configurations you want to migrate. You can select multiple configurations at once.
4. For the selected configurations, select **Properties** for the **Conversation Start** topic. The **Managed Properties** pane appears.
5. Turn on the **Allow customizations** toggle.
6. Publish the customizations and then [export the solution as a managed solution](/power-apps/maker/data-platform/export-solutions#export-from-power-apps). A .zip file is downloaded to your local machine.
7. In the target environment, import the solution you downloaded from the source environment. Learn more in [Import a solution](/power-apps/maker/data-platform/import-update-export-solutions).
1. In Copilot Service admin center, verify the following information:
    - Chat and voice workstreams are available.
    - The survey agent is available with the status set to Ready. Learn more in [Manage the survey](configure-surveys.md#manage-the-surveys)
1. Add a new connection to Copilot Studio in Power Apps, if the imported connection references to connected with Dataverse are missing. Learn more in [Use a connection reference in a solution with Microsoft Dataverse](/power-apps/maker/data-platform/create-connection-reference).
1. In Copilot Studio, make sure the survey agents are working as expected and that the connection references are properly configured to point to the current organization. Learn more in [Configure and manage connections](/microsoft-copilot-studio/authoring-connections).
1. Save and publish the configurations.
1. In Copilot Service admin center, verify that the chat and voice workstreams are working as expected. Set up the queue and update the other required settings accordingly.

## Related information

[Configure feedback surveys using Copilot Studio (preview)](configure-surveys.md)