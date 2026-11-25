---
title: Manage Customer Intent Agent
description: Learn how to manage Customer Intent Agent in Dynamics 365. Enable intent discovery, manage intent groups, and improve customer service efficiency.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/24/2026
ms.update-cycle: 180-days
ai-usage: ai-assisted
ms.custom:
  - bap-template
  - ai-gen-docs-bap
  - ai-gen-description
  - ai-seo-date:03/25/2025
---

# Manage Customer Intent Agent

Customer Intent Agent uses generative AI to autonomously discover intents from your customer service instance, analyzing past interactions to create an intent library that enhances dynamic conversations. The customer service representatives (service representatives or representatives) use the information to quickly understand customer needs, guide conversations with follow-up questions, and provide tailored solutions in real time.

The AI agent presents a curated list of questions and suggested solutions in the chat response box, which enhances efficiency by reducing manual typing. For self-service, the agent generates relevant follow-up questions and uses the information to query the knowledge source, leading to higher deflection rates and allowing representatives to focus on cases that require manual intervention.  

Use the information in this article to manage the intents in Copilot Service admin center.

## Prerequisites

- [Set up a pay-as-you-go plan](/dynamics365/customer-service/administer/setup-pay-as-you-go?context=/dynamics365/contact-center/context/administer-context).
- The Intent Manager role to create instructions and the CSR Manager role.

## Enable Customer Intent Agent

1. In the site map of Copilot Service admin center, select **Intent** under **Customer support**.
1. On the **Customer Intent Agent** page that appears, enable the **Turn on Customer Intent Agent** toggle.

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

### Discover line of business unique IDs

You might need to find the unique ID for your line of business when building use cases for your Customer Intent Agent. For example, you might want to set the line of business to integrate a [Copilot voice agent](set-up-voice-agents-to-use-intents.md) or [Copilot agent](set-up-intent-agent.md).

You can find the unique IDs for your line of business by using Open Data Protocol (OData) queries on the entity msdyn_intentfamilies table and finding the msdyn_intentfamilyid field. For example, https://[Organization domain]/api/data/v9.2/msdyn_intentfamilies?$select=msdyn_intentfamilyid,msdyn_name.

### Create rules for cases, conversations, and emails

For every line of business that you identify, create rules for cases, conversations, and emails. You can create only one rule each for a case and conversation per line of business. During runtime, for chat and other channels, Copilot and intent-based suggestions must be enabled to determine the intent.

1. On the **Manage Lines of business** page, in **Case Rules**, select **Create rule**.
1. On the dialog that appears, enter the rule name and select a line of business.
1. In **Conditions**, define the conditions for the rules to run.
   > [!IMPORTANT]
   > Configure the workstream name in the line of business configuration rules for chat workstreams. Because the system tightly couples the chat widget with the line of business, specifying the line of business helps you make sure that the chat belongs to the same line of business as its workstream. Otherwise, the chat might end up with a different line of business other than its workstream.

1. Save and close.

Repeat the steps for creating rules and conditions for conversations and emails for the lines of business you want to add.

## Manage intent discovery setup

You can enable Customer Intent Agent to analyze past conversations within the Customer Service instance to discover new intents to add into the intent library. After you set it up, the first run of intent discovery analyzes historical data for up to two months. After that, the intent discovery runs daily.

You need to run the AI model on data sources like conversations to identify intent groups and related intents.

1. On the **Customer Intent Agent** page, select **Manage** for **Manage intent discovery settings (optional)**.
1. Select **Edit** for business profile to provide a business profile to consider while mining intents. (optional)
1. On the **Manage intent discovery setup** page, select **Setup intent discovery for a new LOB**.
1. In **Add settings for intent discovery**, enter the details:
   - **Name**: An intuitive name that meets your business requirement.
   - **Data source**: Available for conversations only and therefore read-only.
   - **Data source rules**: Create a rule for the selected data sources. This step is required. Only cases, conversations, and emails that meet the rules you set are used for intent discovery.
   
