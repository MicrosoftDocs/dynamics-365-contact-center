---
title: Enable summarization of cases and conversations
description: Learn how to enable summarization of cases and conversations using Copilot in Customer Service.
author: gandhamm
ms.author: mgandham
ms.reviewer: neeranelli
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 07/01/2024
ms.custom: bap-template 
---

# Enable Copilot case and conversation summaries

Copilot case and conversation summaries help you to quickly understand the context of a case and resolve customer issues more efficiently.

> [!NOTE]
> The feature availability information is as follows.
>
> |Feature| Dynamics 365 Contact Center&mdash;embedded | Dynamics 365 Contact Center&mdash;standalone | 
> |--------------|----------|----------|
> | Case Summary | No  | Yes   |
> | Conversation Summary | Yes   | Yes   | 

## Enable case summaries

Case summaries help agents understand the context of a case, enabling them to resolve customer issues efficiently. Agents get a concise summary of the case based on their CRM as follows:

- Salesforce: case id, description, subject, priority, type, customer name, case url, email, and text post activities linked to the case.
- ServiceNow: incident id, description, short description, priority, type, customer name, incident url, email, and notes linked to the incident.

> [!IMPORTANT]
> - Copilot case summary is available in the Contact Center standalone app only.
> - A minimum of 50 [tokens](https://platform.openai.com/docs/introduction) are required to generate a case summary. 50 tokens translate to approximately 38 words in English, without counting spaces. Therefore, you'll need a minimum of 38 English words specified across the case fields that copilot uses to generate the case summary.
> - Bot conversations aren't automatically included in the conversation summary.
 
1. In Contact Center admin center, use one of the following navigation options: 
    - **Agent Experience** > **Productivity** > **Summaries**
    - **Operations** > **Insights** > **Summaries**
1. Select **Manage** in **Summaries**.
1. Select **Make case summaries available to agents** to display a summary of the case on the **Case** page. 
1. If you want Copilot to exclude emails from specific email addresses when generating responses, select **Add email address**. You can specify up to 10 email addresses. For example, you might not want to include automatic notification emails in your case summary. You can add the email address and Copilot won't use those emails to generate case summaries.

## Enable conversation summaries

Conversation summaries enable agents to collaborate effectively with other agents and contacts, by enabling agents to easily recap an ongoing chat or a transcribed voice conversation.

For Copilot to automatically generate a conversation summary for a live conversation, in Contact Center admin center, select the following options on the **Summaries** page:
   - **When an agent joins a conversation**: Generates a summary when an agent joins a conversation. A summary is also generated when the primary agent invites a collaborator and a second agent joins the conversation or when the primary agent transfers a conversation.
   - **When a conversation ends**: Generates a summary when the conversation ends. 
      - Select **Allow agents to create case with a button in the summary** to allow agents to see the **Create case** button in the conversation summary. A new case is created when the agent selects **Create case**.
   - **On demand, by selecting a button to summarize the conversation**: Generate a summary at any point in the conversation, whenever the agent selects the copilot **Summarize conversation** in the conversation panel.

## Enable translation

Copilot can translate case and conversation summaries to the agent's preferred language. To enable translation, in the Contact Center admin center, select **Let agents translate responses**. Agents can select the **Translate** button to translate the summary to their preferred language.

### See also

[Use Copilot to summarize cases and conversations](../use/copilot-use-summary.md)<br>
[Enable features in Copilot pane](copilot-enable-help-pane.md)
