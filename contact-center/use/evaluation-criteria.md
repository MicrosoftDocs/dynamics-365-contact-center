---
title: Use evaluation criteria
description: Learn how to create, edit, extend, and test evaluation criteria for quality evaluations in Dynamics 365 Customer Service and Dynamics 365 Contact Center.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 11/12/2026
ms.custom: bap-template 
---

# Use evaluation criteria

Evaluation criteria define the questions, instructions, and scoring that you use to assess cases and conversations in Dynamics 365 Customer Service and Dynamics 365 Contact Center.

Learn how to use built-in criteria, create and customize criteria, configure scoring, manage versions, test with simulations, extend criteria across business units, and link knowledge articles to guide evaluations.

## Prerequisites

Before you create evaluation criteria, complete the following tasks:

- Enable [Quality evaluation](../administer/manage-quality-evaluation-agent.md).
- Complete prerequisites to use knowledge sources in evaluation criteria.
- Assign required [roles and privileges](../administer/manage-quality-evaluation-agent.md#roles-and-privileges).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).

## Use the out-of-the-box evaluation criteria

As a Quality Evaluator, you can use or copy the out-of-the-box evaluation criteria, create a new evaluation criteria, and edit published evaluation criteria. 


> [!NOTE]
> The out-of-the-box evaluation criteria are prefilled, published, and read-only.

To view evaluation criteria, complete the following steps:

1. In the site map of Copilot Service workspace, go to **Evaluation criteria**.

1. On the **Evaluation criteria** page, select the out-of-the-box evaluation criteria to view the details.

## Create evaluation criteria

Refer to the [limitations](#limitations-for-evaluation-criteria) and [instructions for evaluation criteria](#best-practices-for-evaluation-criteria) when you create evaluation criteria.

1. On the **Evaluation criteria** page, select **New**.

1. On the **New evaluation criteria** page, in the **Criteria details** section, enter the **Criteria name** and **Description**.

1. Turn on the **Criteria scoring** toggle to enable scoring per criteria.

1. Turn on the **Allow scoring for question** toggle to define weights per question within a section.

1. Select your language from the **Language** dropdown list. By default, all existing criteria are in English. You can't change the language after you save a criteria, even in the **Draft** state. Evaluation results are returned in the same language.

1. In the **Knowledge sources** section, turn on the **Link knowledge article** toggle, if you want to associate published knowledge articles to an evaluation criteria. Learn more in [Use knowledge sources in evaluation criteria](#use-knowledge-sources-in-evaluation-criteria).

    - In **Knowledge source**, add a published knowledge article. The latest version of the article is used.

    - Define the evaluation criteria questions.

    - For applicable questions, turn on the toggle to use a knowledge source and link the knowledge article.

    - Provide any supplemental instructions required for the question.

1. In the **Add form level instructions** section, enter instructions, if any.

1. In **Section 1**, enter the following details:

    - **Section name**: Enter a name.

    - **Description**: Enter a description.

    - **Section weight (%)**: Assign a weight to the evaluation criteria. The total weight across sections must equal 100%.

1. Select **Add question** if you want to add a question.

    For each question, enter the following details:

    - **Select answer type**: Select from the options, **Yes/No**, **Multi-select**, **Single-select**, or **Descriptive**.

    - **Form question text**: Enter the form question text.

    - **Add question-level instructions**: Enter instructions for the question, if any. Instructions help generate evaluation answers and improve accuracy.

    - **Allow Not Applicable responses**: Select to allow evaluators to mark the question as not applicable. When selected, other answer choices are cleared, and the question is excluded from the evaluation score. The score is calculated based only on applicable questions. Learn more in [Overall evaluation score](evaluation-plan.md#overall-evaluation-score).

    - Select **AI response enabled** to allow AI to predict an answer for this question. If you don't select this option, AI doesn't process the input or return an answer. Evaluation creation fails if the criteria lacks AI-enabled questions for the selected mode in an evaluation plan, as follows:

    - **AI agent mode**: All questions must be AI-enabled. Manual editing isn't allowed.
    - **AI assisted mode**: At least one question must be AI-enabled.

        This requirement applies to both on-demand evaluations and evaluation plans.

    - Depending on the answer type, select **Scoring enabled** to add scoring. Turn off the scoring toggle if you don't want to create a criteria with scoring.

    - Select **Mark as critical question** if you want the question to be marked as critical. Learn more in [Mark a question as critical](#mark-a-question-as-critical).

1. For **Answer options** depending on the answer type you select, the answer options appear. In **Answer options**, provide answer-level instructions for each answer. If you marked the question as critical, you must select the **Mark as fail** option for an answer to avoid errors.

    You can delete or duplicate a section or question, as required.

1. Select **Save**, and then select **Publish**.

## Define scores for your evaluation criteria

Quality evaluation uses a weighted scoring model that calculates scores at the question level, aggregates them into section scores, and then combines those scores to determine the overall evaluation score.

Every evaluation is built from the following levels:

| Level | Component | Description |
|-------|-----------|-------------|
| 1 | Evaluation criteria | The top-level scoring framework that you configure. It defines the overall structure, sections, and weight for an evaluation. |
| 2 | Sections | Groups of related questions. Each section has a percentage weight. All section weights must total 100%. |
| 3 | Questions | Individual questions within each section. Each question is scored on a scale of 0 to 100. |

### Section scoring

A section's contribution to the overall score depends on the section weight and the scores of the questions in that section.

**Equal distribution (default)**: When you don't configure question-level weights, the model distributes the section weight equally across all questions in the section. The model calculates the section score by using the following formula:

Section score = Average of all question scores × Section weight percentage

### Question-level weighting

When you configure question-level weights, the system calculates scores by using the assigned weight of each question. This approach lets organizations give greater importance to specific questions based on business requirements. The weighted question scores are then aggregated to calculate the section score and overall evaluation score.

> [!NOTE]
> You enable question-level weighting through a separate toggle. It doesn't affect previously created criteria unless administrators choose to enable the feature.

When you enable question-level weighting:

- Each section must still have a total section weight percentage.
- You can assign specific weight percentages to individual questions within a section.
- The combined weight of all questions in a section can't exceed the section's assigned weight.
- Validation messages appear when the total question weights exceed the section weight limit.

**Question scoring**: Each question produces a score between 0 and 100. The scoring method depends on the question type.

- For **Yes/no** and **single-answer** questions:

  - A correct answer scores 100.
  - An incorrect answer scores 0.

- For multi-select questions:

  - All option set values within a question must total exactly 100.
  - The question score equals the sum of points for the selected answers, capped at 100.
  - Selecting an incorrect option doesn't reduce the score. There are no penalties.

- For single-select questions:

    Single-select questions allow evaluators to choose one option from a predefined list. Supervisors assign a score (0-100) to each option, and the selected option determines the question score. Option scores don't need to add up to 100.

    Example: Excellent = 100, Good = 75, Needs Improvement = 50, Poor = 0. If Good is selected, the question score is 75/100.

    For **Descriptive** questions, there's no scoring.

### Scoring with extended criteria

Extended criteria (child criteria) let organizations enforce a shared evaluation baseline while allowing individual business units to add their own evaluation questions.

When an evaluation runs against extended criteria, the score is calculated in two parts:

- **Parent portion score**: Scored by using the standard section and question scoring logic from the source criteria.
- **Child portion score**: Scored by using the standard section and question scoring logic from the extended criteria.

At the extended-criteria level, admins assign a percentage weight to the parent portion and a percentage weight to the child portion. The parent and child weights must total 100%.

Final score = (Parent portion score × Parent weight percentage) + (Child portion score × Child weight percentage)

## Mark a question as critical

Turn on **Mark as critical question** to designate a question as critical within a criteria. Critical questions highlight requirements such as compliance, safety, or required process steps.

If a critical question is answered with a fail option, the entire evaluation or simulation fails. You can mark multiple questions as critical within a criteria, but each critical question must have at least one fail option configured. If not, an error appears. Scoring doesn't change when a critical question causes an evaluation to fail.

During simulations and evaluations, the results indicate whether a critical question caused the failure. The critical question information is shown at both in the **Evaluation Summary** level and at the individual question level in the side panel. Additionally, the evaluations grid also includes a column that identifies evaluations that failed due to a critical question.

The following examples show questions where a failure should immediately fail the entire evaluation:

- Did the correct action get selected when prompted with a compliance checkpoint?
(Fail if an incorrect action was chosen.)

- Was customer consent obtained before recording the call?
(Fail if consent wasn't explicitly confirmed.)

## Edit your published evaluation criteria

You can [copy the default evaluation criteria](#copy-the-default-evaluation-criteria-for-cases-and-conversations) or create new evaluation criteria and then make edits.

To edit your published evaluation criteria, complete the following steps:

1. In the site map of Copilot Service workspace, go to **Evaluation criteria**.
1. On the **Evaluation criteria** page, select the evaluation criteria you want.
1. On the selected evaluation criteria page, select **Edit**.
1. Save the changes. The criteria is saved as a draft. You can also revert to the published criteria at this stage.
1. Publish the changes. 

> [!NOTE]
> - You can't change the scoring toggle at the criteria level after you publish the criteria.
> - Evaluation plans that are already running continue to use the existing criteria. After you publish the updated criteria, evaluation plans use the latest criteria in the next run. 

## Manage evaluation criteria versions

Each edit and publish action increments the evaluation criteria version. The latest published version is always used for new evaluations. Supervisors can review prior versions, restore any version to make it the current one, or discard draft changes as needed.

1. Select the source criteria and go to the **Versioning History** tab to view versions and version numbers along with the latest data that might be added to the criteria.
1. Select **Record** to go to a specific version and view the details in read-only mode.
1. Select **Restore/Publish** to republish the selected version as the latest. This action discards the current draft and increments the version number of the published criteria.

You can also add the **Version** column to the evaluation grid to track versions. Learn more in [Evaluations](use-evaluations.md).

## Create and run a simulation

Before you run a simulation, you need to enable the **QEA Simulation** flow. Learn more in [Configure connection references](/dynamics365/customer-service/administer/admin-km-agent-connections#set-up-connection-references-for-quality-evaluation).

Supervisors can select any criteria in **Draft** or **Published** state and run a simulation test with real case and conversation data to preview quality evaluation prediction outcomes.

> [!NOTE]
> You can't include attachments for case data.

To create and run a simulation:

1. Select the criteria, and then select **Create Simulation**.
1. On the **New Criteria Simulation** page, **General** tab, **Simulation overview** section, enter the following information:
    1. **Criteria Name**: Enter a name.
    1. **Record Type**: Select **Case** or **Conversation**.
    1. **Criteria Version**: Select the version of the published criteria. Criteria in **Draft** state don't have a version assigned.
1. **Conditions**: Select the conditions to run a simulation.
By default, the simulation runs on the 25 most recent records that match the selected conditions.
1. Save the changes.
1. Select **Run Simulation**. Your criteria simulation record is created. 
1. Select the **Simulation Results** tab to view the simulation results.

You can also view the simulation details from the **Simulation Run** tab of your criteria. You can view details such as **Evaluation Criteria version**, **Record Type**, **Status**, and **Created On** data. 
1. Select a simulation record that's in **Completed** state.
1. From the simulation record page, select the **Simulation Results** tab and then select the required simulation result to view the prediction done by the quality evaluation on the side pane.

Supervisors can view simulation results. The results don't affect records or quality metrics, so you can validate and refine criteria before publishing. Each simulation consumes [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go).

## Extend your evaluation criteria

After you create source criteria for your business unit, you can extend the criteria to suit your organizational requirements. Updates to the source criteria automatically appear in all the extended criteria. Select any custom evaluation criteria in the **Published** state as source criteria to extend.

1.  Select the criteria, and then select **Extend criteria**. The **New extended evaluation criteria** page appears.

1.  In the **Extended criteria details** section, enter the following details:

    1.  **Criteria name**: Enter a name.

    1.  **Description**: Provide a description. To provide your own instructions, turn off the **Use source instructions** toggle.
        To use the source instructions, turn on the **Use source instructions** toggle.

    1.  **Extended scoring weight**: If the source criteria has scoring criteria enabled, provide the extended scoring weight.

    1.  **Source scoring weight**: Calculated automatically from the extended scoring weight.

1.  Select **Add question** to add questions to the extended criteria.

1.  Select **Save**, and then select **Publish**.

    > [!NOTE]
    > - The **Source criteria details** on the **Extended criteria details** page isn't editable. However, if you make updates to the source criteria, the extended criteria updates.
    > - The **Criteria scoring** reflects the selection you made in the source criteria.
    > - You can't extend an out-of-the-box criteria such as, **Support quality**.

## Copy the default evaluation criteria for cases and conversations

1. Select the checkbox for the default criteria, and then select **Copy**. You receive a copy of the prefilled default criteria form as the source. You can make edits as needed.

1. Select **Save** when you finish making edits.

## Use knowledge sources in evaluation criteria

Knowledge adherence enables evaluators to use knowledge articles as reference sources for specific evaluation questions. During evaluation, the system retrieves relevant information from the linked articles and uses it to generate responses. The feature uses existing knowledge base assist retrieval capabilities and requires Dataverse Copilot provisioning for knowledge retrieval.

When an evaluation runs, the agent grounds its scoring against the linked article and cites the reasoning from the knowledge article sources, which helps your organization enforce their own evaluation policies.

For any case, you can view the criteria and the knowledge source used for the answers provided in the evaluation summary. You can also select the knowledge article link to view the article.

### Prerequisites for knowledge sources

- Knowledge-source-based evaluation criteria is enabled in your environment.
- A published knowledge article exists in Dynamics 365.
- You have permissions to create and manage evaluation criteria.
- Dataverse Copilot provisioning and knowledge sources are enabled from the Copilot Service admin center.

### Limitations

- You can add one knowledge article per criteria and link the article to two knowledge-enabled questions per criteria.
- Supported for the case entity and for on-demand evaluations only.
- Simulation on knowledge criteria isn’t supported.
- Knowledge sources can't be added if the character limit of the criteria has been reached.
- Only Dynamics 365 knowledge articles are supported.

## Best practices for evaluation criteria

Learn more in [Write instructions for evaluation criteria](evaluation-criteria-best-practices.md).

## Limitations for evaluation criteria

**Question limits**

- By default, each evaluation criteria can include up to 50 questions. This limit applies to the entire criteria, not to each section.
- You can distribute questions across sections in any combination, as long as the total number of questions doesn't exceed 50.
- When you reach the limit:
    - You can't add or duplicate questions.
    - You can't add or duplicate sections if doing so would exceed the limit.


**Character limits for criteria content**

The following per-field character limits apply to all instruction types (criteria-level, question-level, and option-level):

|Field | Limit  |
|---------|---------|
|Instructions     |     2,000 characters     |
|Question text    |  300 characters       |
|Option text    |   100 characters      |

**Character limits by language**

The system monitors the total character count and displays a warning when content exceeds the recommended limit for the selected language. Recommended limits vary by language category:

- 90,000 characters for most languages.
- 60,000 characters for some languages, such as Arabic.
- 30,000 characters for languages with higher token expansion.

The recommended character limit updates dynamically when you change the selected language. For example, switching from English to Arabic reduces the limit from 90,000 to 60,000 characters. The system evaluates limits based on the language selected in the criteria settings.

When you exceed limits:

- A warning banner appears, indicating that evaluation accuracy might be affected. You can still save and use the criteria.
- An error message appears if content exceeds 700,000 characters, which prevents you from saving the criteria.

**Extended criteria**

Creating extended criteria introduces a parent-child relationship between source criteria and extended criteria.

- Question limits: The system enforces question limits independently for parent and child criteria, with up to 50 questions each.
- Character limits: The system calculates recommended character limits (for example, 90,000 characters) by using both parent and child content combined.

|Limit type  | Behavior  |
|---------|---------|
|Question count     |  50 total per criteria        |
|Recommended size    |   Language-specific warning appears   |
|Hard size limit    |   Approximately 700,000 characters; saving is blocked      |
|Instruction limit    |    2,000 characters    |

## Related information

[Manage quality evaluation](../administer/manage-quality-evaluation-agent.md)  
[Use evaluation plans](evaluation-plan.md)  
[Use evaluations](use-evaluations.md)  
[Troubleshoot failed quality evaluations](/troubleshoot/dynamics-365/customer-service/omnichannel-for-customer-service/quality-evaluation-retry)