1. Provide guidance to shape the granularity of generated intents and the total number of intents and intent groups. With guidance, you can also control when a case should map to an existing intent versus when it warrants a new one, and the heuristic used to classify and cluster cases. (optional)
1. Select **Auto-promote high-confidence intents** to auto-promote intents that meet the confidence and case or conversation count thresholds you set. Choose the maximum promotions per run and whether to auto-promote intents as pending or approved. (optional)
1. If you want to simulate the intent discovery, select **Test**. After the discovery is complete, a simulation of the intent and intent groups is available.
1. Select **Add into job schedule** to run the intent discovery.
1. In **Test results**, select the simulation to view the details. The simulation details are displayed. Simulation uses the last 1,000 records to generate intent and intent groups. The simulation helps administrators evaluate the intents and intent groups.
1. Select the simulation, and then select **View job details** option.
1. After you validate the intents and intent groups that reflect your business needs, select **Set up intent discovery** to run the intent discovery.
   > [!NOTE]
   > You can view the simulation for successful runs only. The simulation job shows a failure message if the simulation is unsuccessful.

### Discovery updates to existing intents

Your intent library stays current. Existing intents are updated so that the titles, descriptions, attributes, and common customer utterances continue to reflect your products and triage processes as they change. An intent is updated when intent guidance changes, when a newly-mined case surfaces a crucial attribute, or when the model determines that existing details are out of date.

Updates to proposed intents appear as usual on the job details page, while updates to intents already in the library appear on a separate tab with **Change Reason** and **Change Summary** columns. Promoting an updated intent patches the existing intent with the new title, description, and attributes.

### Promote intents to intent library

1. On **Customer Intent Agent**, select **Manage** under **Manage intents**.
1. On the **Manage intent discovery setup** page, select the discovery job or jobs you want to review and select **View job details**.
1. In the job details page, you see how many new intents and intent groups were generated in this discovery job.
1. Select the intents or intent groups you want to promote to your intent library and then select **Move to intent library**.
1. After you review the job, select **Mark jobs** as reviewed. This action helps you and other administrators distinguish the jobs that are reviewed and pending review.

## Build and refine your intent library

You can build an intent library by using intent discovery, creating intents manually, or combining both approaches. Intent discovery is optional. It analyzes historical interactions to identify intents and intent groups, and the generated content can include intent descriptions and attributes. You don't need to create a line of business to start building your library.

If you use intent discovery, review the results, promote the intents and intent groups you want to keep, and refine the promoted items. Create additional intents and groups for requests that discovery doesn't cover. If you don't use discovery, start by creating intents and intent groups manually.

Before creating an intent, review all approved intents in the library, including those promoted from discovery. Avoid creating a semantically duplicate intent just because its name or wording differs. Update an existing intent when appropriate.

Use descriptions to define the requests that an intent covers. Use instructions to explain how Customer Intent Agent should handle those requests.

## Manage intents

1. On the **Customer Intent Agent** page, select **Manage** for **Manage intents**.

1. Select **New**, and enter intent details as follows:
   - **Name**: Enter a name for the intent. The name should be intuitive and meet your business requirement.
   - **Intent group**: Select the intent group that you want to associate with the intent.
   - **Line of business**: Select the line of business that you want to associate with the intent.
   - **Review status**: Select **Pending**, **Approved**, or **Discarded** in the list to indicate the default status that you'd like to set for the intent.
   - **Autonomous support**: Select **Self-service support** if you want the AI agent to autonomously handle this intent for immediate deflection.
1. Save the information.
1. On the **Attributes** tab, add the attributes that you want to associate with the intent. The attributes are used to provide additional information about the intent. You can add multiple attributes for an intent.
1. On the **Knowledge articles** tab, select **Add** to associate the knowledge articles with the intent. The knowledge articles are used to provide additional information about the intent. You can add multiple knowledge articles for an intent.

  :::image type="content" source="../media/create-intent.png" alt-text="Screenshot of create intent page with all details and attributes." lightbox="../media/create-intent.png":::

You can manage the intents to be used in AI agent in bulk. On the **Manage intents** page, select the approved intents, and on the command menu, select **Use in AI agent**. The intents are used in the AI agent.

### Write intent descriptions

An intent description defines the customer request, while instructions explain how to handle it. Include the following information in a description:

- **Customer goal**: State what the customer wants to do.
- **Match signals**: Identify symptoms or details that support the intent.
- **Exclusions**: Identify similar requests that don't belong.
- **Conditions**: State what must be true for the request to fit. Put the steps for checking those conditions in the instructions.

Use a pattern such as: "Use this intent when [customer goal] and [matching signal]. Don't use it when the main request is [another request type]."

