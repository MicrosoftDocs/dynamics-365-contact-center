---
title: Configure bullseye routing using conversation orchestration playbooks (preview)
description: Configure bullseye routing to optimize customer service assignments. Discover how to evaluate assignment flows and prioritize users effectively.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 07/13/2026
ms.topic: how-to
ms.collection: bap-ai-copilot
---

# Configure bullseye routing by using conversation orchestration playbooks (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Bullseye routing assigns conversations by progressively expanding the pool of eligible users within a queue until it finds a suitable match. It doesn't assign from a fixed pool or wait for overflow rules to trigger. It uses levels to define how the assignment scope expands over time.

By configuring this behavior in [conversation orchestration](configure-conversation-orchestration.md), you ensure that the system first attempts assignment within the most targeted set of users before gradually expanding to a broader set when no match is found.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/production-ready-preview-dynamics365.md)]

## Prerequisites

- Conversation orchestration is available.
- At least one user and queue is associated with a [user group](#create-user-groups).

## Configure bullseye routing

Follow the steps in [Create a playbook](configure-conversation-orchestration.md) to configure the bullseye playbook with levels and wait times for routing. Use the onscreen help and tips to define the levels.

- Ensure multiple queues selected in a playbook share common user groups. The playbook displays user groups that are common across the selected queues only during configuration.
- Create different bullseye routing playbooks for different queues if the queues don't share user groups.

A sample configuration is as follows.

:::image type="content" source="../media/screenshot-bullseye-routing-configuration.png" alt-text="A screenshot of a sample setting to handle routing of work items using bullseye assignment method.":::

## How bullseye routing works

When a conversation enters a queue, the system performs assignment in a progressive sequence. You can configure one or more user groups at each level. The system evaluates the user groups that you configure at the same level. Based on the wait time thresholds, the system gradually expands the assignment pool to include more support representatives from each level.

The system runs the routing as follows:

1. Attempts to assign the conversation to representatives in the user groups defined at Level 0.
1. Expands the next level based on the configured wait time if no eligible representative is found in the previous level.
1. Adds the user groups defined at a level to the existing pool of eligible representatives from the previous level. User groups from earlier levels remain active and continue to be considered for assignment.
1. Establishes assignment priority by considering all active user groups until the current level of expansion. Representatives from previous levels receive higher priority than representatives added at later levels.
1. Finds the most suited service representative within a user group based on the queue's assignment strategy (round robin, highest capacity, least active) when multiple users are eligible with the same priority at any level. Custom assignments aren't supported.
1. Honors all checks for representative presence, capacity, and skills (if skill-based routing is configured).
1. Applies the configured fallback option if no eligible user is found after all levels are evaluated. If a user group is associated with the queue, the system considers all users in that user group as part of the queue.
1. Finalizes fallback depending on configuration by either assigning the conversation to any eligible user in the queue (direct member of the queue or member via user group), or by restricting assignment to users within the defined user groups. This process ensures that conversations can still be assigned when no match is found within the configured levels.

## Configure wait times

Wait time determines when each level becomes eligible for expansion within the queue. The assignment scope expands cumulatively across levels, while previous levels remain active and retain higher priority.

1. Measures wait time cumulatively from when the system first attempts to assign the conversation to a human support representative.
1. Evaluates level increments accurately. For example, if Level 1 is configured to expand at 30 seconds and Level 2 at 45 seconds, Level 2 expansion occurs at 45 seconds after the initial assignment attempt (15 seconds after level 1 expansion happens).
1. Expands consecutive levels back-to-back with no delay if they have the same wait time. The user group priority is maintained. To continue the example in the previous step, let's say Level 3 is also configured to expand at 45 seconds. Then, the Levels 2 and 3 expansion happen at the same time, with the user group priorities for Levels 2 and 3 maintained. However, Level 2 user group has a higher priority than Level 3.
1. Sets the minimum wait time to at least 30 seconds. The next level wait time can be the same as the previous level or should increment by at least 10 seconds. Note that Level 1 also supports a 0 second wait time.
1. Resets the wait time and restarts evaluation from Level 0 in the new queue if a conversation is transferred to another queue.

## Process a routing example

Consider a configuration with three levels: Level 0 (Expert support group), Level 1 at 30 seconds (Regional support group), and Level 2 at 60 seconds (General support group).

1. The system attempts assignment to the Expert support group at Level 0.
1. The system adds the Regional support group after 30 seconds, while continuing to consider service representatives from the Expert group.
1. The system adds the General support group after 60 seconds, while still prioritizing earlier groups.
1. The system applies the fallback behavior to ensure assignment completion if no assignment is made after all levels.

## Extend with dynamic prioritization

You can increment the priority of conversations based on wait time or perform overflow actions with bullseye routing.

1. Navigate to Conversation orchestration.
1. Configure dynamic prioritization or overflow playbooks for the same queue to extend your routing behavior.

### Create user groups

Create user groups to organize members by skills, language, region, or other attributes. Use user groups to assign work items by configuring natural language playbooks for bullseye routing. When you configure user groups, you don't need to manually add users to queues because the queue membership comes through the user groups.

1. In the site map of Copilot Service admin center, under **Customer support**, select **User management**.

1. Under **User groups**, select **Manage**.
1. Select **New**.
1. On **Create user group**, enter the following details:
   - **Group name**
   - **Description**
   - **Add members**: Select and add the users for the group. Use **Filters** on the top right to view the active filters and filter by the appropriate set of users for the group. This filtering criteria doesn't assign any filter category to the user group.
   - **Add queues**: Add the queues that the user group needs to belong to.

1. Save the changes.

### View diagnostics for bullseye routing

You can view the diagnostics information by using a custom query. Learn more in [Sample queries and dashboards](/dynamics365/guidance/resources/conversation-diagnostics-sample-queries).

### Related information

[Set up unified routing](/dynamics365/customer-service/administer/overview-unified-routing)  
[Assignment methods](/dynamics365/customer-service/administer/assignment-methods)  
