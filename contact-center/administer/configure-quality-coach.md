---
title: Configure quality and coaching skill in Dynamics 365 Contact Center
description: Create evaluation plans, quality indicators, and guardrails for AI-powered quality evaluations and coaching guidance.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 09/08/2026
ms.custom: bap-template
ai-usage: ai-assisted
---

# Configure quality and coaching skill

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

Quality and coaching skills help organizations consistently monitor, measure, and improve customer conversations through AI-powered evaluations and real-time coaching. With a centralized quality library and flexible evaluation plans, supervisors can identify problems early, coach representatives in real time, and help ensure that AI-driven conversations meet organizational and compliance standards at scale.

## Key concepts

- **Evaluation plans**: Define how quality indicators and guardrails are applied and monitored. An evaluation plan specifies the criteria to use, the conversations to include, the evaluation timing and frequency, and the actions or alerts triggered by results.
- **Quality library**: Contains the reusable quality indicators and guardrails that you can add to evaluation plans.
  - **Quality indicators**: Represent measurable dimensions of conversation quality, such as the use of empathetic language, greeting etiquette, or the handling of sensitive information. Each indicator contains one or more questions used to score conversations. Scored indicators contribute to an overall quality score and can be reused across evaluation plans.
  - **Guardrails**: Define required or prohibited behaviors in a conversation, such as avoiding financial advice or applying extra care when interacting with vulnerable customers. Guardrails are evaluated for violations rather than assigned numeric scores. Each guardrail has a priority that indicates the urgency of a violation. You can optionally provide representatives with a suggested next response when a violation is detected.

> [!IMPORTANT]
> - This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature isn't intended for use in making—and shouldn't be used to make—decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This responsibility also includes adequately notifying end users that their communications with representatives might be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users might be monitored, recorded, or stored.
> - Customers should avoid using the system to infer or draw conclusions about the emotional or psychological states of employees or customers, such as stress levels, intent, or sentiment beyond supported signals. The system doesn't reliably detect mental or emotional conditions.

## Prerequisites

- You must have the Omnichannel Administrator role.
- Set up [consumption-based billing and capacity](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).

## Open quality and coaching skill

1. In Copilot Service admin center, go to **Customer Support** > **Quality and coaching**.
1. Select **Evaluation plans** to create and manage evaluation plans, or select **Quality library** to manage quality indicators and guardrails.

## Create an evaluation plan

The **Evaluation plans** page lists the plans in your environment, including their frequency, status, and quality criteria.

  :::image type="content" source="../media/quality-coaching-evaluation-plan.png" alt-text="Evaluation plans page listing plans and their frequency, status, and quality criteria." lightbox="../media/quality-coaching-evaluation-plan.png":::

To create an evaluation plan:

1. Select **Add new**.
1. In the **New evaluation plan** dialog, select a **Frequency** option:
   - **In real time**: Evaluations run continuously during the conversation. Quality scores and guardrails are assessed in real time so that configured actions can occur immediately.
   - **On conversation close**: The evaluation runs once after the conversation closes. Results are available only after the conversation is closed.
1. Select **Next**.
1. In **General details**, provide the following information:
   - **Plan name**: Enter a descriptive name for the plan.
   - **Description**: Optionally describe what the plan evaluates.
   - **Quality criteria**: Select the quality indicators and guardrails to include.
1. Select **Next**.
1. In **Conditions**, add one or more conditions that identify the conversations to evaluate. For example, select conversations from a specific queue or workstream.
1. In **Conversation sampling**, specify the percentage of matching conversations to evaluate.
1. Select **Next**.
1. Configure the settings for the selected frequency:
   - For an **In real time** plan, in **Actions**, define score ranges and choose whether to notify a supervisor, send a coaching nudge to the representative, or do both. Nudges appear as messages during the conversation.
     - Define scored-indicator ranges as **Critical**, **Warning**, or **Normal**.
     - For each range, select whether to notify a supervisor, send a coaching nudge to the representative, or both.
   - For an **On conversation close** plan, in **Weights**, specify how much each quality indicator contributes to the overall score.
1. Save the plan.
1. On the **Quality and coaching** page, activate the plan so that evaluations can begin.

## Manage the quality library

The **Quality library** lists all quality indicators and guardrails available in your environment. Quality indicators and guardrails define the criteria used to evaluate conversations. You can create an indicator or copy a built-in indicator to edit and use. You can delete inactive quality indicators.

### Manage a quality indicator

1. In **Quality library**, under **Quality indicators**, select **Add new** or select an existing indicator.
1. On the **Add quality indicator** dialog, provide the following information:
   - **Quality indicator name**: Enter a name for the indicator.
   - **Description**: Optionally, describe the quality behavior to evaluate.
   - **Questions**: Add one or more questions used to assess conversations.
     - For **Type of answers**, select **Yes/No**, **Multi-select**, or **Single select**. **Multi-select** allows more than one answer; **Single select** allows one answer.
     - Assign a score to each answer option.
     - Optionally add evaluation instructions to improve scoring accuracy.
1. Save the quality indicator.
1. On the **Quality and coaching** page, activate the quality indicator before adding it to an evaluation plan.

  :::image type="content" source="../media/quality-coaching-quality-indicators.png" alt-text="Quality indicator configuration with questions, answer types, and assigned scores." lightbox="../media/quality-coaching-quality-indicators.png":::

### Manage a guardrail

1. In **Quality library**, under **Guardrails**, select **Add new** or select an existing guardrail.
1. On the **New guardrail** dialog, provide the following information:
   - **Guardrail name**: Enter a name for the guardrail.
   - **Description**: Describe the behavior that the guardrail requires or prohibits.
   - **Priority**: Select **Low**, **Medium**, or **High** to indicate the urgency of a violation.
   - **Nudge text**: Optionally, enter the message to display to representatives.
   - **Suggest next response**: Select this option to provide AI-generated guidance when a violation is detected.

1. Save the guardrail.
1. On the **Quality and coaching** page, activate the guardrail before adding it to an evaluation plan.

  :::image type="content" source="../media/quality-coaching-guardrails.png" alt-text="Guardrail configuration with priority, representative nudge, and suggested-response settings." lightbox="../media/quality-coaching-guardrails.png":::

## Best practices

- Build the quality library before creating plans so that you have indicators and guardrails ready to reuse.
- Keep each indicator focused on one quality dimension to make scores easier to interpret.
- Use conditions and sampling to limit real-time evaluation to priority queues or workstreams.
- Start with conservative actions and expand notifications or nudges based on operational readiness.
- Review results regularly and refine criteria, weights, conditions, and actions as needed.

## Related information

- [Contact center agents in Dynamics 365 Contact Center](overview-contact-center-agents.md)
- [Use quality and coaching skill](../use/use-quality-coach.md)
- [Use the Quality Assurance Agent dashboard](../use/quality-assurance-agent-dashboard.md)
- [Responsible AI FAQ for AI agents](../implement/faq-rai-ai-agents.md)