For example:

> Use this intent when a Contoso Coffee customer reports unexpected coffee taste and provides details suggesting that beans, grind size, water, or filtration are the likely cause. Don't use it when the main request concerns cleaning, brew settings, or an equipment fault.

Match the customer's main request rather than a single word. For example, mentioning cleaning doesn't exclude this intent when the customer's primary concern is a taste change associated with new beans.

## Manage intent groups

You can logically organize the intents into intent groups. The intent group represents the business expertise needed to solve the intents belonging to the group. The intent groups that the AI model identifies are displayed on the **All intent groups** page. You can manage the intent groups by reviewing, approving, or updating the intents in them.

1. On the **Customer Intent Agent** page, select **Manage** for **Manage intent groups**. The **All intent groups** page lists the intent groups that the AI model discovered. If you create a custom intent group, the intent source shows as **Admin edited**. The **Intents** column displays the number of intents in each intent group.

   :::image type="content" source="../media/list-of-intent-groups.png" alt-text="Screenshot of intent groups list." lightbox="../media/list-of-intent-groups.png":::

1. Select an intent group to manage its intents. The `<intent_group_name>` page displays the details, such as review status and the list of intents in the group.

   :::image type="content" source="../media/manage-intents.png" alt-text="Screenshot of manage intents in intent group." lightbox="../media/manage-intents.png":::

1. Select **Manage intents** to add new intents or remove existing ones.
1. On the **Manage intents** dialog, you can make the following updates:
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

### Define intent groups

Use a group description to define a broad category, and use intent descriptions to define the specific requests within it. State what the group covers and excludes. Keep shared checks and handling steps in the group instructions.

For example:

> This group covers unexpected coffee taste related to beans, water, grind size, cleaning, or brew settings. It excludes requests about a machine that won't turn on or dispense coffee, leaks, or makes unusual noises.

Describe each request type in plain language instead of using references such as "use the parent group". Review related descriptions together to identify gaps and overlap.

## Manage instructions (optional)

Set up instructions to streamline Customer Intent Agent behavior. You can add instructions for the line of business, intent groups, and intents.

Put each instruction at the level where it applies:

| Level | Use for | Keep at another level |
|---------|---------|---------|
| Organization or line of business | Role, shared conversation flow, language, channel guidance, terminology, boundaries, and handoff policy. | Steps for one group or intent. |
| Intent group | Shared checks, clarification, and handling rules for related intents. | Steps for one intent. |
| Intent | Checks, ordered steps, branches, configured actions, and handoff conditions for one request. | Rules covered at a broader level. |

Instructions configured for a selected line of business are applicable across the line of business. If you don't select a line of business, configure the organization's default instructions. Keep rules consistent across levels. A more specific instruction might not override a conflicting rule.

At runtime, if the wrong intent is selected, review descriptions and any eligibility or exclusion conditions in the instructions. If the correct intent is selected but handling is wrong, review the instructions and configured actions.

To add instructions, complete the following steps:

1. On the **Customer Intent Agent** page, select **Manage** for **Manage instructions (optional)**.

1. On the **Manage instructions** page, select a line of business in **Select line of business**. If you don't specify a line of business, Customer Intent Agent follows the default instructions for the organization.
1. In the **Line of business instructions (optional)** section, select **Add**.
1. On the **Add instructions** dialog, add the instructions for the line of business. You can enter up to 4,000 characters. Expand **View example instructions** to view sample instructions.
1. Select **Save**. The instructions are available immediately for use by Customer Intent Agent.
1. In the **Instructions for intent groups and intents** section, select the following options to create instructions for intent groups and intents.
   - **Manage Intent groups**: In the list of intent groups page, select an intent group.
       1. On the `<intent_group_name>` page, in **Intent group instructions (optional)** , select **Add**. The **Add instructions** dialog appears.
       1. Add instructions for the intent group. You can enter up to 4,000 characters.
       1. Save and close.
   - **Manage intents**: In the list of intents page, select an intent.
       1. On the `<intent_name>` page, in **Intent instructions (optional)** , select **Add**. The **Add instructions** dialog appears.
       1. Add instructions for the intent. You can enter up to 4,000 characters.
       1. Save and close.

You can edit or delete instructions for a line of business, intent groups, or intents using the **Edit** and **Delete** options in the instructions section of the corresponding pages.

