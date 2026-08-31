---
title: Enable Copilot case and conversation summaries
description: Learn how to enable Copilot case and conversation summaries for service representatives.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 08/27/2026
ms.update-cycle: 180-days
ms.custom: bap-template 
---

# Enable Copilot case and conversation summaries

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]

Copilot case and conversation summaries help service representatives quickly understand case and conversation context.

## Enable case summaries

[!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]

Case summaries help representatives understand the context of a case. Representatives get a concise summary that includes the case title, customer, case subject, product, priority, case type, and case description. Copilot also uses email activity records, notes linked to the case, and conversation summaries.

> [!IMPORTANT]
> - A minimum of 50 [tokens](https://platform.openai.com/docs/introduction) are required to generate a case summary. Fifty tokens translate to approximately 38 English words, excluding spaces. Specify at least 38 English words across the case fields that Copilot uses to generate the summary.
> - AI agent conversations aren't automatically included in the conversation summary.

In Copilot Service admin center:

1. In **Copilot for questions and emails**, turn on **Ask a question**.
1. Use one of the following navigation options: 
    - **Support Experience** > **Productivity** > **Summaries**
    - **Operations** > **Insights** > **Summaries**
1. Select **Manage** in **Summaries**.
1. Select **Make case summaries available to representatives** to display a summary of the case on the **Case** page. 
1. Select **Manage data** to [modify the source case fields that Copilot uses to generate case summaries](/dynamics365/customer-service/administer/copilot-map-custom-fields). 
1. Select **Specify information to exclude** to add email addresses and text that you want Copilot to exclude when generating responses. You can specify up to 10 email addresses and three disclaimers, headers, or footers within the email that you want Copilot to ignore. For example, add the sender address for automatic notification emails so Copilot doesn't use those emails to generate case summaries.

Perform the steps in [Display case summary on custom case forms](/dynamics365/customer-service/administer/copilot-powerapps-settings) for the Copilot case summary to be displayed on custom case forms. 

## Enable conversation summaries

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

Conversation summaries help service representatives recap an ongoing chat or a transcribed voice conversation when they collaborate with other representatives and contacts.

On the **Summaries** page in Copilot Service admin center, select the options that apply:
   - **When a representative joins a conversation**: Generates a summary when a representative joins a conversation. A summary is also generated when the primary representative invites a collaborator and a second representative joins the conversation or when the primary representative transfers a conversation.
   - **When a conversation ends**: Generates a summary when the conversation ends. 
      - Select **Allow customer service representatives to create case with a button in the summary** to allow service representatives to see the **Create case** button in the conversation summary. A new case is created when the service representative selects **Create case**.
      - The conversation summary also appears for the closed conversation in the **Summary** tab of the conversation form. You can access this form for a closed conversation in Copilot Service workspace by selecting **Activities** and then filtering by **Conversations**.
   - **On demand, by selecting a button to summarize the conversation**: Generates a summary whenever a service representative selects **Summarize conversation** in the conversation panel.
   - Select [**Manage format**](customize-copilot-conv-summary.md) to change how the conversation summary appears to service representatives.

### Related information

[Use Copilot to summarize cases and conversations](../use/copilot-use-summary.md)  
[Enable features in Copilot pane](copilot-enable-help-pane.md)
