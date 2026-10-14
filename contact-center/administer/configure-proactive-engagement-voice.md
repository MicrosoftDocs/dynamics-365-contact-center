---
title: Configure proactive engagement for voice
description: Configure proactive voice engagements in Dynamics 365 Contact Center, including outbound workstreams, dial modes, reattempts, and call management.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 10/14/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Configure proactive engagement for voice

This article describes how to configure proactive voice engagements led by service representatives or AI agents. Set up the voice workstream, configure the engagement, and manage voice-specific settings.

## Prerequisites

- Review the shared prerequisites, consent responsibilities, and audience options in [Set up proactive engagement](configure-proactive-engagement.md).
- Voice channel is provisioned and configured. Learn more in [Provision channels](../implement/provision-channels.md) and [Install the voice channel](/dynamics365/customer-service/administer/voice-channel-install?context=/dynamics365/contact-center/context/administer-context).

### Requirements for direct routing

- If you use direct routing, review the following requirements for representative-led progressive and predictive dial modes. These requirements ensure that the Session Border Controller (SBC) can handle the call-transfer scenarios that progressive and predictive dialing rely on.
  - Ensure that the SBC supports RFC 3891 `Replaces` headers, including INVITE messages with the `Require: replaces` and `Replaces` headers. This capability is essential for the mid-call transfer flows used in progressive and predictive dial modes.
  - Ensure that the SBC supports RFC 3325 handling for `P-Asserted-Identity` with Privacy ID and other applicable direct routing SIP requirements.
  - Include all supported root certificate authorities (CAs) for Teams SIP interface certificates in the SBC trust store. Teams SIP interface client and server certificates can chain to any one of the supported root CAs, so the SBC trust store must include all supported roots.
  - For Oracle SBC deployments, `Replaces` support depends on the `sip-profile` configuration. Configure Replaces header support by applying a SIP profile to a session agent, realm, or SIP interface. The `replace-dialogs` parameter controls this feature.

   Use the following Oracle-documented ACLI sequence to configure the core parameter:

    ```text
    configure terminal
    session-router
    sip-profile
      replace-dialogs enabled
    done
    ```

    Bind the SIP profile to the session agent, realm, or SIP interface used for the Microsoft-facing leg based on your deployment topology and software version. If the endpoints in the `Replaces` scenario are in the same realm, enable `mm-in-realm` in `realm-config`.
  
> [!NOTE]
> - After you enable `replace-dialogs`, bind the SIP profile to the session agent, realm, or SIP interface used for the Microsoft-facing leg, based on your deployment topology and software version.
> - If the endpoints in the Replaces scenario are in the same realm, enable `mm-in-realm` in `realm-config`. Otherwise, the SBC can't generate the SDP for the 200 OK, and the call fails.

## Set up an outbound workstream

1. Create a workstream by selecting the **Outbound** option. Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context).

1. In the **Setup Behaviors** section of the workstream, select **Setup**.