### Use channel-specific, self-service, or assisted-service instructions

Tag instructions with specific syntax to apply them in certain channels, or for self-service (unsupervised) or assisted-service (supervised) scenarios. Tags work for organizational, intent group, and intent instructions.

|Tag |Definition |
|---------|---------|
|{{text}} instruction 1 {{/text}}     |    Instruction applied to text channel for both self-service and assisted service.     |
|{{voice}} instruction 2 {{/voice}}    |  Instruction applied to voice channel for both self-service and assisted service.       |
|{{email}} instruction 3 {{/email}}     |  Instruction applied to email channel for both self-service and assisted service.       |
|{{supervised}} instruction 4 {{/supervised}}     |   Instruction applied to all channels for assisted service only.     |
|{{unsupervised}} instruction 5 {{/unsupervised}}    |     Instruction applied to all channels for self-service only.    |

Check every configured channel and service mode. Questions, response format, and handoff behavior can differ between text and voice, and between self-service and assisted service. Test each scenario, confirm that specialized instructions agree with shared rules, and make sure that the instructions always define a next step.

## How to write clear instructions

These guidelines define how you can write intent-level, group-level, and organizational-level instructions to ensure clarity, consistency, and alignment with the agent’s goals.

### Write shared instructions

|Guidelines |Why it matters   |Example   |
|---------|---------|---------|
|Start with a concise statement that defines the objective of Customer Intent Agent.   | Establishes the brand voice and scope, and helps Customer Intent Agent select the right tone.         |   "You're a representative from Contoso Coffee, assisting customers with orders and account questions."       |
|Tweak overall tone to reflect brand personality. |    Creates a consistent voice across all customer interactions.     |   "Keep language warm, empathetic, and professional. Show understanding without over-apologizing."|
|Define general behavioral boundaries and escalation policies.    |  Ensures compliance and predictable outcomes.       |   "If resolving the issue requires judgment, verification, or policy exceptions, summarize context and hand off to a service representative."     |
|Include a glossary of common terms and abbreviations.    | Reduces ambiguity across regions or departments. |   "'SHS' = Successful Handling Score"; "'PSS' = Product Support Specialist;"      |

Use organization or line-of-business instructions to define shared conversation flow, language, tone, terminology, and handoff policy. State how to handle unsupported languages, off-topic requests, and missing information.

Define safety boundaries that are applicable across the organization or selected line of business, including when the Customer Intent Agent must stop troubleshooting and hand off. Keep these shared rules at this level instead of repeating them in every group or intent.

Distinguish between situations that require immediate handoff and those where the Customer Intent Agent should attempt clarification first. If the customer's response still doesn't establish a supported next step, hand off instead of repeating questions or guessing. Don't configure handoff to a representative for requests the Customer Intent Agent can resolve.

For example, define a shared flow as follows:

1. Use the opening behavior defined for the channel and service mode.
1. Identify the customer's main request from the information provided.
1. Follow the relevant instructions and use configured business sources.
1. Ask only for details needed to continue.
1. Hand off to a service representative if no supported next step exists or handling would be unsafe.

Keep request-specific troubleshooting steps in intent instructions.

### Write intent group instructions

|Guidelines  |Why it matters |Example   |
|---------|---------|---------|
|Define complex disambiguation logic across related intents.    |   Helps Customer Intent Agent handle overlapping or multi-intent requests effectively.      | "If a user mentions both 'cancel order' and 'return product,' prioritize return flow first, then confirm if cancellation is still needed."      |

Add rules that apply to every intent in the group. State what Customer Intent Agent must check and what to do for each possible result. Use this level for requirements specific to the group only:

- **Immediate handoff**: If the entire group requires a representative, hand off without asking troubleshooting questions.
- **Shared condition**: State what to check first and what to do if the condition isn't met.
- **Clarification**: Ask for details that distinguish related requests. Define the handoff path if the answer doesn't establish a supported next step.
- **Stop condition**: Define group-specific conditions that require handling to stop. Keep them consistent with the shared safety and handoff policy.

For example:

> Apply the shared safety and handoff policy before troubleshooting. For taste issues, determine whether the customer's description points to beans, grind size, water, cleaning, or brew settings. Follow the matching configured intent when the available details support it. If clarification is needed, ask for the missing details only. If the response still doesn't establish a supported path, hand off rather than guess.

