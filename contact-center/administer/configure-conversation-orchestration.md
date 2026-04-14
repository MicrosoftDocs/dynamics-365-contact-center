---
title: Configure conversation orchestration in Dynamics 365 Contact Center (preview)
description: Learn how to manage intelligent conversation routing with conversation orchestrator. Set up dynamic prioritization and overflow actions to enhance customer service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 04/07/2026
ms.topic: how-to
ms.collection: bap-ai-copilot
---

# Configure conversation orchestration (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Conversation orchestration keeps every conversation actively managed throughout the conversation lifecycle from initiation through resolution. Instead of applying fixed rules at different stages of conversation journey, conversation orchestration monitors each conversation as the conditions evolve&mdash;increase in wait time, filling up of the queues, service representatives going offline&mdash; and responds automatically with the right action. Administrators define the conversation orchestration logic using natural-language playbooks, and conversation orchestration handles the .

Conversation orchestration enables you to create intelligent, AI-driven routing and prioritization policies using natural language. You can define how to prioritize conversations, when to run overflow actions, and how work items are routed&mdash;all through an intuitive playbook-based configuration experience.

> [!IMPORTANT]
> In preview, conversation orchestration is available for voice and live chat channels only.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/production-ready-preview-dynamics365.md)]

## Prerequisites

- Specific licensing requirements apply to configure and use conversation orchestration in Dynamics 365 Contact Center. Learn more in [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/?LinkId=866544).
- System administrator or Omnichannel administrator role.
- Unified routing enabled for your environment.
- At least one queue configured for voice or messaging channels.
- A voice or messaging channel is configured.

## Understand playbooks

A playbook is a set of rules that define how to handle conversations for specific scenarios. Each playbook consists of:

- **Queues**: The queues for which the playbook applies.
- **Trigger event**: The event that initiates the playbook, such as a conversation waiting in queue or conversation transferred.
- **Conditions**: Business rules based on context variables, such as customer tier or country/region.
- **Actions**: The outcomes when conditions are met, such as increasing priority or transferring to an overflow queue.

A playbook can have one of the following statuses.

| Status | Description |
|--------|-------------|
| **Draft** | The playbook is saved but not active. You can make changes freely. |
| **Active** | The playbook is published and actively routing conversations. |

## Access conversation orchestration playbooks

In Copilot Service admin center, go to **Customer support** > **Conversation Orchestration (Preview)**. The conversation orchestration home page displays available playbook templates organized by scenario.

## Create and manage playbooks

### Create a playbook

1. On the **Conversation Orchestration** page, select one of the following prompt templates that matches your scenario:
   - **Escalate priority based on wait time**: For wait time-based prioritization.
   - **Escalate priority based on transfer to queue**: For transfer-based prioritization.
   - **Configure overflow based on agent availability in the queue**: For agent availability overflow.

1. In the playbook editor, accept the default name or enter a name in **Playbook name**.
1. Select **Queues** > **Edit** to open the queues pane.
   1. **Channel**: Select **Voice** or **Messaging**.
   1. In **Apply to**, select how to apply the playbook.
      - **All queues**: Applies to all queues for the selected channel.
      - **List of queues**: Select specific queues from the list.
      - **All queues except**: Applies to all queues except the ones you exclude.
   1. Select **Save**.

1. Optionally, add context variables to create conditions based on customer or conversation attributes:
   1. In the **Add variables** section, select **Add customer attribute**.
   1. Choose from available context variables such as CustomerTier, Is VIP Customer, Preferred Language, Customer Region, or Account Type.
   1. Provide a description for how the variable appears in the playbook.
   1. Select the values you want to use in your conditions.

   > [!NOTE]
   > In preview, you can add up to two customer variables only per playbook.

