---
title: Configure conversation orchestration in Dynamics 365 Contact Center (preview)
description: Learn how to manage intelligent conversation routing with conversation orchestration. Set up dynamic prioritization and overflow actions to enhance customer service.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 04/27/2026
ms.topic: how-to
ms.collection: bap-ai-copilot
---

# Configure conversation orchestration using AI-powered playbooks (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Conversation orchestration keeps every conversation actively managed throughout the conversation lifecycle from initiation through resolution. Instead of applying fixed rules at different stages of conversation journey, conversation orchestration monitors each conversation as the conditions evolve&mdash;increase in wait time, filling up of the queues, service representatives going offline&mdash; and responds automatically with the right action. Administrators define the conversation orchestration logic using natural-language playbooks, and conversation orchestration handles the execution.

In the preview release, conversation orchestration is available for voice and live chat channels only.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- Specific licensing requirements apply to configure and use conversation orchestration in Dynamics 365 Contact Center. Learn more in [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/?LinkId=866544).
- System administrator or Omnichannel administrator role.
- Unified routing enabled for your environment.
- At least one queue and workstream is configured for voice or messaging channels.
- A voice or messaging channel is configured.

## Understand playbooks

Configure playbooks per scenario through guided templates that keep instructions focused and reliable. A playbook consists of a trigger event and a set of conditions and actions to run when the trigger event occurs.

- **Queues**: The queues for which the playbook applies.
- **Trigger event**: The event that initiates the playbook, such as a conversation waiting in queue or conversation transferred.
- **Channel**: The channel that you select in the **Queues** dialog. The context variables that appear are based on the selected channel. If you update the channel in a draft playbook, then you have to update the applicable context variables and the corresponding prompt.
- **Conditions**: Business rules based on context variables, such as customer tier or country/region. You can define up to 10 conditions to configure the granularity. These conditions can have up to two context variables.
- **Actions**: The outcomes when conditions are met, such as increasing priority or transferring to an overflow queue.

A playbook can have one of the following statuses.

| Status | Description |
|--------|-------------|
| **Draft** | The playbook is saved but not active. You can make changes freely. |
| **Active** | The playbook is published and actively orchestrates conversations. |

## Access conversation orchestration playbooks

In Copilot Service admin center, go to **Customer support** > **Conversation Orchestration (Preview)**. The **Conversation orchestration (Preview)** > **New** page displays available playbook templates organized by scenario.

## Create and manage playbooks

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team’s performance and improve customer satisfaction. This feature is not intended for use in making&mdash;and should not be used to make&mdash;decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws relating to accessing individual employee analytics and monitoring, recording, and storing communications with end users. This also includes adequately notifying end users that their communications with representatives may be monitored, recorded, or stored and, as required by applicable laws, obtaining consent from end users before using the feature with them. Customers are also encouraged to have a mechanism in place to inform their representatives that their communications with end users may be monitored, recorded, or stored.

### Create a playbook

By default, the conversation orchestration page displays three popular prompts. Use **Prompt gallery** to view prompts for the different scenarios.

1. On the **Conversation Orchestration** page, select **Prompt gallery**. The pop-up window displays prompt templates for all scenarios by default.
1. In the drop-down field, select one of the following categories and then a prompt template that matches your scenario:
   - Dynamic prioritization:
      - **Escalate priority based on wait time**: For wait time-based dynamic or real-time prioritization.
      - **Escalate priority based on transfer to queue**: For transfer-based prioritization.
   - Overflow handling:
      - **Configure overflow based on support representative availability in the queue**: For representative availability overflow.

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

1. Configure conditions and actions based on your selected template. See **Tips for this playbook** on the edit playbook page to optimally configure the conditions.

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

> [!IMPORTANT]
> If you delete an active playbook, conversation orchestration stops for the corresponding queue immediately.

## Validations

Conversation orchestration validates your playbook configuration and displays warnings for potential issues.

| Validation | Description |
|------------|-------------|
| **Required fields** | Mandatory fields are empty (priority score, time interval, action) |
| **Range validation** | Values are outside allowed ranges (priority: 0–10,000; time: minimum 30 seconds) |
| **Duplicate conditions** | Two conditions have identical variable-value combinations |
| **Conflicting conditions** | Overlapping conditions might cause unexpected behavior |
| **Cross-playbook conflicts** | Multiple active playbooks exist for the same queue and scenario |

### Multiple playbooks for the same queue

When you configure multiple playbooks that apply to the same queue, Conversation Orchestration handles them differently based on whether they target the same or different scenarios.

**Same queue, same scenario (Conflict)**

You can't have multiple active playbooks for the same scenario and the same queue. This configuration creates a conflict that prevents publishing.

