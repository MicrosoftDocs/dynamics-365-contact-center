---
title: Configure proactive engagement in Dynamics 365 Contact Center
description: Learn how to set up proactive engagement, including dial modes and operational rules for optimized customer service in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 04/29/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Configure proactive engagement

Proactive engagement in Dynamics 365 helps your organization improve customer interactions by initiating outbound communications through the voice and SMS channels. This feature helps your business streamline customer outreach, boost agent productivity, and deliver personalized experiences. This article explains how to configure proactive engagement settings, including dialing modes, routing details, and operational rules to optimize your customer service operations.

## Prerequisites

### [Voice](#tab/voice)

- Voice channel is provisioned and configured. Learn more in [Provision channels](../implement/provision-channels.md) and [Install the voice channel](/dynamics365/customer-service/administer/voice-channel-install?context=/dynamics365/contact-center/context/administer-context).

### [SMS](#tab/sms)

- SMS channel is provisioned and configured. Learn more in [Provision channels](../implement/provision-channels.md) and [Configure SMS channel](/dynamics365/customer-service/administer/configure-sms-channel?context=/dynamics365/contact-center/context/administer-context).

---

- Dynamics 365 Customer Insights if you want to use journey for your customer journey authoring.
- Microsoft Copilot Studio to use Copilot agents.

## Set up an outbound workstream

### [Voice](#tab/voice)

1. Create a workstream by selecting the **Outbound** option. Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context).