1. On the **Phone number** page, select a number in the **Shared numbers** list. You can use a number configured for an outbound profile (for representative dialing in Copilot Service workspace) or outbound workstream only. Learn more in [Configure phone numbers for outbound calling](/dynamics365/customer-service/administer/voice-channel-outbound-calling#configure-phone-numbers-for-outbound-calling).
   
   > [!NOTE]
   > Azure Communication Services supports Direct Routing numbers only. Teams Phone supports Direct Routing, Direct Offer, and Operator Connect numbers.

1. Set up the language and outbound behaviors. Learn more in [Configure the voice channel](/dynamics365/customer-service/administer/voice-channel-inbound-calling?tabs=enhancedvoice#configure-a-voice-channel).
1. Configure [work distribution](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution). Optionally add an [AI agent](/dynamics365/customer-service/administer/create-workstreams#add-an-agent-to-a-workstream) to the workstream, and configure representative notifications. The following notification templates are available out of the box:
    - **Voice call - outbound agent dial - default**: For preview dial mode calls
    - **Voice call - outbound pre-dial - default**: For predictive, progressive, and Copilot dial mode calls

The system automatically configures the routing rules based on the proactive engagement settings. These rules appear under the **Auto generated rules (advanced)** section of the workstream.

## Create a voice proactive engagement

[!INCLUDE [proactive-setup](../includes/proactive/cc-proactive-setup.md)]

The **Create new proactive engagement** wizard guides you through the steps outlined in the following sections:

- Audience
- Details
- Dialing modes 
- Display number configuration 
- Reattempts 
- Frequency limits
- Summary

> [!NOTE]
> Delivery windows and expiration dates can't extend more than 30 days into the future. If a request or uploaded record doesn't specify a delivery window, the system uses a 24-hour window that starts immediately, or at the requested earliest schedule date when that date is in the future.

## Audience

[!INCLUDE [proactive-audience](../includes/proactive/cc-proactive-audience.md)]

2. Under **Engagement type**, select one of the options to determine how the call is handled:

      - **Led by representatives**: Always connect customers to service representatives.
      - **Led by AI**: Let Copilot interact with customers first as they answer the calls, then add representatives at the right moment.

   > [!NOTE]
   > A single workstream can run both AI-led and representative-led proactive engagements simultaneously.

3. Select **Next**.

## Details

[!INCLUDE [proactive-details](../includes/proactive/cc-proactive-details.md)]

## Dialing modes

The dial modes determine how the system places outbound calls to customers. Learn more in [Dial modes for proactive engagement](proactive-engagement-dial-modes.md).

1. Select one of the following dial modes:
   - **Copilot**: Applies to AI agent-led engagements. The system automatically dials the customer and connects the call to the AI agent when the customer answers. Use this mode for high-volume outbound calls.
   - **Preview**: Applies to representative-led engagements. The system notifies a service representative of the outbound call request and after acceptance, places the call to the customer.
   - **Progressive**: Applies to both representative- and AI agent-led engagements. The system starts calls equal to the number of available representatives, and on customer answer adds a representative or AI agent based on the engagement type. If type is representative led, service representatives are reserved ahead of time for a good customer experience.
   - **Predictive**: The system starts calls proportional to the number of available representatives, and on customer answer adds a representative or AI agent based on the engagement type. A predictive model considers factors like representative availability, abandonment rate, and answer rate to determine the number of calls to initiate per representative. If type is representative led, representatives are reserved ahead of time to ensure a good customer experience.

1. Priority determines the processing order of the proactive engagement. Select one of the following priority levels:
   - **Normal**
   - **High**
   - **Critical**
   
     Priority also determines the processing order when multiple proactive engagements compete for the same representatives (same queue and skill set). Higher-priority engagements are processed first. For example, if a critical and a normal proactive engagement both target the same queue, the system processes the critical engagement first and handles the normal engagement only when no higher-priority requests are pending.
     
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

   - **Skip CSR availability checks**: Select this option if you want preview calls to be added to the routing backlog irrespective of representative availability. By default, proactive engagement queues preview calls proportional to the number of available representatives, accounting for calls that are already in waiting. If selected, specify a **Maximum number of conversations in waiting** value. You can specify up to 50.

1. For AI agent-led predictive dial mode, configure the **Call settings**:
   - Select the action for how the call needs to be handled if the AI agent fails during the call.
      - **Stop making calls immediately**: No further calls are made.
      - **Continue making calls**:
        - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.

1. For AI agent-led progressive dial mode, configure the **Call settings**:
   - Select the max number of calls that you can assign to the representative in **Maximum calls per representative**. This setting is available for the progressive dial mode. A lower number indicates a balanced call volume for the representative. You can specify up to five calls.
   - Select the action for how the call needs to be handled if the AI agent fails during the call.
      - **Stop making calls immediately**: No further calls are made.
      - **Continue making calls**:
        - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.
        > [!NOTE]
        > For AI agent-led engagements, configure answering machine detection in the Copilot IVR agents.

1. For representative-led progressive and predictive dial modes, select the action if the system detects an answering machine.
     - **End call immediately** ends the call if the system detects a voicemail or answering machine.
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

## Display number configuration

On **Display number configuration**, choose the phone numbers to use for outbound calls.

1. The **Workstream number** is the default display number and you can't change it for the engagement.

1. In **Display numbers**, select one or more phone numbers to use as display numbers. You can't use shared numbers for existing workstreams as display numbers.

   > [!NOTE]
   > Calls originate from the display number.
   > Display numbers must match the number type of the workstream number. For example, if the workstream uses Azure Communication Services Direct Routing numbers, display numbers must also be Azure Communication Services Direct Routing numbers.
   > You can use numbers that aren't used in an outbound workstream.
   > You configure multiple display numbers at the engagement level only. You can't add multiple display numbers on the workstream itself.

1. Under **Distribution**, choose how the system selects the number to use for each call:

   - **Automated**: The system rotates through display numbers by using pseudo-random selection, ensuring equal distribution across all configured numbers. You can't control a specific number to use for a specific call.
   - **Rule-based**: Create custom rules to distribute calls based on contact attributes. Specify up to five rules by using the following fields:
     - **Field**: The contact attribute to match on, such as State, City, or Zip code.
     - **Condition**: The matching condition, such as **Starts with**.
     - **Value**: The value to match.
     - **Display number**: The number to use when the rule matches.

1. Select **Next**.

## Reattempts

On the **Retry attempts** page, configure retry behavior for contacts you don't reach on the first attempt.

1. Under **Abandonment reasons**, select the call outcomes that trigger a retry attempt:

   - **No answer**
   - **Busy**
   - **Failed**
   - **Answering Machine**

   This list of systemic outcomes is fixed. You can't add custom values to it.

1. In **Disposition codes**, select any disposition codes that trigger a retry attempt. These codes represent business outcomes that service representatives set during or after a call. To make a code available for retry selection, create it under the category **Not right party**. The same disposition codes also appear on the representative's screen during the call. Learn more in [Configure disposition codes](configure-disposition-codes.md).

1. Under **Retry settings**, specify **Number of attempts**, **Wait time**, and one of the following **Priority** values:
   - Same as new deliveries
   - Higher than new deliveries
   - Lower than new deliveries

   You can configure up to 10 attempts. The wait time between attempts must be from 5 minutes through 48 hours.

1. Under **Follow up on SMS**, optionally select an SMS proactive engagement configuration to use when all retry attempts are exhausted.
   Select **None** if no fallback is needed.

   > [!NOTE]
   > SMS fallback is currently in preview and requires opting in to the preview.

1. Select **Next**.

## Frequency limits
[!INCLUDE [proactive-frequency-limits](../includes/proactive/cc-proactive-frequency-limits.md)]

## Summary

Review all settings on the **Summary** page, and select **Create**.
## File upload
[!INCLUDE [proactive-file-upload](../includes/proactive/cc-proactive-file-upload.md)]

Learn more about available outcomes and SIP-based result values in [Outcomes for proactive engagement](proactive-engagement-outcomes.md).

## Manage proactive engagements

The following management options apply to voice proactive engagements.

### Configure multiparty (account) engagements

Contact chaining lets you group related contacts, such as members of the same household or account, and treat them as a single unit for a voice engagement. Contact chaining isn't supported for messaging engagements.

- You can group up to five contacts when you upload a file or submit requests through the API.
- Consider all contacts in the chain for every attempt. The default phone type priority is **Mobile**, **Business**, and then **Home**. Skip phone types that don't contain a number.
- Use **Engagement sequence** in the retry settings to select how the system traverses the chain:
   - **Contact first** (default): Tries each contact's numbers in phone type priority order before moving to the next contact in the file or API array.
   - **Phone type first**: Tries the highest-priority phone type for every contact before moving to the next phone type.
- One pass can include up to 15 dials: five contacts multiplied by three phone number types.
- Configure a delay from 5 through 60 minutes between phone number types and a delay from 5 through 240 minutes between contacts. The delays apply to the corresponding transition in either engagement sequence.
- If all phone numbers across all chained contacts are exhausted on an attempt, the system waits for the configured retry interval before starting the next attempt and cycles through all contacts again.

### Configure voice call cancellation and suppression

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
> Cancellation applies to queued calls only. To cancel an individual delivery through the CCaaS API, use `CCaaS_CreateOperation` with the `Cancel` operation and the delivery ID. To cancel all pending and future attempts in a contact chain, use `CCaaS_CancelDeliveryTask` with the delivery task ID. Learn more in [Use CCaaS_CreateOperation API](../extend/api/ccaas_createoperation.md).



## Related information

[Set up proactive engagement](configure-proactive-engagement.md)  
[Configure proactive engagement for messaging](configure-proactive-engagement-messaging.md)  
[Overview of proactive engagement](overview-proactive-engagement.md)  
[Dial modes for proactive engagement](proactive-engagement-dial-modes.md)  
[Manage consent for proactive engagement](proactive-engagement-manage-consent.md)  
[Outcomes for proactive engagement](proactive-engagement-outcomes.md)  
[Best practices for proactive engagement campaigns](proactive-engagement-best-practices.md)  
[How proactive engagement works](../use/how-proactive-engagement-works.md)  
[Overview of conversational journeys](/dynamics365/customer-insights/journeys/conversational-journeys-overview)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
[Use CCaaS_CreateProactiveVoiceDelivery API](../extend/api/ccaas_createproactivevoicedelivery.md)  
[Use CCaaS_CreateOperation API](../extend/api/ccaas_createoperation.md)  
[Use CCaaS_CreateProactiveDelivery API](../extend/api/ccaas_createproactivedelivery.md)  
[Proactive Outbound dashboard](../use/proactive-outbound-dashboard.md#proactive-outbound-dashboard)
