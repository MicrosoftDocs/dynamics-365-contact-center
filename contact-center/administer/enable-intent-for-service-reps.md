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

For agents to be able to use intent-based suggestions for live chat and persistent conversations, you need to enable **Intent-based suggestions (preview)** in agent experience profiles. By default, agents added to the out-of-the-box agent experience profiles can use the intent-based suggestions.

## Prerequisites

Make sure that your administrator enabled the Ask-a-question feature in Copilot help pane. Learn more in [Enable Copilot assist features](copilot-enable-help-pane.md).


## Enable intent-based suggestions

You can create a custom agent experience profile and enable the required features to limit the features agents can use. You can then assign the custom profile to the agents.

Perform the following steps to add the Copilot features to an agent experience profile:

1. Go to Agent experience profiles using one of the following navigation options:
   - **Agent experience** > **Workspaces**
   - **Intent > Agent access** > **Customer Intent Agent (preview)** > **Enable for support representatives**
1. Select the required agent experience profile.
1. On the Productivity Pane, turn on the **Copilot help pane** toggle so that agents can use the ask-a-question feature.
1. In the **Copilot AI features** section, select edit and then select the required **Intent-based suggestions(preview)**.


## How intent-based suggestions work

When you accept a live chat or persistent chat conversation, the application shows **Intent-based suggestions (preview)** in **Ask a question** in Copilot help pane. The intent shows the following based on whether the agent maps the conversation context to a specific intent, a general intent group, or can't map it to any known intent.

- When the agent maps the context of the conversation to a specific intent, the intent is displayed as the issue. When a customer service representative expands this card, the intent attributes linked to the intent are displayed as questions. Intent attributes are the relevant information that the service representatives need to resolve the issue.
   
  For example, the agent maps the customer's issue to the intent "Returning Contoso CX300 coffee machine". This intent has the following intent attributes:
    -	Date of purchase
    -	Order number
    -	Return reason

  Service representative can use the questions suggested by the agent that are related to these attributes, such as “When did you buy the coffee machine?” and “What is your order number?” to gather the necessary information to resolve the issue.

- When the agent maps the context of the conversation to a general intent group but not to a specific intent, the agent shows the intent along with a follow-up questions to clarify the intent. 

   For example, the agent maps the customer's issue to the intent group, “Coffee machine issues”. To narrow down the intent, the agent then suggests questions the service representative can ask the customer to gather more information to resolve the issue, such as “What kind of coffee machine issue do you have?”

- When the agent can't map the context of the conversation to a known intent group or intent, it shows nothing.
- When a customer's intent changes during a conversation, the agent detects change in intent and updates the suggestions based on the current intent. It saves previous intents and suggested questions with conversation history. So even if you transfer conversation to another service representative, they can view historical intents and suggested questions.
  