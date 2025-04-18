---
title: Overview of Customer Intent Agent (preview)
description: Learn about Customer Intent Agent and how it works in Dynamics 365 Contact Center and Dynamics 365 Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: 
ms.topic: overview
ms.collection: bap-ai-copilot
ms.date: 03/28/2025
ms.custom: bap-template
---

# Overview of Customer Intent Agent (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Customer Intent Agent uses generative AI to autonomously discover intents in your contact center instance. It analyzes past interactions between customer service representatives (service representatives or representatives) and customers to create an intent library that enhances dynamic conversations. Intent benefits both assisted and self-service scenarios by enabling agents and representatives to quickly understand customer needs, guide conversations with follow-up questions, and provide tailored solutions in real time. 

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

Customer Intent Agent can be used in the following scenarios:

**Self service**: You can add the intent to a custom Copilot agent that connects with the intent library and dynamically chats with the customer to:

- Determine customer intent based on discovered intents, such as refund, from the intent library.
- Ask follow-up questions based on other attributes, such as error code, product name, and purchase date, discovered from historical conversations.
- Understand responses from customers to determine what follow-up questions are answered by the customer.
- Generate a query to knowledge base to search for solutions based on gathered information.

**Assisted service**: Significantly reduce issue handling time by continuously detecting updates to intent based on ongoing conversations and provide: 
- Information that's discovered by Copilot in self service to quickly get the representative up to speed on the intent and collected information.
- A curated list of questions and suggested solutions as the next response that the representative can send to the customer.
- The detected intent separately, suggested follow-up questions and responses, and suggested solutions in a holistic view.

### Related information

[Manage Customer Intent Agent](manage-customer-intent-agent.md)  
[Enable intent for service representatives](enable-intent-for-service-reps.md)  
[Set up intent agent](set-up-intent-agent.md)  
[Use intent-based suggestions](../use/use-intent-suggestions.md)  
