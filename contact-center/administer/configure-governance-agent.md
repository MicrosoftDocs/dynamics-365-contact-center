---
title: Configure Governance Agent
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

# Configure Governance Agent

Governance Agent enables organizations to enforce compliance, security, and content‑safety standards across customer communications. It evaluates outbound messages, both AI‑generated and human‑authored against configurable guardrails, helping administrators ensure that sensitive, restricted, or non‑compliant content is automatically detected and managed. This feature supports the email channel and extends the safety checks used across other autonomous agents.

## Prerequisites

- Setup copilot messages credits [pay-as-you-go](/dynamics365/customer-service/administer/setup-pay-as-you-go) or pre-paid.
- [Data movement across regions](manage-quality-evaluation-agent.md#data-movement-across-regions).
- AI agent enabled setting.

## Roles and privileges

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

## Enable Governance Agent

1. In the site map of Copilot Service admin center, select **Governance Agent**.
1. On the **Governance Agent** page, turn on the Governance Agent toggle.
1. Select **New guardrail**.
1. On the **Create guardrail **dialog, provide the following information:
    1. In the **Guardrail details** section:
        1. **Guardrail name**: Provide a name.
        1. **Instructions**: Add instructions for the guardrail type that you want to create. The description should clearly express what content to detect, block, or manage to ensure that the system prompt is accurate.
    1. In the **Assign guardrail** section, provide:
        1. **Channel**: Email only. The guardrail agent evaluates every outgoing email to ensure it complies with the defined policies.
        1. **Method**: Select **Manual - Email drafted by a person** or **AI agent - AI completes and sends email**.
        1. **Detection method**: Select from **Log only** or **Log and Block**.
    1. **Conditions**: Add conditions to select a subset of emails where this guardrail will be run. If you don’t select any conditions, all emails are run through the guardrail check.
1. Save and activate.

You must review the prompt generated. If you want to make changes, update the instructions to refine prompt. Microsoft Copilot credits are consumed each time a prompt is generated.

## View detection log

You can view logs under the **Detection log** tab on the **Governance Agent** page. 
When you select **Log only**, the agent records that the guardrail check was run and failed. While **Log and block**, both blocks the email and logs the failure for audit.

## How Governance Agent works

### Runtime evaluation

When a service representative or AI agent drafts an email, the message is passed through the Governance Agent pipeline, where the agent compares content against active guardrails. When a rule violation is detected, the Governance Agent can perform one of the following actions:

- Block the outgoing message
- Log the violation for later review
- Route for manual approval workflows

### Log and review

Administrators can:

- Review detection logs
- Identify repeated risk patterns
- Adjust rule descriptions to refine system prompts

## Example scenarios

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

Governance Agent ensures unsafe messages are intercepted before reaching customers. Until the representative updates the email draft to meet policy requirements, Governance Agent continues to block it from being sent. Each failed guardrail check is recorded, allowing the representative to view previous failures for that draft.