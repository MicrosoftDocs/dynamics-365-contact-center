---
title: Enable Copilot to draft emails 
description: Learn how to enable Copilot email drafting in the rich text editor and Copilot help pane.
author: gandhamm 
ms.author: mgandham 
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 08/27/2026
ms.update-cycle: 180-days
ms.custom: bap-template 
---

# Enable Copilot to draft emails 

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

Customer service representatives (service representatives or representatives) can use Copilot to draft emails in the help pane or inline in the rich text editor.

## Prerequisites

- [Enable data movement across regions](/power-platform/admin/geographical-availability-copilot#enable-data-movement-across-regions) in Power Platform admin center if your environment doesn't have United States, India, Australia, and United Kingdom as the geography for data processing and storage.
- [Opt in to AI terms to continue with Copilot setup](configure-copilot-features.md#opt-in-to-continue-with-copilot-setup) in Customer Service admin center.

## Enable knowledge sources for Copilot to draft emails

By default, the option to use knowledge sources to draft emails is disabled. If you want Copilot to use knowledge articles or trusted websites to draft emails, you must [enable knowledge sources for Copilot](copilot-enable-help-pane.md#customer-support-agent).

## Enable email drafting in the rich text editor

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

To enable service representatives to draft an email inline in the rich text editor:

1. In [Power Apps](https://make.powerapps.com/), select the environment that contains your solution.
1. In **Apps**, select the required app to enable the Copilot control in the rich text editor.
1. Select **Settings**.
1. Select **Features**.
1. Switch the **Contextual email drafting with AI** toggle to **Yes**.
1. Select **Save**.

> [!NOTE]
> The Copilot control for rich text editors is available in version two only.

## Enable email drafting in the help pane

To enable service representatives to draft an email in the Copilot help pane, complete these steps in Copilot Service admin center:

1. Go to **Copilot for questions and emails** by using one of the following options:
      - **Agent Experience** > **Productivity** 
      - **Operations** > **Insights**
1. Under **Copilot for questions and emails**, select **Manage**.
1. Turn on **Help pane - Write an email:**
1. Select **Save**.

## Enable Copilot-recommended email templates

Select the **Copilot for email templates** checkbox to enable Copilot to recommend email templates. Copilot automatically selects the most appropriate email template and inserts it in the email editor, based on the prompt specified by the service representative. Learn more in [Use Copilot to draft an email in the rich text editor](/dynamics365/contact-center/use/use-copilot-email#use-copilot-to-draft-an-email). This feature is available in the inline email editor only.

## Modify the fields used to draft emails in Copilot help pane

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

You can modify the source case fields that Copilot uses to draft emails and improve the context and accuracy of the results. You can also select a custom field that Copilot uses to generate responses. This feature is available in the Copilot help pane only.

Copilot uses the following out-of-the-box case fields to draft emails:

- Case Title
- Case Description
- Customer Contact
- Subject
- Case Notes
- Email Content

In Copilot Service admin center, go to **Copilot for questions and emails**, and then select **Manage data**. Follow the steps to [modify the fields used to generate case summaries](/dynamics365/customer-service/administer/copilot-map-custom-fields#modify-the-fields-used-to-generate-case-summaries).

> [!NOTE]
> You can't modify the **Case Notes** and **Email Content** field values that Copilot uses to draft emails.

## Next steps

[Write an email with Copilot](../use/use-copilot-email.md)

## Related information

[Understand Copilot language support](../use/copilot-language-support.md)  
[Configure Copilot features](../administer/configure-copilot-features.md)
[FAQ for Copilot](/dynamics365/customer-service/administer/faq-copilot-features)    
[Responsible AI FAQ for copilot features](/dynamics365/customer-service/implement/faq-responsible-ai-copilot)   
