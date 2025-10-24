---
title: Use evaluations
description: Learn how to use evaluations to assess cases and conversations, access results, and improve quality with actionable insights and scoring details in in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot 
ms.date: 10/24/2025
ms.custom: bap-template
---

# Use evaluations

Use evaluations to assess and improve the quality of cases and conversations. This article explains how to access evaluation results, understand scoring and compliance details, and interpret evaluation states.

> [!IMPORTANT]
>
> - Evaluations for conversations is a preview feature. 
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520), and are available before an official release so that customers can get early access and provide feedback.

## Prerequisites

- You have enabled [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- You have the required [Roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges)
- You have [set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- You provided consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).


## Evaluations

To view evaluations for your criteria:
    
  1.  In the site map of Copilot Service workspace, go to **Evaluations**. The **All evaluations** data grid appears.
  You can view specific data by using filters such as **Evaluation Name**, **Score**, **Evaluation method**, **AI agent status**, **Evaluator status**, **Evaluation criteria**, **Evaluator expiration date**, and **Evaluator completion date**.
    
  2.  Select the required **Evaluation**. The evaluation for the case or conversation that you selected appears on the **Evaluations** side pane.

  If you have enabled scoring for your criteria, you see the following:
    
  - **Evaluation Summary:** Highlights evaluation results and suggests actions for improvement, like coaching opportunities for  representatives or specific activities to bring a case back on track. The Quality Manager and Quality Reviewer base these actions on evaluation results to improve the overall quality.
  - **Suggested actions**: Shows if any immediate actions are required or improvements that can be made.
    
  - **Scoring overview:** Shows the **Overall evaluation score**, including the **Total score** and **Scoring ratio**.
    
  If you have extended the evaluation criteria, you see the following:
    
  - **Source criteria evaluation** and **Extend criteria evaluation** details.

### Evaluation states

**Evaluator status**: 

You see the following evaluator and AI agent states on the grid.

| State  | What it indicates  |
|--------|--------------------|
| Pending         | The evaluation hasn’t started.  |
| In-progress     | The evaluator is filling in the evaluation. |
| Completed       | The evaluator has finished and submitted the evaluation.  |
| Expired         | The due date provided in the evaluation criteria has expired, and the evaluator can no longer open the evaluation. |
| Not applicable  | The AI agent is in **Error** status, and therefore the evaluator can’t evaluate. |

**AI agent status**:

|State | What it indicates|
|-------|-----------------|
| Pending| The evaluation hasn’t started. |
| In-progress | Evaluation is in progress |
| Completed| Evaluation is complete. |
| Error | AI agent shows errors due to issues. |
| Not applicable| Evaluation isn’t using an AI agent and a manual review is performed. |

## Related information

[Manage Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent)  
[Use evaluation plan](evaluation-plan.md#use-evaluation-plan)  
[Use evaluation criteria](evaluation-criteria.md#use-evaluation-criteria)
