---
title: Configure knowledge articles for verbatim responses in Copilot (preview)
description: Learn how to mark entire knowledge articles or specific sections of knowledge articles so Microsoft Copilot can return verbatim responses.
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days 
ms.date: 04/21/2026
ms.custom: bap-template
---

# Configure knowledge articles for verbatim responses in Copilot (preview)

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

[This article is prerelease documentation and is subject to change.]

Customer service representatives (service representatives or representatives) must sometimes share information using approved, exact wording for legal text, regulatory guidance, or standardized procedures. To support these scenarios, Copilot can return verbatim responses from knowledge articles without rewriting or summarizing the content when representatives use the **Ask a question** experience. Use verbatim responses to maintain accuracy and compliance while Copilot efficiently supports customer interactions.

> [!IMPORTANT]
>
> - This is a preview feature.
> - Preview features aren't meant for production use and might have restricted functionality. These features are available before an official release so that customers can get early access and provide feedback.

## How verbatim responses work

Verbatim responses work as follows:

- Copilot evaluates the service representative's question and retrieves relevant knowledge articles.
- If the matching content is marked for verbatim use, Copilot returns the original wording from the knowledge article.
- The response includes a reference to the source article so that service representatives can review the full context.

Verbatim responses apply to the **Ask a question** capability. Other Copilot features, such as drafting emails or chat responses, continue to use standard response-generation behavior.

## Mark knowledge content for verbatim responses

Verbatim responses are controlled at the knowledge article level, not through Copilot settings. Knowledge managers can configure verbatim behavior by tagging knowledge content directly in the knowledge article editor. 

You can mark an entire article or specific sections as verbatim.

### Mark an entire knowledge article as verbatim

For articles that must be delivered verbatim in full:

1. In **Copilot Service workspace**, go to **Service** > **Knowledge Articles**.
1. Either open an existing article or select **New** to create one.
1. Add the **doNotSummarize** keyword in the article content.
1. Save and publish the article.

When Copilot retrieves this article, the content is returned verbatim, and a link to the article is included for reference.

### Mark specific sections of an article as verbatim

Mark individual sections when only specific parts require verbatim responses.

1. In **Copilot Service workspace**, go to **Service** > **Knowledge Articles**.
1. Either open an existing article or select **New** to create one.
1. Select the subsection that must be returned verbatim.
1. Use the **Verbatim** icon to add a verbatim comment to the selected content.
1. Save and publish the article.

Only the marked subsection is returned verbatim when Copilot retrieves the article. Other parts of the article continue to follow standard response behavior.

## Review verbatim responses

Service representatives can review the source of a verbatim response by selecting **Check sources** in the Copilot pane. The linked knowledge article opens in view-only mode, and verbatim content is highlighted so that representatives can easily identify text returned without modification. If multiple relevant knowledge articles are available, representatives can switch between sources to review alternate responses.

## Related information

[Knowledge sources overview](/microsoft-copilot-studio/knowledge-copilot-studio)  
[Enable knowledge sources from Microsoft Copilot Studio (preview)](knowledge-copilot.md)
