---
title: Use evaluation criteria
description: Learn how to use, edit, and extend evaluation criteria to assess cases and conversations effectively in Dynamics 365 Customer Service.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection:
ms.date: 10/14/2025
ms.custom: bap-template 
---

# Use evaluation criteria

This article explains how to use, edit, and extend evaluation criteria, including best practices for creating clear and actionable instructions. Learn how to leverage built-in criteria, customize evaluation plans, and optimize quality assessments for your organization.

## Prerequisites

- You have enabled [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- You have the required [Roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges)
- You have [set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- You provided consent for potential [data movement across regions][Data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).

### Use the out-of-the-box evaluation criteria

As a quality evaluation supervisor, you can use or copy the default evaluation criteria, create a new evaluation criteria, and edit a published evaluation criteria, to evaluate your cases and conversations. 

- Use the **Support quality** evaluation criteria for both cases and conversations. 
- Use the **Closed Conversations Default Criteria** for conversations only.

> [!NOTE]
> The default evaluation criteria is pre-filled, published, and read-only.

To view an evaluaton criteria:

1.  In site map of Copilot Service workspace, go to **Evaluation criteria.**

1.  On the **Evaluation criteria** page, depending on your record type, select the default evaluation criteria to view the details.

### Edit your published evaluation criteria

You can edit your published evaluation criteria.

1. In site map of Copilot Service workspace, go to Evaluation **criteria.**

1. On the **Evaluation criteria** page, select the default evaluation criteria, as required.
1. On the selected evaluation criteria page, select **Edit**.
1. Save the changes. The criteria is saved as a draft. You can also revert to the published criteria at this stage.
1. Publish the changes. 

> [!NOTE]
> - You can't change the scoring toggle at the criteria level after the criteria is published.
> - Any evaluation plan that's still running continues to use the existing criteria. After you publish the edited evaluation criteria, evaluation plans use the latest criteria in the next run.

### Extend your evaluation criteria

After you create a baseline criteria for your business unit, you can extend it to fit your organizational requirements. Updates to the baseline criteria automatically appear in all extended criteria. Select any custom evaluation criteria in the **Published** state as source criteria to extend it further.

1.  Select a criteria and then select **Extend criteria**. The **New extended evaluation criteria** page appears.

1.  In the **Extended criteria details** section, enter the following details:

    1.  **Criteria name**: Provide a name.

    1.  **Description**: Provide a description. To provide your own
        instructions, turn off the **Use source instructions** toggle.
        To use the source instructions, turn on the **Use source
        instructions** toggle.

    1.  **Extended scoring weight**: If the source criteria has scoring
        criteria enabled, provide the extended scoring weight.

    1.  **Source scoring weight**: Gets auto calculated, depending on
        the extended scoring criteria.

1.  Select **Add question** to add questions to the extended criteria.

1.  Select **Save** and then select **Publish**.

    > [!NOTE]
    > - The **Source criteria details** in the **Extended criteria details** page isn’t editable. However, if you make updates to the source criteria, the extended criteria is updated as well.
    > - The **Criteria scoring** reflects the selection you made in the source criteria.
    > - You can’t extend an out-of-the-box criteria, for example, **Support quality**.

### Copy the default quality evaluation criteria for cases and conversations

1. Select the checkbox for the default criteria and then select **Copy**. A copy of the prefilled default criteria form is provided to you as the source. You can make edits as needed.

1. Select **Save**, once you are done making edits.

### Create a scoring evaluation criteria

1.  On the **Evaluation criteria** page, select **New**.

1.  On the **New evaluation criteria** page, in the **Criteria details** section, provide the **Criteria name** and **Description**.

1.  In the **Add form level instructions**, provide instructions, if any.

1.  In **Section 1**, enter the following details:

    1.  **Section name**: Provide a name.

    1.  **Description**: Provide a description.

    1.  **Section weight (%)**: Provide a weightage for the evaluation criteria. The weight % across sections should add up to 100.

1.  Select **Add question,** if you want to add a question.

    For every question,

    1.  **Select answer type**: Select from the options, **Yes/No**, **Multiple choice**, **Choose from list**, or **Text selection**.

    1.  **Form question text**: Enter the form question text.

    1.  **Add question-level instructions**: Provide instructions for the question, if any. Instructions help Quality Evaluation Agent predict answers and improve accuracy.

    1.  Depending on the answer type you select, you can add scoring for the answers by selecting the **Scoring enabled** checkbox.

1.  For **Answer options,** depending on the answer type you select, the answer options appear. Provide **answer-level instructions** for your answers, as required.

1.  You can select **Delete section** or **Duplicate section** or **Delete question** or **Duplicate question** for sections or
    questions, respectively.

1.  Select **Save** and then select **Publish**.

#### Best practices

- **Criteria-level instructions:** Define instructions that apply to the entire evaluation criteria. Include overarching goals, expectations, and constraints to guide Quality Evaluation Agent behavior across all questions and answers.

- **Question-level instructions**: Provide specific instructions for each question to guide the Quality Evaluation Agent’s evaluation. These instructions are scoped to the question only, and don’t influence other parts of the evaluation.

- **Answer-level instructions**: Include answer-specific instructions for each answer option to help the Quality Evaluation Agent understand the intent and context of the response.

- **Answer choices**: Clearly define answer options, especially for multi-choice or list-type questions. Ensure that you include fallback options to handle ambiguous or unexpected responses.

- **Clarity drives accuracy**: Use precise and detailed instructions to improve the accuracy of Quality Evaluation Agent evaluations. Avoid vague language and ensure that all instructions are explicit, contextual, and actionable.

- **Question text**: Define each evaluation question to assess a single, well-defined objective to help ensure clarity and direct alignment with the answer options.
