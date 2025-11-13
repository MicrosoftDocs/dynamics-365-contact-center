---
title: Transfer conversations from customer service representatives to agents
description: Learn how a customer service representative can transfer a conversation back to an agent.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection:
ms.date: 06/27/2025
ms.custom:
  - bap-template
  - ai-gen-docs-bap
  - ai-gen-title
  - ai-seo-date:11/11/2024
---

# Transfer conversations from customer service representatives to AI agents

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]

In some support scenarios, a customer service representative (service representative or representative) needs to transfer a conversation back to an AI agent (agent) after providing personalized support. This transfer helps with basic, repetitive tasks or collects more information, like in a customer survey.

You can facilitate the transfer of a conversation from a service representative back to an AI agent in the following ways:

- Create two agents that reside in two queues
- Create two agents that reside in the same queue

### Two agents in two queues

In this scenario, an AI agent transfers a conversation to a service representative. The representative then transfers the conversation to another AI agent in a different queue.

1. A customer starts a conversation.
2. The conversation is routed to Queue 1.
3. The first AI agent (Agent A) accepts the conversation.
4. The customer requests to chat with a service representative.
5. The conversation is transferred to a service representative within Queue 1.
6. The customer converses with the service representative.
7. The service representative finishes delivering support and wants to hand off the conversation to a second AI agent, Agent B.
8. The service representative is disconnected from the conversation.
9. The conversation routed to Agent B in Queue 2.
10. The system triggers Agent B to send a greeting message.
11. The customer now chats with Agent B.

### Two agents in one queue

In this scenario, after an AI agent has transferred a conversation to a service representative, the representative will transfer the conversation to another AI agent in the same queue when the service representative's task is over. For the conversation to flow correctly, you must set the first AI agent (Agent A) with the highest capacity, the service representative with the next highest capacity, and the second AI agent (Agent B) with the lowest capacity.

1. A customer starts a conversation that is routed to a queue.
2. The first agent (Agent A) that has the highest capacity accepts the conversation.
3. The customer requests to chat with a service representative.
4. The conversation is transferred to a service representative as the representative has second-highest capacity.
5. The customer chats with the service representative.
6. The service representative has finished delivering support and wants to hand off the conversation to a second agent (Agent B), which resides in the same queue.
7. The service representative is disconnected from the conversation, and the conversation is routed to Agent B.
8. Agent B receives the messages in the following order:
    - A conversation update that the "Agent is added"
    - The Omnichannel Set context event
9. The system triggers Agent B to send a greeting message.
10. The customer now chats with Agent B.

### Related information

[Integrate a Copilot agent](/dynamics365/customer-service/administer/configure-bot-virtual-agent)  