Keep resolution steps for a single request in its intent instructions. Keep organization-wide or line-of-business-wide rules in shared instructions.

### Write intent instructions

|Guidelines  |Why it matters  |Example  |
|---------|---------|---------|
|Start with steps that outline the flow and then add details.  |    Creates a logical, easy-to-follow sequence.   | 1. Clarify the problem. <br> 2. Pick the likely cause. <br> 3. Try one fix at a time. |
|List required checks or prerequisites.    |  Ensures that required information isn't missed before Customer Intent Agent takes action or performs lookups.   | If the user reports an issue, first confirm the product model and purchase date.|
|Explain what's out of scope or not allowed.| Prevents unnecessary work or compliance issues.   | Don't ask for social security numbers or payment card details.|
|Use if-then logic for decision points. | Reduces ambiguity without technical syntax.| If the product is under warranty, offer a replacement. Otherwise, provide repair options.|
|Specify when to escalate issues or hand them off to service representatives. |    Ensures a smooth transition when automated resolution isn't possible. |  Hand-off to a service representative if the customer requests a refund over $100 or expresses dissatisfaction.|
|Break multi-part instructions into smaller steps.  |   Avoids missed details and simplifies handoffs.|  Instead of Verify account and reset password, split into: 1. Verify account. 2. Reset password.       |
|Don't use unnecessary technical or system jargon. |  Keeps instructions readable and usable without requiring technical expertise.|  Use Look up the customer’s order in the system, instead of Execute GET request on Order API. |

Use ordered steps with required checks, a next step for every result, and a point at which handling must stop. Reuse information that the customer already provided. Explain what to do when information is missing, unclear, or inconsistent with the selected intent.

If clarification is allowed, specify what information is needed and what to do if the response still doesn't establish a supported next step. Include a fallback such as: "If these instructions don't provide a clear next step, hand off to a service representative."

For example:

1. Confirm that the customer reports unexpected coffee taste after a possible change to beans, grind size, water, or filtration.
1. Ask only for missing details needed to identify the likely cause.
1. For beans or grind size, use configured guidance on freshness, storage, and grind suitability.
1. For water or filtration, use configured guidance on water quality, source changes, and filter replacement.
1. If the main request concerns cleaning, brew settings, or an equipment fault, follow the relevant configured intent instead.
1. If the available information or the customer's clarification doesn't establish a supported next step, hand off. Follow the shared safety and handoff policy throughout.

Adapt examples to your business. Replace references to "configured guidance" with the actual handling steps or approved information Customer Intent Agent should use. Use available knowledge and configured actions only. Writing an instruction doesn't create an action.

### Keep instructions clear

Use the following practices to supplement the guidelines:

- **Give an alternative**: Explain what to do when a request doesn't fit.
- **Use emphasis sparingly**: Don't mark every step as mandatory.
- **Use consistent terms**: Use the same names for products, concepts, and handoffs.
- **Describe business behavior**: State what to ask and do, not how internal components work.
- **Be specific**: Name the alternative request type instead of referring to a sibling intent.
- **Use fictional examples**: Replace real customer details with placeholders.
- **Remove duplication**: Put each rule at the narrowest level where it applies. Keep shared rules in organization, line-of-business, or group instructions, and request-specific rules in intent instructions.

Before adding more wording, check for conflicting rules. A strict instruction still requires complete steps, decision points, and a fallback.

## Test changes to descriptions and instructions

Test intent selection and handling separately. The selection of the correct intent is only one part of a successful result.

Make and compare configuration changes in a test environment before applying them to production. Use representative test cases, and verify that the required knowledge sources, connections, permissions, and actions are configured for testing. Use test data and actions that don't unintentionally affect production records or customers.

### Record a baseline

Before you edit the test environment, record the current descriptions, instructions, relevant action configuration, and baseline test results. For each test case, record the expected group, intent, and handling outcome.

Change the smallest relevant part. Make one change at a time so you can isolate its effect.

### Choose test cases

Include the following types of test cases.

