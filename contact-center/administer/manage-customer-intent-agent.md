---
title: Manage Customer Intent Agent (Preview)
description: Learn how to manage Customer Intent Agent in Dynamics 365. Enable intent discovery, manage intent groups, and improve customer service efficiency.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 01/08/2025
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

[Set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).

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
   > Configure the workstream name in the line of business configuration rules for chat workstreams. Because the chat widget is tightly coupled with the line of business, by specifying the line of business, you can make sure that the chat belongs to the same line of business as its workstream. Otherwise, the chat might end up with a different line of business other than its workstream.

1. Optionally, select **Run backfill**. When selected, it’s used to associate past cases with a line of business for intent discovery. The system makes sure that intent discovery works properly by tagging past cases with the appropriate line of business.
1. Save and close.

Repeat the steps for creating rules and conditions for conversations for the lines of business you’d like to add.

## Manage intent discovery setup

You can enable Customer Intent Agent to analyze past conversations within the Customer Service instance to discover new intents to add into the intent library. After you set it up, the first run of intent discovery analyzes historical data for up to two months. After that, the intent discovery runs daily.

You need to run the AI model on data sources like conversations to identify intent groups and related intents.

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage intent discovery setup**.
1. On the **Manage intent discovery setup** page, select **Add intent discovery setting**.
1. In **Intent discovery settings**, enter the following details:
   - **Name**: An intuitive name that meets your business requirement.
   - **Data source**: Available for conversations only and therefore read-only.
   - **Intent group granularity**: Select **Low**, **Medium**, or **High** in the list. If you select low, fewer intent groups are created, and vice versa happens if you select high. If you select **Medium**, the system creates a balanced number of intent groups between low and high.
   - **Record status**: Select **Pending**, **Approved**, or **Discarded** in the list to indicate the default status that you'd like to set for the newly-discovered intents.
1. If you want to simulate the intent discovery, select **Test**. After the discovery is complete, a simulation of the intent groups is available.
1. Select **Add into job schedule** to run the intent discovery.
1. In **Test results**, select the simulation to view the details. The simulation details, such as status, data source, and intent group granularity are displayed. Simulation uses the last 1000 records to generate intent and intent groups. The simulation helps administrators evaluate the intents and decide on granularity.
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
1. Select the intents in the list that match, and then select **Add**.
1. Select **Save**. The intent group is displayed in the **All intent groups** view.

## Manage instructions (optional)

You can enable Customer Intent Agent to follow instructions that you set up to help resolve intents. 
> [!NOTE]
> As an administrator or supervisor, you must have the Intent Manager role to create instructions.

