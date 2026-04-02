---
title: Manage Quality Evaluation Agent
description: Learn how to configure and enable Quality Evaluation Agent in Dynamics 365 Customer Service and Dynamics 365 Contact Center. Use agent evaluations to improve customer engagement and assess interactions against quality standards.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.update-cycle: 180-days 
ms.date: 03/31/2026
ms.custom: bap-template
---

# Manage Quality Evaluation Agent

**Conversations**: [!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

**Cases**: [!INCLUDE[cc-feature-availability-cs-only](../includes/cc-feature-availability-cs-only.md)]

Quality Evaluation Agent is an AI agent that assesses customer engagement using an evaluation framework defined by supervisors. The quality evaluation framework comprises evaluation criteria, evaluation plan, and evaluations that are essential for the AI Agent to work. 

Quality Evaluation Agent autonomously scores cases and conversations, delivering actionable insights to help supervisors improve interaction quality. It evaluates cases and closed conversations to make sure they comply with required standards. When standards aren't met, the AI Agent recommends actions to enhance future interactions.

**Evaluation criteria**:

Create a form with questions, answer choices, scoring metrics, and detailed instructions for the Quality Evaluation Agent. The AI agent uses this form to assess interactions. 

**Evaluation plan**:

Set up plans to schedule when to evaluate interactions. You can select interactions based on specific conditions and use the right evaluation criteria to review interactions systematically. You can create, activate, and manage evaluation plans, request on-demand evaluations, and enable bulk evaluations to streamline your review process.

**Evaluations**:

The Quality Evaluation Agent evaluates case and conversations, provides summaries of the interactions, with insights and recommendations that help improve customer interactions. You can use [on-demand evaluation](on-demand-evaluation.md) to check cases, conversations, and emails when needed.

> [!IMPORTANT]
> - This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. <br> 
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Prerequisites

- Assign the Quality Manager, Quality Evaluator, and the Quality Administrator roles.
- Configure [Configure connection references](#configure-connection-references).
- Set up [Microsoft Copilot credits](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- Provide consent for potential [data movement across regions](#data-movement-across-regions).

## Data movement across regions

For optimal performance, service calls might be routed outside the customer's regional boundary if local capacity is temporarily unavailable. To participate, customers are requested to provide consent for potential data movement across regions. This consent enables us to deliver a seamless experience by using the full capabilities of Copilot and generative AI features within Power Platform.

Learn more in [Move data across regions for Copilots and generative AI features – Power Platform](/power-platform/admin/geographical-availability-copilot?utm_source=chatgpt.com&tabs=new).

## Role and privileges


| Persona      | Role            | Privileges                                                                 |
|--------------|-----------------|---------------------------------------------------------------------------|
| Administrator| Quality Administrator   | - Configure Quality Evaluation Agent.<br> - Create evaluation criteria and evaluation plan.<br> - Complete or assign an evaluation. |
| Supervisor   | Quality Manager | - Create evaluation criteria and evaluation plan.<br> - Complete or assign an evaluation. |
| Supervisor   | Quality Evaluator| Complete or assign an evaluation.                                         |

## Configure connection references

When you navigate to the Quality Evaluation Agent page in Copilot Service admin center, a **Prerequisites** section appears at the top of the page that indicates whether connection references are set up. You need to configure connection references for Quality Evaluation Agent flow to integrate with Microsoft services. These connections link flow to essential data sources such as Microsoft Dataverse and Copilot Studio, ensuring smooth operation and enhanced functionality.

1. In Copilot Service admin center, go to **Customer Support** > **Quality management.** The **Quality management** page appears.
1. Select **Manage** for **Quality Evaluation Agent**. The **Quality Evaluation Agent** page appears.
1. In the **Prerequisites** section, verify if **Step 1: Connection References**, **Step 2: Power Automate Flows**, and **Step 3: Copilot Studio Agent** show as **Ready**.
    1. If **Step 1: Connection References** shows as **In progress** or **Incomplete**, then select **Manage connections**.
    1. In the **Configure Connections** dialog, select **Update connection references to use your connector** to complete connection references.
    1. In **Step 2: Power Automate Flows**, if a flow is turned off, use the navigation link to open the flow in Power Automate and enable it.
    1. Once all tiles show as **Ready**, select **Publish** in **Step 3: Copilot Studio Agent** to complete the setup.

After completing the configuration, you might need to perform a hard refresh to see the updated status.

If you have issues configuring connection references from the **Quality Evaluation Agent** page, you can do a manual setup. Follow the steps provided in [Connection references for Quality Evaluation Agent flow](/dynamics365/customer-service/administer/admin-km-agent-connections?context=/dynamics365/contact-center/context/administer-context).

## Enable Quality Evaluation Agent

You need to enable Quality Evaluation Agent for your supervisors in Copilot Service admin center. You can select cases, conversations, or email record type. You can also set a scoring and threshold value. Each criteria and question in the evaluation is scored out of 100 points. You can set thresholds to define good and poor-quality metrics.

1. In Copilot Service admin center, go to **Customer Support** > **Quality management.** The **Quality management** page appears.
1. Select **Manage** for **Quality Evaluation Agent**. The **Quality Evaluation Agent** page appears.
1. In the **Enablement by record type** section:
1. Select **Case**, **Conversation**, or **Email** and then select **Save**.
    1. If you select **Case** and need to perform bulk evaluation for cases, select the **Enable bulk evaluations** option.
1. For each record type, in **Specify data**, you can see the default entities that are added. For **Email** record type, you need to add the **Description** in the **Data field** and save it. 
    1. Select **Manage data** to go to the **Specify data** dialog, where you can:
        - Delete data types or clear a row to temporarily exclude the data type from being summarized.
        - Add more data type fields for Quality Evaluation Agent input configuration by selecting **Add data**.
          > [!NOTE]
          > You can add up to 10 one-to-one data types and six one-to-many data types in addition to the ones available by default.
 1. In the **Evaluation criteria score** section, select **Enable scoring for criteria**. The **Evaluation criteria scoring turned on** dialog appears.
 1. Select **Turn on**. You can't turn off this feature after you enable it.
 1. From the **Set threshold value out of 100** dropdown list, select a threshold value.
 1. Select **Save**.

## Related information

[Use evaluation plan](../use/evaluation-plan.md)   
[Use on-demand evaluation](../use/on-demand-evaluation.md)   
[Use evaluation criteria](../use/evaluation-criteria.md)    
[Use evaluations](../use/use-evaluations.md)