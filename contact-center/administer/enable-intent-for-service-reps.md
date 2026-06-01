---
title: Enable intent-based suggestions for service representatives
description: Learn how to enable intent-based suggestions in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 06/01/2026
ms.update-cycle: 180-days
ms.custom: bap-template 
---

# Enable intent-based suggestions for service representatives

Intent-based suggestions and next best actions help customer service representatives (service representatives or representatives) handle customer interactions efficiently by combining real-time guidance with actionable recommendations.  

Intent-based suggestions use AI to analyze customer conversations during live chats and calls. Based on the detected intent, the autonomous agent suggests relevant questions that help service representatives gather the information needed to understand and resolve the issue.    
Next best actions extend this experience into the case workflow. After a case is created or updated, the agent analyzes the case context and recommends appropriate next steps. These actions help service representatives review generated responses, follow up with customers, reuse content, or resolve the case without manually determining the next course of action.  

Enable intent-based suggestions in experience profiles for service representatives to use them.

## Prerequisites

Before setting up the autonomous agent, ensure the following configurations are in place. If these prerequisites aren't already set up, they are automatically configured when you enable and save the settings on the **Intent-based suggestions** page:

  - [Intent](manage-customer-intent-agent.md) or knowledge management is configured.
    > [!NOTE]
    > Knowledge management isn't set up automatically when the page is saved.
  - The Ask-a-question feature in Copilot help pane is enabled. Learn more in [Enable Copilot assist features](copilot-enable-help-pane.md). 
 
- Optionally, you can configure connectors for the agent to retrieve relevant information from external knowledge sources. Learn more in [Manage custom connectors](manage-customer-intent-agent.md#manage-connectors-for-ai-agents-optional) 

## Enable intent-based suggestions and next best actions

To enable intent-based suggestions and next best actions, complete the following steps in Copilot Service admin center:

1. Select **Productivity** in **Support experience**. The **Productivity** page appears.
1. Select **Manage** for **Intent-based suggestions**. The **Intent-based suggestions** page appears.
1. In the **Turn on intent-based suggestions** section, select the following options:

   - **Conversation content**
   - **Actions**: Select to enable next best actions for cases, such as drafting emails or resolving the case.
1. In **Enable in experience profiles**, select **Select experience profiles**.
     1. On **Select experience profiles**, select the experience profiles. 
     1. Select **Save**.
> [!NOTE]
> If you turn off intent-based suggestion or remove it from an experience profile, it doesn't revert the Copilot or other shared settings.

   :::image type="content" source="../media/intent-based-suggestions.png" alt-text="Screenshot for intent based suggestions admin UI.":::


## How intent-based suggestions work

When a service representative accepts a live chat or persistent chat conversation, the **Intent-based suggestions** card appears in the **Ask a question** tab of Copilot help pane.

The autonomous agent maps the context of the conversation to a specific intent and displays the relevant intent attributes as questions. The service representative can use these questions to get the necessary information from the customer to resolve the issue.

For example, the agent maps the customer's issue to the intent "Returning Contoso CX300 coffee machine". This intent has the following intent attributes:

- Date of purchase
- Order number
- Return reason

Service representatives can use the questions that the agent suggests for these attributes, such as "When did you buy the coffee machine?" and "What is your order number?" to get the necessary information from the customer.

When the agent maps the context to a general intent group but not a specific intent, the service representative sees only the high level intent and a follow-up question to clarify the intent. 

For example, the agent maps the customer's issue to the intent group "Coffee machine issues". To narrow down the intent, it suggests a question that the representative can ask the customer for more information, such as "What kind of coffee machine issue do you have?"

If the agent can't map the context to any known intent group or intent, it shows nothing.

If a customer's intent changes during a conversation, the agent detects the change and updates the suggestions based on the current intent. It also saves the previous intents and suggested questions with the conversation history.

## How next best actions work

For a case, the autonomous agent analyzes case data such as emails and notes and maps the customer's issue to the available intents.

For example, a service representative creates or updates a case for a customer who wants to return a Contoso CX300 coffee machine. 

Based on the case context, the agent evaluates the information and suggests next best actions in the Copilot pane.
For this scenario, the autonomous agent might recommend the following actions:

- Follow up with the customer if additional confirmation is required
- Review draft of a response generated for the customer
- Resolve the case after confirming the return request is completed

## Next steps

 [Use intent-based suggestions](../use/use-intent-suggestions.md)