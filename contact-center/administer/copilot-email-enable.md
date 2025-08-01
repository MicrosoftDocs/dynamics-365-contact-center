---
title: Enable Copilot to draft emails 
description: Learn how to enable the draft an email feature in Copilot to help customer service representatives draft emails faster.
author: gandhamm 
ms.author: mgandham 
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 06/04/2025
ms.update-cycle: 180-days
ms.custom: bap-template 
---

# Enable Copilot to draft emails 

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

Customer Service representatives (service representatives or representatives) can draft emails faster with Copilot. Service representatives can draft emails in the Copilot side pane or inline from the rich text editor. 

## Prerequisites

- [Enable data movement across regions](/power-platform/admin/geographical-availability-copilot#enable-data-movement-across-regions) in Power Platform admin center if your environment doesn't have United States, India, Australia, and United Kingdom as the geography for data processing and storage.
- [Opt in to AI terms to continue with Copilot setup](configure-copilot-features.md#opt-in-to-continue-with-copilot-setup) in Customer Service admin center.


## Enable knowledge sources for Copilot to draft emails

By default, the option to use knowledge sources to draft emails is disabled. If you want Copilot to use knowledge articles or trusted websites to draft emails, you must [enable knowledge sources for Copilot](copilot-enable-help-pane.md#enable-knowledge-base).


## Enable draft an email in the rich text editor

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]


For your service representatives to write an email inline in the rich text editor, do the following steps:

1. In [Power Apps](https://make.powerapps.com/), select the environment that contains your solution.
1. In **Apps**, select the required app to enable the Copilot control in the rich text editor.
1. Select **Settings** and then select **Features**.
1. Switch the **Contextual email drafting with AI** toggle to **Yes**.
1. Select **Save**.

> [!NOTE]
> The Copilot control for rich text editors is available in version two only.

## Enable write an email in the side pane

To enable your service representatives to write an email in the Copilot side pane, perform the following steps in Copilot Service admin center:

1. Go to **Copilot for questions and emails** using one of following options:
      - **Agent Experience** > **Productivity** 
      - **Operations** > **Insights**
1. Select **Manage** in **Copilot for questions and email**. The **Copilot for questions and email** page appears. 
1. Switch the **Write an email - Help pane** toggle to **On**.
1. Select **Save**.

## Enable Copilot to recommend email templates

Select the **Copilot for email templates** checkbox to enable Copilot to recommend email templates. Copilot automatically selects the most appropriate email template and inserts it in the email editor, based on the prompt specified by the service representative. Learn more in [Use Copilot to draft an email in the rich text editor](/dynamics365/contact-center/use/use-copilot-email#use-copilot-to-draft-an-email). This feature is available in the inline email editor only.

### Modify the fields used to draft emails in Copilot help pane

[!INCLUDE[cc-feature-availability](../includes/cc-feature-availability.md)]

You can modify the source case fields that Copilot uses to draft emails and improve the context and accuracy of the results. You can also select a custom field that Copilot uses to generate responses. This feature is available in the Copilot help pane only.

Copilot uses the following out-of-the-box case fields to draft emails:

- Case Title
- Case Description
- Customer Contact
- Subject
- Case Notes
- Email Content

In Copilot Service admin center, go to **Copilot for questions and emails** and then select **Manage data**. The steps to modify the source fields that Copilot uses to draft emails are like the steps to modify the fields used to generate case summaries. Learn more in [modify the fields used to generate case summaries](/dynamics365/customer-service/administer/copilot-map-custom-fields#modify-the-fields-used-to-generate-case-summaries).

> [!NOTE]
> You can't modify the **Case Notes** and **Email Content** field values that Copilot uses to draft emails.

## Next Steps

[Write an email with Copilot](../use/use-copilot-email.md)

### Related information

[Understand Copilot language support](../use/copilot-language-support.md)  
[Manage copilot features](../administer/configure-copilot-features.md)   
[FAQ for Copilot](/dynamics365/customer-service/administer/faq-copilot-features)    
[Responsible AI FAQ for copilot features](/dynamics365/customer-service/implement/faq-responsible-ai-copilot)   
