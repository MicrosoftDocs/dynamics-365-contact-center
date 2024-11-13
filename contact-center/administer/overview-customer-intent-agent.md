---
title: Overview of customer intent agent
description: Learn about what is customer intent agent and how it works in Dynamics 365 Contact Center and Dynamics 365 Customer Service.
author: neeranelli
ms.author: nenellim
ms.reviewer: 
ms.topic: overview
ms.collection: bap-ai-copilot
ms.date: 11/13/2024
ms.custom: bap-template
---

# Overview of customer intent agent

Customer intent agent uses generative AI to autonomously discover ongoing intents in your contact center instance, analyzing past interactions between customer service representatives (service representatives or representatives) and customers to create an intent library that enhances dynamic conversations. This benefits both assisted and self-service scenarios by enabling agents and representatives to quickly understand customer needs, guide conversations with follow-up questions, and provide tailored solutions in real time. 

Customer intent agent can be used in the following scenarios:

**Self service**: The intent can be added to a custom Copilot Studio agent that connects to the intent library to dynamically chat with the customer to:

- Determine customer intent based on discovered intents, such as refund, from the intent library.
- Ask follow-up questions based on additional attributes, such as error code, product name, and purchase date that're mined from historical conversations.
- Understand responses from customers to determine what follow-up questions have been answered by the customer.
- Generate a query to knowledge base to search for solutions based on gathered information.

**Assisted service**: Significantly reduce issue handling time by continuously detecting updates to intent based on ongoing conversations and provide: 
- Persist information that's discovered by Copilot in self service to quickly get the service representative up to speed on the intent and information gathered.
- A curated list of questions and suggested solutions as the next response that Copilot recommends the representative send to the customer.
- Separately show the detected intent, suggested follow-up questions and responses, suggested solutions in a holistic view. 
- 