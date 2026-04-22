---
title: Configure governance policies (preview)
description: Governance policies help you enforce compliance, security, and content-safety for customer communications. Learn how to set up and manage effective policies.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 04/22/2026
ms.custom: bap-template
---

# Configure governance policies (preview)

Configure governance policies to enforce compliance, security, and content‑safety standards across customer communications in your organization. It evaluates outbound messages, both AI‑generated and human‑authored against configurable policies, helping you ensure that sensitive, restricted, or noncompliant content is automatically detected and managed. This feature supports the email channel and extends the safety checks used across other autonomous agents.

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
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go).
- Provide consent for potential [data movement across regions](/power-platform/admin/geographical-availability-copilot?utm_source=chatgpt.com&tabs=new).
- Enable AI agents for your Dynamics 365 environment in Power platform admin center. Learn more in [Copilot adoption in the Power Platform](/power-platform/admin/copilot/copilot-hub).

## Enable governance

1. In the site map of Copilot Service admin center, in **Customer Support** > select **Quality management**.
1. On the **Quality management** page, select **Manage** for **Governance (preview)**.
1. On the **Governance (preview)** page, turn on the toggle for governance.

## How a governance policy works

**Runtime evaluation**:
The system evaluates each email drafted by a service representative or AI agent by validating the message through the governance policy and checking the content against active policies. When it detects a rule violation, the system performs one of the following actions:

- Blocks the outgoing message
- Logs the violation for later review
- Routes the message for manual approval workflows

**Log and review**: 
Administrators can:

- Review detection logs
- Identify repeated risk patterns
- Adjust rule descriptions to refine system prompts

### Scenario examples

**Prevent agents from sending political content**

Administrator creates a rule: Ensure no political content is included in any customer communications.
- System generates a policy prompt
- All outbound emails are evaluated against this category

**Block competitor comparisons in support responses**

If teams prefer not to mention competitors:
- Create a policy referencing known competitor names
- Messages containing such content are automatically blocked

**Enforce compliance for regulated industries**

Healthcare, legal, and finance teams can set policy checks for:

- High‑risk advice
- Sensitive data leakage
- Restricted terminology

Governance policies ensure unsafe messages are intercepted before reaching customers. Until the representative updates the email draft to meet policy requirements, the checks continue to block it from being sent. Each failed policy check is recorded, allowing the representative to view previous failures for that draft.

## Related information

[Use governance policies (preview)](../use/use-governance-policies.md)