For example, if you have an active "Escalate priority based on wait time" playbook for Queue A, you can't publish another wait time-based priority playbook for Queue A - even if the time interval or priority values are different. Instead, edit the existing playbook to update its configuration.

When you attempt to publish a playbook that conflicts with an existing active playbook, the system displays an error message similar to the following one:

"Failed to publish policy: A playbook for "Escalate priority based on wait time" is already published for `queue_name`. You cannot publish a duplicate policy for the same queue(s). Please modify the existing published policy."

To resolve this conflict, do one of the following steps:

- Modify the queue selection in your new playbook to exclude the conflicting queues
- Edit or deactivate the existing active playbook before publishing your new one

You can save a playbook as a draft even if it conflicts with an existing active playbook.

> [!IMPORTANT]
> The system performs the **cross-playbook validation** only when you publish a playbook, not when you save it as a draft. The system checks your playbook against other published active playbooks only.

**Same queue, different scenarios (Allowed)**

You can configure different scenarios for the same queue. For example, a single queue can have both a "Dynamic Prioritization - Wait Time" playbook and an "Agent Availability Based Overflow" playbook active simultaneously.

When multiple playbooks with different scenarios are active for the same queue, they run based on the triggering event.

**Example: How multiple playbooks for the same queue across different scenarios work**

Consider a queue configured with two playbooks, each designed to handle a distinct scenario:

- **Dynamic prioritization playbook**
  - **Trigger**: Wait time
  - **Condition**: Customer tier = Gold  and wait time ≥ 30 seconds
  - **Action**: Increase priority by 1

- **Agent availability overflow playbook**
  - **Trigger**: Immediate evaluation on queue entry
  - **Condition**: Customer tier = Gold **and** no agents are available
  - **Action**: Run overflow (for example, route to voicemail, transfer to another queue, or redirect to another number)

Although both playbooks target Gold-tier customers, they differ in their triggering condition&mdash;one is based on elapsed wait time, and the other on real-time agent availability.

**How playbooks are run**

**Scenario 1: Agents are available initially**

1. A conversation enters the queue. Agents are available > overflow condition isn't met, so no overflow action runs.
1. The conversation remains unassigned for 30 seconds.
1. The dynamic prioritization condition is now met, triggering a priority increase as defined.

**Result**: The system runs the dynamic prioritization playbook only.

**Scenario 2: No agents available at entry**

1. A conversation enters the queue. No agents are available > **overflow condition is met immediately**. The overflow action is triggered (for example, redirect to voicemail or another queue).
1. If the conversation:
   - **Leaves the queue or is closed** > no further actions occur.
   - **Remains in the queue and is still waiting**: On reaching 30 seconds, the action for **dynamic prioritization playbook** runs and increases the priority.
   - Overflow action runs first based on availability.
   - Dynamic prioritization runs only if the conversation remains in the queue long enough.

## Things to consider

| Issue | Resolution |
|-------|------------|
| Playbook isn't routing conversations | Verify the playbook status is Active, check that the correct queues are selected, and ensure the channel matches your conversation type. |
| Priority isn't increased as expected | Confirm the time interval setting, verify context variable values match your conditions, and check that the conversation is in a queue where the playbook is active. Also verify that the queue doesn't have custom prioritization rules configured. |
| Overflow isn't triggered | Verify agent availability settings (presence, capacity, skills), check that the "no agents available" condition is being met, and ensure the playbook is active for the correct queue. |
| Unable to publish playbook due to conflict | Another active playbook already exists for the same scenario and queue. Edit the existing playbook or modify the queue selection in your new playbook to avoid overlap. |
| Dynamic prioritization isn't being applied to a queue | The queue might have custom prioritization rules configured. Remove the custom prioritization configuration from the queue settings to enable dynamic prioritization. |

## View diagnostics using a custom query

To help you monitor and troubleshoot your playbooks, Conversation Orchestration provides diagnostics information for each conversation that is processed by an active playbook. You can view the diagnostics information by using a custom query. Learn more in [Sample queries and dashboards](/dynamics365/guidance/resources/conversation-diagnostics-sample-queries#conversation-orchestration).

### Related information

[Set up unified routing](/dynamics365/customer-service/administer/overview-unified-routing)  
[Create and manage queues](/dynamics365/customer-service/administer/queues-omnichannel)  
[Configure context variables](/dynamics365/customer-service/administer/manage-context-variables)  
[Dynamic prioritization scenarios](/dynamics365/customer-service/administer/assignment-methods#how-dynamic-prioritization-works)  
[Overflow scenario](/dynamics365/customer-service/administer/manage-overflow)
