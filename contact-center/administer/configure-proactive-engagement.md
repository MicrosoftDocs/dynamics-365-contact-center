---
title: Configure proactive engagement (preview)
description: Learn how to configure proactive engagement in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim 
ms.reviewer: 
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 05/19/2025
ms.custom: bap-template
---

# Configure proactive engagement (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Proactive engagement in Dynamics 365 enables organizations to enhance customer interactions by initiating outbound communications through the voice channel. This feature allows businesses to streamline customer outreach, improve agent productivity, and deliver personalized experiences. This article describes how to configure proactive engagement settings, including dialing modes, routing details, and operational rules to optimize your customer service operations.

## Prerequisites

- Specific licenses are required to configure and use proactive engagement in Dynamics 365 Contact Center. Learn more in [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/?linkid=2309719).
- Voice channel is provisioned and configured. Learn more in [Provision channels](../implement/provision-channels.md) and [Install the voice channel](../implement/install-voice-channel.md).
- Dynamics 365 Customer Insights
- Microsoft Copilot Studio

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## How it works

1. Configure a phone number.
1. Configure an outbound type of workstream for voice in the Copilot Service admin center.
1. Configure the voice channel.
1. Configure an AI agent.
1. Add the AI agent to the workstream.
1. Configure outcomes using Power Automate flows.
1. Configure context variables.
1. Configure notification templates.
1. Configure outbound profile settings.
1. Define notification templates to use in progressive dialing mode.
1. Create a proactive engagement in the Copilot Service admin center.
1. Configure journeys using Customer Insights or the API.

## Configure settings for proactive engagement

You can navigate to the proactive engagement settings in one of the following ways and then create a proactive engagement.

- In the site map of Copilot Service admin center, select **Productivity** under **Support experience**. Select **Manage** for **Proactive engagements (preview)**, and then select **New**.
- Create an [outbound type of workstream](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context) for voice, and on the workstream page, select **New proactive engagement**.

1. On **Create new proactive engagement (preview)**, enter the following details in **Engagement details**:
   - **Name**: Enter a name for the proactive engagement.
   - **Description**: Enter a description for the proactive engagement.
   - **Workstream**: Select a workstream.
   - **Channel type**: **Voice** is selected by default and not available for edit.
1. In **Routing details**, enter the following information:
   - **Primary queue**: Select a queue. 
   - **Fallback queue**: Select a fallback queue.
   - **Skills**: Select the skills that are required for the proactive engagement.
1. Select **Next**. The **Dialing modes** page appears.
1. Select one of the dialing modes as follows:
   - **Copilot**: The system automatically dials the customer and connects the call to the agent when the customer answers. This mode is used for high-volume outbound calls.
   - **Progressive**: The system starts the call with an agent and then adds a representative after the agent actions are complete.
   - **Preview**: The system add the representative to the call and then dials the customer.
1. Select one of the following priority levels:
   - **Normal**: 
   - **High**: 
   - **Critical**: 
1. Select the number of concurrent calls that can be assigned to the representative in **Maximum calls per representative**. This setting is available for Copilot and progressive dialing modes.
1. In **Call order**, select one of the following options:
   - **Earliest Scheduled Date**
   - **Last in First Out**
   - **First in, First Out**
1. Under **Operating hours**, select the checkbox if calls can be made outside of queue hours. This setting is available for Copilot dialing mode only.
1. Select the action for how the call needs to be handled if the AI agent fails during the call.
   - **Stop making calls immediately**: No further calls are made.
   - **Continue making calls**:
     - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.
1. Optionally, select **Use rules** to define rules in the **Rules** section. Configure the settings to decrease the concurrent calls percent based on the threshold parameters for one of the following:
   - **Average wait time**
   - **Abandonment rate**
1. Select **Next**.
1. On the **Outcomes** page, select the outcomes that are available for the proactive engagement, and then select **Next**.
1. The **Summary** page displays the settings that you configured. Review the settings, and then select **Create**.

## Configure proactive engagement with a journey using Customer Insights

To be linked to the Customer Insights documentation.

## Configure proactive engagement with a journey using the API

To configure the proactive engagement with a journey using the API, follow the steps in [Initiate proactive outbound call using API](../extend/api/ccaas_createproactivevoicedelivery.md).

## Dial modes

The dial modes are used to determine how the system will initiate calls to customers.

- **Copilot**: Use the Copilot dial mode for making announcements, notifications, or any outbound call that can be handled by an IVR agent. A large number of these calls can be made simultaneously. A few examples are payment reminders, service restoration, and delivery notifications. When a customer picks an outbound call, the agent registered on the workstream engages with the customer. The agent can escalate to a service representative if required. However, the wait times might be similar to if the customer had called into the contact center for assistance.

- **Progressive**: Use the progressive dial mode to call the customer first. As soon as the customer picks the call, a Copilot agent is added to the call to perform basic tasks like determining if the right person has answered the call and if they are free to talk. Using an AI agent to gather this information saves service representatives from joining calls that don't need them to be on it further maximizing time spent in helping customers. The number of calls made simultaneously is determined by the number of available agents in the queue specified&mdash;a new call is placed for every representative that gets available ensuring that customers get a good experience with minimal wait times.
 
- **Preview**: Use the preview dial mode to identify a service representative from the specified queue and then notify them of the request to make the outbound call. If the representative accepts, then the system places the outbound call to customer with the representative already on the line. Representative gets to speak to the customer if they pick up or leave a voicemail. This dial mode prioritizes customer experience over representative use, and is best suited for scenarios that require a personalized experience. As a result the amount of simultaneous calls made is dependent on number of available representatives.


## Outcomes

_Need information on how to configure outcomes._

## Runtime experience

_Need information on runtime experience._

### Related information
