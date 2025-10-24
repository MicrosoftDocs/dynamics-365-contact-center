---
title: Use on-demand evaluation
description: Learn how to use on-demand evaluation to assess cases and conversations efficiently with AI-assisted, manual, or AI agent methods.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: conceptual
ms.collection:
ms.date: 10/23/2025
ms.custom: bap-template
---

# Use on-demand evaluation

> [!IMPORTANT]
>
> - Evaluations for conversations is a preview feature and is available in Dynamics 365 Contact Center only. 
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520), and are available before an official release so that customers can get early access and provide feedback.

Use on-demand evaluation to check cases and conversations. Request evaluations with AI-assisted, manual, or AI agent methods for flexible quality management. This article explains how to use on-demand evaluation, including prerequisites and step-by-step instructions.

## Prerequisites

- You have enabled [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- You have the required [Roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges)
- You have [set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- You provided consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).


## On-demand evaluation for cases

To request evaluations for multiple cases from the case grid:

1. Select the required records.
    
1.  Select **Request evaluation**. You can select up to 20 records for evaluation. 

To request evaluation for a particular case:

1.  Go to **Cases**, select the required case, and then select **Request evaluation**.

1.  On the **Request evaluation** dialog, select the following:

    1.  **Evaluation criteria:** Search and select an evaluation criteria from the list of criteria.

    1.  **Evaluation method:** Select an evaluation method: **AI assisted**, **Manual**, or **AI agent**.

    1.  **Assigned to:** Select the user.

    1.  **Evaluation due date:** Select a due date for the evaluation.

3.  Select **Request**.

4.  Once the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation    Summary** provided by Copilot.

5.  Select **Submit and Close**. The **Evaluator status** appears as **Completed**.

## On-demand evaluation for conversations

To request evaluation for closed conversations:

1. Go to **Activities** > **Closed Conversations**.

1. Select a closed conversation, and then on the specific conversation, select **Request evaluation**.

1. On the **Request evaluation** dialog, select the following:

    1.  **Evaluation criteria:** Search and select an evaluation criteria from the list of criteria.
    
    1.  **Evaluation method:** Select an evaluation method: **AI assisted**, **Manual**, or **AI agent**. If you select **AI agent**, the **Assigned to** and **Evaluation due date** is turned off.
    
    1.  **Assigned to:** Select the user.
    
    1.  **Evaluation due date:** Select a due date for the evaluation.
    
1.  Select **Request**. 

1. Once the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation    Summary** provided by Copilot.

1.  Select **Submit and Close**. The **Evaluator status** appears as **Completed**.


## Related information

[Use evaluation plan](evaluation-plan.md#use-evaluation-plan)  
[Use evaluations](use-evaluations.md#use-evaluations)  
[Use evaluation criteria](evaluation-criteria.md#use-evaluation-criteria)  
[Manage Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent)