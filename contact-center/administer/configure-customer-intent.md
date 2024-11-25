---
title: Manage intent using Copilot (preview)
description: 
author: neeranelli
ms.author: nenellim
ms.reviewer: 
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/14/2024
ms.custom: bap-template
---

# Manage intent using Copilot

Customer intent agent uses generative AI to autonomously discover ongoing intents from your customer service instance, analyzing past interactions to create an intent library that enhances dynamic conversations. The service representatives use the information to quickly understand customer needs, guide conversations with follow-up questions, and provide tailored solutions in real time.

Copilot presents a curated list of questions and suggested solutions in the chat response box, which enhances efficiency by reducing manual typing. For self-service, Copilot generates relevant follow-up questions and uses the information to query the knowledge source, leading to higher deflection rates and allowing representatives to focus on cases that require manual intervention.

Use the information in this article to manage the intents in Contact Center admin center or Customer Service admin center in your Dynamics 365 instance.

## Enable customer intent agent

1. In Contact Center admin center or Customer Service admin center, select **Intent** under **Customer support**.
1. On the **Customer Intent Agent (preview)** page that appears, enable the **Turn on Customer Intent Agent** toggle.

## Manage intent discovery setup

You can enable customer intent agent to analyze past conversations within the Customer Service instance to discover new intents to add into the intent library. After you set it up, the first run of intent discovery analyzes historical data for up to two months. After that, the intent discovery runs daily.

You need to run the AI model on data sources like cases and conversations to identify intent groups and related intents.

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage intent discovery setup**.
1. On the **Manage intent discovery setup** page, select **Add intent discovery setting**.
1. In **Intent discovery settings**, enter the following details:
   - **Name**: An intuitive name that meets your business requirement.
   - **Data source**: Available for conversations only and therefore read-only.
   - **Data granularity**: Select **Low**, **Medium**, or **High** in the list. If you select low, fewer intent groups are created.
   - **Record status**: Select **Pending**, **Approved**, or **Discarded** in the list to indicate the default status that you'd like to set for the newly-mined intents.
1. If you want to simulate the intent discovery, select **Simulate**. After the simulation is complete, you can export the simulation data using the Export to Excel option to validate the intent groups.

After the first run of the intent discovery, the intent groups are listed on the **All intent groups** page.


## Manage intent groups

The intent groups that the AI model identifies are displayed on the **All intent groups** page. You can manage the intent groups by reviewing, approving, or editing the intents in them.

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage intent groups and intents**. The **All intent groups** page displays the list of intents that the AI model discovered. If you create a custom intent group, the intent source shows as **Admin edited**. The **Intents** column displays the number of intents in each intent group.
    
   :::image type="content" source="../media/list-of-intent-groups.png" alt-text="Screenshot of intent groups list.":::

1. Select an intent group to edit its intents. The `<intent_group_name>` page displays the details, such as review status and the list of intents in the group.

   :::image type="content" source="../media/manage-intents.png" alt-text="Screenshot of manage intents in intent group.":::

1. Select **Manage intents** to add new intents or remove existing ones.
1. On the **Manage intents** dialog, you can do the following updates:
   - Select **Add intents** > **Add existing**, and select the intents that you want to add to the group. A message appears stating that changing the intents might affect other processes. 
   - Select **Add**. The intents are added to the list.
   - Select an intent and do the following:
      - Discard an approved intent. The intent doesn't appear for selection in the **Add intents** list of any intent group.
      - Update the intent name. We recommend to update the name to address typos only. If you change the name, it can affect the accuracy of the AI model.
      - Remove an intent from the intent group.
1. Select **Save**.

### Create a custom intent group 

1. On the **All intent groups** page, select **New** to create a custom intent group.
1. On the **New intent group** dialog, in **Define intent group**, enter a name and select a review status.
1. Select **Next**.
1. On the page that appears, select **Add**.
1. Select the intents in the list that match and select **Add**.
1. Select **Save**. The intent group is displayed in the **All intent groups** view.
 
### Related information

[Enable intent for support representatives]  
[Use intent agents]  