1. Configure conditions and actions based on your selected template:

   **For dynamic prioritization playbooks:**
   - For **Update priority based on transfer to queue** playbook, the trigger event is preset to **Conversation is transferred**.
   - For **Update priority based on conversation wait time** playbook, the trigger event is preset to **Conversation is waiting in queue**.
   - Set the time interval for priority increases (minimum 30 seconds).
   - For each condition branch, select the context variable values that trigger this condition and set the priority score to increase (0–100,000).
   - Configure the default priority score for conversations that don't match any condition.


   **For overflow playbooks:**
   - The trigger condition is preset to **Conversation is waiting in queue**.
   - For each condition branch, select the context variable values that trigger this condition and choose the overflow action (transfer to queue, direct callback, voicemail, or end conversation).
   - Configure the default action for conversations that don't match any condition.

   > [!TIP]
   > In the preview release, you can add up to 12 condition branches per playbook.

1. Select **Save**. The playbook is saved as a draft.

1. Review your configuration for any validation warnings, and then select **Publish** to activate the playbook.

### Edit a playbook

1. Go to the **All playbooks** tab in **Conversation Orchestration**.
1. Find the playbook you want to edit.
1. Select the actions menu (**...**), and then select **Edit**.
1. Make your changes.
1. Do one of the following:
   - For draft playbooks: Select **Save** to save your changes, or select **Publish** when ready to activate.
   - For active playbooks: Select **Save & publish** to save and immediately publish your changes. The **Save** button is disabled for active playbooks to prevent unintended changes to live routing. If you cancel, the playbook reverts to the last published version.

### Delete a playbook

1. Go to the **Playbook** tab.
1. Select the actions menu (**...**) for the playbook and then select **Delete**.
1. Confirm the deletion.

> [!IMPOrTANT]
> If you delete an active playbook, it stops routing conversations immediately.

## Scenario: Dynamic prioritization - Wait time escalation

This scenario automatically increases the priority of conversations based on how long customers wait in the queue.

**Trigger event**: Conversation is waiting in queue

**How it works:**

1. When a conversation enters the queue, the playbook evaluates the configured conditions.
1. Based on matching context variable values, the system increases the priority score at the specified time interval.
1. The system offers higher priority conversations to representatives first than the lower priority ones.

**Example:**

| Customer segment | Priority increase | Time interval |
|------------------|-------------------|---------------|
| VIP customers | 20 | Every 30 seconds |
| Gold tier customers | 15 | Every 30 seconds |
| All other customers | 5 | Every 30 seconds |

## Scenario: Dynamic prioritization - Queue transfer escalation

This scenario increases conversation priority when a conversation is transferred to a specific queue.

**Trigger event**: Conversation is transferred to queue

**How it works:**

1. When you transfer a conversation to a queue where this playbook is active, the priority increases immediately.
1. The priority increase is a one-time adjustment based on the configured conditions.
1. Transferred conversations receive appropriate attention based on your business rules.

**Example:**

| Customer segment | Priority increase |
|------------------|-------------------|
| VIP customers | 50 |
| Escalation transfers | 30 |
| All other transfers | 10 |

## Scenario: Representative availability based overflow

This scenario triggers overflow actions when no representatives are available to handle conversations.

**Trigger event**: Conversation is waiting in queue and no representative is available.

**How it works:**

1. When a conversation enters the queue, the system checks for availability of representatives.
1. If no representatives are available based on presence, capacity, and skills, the overflow action triggers immediately.
1. You can configure different actions based on customer attributes.

**Available overflow actions:**

| Action | Description |
|--------|-------------|
| **Transfer to queue** | Route the conversation to a different queue |
| **Direct callback** | Offer the customer a callback option |
| **Voicemail** | Route to voicemail for later follow-up |
| **End conversation** | End the conversation with a message |

**Example:**

| Customer segment | Overflow action |
|------------------|-----------------|
| VIP customers | Transfer to VIP Overflow Queue |
| After-hours calls | Route to voicemail |
| All other customers | Offer direct callback |

## Validations

Conversation orchestration validates your playbook configuration and displays warnings for potential issues.

