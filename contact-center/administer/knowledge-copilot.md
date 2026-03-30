---
title: Enable knowledge sources from Microsoft Copilot Studio (preview)
description: Learn how to enable knowledge sources from Microsoft Copilot Studio.
author: Soumyasd27
ms.author: sdas
ms.reviewer: Soumyasd27
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days 
ms.date: 03/31/2026
ms.custom: bap-template
---

# Enable knowledge sources from Microsoft Copilot Studio (preview)

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

[This article is prerelease documentation and is subject to change.]

The performance of your Copilot is highly correlated to the quality of the knowledge sources it can access. You can enable customers to integrate various knowledge platforms without having to add the content directly into the Dynamics 365 knowledge base. The expanded Dynamics 365 knowledge base improves your Copilot's response quality, along with its experience and productivity.

> [!IMPORTANT]
>
> - This is a preview feature.
> - Preview features aren't meant for production use and might have restricted functionality. These features are available before an official release so that customers can get early access and provide feedback.

## Prerequisites

- You have the System Administrator role. 
- A license for  Microsoft Copilot Studio is available. 
- [Copilot in Customer Service is enabled](/dynamics365/customer-service/administer/configure-copilot-features#manage-copilot-features-in-customer-service).
- For SharePoint, Dataverse, or enterprise data using Microsoft Graph connectors, you must have the required authentication. Learn more in [source authentication](/microsoft-copilot-studio/knowledge-copilot-studio#source-authentication).

## Enable knowledge sources configured in Copilot Studio
 
1. In Copilot Service admin center, go to **Productivity** > **Copilot for questions and emails** > **Manage**. 
1. In the **Knowledge sources** section, select the **Use knowledge sources configured in Copilot Studio (preview)** option, which opens Copilot Studio. 
1. In Copilot Studio, select **Copilot in Dynamics 365 Customer Service**.
1. On the **Knowledge** page, select **Add knowledge**.
1. Select from the following knowledge sources:
    - [Public website](/microsoft-copilot-studio/knowledge-add-public-website)
    - [SharePoint](/microsoft-copilot-studio/knowledge-add-sharepoint)
    - [File upload](/microsoft-copilot-studio/knowledge-add-file-upload)
    - [Dataverse](/microsoft-copilot-studio/knowledge-add-dataverse)
    - [Enterprise data](/microsoft-copilot-studio/knowledge-graph-connections)
1. In Customer Service admin center, select **Save** or **Save and close**.
1. On the **Publish knowledge sources** dialog that appears, select **Publish**.

If you made any unpublished modifications to the Copilot plugins, you see a **Detected unpublished plugin** dialog. Select **Publish** if you're ready to publish the unpublished plugin changes. Learn more about plugins in [Enable plugins for generative AI (preview)](enable-copilot-plugins-for-generative-ai.md#enable-plugins-for-generative-ai-preview).

> [!NOTE]
> - Enterprise data that uses Copilot connectors as knowledge sources currently isn't supported. Instead, customers can optionally use Microsoft Graph connectors for their preferred sources.
> - Knowledge in Copilot Studio as a source only works with Ask a Question. Learn more in [Features supported with different knowledge sources](copilot-enable-help-pane.md#features-supported-with-different-knowledge-sources).

## Configure knowledge articles for verbatim responses in Copilot

In some scenarios, service representatives must share information with customers using approved, exact wording, such as legal text, regulatory guidance, or standardized procedures. To support these scenarios, Copilot can return verbatim responses from knowledge articles without rewriting or summarizing the content when service representatives use the **Ask a question** experience. Verbatim responses help ensure accuracy and compliance while allowing Copilot to assist service representatives efficiently during customer interactions.

Verbatim responses are controlled at the knowledge article level, not through Copilot settings. Knowledge managers configure which content must be returned verbatim by tagging knowledge articles or specific article sections.

### How verbatim responses work

The functionality for verbatim responses is as follows:

- Copilot evaluates the service representative's question and retrieves relevant knowledge articles.
- If the matching content is marked for verbatim use, Copilot returns the original wording from the knowledge article.
- The response includes a reference to the source article so that service representatives can review the full context.

Verbatim responses apply to the **Ask a question** capability. Other Copilot features, such as drafting emails or chat responses, continue to use standard response-generation behavior.

### Mark knowledge content for verbatim responses

Knowledge managers configure verbatim behavior by tagging knowledge content directly in the knowledge article editor.

**Mark an entire knowledge article as verbatim**

When the full article must always be returned without modification:

1. Open the knowledge article in the knowledge authoring experience.
1. Add the **doNotSummarize** keyword to the article.
1. Save and publish the article.

When Copilot retrieves this article, the content is returned verbatim, and a link to the article is included for reference.

**Mark specific sections of an article as verbatim**

When only part of an article must be returned verbatim, mark individual sections:

1. Open the knowledge article in the editor.
1. Select the subsection that must be returned verbatim.
1. Use the **verbatim** icon on the editor toolbar to add a verbatim comment to the selected content.
1. Save and publish the article.

Only the marked subsection is returned verbatim when Copilot retrieves the article. Other parts of the article continue to follow standard response behavior.

### Review verbatim responses

Service representatives can review the source of a verbatim response by selecting **Check sources** in the Copilot pane. The linked knowledge article opens in view-only mode, and verbatim content is highlighted so that representatives can easily identify text returned without modification. If multiple relevant knowledge articles are available, representatives can switch between sources to review alternate responses.

## Related information

[Knowledge sources overview](/microsoft-copilot-studio/knowledge-copilot-studio)
