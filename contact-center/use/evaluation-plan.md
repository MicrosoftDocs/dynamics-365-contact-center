---
title: Use evaluation plan 
description: Create and manage evaluation plans in Dynamics 365 to ensure consistent reviews for cases and conversations. Learn how to activate and optimize evaluations.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to 
ms.collection:
ms.date: 10/14/2025
ms.custom: bap-template
---

## Use evaluation plan

Evaluation plans help supervisors ensure consistent and objective reviews of cases and conversations. By defining criteria, methods, and conditions, evaluation plans support both manual and AI-driven assessments. This article describes how to create, activate, and manage evaluation plans, request on-demand evaluations, and enable bulk evaluations to streamline your review process.

## Prerequisites

- You have enabled [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- You have the required [Roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges)
- You have [set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- You provided consent for potential [data movement across regions][Data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).

### Create and activate evaluation plan for cases and conversations

> [!NOTE]
> You can use conversation evaluations for voice and live chat channels only.

1.  In Customer Service workspace, go to **Evaluation Plans**.

1.  On the **Evaluation plans** page, select **New**.

1.  On the **New Evaluation Plan** page,

    1.  In the **Evaluation plan details** section, provide the following:

        1.  **Plan name**: Enter plan name.

        1.  **Description**: Enter description.

        1.  **Record type**: Select **record type** as **Conversations** or **Cases**.

    1.  If you select **Conversations**, then in the **Frequency** section, select the following:

        1.  **Frequency type:** Select **Trigger,** and then provide the following:

            1.  **Occurence**: If you have frequency type as **Trigger**, then select **Closed conversation**.

            1.  **Start date**: Provide a start date.

            1.  **End date**: Provide an end date.
            
    1. If you select **Cases**, then in the **Frequency** section, select the following:

        1.  **Frequency type:** Select **Recurring,** and then provide the following:
            
            1. **Occurence**: Select **Daily**.

            1.  **Start date**: Provide a start date.

            1.  **End date**: Provide an end date.

    1.  In the **Conditions** section, select **Add** to add conditions to your evaluation plan. For example, Add **Conversation status**> **Equals** > **Closed** or add **Channel type > Contains data > Live chat.**

    1.  In the **Assign evaluation** section, provide the following:

        1.  **Evaluation criteria:** Select the criteria from the dropdown. Example, select **Closed Conversations Default Criteria**.

        1.  **Evaluation method:** Select from **AI assisted, AI agent**, or **Manual.**

        1.  If you select the **AI assisted** option, from the **Assigned To** dropdown list, you need to select **Team** or **User**.

        1.  **Due date**: Select a due date.

1.  Select **Save**.

1.  Select **Activate plan**. The **Activate plan** dialog appears.
1.  Select **Activate plan**. On successful activation, a success message appears.

## Activate, pause, resume, or delete an evaluation plan

1.  In Customer Service workspace, go to **Evaluation plans**.

1. On the **Evaluation Plans** page, select the evaluation plans that you would like to activate, delete, resume, or pause.

1.  Select **Activate plan, Pause plan,** **Resume plan**, or **Delete**. On the respective dialog box, confirm the action and save.

## On-demand evaluation for cases

The on-demand evaluation feature allows users to request evaluations for specific cases.

To request evaluations for multiple cases from the case grid:

1. Select the required records.
    
1.  Select **Request evaluation**.

> [!NOTE]
> You can select up to 20 records for evaluation. 

To request evaluation for a particular case:

1.  Go to **Cases**, select the required case, and then select **Request
    evaluation**.

1.  On the **Request evaluation** dialog, select the following:

    1.  **Evaluation criteria:** Search and select an evaluation criteria from the list of criteria.

    1.  **Evaluation method:** Select an evaluation method.

    1.  **Assigned to:** Select the user.

    1.  **Evaluation due date:** Select a due date for the evaluation.

3.  Select **Request**.

4.  Once the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation    Summary** provided by Copilot.

5.  Select **Submit and Close**. The **Evaluator status** appears as **Completed**.

## On-demand evaluation for conversations (preview)

> [!NOTE]
> On-demand evaluation for conversations is in preview and is available on Dynamics 365 Contact Center only.

To request evaluation for closed conversations:

1. Go to **Activities** > **Closed Conversations**.

1. Select a closed conversation, and then on the specific conversation, select **Request evaluation**.

1. On the **Request evaluation** dialog, select the following:

    1.  **Evaluation criteria:** Search and select an evaluation criteria from the list of criteria.
    
    1.  **Evaluation method:** Select an evaluation method: **AI assisted**, **Manual**, or **AI agent**. If you select **AI agent**, the **Assigned to:** and **Evaluation due date:** is turned off.
    
    1.  **Assigned to:** Select the user.
    
    1.  **Evaluation due date:** Select a due date for the evaluation.
    
1.  Select **Request**. 

1. Once the AI agent status appears as **Completed,** on the **Evaluation associated view**, you can review the **Evaluation    Summary** provided by Copilot.

1.  Select **Submit and Close**. The **Evaluator status** appears as **Completed**.


## Enable bulk evaluation for cases

1. On the **Quality Evaluation Agent** page, in the **Enablement by record type** section, select **Case**, and then select **Enable bulk evaluation**. The bulk evaluation provisioning starts.

1. Select **Activate**. The plan gets activated only after the data transfer is complete. You can create and save your plan as draft in the meantime.

> [!NOTE]
> You can evaluate up to 10,000 entity records in a single batch run. A single batch run might take upto four hours to complete.
