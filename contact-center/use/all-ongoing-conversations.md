---
title: Manage ongoing conversations
description: Learn how to resolve customer queries faster with the All Ongoing Conversations view. Perform bulk actions, notify representatives, and track updates.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: conceptual
ms.collection:
ms.date: 11/06/2025
ms.custom: bap-template
---

# Manage ongoing conversations

The Ongoing Conversations view helps supervisors monitor, manage, and optimize customer conversations across digital messaging, voice, and record channels. Use the view to filter conversations, run bulk actions, and work with your team. This article shows how to use the view to resolve queries quickly, notify representatives, and track updates.

In the site map of Copilot Service workspace, go to **Conversations**. The **All ongoing conversations** view appears by default.

## Key capabilities

- **Live conversation monitoring**: View all active conversations by channel (chat or voice) in a dedicated, organized interface.
- **Immediate actions**: Assign, transfer, monitor, force close, or notify conversations individually, enabling prompt intervention.
- **Advanced filtering and saved views**: Filter conversations by agent, queue, channel, or sentiment, and save or share custom views to enhance team coordination.
- **Bulk management**: Efficiently manage large volumes of conversations with multi-conversation actions for persistent interactions.

## Prerequisites

- You have the Omnichannel Supervisor role. Learn more in [Assign roles and enable users](/dynamics365/customer-service/implement/add-users-assign-roles).

## Perform bulk actions

As a supervisor, managing multiple items individually can be time-consuming and error-prone. Bulk actions enables supervisors to perform operations on multiple records simultaneously, reducing repetitive tasks and improving efficiency. Batch processing helps reduce errors and keeps updates consistent across selected records.

Select multiple conversations to view and perform bulk actions on the **Ongoing Conversations** view. 

:::image type="content" source="../media/all-ongoing-conversations-view.png" alt-text="Screenshot of all ongoing conversations with bulk actions enabled.":::

You can perform the following actions:

### Assign

Assign conversations to the appropriate queue, based on agent skills or availability. Applicable to persistent and live chat conversations in **Open** status.

- Select the required conversations, and then select **Assign** to transfer selected conversations to that queue.
 
    :::image type="content" source="../media/bulk-assign.png" alt-text="Screenshot of assign to a queue or agent dialog." lightbox="../media/bulk-assign.png":::

### Force Close

Close multiple conversations at once and easily manage inactive threads. Applicable to persistent and live chat conversations in **Open**, **Active**, **Wrap-up**, and **Waiting**. You can clear multiple test conversations at once for both persistent and live chat.

- Select the required conversations, and then select **Force Close** to close  multiple conversations. Confirm your action on the confirmation message.

### Message Customer

Send broadcast messages to customers to provide resolution and closure outside the conversation channel. You can send messages to multiple customers at once. Available to persistent chat conversations in **Open** status. Once the message is sent, the conversations move to **Waiting** status.

- Select the required conversations, and then select **Message Customer** to directly chat with the customers.

### Notify representative

Notify customer service representatives with real-time updates or guidance related to specific conversations. Applicable to active, persistent, and live chat conversations currently assigned to representatives. Upon notification, status updates are visible in **Action History** section. 

- Select **Notify CSR** to send notification to agents, such as alerts about ongoing issues.

    :::image type="content" source="../media/notify-csr.png" alt-text="Screenshot of Send notification to representatives dialog." lightbox="../media/notify-csr.png":::

### Action History

Track the status of bulk actions performed on conversations. All bulk actions are recorded in **Action History**, including details such as **Action type**, **Title**, **Created by**, **Recipients**, **Start and End time**, **Status**, and **Action status details**. You can also view the action history by selecting the **Bulk action status** option, that appears once you have taken any action on conversations.
 
- Select **Action History** to check the status of the action that you have taken for conversations.

    :::image type="content" source="../media/bulk-action-history.png" alt-text="Screenshot shows bulk action history details." lightbox="../media/bulk-action-history.png":::

## Limitations

- Bulk actions require confirmation from a supervisor and the Omnichannel Supervisor role for execution. Deletion rights are restricted to administrators only.
- Bulk actions can be performed on up to 1,000 conversations simultaneously. 
- Message fields to send messages to customers or notify representatives are limited to 1,000 characters. 

## Related information

[Assign roles and enable users](/dynamics365/customer-service/implement/add-users-assign-roles)