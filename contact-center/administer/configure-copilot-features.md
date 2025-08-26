---
title: Enable Copilot features 
description: Learn how to enable the various Copilot features
author: gandhamm
ms.author: mgandham
ms.reviewer: neeranelli
ms.topic: how-to
ms.date: 05/07/2025
ms.update-cycle: 180-days
ms.custom: bap-template 
ms.collection: bap-ai-copilot
---

# Manage Copilot features

Copilot provides real-time AI assistance that helps customer service representatives (service representatives or representatives) automate time-consuming tasks to handle cases efficiently and resolve issues faster so that they can deliver value to customers.

When you enable the Copilot features, service representatives can do the following actions:

|Feature| Dynamics 365 Contact Center&mdash;embedded | Dynamics 365 Contact Center&mdash;standalone |
|----------|----------|----------|
| Ask a question   | Yes   | Yes   |
| Compose an email  | Yes   | Yes   |
| Summarize a case  | No  | Yes   |
| Summarize a conversation | Yes   | Yes   |
| Suggest a response  | Yes  | Yes   |

## License requirements

- Dynamics 365 Contact Center license. See: [Licenses](../implement/system-requirements-contact-center.md#licenses) 

## Prerequisites

You have the System Administrator role.

## Region availability and data movement

The respond to questions, compose an email, and summarize cases and conversations features are generally available in the North America region only. These features are in preview in the rest of the supported regions. More information: [Region availability](/dynamics365/customer-service/administer/cs-region-availability-service-limits#region-availability-of-analytics-and-insights?context=/dynamics365/contact-center/context/administer-context).

## Supported languages

To learn about supported languages for Copilot, see [Language support for AI-based analytics and insights]( /dynamics365/customer-service/administer/cs-region-availability-service-limits#language-support-for-ai-based-analytics-and-insights-in-customer-service?context=/dynamics365/contact-center/context/administer-context).


## Opt in to continue with Copilot setup

In Copilot Service admin center, the [**Copilot for questions and emails**](copilot-enable-help-pane.md) or [**Summaries**](copilot-enable-summary.md) page, when you enable the copilot features, you must opt in to continue with the setup. The opt-in page displays a link to review the terms and conditions. You can select **Opt in** to continue with the setup.  

## Opt out from using Copilot features

In Copilot Service admin center, opt out from the copilot features on the **Copilot for questions and emails** or **Summaries** page. When you opt out, the application erases the training data. If you want to use the features again, you must consent to the terms of use and opt in.

## Make Copilot available to service representatives

For service representatives to be able to use the copilot features, you need to enable the copilot features in [experience profiles](/dynamics365/customer-service/administer/add-profile-default?context=/dynamics365/contact-center/administer-context). By default, service representatives added to the out-of-the-box experience profiles can use the Copilot features.

You can create a custom experience profile and enable the required features to limit the features service representatives can use. You can then [assign the custom profile to the service representatives](/dynamics365/customer-service/administer/add-profile-default?context=/dynamics365/contact-center/administer-context).

Perform the following steps to add the Copilot features to an experience profile:

1. Go to [**Experience profiles**](/dynamics365/customer-service/administer/create-agent-experience-profile?context=/dynamics365/contact-center/administer-context) using one of the following navigation options:
   - **Support experience** > **Workspaces**
   - **Copilot for questions and emails** > **Agent access** > **Experience profiles**
1. Select the required experience profile.
1. On the **Productivity Pane**, turn on the **Copilot for questions and emails* toggle so that service representatives can use the Copilot features such suggest a response, ask a question, and write an email on the productivity pane.

   :::image type="content" source="../media/copilot-help-pane-enable-mini.png" alt-text="Screenshot of the Productivity panel in experience profile." lightbox="../media/copilot-help-pane-enable.png":::|

1.  In the **Copilot AI features** section, select edit and then select  the required features **Ask a question**, **Write an email**, **Case summary**, **Live conversation summary**, you want to enable for that profile.  

## Record service representatives interactions with Copilot

In the **Summaries** and **Copilot for questions and emails** configuration pages, you can select **Record transcripts of representative interactions with Copilot, representative actions, and representative feedback on AI suggestions** to record and understand how service representatives are interacting with Copilot and how Copilot is performing in a support organization. Agents can also share feedback about Copilot actions, which helps Copilot perform better. You can also [download](/dynamics365/customer-service/develop/reference/entities/msdyn_copilottranscriptdata?context=/dynamics365/contact-center/extend-context) and use the data to analyze knowledge sources, and build usage reports.

## Assign roles and privileges

Out of the box, users with the Customer Service Representative role only can use the copilot features. Therefore, make sure that users with custom roles have the following privileges: 

- prvCreatemsdyn_copilotinteraction 
- prvAppendmsdyn_copilotinteraction 
- prvCreatemsdyn_copilotinteractiondata 
- prvReadmsdyn_copilotinteraction
- prvReadmsdyn_copilotinteractiondata
- prvWritemsdyn_copilotinteractiondata
- prvAppendTomsdyn_copilotinteractiondata
- prvCreatemsdyn_copilotinteractiondata
- prvReadmsdyn_copilotagentpreference
- prvCreatemsdyn_copilotagentpreference
- prvWritemsdyn_copilotagentpreference
- prvReadmsdyn_appcopilotconfiguration
- prvReadmsdyn_agentcopilotsetting
- prvReadmsdyn_aimodel
- prvReadmsdyn_aitemplate
- prvReadmsdyn_copilotsummarizationsetting 
- prvReadmsdyn_conversationinsight
- prvWritemsdyn_copilottranscriptdata 
- prvAppendTomsdyn_copilottranscriptdata  
- prvReadmsdyn_copilottranscriptdata 
- prvCreatemsdyn_copilottranscriptdata 
- prvWritemsdyn_copilottranscriptdata 
- prvAppendmsdyn_copilottranscriptdata
- prvIntelligenceUsage: This privilege is required to access the Copilot case summary. By default, this privilege is available for out-of-the-box security roles. Make sure that your users have  [**Miscellaneous privileges**](/power-platform/admin/security-roles-privileges#define-the-privileges-and-properties-of-a-security-role) > **prvIntelligenceUsage** assigned to the required custom security roles.
- prvReadOrganizationSetting
- prvReadmsdyn_panetabconfiguration 
- prvReadmsdyn_paneconfiguration 
- msdyn_appconfiguration
- msdyn_panetoolconfiguration

More information: [Security roles and privileges](/power-platform/admin/security-roles-privileges)

## Next steps

[Enable Copilot case and conversation summaries](copilot-enable-summary.md)  
[Enable Copilot help pane](copilot-enable-help-pane.md)  

### Related information

[Responsible AI FAQ for copilot features](/dynamics365/customer-service/implement/faq-responsible-ai-copilot?context=/dynamics365/contact-center/administer-context)  
[FAQ for Copilot in Customer Service](/dynamics365/customer-service/administer/faq-copilot-features?context=/dynamics365/contact-center/administer-context)  
