---
title: Enable intent-based suggestions for service representatives
description: Enable intent-based suggestions in Customer Service admin center or Contact Center admin center to help customer service representatives handle customer conversations with ease.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/13/2024
ms.custom: bap-template 
---

# Enable intent-based suggestions for service representatives

Intent-based suggestions help customer service representatives (service representatives or representatives)  resolve live chat and persistent chat issues faster and more accurately. For service representatives to use this feature, you need to enable **Intent-based suggestions (preview)** in agent experience profiles. By default, representatives added to the out-of-the-box agent experience profiles can use the intent-based suggestions.

## Prerequisites

- The Ask-a-question feature in Copilot help pane is enabled. Learn more in [Enable Copilot assist features](copilot-enable-help-pane.md).


## Enable intent-based suggestions

You can create a custom agent experience profile and enable the required features to limit the features representatives can use. You can then assign the custom profile to the representatives.

To add the Copilot features to an agent experience profile, follow these steps:

1. Go to Agent experience profiles using one of the following navigation options:
   - **Agent experience** > **Workspaces**
   - **Intent > Agent access** > **Customer Intent Agent (preview)** > **Enable for support representatives**
1. Select the required agent experience profile.
1. In **Productivity pane**, select **Edit** and then turn on the **Copilot** toggle.
1. In **Copilot AI features** select **Edit** and then select the following for the representatives to be able to view intent-based suggestions:
     1. **Ask a question**
     1. **Intent-based suggestions (preview)**
1. In the **Copilot AI features** section, select edit and then select the required **Intent-based suggestions(preview)**.

## How intent-based suggestions work

When a service representative accepts a live chat or persistent chat conversation, Copilot shows **Intent-based suggestions (preview)** in **Ask a question**. The suggestions depend on whether Copilot can map the conversation context to a specific intent, a general intent group, or no known intent.

- If the intent agent maps the context to a specific intent, it shows the intent as the issue. When you expand the card, it shows the intent attributes as questions. Intent attributes are the relevant information that you need to resolve the issue.
   
  For example, the agent maps the customer's issue to the intent "Returning Contoso CX300 coffee machine". This intent has these intent attributes:
    -	Date of purchase
    -	Order number
    -	Return reason

  You can use the questions that the agent suggests for these attributes, such as “When did you buy the coffee machine?” and “What is your order number?” to get the necessary information from the customer.

- If the agent maps the context to a general intent group but not a specific intent, it shows the intent group and a follow-up question to clarify the intent. 

   For example, the agent maps the customer's issue to the intent group "Coffee machine issues". To narrow down the intent, it suggests a question that you can ask the customer for more information, such as “What kind of coffee machine issue do you have?”

- If the agent can't map the context to any known intent group or intent, it shows nothing.
- If a customer's intent changes during a conversation, the agent detects the change and updates the suggestions based on the current intent. It also saves the previous intents and suggested questions with the conversation history. This way, if you transfer the conversation to another rep, they can see the historical intents and suggested questions.