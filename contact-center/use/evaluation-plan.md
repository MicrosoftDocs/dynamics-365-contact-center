---
title: Use evaluation plan 
description: Create and manage evaluation plans in Dynamics 365 Customer Service and Dynamics 365 Contact Center for consistent reviews of cases and conversations. Learn how to activate and optimize evaluations.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 03/23/2026
ms.custom: bap-template
---

# Use evaluation plan

**Conversations**: [!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

**Cases**: [!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]


Evaluation plans help supervisors perform consistent and objective reviews of cases and conversations. You can define criteria methods, conditions, and evaluation plans to support both manual and AI-driven assessments. This article describes how to create, activate, and manage evaluation plans, and how to enable bulk evaluations to streamline your review process.

## Prerequisites

- Enable [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- Assign the required [roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).

## Create and activate evaluation plan for cases and closed conversations

You must enable the **Enable bulk evaluations** checkbox in Copilot Service admin center before you create and activate an evaluation plan for cases. Learn more in [Enable Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#enable-quality-evaluation-agent).

> [!NOTE]
> You can use conversation evaluations for voice and live chat channels only.

1.  In Copilot Service workspace, go to **Evaluation Plans**.

1.  On the **Evaluation plans** page, select **New**.

1.  On the **New Evaluation Plan** page,

    1.  In the **Evaluation plan details** section, provide the following:
        - **Plan name**: Enter plan name.
        - **Description**: Enter description.
        - **Record type**: Select **record type** as **Conversations** or **Cases**.

    1.  If you select **Conversations**, then in the **Frequency** section, select the following options:

        1.  **Frequency type:** Select **Trigger,** and then provide the following:
            - **Occurrence**: Select **Closed conversations**.
            - **Start date**: Specify the start date for the plan.
            - **End date**: Specify the end date for the plan.
            
    1. If you select **Cases**, then in the **Frequency** section, select the following options:

        1.  **Frequency type:** Select **Recurring,** and then provide the following:
            - **Occurrence**: Select **Daily**.
            - **Start date**: Specify the start date for the plan.
            - **End date**: Specify the end date for the plan.
        1. If you select the **Frequency type** as **Trigger**, then select the **Evaluation Trigger Config** as **Default Trigger Config for Resolved Cases**. This selection creates trigger-based evaluations for resolved cases only.

    1.  In the **Conditions** section, select **Add** to add conditions to your evaluation plan. For example, Add **Conversation status**> **Equals** > **Closed** or add **Channel type > Contains data > Live chat.**

    1.  In the **Assign evaluation** section, provide the following:

        1.  **Evaluation criteria:** Select the criteria from the dropdown. Example, select **Closed Conversations Default Criteria**.

        1.  **Evaluation method:** Select from **AI assisted, AI agent**, or **Manual.**
        > [!NOTE]
        > If you select the **AI assisted** or **AI agent** evaluation method, make sure that **AI response enabled** is selected for your questions in the criteria, as follows:
        > - For **AI agent** mode: All questions must be AI-enabled (manual editing isn't allowed).
        > - For **AI assisted** mode: At least one question must be AI-enabled.

        1.  If you select the **AI assisted** option, from the **Assigned To** dropdown list, you need to select **Team** or **User**.

        1.  **Due date**: Select a due date.

1.  Select **Save**.

1.  Select **Activate plan**. The **Activate plan** dialog appears.
1.  Select **Activate plan**. On successful activation, a success message appears.

### View run history for a plan

When you run an evaluation plan, it generates a run‑history record that captures the plan name, execution timestamp, total number of records processed, and the final status. This record provides structured visibility into batch runs and their outcomes.

Select **Run history** on your evaluation plan to view the details.

## Use on-demand evaluation

You can also use [on-demand evaluation](on-demand-evaluation.md#use-on-demand-evaluation) to check cases and conversations when needed.

## Configure trigger-based evaluation plans for resolved cases

You can create and activate trigger-based evaluation plans for resolved cases only. Trigger-based evaluations run automatically when a case gets resolved and specific conditions are met.

When you [create and activate an evaluation plan](#create-and-activate-evaluation-plan-for-cases-and-closed-conversations) from the **Evaluation plans** page, select the **Frequency type** as **Trigger** and **Evaluation Trigger Config** as **Default Trigger Config for Resolved Cases**. 

When a case is resolved, one evaluation is created for each plan that matches the specified conditions. Multiple evaluations can be created for the same case. 

To view the evaluations, go to the **Evaluations** page. Once the **AI agent status** appears as **Completed** for the evaluations, select the required evaluation. Review the **Evaluation Summary** provided by Quality Evaluation Agent.

## Create and activate a real-time evaluation plan for ongoing conversations

You need to turn on the **Criteria scoring** toggle for your evaluation criteria. Learn more in [Create evaluation criteria](evaluation-criteria.md#create-evaluation-criteria).

To create a real-time evaluation plan:

1. In Copilot Service workspace, go to **Evaluation Plans**.

1. On the **Evaluation plans** page, select **New**.

1. On the **New Evaluation Plan** page, in the **Evaluation plan details** section, provide the following information:

    - **Plan name**: Enter plan name.
    - **Description**: Enter description.
    - **Record type**: Select **record type** as **Conversations**.
     
1. In the **Frequency** section, for **Frequency type**, select **Real-Time**.

1. In the **Conditions** section, add the workstreams for which you want to enable real-time evaluation.

1. In the **Assign Evaluation** section, for **Evaluation method**, select **AI assisted**.
    
1.  Select **Save**.

Learn how to view scores for the real-time evaluation plan in [Manage ongoing Quality Evaluation Agent conversations](ongoing-quality-evaluation-agent-conversations.md).

## Activate, pause, resume, or delete evaluation plans

1. In Copilot Service workspace, go to **Evaluation plans**.

1. On the **Evaluation Plans** page, select the evaluation plans that you would like to activate, delete, resume, or pause.

1. Select the action that you want to take. On the respective dialog box, confirm the action and save.

When you pause a plan, it finishes the current batch and then stops before the next run. When you resume, the plan starts at its next scheduled time.

## Edit evaluation plans

You can't edit active evaluation plans, or modify the existing record type or evaluation criteria for a plan.

1. On the **Evaluation Plans** page, select the evaluation plans that you want to edit, and then select **Pause plan**.

1. Select **Edit**. All the fields become editable except for **Record type** and **Evaluation criteria**.

1. Save the changes.

1. Select **Activate plan** to activate the plan.

## Enable bulk evaluation for cases

Bulk evaluations enable automatic evaluations on large sets of records using recurring evaluation plans. To perform bulk evaluations, make sure that bulk evaluations are turned on for cases in the Copilot Service admin center, evaluation plans for cases are created and activated, and the frequency for the plans is set to recurring.

1. In Copilot Service workspace, go to **Evaluation plans**.

1. On the **Evaluation plans** page, select the evaluation plans.

1. Select **Activate**. The plans are activated only after the data transfer is complete.

Each batch run supports a maximum of 20,000 records.

You can view the results in the following ways:

- From the **Run history** tab of an evaluation plan. The status show as Completed, if the run is successful.
- From the **Evaluations** grid, when you select **Evaluations** in Copilot Service workspace.

## Use sampling in recurring evaluation plans

Sampling lets you evaluate a subset of records instead of all records identified by an evaluation plan. For example, you can run evaluations on 10% of 100 records. The **Sampling** section appears when the record type is **Case** and frequency is set to **Recurring** only.

1. In the **Sampling** section of the **Evaluation Plans** page, provide the following information:
1. In the **Sampling mode** dropdown, select either **Absolute number** or **Percentage**.
    1. If you select **Absolute number**, then provide the following information:
        1. **Sampling value**: Enter a value of 1 or more. If the value is less than 1, you receive an error message stating that the sampling value must be at least 1 when the sampling mode is set to absolute number.
        1. **Selection strategy**: Select **Top** or **Bottom**. Based on the absolute number you specified, the system selects records from the top or bottom of the list. 
        1. **Filter data type**: Select a filter data type, such as **Created On** or **Modified On**.

Once you activate a plan with sampling, the sampling fields become noneditable. To edit the sampling settings, you must first pause the plan.

The Run history tab displays the outcomes of each evaluation run. It includes the following columns:

- **Records identified by condition**: The total number of records that meet the evaluation plan's conditions.
- **Records identified by sampling**: The number of records selected based on your sampling settings.
- **Records eligible for evaluation**: The final number of records evaluated, calculated as the minimum of the values in the **Records identified by condition** and **Records identified by sampling** columns.

Each batch run supports a maximum of 20,000 records.

## Related information

[Manage Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md)  
[Use evaluations](use-evaluations.md)  
[Use evaluation criteria](evaluation-criteria.md)  
[Use on-demand evaluation](on-demand-evaluation.md)