1. In the **Setup Behaviors** section of the workstream, select **Setup**.
1. On the **Phone number** page, select a number in the **Shared numbers** list. You can use a number configured for an outbound profile (for representative dialing in Copilot Service workspace) or outbound workstream only. Learn more in [Configure phone numbers for outbound calling](/dynamics365/customer-service/administer/voice-channel-outbound-calling#configure-phone-numbers-for-outbound-calling).
1. Set up the language and outbound behaviors. Learn more in [Configure the voice channel](/dynamics365/customer-service/administer/voice-channel-inbound-calling?tabs=enhancedvoice#configure-a-voice-channel).
1. Configure [work distribution](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution). Optionally add an [AI agent](/dynamics365/customer-service/administer/create-workstreams#add-an-agent-to-a-workstream) to the workstream, and configure representative notifications. The following notification templates are available out of the box:
    - **Voice call - outbound agent dial - default**: For preview dial mode calls
    - **Voice call - outbound pre-dial - default**: For predictive, progressive, and Copilot dial mode calls

> [!NOTE]
> By using Azure Communication Services, you can use Direct Routing numbers only. By using Teams Phone numbers, you can use Direct Routing, Direct Offer, and Operator Connect numbers.

### [SMS](#tab/sms)

1. Create a workstream by selecting the **Outbound** option and setting the type to **Messaging** and channel to **SMS**. Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context).

1. Set up the outbound workstream behaviors in the **Setup up your SMS channel** section of the workstream as follows:

    - Select **Setup**, and on the page that appears, select the **SMS Number** in the list. Numbers available to use only are displayed. Learn more in [Configure SMS channel](/dynamics365/customer-service/administer/configure-sms-channel?context=/dynamics365/contact-center/context/administer-context).
    - Set up the outbound behaviors. Learn more in [Configure SMS channel](/dynamics365/customer-service/administer/configure-sms-channel?context=/dynamics365/contact-center/context/administer-context).
1. Configure [work distribution](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution), optionally add an [AI agent](/dynamics365/customer-service/administer/create-workstreams#add-an-agent-to-a-workstream) to the workstream, and configure representative notifications.

---

> [!NOTE]
> The system automatically configures the routing rules based on the proactive engagement settings. These rules appear under the **Auto generated rules (advanced)** section of the workstream.

## Configure settings to engage proactively with customers

1. In the site map of Copilot Service admin center, go to the settings by using one of the following methods. Then, create a proactive engagement setting.

   - Select **Productivity** under **Support experience**. Select **Manage** for **Proactive engagements**, and then select **New**.
   - Select **Workstreams** under **Customer support**, select an outbound workstream for voice, and on the workstream page, select **New proactive engagement**.

   The **Create new proactive engagement** wizard guides you through the steps outlined in the following sections:
   - **Audience**
   - **Details**
   - **Dialing modes** (voice only)
   - **Display number configuration** (voice only)
   - **Reattempts** (voice only)
   - **Frequency limits**
   - **Preferences** (SMS only)
   - **SMS template configuration** (SMS only)
   - **Summary**

### [Voice](#tab/voice)

[!INCLUDE [proactive-audience](../includes/proactive/cc-proactive-audience.md)]

1. Under **Engagement type**, select one of the options to determine how the call is handled:

      - **Led by representatives**: Always connect customers to service representatives.
      - **Led by AI**: Let Copilot interact with customers first as they answer the calls, then add representatives at the right moment.

   > [!NOTE]
   > A single workstream can run both AI-led and representative-led proactive engagements simultaneously.

1. Select **Next**.

[!INCLUDE [proactive-details](../includes/proactive/cc-proactive-details.md)]

**Dialing modes**

The dial modes determine how the system places outbound calls to customers. Learn more in [Dial modes for proactive engagement](proactive-engagement-dial-modes.md).

1. Select one of the following dial modes:
   - **Copilot**: Applies to AI agent-led engagements. The system automatically dials the customer and connects the call to the AI agent when the customer answers. Use this mode for high-volume outbound calls.
   - **Preview**: Applies to representative-led engagements. The system notifies a service representative of the outbound call request and after acceptance, places the call to the customer.
   - **Progressive**: Applies to both representative- and AI agent-led engagements. The system starts calls equal to the number of available representatives, and on customer answer adds a representative or AI agent based on the engagement type. If type is representative led, service representatives are reserved ahead of time for a good customer experience.
   - **Predictive**: The system starts calls proportional to the number of available agents or representatives, and on customer answer adds a representative or AI agent based on the engagement type. A predictive model considers factors like representative availability, abandonment rate, and answer rate to determine the number of calls to initiate per representative. If type is representative led, representatives are reserved ahead of time to ensure a good customer experience.

1. Priority determines the processing order of the proactive engagement. Select one of the following priority levels:
   - **Normal**
   - **High**
   - **Critical**
   
     Priority determines the processing order when multiple proactive engagements compete for the same representatives (same queue and skill set). Higher-priority engagements are processed first. For example, if a critical and a normal proactive engagement both target the same queue, the system processes the critical engagement first and handles the normal engagement only when no higher-priority requests are pending.
     
     The system processes proactive engagements with same priority in a queue in a round robin manner to ensure fair processing.

1. In **Call order**, select one of the following options to define how the system processes requests within each proactive engagement:
   - **Earliest Scheduled Date** - Processes records that are close to end of calling window first.
   - **Last in First Out** - Processes most recent records first, in a last in first out manner.
   - **First in, First Out** - Processes older records first, in a first in first out manner.
   - **Custom priority ascending**: Processes records in ascending order based on a priority attribute (date or number) specified in the contact list or API payload.
   - **Custom priority descending**: Processes records in descending order based on the priority attribute.
      When custom priority is used, if a runtime misconfiguration is detected - such as missing or invalid priority data - the system falls back to first in, first out processing of the misconfigured records.

1. For Copilot dial mode, configure the **Call settings**:
   - Select the **Max number of concurrent calls for Copilot Mode** that refers to the maximum number of calls the AI agent can make concurrently. The maximum number that you can specify is 500.
   - Under **Operating hours**, select the checkbox if calls can be made outside of queue hours. This setting is available for Copilot dial mode only.
   - Select the action for how the call needs to be handled if the AI agent fails during the call.
      - **Stop making calls immediately**: No further calls are made.
      - **Continue making calls**:
         - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.

1. For preview dial mode, configure the **Call settings**:
   - **Automatic**: The system initiates the call after a countdown timer expires. The timer starts when a representative accepts the invite. Specify the duration in seconds for the timer. Service representatives can start the call early or cancel it before the timer expires.
   - **Manual**: The service representative must manually start the call after reviewing customer details.
       > [!NOTE]
       > Timer and delayed start are available on Teams Phone Extensibility only. If you're using Azure Communication Services, preview calls start automatically after the representative accepts the invite.

1. For AI agent-led predictive dial mode, configure the **Call settings**:
   - Select the action for how the call needs to be handled if the AI agent fails during the call.
      - **Stop making calls immediately**: No further calls are made.
      - **Continue making calls**:
        - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.

1. For AI agent-led progressive dial mode, configure the **Call settings**:
   - Select the max number of calls that can be assigned to the representative in **Maximum calls per representative**. This setting is available for the progressive dial mode. A lower number indicates a balanced call volume for the representative. You can specify up to five calls.
   - Select the action for how the call needs to be handled if the AI agent fails during the call.
      - **Stop making calls immediately**: No further calls are made.
      - **Continue making calls**:
        - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.
        > [!NOTE]
        > For AI agent-led engagements, answering machine detection is configured in the Copilot IVR agents.

1. For representative-led progressive and predictive dial modes,
   - Select the action if answering machine is detected.
     - **End call immediately** ends the call if a voicemail or answering machine is detected.
     - **Leave a voicemail** plays the text in **Voicemail prompt** at the appropriate time, at the end of the greeting.
         - **Call is abandoned after**: Enter the duration after which a call is considered abandoned if no service representative connects after the customer answers.
         - **Abandoned message**: Enter the message that plays to the customer waiting on line if the call is abandoned before the call ends.
       > [!IMPORTANT]
       > The call connection time for service representative-led progressive and predictive dial modes isn't compliant with the Telephone Consumer Protection Act (TCPA). Review applicable telecommunications regulations before using service representative-led modes.

1. For AI agent-led engagements, select **Use rules** to set rules for the following parameters that help control the throttling and pacing for the proactive engagement:
   - **Abandonment rate**: (Copilot, progressive, and predictive modes). The percentage of customers who hang up before connecting with a representative.
   - **Average wait time**: (Copilot, progressive, and predictive modes). The average amount of time it takes for customers to connect to representatives.
   - **Escalation count**: (Copilot mode). The total number of escalations made from the AI agent.
   - **Open concurrent escalations**: (Copilot mode). The total number of open escalations that aren't resolved.
   - **Percentage of queue**: (Predictive mode) To balance queue capacity, set how much percent of the queue you want dedicated to the proactive engagement.

1. For representative-led progressive and predictive dial modes, select **Use rules** to set rules for the following parameters that help control the throttling and pacing for the proactive engagement:
   - **Abandonment rate**: The maximum percentage of customers who don't get connected to a representative before the threshold mentioned in the duration. The proactive engagement pauses if the threshold is reached and requires manual intervention to restart the proactive engagement.
   - **Percentage of queue**: To balance queue capacity, set the percent of the queue you want dedicated to the proactive engagement.

1. Select **Next**.

**Display number configuration**

On **Display number configuration**, choose the phone numbers to use for outbound calls.

1. The **Workstream number** is the default display number and you can't change it for the engagement.

1. In **Display numbers**, select one or more phone numbers to use as display numbers. You can't use shared numbers for existing workstreams as display numbers.

   > [!NOTE]
   > Calls originate from the display number.
   > Display numbers must match the number type of the workstream number. For example, if the workstream uses Azure Communication Services Direct Routing numbers, display numbers must also be Azure Communication Services Direct Routing numbers.
      > You can use numbers that aren't used in an outbound workstream.
   > You configure multiple display numbers at the engagement level only. You can't add multiple display numbers on the workstream itself.

1. Under **Distribution**, choose how the system selects the number to use for each call:

   - **Automated**: The system rotates through display numbers by using pseudo-random selection, ensuring equal distribution across all configured numbers. You can't control a specific number to be used for a specific call.
   - **Rule-based**: Create custom rules to distribute calls based on contact attributes. Specify up to five rules by using the following fields:
     - **Field**: The contact attribute to match on, such as State, City, or Zip code.
     - **Condition**: The matching condition, such as **Starts with**.
     - **Value**: The value to match.
     - **Display number**: The number to use when the rule matches.

1. Select **Next**.

**Reattempts**

On the **Reattempts** page, configure retry behavior for contacts who aren't reached on the first attempt.

1. Under **Abandonment reasons**, select the call outcomes that trigger a reattempt:

   - **No answer**
   - **Busy**
   - **Failed**
   - **Answering Machine**

   This list of systemic outcomes is fixed. You can't add custom values to it.

1. In **Disposition codes**, select any disposition codes that trigger a reattempt. These codes represent business outcomes that service representatives set during or after a call. To make a code available for reattempt selection, create it under the category **Not right party**. The same disposition codes also appear on the representative's screen during the call. Learn more in [Configure disposition codes](configure-disposition-codes.md).

1. Under **Retry settings**, specify **Number of attempts**, **Wait time**, and one of the following **Priority** values:
   - Same as new deliveries
   - Higher than new deliveries
   - Lower than new deliveries

1. Under **Follow up on SMS**, optionally select an SMS proactive engagement configuration to use when all retry attempts are exhausted.
Select **None** if no fallback is needed.

   > [!NOTE]
   > SMS fallback is currently in preview and requires opting in to the preview.

1. Select **Next**.

**Frequency limits**

On the **Frequency limits** page, set how often you can reach contacts and during which hours.

1. Select **Use frequency limits** to turn on frequency controls, and then enter values for:
   - **Maximum engagements per day**: The maximum number of times you can reach a contact in a day across all channels.
   - **Maximum engagements per week**: The maximum number of times you can reach a contact in a week across all channels.

1. Under **Schedule**, select at least one phone number type and set quiet hours for each:
   - **Mobile Phone**
   - **Business Phone**
   - **Home Phone**

   If you select more than one number type, set the preferred contact order by using the arrows to move the phone numbers up or down. The system respects the quiet hours you set for each number type and doesn't place calls during those windows. You must set quiet hours for every phone number type you select before you can proceed.

1. Under **Time zones**, select how to determine the time zone for each contact:
   - **Use customer's local time zone when available (defaults to UTC if not available)**: The system uses the time zone attribute on each contact record to evaluate quiet hours in that contact's local time. If no time zone is specified on the contact, UTC is used. You must explicitly provide the time zone value in the uploaded file or API payload - the system doesn't auto-detect or geo-infer time zones.
   - **Use Coordinated Universal Time (UTC)**: The system evaluates all contacts against quiet hours by using UTC, regardless of their location.

1. Select **Next**.

**Summary**

Review all settings on the **Summary** page, and select **Create**.

[!INCLUDE [proactive-file-upload](../includes/proactive/cc-proactive-file-upload.md)]

Learn more about available outcomes and SIP-based result values in [Outcomes for proactive engagement](proactive-engagement-outcomes.md).

### [SMS](#tab/sms)

[!INCLUDE [proactive-audience](../includes/proactive/cc-proactive-audience.md)]
[!INCLUDE [proactive-details](../includes/proactive/cc-proactive-details.md)]

**Preferences**

On the **Preferences** page, configure channel behaviors and throttling rules for the SMS engagement.

1. Under **Channel behaviors**, configure the following:

   - **First response timeout**: Set the duration (in minutes, hours, or days) the system waits for a customer to respond to the initial SMS before the request expires. If the recipient doesn't respond within the timeout period, the request expires and any later reply is treated as a new anonymous inbound conversation, losing the context. The default is 5 minutes.
   - **Priority level**: Select the priority for the engagement — **Normal**, **High**, or **Critical**. Priority determines which proactive engagement is processed first when multiple engagements compete for the same queue and skillset.
   - **Message order**: Select how messages within the engagement are processed:
     - **Earliest Scheduled Date**: Processes records that are close to the end of the messaging window first.
     - **Last in First Out**: Processes the most recent records first.
     - **First in, First Out**: Processes older records first.
     - **Custom priority ascending**: Processes records in ascending order based on a priority attribute specified in the contact list or API payload.
     - **Custom priority descending**: Processes records in descending order based on the priority attribute.

1. Under **Rules**, select **Use rules** to set throttling and pacing rules for the engagement. Configure conditions based on the following parameters:

   - **Average wait time**: The average amount of time it takes for customers to connect to representatives.
   - **Escalation count**: The total number of escalations made from the AI agent.
   - **Open concurrent escalations**: The total number of open escalations that haven't been resolved.

   For each rule, specify the threshold value, the time window (**In the last**), and the **Decrease concurrent calls by** percentage to control pacing when the condition is met.

1. Select **Next**.

**SMS template configuration**

On the **SMS template configuration** page, create and customize the SMS message template for this engagement.

1. Under **Templates**, turn on **Enable message templates for this workflow**. This setting is turned on by default if you select **Upload a file** as the intake method. For **CCaaS API** and **MCP**, this is optional&mdash;the message content can be included directly in the payload instead.

1. In the **Message** field, compose the SMS message to send to customers. Use the personalization menu to insert dynamic fields from the contact record, including:
   - **First Name**
   - **Last Name**
   - **Phone Number**
   - **Email**
   - **Postal Code**
   - **Country**
   - **City**
   - **Street**

   The **Preview** pane on the right shows a directional rendering of the message as it would appear on a mobile device. Actual renditions might vary.

   > [!NOTE]
   > The message field supports up to 1000 characters.

1. Select **Next**.

**Frequency limits**

On the **Frequency limits** page, configure how often contacts can be reached and during which hours.

1. Select **Use frequency limits** to enable frequency controls, and then specify:
   - **Maximum engagements per day**: The maximum number of times a contact can be reached in a day across all channels.
   - **Maximum engagements per week**: The maximum number of times a contact can be reached in a week across all channels.

1. Under **Schedule**, select at least one phone number type and set quiet hours for each:
   - **Mobile Phone**
   - **Business Phone**
   - **Home Phone**

   If you select more than one number type, set the preferred contact order by dragging the rows. The system respects the quiet hours configured for each number type and won't send messages during those windows. You must configure quiet hours for every phone number type you select before you can proceed.

1. Under **Time zones**, select how to determine the time zone for each contact.
   - **Use customer's local time zone when available (defaults to UTC if not available)**: The system uses the time zone attribute on each contact record to evaluate quiet hours in that contact's local time. If no time zone is specified on the contact, UTC is used. The time zone value must be explicitly provided in the uploaded file or API payload—the system does not auto-detect or geo-infer time zones.
   - **Use Coordinated Universal Time (UTC)**: All contacts are evaluated against quiet hours using UTC, regardless of their location.

1. Select **Next**.

**Summary**

Review all settings on the **Summary** page, and select **Create**.

[!INCLUDE [proactive-file-upload](../includes/proactive/cc-proactive-file-upload.md)]

---

## Manage proactive engagements

### Configure multiparty (account) engagements

Contact chaining lets you group related contacts, such as members of the same household or account, and treat them as a single unit for engagement purposes.

- You can group up to five contacts when you are uploading a file or submitting requests through the API.
- All contacts in the chain are considered for every attempt. The system dials contacts in the order they appear in the file or API array.
- If all phone numbers across all chained contacts are exhausted on an attempt, the system waits for the configured retry interval before starting the next attempt and cycles through all contacts again.

### Configure call cancellation and suppression

You can cancel pending calls and optionally suppress future calls that match defined criteria.

1. In the site map, select **Productivity** under **Support experience**, and select **Manage** for **Proactive engagements**.

1. Select **Go to settings**, and then select **Add a cancellation policy**.

1. Specify filter criteria using any combination of the following in AND conditions:
   - Proactive engagement configuration ID
   - Country/Region
   - State
   - Postal code

1. Optionally, specify an end date in **Execute policy until**. Contacts matching the criteria won't be processed for new calls during the specified period.
1. Optionally, enter a **Comment**. Cancelled calls are marked in the delivery tables with a reference to the cancellation policy to enable reporting.

> [!NOTE]
> Cancellation applies to queued calls only. You can also trigger cancellation and suppression through the CCaaS API. Learn more in [Use CCaaS_CreateProactiveVoiceDelivery API](../extend/api/ccaas_createproactivevoicedelivery.md).

### Related information

[Overview of proactive engagement](overview-proactive-engagement.md)  
[Dial modes for proactive engagement](proactive-engagement-dial-modes.md)  
[Outcomes for proactive engagement](proactive-engagement-outcomes.md)  
[Best practices for proactive engagement campaigns](proactive-engagement-best-practices.md)  
[How proactive engagement works](../use/how-proactive-engagement-works.md)  
[Overview of conversational journeys](/dynamics365/customer-insights/journeys/conversational-journeys-overview)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
[Use CCaaS_CreateProactiveVoiceDelivery API](../extend/api/ccaas_createproactivevoicedelivery.md)  
[Use CCaaS_CreateOperation API](../extend/api/ccaas_createoperation.md)  
[Use CCaaS_CreateProactiveDelivery API](../extend/api/ccaas_createproactivedelivery.md)  
[Proactive Outbound dashboard](../use/proactive-outbound-dashboard.md#proactive-outbound-dashboard)
