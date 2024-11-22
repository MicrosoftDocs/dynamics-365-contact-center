---
title: Manage intent using Copilot (preview)
description: 
author: neeranelli
ms.author: nenellim
ms.reviewer: 
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/14/2024
ms.custom: bap-template
---

# Manage intent using Copilot

Customer intent agent uses generative AI to autonomously discover ongoing intents from your customer service instance, analyzing past interactions to create an intent library that enhances dynamic conversations. The service representatives use the information to quickly understand customer needs, guide conversations with follow-up questions, and provide tailored solutions in real time.

Copilot presents a curated list of questions and suggested solutions in the chat response box, which enhances efficiency by reducing manual typing. For self-service, Copilot generates relevant follow-up questions and uses the information to query the knowledge source, leading to higher deflection rates and allowing representatives to focus on cases that require manual intervention. 

## Enable customer intent agent

1. In Contact Center admin center or Customer Service admin center, select **Intent** under **Customer support**.
1. On the **Customer Intent Agent (preview)** page that appears, enable the **Turn on Customer Intent Agent** toggle.

## Manage intent discovery setup

You need to run the AI model on data sources like cases and conversations to identify intent groups and related intents.

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage intent discovery setup**.
1. On the **Manage intent discovery setup** page, select **Add intent discovery setting**.
1. In **Intent discovery settings**, enter the following details:
   - **Name**: An intuitive name that meets your business requirement.
   - **Data source**: Available for conversations only and therefore read-only.
   - **Data granularity**: Select **Low**, **Medium**, or **High** in the list.
   - **Record status**: Select **Pending**, **Approved**, or **Discarded** in the list.
1. Select **Simulate** to simulate the 




