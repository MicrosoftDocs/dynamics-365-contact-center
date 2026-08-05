---
title: Use evaluations
description: Learn how to use evaluations to assess cases and conversations, access results, and improve quality with actionable insights and scoring details in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 08/05/2026
ms.custom: bap-template
---

# Use evaluations

**Conversations**: [!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

**Cases**: [!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]

Use evaluations to assess and improve the quality of cases and conversations. This article explains how to access evaluation results, understand scoring and compliance details, and interpret evaluation states.

## Prerequisites

- Enable [quality evaluation](../administer/manage-quality-evaluation-agent.md).
- Assign the required [roles and privileges](../administer/manage-quality-evaluation-agent.md#roles-and-privileges).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).

## View evaluations

To view evaluations for your criteria:
    
1. In the site map of Copilot Service workspace, go to **Evaluations**. The **All evaluations** data grid appears.
   You can view specific data by using filters such as **Evaluation Name**, **Score**, **Evaluation method**, **AI agent status**, **Evaluator status**, **Evaluation criteria**, **Evaluator expiration date**, and **Evaluator completion date**.
    
1. Select the required **Evaluation**. The evaluation for the selected case or conversation appears in the **Evaluations** side pane. Evaluations return results in the language in which the criteria were created.

If scoring is enabled for your criteria, the following details appear:
    
- **Evaluation Summary**: Highlights evaluation results and suggests actions for improvement, like coaching opportunities for representatives or specific activities to bring a case back on track. The **Quality Manager** and **Quality Reviewer** use these insights to improve the overall quality.
  
- **Suggested actions**: Shows if any immediate actions are required or improvements that can be made.
  
- **Scoring overview**: Shows the **Overall evaluation score**, including the **Total score** and **Scoring ratio**.
  
If you extended the evaluation criteria, the **Source criteria evaluation** and **Extend criteria evaluation** details appear.

If you edited and published an evaluation plan and added the **Version** column to the grid, the details of each version appear.

### Evaluation states

**Evaluator status**: 

The grid displays the following evaluator and AI agent states.

| State  | What it indicates  |
|--------|--------------------|
| Pending         | The evaluation hasn't started.  |
| In-progress     | The evaluator is completing the evaluation. |
| Completed       | The evaluator finished and submitted the evaluation.  |
| Expired         | The due date provided in the evaluation criteria expired and the evaluator can no longer open the evaluation. |
| Not applicable  | The AI agent is in **Error** status, so the evaluator can't complete the evaluation. |

**AI agent status**:

|State | What it indicates|
|-------|-----------------|
| Pending| The evaluation hasn't started. |
| In-progress | The evaluation is in progress. |
| Completed| The evaluation is complete. |
| Error | The AI agent encountered an error during the evaluation. |
| Not applicable| The evaluation doesn't use an AI agent and is completed manually. |

## Edit submitted evaluations

Edit evaluations and modify responses in an evaluation after it's submitted. When you submit an evaluation, it initially appears in a read-only view. Select **Edit** to update answers and then submit the changes. Changes don't take effect until you resubmit the evaluation plan.

> [!NOTE]
> You can't edit evaluations that are in **In progress** status. The **Edit** action remains disabled for nonsubmitted evaluations.

### Requirements to edit an evaluation

Before you edit a submitted evaluation, make sure that you meet the following requirements.

- The evaluation must be **submitted (completed)**.
- You have the **Quality Admin** or the **Quality Manager** role, or the **Override submitted evaluation** (Miscellaneous privilege) added to your role. In Power Platform admin center, search for the **Evaluation (msdyn_evaluation)** table and the **Miscellaneous privileges** > **Override Submitted evaluation (prvOverrideSubmittedEval)** privilege. Learn more in [User management](/dynamics365/customer-service/implement/overview-users).

To edit:

1. In the site map of Copilot Service workspace, go to **Evaluations** in **Service**.
1. Select and open an evaluation with the status **Completed**. The evaluation opens in a read-only view and indicates that it's submitted.
1. Select **Edit**. The evaluation switches to **Edit** mode and indicates that you can update responses and submit when ready.
1. Update the answers as required.
1. Select **Submit** to apply your changes. Your changes don't take effect until you submit. After you submit, the evaluation returns to the submitted (read-only) state.

## Regenerate evaluation summaries

As an evaluator, when you update evaluation responses, the system regenerates the summary upon submission to reflect the finalized evaluation. If you don't make any changes, the system skips summary regeneration to optimize performance and cost.

When enabled, the **Evaluation Summary** section includes a **Regenerate summary** option that you can use to:

- Generate summaries for manual evaluations.
- Regenerate summaries for completed AI-assisted and AI Agent evaluations.
- Update summaries after modifying evaluation responses.
- View the summary generation status and the last generated date and time.

Learn more about the admin settings to enable the feature in [Manage quality evaluation](../administer/manage-quality-evaluation-agent.md).

## Troubleshoot failed quality evaluations

If a quality evaluation doesn't complete successfully, refer to the [Troubleshoot failed quality evaluations](/troubleshoot/dynamics-365/customer-service/omnichannel-for-customer-service/quality-evaluation-retry) article to determine the cause and resolve the problem.

## Related information

[Manage quality evaluation](../administer/manage-quality-evaluation-agent.md)  
[Use evaluation plan](evaluation-plan.md)  
[Use evaluation criteria](evaluation-criteria.md)
