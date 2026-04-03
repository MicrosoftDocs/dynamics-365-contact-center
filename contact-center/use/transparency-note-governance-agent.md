---
title: Transparency Note for Governance Agent
description: Learn about Governance Agent, a rule-based system that ensures AI assistants operate safely and within compliance guidelines.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 04/03/2026
ms.custom: bap-template
---

# Transparency note for Governance Agent

This transparency note provides information about Governance Agent, also known as the Guardrails Agent, including its capabilities, limitations, and intended uses.

> [!IMPORTANT]
> This document is part of Microsoft's commitment to responsible AI development and deployment.

## What is Governance Agent?

Governance Agent is a rule-based system that helps ensure AI assistants operate safely and within compliance guidelines. In practical terms, it acts as a safeguard layer on top of AI models or human responses. For example, when a customer service representative (service representative or representative) is about to send an email, Governance Agent intercepts that action and checks it against a set of predefined guardrails, such as rules and policies. If the output violates a policy, Governance Agent can block the email to prevent harmful or non-compliant results.

Governance Agent was developed to address the inherent nondeterminism of generative AI, where identical prompts can yield different outputs that may contain competitor references or violate business policies. This poses significant risks in regulated industries. The system ensures compliance by validating model inputs and outputs at runtime, blocking or correcting any content that falls outside approved boundaries.

## Key terms

- **Governance Agent**: A service that enforces configurable guardrails on other AI agents’ actions or emails by CSR and outputs. It intercepts an email and evaluates it against a set of rules to ensure compliance with specified policies. 
- **Guardail Rule**: An individual condition or check that can be configured within a guardrail. Rules can take many forms (e.g. “the response must not contain profanity” or “if the AI gives financial advice, it must include a disclaimer”).  
- **AI Agent**: The AI system or assistant whose behavior is being governed by the guardrails. This could be a chatbot, an email composition assistant, a customer service agent, or any autonomous AI that produces content or takes actions. The Governance Agent works as a companion to such an AI agent, overseeing its outputs. 
- **Failure action**: The predefined outcome when a rule is violated. For example, a failure action might be “respond with a standard refusal message and escalate to a human supervisor” if an AI’s output doesn’t meet a compliance rule3. Each rule/guardrail can have a different failure handling configuration (e.g. some might simply remove the offending content, others might stop the AI’s response entirely). 

## System behavior

Governance Agent ensures AI system compliance by managing the complete policy enforcement lifecycle, including rule configuration, runtime evaluation, execution of failure actions, and comprehensive reporting of outcomes. The major components of the system are as follows:

**Types of guardrail rules** 

The system supports a variety of rule types to cover different aspects of AI behavior.

- **Compliance rules** – These rules enforce business, legal, or regulatory requirements in the AI's responses. Here's an example: "Always include a specific legal disclaimer whenever financial investment advice is given."

- **Topic filters** – These rules block or flag content on certain subjects that an organization wants to avoid.

## Use cases

### Intended uses

Governance Agent is designed to be used by organizations that deploy AI systems in scenarios where additional oversight is needed to meet business or compliance requirements. Some of the intended use cases are:

- Case Management Agent
- Emails sent by humans which require checks like:
  - Competitor checks
  - Financial advice validation
  - Poor response detection

### Legal and regulatory considerations

> [!WARNING]
> Organizations need to evaluate potential specific legal and regulatory obligations when using any AI services and solutions, which might not be appropriate for use in every industry or scenario.

Restrictions might vary based on regional or local regulatory requirements. Additionally, AI services or solutions aren't designed for and may not be used in ways prohibited by applicable terms of service and relevant codes of conduct.

In other words, even though Governance Agent adds control to AI systems, deploying AI in sensitive areas still requires careful thought. Customers should ensure that using an AI with guardrails complies with laws and policies relevant to their region and industry, and they must adhere to Microsoft's terms of service.

## Setup and configuration

### Enable Governance Agent

Customers need to enable Governance Agent in Customer Service admin center.

### Configure custom guardrails

Customers can set up their own guardrails as per business policy.

### Runtime behavior

During runtime, the same process applies while sending emails. Governance Agent intercepts and validates content before it's sent.

### View execution logs

Customers can view the logs of failed executions to monitor and troubleshoot guardrail enforcement.

## System performance

As Governance Agent serves as a gatekeeper for AI outputs, performance in this context refers to how accurately and efficiently it enforces the intended rules. There are two main aspects to consider:

- Rule enforcement accuracy: Detecting genuine policy violations while avoiding unnecessary blocking of compliant content.
- Operational efficiency: Minimal latency and system overhead.

### Reliability and accuracy

Governance Agent is designed to be highly reliable in applying deterministic rules. Whenever a guardrail rule is clearly defined, for example, a specific forbidden phrase, the system consistently flags it every time. It doesn't suffer from random variation.

However, no AI oversight system is perfect. There is always a balance between:

- **False positives** – Flagging or blocking content that actually would have been fine.
- **False negatives** – Allowing something through that should have been stopped.

The goal of Governance Agent is to maximize true positives or negatives and minimize the errors. For example, using exact-match rules for clearly forbidden phrases yields very few false negatives, and using context-aware checks for more nuanced content helps reduce false positives. The following table explains these terms with examples in the context of the Governance Agent.


|Outcome  | Meaning  | Example Scenario  |
|---------|---------|---------|
|True Positive     |   A policy-violating output is correctly identified and blocked by the guardrail.       |    The AI scheduler attempts to automatically send an email containing a client’s credit card number, but a guardrail catches this sensitive data and prevents it from being sent, thereby averting a privacy breach.      |
|False Positive      |  An output that actually does not violate policy gets incorrectly blocked by a guardrail.        |   The word “Apple” is on a company’s competitor blocked guardrail. The AI writes “Apple” referring to the fruit in a recipe, but the guardrail, not understanding context, flags it and unnecessarily blocks the sentence.       |
|False Negative      |  A truly policy-violating output is missed by the guardrails and allowed to go through.       |   A clever user request slips past a keyword filter (for example, using slang or an uncommon spelling for a banned term) and the AI’s response contains a statement that should have been disallowed, which the guardrail did not catch.       |
|True Negative     |   A clean, policy-compliant output passes through the guardrails with no issues (as it should).       |    The AI drafts a polite, standard response email that conforms to all policies; the guardrails check it quickly and let it through without any modifications.      |


### Operational efficiency

Governance Agent is engineered to add minimal overhead to the AI's operation. Currently, the system adds **1.35 seconds** while sending emails via representatives or Case Management Agent.

> [!NOTE]
> Performance metrics are subject to change as the system evolves and improvements are made.

## Responsible AI considerations

Microsoft is committed to developing AI systems that are:

- **Fair** – Treat all people equitably
- **Reliable and safe** – Operate consistently and minimize harm
- **Private and secure** – Protect data and privacy
- **Inclusive** – Empower everyone and engage people
- **Transparent** – Enable understanding of how AI systems work
- **Accountable** – Ensure people are accountable for AI systems

Governance Agent is designed with these principles in mind, providing organizations with the tools they need to deploy AI responsibly.

Learn more about responsible AI at Microsoft at [Responsible AI website](https://www.microsoft.com/ai/responsible-ai).

## Related information

- [Dynamics 365 Customer Service documentation](/dynamics365/customer-service/)
- [Responsible AI principles](https://www.microsoft.com/ai/responsible-ai)
