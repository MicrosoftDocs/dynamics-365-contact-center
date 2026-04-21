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

Conversation orchestration keeps every conversation actively managed throughout the conversation lifecycle from initiation through resolution. Instead of applying fixed rules at different stages of conversation journey, conversation orchestration monitors each conversation as the conditions evolve&mdash;increase in wait time, filling up of the queues, service representatives going offline&mdash; and responds automatically with the right action. Administrators define the conversation orchestration logic using natural-language playbooks, and conversation orchestration handles the execution.

In the preview release, conversation orchestration is available for voice and live chat channels only .

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

1. On the **Conversation Orchestration** page, select one of the following prompt templates that matches your scenario:
   - **Escalate priority based on wait time**: For wait time-based dynamic or real-time prioritization.
   - **Escalate priority based on transfer to queue**: For transfer-based prioritization.
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

   > [!NOTE]
   > In preview, you can add up to two customer variables only per playbook.

1. Configure conditions and actions based on your selected template:

   **For dynamic prioritization playbooks:**
   - For **Update priority based on transfer to queue** playbook, the trigger event is preset to **Conversation is transferred**.
   - For **Update priority based on conversation wait time** playbook, the trigger event is preset to **Conversation is waiting in queue**.
   - Set the time interval for priority increase (minimum 30 seconds).
   - For each condition branch, select the context variable values that trigger this condition and set the priority score to increase (0–100,000).
   - Configure the default priority score for conversations that don't match any condition.

   **For overflow playbooks:**
   - The trigger condition is preset to **Conversation is waiting in queue**.
   - For each condition branch, select the context variable values that trigger this condition and choose the overflow action (transfer to queue, direct callback, voicemail, or end conversation).
   - Configure the default action for conversations that don't match any condition.

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

## View diagnostics using a custom query

To help you monitor and troubleshoot your playbooks, Conversation Orchestration provides diagnostics information for each conversation that is processed by an active playbook. You can view the diagnostics information by using a custom query. Learn more in [Sample queries and dashboards](/dynamics365/guidance/resources/conversation-diagnostics-sample-queries#conversation-orchestration).

### Related information

[Set up unified routing](/dynamics365/customer-service/administer/set-up-routing)  
[Create and manage queues](/dynamics365/customer-service/administer/queues-omnichannel)  
[Configure context variables](/dynamics365/customer-service/administer/context-variables)  
