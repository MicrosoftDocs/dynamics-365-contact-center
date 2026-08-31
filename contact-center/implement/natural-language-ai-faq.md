---
title: Responsible AI FAQ for NLU in AI agents
description: Find answers about the responsible use of natural language understanding in AI agents for Dynamics 365 Contact Center and Customer Service.
author: gandhamm
ms.author: mgandham
ms.reviewer: gandhamm
ms.topic: faq
ms.collection: bap-ai-copilot
ms.date: 08/27/2026
ms.update-cycle: 180-days
ms.custom: 
- bap-template
- responsible-ai-faq
---

# Responsible AI FAQ for NLU in AI agents

This FAQ describes the AI impact of generative orchestration and natural language understanding (NLU) for Microsoft Copilot Studio agents used in Customer Service.

## What is NLU and how is it used in agents?

Natural language understanding (NLU) enables AI agents to interpret user statements and convert them into actions. In Dynamics 365 Contact Center, NLU helps agents identify intents, extract meaning, and respond in digital and voice interactions. Learn more in the [NLU overview](/microsoft-copilot-studio/nlu-overview).

## What NLU options are available in Copilot Studio?

Copilot Studio offers multiple NLU options for building agents. You can choose generative AI for a more agentic system or classic orchestration for more control and fine-tuning. Select these options in the Language Understanding section in Copilot Studio.

## How do different NLU options impact my agent's performance?

Each NLU option has capabilities and limitations that might affect agent behavior and performance. Classic orchestration uses customer-provided training data to create a dynamic language model (DLM) at runtime. Generative AI uses pretrained large language models (LLMs), which might provide different capabilities and behaviors.

## Where does NLU processing occur for different options?

For NLU, runtime processing happens within Copilot Studio itself. For NLU+, the runtime processing occurs in Dynamics 365 Contact Center. Understanding where processing occurs can help you make informed decisions about performance and integration requirements.

## What should I consider from a responsible AI perspective when selecting an NLU option?

When selecting an NLU option, make sure you thoroughly review the capabilities and limitations of each option to make an informed decision that best fits your Dynamics 365 Contact Center business needs. We recommend that you consider factors such as transparency, data privacy, expected performance, and how well the option aligns with your specific use cases and customer expectations.

## How do the underlying technologies differ between NLU options?

Classic orchestration relies on customer-provided training data to create dynamic language models (DLMs) that are used at runtime. Generative AI uses pretrained LLMs, which might offer different capabilities and responsible deployment considerations.

## What transparency considerations should I keep in mind when implementing generative orchestration?

When you implement generative orchestration, it’s important to understand how your chosen [NLU model](/microsoft-copilot-studio/nlu-overview) influences your AI agent’s behavior and performance. Be aware of how the system interprets user inputs, determines actions, and generates responses. Maintain transparency in these processes to build trust with your customers and make sure that your agent’s actions align with your intended outcomes.

## Related information

[FAQ for using generative orchestration](/microsoft-copilot-studio/faqs-generative-orchestration#what-is-generative-orchestration)  
