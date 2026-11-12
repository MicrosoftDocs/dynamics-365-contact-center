---
title: Write instructions for evaluation criteria
description: Learn how to write criteria, question, and answer instructions that help Quality Evaluation Agent return consistent, accurate evaluation results.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 11/12/2026
ms.custom: bap-template 
---

# Write instructions for evaluation criteria

Effective instructions help Quality Evaluation Agent apply your evaluation criteria consistently and select the appropriate answer for each question. Write instructions as explicit decision rules that the agent can apply to the data included in the evaluation.

This article explains how to write criteria-level, question-level, and answer-level instructions, avoid common instruction patterns that cause inconsistent results, and test your criteria before publishing them.

## How instructions are used

An evaluation criteria contains categories, questions, and answer options. During an evaluation, Quality Evaluation Agent processes all enabled questions and returns an answer and supporting reason for each question.

The agent uses the following instruction fields:

| Instruction field | Purpose |
|---|---|
| Criteria instructions | Define rules that apply to every category and question, such as scope, evidence requirements, and tie-breaking behavior. |
| Question instructions | Define what the agent must evaluate and how it must assess the available evidence. |
| Answer instructions | Define the conditions for selecting a specific answer option. |

> [!IMPORTANT]
> Place evaluation guidance in the criteria, question, or answer instruction fields. The agent doesn't use descriptions, scores, or category weights to select an answer. Scores and weights are applied after the evaluation to calculate the final score.

Each criteria, question, and answer instruction field supports up to 2,000 characters. The limit is validated when you publish the criteria.

## Before you write instructions

Before you create instructions, confirm that the evaluation input includes the data required to answer each question. For example, don't ask the agent to evaluate an email response if the evaluation input doesn't include the email body.

Also consider the following system behaviors:

- The agent bases its response on the text and structured values included in the evaluation input.
- The agent can't evaluate UI elements, colors, icons, screenshots, or data that the evaluation input doesn't include.
- The evaluation output redacts or paraphrases personally identifiable information.
- Borderline questions can produce different results when multiple answers are defensible. Explicit decision rules reduce this variation.

## Write criteria instructions

Use criteria instructions to define rules that apply to the entire evaluation. Include the following information:

- **Scope:** Identify the people, actions, communications, and data that the agent must evaluate. Also identify anything that must be excluded.
- **Evidence:** Require answers to be based on observable information in the evaluation input. Don't allow unsupported assumptions.
- **Tie-breaking:** Specify which answer to select when the evidence partially supports more than one option.
- **Completeness:** Require every condition for an answer to be met when the instructions define a checklist.
- **Independence:** Require each question to be evaluated independently.
- **Timeline:** If sequence matters, instruct the agent to use dates and timestamps to construct the interaction timeline.

The following example shows criteria instructions for evaluating email-based customer service cases:

Apply these rules to every question:

1. Base each answer only on evidence in the case data. Don't infer intent or assume that an undocumented action occurred.
2. If evidence supports both a higher and a lower answer, select the lower answer. Select the highest answer only when all its conditions are met.
3. When an answer includes a checklist, require every checklist item to be met.
4. Evaluate each question independently.
5. Evaluate only the representative's actions and customer-facing communications unless a question specifies otherwise. Exclude customer behavior, automated messages, and internal notes unless the question includes them.
6. When sequence matters, use the available dates and timestamps to construct the case timeline.

## Write question instructions

Question instructions define what the agent must evaluate. Write them as observable checks instead of subjective judgments.

For example, replace *Did the representative provide clear next steps?* with instructions that define the elements of a complete next step:

Check whether the response includes these elements:

1. A specific action or solution.
2. The person responsible for the next action.
3. A specific or bounded timeframe.

Count how many elements are present. Use the answer instructions to map the count to an answer.

Use explicit quantifiers such as all, any, only, both, none, at least one, and exactly one. These terms turn general guidance into decision rules.

### Instructions for each question type

Use the instruction pattern that matches the question type.

- **Single-select**

Define a checklist and map the number of satisfied conditions to one answer. This pattern works well for answer sets such as **Pass**, **Partial**, and **Fail**.

Check whether the response contains these three elements:

1. A specific solution or action.
2. An owner for the next step.
3. A specific timeframe.

Count how many elements are present.

- **Multiple-select**

Define each answer as an independent condition. Instruct the agent to select every answer supported by evidence.

Select every answer whose condition is directly supported by the case data. Don't select an answer based on an assumption that the condition might apply.

- **Yes** or **No**

Define the evidence required for **Yes** and clarify what isn't sufficient.

Select **Yes** only if the customer explicitly states or strongly implies that they plan to use another supplier. Frustration or complaint language alone isn't sufficient.

- **Descriptive**

Define the expected length, content, style, and behavior when information is unavailable.

Summarize the customer's reason for contact in one or two sentences. Use neutral, factual language and don't include personally identifiable information. If the reason isn't stated, indicate that it can't be determined from the available data.

## Write answer instructions

Answer instructions must define:

1. When to select the answer.
2. When not to select the answer.

Make the conditions for each answer mutually exclusive. If two answers can apply to the same evidence, the result can vary between evaluation runs.

- **Pass answer**

Use **only if all** to define the highest answer. Add negative conditions to block common false-positive results.

