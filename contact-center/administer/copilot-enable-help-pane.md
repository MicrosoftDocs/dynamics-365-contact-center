---
title: Enable features in Copilot pane
description: Learn how to enable features that appear in the Copilot help pane to increase customer service representative productivity.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 03/07/2025
ms.custom: bap-template 
---

# Enable features in Copilot pane

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

The Copilot help pane allows customer service representatives (service representatives or representatives) to use Copilot features such as respond to questions, compose an email, and draft a chat response in Contact Center workspace and Customer Service workspace.

## Prerequisites

- You have the System Administrator role.
- If you aren't in the North America region and you want to use the web search powered by Bing feature, you must enable data movement across regions and Bing search in Power Platform admin center. See [Enable data movement across regions](/power-platform/admin/geographical-availability-copilot).

   :::image type="content" source="../media/ppac-gen-ai-features.png" alt-text="Power Platform Admin center bing chat.":::

## Enable Copilot assist features

Perform the following steps to enable the Copilot features in Contact Center admin center or Customer Service admin center:

1. Use one of the following navigation options:
      - **Agent Experience** > **Productivity** > **Copilot for questions and email**
      - **Operations** > **Insights** > **Copilot for questions and email**
1. Select **Manage** in **Copilot for questions and email**. The **Copilot for questions and email* page appears. You can select the Copilot features you'd like to enable for service representatives on this page.

     :::image type="content" source="../media/copilot-admin-email-mini.png" alt-text="Screenshot of ask a question in Copilot pane." lightbox="../media/copilot-admin-email.png":::


## Enable ask a question

Select **Make Copilot available to agents** in the **Copilot for questions and email** page of Customer Service admin center. The **Ask a question** tab on the **Copilot for questions and email** appears when service representatives sign in to Customer Service workspace. Agents can ask questions conversationally, and Copilot answers the questions based on the internal knowledge base sources.

## Enable proactive prompts in ask a question

Proactive prompting enables service representatives to discover and prompt Copilot effortlessly, without the need for manual typing. This saves the service representative’s time and improves the quality of their overall experience.

You can enable and configure the prompts that appear in the **Ask a question** tab. You can configure the following prompts in Contact Center admin center or Customer Service admin center:

1.	Go to **Agent Experience** > **Productivity** >, and select **Manage** for **Copilot for questions and emails**.
1.	On the **Copilot for questions and emails** page, select **Ask a question**.
1. On the **Manage prompt settings** page, select the following as required:
    - **Suggested prompts**
    - **Proactive insights**
3.	In the **Prompts from my organization** section, select **Add new prompt** to add the prompts that you would like to use.
4.	Select **Save and close**.

## Enable draft a response (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

Select **Suggest a response (preview)** in the **Copilot for questions and email** page of Contact Center admin center or Customer Service admin center. The one-click response generation button appears on both the communication panel for a conversation and on the **Ask a question** tab on the Copilot help pane in Customer Service workspace. Copilot retrieves the context and drafts the response based on the knowledge resources configured for your organization.

## Configure knowledge sources

You can configure the knowledge base for Copilot to generate responses.

### Prerequisites

Make sure that you have [knowledge management](/dynamics365/customer-service/administer/set-up-knowledge-management-embedded-knowledge-search#setup-overview) configured in your environment and your knowledge article parameters are as follows:
   - Updated with the latest version
   - The state is set to Published

> [!NOTE]
 > - Copilot uses the content attribute only in the knowledge article table to generate responses for ask a question, write an email, and draft a chat features. You can't customize this behavior.
> - Copilot uses knowledge articles tagged with the same language as the UI to generate responses.

### Enable knowledge base

Select **Knowledge base** to allow Copilot to use internal knowledge base resources for generating responses. Then information is used for the ask a question and draft an email in the Copilot help pane and rich text editor. By default, this option is disabled.

If you've disabled the knowledge base option, agents can use Copilot to draft an email using the **Suggest a call**, **Request more information**, **Empathize with feedback** and **Custom** prompts.

### Add trusted webpages as sources

[!INCLUDE [cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

You can select **Add web address** in **Web resources** to add trusted domains. You can add up to five trusted web domains for Copilot to search and generate responses from. Copilot searches for information up to two levels down from the configured domain. You must enable the Bing Search in Power Platform admin center to add trusted web sources. See [Enable data across geographic locations](/microsoft-copilot-studio/manage-data-movement-outside-us#enable-data-across-geographic-locations).

Copilot uses articles that are two nodes down the configured domain.

> [!NOTE]
> - The knowledge base content is refreshed every day.
> - External websites are used by Copilot to draft emails and chat replies only.

## Enable translation

Select **Let agents translate responses** to allow service representatives to translate responses generated by Copilot to their preferred language. Agents can choose from a list of languages that your organization has added to Dynamics 365 Customer Service.

## Set up filters

Filters enable Copilot to generate responses based on a specific set of topics. You can set up filters for ask a question and draft a response.

> [!NOTE]
> We recommend that the appropriate knowledge content is available for the filters you have set so that service representatives can see the expected responses. 

You can apply the filters in the following sections.

### Preset filters

Specify filters that are applied by default in the background to filter knowledge base articles. Agents can't see these filters. You can set predefined filters for ask a question and draft a response features as follows:
 1. Select **Manage Filters** in **Filters**. The **Manage filters** pane appears.
 1. Select **Manage rules** in **Preset filters** for the required feature.
 1. Specify the required conditions for the filter.
 1. Select **Finish editing**.
    
### Agent filters

 Specify the filters that service representatives can apply to further filter and refine Copilot responses. Representatives can see and select or deselect these filters in the Copilot help pane for the ask a question feature.  If a filter isn't configured as an agent filter, it operates in the background and isn't visible to agents.

To configure an agent filter, do the following steps:
1. Select **Add Filter** for **Agent Filters**.
1. Specify the required knowledge base field that representatives can use. You can also specify the display name and add the values from the field that the service representative can select.
1. Turn on the **Filter status** toggle. This toggle must be turned on for the service representative to see the filter.
1. Select **Finish editing**. 

### Automated filters

Specify the filters that are automatically applied. The service representatives don't need to explicitly set them in the Copilot help pane. To configure automated filters, do the following steps:

1. Select **Add Filter** for **Automated Filters**.
1. Specify the required knowledge base field and the rules that correspond to the field's value. The filter rule is applied only on the record type the service representatives is currently working on.
1. Turn on the **Use untagged content if the field value is null** toggle to view all the content if the field value doesn't match the specified value.
1. Turn on the **Allow agents to view or change this filter** toggle for service representatives to see a visual cue that the automated filter is applied and change the filtering options. Based on your setting, the following actions apply: 
   - **On**: The application prompts you to create a corresponding agent filter for the same knowledge attribute in **Agent Filters** Representatives then see the filters on the Copilot help pane.
   -  **Off**: Agents can't see the filter on the Copilot help pane. The filters operate in the background without any service representative notifications.
1. Select **Finish editing**.

> [!NOTE]
> You can add up to five filters per category.

### Features supported with different knowledge sources

The following table summarizes the Copilot features supported for a configured knowledge source.

| Feature | Knowledge base | External web resources | Knowledge sources in Copilot Studio|
|-------|----------|---------|--------|
|Ask a question |✔|X| ✔|
|Write an email | ✔|✔|X|
|Draft a response |✔|✔|X|

### Related information

[Use Copilot to solve customer issues](../use/use-copilot-features.md)
