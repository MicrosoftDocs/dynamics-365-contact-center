---
title: Enable knowledge sources from Microsoft Copilot Studio (preview)
description: Learn how to enable knowledge sources from Microsoft Copilot Studio.
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days 
ms.date: 03/31/2026
ms.custom: bap-template
---

# Configure knowledge articles for verbatim responses in Copilot

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

[This article is prerelease documentation and is subject to change.]

In some scenarios, service representatives must share information with customers using approved, exact wording, such as legal text, regulatory guidance, or standardized procedures. To support these scenarios, Copilot can return verbatim responses from knowledge articles without rewriting or summarizing the content when service representatives use the **Ask a question** experience. Verbatim responses help ensure accuracy and compliance while allowing Copilot to assist service representatives efficiently during customer interactions.

> [!IMPORTANT]
>
> - This is a preview feature.
> - Preview features aren't meant for production use and might have restricted functionality. These features are available before an official release so that customers can get early access and provide feedback.

## How verbatim responses work

The functionality for verbatim responses is as follows:

- Copilot evaluates the service representative's question and retrieves relevant knowledge articles.
- If the matching content is marked for verbatim use, Copilot returns the original wording from the knowledge article.
- The response includes a reference to the source article so that service representatives can review the full context.

Verbatim responses apply to the **Ask a question** capability. Other Copilot features, such as drafting emails or chat responses, continue to use standard response-generation behavior.

## Mark knowledge content for verbatim responses

Verbatim responses are controlled at the knowledge article level, not through Copilot settings. Knowledge managers can configure verbatim behavior by tagging knowledge content directly in the knowledge article editor. 

You can mark an entire article or specific sections as verbatim.

### Mark an entire knowledge article as verbatim

When the full article must always be returned without modification:

1. Open the knowledge article in the knowledge authoring experience.
1. Add the **doNotSummarize** keyword to the article.
1. Save and publish the article.

When Copilot retrieves this article, the content is returned verbatim, and a link to the article is included for reference.

### Mark specific sections of an article as verbatim

When only part of an article must be returned verbatim, mark individual sections:

1. Open the knowledge article in the editor.
1. Select the subsection that must be returned verbatim.
1. Use the **Verbatim** icon on the editor toolbar to add a verbatim comment to the selected content.
1. Save and publish the article.

Only the marked subsection is returned verbatim when Copilot retrieves the article. Other parts of the article continue to follow standard response behavior.

## Review verbatim responses

Service representatives can review the source of a verbatim response by selecting **Check sources** in the Copilot pane. The linked knowledge article opens in view-only mode, and verbatim content is highlighted so that representatives can easily identify text returned without modification. If multiple relevant knowledge articles are available, representatives can switch between sources to review alternate responses.

## Related information

[Knowledge sources overview](/microsoft-copilot-studio/knowledge-copilot-studio)  
[Enable knowledge sources from Microsoft Copilot Studio (preview)](knowledge-copilot.md)
