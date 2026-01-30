---
title: Use evaluation plan 
description: Create and manage evaluation plans in Dynamics 365 Customer Service and Dynamics 365 Contact Center for consistent reviews of cases and conversations. Learn how to activate and optimize evaluations.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days
ms.date: 01/28/2026
ms.custom: bap-template
---

# Use evaluation plan

**Conversations**: [!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

**Cases**: [!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]


Evaluation plans help supervisors perform consistent and objective reviews of cases and conversations. You can define criteria methods, conditions, and evaluation plans to support both manual and AI-driven assessments. This article describes how to create, activate, and manage evaluation plans, and enable bulk evaluations to streamline your review process.

> [!IMPORTANT]
>
> - Evaluations for conversations and bulk evaluations for cases are preview features. 
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520), and are available before an official release so that customers can get early access and provide feedback.

## Prerequisites

- Enable [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- Assign the required [roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).

## Create and activate evaluation plan for cases and closed conversations

You must enable the **Enable bulk evaluations (preview)** checkbox in Customer Service admin center before you create and activate an evaluation plan for cases. Learn more in [Enable Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#enable-quality-evaluation-agent).

> [!NOTE]
> You can use conversation evaluations for voice and live chat channels only.

1.  In Customer Service workspace, go to **Evaluation Plans**.

1.  On the **Evaluation plans** page, select **New**.

1.  On the **New Evaluation Plan** page,

    1.  In the **Evaluation plan details** section, provide the following:
        - **Plan name**: Enter plan name.
        - **Description**: Enter description.
        - **Record type**: Select **record type** as **Conversations** or **Cases**.

    1.  If you select **Conversations**, then in the **Frequency** section, select the following:

        1.  **Frequency type:** Select **Trigger,** and then provide the following:
            - **Occurence**: If you have frequency type as **Trigger**, then select **Closed conversation**.
            - **Start date**: Specify the start date for the plan.
            - **End date**: Specify the end date for the plan.
            
    1. If you select **Cases**, then in the **Frequency** section, select the following:

        1.  **Frequency type:** Select **Recurring,** and then provide the following:
            - **Occurence**: Select **Daily**.
            - **Start date**: Specify the start date for the plan.
            - **End date**: Specify the end date for the plan.

    1.  In the **Conditions** section, select **Add** to add conditions to your evaluation plan. For example, Add **Conversation status**> **Equals** > **Closed** or add **Channel type > Contains data > Live chat.**

    1.  In the **Assign evaluation** section, provide the following:

        1.  **Evaluation criteria:** Select the criteria from the dropdown. Example, select **Closed Conversations Default Criteria**.

        1.  **Evaluation method:** Select from **AI assisted, AI agent**, or **Manual.**

        1.  If you select the **AI assisted** option, from the **Assigned To** dropdown list, you need to select **Team** or **User**.

        1.  **Due date**: Select a due date.

1.  Select **Save**.

1.  Select **Activate plan**. The **Activate plan** dialog appears.
1.  Select **Activate plan**. On successful activation, a success message appears.

You can also use [on-demand evaluation](on-demand-evaluation.md#use-on-demand-evaluation) to check cases and conversations when needed.

## Create and activate a real-time evaluation plan for ongoing conversations (preview)

You need to turn on the **Criteria scoring** toggle for your evaluation criteria. Learn more in [Create evaluation criteria](evaluation-criteria.md#create-evaluation-criteria).

To create a real-time evaluation plan:

1. In Customer Service workspace, go to **Evaluation Plans**.

1. On the **Evaluation plans** page, select **New**.

1. On the **New Evaluation Plan** page, in the **Evaluation plan details** section, provide the following information:

    - **Plan name**: Enter plan name.
    - **Description**: Enter description.
    - **Record type**: Select **record type** as **Conversations**.
     
1. In the **Frequency** section, for **Frequency type**, select **Real-Time**.

1. In the **Conditions** section, add the workstreams for which you want to enable real-time evaluation.

1. In the **Assign Evaluation** section, for **Evaluation method**, select **AI assisted**.
    
1.  Select **Save**.

Learn how to view scores for the real-time evaluation plan in [Manage ongoing Quality Evaluation Agent conversations (preview)](ongoing-quality-evaluation-agent-conversations.md).

## Activate, pause, resume, or delete evaluation plans

1. In Customer Service workspace, go to **Evaluation plans**.

1. On the **Evaluation Plans** page, select the evaluation plans that you would like to activate, delete, resume, or pause.

1. Select the action that you want to take. On the respective dialog box, confirm the action and save.

When you pause a plan, it finishes the current batch and then stops before the next run. When you resume, the plan starts at its next scheduled time.

## Enable bulk evaluation for cases (preview)

1. In Customer Service workspace, go to **Evaluation plans**.

1. On the **Evaluation plans** page, select the evaluation plans.

1. Select **Activate**. The plans gets activated only after the data transfer is complete.

You can evaluate up to 10,000 entity records in a single batch run. A single batch run might take up to four hours to complete.

## Related information

[Manage Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md)  
[Use evaluations](use-evaluations.md)  
[Use evaluation criteria](evaluation-criteria.md)  
[Use on-demand evaluation](on-demand-evaluation.md)
