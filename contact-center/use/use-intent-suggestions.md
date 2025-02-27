---
title: Use intent-based suggestions
description: Learn how to use intent-based suggestions to help customer service representatives handle customer conversations with ease.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: 
ms.date: 11/13/2024
ms.custom: bap-template 
---


# Use intent-based suggestions

Intent based suggestions help customer service representatives (CSRs) handle customer conversations with ease. The intent agent analyzes your organization's historical support interactions to provide real-time context and intelligent guidance throughout the chat, enabling service representatives to quickly understand customer needs, ask the right questions, and deliver accurate solutions—all while reducing manual typing and handling time.

## Prerequisites

Make sure that your administrator enabled the following features in Customer Service admin center or Contact Center admin center:
- The Ask-a-question feature in Copilot help pane. Learn more in [Enable Copilot assist features](../administer/copilot-enable-help-pane.md).
- Intent discovery.
- Intent-based suggestions for the required [agent experience profile](/dynamics365/customer-service/administer/create-agent-experience-profile). 

## How intent-based suggestions work

When you accept a live chat or persistent chat conversation, the application shows **Intent-based suggestions (preview)** in **Ask a question** in Copilot help pane. 

- Based on whether the agent maps the conversation context to a specific intent, a general intent group, or can't map it to any known intent, you'll see the following:
   - Intent as the issue and relevant questions that you need to resolve the issue
   - Intent as the issue along with further questions to clarify the intent
   - Nothing is displayed 
- If a customer's intent changes during a conversation, the agent detects the change in intent and updates the suggestions based on the current intent. The agent saves previous intents and suggested questions along with the conversation history. So even if you transfer conversation to another service representative, they can view historical intents and suggested questions.
  
### Use intent-based suggestions

You can do these actions in **Intent-based suggestions (preview)**:

- After you send a greeting message to the customer, the relevant questions are displayed in order. The agent also fills your chat text box with the current question. You can use question as-is or edit it before sending it to customer. 
- Optionally, you can hover over any question to fill the chat text box with the specific question. 
- If the customer answers the question, the agent marks the question as answered and moves on to next attribute. It shows a visual indicator next to attribute along with the customer's response to show that you captured the relevant information.
 > [!NOTE]
 > If customer answers question before it suggests it, it recognizes that question has been answered and moves on to next attribute and doesn't ask question again.
- Select **Request Solution** after you think you have all the information required to resolve the issue. The agent retrieves information from your organization's knowledge base and shows the solution in **Ask a question**, only if there's no existing ongoing conversation in the Ask a question pane.
- Select **Follow-up suggestions** to see historical intents and suggested questions for conversation, and customer’s responses.
- Select **thumbs-down button** if the agent incorrectly identified the issue. It stops showing issue and disables suggested questions.



:::image type="content" source="../media/intent-mgmt-agent-experience-mini.png" alt-text="Screenshot of the structured settings for conversation summary" lightbox="../media/intent-mgmt-agent-experience.png":::|