---
title: Use on-demand evaluation
description: Learn how to use on-demand evaluation in Dynamics 365 Customer Service and Dynamics 365 Contact Center to assess cases and conversations efficiently with AI-assisted, manual, or AI agent methods.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 02/06/2026
ms.custom: bap-template
---

# Use on-demand evaluation

**Conversations**: [!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

**Cases**: [!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]

Use on-demand evaluation to check cases and conversations. Request evaluations with AI-assisted, manual, or AI agent methods for flexible quality management. This article explains how to use on-demand evaluation, including prerequisites and step-by-step instructions.

## Prerequisites

- Enable [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- Assign the required [roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).


## On-demand evaluation for cases

To request evaluations for multiple cases from the case grid:

1. Select the required records.
    
1.  Select **Request evaluation**. You can select up to 20 records for evaluation. 

To request evaluation for a particular case:

1.  Go to **Cases**, select the required case, and then select **Request evaluation**.

1.  On the **Request evaluation** dialog, select the following:

    - **Evaluation criteria:** Search and select an evaluation criteria from the list of criteria.
    - **Evaluation method:** Select an evaluation method: **AI assisted**, **Manual**, or **AI agent**.
    - **Assigned to:** Select the user.
    - **Evaluation due date:** Select a due date for the evaluation.

1.  Select **Request**.

1.  Once the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation    Summary** provided by Copilot.

1.  Select **Submit and Close**. The **Evaluator status** appears as **Completed**.

## On-demand evaluation for conversations

To request evaluation for closed conversations:

1. Go to **Activities** > **Closed Conversations**.

1. Select a closed conversation, and then on the specific conversation, select **Request evaluation**.

1. On the **Request evaluation** dialog, select the following:

   - **Evaluation criteria:** Search and select an evaluation criteria from the list of criteria.
   - **Evaluation method:** Select an evaluation method: **AI assisted**, **Manual**, or **AI agent**. If you select **AI agent**, the **Assigned to** and **Evaluation due date** is turned off.
   - **Assigned to:** Select the user.
   - **Evaluation due date:** Select a due date for the evaluation.
    
1.  Select **Request**. 

1. Once the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation    Summary** provided by Copilot.

1.  Select **Submit and Close**. The **Evaluator status** appears as **Completed**.


## Related information

[Use evaluation plan](evaluation-plan.md)  
[Use evaluations](use-evaluations.md)  
[Use evaluation criteria](evaluation-criteria.md)  
[Manage Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md)