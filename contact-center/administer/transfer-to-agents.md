---
title: Transfer conversations from customer service representatives to bots
description: Learn how a customer service representative can transfer a conversation back to a bot.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: conceptual
ms.collection:
ms.date: 11/15/2024
ms.custom:
  - bap-template
  - ai-gen-docs-bap
  - ai-gen-title
  - ai-seo-date:11/11/2024
---

# Transfer conversations from customer service representatives to bots

In some support scenarios, a customer service representative may need to transfer a conversation back to a Copilot Studio bot after providing personalized support. This transfer can help with basic, repetitive tasks or collect additional data, such as in a customer survey.

You can facilitate the transfer of a conversation from a human agent back to a bot in the following ways:

- Create two bots that reside in two queues
- Create two bots that reside in the same queue

### Two bots in two queues

In this scenario, a bot has transferred a conversation to a human agent. The human agent will transfer the conversation again to another bot in another queue.

1. A customer starts a conversation.
2. The conversation is routed to Queue 1.
3. The first bot (Bot A) accepts the conversation.
4. The customer requests to chat with a human agent.
5. The conversation is transferred to a human agent within Queue 1.
6. The customer converses with the human agent.
7. The human agent has completed delivering support and wants to hand off the conversation to a second bot (Bot B), which resides in Queue 2.
8. The human agent is disconnected from the conversation.
9. The conversation routed to Bot B in Queue 2.
10. The system triggers Bot B to send a greeting message.
11. The customer now chats with Bot B.

### Two bots in one queue

In this scenario, after a bot has transferred a conversation to a human agent, the agent will transfer the conversation to another bot in the same queue when the agent's task is over. For the conversation to flow correctly, you must set the first bot (Bot A) with the highest capacity, the human agent with the next highest capacity, and the second bot (Bot B) with the lowest capacity.

1. A customer starts a conversation that is routed to a queue.
2. The first bot (Bot A) that has the highest capacity accepts the conversation.
3. The customer requests to chat with a human agent.
4. The conversation is transferred to a human agent as the agent has second-highest capacity.
5. The customer chats with the human agent.
6. The human agent has finished delivering support and wants to hand off the conversation to a second bot (Bot B), which resides in the same queue.
7. The human agent is disconnected from the conversation, and the conversation is routed to Bot B.
8. Bot B receives the messages in the following order:
    - A conversation update that the “Bot is added”
    - The Omnichannel Set context event
9. The system triggers Bot B to send a greeting message.
10. The customer now chats with Bot B.