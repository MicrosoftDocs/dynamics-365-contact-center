---
title: Configure proactive engagement (preview)
description: Learn how to set up proactive engagement, including dialing modes and operational rules for optimized customer service in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim 
ms.reviewer: 
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 05/23/2025
ms.custom: bap-template
---

# Configure proactive engagement (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Proactive engagement in Dynamics 365 enables organizations to enhance customer interactions by initiating outbound communications through the voice channel. This feature allows businesses to streamline customer outreach, improve agent productivity, and deliver personalized experiences. The article describes how to configure proactive engagement settings, including dialing modes, routing details, and operational rules to optimize your customer service operations.

## Prerequisites

- Voice channel is provisioned and configured. Learn more in [Provision channels](../implement/provision-channels.md) and [Install the voice channel](../implement/install-voice-channel.md).
- Dynamics 365 Customer Insights to use journey for your customer journey authoring.
- Microsoft Copilot Studio to use Copilot agents.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Set up an outbound workstream

1. Create a workstream by selecting the **Outbound (preview)** option. Learn more in [Create and manage workstreams](/dynamics365/contact-center/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context).
1.	Set up the outbound workstream behaviors.
1.	Select the [calling number and caller ID number](/dynamics365/customer-service/administer/voice-channel-outbound-calling#configure-phone-numbers-for-outbound-calling). Numbers available to use only are displayed.
1.	Set up the language and outbound behaviors. Learn more in [Configure the voice channel](/dynamics365/customer-service/administer/voice-channel-inbound-calling?tabs=enhancedvoice#configure-a-voice-channel)
1.	Finish setting up your outbound workstream by configuring work distribution, add an AI agent to the workstream, and configuring representative notifications. The following notification templates are available out of the box:
    - **Voice call - outbound agent dial - default**: For preview dial mode calls
    - **Voice call - outbound pre-dial - default**: For progressive and copilot dial mode calls

> [!NOTE]
> The routing rules are automatically configured based on the proactive engagement settings and appear under the **Auto generated rules (advanced)** section of the workstream.

## Configure settings for proactive engagement

You can navigate to the proactive engagement settings in one of the following ways and then create a proactive engagement.

- In the site map of Copilot Service admin center, select **Productivity** under **Support experience**. Select **Manage** for **Proactive engagements (preview)**, and then select **New**.
- Create an [outbound type of workstream](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context) for voice, and on the workstream page, select **New proactive engagement**.

1. On **Create new proactive engagement (preview)**, enter the following details in **Engagement details**:
   - **Name**: Enter a name for the proactive engagement.
   - **Description**: Enter a description for the proactive engagement.
   - **Workstream**: Select a workstream.
   - **Channel type**: **Voice** is selected by default and not available for edit.
   
   > [!NOTE]
   > The name and description of the engagement appears on the representative notification. We recommend that you use descriptive information to help them understand the purpose of the call.

1. In **Routing details**, enter the following information:
   - **Primary queue**: Select a queue. 
   - **Fallback queue**: The queue is prepopulated based on the fallback queue set for the outbound workstream.
   - **Skills**: Select the skills that are required for the proactive engagement.
1. Select **Next**. The **Dialing modes** page appears. Do the steps in the **Configure dialing modes** section that follows.

### Configure dialing modes

The dialing modes are used to determine how the system can make calls to customers. The following dialing modes are available:

1. On the **Create new proactive engagement (preview)** dialog, select one of the dialing modes as follows:
   - **Copilot**: The system automatically dials the customer and connects the call to the agent when the customer answers. This mode is used for high-volume outbound calls.
   - **Progressive**: The system starts the call with an agent and then adds a representative after the agent actions are complete.
   - **Preview**: The system adds the representative to the call and then dials the customer.

1. Select one of the following priority levels:
   - **Normal**
   - **High**
   - **Critical** 

1. Select the **Max number of concurrent calls for Copilot Mode** that refers to the maximum number of calls the AI agent can make concurrently. The maximum number that you can specify is 500.

1. Select the max number of calls that can be assigned to the representative in **Maximum calls per representative**. This setting is available for the progressive dialing mode that refers to the maximum number of customer calls to make per available representative. A lower number indicates a balanced call volume for the representative. You can specify up to five calls.

1. In **Call order**, select one of the following options:
   - **Earliest Scheduled Date**
   - **Last in First Out**
   - **First in, First Out**

1. Under **Operating hours**, select the checkbox if calls can be made outside of queue hours. This setting is available for Copilot dialing mode only.

1. Select the action for how the call needs to be handled if the AI agent fails during the call.
   - **Stop making calls immediately**: No further calls are made.
   - **Continue making calls**:
     - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.

1. For Copilot and progressive modes, set rules for the following parameters that help control the throttling and pacing for the proactive engagement:
   - **Abandonment rate**: (Copilot and progressive modes). Refers to the percentage of customers who hang up before connecting with a representative.
   - **Average wait time**: (Copilot and progressive modes). Refers to the average amount of time it takes for customers to connect to representatives.
   - **Escalation count**: (Copilot mode). Refers to the total number of escalations made from the AI agent.
   - **Open concurrent escalations**: (Copilot mode). Refers to the total number of open escalations that haven't been resolved. 

1. Select **Next**.

1. On the **Outcomes** page, select the outcomes that are available for the proactive engagement, and then select **Next**.
   - To add attributes, [configure context variables for the outbound workstream](/dynamics365/customer-service/administer/manage-context-variables).
   - Make sure that when you add the context variables in Copilot agent, you use the same names that you created in the workstream. Learn more in [Configure context variables for Copilot agent](/dynamics365/customer-service/administer/context-variables-for-bot#configure-context-variables-for-copilot-agent).

1. Review the settings on the **Summary** page, and then select **Create**.

## Configure proactive engagement with a journey using Customer Insights



## Configure proactive engagement with a journey using the API

To configure the proactive engagement with a journey using the API, follow the steps in [Initiate proactive outbound call using API](../extend/api/ccaas_createproactivevoicedelivery.md).

## Dial modes

The dial modes are used to determine how the system makes calls to customers.

> [!IMPORTANT]
> The use of Copilot and or progressive dial modes for non-transactional commercial purposes constitutes a violation of Microsoft's terms of service.

### Copilot

Use the Copilot dial mode for making announcements, notifications, or any outbound call that can be handled by an IVR agent. A large number of these calls can be made simultaneously. A few examples are payment reminders, service restoration, and delivery notifications. When a customer picks an outbound call, the agent registered on the workstream engages with the customer. The agent can escalate to a service representative if necessary. However, the wait times might be similar to if the customer had called into the contact center for assistance.

### Progressive

Use the progressive dial mode to call the customer first. As soon as the customer picks the call, a Copilot agent is added to the call to do basic tasks like determining if the right person has answered the call and if they're free to talk. Using an AI agent to gather this information saves service representatives from joining calls that don't need them to be on it further maximizing time spent in helping customers. The number of calls made simultaneously is determined by the number of available agents in the queue specified&mdash;a new call is placed for every representative that gets available ensuring that customers get a good experience with minimal wait times.
 
### Preview

Use the preview dial mode to identify a service representative from the specified queue and then notify them of the request to make the outbound call. If the representative accepts, then the system places the outbound call to customer with the representative already on the line. Representative gets to speak to the customer if they pick up or leave a voicemail. This dial mode prioritizes customer experience over representative use, and is best suited for scenarios that require a personalized experience. As a result, the number of simultaneous calls made is dependent on the number of available representatives.


## Runtime experience

Service representatives view the proactive engagement calls based on the notification template that's attached to the outbound workstream for preview and progressive calls. The name and description that you specify for the proactive engagement appears on the notification.
For the preview mode, service representatives can start or reject the calls. 
For the progressive mode, service representatives can only start the call. 

If you configure disposition codes settings, service representatives can select disposition codes to record the outcome of the interaction. Learn more in [Configure disposition codes].(configure-disposition-codes.md)

### Related information

[Overview of proactive engagement](overview-proactive-engagement.md)  