---
title: Manage Customer Intent Agent (Preview)
description: Learn how to manage Customer Intent Agent in Dynamics 365. Enable intent discovery, manage intent groups, and improve customer service efficiency.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 09/17/2025
ms.update-cycle: 180-days
ms.custom:
  - bap-template
  - ai-gen-docs-bap
  - ai-gen-description
  - ai-seo-date:03/25/2025
---

# Manage Customer Intent Agent (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Customer Intent Agent uses generative AI to autonomously discover intents from your customer service instance, analyzing past interactions to create an intent library that enhances dynamic conversations. The customer service representatives (service representatives or representatives) use the information to quickly understand customer needs, guide conversations with follow-up questions, and provide tailored solutions in real time.

The AI agent presents a curated list of questions and suggested solutions in the chat response box, which enhances efficiency by reducing manual typing. For self-service, the agent generates relevant follow-up questions and uses the information to query the knowledge source, leading to higher deflection rates and allowing representatives to focus on cases that require manual intervention.  

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

Use the information in this article to manage the intents in Copilot Service admin center.

## Prerequisites

- [Set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- The Intent Manager role to create instructions.

## Enable Customer Intent Agent

1. In the site map of Copilot Service admin center, select **Intent** under **Customer support**.
1. On the **Customer Intent Agent (preview)** page that appears, enable the **Turn on Customer Intent Agent** toggle.

## Manage lines of business

A line of business can be a service, product, product category, or the way your company organizes and supports its business activities. It's used as a partition that represents a specific set of intents and intent groups in a large enterprise. You need to add lines of business if you want to enable intent-based routing for a selective set of workstreams and queues. Otherwise, intent-based routing is enabled for the whole organization.
The following entities are associated with a line of business:

- Intents and intent groups
- User groups (A representative can be a part of many user groups that belong to different lines of business)
- Workstreams
- Queues

### Add line of business

1. In the site map of Copilot Service admin center, go to **Intent**, and then select **Manage** for **Add Line of business (Optional)**.
1. On the **Manage Lines of business** page, select **Add Line of business**.
1. Enter the name and description that indicates the line of business.
1. Select **Add**. The line of business is listed in the **Lines of business** table.

### Create rules for cases and conversations

For every line of business that you identify, you can create rules for cases and conversations. You can create one rule only (one each for a case and conversation) per line of business. During runtime, for chat and other channels, Copilot and intent-based suggestions must be enabled to determine the intent.

1. On the **Manage Lines of business** page, in **Case Rules**, select **Create rule**.
1. On the dialog that appears, enter the rule name and select a line of business.
1. In **Conditions**, define the conditions for the rules to run.
   > [!IMPORTANT]
   > Configure the workstream name in the line of business configuration rules for chat workstreams. Because the system tightly couples the chat widget with the line of business, specifying the line of business helps you make sure that the chat belongs to the same line of business as its workstream. Otherwise, the chat might end up with a different line of business other than its workstream.

1. Optionally, select **Run backfill**. When selected, it’s used to associate past cases with a line of business for intent discovery. The system makes sure that intent discovery works properly by tagging past cases with the appropriate line of business.
1. Save and close.

Repeat the steps for creating rules and conditions for conversations for the lines of business you’d like to add.

## Manage intent discovery setup

You can enable Customer Intent Agent to analyze past conversations within the Customer Service instance to discover new intents to add into the intent library. After you set it up, the first run of intent discovery analyzes historical data for up to two months. After that, the intent discovery runs daily.

You need to run the AI model on data sources like conversations to identify intent groups and related intents.

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage intent discovery setup**.

1. On the **Manage intent discovery setup** page, select **Add intent discovery setting**.
1. In **Intent discovery settings**, enter the  details:
   - **Name**: An intuitive name that meets your business requirement.
   - **Data source**: Available for conversations only and therefore read-only.
   - **Intent group granularity**: Select **Low**, **Medium**, or **High** in the list. If you select low, fewer intent groups are created, and vice versa happens if you select high. If you select **Medium**, the system creates a balanced number of intent groups between low and high.
   - **Record status**: Select **Pending**, **Approved**, or **Discarded** in the list to indicate the default status that you'd like to set for the newly discovered intents.
1. If you want to simulate the intent discovery, select **Test**. After the discovery is complete, a simulation of the intent groups is available.
1. Select **Add into job schedule** to run the intent discovery.
1. In **Test results**, select the simulation to view the details. The simulation details, such as status, data source, and intent group granularity are displayed. Simulation uses the last 1,000 records to generate intent and intent groups. The simulation helps administrators evaluate the intents and decide on granularity.
1. Select the simulation, and then select **Export to Excel** option. The Excel file is downloaded to your local computer.
1. After you validate and choose the intent group granularity that reflects your business needs, select **Set up intent discovery** to run the intent discovery.
   > [!NOTE]
   > You can view the simulation for successful runs only. The Excel file is empty for failed simulations.

After the first run of the intent discovery, the intent groups are listed on the **All intent groups** page.

## Manage intents

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage intents**.

1. Select **New**, and enter intent details as follows:
   - **Name**: Enter a name for the intent. The name should be intuitive and meet your business requirement.
   - **Intent group**: Select the intent group that you want to associate with the intent.
   - **Line of business**: Select the line of business that you want to associate with the intent.
   - **Review status**: Select **Pending**, **Approved**, or **Discarded** in the list to indicate the default status that you'd like to set for the intent.
   - **Use in AI Agent**: Select **Yes** if you want to use the intent in the AI agent.
1. Save the information.
1. On the **Attributes** tab, add the attributes that you want to associate with the intent. The attributes are used to provide additional information about the intent. You can add multiple attributes for an intent.
1. On the **Knowledge articles** tab, select **Add** to associate the knowledge articles with the intent. The knowledge articles are used to provide additional information about the intent. You can add multiple knowledge articles for an intent.

  :::image type="content" source="../media/create-intent.png" alt-text="Screenshot of create intent page with all details and attributes." lightbox="../media/create-intent.png":::

You can manage the intents to be used in AI agent in bulk. On the **Manage intents** page, select the approved intents, and on the command menu, select **Use in AI agent**. The intents are used in the AI agent.

## Manage intent groups

You can logically organize the intents into intent groups. The intent group represents the business expertise that's needed to solve the intents belonging to the group. The intent groups that the AI model identifies are displayed on the **All intent groups** page. You can manage the intent groups by reviewing, approving, or updating the intents in them.

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage intent groups and intents**. The **All intent groups** page displays the list of intents that the AI model discovered. If you create a custom intent group, the intent source shows as **Admin edited**. The **Intents** column displays the number of intents in each intent group.

   :::image type="content" source="../media/list-of-intent-groups.png" alt-text="Screenshot of intent groups list." lightbox="../media/list-of-intent-groups.png":::

1. Select an intent group to manage its intents. The `<intent_group_name>` page displays the details, such as review status and the list of intents in the group.

   :::image type="content" source="../media/manage-intents.png" alt-text="Screenshot of manage intents in intent group." lightbox="../media/manage-intents.png":::

1. Select **Manage intents** to add new intents or remove existing ones.
1. On the **Manage intents** dialog, you can do the  updates:
   - Select **Add intents** > **Add existing**, and select the intents that you want to add to the group. A message appears, stating that changing the intents might affect other processes. 
   - Select **Add**. The intents are added to the list.
   - Select an intent, and then do the following actions:
      - Discard an approved intent. The intent doesn't appear for selection in the **Add intents** list of any intent group.
      - Update the intent name. We recommend updating the name to address typos only. If you change the name, it can affect the accuracy of the AI model.
      - Remove an intent from the intent group.
1. Select **Save**.

### Create a custom intent group

1. On the **All intent groups** page, select **New** to create a custom intent group.

1. On the **New intent group** dialog, in **Define intent group**, enter a name and select a review status.
1. Select **Next**.
1. On the page that appears, select **Add**.
1. Select the intents in the list that match, and then select **Add**.
1. Select **Save**. The intent group is displayed in the **All intent groups** view.

## Manage instructions (optional)

Set up instructions to streamline Customer Intent Agent behavior. You can add instructions for the line of business, intent groups, and intents.

To add instructions, complete the following steps:

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage instructions (optional)**.

1. On the **Manage instructions (preview)** page, select a line of business in **Select line of business**. If you don't specify a line of business, Customer Intent Agent follows the default instructions for the organization.
1. In the **Line of business instructions (optional)** section, select **Add**.
1. On the **Add instructions** dialog, add the instructions for the line of business. You can enter up to 4,000 characters. Expand **View example instructions** to view sample instructions.
1. Select **Save**. The instructions are available immediately for use by Customer Intent Agent.
1. In the **Instructions for intent groups and intents** section, select the following options to create instructions for intent groups and intents.
   - **Manage Intent groups**: In the list of intent groups page, select an intent group.
       1. On the `<intent_group_name>` page, in **Intent group instructions (optional)** , select **Add**. The **Add instructions** dialog appears.
       1. Add instructions for the intent group. You can enter up to 2,000 characters.
       1. Save and close.
   - **Manage intents**: In the list of intents page, select an intent.
       1. On the `<intent_name>` page, in **Intent instructions (optional)** , select **Add**. The **Add instructions** dialog appears.
       1. Add instructions for the intent. You can enter up to 2,000 characters.
       1. Save and close.

You can edit or delete instructions for a line of business, intent groups, or intents using the **Edit** and **Delete** options in the instructions section of the corresponding pages.

### How to write clear instructions

|Guidelines  |Why it matters  |Example  |
|---------|---------|---------|
|Start with a concise statement that defines the objective of Customer Intent Agent.    |   Establishes the brand voice and scope, and helps Customer Intent Agent choose the right tone.      |    "You're a representative from Contoso Coffee, assisting customers with orders and account questions."     |
|Start with steps that outline the flow and then add details.  |    Creates a logical, easy-to-follow sequence.   | 1. Clarify the problem. <br> 2. Pick the likely cause. <br> 3. Try one fix at a time. |
|List required checks or prerequisites.    |     Ensures that required information isn't missed before the agent takes action or performs lookups.   | If the user reports an issue, first confirm the product model and purchase date.|
|Explain what's out of scope or not allowed.|     Prevents unnecessary work or compliance issues.   | Don't ask for social security numbers or payment card details.|
|Use if-then logic for decision points. | Reduces ambiguity without technical syntax.| If the product is under warranty, offer a replacement. Otherwise, provide repair options.|
|Specify when to escalate issues or hand them off to service representatives. |    Ensures a smooth transition when automated resolution isn't possible. |  Hand-off to a service representative if the customer requests a refund over $100 or expresses dissatisfaction.|
|Break multi-part instructions into smaller steps.      |   Avoids missed details and simplifies handoffs.|  Instead of Verify account and reset password, split into: 1. Verify account. 2. Reset password.       |
|Don't use unnecessary technical or system jargon. |  Keeps instructions readable and usable without requiring technical expertise.|  Use Look up the customer’s order in the system, instead of Execute GET request on Order API. |

## Manage connectors for AI agents (optional)

Connectors let systems work together, transfer data, and allow AI agents to automatically handle tasks for issue resolution.

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage connectors for AI agents (optional)**.

1. On the **Manage custom connectors (preview)** page, select **Add connector**. Learn how to add a connector in [Create a custom connector](/connectors/custom-connectors/define-blank).
1. On the **Select a connector** dialog, search and select a connector. You can add up to 30 connectors.
1. Select **Next**.
1. On the **Set up the connector** dialog, select a connection from the **Connection** dropdown. You can also create a new connection in Power Platform. Learn more in [Add connection references to a solution](/power-apps/maker/data-platform/create-connection-reference#add-connection-references-to-a-solution).
    > [!NOTE]
    > Make sure that the connection you select is shared with the **Dynamics 365 Analytics** service principal. 
    
    Learn more in [Share a custom connector in your organization](/connectors/custom-connectors/share).
1. Specify if the type for the connector is **General** or **For specific intents**.
1. If you select **For specific intents**, you need to map the custom connector as a solution as explained in the section that follows.
1. Select **Save**.

### Map a connector to an intent

1. Select **Manage** for **Manage intents** on the **Customer Intent Agent (preview)** page.

1. Select the specific intent, and on the intent page, in the **Solution (Optional)** section, select the **Connectors** option, and then select **Add**.
1. On the **Edit solution** page, search and select a connector for the intent. The application displays connectors created for use with specific intents only.
1. Select **Save and close**.

> [!NOTE]
> - To map a connector to an intent, the connector must have one action only. If your connector has multiple actions, you can't run any actions for that intent.
> - After you add or remove a connector, changes can take up to 15 minutes to appear in the Customer Intent Agent.

You can edit or delete a connector after you select the required connector on the **Manage custom connectors (preview)** page. 

## Configure knowledge sources for an intent

### Map an intent to knowledge articles

You can add knowledge articles to an intent directly from the intent page, so that users see articles specified for the intent only. 

1. Select the intent for which you want to add knowledge articles and custom AI agent.
1. On the `<intent_name>` page, scroll to the bottom and in **Solution (Optional)**, select **Dynamics 365 knowledge articles**, and then select **Add**. A list of published knowledge articles appears.
1. Select the articles pertinent to the intent and save and close.
1. Select **Custom AI agent**, and then select **Add**.
1. In the list of agents that appears, select an AI agent and save and close.

### Specify filters for Dynamics 365 knowledge articles for Customer Intent Agent

You can specify knowledge sources for intents by providing specific filters.

1. On the **Customer Intent Agent (preview)** page, **Instructions and solutions** section, select **Manage** for **Knowledge sources for intents**.
1. On the **Knowledge source for Customer Intent Agent** page, select a knowledge source.
1. Select **Dynamics 365 knowledge**, then select **Manage filters** to specify your filters.
   1. On the **Manage knowledge filters for intents** dialog, add or remove the filters, as required. The filters you specify on this dialog, apply only to the Dynamics 365 knowledge articles for intent management and intent-based features.
   1. Select **Save**.

### Add knowledge from Copilot Studio

1. On the **Customer Intent Agent (preview)** page, **Instructions and solutions** section, select **Manage** for **Knowledge sources for intents**.
1. On the **Knowledge source for Customer Intent Agent** page, select **Copilot Studio knowledge (preview)**.
1. Select **Save**.

You should have already set up knowledge for your agent in Copilot Studio before you enable this option. Learn more in [Connect Customer Intent Agent to Copilot Studio knowledge](set-up-intent-agent.md#connect-customer-intent-agent-to-copilot-studio-knowledge).


### Related information

[Enable intent for support representatives](enable-intent-for-service-reps.md)  
[Use intent agents](../use/use-intent-suggestions.md)  
[Create rollout plans](create-rollout-plans.md)  