| Case type | What to include | What to verify |
|---------|---------|---------|
| Positive | Use different ways to ask for the target request. | Verify that the expected intent matches and the handling is correct. |
| Negative | Use similar requests that belong elsewhere. | Verify that the target intent doesn't match. |
| Ambiguous | Use requests with missing or unclear details. | Verify that the configured clarification or handoff occurs. |
| Multiple requests | Include several needs or conflicting signals in one message. | Verify that the configured priority and handling are followed. |
| Channel and service mode | Cover each channel and service mode in use. | Verify the format, questions, and handoff. |
| Boundary and failure conditions | Include unmet conditions, missing data, failed actions, and unsafe or unsupported requests. | Verify that the configured alternative or handoff occurs. |

### Compare results

Use the same cases to compare behavior before and after the change:

1. Run the cases against the baseline and changed configurations.
1. Include the changed intent and related intents whose descriptions overlap.
1. For shared-instruction changes, include representative intents across the affected group or line of business.
1. Repeat representative cases, especially unclear or overlapping requests. One successful run doesn't demonstrate consistent behavior.
1. Check intent selection, questions, use of customer details, actions, and handoffs.
1. Investigate new incorrect matches or handling failures.
1. Retain the cases and results for future changes.
1. Add new customer wording over time.

Use the following measures to evaluate results.

| Measure | What to check |
|---------|---------|
| Correct matches | Check the share of positive cases assigned to the expected intent. |
| Incorrect matches | Check the share of negative cases assigned to the target intent. |
| Clarification and handoff | Check whether unclear cases follow the configured policy. A handoff isn't always a success or failure. |
| Handling after a correct match | Check whether Customer Intent Agent follows the expected checks, steps, actions, and stop conditions. |

Update expected results only when behavior changes intentionally, and record the reason. Don't change expectations to hide a regression.

> [!IMPORTANT]
> Saved instructions take effect immediately. Complete the comparison in the test environment before applying validated changes to production. After applying them, perform limited verification to confirm that the production configuration works as expected.

## Manage connectors for AI agents (optional)

Connectors let systems work together, transfer data, and allow AI agents to automatically handle tasks for issue resolution.

1. On the **Customer Intent Agent** page, select **Manage** for **Manage connectors for AI agents (optional)**.

1. On the **Manage custom connectors** page, select **Add connector**. Learn how to add a connector in [Create a custom connector](/connectors/custom-connectors/define-blank).
1. On the **Select a connector** dialog, search and select a connector. You can add up to 30 connectors.
1. Select **Next**.
1. On the **Set up the connector** dialog, select a connection from the **Connection** dropdown. You can also create a new connection in Power Platform. Learn more in [Add connection references to a solution](/power-apps/maker/data-platform/create-connection-reference#add-connection-references-to-a-solution).
    > [!NOTE]
    > Make sure that the connection you select is shared with the **Dynamics 365 Analytics** service principal. 
    
    Learn more in [Share a custom connector in your organization](/connectors/custom-connectors/share).
1. Specify if the type for the connector is **General** or **For specific intents**.
1. If you select **For specific intents**, you must first make the custom connector available for specific intents. You can then map its actions as tools to intents, as described in the following section.
1. Select **Save**.

### Map a tool to an intent

Tools help systems connect and enable data flow or actions. Customer Intent Agent currently supports custom connectors as tools. When you specify a connector for specific intents, you can add its actions as tools that the Customer Intent Agent uses to resolve those intents.

1. Select **Manage** for **Manage intents** on the **Customer Intent Agent** page.
1. Select the specific intent, and on the intent page, in the **Resource (Optional)** section, select the **Tools** option, and then select **Add**.
1. On the **Add a resource** page, search and select a connector action to map to the intent. The application displays connectors created for use with specific intents only.
1. Select **Save and close**.

> [!NOTE]
> After you add or remove a connector, changes can take up to 15 minutes to appear in the Customer Intent Agent.

You can edit or delete a connector after you select the required connector on the **Manage custom connectors** page. You can also view which intents are using the connector when you edit the connector.

### Check connector actions

Before changing a description or instructions to address an action failure, check that the required action is available, connected, authorized, and returns the expected result. If you recently added or removed a connector, allow up to 15 minutes for the change to appear.

Timeouts, authentication failures, and missing data might be because of configuration issues, and not proof that the selected intent was incorrect. Define what the Customer Intent Agent must do when an action fails. If no supported option remains, follow the handoff policy.

### Related information

[Enable intent for support representatives](enable-intent-for-service-reps.md)  
[Use intent agents](../use/use-intent-suggestions.md)  
[Create rollout plans](create-rollout-plans.md)  
