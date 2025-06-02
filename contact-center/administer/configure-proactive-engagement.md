---
title: Configure proactive engagement (preview)
description: Learn how to set up proactive engagement, including dialing modes and operational rules for optimized customer service in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim 
ms.reviewer: 
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 06/02/2025
ms.custom: bap-template
---

# Configure proactive engagement (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Proactive engagement in Dynamics 365 enables organizations to enhance customer interactions by initiating outbound communications through the voice channel. This feature allows businesses to streamline customer outreach, improve agent productivity, and deliver personalized experiences. The article describes how to configure proactive engagement settings, including dialing modes, routing details, and operational rules to optimize your customer service operations.

## Prerequisites

- Voice channel is provisioned and configured. Learn more in [Provision channels](../implement/provision-channels.md) and [Install the voice channel](/dynamics365/customer-service/administer/install-voice-channel?context=/dynamics365/contact-center/context/administer-context).
- Dynamics 365 Customer Insights if you want to use journey for your customer journey authoring.
- Microsoft Copilot Studio to use Copilot agents.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Set up an outbound workstream

1. Create a workstream by selecting the **Outbound (preview)** option. Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context).
1.	Set up the outbound workstream behaviors in the **Setup Behaviors** section of the workstream as follows:
   
    - Select **Setup**, and on the page that appears, select the **Caller ID Number** in the list. Numbers available to use only are displayed. Learn more in [Configure phone numbers for outbound calling](/dynamics365/customer-service/administer/voice-channel-outbound-calling#configure-phone-numbers-for-outbound-calling).
    - Select a number in the **Shared numbers** list. The numbers available to use only are displayed.
1.	Set up the language and outbound behaviors. Learn more in [Configure the voice channel](/dynamics365/customer-service/administer/voice-channel-inbound-calling?tabs=enhancedvoice#configure-a-voice-channel)
1.	Configure [work distribution](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution), add an [AI agent](/dynamics365/customer-service/administer/create-workstreams#add-an-agent-to-a-workstream) to the workstream, and configure representative notifications. The following notification templates are available out of the box:
    - **Voice call - outbound agent dial - default**: For preview dial mode calls
    - **Voice call - outbound pre-dial - default**: For progressive and copilot dial mode calls

> [!NOTE]
> The routing rules are automatically configured based on the proactive engagement settings and appear under the **Auto generated rules (advanced)** section of the workstream.

## Configure settings to engage proactively with customers

In the site map of Copilot Service admin center, you can navigate to the proactive engagement settings in one of the following ways and then create a proactive engagement setting.

- Select **Productivity** under **Support experience**. Select **Manage** for **Proactive engagements (preview)**, and then select **New**.
- Select **Workstreams** under **Customer support**, select an outbound workstream for voice, and on the workstream page, select **New proactive engagement**.

1. On **Create new proactive engagement (preview)**, enter the following details in **Engagement details**:
   - **Name**: A name for the proactive engagement. 
   - **Description**: A description for the proactive engagement that helps the representative understand the purpose of the call.
   - **Workstream**: A workstream.
   - **Channel type**: **Voice** is selected by default and not available for edit.

1. In **Routing details**, enter the following information:
   - **Primary queue**: Select a queue. 
   - **Fallback queue**: The queue is prepopulated based on the fallback queue set for the outbound workstream.
   - **Skills**: Select the skills that are required for the proactive engagement.
1. Select **Next**. The **Dialing modes** page appears. Do the steps in the **Configure dialing modes** section that follows.

### Configure dialing modes

The dialing modes are used to determine how the system can make calls to customers. The following dialing modes are available:

1. On the **Create new proactive engagement (preview)** dialog, select one of the dialing modes as follows:
   - **Copilot**: The system automatically dials the customer and connects the call to the AI agent when the customer answers. This mode is used for high-volume outbound calls.
   - **Progressive**: The system starts the call with the AI agent and then adds a representative after the agent actions are complete.
   - **Preview**: The system adds the representative to the call and then dials the customer.

1. Select one of the following priority levels:
   - **Normal**
   - **High**
   - **Critical** 

1. Select the **Max number of concurrent calls for Copilot Mode** that refers to the maximum number of calls the AI agent can make concurrently. The maximum number that you can specify is 500.

1. Select the max number of calls that can be assigned to the representative in **Maximum calls per representative**. This setting is available for the progressive dialing mode. A lower number indicates a balanced call volume for the representative. You can specify up to five calls.

1. In **Call order**, select one of the following options:
   - **Earliest Scheduled Date**
   - **Last in First Out**
   - **First in, First Out**

1. Under **Operating hours**, select the checkbox if calls can be made outside of queue hours. This setting is available for Copilot dialing mode only.

1. Select the action for how the call needs to be handled if the AI agent fails during the call.
   - **Stop making calls immediately**: No further calls are made.
   - **Continue making calls**:
     - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.

1. For Copilot and progressive modes, select **Use rules** to set rules for the following parameters that help control the throttling and pacing for the proactive engagement:
   - **Abandonment rate**: (Copilot and progressive modes). The percentage of customers who hang up before connecting with a representative.
   - **Average wait time**: (Copilot and progressive modes).The average amount of time it takes for customers to connect to representatives.
   - **Escalation count**: (Copilot mode). The total number of escalations made from the AI agent.
   - **Open concurrent escalations**: (Copilot mode). The total number of open escalations that haven't been resolved. 

1. Select **Next** if you want to configure the outcomes.

### Configure outcomes

The outcomes are the results of the proactive engagement call. The outcomes are used to determine how the system handles the call when a customer answers.

1. On the **Create new proactive engagement (preview)** dialog, on the **Outcomes** page, select the outcomes that are available for the proactive engagement, and then select **Next**.
   - To add attributes, [configure context variables for the outbound workstream](/dynamics365/customer-service/administer/manage-context-variables).
   - Make sure that when you add the context variables in Copilot agent, you use the same names that you created in the workstream. Learn more in [Configure context variables for Copilot agent](/dynamics365/customer-service/administer/context-variables-for-bot#configure-context-variables-for-copilot-agent).

1. Review the settings on the **Summary** page, and then select **Create**.

## Configure proactive engagement with a journey using Customer Insights

Learn about how to configure a journey using Dynamics 365 Customer Insights in [Preview: How to](/dynamics365/customer-insights/journeys/proactive-engagement-how-to).

## Configure proactive engagement with a journey using the API

To configure the proactive engagement with a journey using the API, follow the steps in [Initiate proactive outbound call using API](../extend/api/ccaas_createproactivevoicedelivery.md).

## Dial modes

The dial modes are used to determine how the system makes calls to customers.

> [!IMPORTANT]
> The use of Copilot and or progressive dial modes for non-transactional commercial purposes constitutes a violation of Microsoft terms of service.

### Copilot

Use the Copilot dial mode for making announcements, notifications, or any outbound call that can be handled by an IVR agent. A large number of these calls can be made simultaneously. A few examples are payment reminders, service restoration, and delivery notifications. When a customer picks an outbound call, the AI agent registered on the workstream engages with the customer. The agent can escalate to a service representative if necessary. However, the escalated calls might have wait times similar to calls made by the customer directly to the contact center for assistance.

### Progressive

Use the progressive dial mode to call the customer first. As soon as the customer picks the call, a Copilot agent is added to the call to do basic tasks like determining if the right person has answered the call and if they're free to talk. Using an AI agent to gather this information helps service representatives avoid calls that don't need their presence. The number of calls made simultaneously is determined by the number of available agents in the queue specified&mdash;a new call is placed for every representative who is available, so that customers get a good experience with minimal wait times.
 
### Preview

Use the preview dial mode to identify a service representative from the specified queue and then notify them of the request to make the outbound call. The number of simultaneous calls made is dependent on the number of available representatives. If the representative accepts, then the system places the outbound call to customer with the representative already on the line. Representative gets to speak to the customer if they pick up or leave a voicemail. This dial mode prioritizes customer experience over representative use, and is best suited for scenarios that require a personalized experience.

## Runtime experience

Service representatives view the proactive engagement calls based on the notification template that's attached to the outbound workstream for preview and progressive modes. The name and description that you specify for the proactive engagement appears on the notification.
For the preview mode, service representatives can accept or reject the calls. 
For the progressive mode, service representatives can only start the call. 

If you configure disposition codes, service representatives can select the disposition codes to record the outcome of the interaction. Learn more in [Configure disposition codes](configure-disposition-codes.md).

### Related information

[Overview of proactive engagement](overview-proactive-engagement.md)  
[Overview of conversational journeys](/dynamics365/customer-insights/journeys/conversational-journeys-overview)  