Select **Pass** only if all the following conditions are met:

- The response provides a specific action or solution.
- The response identifies the owner of the next step.
- The response provides a specific or bounded timeframe.

Don't select **Pass** if the response uses only vague language such as "soon," "as soon as possible," or "we'll look into it."

- **Partial answer**

Define the exact middle-ground condition.

Select Partial if one or two of the three required elements are present. Also select Partial if all three elements are present but one uses vague or noncommittal language.

- **Fail answer**

Use **if any** to define specific failure conditions.

Select **Fail** if any of the following conditions are met:

- None of the required elements are present.
- The response only acknowledges the request and doesn't identify a next step.
- The response doesn't provide an action or solution.

## Use observable conditions

Replace subjective terms with conditions that the agent can verify in the evaluation input.

| Avoid | Use instead |
|---|---|
| Clear next steps | Names a specific action, identifies who performs it, and provides a specific timeframe. |
| Appropriate empathy | Includes at least one statement that acknowledges the customer's impact or frustration. |
| Reasonable grammar | Contains no more than three spelling errors in one message, and no error changes or obscures the meaning. |
| Took ownership | Uses first-person ownership language, such as *I will*, *I have*, or *I can*. |

If you must use a subjective term, define it with concrete conditions or examples.

## Scope the evaluation

Specify whose behavior and which data sources the agent must evaluate. Without explicit scope, the agent might combine customer communications, representative communications, automated messages, and internal records.

For example:

Evaluate only the representative's outgoing messages to the customer. Don't evaluate customer language, automated system messages, or internal case notes.

## Reference only available data

Reference field names and values instead of their visual representation in the application. For example,

Don't write: Confirm that all milestones display blue dots.

Write: Confirm that every value in the business process flow stage data is Completed.

The second instruction is valid only if the business process flow stage data is included in the evaluation input.

## Disable AI responses for unsuitable questions

Turn off AI responses for a question when the correct answer requires information that isn't available to the agent or isn't suitable for AI evaluation. Learn more about [managing AI-enabled questions](evaluation-criteria.md). Examples include:

- Highly subjective sentiment judgments when an authoritative customer score is available elsewhere.
- Questions that require dashboards, audio, video, screenshots, or other content that isn't included in the evaluation input.
- Questions that require comparison with a policy, baseline, or reference document that isn't included in the input.

These questions can remain available for manual evaluation.

## Avoid common instruction issues

Before publishing the criteria, review your instructions for the following issues:

- **Human-reviewer language:** Write direct commands such as *Select Pass if* or *Check whether*. Don't write coaching notes for the representative being evaluated.
- **Overlapping answers:** Ensure that only one answer can apply to a given set of evidence.
- **Subjective boundaries:** Replace words such as *reasonable*, *appropriate*, *clear*, *minor*, and *sufficient* with observable conditions.
- **Visual references:** Don't refer to colors, icons, buttons, screenshots, or other UI elements.
- **Invented numeric ratings:** Don't ask the agent to translate an interaction into a score such as 9 out of 10 unless the criteria define an objective calculation.
- **Long narrative instructions:** Prefer concise checklists and explicit rules. Split a question if one answer requires extensive exceptions.
- **Pass based on missing evidence:** Define the positive evidence required for Pass instead of selecting Pass when no problem is found.
- **Multiple concepts in one question:** Split questions that evaluate separate behaviors, such as acknowledging an issue and providing a solution.
- **Unnecessary not-applicable answers:** Add a not-applicable option only when it represents a valid business outcome. Disable AI responses when the question isn't suitable for AI evaluation.
- **Guidance in description fields:** Move evaluation rules from description fields to the supported instruction fields.

## Test the criteria before publishing

Use representative cases to verify that the instructions produce stable and defensible results.

1. Choose at least three cases:
   - A case that clearly meets the highest answer conditions.
   - A case that clearly meets the lowest answer conditions.
   - A borderline case.
2. Run each case with the same criteria version and unchanged case data.
3. Compare the selected answers and supporting reasons.
4. Identify questions whose answers change between runs.
5. Tighten the scope, evidence requirements, answer boundaries, or tie-breaking rules for those questions.
6. Repeat the test until the results are stable or any remaining variation represents answers that are equally defensible.

## Troubleshoot inconsistent evaluations

When evaluation results are inconsistent, first verify that the compared runs used:

- The same published criteria version.
- The same unchanged case data.
- The same evaluation input configuration.
- All data fields referenced by the questions.

Next, review the supporting reason for each changed answer.

| Observation | Recommended action |
|---|---|
| Different runs cite valid evidence but select different answers. | Remove overlapping answer conditions and add explicit tie-breaking rules. |
| The reason follows the instructions, but the result doesn't match the intended business rule. | Rewrite the instructions to reflect the intended rule. |
| The reason includes information that isn't in the input. | Collect the case ID, evaluation ID, and reason, and escalate for investigation. |
| The reason ignores information that's present in the input. | Verify that the input isn't missing or truncating data. Contact Microsoft Support if the data was provided correctly. |
| The evaluation returns no result or a service, schema, or parsing error. | Collect the correlation details and contact Microsoft Support. |

After you update the instructions, rerun the same cases and confirm that the previously unstable questions now produce consistent results.

## Related information

[Use evaluation criteria](evaluation-criteria.md)