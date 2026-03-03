---
title: Use intent-based suggestions
description: Learn how to use intent-based suggestions to help customer service representatives handle customer conversations with ease in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 01/13/2026
ms.custom: bap-template 
---


# Use intent-based suggestions

Intent-based suggestions help you handle customer conversations with ease. The intent agent analyzes your organization's historical support interactions to provide real-time context and intelligent guidance throughout the chat. You can quickly understand customer needs, ask the right questions, and deliver accurate solutions—all while reducing manual typing and handling time.

## Prerequisites

To use intent-based suggestions, you need the following features enabled by your administrator in Copilot Service admin center:

- Customer Intent Agent is enabled. Learn more in [Manage Customer Intent Agent](../administer/manage-customer-intent-agent.md)
- The Ask-a-question feature in Copilot help pane is enabled. Learn more in [Enable Copilot assist features](../administer/copilot-enable-help-pane.md).
  
## Use intent-based suggestions

You can do the following actions in **Intent-based suggestions**:

- View the intent identified by the agent. The agent tries to map the conversation context to a specific intent or a general intent group based on your organization's data. You see one of the following suggestions:
   - "Looking for suggestions", when the agent is mapping the context to an intent.
   - The intent as the issue and relevant questions that you need to ask to resolve the issue.
   - The intent group as the issue along with further questions to clarify the issue.
   - Nothing, if the agent can't map the context to any known intent.
   > [!NOTE]
   > When active conversations aren't there, the agent displays the "Suggestions unavailable" message on the card.
- Select **Tab** to populate the current question in your chat text box. You can send the question as-is or edit the text before you send it to the customer. 
- Optionally, you can hover over any question and then select **Send to conversation** to fill the chat text box with the question. 
- View a visual indicator against each question the customer answers. The customer's responses also appear with the question. If the customer answers the question, the agent marks it as answered and moves on to the next question. 
  > [!NOTE]
  > If the customer answers a question before the agent suggests a question, the agent recognizes that the question is answered and moves on to the next question.
- Select **Request Solution** after you have all the information required to resolve the issue. The agent retrieves information from your organization's knowledge base and shows it in **Ask a question**, only when there's no existing ongoing conversation in the pane.
- Expand the **Intent-based suggestions** header to see all the historical intents identified for a conversation. Select a historical intent to view the suggested questions and the customer's response.  
  If the customer's intent changes during a conversation, the agent detects the change and updates the suggestions based on the current intent. The agent also saves previous intents and suggested questions along with the conversation history. This way, if you transfer the conversation to another service representative, they can view historical intents and suggested questions.
- Select **thumbs-down button** if the agent incorrectly identified the issue. It stops showing that issue and disables the suggested questions.

   :::image type="content" source="../media/intent-mgmt-agent-experience-mini.png" alt-text="Screenshot of the structured settings for conversation summary" lightbox="../media/intent-mgmt-agent-experience.png":::|

## Related information

[Enable intent-based suggestions for service representatives](../administer/enable-intent-for-service-reps.md)