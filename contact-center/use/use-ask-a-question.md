---
title: Ask a question
description: Learn how to use ask a question feature in Copilot within customer service representative apps to enhance efficiency.
author: gandhamm
ms.author: mgandham
ms.reviewer: 
ms.topic: how-to
ms.collection:
ms.date: 07/14/2025
ms.custom: bap-template 
---

# Ask a question 

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability.md)]


[!INCLUDE [cc-ask-question-intro](../../shared/cc-ask-question-intro.md)]

> [!IMPORTANT]
> The AI-generated content is a suggestion. It's your responsibility to review and edit the suggested content to make sure it's accurate and appropriate before sharing the responses.

## Prerequisites

- Make sure that your administrator has turned on the Copilot features.
- To use the summarize cases feature, [case summaries through ask a question](/dynamics365/customer-service/administer/enable-ask-summarize-cases) is enabled.


## Draft questions

[!INCLUDE[cc-ask-question-draft-question](../../shared/cc-ask-question-draft-question.md)]

 :::image type="content" source="../media/copilot-ask-question.png" alt-text="Screenshot of the Ask a question tab in Copilot.":::

## Summarize cases and ask about case data

Based on the app, you're using, you can use Copilot to generate case summary and ask about case data from the **Ask a question** tab.

> [!IMPORTANT]
> Case summaries and case data are available only if case management is available. If you are using the Customer Service Hub app, you can use Copilot to ask questions about cases, but not to summarize them.

 In Copilot Service workspace, Copilot enables you to:

- **Ask to summarize cases** (preview): Copilot generates case summaries directly within the Ask a question tab, allowing you to access them without disrupting your current workflow. The case summary includes key information such as the case title, customer, priority, case type, and description.
- **Ask about case data** (preview): Copilot enables you to access and use case data effectively, resulting in improved case management. You can ask questions about your case data to manage case workload in a better way.

You can make the following types of requests:

- Get details on the high-priority cases for a specified date range.
- Show all high-priority cases.
- Show active escalated cases.
- Show cases that are due soon.
- Show cases due the next day.
- Show active cases that service representatives own.
- Show my active cases.
- Get the case details.
- Get the case resolution details for a case.
- Show cases for owner {owner name}.
- Show case history.

## Use auto prompts

[!INCLUDE [cc-ask-question-autoprompt](../../shared/cc-ask-question-autoprompt.md)]

## Use proactive prompts

[!INCLUDE [cc-ask-question-proprompt](../../shared/cc-ask-question-proprompt.md)]

  :::image type="content" source="../media/proactive-prompting.png" alt-text="Screenshot shows options in proactive prompting.":::

## Use targeted phrases in Copilot to get responses from plugins (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

[!INCLUDE [cc-ask-question-copilotprompt](../../shared/cc-use-ask-copilotprompt.md)]


 :::image type="content" source="../media/screenshot-of-prompt-plugin-response-in-copilot.png" alt-text="A screenshot of the Copilot response generated through the prompt plugin.":::

## Use the responses

[!INCLUDE [cc-ask-question-responses](../../shared/cc-ask-question-responses.md)]

## Review responses from knowledge articles (preview)

> [!IMPORTANT]
>
> - This is a preview feature.
> - Preview features aren't meant for production use and might have restricted functionality. These features are available before an official release so that customers can get early access and provide feedback.

When Copilot answers a question using knowledge content, the response might be returned directly from a knowledge article.

If the knowledge content is configured to be returned verbatim, Copilot displays the approved wording without rewriting or summarizing it. This behavior helps ensure accuracy and compliance when exact language is required.

When a verbatim response is returned:

- The response indicates that the information is provided directly from a knowledge document.
- The content isn’t rewritten or summarized.
- The most relevant section of the knowledge article is surfaced automatically.

To review the full source content, select **Check sources** in the Copilot pane. The linked knowledge article opens in view-only mode, and the content used in the response is highlighted so that you can easily identify it.

If multiple knowledge articles are available, you can use the source navigation controls to switch between articles and review alternate responses.

Always review Copilot responses before sharing them with customers, especially when the response is based on knowledge content.

## Translate responses

[!INCLUDE [cc-use-translate-responses](../../shared/cc-use-translate-responses.md)]

## Related information

[Enable features in Copilot pane](../administer/copilot-enable-help-pane.md)

