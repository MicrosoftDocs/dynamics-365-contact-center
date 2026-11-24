---
title: Manage queue profiles
description: Queue profiles help tailor customer and representative experiences in your contact center. Set channel-specific rules and apply profiles to the right queues.
ms.date: 11/24/2026
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ai-usage: ai-assisted
---

# Manage queue profiles

Use queue profiles to customize conversation behavior at the queue level. This feature is currently available at the workstream and channel level. After you configure and assign the profile to the queue, you can control behaviors such as which automated messages customers receive and what happens when a customer or service representative doesn't respond.

The following steps describe how to configure a profile and apply it to a queue. These profiles are applicable to voice and messaging channels only.

The settings available in a queue profile depend on the channel you select.

> [!IMPORTANT]
> The configurations in the selected queue profile apply to all conversations in the queue and override the workstream settings.

## Create a queue profile

1. In Copilot Service admin center, select **Channels** in **Customer support**, and then open **Queue profiles**.
2. On the **Queue profiles** page, select **Add queue profile**.
3. On the **Summary** page, in **Profile overview**, enter the following details:
   - **Profile name**: Enter a name for the queue profile.
   - **Description**: Optionally, enter a description.
   - **Channel**: Select one of the following channels:
       - **Chat**
       - **Voice call**
       - **WhatsApp**
       - **SMS**
       - **Facebook**
       - **LINE**
       - **Microsoft Teams**
       - **Custom**
4. Select **Save** on the command bar. The profile status changes from **Draft** to **Active**.

   The following tabs appear based on the channel you selected:

   - **Automated messages**
   - **Timeout rules**
   - **Agent affinity**
   - **Custom voice message**
   - **Notifications**
   - **After call work**
   - **Post-call survey**

   :::image type="content" source="../media/queue-profile-summary.png" alt-text="A summary screenshot of the queue profile for voice channel with the configured behavior.":::

   Use the information in the following sections to configure these options.

### Configure automated messages

Set up messages that the system sends when specific events happen during a conversation. For example, you can send a greeting when a service representative joins a customer conversation.

1. In the queue profile, select **Automated messages**.
1. Select **Add automated message**.
1. In the **Add automated message** pane, configure the following fields:
   - **Name**: Enter a name for the message.
   - **Message trigger**: Select the event that sends the message. For example, select **Agent joined customer conversation** to send a greeting when a service representative joins.
   - **Automated message**: Enter the message text.
   - **Default language**: Select the language for the message.

   The **Channel type** field is populated from the profile's channel. 
1. Select **Save** in the pane.
Add more automated messages as needed, and then select **Save** on the command bar to save the profile changes.

### Configure timeout rules

Use timeout rules to specify an action when a customer or service representative doesn't respond within a configured time.

1. In the queue profile, select **Timeout rules**, and then select **Add timeout rule**.
1. Configure the following fields:
   - **Trigger event**: Select **Customer Non-Response Time** or **Representative Non-Response Time**.
   - **Time threshold**: Enter the amount of time to wait before taking the action.
   - **Unit**: Select **Minutes**, **Hours**, or **Days**.
   - **Action**: Select the action to take when the time threshold is reached.
1. To send a reminder to a customer who doesn't respond, select **Customer Non-Response Time** as the trigger and **Send customer automated message** as the action. Select the **Language**, and enter the reminder text in **Automated message**. For example, set the threshold to **1** and the unit to **Minutes** to send a reminder after one minute without a customer response.
1. Optionally, select **Add message** to configure another language and message, or select **Add timeout rule** to configure another rule.

### Configure representative affinity

Representative affinity is available for async channels only. Use it to assign returning conversations to the service representative who handled them previously.

1. In the queue profile, select **Agent affinity**.
1. Turn on the **Agent affinity** toggle to assign returning conversations to the previous representative, or turn it off to disable this behavior.
1. Select **Save** on the command bar.

### Configure a custom voice message

For the voice channel, configure voice messages to deliver engaging and informative waiting experiences to customers while their conversations wait in the queue. By using text-to-speech messages and time-based automation rules, administrators can tailor queue behaviors to improve customer satisfaction and reduce perceived wait times. Define message delivery timing by delay after conversation enters the queue. Configure up to seven automated messages.

1. In the voice queue profile, select **Custom voice message**, and then select **Add custom voice message**.
1. In the **Add custom voice message** pane, configure the following fields:
   - **Language code**: Select the language for the message.
   - **Message**: Enter the message text.
   - **Delay before the message is played**: Enter the delay in seconds before the message plays.
   - **Recurring message**: Select one of the following options:
       - **Yes**: Enter values to indicate the number of times the system repeats the message and the interval in seconds in the corresponding fields.
       - **No**: Plays it once.

   The **Trigger** and **Message recipient** fields are preset to **Conversation waiting in queue** and **Customer**, respectively that aren't editable.
1. Select **Save** in the pane.
1. Save the changes.

**How it works**

- The system activates the rules after the open call enters the queue.

- If the call moves to active state and then back to open, the messages restart from the beginning.
- The system uses workstream music, and after each message restarts the same music file.
- Calls transferred to another queue restart the new queue’s sequence of wait messages if configured.
- If you configure other automated messages (overflow messages, direct callback messages, average wait time, or queue position), they play at their specified time. If their playback conflicts with a custom queue wait message, they play sequentially and don't interrupt current playback.

### Configure notifications

Select the notification templates that service representatives receive for different voice call events.

1. In the voice queue profile, select **Notifications**.
1. Under **Notification settings**, select a notification template for each of the following events:
   - **Incoming unauthenticated**: An incoming call from an unauthenticated customer.
   - **Incoming authenticated**: An incoming call from an authenticated customer.
   - **Direct callback - preview**: A notification for a direct callback preview dialing.
   - **Consult**: A consultation request.
   - **Transfer**: A call transfer.
   - **Supervisor assign**: A call assigned by a supervisor.
1. Save the changes.

### Configure after-call work

Choose whether a service representative's capacity stays blocked while they wrap up a conversation.

1. In the voice queue profile, select **After call work**.
1. In **Block capacity for wrap-up**, select the required option. For example, select **Always block** to keep the representative's capacity blocked during wrap-up.
1. Select **Save** on the command bar.

### Configure a post-call survey

Send a survey to customers after their voice conversation ends to collect feedback.

1. In the voice queue profile, select **Post-call survey**.
1. Turn on **Enable post-call survey**.
1. In **Survey bot**, select the agent to use for the survey.
1. Select **Save**.

## Apply the profile to a queue

After you configure the profile, select it in the queue that should use its settings.

1. In Copilot Service admin center, select **Queues** in **Customer support**, and then open the queue.
1. In the **Queue profile** section, select **Edit**.
1. In the **Edit queue profile** pane, select the profile in **Select a queue profile**.
1. Select **Save and close**. The profile name appears under **Selected profile** in the queue's **Queue profile** section.

## Related information

[Create queues](/dynamics365/customer-service/administer/queues-omnichannel?context=/dynamics365/contact-center/context/administer-context)  

