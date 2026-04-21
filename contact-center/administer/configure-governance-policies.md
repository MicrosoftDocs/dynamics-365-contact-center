---
title: Configure governance policies
description: Learn about governance policies, a rule-based system that ensures AI assistants operate safely and within compliance guidelines.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 04/21/2026
ms.custom: bap-template
---

# Configure governance policies

Configure governance policies enforce compliance, security, and content‑safety standards across customer communications in your organization. It evaluates outbound messages, both AI‑generated and human‑authored against configurable guardrails, helping administrators ensure that sensitive, restricted, or non‑compliant content is automatically detected and managed. This feature supports the email channel and extends the safety checks used across other autonomous agents.

> [!IMPORTANT]
>
> - This is a preview feature. 
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520), and are available before an official release so that customers can get early access and provide feedback.

## Prerequisites

- Administrators need the CSR Manager role.
- Service representatives need the Customer Service Representative role.
- For custom roles assigned to service representatives, you need to add Read at Global level on msdyn_governanceagent_status.
- For custom roles assigned to administrators, you need to add Read, Create, Write, Delete, Append, Appendto, Assign at Global level on:
    - msdyn_governanceagent_status
    - msdyn_guardrail_consumer_mapping
    - msdyn_guardrail_execution_info
    - msdyn_guardrail_rule
    - msdyn_guardrail_rule_version
    - msdyn_guardrail_scenariotype
- Setup [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go) or pre-paid.
- Provide consent for potential [data movement across regions](manage-quality-evaluation-agent.md#data-movement-across-regions).
- Enable AI agents for your Dynamics 365 environment in Power platform admin center. Learn more in [Copilot adoption in the Power Platform](/power-platform/admin/copilot/copilot-hub).

## Enable governance

1. In the site map of Copilot Service admin center, in **Customer Support** > select **Quality management**.
1. On the **Quality management** page, select **Manage** for **Governance (preview)**.
1. On the **Governance (preview)** page, turn on the toggle for governance.

## How Governance Agent works

- Runtime evaluation: When a service representative or AI agent drafts an email, the message is passed through the Governance Agent pipeline, where the agent compares content against active guardrails. When a rule violation is detected, the Governance Agent can perform one of the following actions:

    - Block the outgoing message
    - Log the violation for later review
    - Route for manual approval workflows

- Log and review: Administrators can

    - Review detection logs
    - Identify repeated risk patterns
    - Adjust rule descriptions to refine system prompts

### Scenario examples

**Prevent agents from sending political content**

Administrator creates a rule: Ensure no political content is included in any customer communications.
- System generates guardrail prompt
- All outbound emails are evaluated against this category

**Block competitor comparisons in support responses**

If teams prefer not to mention competitors:
- Create a guardrail referencing known competitor names
- Messages containing such content are automatically blocked

**Enforce compliance for regulated industries**

Healthcare, legal, and finance teams can set guardrails for:

- High‑risk advice
- Sensitive data leakage
- Restricted terminology

Governance policies ensures unsafe messages are intercepted before reaching customers. Until the representative updates the email draft to meet policy requirements, the checks continues to block it from being sent. Each failed guardrail check is recorded, allowing the representative to view previous failures for that draft.