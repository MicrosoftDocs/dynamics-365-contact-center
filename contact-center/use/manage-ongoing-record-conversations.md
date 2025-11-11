---
title: Manage ongoing record conversations
description: Learn how to manage ongoing record conversations effectively in Dynamics 365 Contact Center. Assign, transfer, release, or remove conversations to improve operational efficiency.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection:
ms.date: 11/11/2025
ms.custom: bap-template
---

# Manage ongoing record conversations

As a supervisor, you can efficiently manage ongoing record conversations to ensure smooth operations and enhance customer engagement. The ongoing record conversations view enables you to assign, transfer, release, and remove conversations with ease.

## Prerequisites

- You have the Omnichannel Supervisor role. Learn more in [Assign roles and enable users](/dynamics365/customer-service/implement/add-users-assign-roles). 


## Access the Ongoing record conversations view

In the site map of Copilot Service workspace, go to **Conversations**. Select **Ongoing record conversations** from the dropdown.

## Tasks you can perform

### Assign a conversation

Assign open conversations to representatives or queues.

1. Select a conversation with an **Open** status from the entity record list.
1. Select **Assign**.
1. On the **Assign work item** dialog, select either an representative (filter by name, queue, skills, or presence) or a queue (filter by queue name).
1. Select **Assign** to assign the conversation to the representative or queue. 

If no eligible representatives or queues are available, the system notifies you.

###  Transfer a conversation

Transfer conversations, with additional options for intent-based conversations (selecting user groups, intent families, and queue priorities).

1. Select the conversation you want to transfer.
1. Select **Transfer**.
1. In the **Transfer work item** dialog:
    - For standard cases, filter and select a representative (filter by name, queue, skills, or presence) as required.
    - For intent-based conversations, review and select the representative (filter by name, intent family, intent group, intent, user group and presence) and queue (filter by intent-based and queue priority).
1. Select **Transfer** to move the conversation to the selected representative or queue.
    
The dialog displays relevant fields based on the conversation type.

### Release a conversation

Release a conversation, making it available for other representatives in the queue.

1. Select the conversation you want to release.
1. Select **Release** to confirm the release in the pop-up notification.

The conversation becomes available for other representatives in the queue to pick up.

### Remove a conversation

Remove a conversation from the queue entirely.

1. Select the conversation you wish to remove and select **Remove** to confirm the removal in the pop-up notification.

The conversation is removed from the queue and no longer appears in the list.

## Related information

[Manage all ongoing conversations](all-ongoing-conversations.md)
