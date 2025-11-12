---
title: Manage all ongoing conversations
description: Learn how to resolve customer queries faster with the All ongoing conversations view in Dynamics 365 Contact Center. Perform bulk actions, notify representatives, and track updates.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection:
ms.date: 11/07/2025
ms.custom: bap-template
---

# Manage all ongoing conversations

The **All ongoing conversations** view helps supervisors monitor, manage, and optimize customer conversations across digital messaging, voice, and record channels. Use the view to filter conversations, run bulk actions, and work with your team to track updates. 

**Key capabilities**

- **Live conversation monitoring**: View all active conversations by channel (chat or voice) in a dedicated, organized interface.
- **Immediate actions**: Assign, transfer, monitor, force close, or notify conversations individually, enabling prompt intervention.
- **Advanced filtering and saved views**: Filter conversations by agent, queue, channel, or sentiment, and save or share custom views to enhance team coordination.
- **Bulk management**: Efficiently manage large volumes of conversations with multi-conversation actions for persistent interactions.

## Prerequisites

- You have the Omnichannel Supervisor role. Learn more in [Assign roles and enable users](/dynamics365/customer-service/implement/add-users-assign-roles). 


## Access the All ongoing conversations view

In the site map of Copilot Service workspace, go to **Conversations**. The **All ongoing conversations** view appears by default.


## Perform bulk actions

As a supervisor, managing multiple items individually can be time-consuming and error-prone. Bulk actions enables supervisors to perform operations on multiple records simultaneously, reducing repetitive tasks and improving efficiency. Batch processing helps reduce errors and keeps updates consistent across selected records.

Select multiple conversations to view and perform bulk actions on the **All ongoing conversations** view. 

:::image type="content" source="../media/all-ongoing-conversations-view.png" alt-text="Screenshot of All ongoing conversations with bulk actions enabled.":::

You can perform the following actions.

### Assign conversations

Assign live and persistent chat conversations in open status from specific queues to a new queue, as required.

1. Select the required conversations from the **All ongoing conversations** view. 
1. On the **Assign work item** dialog, go to the **Find a queue** tab.
1. Select the specific queue and then select **Assign** to transfer the selected conversations to the queue.
 
    :::image type="content" source="../media/bulk-assign.png" alt-text="Screenshot of assign to a queue or agent dialog." lightbox="../media/bulk-assign.png":::

### Close multiple conversations

Close multiple conversations pertaining to persistent and live chat that are in open, active, wrap-up, and waiting state.

- Select the conversations, and then select **Force Close**.

### Message customer

Broadcast messages to customers to provide resolution and closure outside the conversation channel. After you broadcast to persistent chat conversations in **Open** status, the conversations move to **Waiting** status.

- Select the required conversations, and then select **Message Customer** to directly chat with the customers.

### Notify representatives

Notify representatives engaged in persistent and live chat conversations with real-time updates or guidance related to specific issues. After notification, the status updates are visible in the **Action History** section. 

- Select **Notify CSR** to send notification to representatives, such as alerts about ongoing issues.

    :::image type="content" source="../media/notify-representative.png" alt-text="Screenshot of Send notification to representatives dialog." lightbox="../media/notify-representative.png":::

### Track the status of bulk actions

Track the status of bulk actions performed on conversations. All bulk actions are recorded in **Action History**, such as **Action type**, **Title**, **Created by**, **Recipients**, **Start and End time**, **Status**, and **Action status details**. You can also view the action history by selecting the **Bulk action status** option, that appears once you have taken any action on conversations.
 
- Select **Action History** to check the status of the action that you have taken for conversations.

    :::image type="content" source="../media/bulk-action-history.png" alt-text="Screenshot shows bulk action history details." lightbox="../media/bulk-action-history.png":::

## Limitations

- Bulk actions require supervisor approval and can only be performed by users with the Omnichannel Supervisor role. Only administrators have permission to delete items.
- Bulk actions can be performed on up to 1,000 conversations simultaneously. 
- Message fields to send messages to customers or notify representatives are limited to 1,000 characters. 

## Related information

[Assign roles and enable users](/dynamics365/customer-service/implement/add-users-assign-roles)