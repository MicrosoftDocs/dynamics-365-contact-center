---
title: Use evaluations
description: Learn how to use evaluations to assess cases and conversations, access results, and improve quality with actionable insights and scoring details.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: 
ms.date: 10/15/2025
ms.custom: bap-template
---

# Use evaluations

Use evaluations to assess and improve the quality of cases and conversations. This article explains how to access evaluation results, understand scoring and compliance details, and interpret evaluation states.

## Prerequisites

- You have enabled [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- You have the required [Roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges)
- You have [set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- You provided consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).


The **Evaluations** side pane shows evaluations for cases and closed conversations.

- **Evaluation Summary:** Highlights evaluation results and suggests actions for improvement, like coaching opportunities for  representatives or specific activities to bring a case back on track. The Quality Manager and Quality Reviewer base these actions on evaluation results to improve the overall quality.

    You can view specific data by using filters such as **Evaluation method**, **AI agent status**, **Evaluator status**, **Evaluator due date**, **Evaluator Completion date**.
    
    1.  In Copilot Service workspace, go to **Evaluations**. The **All evaluations** data grid appears.
    
    2.  Select the required case or conversation record type.
    
    3.  The case or conversation appears with the **Evaluation Summary** and **Suggested actions.**

- **Scoring overview:** You see this overview if you have extended your evaluation criteria. Shows the **Overall evaluation score**, **Compliance score**, and the **Quality and compliance score**, including the **Total score** and **Scoring ratio**.

- **Compliance:** Shows the **Total score** with a **Scoring breakdown.** For every question, you see a **About this answer** that
  shows you the question-level calculation breakdown.

- **Quality compliance:**

### Evaluation states

**Evaluator status**: 

You see the following evaluator and AI agent states on the grid.

| State  | What it indicates  |
|--------|--------------------|
| Pending         | The evaluation hasn’t started.                                                    |
| In-progress     | The evaluator is filling in the evaluation                                        |
| Completed       | The evaluator has finished and submitted the evaluation.                          |
| Expired         | The due date provided in the evaluation criteria has expired, and the evaluator can no longer open the evaluation. |
| Not applicable  | The AI agent is in Error status, and therefore the evaluator can’t evaluate.      |

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
