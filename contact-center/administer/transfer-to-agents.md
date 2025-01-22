---
title: Transfer conversations from customer service representatives to agents
description: Learn how a customer service representative can transfer a conversation back to an agent.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: conceptual
ms.collection:
ms.date: 12/16/2024
ms.custom:
  - bap-template
  - ai-gen-docs-bap
  - ai-gen-title
  - ai-seo-date:11/11/2024
---

# Transfer conversations from customer service representatives to agents

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]


In some support scenarios, a customer service representative may need to transfer a conversation back to a Copilot Studio agent after providing personalized support. This transfer can help with basic, repetitive tasks or collect additional data, such as in a customer survey.

You can facilitate the transfer of a conversation from a customer service representative (service representative or representative) back to an agent in the following ways:

- Create two agents that reside in two queues
- Create two agents that reside in the same queue

### Two agents in two queues

In this scenario, an agent has transferred a conversation to a service representative. The service representative will transfer the conversation again to another agent in another queue.

1. A customer starts a conversation.
2. The conversation is routed to Queue 1.
3. The first agent (Agent A) accepts the conversation.
4. The customer requests to chat with a service representative.
5. The conversation is transferred to a service representative within Queue 1.
6. The customer converses with the service representative.
7. The service representative has completed delivering support and wants to hand off the conversation to a second  (Agent B), which resides in Queue 2.
8. The service representative is disconnected from the conversation.
9. The conversation routed to Agent B in Queue 2.
10. The system triggers Agent B to send a greeting message.
11. The customer now chats with Agent B.

### Two agents in one queue

In this scenario, after an agent has transferred a conversation to a service representative, the service representative will transfer the conversation to another agent in the same queue when the service representative's task is over. For the conversation to flow correctly, you must set the first agent (Agent A) with the highest capacity, the service representative with the next highest capacity, and the second agent (Agent B) with the lowest capacity.

1. A customer starts a conversation that is routed to a queue.
2. The first agent (Agent A) that has the highest capacity accepts the conversation.
3. The customer requests to chat with a service representative.
4. The conversation is transferred to a service representative as the representative has second-highest capacity.
5. The customer chats with the service representative.
6. The service representative has finished delivering support and wants to hand off the conversation to a second agent (Agent B), which resides in the same queue.
7. The service representative is disconnected from the conversation, and the conversation is routed to Bot B.
8. Agent B receives the messages in the following order:
    - A conversation update that the “Agent is added”
    - The Omnichannel Set context event
9. The system triggers Agent B to send a greeting message.
10. The customer now chats with Agent B.