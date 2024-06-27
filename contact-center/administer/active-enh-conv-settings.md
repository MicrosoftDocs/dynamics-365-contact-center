---
title: Manage the enhanced Active Conversation settings | MicrosoftDocs 
description: Manage the enhanced Active Conversation settings.
author: gandhamm 
ms.author: mgandham
ms.reviewer: neeranelli
ms.topic: how-to 
ms.date: 12/21/2023
ms.custom: bap-template 
---

# Manage enhanced Active Conversation settings

The enhanced Active Conversation experience displays the customer details that are relevant to your business. When you enable the **Enhanced active conversation form** option, the **Customer 360** component is available on the **Active Conversation** form by default. You can further customize these components in Power Apps.

- **Customer details**: Use the **Customer 360** component in **Account** > **Account form for Conversation Customer Card** form or **Contact** > **Contact form for Conversation Customer Card** to customize the details displayed on **Customer details**.

## Manage Active Conversation form settings

To enable the enhanced Active Conversation form and customize the form, perform the following steps:

1. In Customer Service admin center, go to **Workspaces**.
1. Select **Manage** for **Active conversation form settings** in **Workspaces**.
1. Select the following options:
    - **Enhanced active conversation form** to enable the enhanced Active Conversation experience. The following features are available as a part of the enhanced experience:
      - Configurable **Customer 360** card with inline edit capabilities. 
      - The default form selector to switch between active and closed conversations is hidden.
    - **Customize active conversation form** to display **Queue**, **Start time**, options to save and refresh on the **Active Conversation** form, and enable customizations in [Customizations supported by the Conversation form](supported-customizations.md#customizations-supported-by-the-conversation-form). Select **Power Apps** to further customize the form. If you're customizing the form in Power Apps, we recommend the following guidelines:
       - Reduce the number of custom controls. Keep only the most frequently used controls on the default tab. The remaining data-driven controls should be distributed into secondary tabs to allow the default tab to load quickly. 
       - Limit the amount of customizations using the form Onload event.
       - Limit the amount of external data coming from Canvas apps for efficient and productive forms.
       More information: [Design forms for performance in model-driven apps](/power-apps/maker/model-driven-apps/design-performant-forms)

   > [!NOTE]
   > When **Customize active conversation form** is enabled:
   > - If an agent initiates an outbound call to emergency services, the active conversation form doesn't display the **Save** and **Refresh** options.
   > - If an agent initiates a consult with other agents who are from a different business unit and don't have the read permissions at the organization level for the conversation entity, they won't have access to the conversation.


    :::image type="content" source="../media/enh-active-conv-config.png" alt-text="Configuration settings" lightbox="../media/enh-active-conv-config-max.png"::: 

## Display the form selector on Active Conversation form

By default, the enhanced **Active Conversation** form doesn't display the form selector to switch between open and closed conversations. To allow your users to toggle between open and closed conversations, perform the following steps:

1. In [Power Apps](https://make.powerapps.com/), add the **Show Conversation form selector** setting definition. More information: [Add an existing setting definition](/power-apps/maker/data-platform/create-edit-configure-settings#adding-an-existing-setting-definition)
1.  In the **Edit Show Conversation form selector**, set the **Setting environment value** option to **Yes**. More information: [Update a setting definition](/power-apps/maker/data-platform/create-edit-configure-settings#updating-a-setting-definition)
1. Optionally, in the **Setting app values** section, for a required app, you can set the value to **Yes** in the **New app value**. The tab set at the application level overrides the environment level setting.
1. Save and publish your customizations.
     
    :::image type="content" source="../media/powerapps-unhide-selector-mini.png" alt-text="View the show selector" lightbox="../media/powerapps-unhide-selector.png"::: 


## Disable enhanced customer details

You can choose to display the default **Customer profile** card on the enhanced **Active Conversation** form even when **Enhanced active conversation form** is enabled.

The following options are available out of the box in Power Apps:

|Option   | Description   |
|----------|-----------|
|Disable Customer 360 card for Open Conversation | Set this option to **Yes** to display the default **Customer profile** card.  |

Perform the following steps to revert to the required default experience:

1. In [Power Apps](https://make.powerapps.com/), select the environment that contains your solution.
2. Select **Solutions**, and then select the required solution.
4. Select **Add Existing** > **More** > **Setting**.
1. On the **Add existing Setting Definition** pane, select the required option.
1. Select **Add**.
1.  Go to **Add Existing** > **App** > **Model-driven app**> **Add existing model-driven apps** pane.
1. On the edit pane for the required option, set **Setting environment value**  to **Yes**.
1. Optionally, select **New app value** for the app. For a specified app, the value set at the application level overrides the environment level setting.
1. Select **Publish All Customizations**.


### See also

[View customer information on Active Conversation form](../use/oc-customer-summary.md) <br>
[Get started with Customer Service workspace](../implement/csw-overview.md)
