---
title: Overview of proactive engagement
description: Learn about proactive engagement in Dynamics 365 Contact Center for optimized customer service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot
ms.date: 01/13/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Overview of proactive engagement

Today, customers want brands to anticipate their needs, provide personalized engagement, and offer effortless support. Businesses seek automation, increased loyalty, and dependability. Proactive engagement is the solution to create AI-driven proactive outbound experiences that enable enterprises to engage with their customers proactively on voice channels. You can integrate Dynamics 365 Contact Center and Customer Insights journeys for an AI-empowered conversational journeys.

## What is proactive engagement?

By using a blend of AI agents and customer service representatives, you can reach out through phone calling to engage with your consumers in meaningful conversations, leading to quicker transactions, faster case closures, and enhanced customer satisfaction.

:::image type="content" source="../media/overview-proactive-engagement.png" alt-text="Overview of proactive engagement." lightbox="../media/overview-proactive-engagement.png":::

## Use cases

### CRM system workflows

Use deterministic proactive engagement to automate workflows that trigger outbound calls based on defined conditions. Examples include case closure notifications, automated data collection, status updates, alerts, and mission-critical engagements. You can trigger these engagements in the following ways:

- **CCaaS API or Power Automate flows**: Available natively with Dynamics 365 Contact Center. Use CCaaS APIs to integrate with non-Microsoft systems, or create a Power Automate flow triggered by changes to Dynamics 365 records such as a case status update.
- **Customer Insights Journey triggers**: Use journey triggers to initiate calls when a record is created or updated. This option requires Dynamics 365 Customer Insights licenses.

### AI agents-led proactive engagement

Use AI agents-led proactive engagement to enable AI agents, such as case monitoring agents, fraud monitoring agents, and personal agents, to initiate on-demand customer engagements. The Dynamics 365 Contact Center MCP server (preview) provides tools that allow agents to schedule outbound voice calls and SMS messages (preview) using customer details and time windows, without requiring manual API integrations.

### Single-channel, single-step engagements

A single-channel, single-step campaign runs one action on a contact segment with optional retry logic. It doesn't branch out based on outcomes or orchestrate follow-up actions across channels. Some examples are as follows:

- **Appointment reminder calls**: A healthcare clinic reminds patients of upcoming appointments.
- **Payment reminder messages**: A utility company notifies customers about overdue bills.
- **Survey outreach**: A bank conducts a customer satisfaction survey by voice.

These campaigns can be configured and run natively within Dynamics 365 Contact Center.

### Deterministic multi-channel, multi-step journeys

A multi-channel, multi-step journey orchestrates multiple sequential or conditional actions across one or more channels, with branching logic based on customer responses, behaviors, or outcomes. Journeys can span multiple days or weeks and support cross-channel orchestration across voice, email, SMS, and push notifications.

You require Dynamics 365 Customer Insights apart from Dynamics 365 Contact Center. Learn about how to configure a journey using [Dynamics 365 Customer Insights](/dynamics365/customer-insights/journeys/proactive-engagement-how-to).

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
[Use CCaaS_CreateProactiveVoiceDelivery API](../extend/api/ccaas_createproactivevoicedelivery.md)  
