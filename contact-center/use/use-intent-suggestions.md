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

Intent-based suggestions help you handle customer conversations with ease. The intent agent analyzes your organization's historical support interactions to provide real-time context and intelligent guidance throughout the chat. You can quickly understand customer needs, ask the right questions, and deliver accurate solutions—all while reducing manual typing and handling time.

## Prerequisites

To use intent-based suggestions, you need the following features enabled by your administrator in Customer Service admin center or Contact Center admin center:
- The Ask-a-question feature in Copilot help pane. Learn more in [Enable Copilot assist features](../administer/copilot-enable-help-pane.md).
- Intent recognition. Learn more in [Manage customer intent agent](../administer/manage-customer-intent-agent.md).
- Intent-based suggestions for the relevant [agent experience profile](/dynamics365/customer-service/administer/create-agent-experience-profile). 


## How intent-based suggestions work

When you accept a live chat or persistent chat conversation, the application shows **Intent-based suggestions (preview)** in **Ask a question** in Copilot help pane. 

- The agent tries to map the conversation context to a specific intent or a general intent group based on your organization's data. You'll see one of the following:
   - The intent as the issue and relevant questions that you need to ask to resolve it.
   - The intent as the issue along with further questions to clarify it.
   - Nothing if the agent can't map the context to any known intent.
- If the customer's intent changes during a conversation, the agent detects the change and updates the suggestions based on the current intent. The agent also saves previous intents and suggested questions along with the conversation history. This way, if you transfer the conversation to another service representative, they can view historical intents and suggested questions.
  
### Use intent-based suggestions


You can do these actions in **Intent-based suggestions (preview)**:

- After you send a greeting message to the customer, the agent shows you the relevant questions in order and fills your chat text box with the current question. You can use the question as-is or edit it before sending it to the customer. 
- Optionally, you can hover over any question to fill the chat text box with that question. 
- If the customer answers the question, the agent marks it as answered and moves on to the next attribute. It shows a visual indicator next to each attribute along with the customer's response to show that you captured the relevant information.
 > [!NOTE]
 > If the customer answers a question before it is suggested, the agent recognizes that and moves on to the next attribute without asking it again.
- Select **Request Solution** after you have all the information required to resolve the issue. The agent retrieves information from your organization's knowledge base and shows it in **Ask a question**, only if there's no existing ongoing conversation in that pane.
- Select **Follow-up suggestions** to see historical intents and suggested questions for this conversation, and how customers responded.
- Select **thumbs-down button** if the agent incorrectly identified the issue. It stops showing that issue and disables the suggested questions.




