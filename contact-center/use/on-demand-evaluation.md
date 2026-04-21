---
title: Use on-demand evaluation
description: Learn how to use on-demand evaluation in Dynamics 365 Customer Service and Dynamics 365 Contact Center to assess cases, conversations, and emails efficiently with AI-assisted, manual, or AI agent methods.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 04/02/2026
ms.custom: bap-template
---

# Use on-demand evaluation

**Conversations**: [!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

**Cases**: [!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]

**Email**: [!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]

Use on-demand evaluation to check cases, conversations, and emails. Request evaluations with AI-assisted, manual, or AI agent methods for flexible quality management. This article explains how to use on-demand evaluation, including prerequisites and step-by-step instructions.

> [!IMPORTANT]
>
> - Evaluation for emails is a preview feature. 
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520), and are available before an official release so that customers can get early access and provide feedback.

## Prerequisites

- Enable [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- Assign the required [roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).


## On-demand evaluation for cases

To request evaluations for multiple cases from the case grid:

1. Select the required records.
    
1. Select **Request evaluation**. You can select up to 20 records for evaluation. 

To request evaluation for a particular case:

1.  Go to **Cases**, select the required case, and then select **Request evaluation**.

1.  On the **Request evaluation** dialog, select the following:

    - **Evaluation criteria:** Search and select an evaluation criteria from the list of criteria.
    - **Evaluation method:** Select an evaluation method: **AI assisted**, **Manual**, or **AI agent**.
    - **Assigned to:** Select the user.
    - **Evaluation due date:** Select a due date for the evaluation.

1.  Select **Request**.

1.  Select **Submit and Close**. The **Evaluator status** appears as **Completed**. 

   When the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation    Summary** provided by Quality Evaluation Agent.

To view the evaluation record, in the site map of Copilot Service workspace:

- Go to **Cases** and then select a case. Go to **Related** > **Evaluations** to view the evaluation records.
- Go to **Evaluations**. The **All evaluations** data grid appears. Select the required evaluation record. The evaluation for the selected case appears in the **Evaluations** side pane.

## On-demand evaluation for conversations

To request evaluation for closed conversations:

1. Go to **Activities** > **Closed Conversations**.

1. Select a closed conversation, and then on the specific conversation, select **Request evaluation**.

1. On the **Request evaluation** dialog, select the following:

   - **Evaluation criteria:** Search and select an evaluation criteria.
   - **Evaluation method:** Select an evaluation method: **AI assisted**, **Manual**, or **AI agent**.
   - **Assigned to:** Select the user.
   - **Evaluation due date:** Select a due date for the evaluation.
    
1.  Select **Request**. 

1.  Select **Submit and Close**. The **Evaluator status** appears as **Completed**.

   When the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation    Summary** provided by Quality Evaluation Agent.

To view the evaluation record, in the site map of Copilot Service workspace:

- Go to **Conversations** and then select a conversation. Go to **Related** > **Evaluations** to view the evaluation records.
- Go to **Evaluations**. The **All evaluations** data grid appears. Select the required evaluation record. The evaluation for the selected conversation appears in the **Evaluations** side pane.

## On-demand evaluation for email (preview)

To request evaluation for emails:

1. Go to **Activities** and select the **Email** record type.
1. Select **Request evaluation**.
1. On the **Request evaluation** dialog, select the following:

   - **Evaluation criteria:** Search and select an evaluation criteria.
   - **Evaluation method:** Select an evaluation method: **AI assisted**, **AI agent**, or **Manual**.
   - **Assigned to:** Select the user.
   - **Evaluation due date:** Select a due date for the evaluation.

1. Select **Request**.

   When the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation Summary** provided by Quality Evaluation Agent.

You can also request an evaluation for an individual email record from the **Evaluation** tab within every email record.

> [!NOTE]
> If you select the **AI assisted** or **AI agent** evaluation method, make sure that **AI response enabled** is selected for your questions in the criteria, as follows:
>- For **AI agent** mode: All questions must be AI-enabled. Manual editing isn't allowed.
>- For **AI assisted** mode: At least one question must be AI-enabled.


## Related information

[Use evaluation plan](evaluation-plan.md)  
[Use evaluations](use-evaluations.md)  
[Use evaluation criteria](evaluation-criteria.md)  
[Manage Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md)