---
title: Overview of proactive engagement
description: Learn about proactive engagement in Dynamics 365 Contact Center for optimized customer service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot
ms.date: 12/05/2025
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Overview of proactive engagement

Today, customers want brands to anticipate their needs, provide personalized engagement, and offer effortless support. Businesses seek automation, increased loyalty, and dependability. Proactive engagement is the solution to create AI-driven proactive outbound experiences that enable enterprises to engage with their customers proactively on voice channels. You can integrate Dynamics 365 Contact Center and Customer Insights journeys for an AI-empowered multichannel proactive engagement.

## What is proactive engagement?

By using a blend of AI agents and customer service representatives, you can reach out through phone calling to engage with your consumers in meaningful conversations, leading to quicker transactions, faster case closures, and enhanced customer satisfaction.

:::image type="content" source="../media/overview-proactive-engagement.png" alt-text="Overview of proactive engagement." lightbox="../media/overview-proactive-engagement.png":::

## How it works

1. Configure [proactive engagement](configure-proactive-engagement.md) in Dynamics 365 Contact Center.

1. You can initiate the calls using one of the following options:
   - Configure journeys using Dynamics 365 Customer Insights to determine contacts and optimal timings for interactions. Journeys are a visual, automated workflow that guides how your customer moves through a series of interactions. It orchestrates personalized experiences across channels like voice, email, SMS, push notifications, and more, based on user behavior and business logic.
   - Integrate CCaaS API to make a call. The Dataverse CCaaS API integrates the contact center with existing campaign tools and supports callbacks.

1. Configure Copilot voice agents to handle preliminary tasks, such as gathering information and answering FAQs.

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
[Use CCaaS_CreateProactiveVoiceDelivery API](../extend/api/ccaas_createproactivevoicedelivery.md)  