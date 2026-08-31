---
title: Configure Copilot features
description: Learn how to configure Copilot features and make them available to service representatives in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: neeranelli
ms.topic: how-to
ms.date: 08/27/2026
ms.update-cycle: 180-days
ms.custom: bap-template 
ms.collection: bap-ai-copilot
---

# Configure Copilot features

Copilot provides real-time AI assistance to help customer service representatives (service representatives or representatives) handle cases and customer conversations.

When you enable Copilot, service representatives can use the following features:

|Feature| Dynamics 365 Contact Center&mdash;embedded | Dynamics 365 Contact Center&mdash;standalone |
|----------|----------|----------|
| Ask a question   | Yes   | Yes   |
| Compose an email  | Yes   | Yes   |
| Summarize a case  | No  | Yes   |
| Summarize a conversation | Yes   | Yes   |

## License requirements

Specific licensing requirements apply when you use Copilot features in Dynamics 365 Contact Center. Learn more in [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/?LinkId=866544).

## Prerequisites

You have the System Administrator role.

## Region availability and data movement

The features that answer questions, compose emails, and summarize cases and conversations are generally available only in North America. These features are in preview in other supported regions. Learn more in [Region availability](/dynamics365/customer-service/administer/cs-region-availability-service-limits#region-availability-of-analytics-and-insights?context=/dynamics365/contact-center/context/administer-context).

## Supported languages

To learn about supported languages for Copilot, see [Language support for AI-based analytics and insights](/dynamics365/customer-service/administer/cs-region-availability-service-limits#language-support-for-ai-based-analytics-and-insights-in-customer-service?context=/dynamics365/contact-center/context/administer-context).

## Opt in to continue with Copilot setup

When you enable Copilot features on the [**Copilot for questions and emails**](copilot-enable-help-pane.md) or [**Summaries**](copilot-enable-summary.md) page in Copilot Service admin center, you must opt in to continue setup. Review the terms and conditions, and then select **Opt in**.

## Opt out from using Copilot features

In Copilot Service admin center, opt out of Copilot features on the **Copilot for questions and emails** or **Summaries** page. When you opt out, the application erases the training data. To use the features again, consent to the terms of use and opt in.

## Make Copilot available to service representatives

For service representatives to use Copilot features, enable the features in [experience profiles](/dynamics365/customer-service/administer/add-profile-default?context=/dynamics365/contact-center/administer-context). By default, service representatives added to the default experience profiles can use Copilot.

To limit the copilot features that the representative can use, create or edit a custom profile and enable specific copilot features for the profile. You can then [assign the custom profile to the service representatives](/dynamics365/customer-service/administer/add-profile-default?context=/dynamics365/contact-center/administer-context).

Perform the following steps to add the Copilot features to the custom experience profile:

1. In Copilot Service admin center, go to [**Experience profiles**](/dynamics365/customer-service/administer/create-agent-experience-profile?context=/dynamics365/contact-center/administer-context) using one of the following navigation options:
   - **Support experience** > **Workspaces**
   - **Copilot for questions and emails** > **Agent access** > **Experience profiles**
1. Select the required experience profile.
1. On the **Productivity pane**, turn on the **Copilot for questions and emails** toggle.

   :::image type="content" source="../media/copilot-help-pane-enable-mini.png" alt-text="Screenshot of the Productivity panel in experience profile." lightbox="../media/copilot-help-pane-enable.png":::|

1. In **Copilot AI features**, select **Edit**.
1. Select the features to enable for the profile, such as **Ask a question**, **Write an email**, **Case summary**, and **Live conversation summary**.
1. Select **Save**.

## Record representative interactions with Copilot

On the **Summaries** and **Copilot for questions and emails** configuration pages, select **Record transcripts of representative interactions with Copilot, representative actions, and representative feedback on AI suggestions** to capture representative interactions and feedback. Representatives can also share feedback about Copilot actions. You can [download Copilot transcript data](/dynamics365/customer-service/develop/reference/entities/msdyn_copilottranscriptdata?context=/dynamics365/contact-center/extend-context) to analyze knowledge sources and build usage reports.

## Assign roles and privileges

By default, only users with the Customer Service Representative role can use Copilot features. Ensure that users with custom roles have the following privileges:

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

Learn more in [Security roles and privileges](/power-platform/admin/security-roles-privileges).

## Next steps

[Enable Copilot case and conversation summaries](copilot-enable-summary.md)  
[Enable Copilot help pane](copilot-enable-help-pane.md)  

### Related information

[Responsible AI FAQ for copilot features](/dynamics365/customer-service/implement/faq-responsible-ai-copilot?context=/dynamics365/contact-center/administer-context)  
[FAQ for Copilot in Customer Service](/dynamics365/customer-service/administer/faq-copilot-features?context=/dynamics365/contact-center/administer-context)  