| Validation | Description |
|------------|-------------|
| **Required fields** | Mandatory fields are empty (priority score, time interval, action) |
| **Range validation** | Values are outside allowed ranges (priority: 0–10,000; time: minimum 30 seconds) |
| **Duplicate conditions** | Two conditions have identical variable-value combinations |
| **Conflicting conditions** | Overlapping conditions might cause unexpected behavior |
| **Cross-playbook conflicts** | Multiple active playbooks exist for the same queue and scenario |

The editor displays warnings with amber styling. You can save a playbook with warnings as a draft, but you must resolve all warnings before publishing.

### Multiple playbooks for the same queue

When you configure multiple playbooks that apply to the same queue, Conversation Orchestration handles them differently based on whether they target the same or different scenarios.

**Same queue, same scenario (Conflict)**

You can't have multiple active playbooks for the same scenario and the same queue. This configuration creates a conflict that prevents publishing.

For example, if you have an active "Escalate priority based on wait time" playbook for Queue A, you can't publish another wait time-based priority playbook for Queue A - even if the time interval or priority values are different. Instead, edit the existing playbook to update its configuration.

When you attempt to publish a playbook that conflicts with an existing active playbook, the system displays the following error:

_To be written_

To resolve this conflict, either:
- Modify the queue selection in your new playbook to exclude the conflicting queues
- Edit or deactivate the existing active playbook before publishing your new one

**Same queue, different scenarios (Allowed)**

You can configure different scenarios for the same queue. For example, a single queue can have both a "Dynamic Prioritization - Wait Time" playbook and an "Agent Availability Based Overflow" playbook active simultaneously.

When multiple playbooks with different scenarios are active for the same queue, they execute in a predefined sequence that follows the unified routing order:

| Run order | Scenario |
|-----------------|----------|
| 1 | Agent availability-based overflow |
| 2 | Dynamic prioritization (Wait Time or Queue Transfer) |

This run order is consistent across all conversations and can't be changed. The system automatically determines the playbook to evaluate first based on the scenario type, ensuring predictable and deterministic behavior for all conversations in the queue.

### Cross-playbook conflict detection

> [!IMPORTANT]
> Cross-playbook validation occurs only when you publish a playbook, not when you save it as a draft. The system checks your playbook against other published active playbooks only.

This means:
- You can save a playbook as a draft even if it conflicts with an existing active playbook.
- The system detects and reports conflicts only when you attempt to publish a playbook.
- If a conflict exists, you must resolve it by modifying either the new playbook or the existing active playbook before publishing.

## Things to consider

- Conversations have a default priority score of 0. Use classification rules to set an initial priority score.
- Customize the prompt to assign different priority scores based on context variables.
- Priority scores range from 0 to 100,000. The minimum wait time is 30 seconds.

> [!IMPORTANT]
> Dynamic prioritization playbooks aren't applicable to queues configured with custom prioritization rules. To use dynamic prioritization, you must first remove the custom prioritization configuration from the queue.

## Troubleshooting

| Issue | Resolution |
|-------|------------|
| Playbook not routing conversations | Verify the playbook status is Active, check that the correct queues are selected, and ensure the channel matches your conversation type. |
| Priority not increasing as expected | Confirm the time interval setting, verify context variable values match your conditions, and check that the conversation is in a queue where the playbook is active. Also verify that the queue doesn't have custom prioritization rules configured. |
| Overflow not triggering | Verify agent availability settings (presence, capacity, skills), check that the "no agents available" condition is being met, and ensure the playbook is active for the correct queue. |
| Unable to publish playbook due to conflict | Another Active playbook already exists for the same scenario and queue. Edit the existing playbook or modify the queue selection in your new playbook to avoid overlap. |
| Dynamic prioritization not applying to a queue | The queue might have custom prioritization rules configured. Remove the custom prioritization configuration from the queue settings to enable dynamic prioritization. |

### Related information

[Set up unified routing](/dynamics365/customer-service/administer/set-up-routing)  
[Create and manage queues](/dynamics365/customer-service/administer/queues-omnichannel)  
[Configure context variables](/dynamics365/customer-service/administer/context-variables)  
