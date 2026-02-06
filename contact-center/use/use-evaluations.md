---
title: Use evaluations
description: Learn how to use evaluations to assess cases and conversations, access results, and improve quality with actionable insights and scoring details in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days 
ms.date: 02/06/2026
ms.custom: bap-template
---

# Use evaluations

**Conversations**: [!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

**Cases**: [!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]

Use evaluations to assess and improve the quality of cases and conversations. This article explains how to access evaluation results, understand scoring and compliance details, and interpret evaluation states.

## Prerequisites

- Enable [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- Assign the required [roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).


## Evaluations

To view evaluations for your criteria:
    
  1.  In the site map of Copilot Service workspace, go to **Evaluations**. The **All evaluations** data grid appears.
  You can view specific data by using filters such as **Evaluation Name**, **Score**, **Evaluation method**, **AI agent status**, **Evaluator status**, **Evaluation criteria**, **Evaluator expiration date**, and **Evaluator completion date**.
    
  2.  Select the required **Evaluation**. The evaluation for the case or conversation that you selected appears on the **Evaluations** side pane.
  

  If you enabled scoring for your criteria, you see the following details:
    
  - **Evaluation Summary**: Highlights evaluation results and suggests actions for improvement, like coaching opportunities for  representatives or specific activities to bring a case back on track. The Quality Manager and Quality Reviewer base these actions on evaluation results to improve the overall quality.
  
  - **Suggested actions**: Shows if any immediate actions are required or improvements that can be made.
  
  - **Scoring overview**: Shows the **Overall evaluation score**, including the **Total score** and **Scoring ratio**.
  
  If you have extended the evaluation criteria, you see the following:

  - **Source criteria evaluation** and **Extend criteria evaluation** details.

  If you’ve edited and published an evaluation plan and added the **Version** column to the grid, you can view the details of each version.

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

[Manage Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md)  
[Use evaluation plan](evaluation-plan.md#)  
[Use evaluation criteria](evaluation-criteria.md)