---
title: Use intent-based suggestions
description: Learn how to use intent-based suggestions in Customer Service admin center or Contact Center admin center to help customer service representatives handle customer conversations with ease.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: 
ms.date: 11/13/2024
ms.custom: bap-template 
---


# Use intent-based suggestions

Intent based suggestions helps customer service representatives (CSRs) handle customer conversations with ease. The intent agent analyzes your organization's historical support interactions to provide real-time context and intelligent guidance throughout the chat, enabling service representatives to quickly understand customer needs, ask the right questions, and deliver accurate solutions—all while reducing manual typing and handling time.

## Prerequisites

Make sure that your administrator has enabled the following in Customer Service admin center or Contact Center admin center:
- [Copilot help pane](/dynamics365/customer-service/administer/copilot-enable-help-pane).
- Intent discovery.
- Intent management for the required [agent experience profile](/dynamics365/customer-service/administer/create-agent-experience-profile). 

## How intent-based suggestions work

When you accept a live chat or persistent chat conversation, the application shows **Intent-based suggestions (preview)** in **Ask a question** in Copilot help pane. The intent shows the following based on whether the agent maps the context of the conversation to a specific intent, a general intent group, or none: 

- When the agent maps the context of the conversation to a specific intent, it shows the intent as the issue. When you expand this card, it shows the intent attributes linked to the intent as questions. Intent attributes are the relevant information that you need to resolve the issue.
   
 For example, the agent maps the customer's issue to the intent “Returning Contoso CX300 coffee machine”. This intent has these intent attributes:
  -	Date of purchase
  -	Order number
  -	Return reason

 The agent then suggests questions related to these attributes, such as “When did you buy the coffee machine?” and “What is your order number?” that you can use to gather the necessary information to resolve the issue.

- When the agent maps the context of the conversation to a general intent group but not to a specific intent, it shows the intent along with a follow-up question to clarify the intent. 
    For example, the agent maps the customer's issue to the intent group, “Coffee machine issues”. It then suggests questions to gather more information to resolve the issue, such as “What kind of coffee machine issue do you have?”

- When the agent can't map the context of the conversation to a known intent group or intent, it shows nothing.
- If a customer's intent changes during a conversation, it detects change in intent and updates the suggestions based on the current intent. It saves previous intents and suggested questions with conversation history. So even if you transfer conversation to another service representative, they can view historical intents and suggested questions.
  
### Use intent-based suggestions

You can do these actions in **Intent-based suggestions (preview)**:

- After you've sent a greeting message to customer, it shows relevant questions in order. It also fills chat text box with question. You can use question as-is or edit it before sending it to customer. 
- Optionally, you can hover over any question to fill chat text box with that question. 
- If customer answers question, it marks question as answered and moves on to next attribute. It shows a visual indicator next to attribute to show that you have captured relevant information.
 > [!NOTE]
 > If customer answers question before it suggests it, it recognizes that question has been answered and moves on to next attribute and doesn't ask question again.
- Select **Request Solution** after you've asked all questions and have information required to resolve issue. It retrieves information from your organization's knowledge base and shows solution in **Ask a question**.
- Select **Follow-up suggestions** to see historical intents and suggested questions for conversation, and customer’s responses.
- Select **thumbs-down button** if it has incorrectly identified issue. It stops showing issue and disables suggested questions.



