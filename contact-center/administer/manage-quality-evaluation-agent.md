---
title: Configure Quality Evaluation Agent in Dynamics 365
description: Learn how to configure and enable the Quality Evaluation Agent to improve customer engagement and ensure compliance with evaluation standards.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: 
ms.date: 10/15/2025
ms.custom: bap-template
---

# Manage Quality Evaluation Agent

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and should not be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. <br> 
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

> [!IMPORTANT]
>
> - Evaluations for conversations is a preview feature and is available in Dynamics 365 Contact Center only. 
> - Preview features aren’t meant for production use and might have restricted functionality. These features are subject to [supplemental terms of use](https://go.microsoft.com/fwlink/?linkid=2189520), and are available before an official release so that customers can get early access and provide feedback.

The Quality Evaluation Agent is an AI agent that assesses customer engagement using an evaluation framework defined by supervisors. The Quality Evaluation Agent autonomously scores cases and conversations, providing insights to help supervisors enhance the quality of case and conversation interactions.

The Quality Evaluation Agent evaluates cases and closed conversations to check if representatives follow required standards. If standards aren't met, the Quality Evaluation Agent provides coaching recommendations or actions to help representatives improve.

The Quality Evaluation Agent includes the evaluation criteria, evaluation plan, and evaluations. These components are essential for the Quality Evaluation Agent to work.

**Evaluation Criteria**:

Supervisors can create a form with questions, answer choices, scoring metrics, and detailed instructions for the Quality Evaluation Agent. They can use this form to assess interactions. The Quality Evaluation Agent predicts responses and assigns quality scores, giving insights into the overall quality score of the contact center.

**Evaluation Plan**:

Supervisors can set up plans to schedule when to evaluate interactions. They can choose interactions based on specific conditions and use the right evaluation criteria to review them systematically.

**Evaluations**:

The Quality Evaluation Agent summarizes case and conversation evaluations in customer service and highlights action plans and recommendations. These insights help AI supervisors improve service quality.

## Prerequisites

- You have the Quality Manager, Quality Evaluator, and the Quality Administrator role.
- You have configured the [Connection references for Quality Evaluation Agent flow](quality-evaluation-agent-connections.md#configure-connection-references-for-quality-evaluation-agent-flow).
- You have [set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- You provided consent for potential [data movement across regions](#data-movement-across-regions).

## Data movement across regions

To ensure optimal performance, service calls may be routed outside the customer's regional boundary if local capacity is temporarily unavailable. To participate, customers are kindly requested to provide consent for potential data movement across regions. This enables us to deliver a seamless experience leveraging the full capabilities of Copilot and generative AI features within the Power Platform.

If a customer prefers to keep data strictly within their region, we respect that choice and recommend waiting for broader availability before enabling the preview.

Learn more in [Move data across regions for Copilots and generative AI features – Power Platform](/power-platform/admin/geographical-availability-copilot?utm_source=chatgpt.com&tabs=new).

## Role and privileges


| Persona      | Role            | Privileges                                                                 |
|--------------|-----------------|---------------------------------------------------------------------------|
| Administrator| Quality Administrator   | Configure Quality Evaluation Agent<br>Create evaluation criteria, evaluation plan<br>Complete or assign an evaluation. |
| Supervisor   | Quality Manager | Create evaluation criteria, evaluation plan<br>Complete or assign an evaluation |
| Supervisor   | Quality Evaluator| Complete or assign an evaluation.                                         |


## Enable Quality Evaluation Agent

As an administrator, you need to enable Quality Evaluation Agent for your supervisors from the Copilot Service admin center. You can select cases or conversations record type, as required. You can also set a scoring and a threshold value. Each criteria and question in the evaluation is scored out of 100 points. You can set thresholds to define good and poor-quality metrics.

1. In the Copilot Service admin center application, go to **Customer Support** > **Quality management.** The **Quality management** page appears.
1. Select **Manage** for **Quality Evaluation Agent**. The **Quality Evaluation Agent** page appears.
1. In the **Enablement by record type** section:

 1. Select the **Case** checkbox for case evaluation or the **Conversation** checkbox for a conversation evaluation.
    1. In **Specify data** section, you can see the default entities that have been added. 
    1. Select **Manage data** to go to the **Specify data** dialog, where you can:
        - Delete data types or uncheck a row to temporarily exclude the data type from being summarized.
        - Add more data type fields for Quality Evaluation Agent input configuration.
    1. Select **Add data**, to add more data on the **Specify data** dialog.
        1. Select **Save** after you have specified the data fields.
 
 1. In the **Evaluation criteria score** section, select the **Enable scoring for criteria** checkbox. The **Evaluation criteria scoring turned on** dialog appears.
 1. Select **Turn on**. Once turned on, it can’t be turned off.
 1. From the **Set threshold value out of 100** dropdown list, select a threshold value.
 1. Select **Save**.

## Related information

[Use evaluation plan](../use/evaluation-plan.md#use-evaluation-plan)  
[Use evaluation criteria](../use/evaluation-criteria.md#use-evaluation-criteria)  
[Use evaluations](../use/use-evaluations.md#use-evaluations)