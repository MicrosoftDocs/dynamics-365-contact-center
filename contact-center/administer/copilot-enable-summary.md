---
title: Enable summarization of cases and conversations
description: Learn how to enable summarization of cases and conversations using Copilot in Customer Service.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 01/13/2026
ms.update-cycle: 180-days
ms.custom: bap-template 
---

# Enable Copilot case and conversation summaries

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]

Copilot case and conversation summaries help you to quickly understand the context of a case and resolve customer issues more efficiently.

## Enable case summaries

[!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]

Case summaries help representatives understand the context of a case, enabling them to resolve customer issues efficiently. Agents get a concise summary of the case with the case title, customer, case subject, product, priority, case type, and case description. Email activity records, notes linked to a case, and conversation summaries are also used to generate the case summary.

> [!IMPORTANT]
> - A minimum of 50 [tokens](https://platform.openai.com/docs/introduction) are required to generate a case summary. 50 tokens translate to approximately 38 words in English, without counting spaces. Therefore, you'll need a minimum of 38 English words specified across the case fields that copilot uses to generate the case summary.
> - AI agent conversations aren't automatically included in the conversation summary.
 
1. In Copilot Service admin center, select **Ask a question** in **Copilot for questions and emails** for Copilot case summaries to be available.
1. Use one of the following navigation options: 
    - **Support Experience** > **Productivity** > **Summaries**
    - **Operations** > **Insights** > **Summaries**
1. Select **Manage** in **Summaries**.
1. Select **Make case summaries available to representatives** to display a summary of the case on the **Case** page. 
1. Select **Manage data** to [modify the source case fields that Copilot uses to generate case summaries](/dynamics365/customer-service/administer/copilot-map-custom-fields). 
1. Select **Specify information to exclude** to add email addresses and text that you want Copilot to exclude when generating responses. You can specify up to 10 email addresses and three disclaimers, headers, or footers within the email that you want Copilot to ignore. For example, you might not want to include automatic notification emails in your case summary. You can add the email address and Copilot won't use those emails to generate case summaries.<br>

Perform the steps in [Display case summary on custom case forms](/dynamics365/customer-service/administer/copilot-powerapps-settings) for the Copilot case summary to be displayed on custom case forms. 

## Enable conversation summaries

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

Conversation summaries enable service representatives to collaborate effectively with other service representatives and contacts, by enabling service representatives to easily recap an ongoing chat or a transcribed voice conversation.

For Copilot to automatically generate a conversation summary for a live conversation, in Copilot Service admin center, select the following options on the **Summaries** page:
   - **When a representative joins a conversation**: Generates a summary when a representative joins a conversation. A summary is also generated when the primary representative invites a collaborator and a second representative joins the conversation or when the primary representative transfers a conversation.
   - **When a conversation ends**: Generates a summary when the conversation ends. 
      - Select **Allow customer service representatives to create case with a button in the summary** to allow service representatives to see the **Create case** button in the conversation summary. A new case is created when the service representative selects **Create case**.
      - The conversation summary also appears for the closed conversation in the **Summary** tab of the conversation form. You can access this form for a closed conversation in Copilot Service workspace by selecting **Activities** and then filtering by **Conversations**.
   - **On demand, by selecting a button to summarize the conversation**: Generate a summary at any point in the conversation, whenever the service representative selects the copilot **Summarize conversation** in the conversation panel.
   - Select [**Manage format**](customize-copilot-conv-summary.md) to  the change the format in which the conversation summary is displayed to service representatives.

### Related information

[Use Copilot to summarize cases and conversations](../use/copilot-use-summary.md)  
[Enable features in Copilot pane](copilot-enable-help-pane.md)
