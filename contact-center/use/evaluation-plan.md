---
title: Use evaluation plan 
description: Create and manage evaluation plans in Dynamics 365 Customer Service and Dynamics 365 Contact Center for consistent reviews of cases and conversations. Learn how to activate and optimize evaluations.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to 
ms.collection:
ms.date: 10/22/2025
ms.custom: bap-template
---

# Use evaluation plan

> [!IMPORTANT]
>
> - Evaluations for conversations is a preview feature and is available in Dynamics 365 Contact Center only. 
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520), and are available before an official release so that customers can get early access and provide feedback.

Evaluation plans help supervisors ensure consistent and objective reviews of cases and conversations. By defining criteria, methods, and conditions, evaluation plans support both manual and AI-driven assessments. This article describes how to create, activate, and manage evaluation plans, and enable bulk evaluations to streamline your review process.

## Prerequisites

- You have enabled [Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent).
- You have the required [Roles and privileges](../administer/manage-quality-evaluation-agent.md#role-and-privileges)
- You have [set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- You provided consent for potential [data movement across regions](../administer/manage-quality-evaluation-agent.md#data-movement-across-regions).

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

            1.  **Start date**: Specify the start date for the plan.

            1.  **End date**: Specify the end date for the plan.
            
    1. If you select **Cases**, then in the **Frequency** section, select the following:

        1.  **Frequency type:** Select **Recurring,** and then provide the following:
            
            1. **Occurence**: Select **Daily**.

            1.  **Start date**: Specify the start date for the plan. 

            1.  **End date**: Specify the end date for the plan.

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

## Activate, pause, resume, or delete evaluation plans

1.  In Customer Service workspace, go to **Evaluation plans**.

1. On the **Evaluation Plans** page, select the evaluation plans that you would like to activate, delete, resume, or pause.

1.  Select the action that you want to take. On the respective dialog box, confirm the action and save.

## Enable bulk evaluation for cases

1. On the **Quality Evaluation Agent** page, in the **Enablement by record type** section, select **Case**, and then select **Enable bulk evaluation**. The bulk evaluation provisioning starts.

1. Select **Activate**. The plan gets activated only after the data transfer is complete. You can create and save your plan as a draft in the meantime.

You can evaluate up to 10,000 entity records in a single batch run. A single batch run might take up to four hours to complete.

## Related information

[Manage Quality Evaluation Agent](../administer/manage-quality-evaluation-agent.md#manage-quality-evaluation-agent)  
[Use evaluations](use-evaluations.md#use-evaluations)  
[Use evaluation criteria](evaluation-criteria.md#use-evaluation-criteria)
[Use on-demand evaluation](on-demand-evaluation.md#use-on-demand-evaluation)