### Add instructions

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage instructions (optional)**.
1. On the **Manage instructions (preview)** page, select a line of business from the **Select line of business** dropdown list. If you don't specify a line of business, the agent follows organizational level instructions.
1. In the **Line of business instructions (optional)** section, select **Add**.
1. On the **Add instructions** dialog, add the instructions for the line of business. You can enter upto 4000 characters.
Select the **View example instructions** dropdown, if you need to refer to examples to create instructions for your line of business.
1. Select **Save**. Once saved, the agent uses these instructions when interacting with the customer immediately.
1. In the **Instructions for intent groups and intents** section, create instructions for intent groups or intents for the specific line of business.
    1. To create instructions for an intent group, select [Manage intent groups](#manage-intent-groups).
    1. To create instructions for an intent, select [Manage intents](#manage-intents).
1. If you select **Manage intent groups**, select an intent group from the **All intent groups** dropdown list.
    1. On the selected intent group page, **Intent group instructions (optional)** section, select **Add**.
    1. On the **Add Instructions** dialog, add instructions for the intent group. You can enter upto 2000 characters.
    1. To edit the line of business instructions, select **Manage instructions**.
    1. Select **Save**.
1. If you select **Manage intents**, select an intent from the **All intents** dropdown list.
1. On the selected intent page, **Intent instructions (optional)** section, select **Add**.
    1. On the **Add Instructions** dialog, add instructions for the intent. You can enter upto 2000 characters.
    1. Select **Save**.


### Edit or delete instructions

You can edit or delete a line of business from the **Line of business instructions (optional)** section.

1. On the **Manage instructions (preview)** page, select a line of business from the **Select line of business** dropdown list.
1. Select **Edit**.
1. On the **Edit instructions** dialog, make changes in the **Line of business instructions** section.
1. Select **Save**.

Select **Delete** if you want to delete the instructions for the selected line of business. A confirmation message appears once the instructions are deleted


### How to write clear instructions


|Guidelines  |Why it matters  |Example  |
|---------|---------|---------|
|Begin with a clear sentence that defines the agent's role and purpose.    |   Establishes the agent's brand voice and scope, and helps it choose the right tone.      |    "You are a representative from Contoso Coffee, assisting customers with orders and account questions."     |
|Start with a few simple steps that outline the flow, then add details.  |    Follows a consistent sequence that's easy to understand.   |     "1. Clarify the problem. <br> 2. Pick the likely cause. <br> 3. Try one fix at a time." |
|List required checks or prerequisites early.    |     Ensures nothing is missed before actions or lookups.    | "If the user reports an issue, first confirm the product model and purchase date."|
|Explain what's out of scope or not allowed.|     Prevents unnecessary work or compliance issues.   | "Don't ask for social security numbers or payment card details."|
|Use simple if-then logic for decision points. | Reduces ambiguity without technical syntax.| "If the product is under warranty, offer a replacement. Otherwise, provide repair options."|
|Define when to escalate issues or hand them off to service representatives. |    Ensures a smooth transition when the process can't continue.       |  "Hand-off to a support rep if the customer requests a refund over $100 or expresses dissatisfaction."|
|Break multi-part instructions into smaller steps.      |   Avoids missed details and simplifies handoffs between people or steps.|  Instead of "Verify account and reset password', split into: “1. Verify account. 2. Reset password.”        |
|Don't use unnecessary technical or system jargon. |  Keeps instructions readable and usable without requiring technical expertise.|  For example, use: "Look up the customer’s order in the system", instead of “Execute GET request on Order API.” |

## Manage connectors for AI agents (optional)

Connectors let systems work together, move data, and let AI agents autonomously complete tasks to resolve issues. 

1. On the **Customer Intent Agent (preview)** page, select **Manage** for **Manage connectors for AI agents (optional)**.
1. On the **Manage custom connectors (preview)** page, select **Add connector**. Learn how to add connector in [Create a custom connector](/connectors/custom-connectors/define-blank).
1. On the **Select a connector** dialog, search and select a connector. You can add upto 30 connectors.    
1. Select **Next**.
1. On the **Set up the connector** dialog, select a connection from the **Connection** dropdown. You can also create a new connection in Power Platform. Learn more in [Add connection references to a solution](/power-apps/maker/data-platform/create-connection-reference#add-connection-references-to-a-solution).
    > [!NOTE]
    > Make sure that the connection you select is shared with one of the following service principals, as per your organization. 
    - Dynamics 365 Analytics (61d02d70-ab6c-4569-be48-787ea2cda65d) 
    - Dynamics CCA Data Analytics - PPE (7c58187c-f28c-4cfb-998c-3d6ba580192c) 
    - Dynamics 365 Analytics - Test (079f5a03-090f-4720-90b9-e03942091e6e) 

    Learn more in [Share a custom connector in your organization](connectors/custom-connectors/share).
1. Specify the type of use for connector, **General** or **For specific intents**.
1. If you select **For specific intents**, you need to map the custom connector as a solution.
1. Select **Save**.

To map a connector to an intent:

1. Select **Manage** for **Manage intents** on the **Customer Intent Agent (preview)** page.
1. Select the specific intent, and on the intent page, in the **Solution (Optional)** section, select the **Connectors** option, and then select **Add**.
1. On the **Add a solution** page, search and select a connector for the intent. Only connectors created for use with specific intents are shown.
1. Select **Save and close**.
> [!NOTE]
> To map a connector to an intent, the connector must have one action only. If your connector has multiple actions, you can't execute any actions for that intent.

### Edit or delete connectors

You can edit or delete a connector from the **Manage connectors for AI agents (optional)** page. 

1. On the **Manage custom connectors (preview)** page, select a connector.
1.  Select **Edit**.
1. On the **Edit connector** dialog, you can select your connection and specify the type of use for your connector.
1. Select **Save**.

Select **Delete** if you want to delete the connector. A confirmation message appears once the connector is deleted.

### Related information

[Enable intent for support representatives](enable-intent-for-service-reps.md)    
[Use intent agents](../use/use-intent-suggestions.md)   



