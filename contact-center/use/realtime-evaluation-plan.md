---
title: Use evaluations for real-time conversations
description:  Learn to create, activate, and manage evaluation plans for ongoing conversations in Dynamics 365 Contact Center. Improve customer experience with real-time insights.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 04/15/2026
ms.custom: bap-template
---

# Use evaluations for real-time conversations

**Conversations**: [!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

Supervisors monitor representatives and AI agents to maintain oversight and brand integrity by enabling monitoring, conducting real-time consultations, and responding to alerts to intervene when necessary. This approach minimizes operational effort, improves customer experience, and accelerates the transition to full automation while maintaining service quality.

By combining real-time monitoring with configurable evaluation plans, the real-time Quality Evaluation Agent empowers organizations to enhance customer satisfaction, improve agent performance, and maintain compliance standards across diverse scenarios. 

Supervisors use the evaluation framework to define the evaluation criteria and create structured evaluation plans. When supervisors execute a plan, the system sends requests to the real-time Quality Evaluation Agent. The real-time Quality Evaluation Agent processes these requests and generates evaluation responses in real time. 

## Prerequisites

- Assign the Quality Manager, Quality Evaluator, Quality Administrator, and the Omnichannel Supervisor roles. Learn more in [Assign roles and enable users](/dynamics365/customer-service/implement/add-users-assign-roles).
- Enable [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).


## Create an evaluation criteria

Follow the [best practices](evaluation-criteria.md#best-practices-for-evaluation-criteria) when you [create an evaluation criteria](evaluation-criteria.md#create-evaluation-criteria).

## Create a real-time evaluation plan for ongoing conversations

You need to turn on the **Criteria scoring** toggle for your evaluation criteria. Learn more in [Create evaluation criteria](evaluation-criteria.md#create-evaluation-criteria).

To create a real-time evaluation plan:

1. In Copilot Service workspace, go to **Evaluation Plans**.

1. On the **Evaluation plans** page, select **New**.

1. On the **New Evaluation Plan** page, in the **Evaluation plan details** section, provide the following information:

    - **Plan name**: Enter plan name.
    - **Description**: Enter description.
    - **Record type**: Select **Conversations**.
     
1. In the **Frequency** section, for **Frequency type**, select **Real-Time**.

1. In the **Conditions** section, add the workstreams for which you want to enable real-time evaluation.

1. In the **Assign Evaluation** section, for **Evaluation method**, select **AI agent**.
    
1.  Select **Save**.

Learn how to view scores for the real-time evaluation plan in [Manage ongoing Quality Evaluation Agent conversations](ongoing-quality-evaluation-agent-conversations.md).

> [!NOTE]
> You can't use simulation with real-time evaluation plan for ongoing conversations when new criteria are created.

## Activate, pause, resume, or delete evaluation plans

Learn more in [Activate, pause, resume, or delete evaluation plans](evaluation-plan.md#activate-pause-resume-or-delete-evaluation-plans).

## Edit evaluation plans

Learn more in [Edit evaluation plans](evaluation-plan.md#edit-evaluation-plans).