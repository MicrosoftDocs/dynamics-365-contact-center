---
title: Configure connection references for Customer Knowledge Management Agent flow
description: Configure connection references for cases and conversations in the Quality Evaluation Agent flow. Follow these steps to get started.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: 
ms.date: 10/15/2025
ms.custom: bap-template
---

# Configure connection references for Quality Evaluation Agent flow

Configure connection references for the Quality Evaluation Agent flow. You need to set the following connection references:

- **QEA On Demand Evaluation Case** for cases.

- **AI Evaluation Flow for Conversation** for conversations.

Learn more in [Add connection references to a solution.](/power-apps/maker/data-platform/create-connection-reference#add-connection-references-to-a-solution).

## Set connection references for Quality Evaluation Agent flow

1. Sign in to [make.powerapps.com](https://make.powerapps.com) and select your environment.

1. Go to **Solutions** > **Default Solution** > **Objects** > **Connection References**.

1. Search for the following connection references:

    - For cases: **QMA.Incident.DVPluginConnection, Microsoft Copilot Studio (Preview) CaseReviewerFlow** and **Microsoft Dataverse FlowRunTest-8625a**.
    
    - For conversations: **Microsoft Dataverse CDS Connection for QEA Conversation, Microsoft Copilot Studio (Preview) CaseReviewerFlow** and **Microsoft Dataverse FlowRunTest-8625a**.

1. To create a connection for **QMA.Incident.DVPluginConnection**:

    1.  In the **Edit** dialog, select **Connection > New connection.**

    2.  Search for **Microsoft Dataverse**, select **Create** and sign in using the **OAuth connection** type to create a Dataverse connection.

    3.  Repeat to create a connection for **Microsoft Copilot Studio (preview)**.

    4.  Go back to the **Edit** dialog of **QMA.Incident.DVPluginConnection**, search for the new connection and save it.

1. Save your changes.

1. Repeat steps 4-6 for **Microsoft Dataverse CDS Connection for QEA Conversation** and **Microsoft Copilot Studio (Preview) CaseReviewerFlow**.

## Turn on the flow

In [make.powerapps.com](https://make.powerapps.com) from **Solutions** > **Default Solution** > **Objects** > **Cloud flows**, select **QEA On Demand Evaluation Case** and **AI Evaluation > Flow for Conversation**, and then select **Turn on**.

Alternatively, in [Power Automate](https://powerautomate.microsoft.com), search for **QEA On Demand Evaluation Case** and the **AI Evaluation Flow for Conversation** in **Cloud flows**, and turn these on. Learn more in [Power Automate](/power-automate/overview-cloud#find-your-flows-easily).

## Publish the Microsoft Copilot Studio agent

1.  In [Microsoft Copilot Studio](https://copilotstudio.microsoft.com/), select your environment, and then search for the **Quality Evaluation Agent - Incident** case agent and the **QualityEvaluationAgentForConversation** conversation agent.

2. [Publish the agent](/microsoft-copilot-studio/publication-fundamentals-publish-channels?tabs=web)

Once done, go to the Copilot Service admin center and enable [Enable Quality Evaluation Agent](manage-quality-evaluation-agent.md#enable-quality-evaluation-agent).

## Related information

[Manage Quality Evaluation Agent](manage-quality-evaluation-agent.md#manage-quality-evaluation-agent)
