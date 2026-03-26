---
title: Configure proactive engagement
description: Learn how to set up proactive engagement, including dial modes and operational rules for optimized customer service in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 03/31/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Configure proactive engagement

Proactive engagement in Dynamics 365 enables organizations to enhance customer interactions by initiating outbound communications through the voice channel. This feature allows businesses to streamline customer outreach, improve agent productivity, and deliver personalized experiences. The article describes how to configure proactive engagement settings, including dialing modes, routing details, and operational rules to optimize your customer service operations.

## Prerequisites

- Voice channel is provisioned and configured. Learn more in [Provision channels](../implement/provision-channels.md) and [Install the voice channel](/dynamics365/customer-service/administer/voice-channel-install?context=/dynamics365/contact-center/context/administer-context).
- Dynamics 365 Customer Insights if you want to use journey for your customer journey authoring.
- Microsoft Copilot Studio to use Copilot agents.

## Set up an outbound workstream

1. Create a workstream by selecting the **Outbound** option. Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context).
2. Set up the outbound workstream behaviors in the **Setup Behaviors** section of the workstream as follows:

    - Select **Setup**, and on the page that appears, select the **Caller ID Number** in the list. Numbers available to use only are displayed. Learn more in [Configure phone numbers for outbound calling](/dynamics365/customer-service/administer/voice-channel-outbound-calling#configure-phone-numbers-for-outbound-calling).
    - Select a number in the **Shared numbers** list. A number can only be used either of an outbound profile (for representative dialing in Copilot service workspace) or outbound workstream.
3. Set up the language and outbound behaviors. Learn more in [Configure the voice channel](/dynamics365/customer-service/administer/voice-channel-inbound-calling?tabs=enhancedvoice#configure-a-voice-channel)
4. Configure [work distribution](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution), add optionally add an [AI agent](/dynamics365/customer-service/administer/create-workstreams#add-an-agent-to-a-workstream) to the workstream, and configure representative notifications. The following notification templates are available out of the box:
    - **Voice call - outbound agent dial - default**: For preview dial mode calls
    - **Voice call - outbound pre-dial - default**: For predictive, progressive and copilot dial mode calls

> [!NOTE]
>
> - With Azure Communication Services, you can use Direct Routing numbers only. With Teams Phone numbers, you can use Direct Routing, Direct Offer, and Operator Connect numbers.
> - The routing rules are automatically configured based on the proactive engagement settings and appear under the **Auto generated rules (advanced)** section of the workstream.

## Configure settings to engage proactively with customers

1. In the site map of Copilot Service admin center, navigate to the settings in one of the following ways and then create a proactive engagement setting.

   - Select **Productivity** under **Support experience**. Select **Manage** for **Proactive engagements**, and then select **New**.
   - Select **Workstreams** under **Customer support**, select an outbound workstream for voice, and on the workstream page, select **New proactive engagement**.

   The **Create new proactive engagement** wizard guides you through the steps outlined in the following sections:
   - **Audience**
   - **Details**
   - **Dialing modes**
   - **Display number configuration**
   - **Reattempts**
   - **Frequency limits**
   - **Summary**

### Audience

On the **Audience** page, configure how customers are sourced and how the engagement is led.

1. Under **Select your audience**, choose how customer contact information is provided:

   - **Contact Center**: If you select this option, choose one of the following intake methods:
     - **Upload a file**
     - **CCaaS API**
     - **MCP** (preview)
   - **Conversational Journeys in Customer Insights**: This option is available only if Customer Insights is enabled. Select if you want to create conversation journeys in Customer Insights.

1. Under **Engagement type**, select one of the options to determine how the call is handled:

   - **Led by AI**: Let Copilot interact with customers first as they answer the calls, then add representatives at the right moment.
   - **Led by representatives**: Always connect customers to service representatives.

   > [!NOTE]
   > A single workstream can run both AI-led and representative-led proactive engagements simultaneously.

1. Select **Next**.

### Details

On the **Details** page, configure the engagement identity, routing, and business unit.

1. In **Engagement details**, enter the following:
   - **Name**: A name for the proactive engagement. Name is natively shown to service representative on the conversation form.
   - **Description**: A description that helps service representatives understand the purpose of the call. The name and description are visible to representatives during the call.
   - **Workstream**: Select the outbbound workstream. If you are creating the proactive engagement from within an workstream, this is preselected.
   - **Channel type**: The channel used for the proactive engagement.

1. Under **Contact unique identifier**, select the contact attribute to use as the unique identifier. The dropdown lists only those attributes that are marked as unique key eligible on the Contact table. The default is **contactid**.

   The system performs an upsert using this identifier; if an incoming record matches an existing contact, the record is updated; otherwise, a new contact is created. Select the correct identifier to prevent duplicate contact records from being created.

   - If Dynamics 365 is your system of record, use **contactid** (the Dynamics contact GUID).
   - If you use an external system such as a CRM or MDM, create a custom attribute on the Contact table to store your external identifier, and then select the custom attribute. By passing your external system's ID in the input you can make sure duplicates aren't created, and the data in the contact center stays updated.

1. In **Routing details**, enter the following details:
   - **Primary queue**: Select a queue.
   - **Fallback queue**: The system populates the queue name based on the fallback queue set for the outbound workstream.
   - **Skills**: Select the skills required for the proactive engagement.

1. The **Business unit** field is automatically set to the business unit of the user creating the engagement. The **Assigned to** field shows the owner that you can change if needed.

1. Select **Next**.

### Dialing modes

The dial modes determine how the system places outbound calls to customers. Learn more in [Dial modes for proactive engagement](dial-modes-proactive-engagement.md).

1. Select one of the following dial modes:
   - **Copilot**: Applies to AI agent led engagements. The system automatically dials the customer and connects the call to the AI agent when the customer answers. This mode is used for high-volume outbound calls.
   - **Preview**: Applies to both representative and AI agent led engagements. The system notifies a service representative of the outbound call request and, after acceptance, places the call to the customer.
   - **Progressive**: The system starts calls equal to the number of available agents, and on customer answer adds a representative or AI agent based on the engagement type. If type is representative led, service representatives are reserved ahead of time to make sure a good customer experience.
   - **Predictive**: The system starts calls proportional to the number of available agents, and on customer answer adds a representative or AI agent based on the engagement type. A predictive model considers factors like agent availability, abandoned rate, and answer rate to determine the number of calls to initiate per representative. If type is representative led, representatives are reserved ahead of time to ensure a good customer experience.

1. Priority determines the processing order of the proactive engagement. Select one of the following priority levels:
   - **Normal**
   - **High**
   - **Critical**
   
     Priority is used to determine which proactive engagement gets priority if two or more are looking for the same representatives (same queue and skill set). If a critical proactive engagement and a normal one are configured to use representatives from the same queue, the critical one is processed first and when there are no pending requests, requests of the normal proactive engagement are processed.
     
     If two proactive engagements of same priority are looking for representatives in the same queue, they are processed in a round robin manner ensuring fair processing.

1. Processing order defines how requests within each proactive engagement are processed. In **Call order**, select one of the following options:
   - **Earliest Scheduled Date** - Processes records that are close to end of calling window first.
   - **Last in First Out** - Processes most recent records first, in a last in first out manner.
   - **First in, First Out** - Processes older records first, in a first in first out manner.
   - **Custom priority ascending**: Processes records in ascending order based on a priority attribute (date or number) specified in the contact list or API payload.
   - **Custom priority descending**: Processes records in descending order based on the priority attribute.
      When custom priority is used, if a runtime misconfiguration is detected—such as missing or invalid priority data—the system falls back to first in, first out processing of the misconfigured records.

1. For the copilot dial mode, configure the **Call start settings**:
   - Select the **Max number of concurrent calls for Copilot Mode** that refers to the maximum number of calls the AI agent can make concurrently. The maximum number that you can specify is 500.
   - Under **Operating hours**, select the checkbox if calls can be made outside of queue hours. This setting is available for Copilot dial mode only.
   - Select the action for how the call needs to be handled if the AI agent fails during the call.
      - **Stop making calls immediately**: No further calls are made.
      - **Continue making calls**:
         - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.

1. For the preview dial mode, configure the **Call start settings**:
   - **Automatic**: The system initiates the call after a countdown timer expires. The time starts from the time a CSR accepts the invite. Specify the duration in seconds for the timer. Service representatives can start the call early or cancel it before the timer expires.
   - **Manual**: The service representative must manually start the call after reviewing customer details.
       > [!NOTE]
       > Timer and delayed start functionality is available on Teams Phone Extensibility only. If you are using Azure Communication Services, preview calls start automatically after the representative accepts the invite.

1. For AI agent-led predictive dial mode, configure the **Call start settings**:
   - Select the action for how the call needs to be handled if the AI agent fails during the call.
      - **Stop making calls immediately**: No further calls are made.
      - **Continue making calls**:
        - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.

1. For AI agent-led progressive dial mode, configure the **Call start settings**:
   - Select the max number of calls that can be assigned to the representative in **Maximum calls per representative**. This setting is available for the progressive dial mode. A lower number indicates a balanced call volume for the representative. You can specify up to five calls.
   - Select the action for how the call needs to be handled if the AI agent fails during the call.
      - **Stop making calls immediately**: No further calls are made.
      - **Continue making calls**:
        - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.
        > [!NOTE]
        > For AI agent led engagements, answering machine detection is configured in the Copilot IVR agents.

1. For representative-led progressive and predictive dial modes,
   - Select the action if answering machine is detected
     - **End call immediately** ends the call if a voicemail or answering machine is detected
     - **Leave a voicemail** plays the text in the Voicemail Prompt at the appropriate time, at the end of the greeting.
         - **Call is abandoned after**: Specify the duration after which a call is considered abandoned if no service representative is connected after the customer answers.
         - **abandoned message**: Specify the message that needs to be played to the customer waiting on line if the calls is abandoned before the call ends.
       > [!IMPORTANT]
       > The call connection time for service representative-led progressive and predictive dial modes isn't compliant with the Telephone Consumer Protection Act (TCPA). Review applicable telecommunications regulations before using service representative-led modes.

1. For AI agent led engagements select **Use rules** to set rules for the following parameters that help control the throttling and pacing for the proactive engagement:
   - **Abandonment rate**: (Copilot, progressive, and predictive modes). The percentage of customers who hang up before connecting with a representative.
   - **Average wait time**: (Copilot, progressive, and predictive modes). The average amount of time it takes for customers to connect to representatives.
   - **Escalation count**: (Copilot mode). The total number of escalations made from the AI agent.
   - **Open concurrent escalations**: (Copilot mode). The total number of open escalations that haven't been resolved.
   - **Percentage of queue**: (Predictive mode) To balance queue capacity, you can set how much percent of the queue you want dedicated to the proactive engagement.

   For representative led progressive and predictive dial modes select **Use rules** to set rules for the following parameters that help control the throttling and pacing for the proactive engagement: 
      - **Abandonment rate**: The maximum percentage of customers who couldn't get connected to a CSR before the threshold specified in the the specified duration. The proactive engagement is paused if the threshold is reached and will require manual intervention to restart the proactive engagemnt.
      - **Percentage of queue**: To balance queue capacity, you can set how much percent of the queue you want dedicated to the proactive engagement.

1. Select **Next**.

### Display number configuration

On the **Display number configuration** page, choose the phone numbers to use for outbound calls.

1. The **Workstream number** is the default display number and can't be changed for the engagement.

1. In **Display numbers**, select one or more additional phone numbers to use as display numbers. Shared numbers for existing workstreams can't be used as display numbers.

   > [!NOTE]
   > Calls are originated from the display number.
   > Display numbers must match the number type of the workstream number. For example, if the workstream uses Azure Communication Services Direct Routing numbers, display numbers must also be Azure Communication Services Direct Routing numbers.
   > Numbers that aren't used in an outbound workstream only are available to use as display number.
   > Multiple display numbers are configured at the engagement level only. You can't add multiple display numbers on the workstream itself.

1. Under **Distribution**, choose how the system selects the number to use for each call:

   - **Automated**: The system rotates through display numbers using pseudo-random selection, ensuring equal distribution across all configured numbers. You can't control a specific number to be used for a specific call.
   - **Rule-based**: Create custom rules to distribute calls based on contact attributes. Specify up to five rules using the following fields:
     - **Field**: The contact attribute to match on, such as State, City, or Zip code.
     - **Condition**: The matching condition, such as **Starts with**.
     - **Value**: The value to match.
     - **Display number**: The number to use when the rule matches.

1. Select **Next**.

### Reattempts

On the **Reattempts** page, configure retry behavior for contacts who couldn't be reached on the first attempt.

1. Under **Reattempt reasons**, select the call outcomes that should trigger a reattempt:

   - **No answer**
   - **Busy**
   - **Failed**
   - **Answering Machine**

   This list of systemic outcomes is fixed. You can't add custom values to it.

1. In **Disposition codes**, select any disposition codes that should also trigger a reattempt. These are business outcomes set by service representatives during or after a call. To make a code available for reattempt selection, create it under the category **Not right party**. The same disposition codes also appear on the representative's screen during the call. Learn more in [Configure disposition codes](configure-disposition-codes.md).

1. Under **Reattempts**, specify:
   - **Retry attempts**: The maximum number of retry attempts.
   - **Time delay before automatically starting the call**: The wait time between attempts.

1. Under **Fallback configuration**, optionally select an SMS proactive engagement configuration to use when all retry attempts are exhausted.
Select **None** if no fallback is needed.

   > [!NOTE]
   > SMS fallback is currently in preview feature and requires opting in to the preview.

1. Select **Next**.

### Frequency limits

On the **Frequency limits** page, configure how often contacts can be reached and during which hours.

1. Select **Use frequency limits** to enable frequency controls, and then specify:
   - **Maximum engagements per day**: The maximum number of times a contact can be reached in a day across all channels.
   - **Maximum engagements per week**: The maximum number of times a contact can be reached in a week across all channels.

1. Under **Schedule**, select at least one phone number type and set quiet hours for each:
   - **Mobile Phone**
   - **Business Phone**
   - **Home Phone**

   If you select more than one number type, set the preferred contact order by dragging the rows. The system respects the quiet hours configured for each number type and won't place calls during those windows. You must configure quiet hours for every phone number type you select before you can proceed.

1. Under **Time zones**, select how to determine the time zone for each contact:
   - **Use customer's local time zone when available (defaults to UTC if not available)**: The system uses the time zone attribute on each contact record to evaluate quiet hours in that contact's local time. If no time zone is specified on the contact, UTC is used. The time zone value must be explicitly provided in the uploaded file or API payload—the system does not auto-detect or geo-infer time zones.
   - **Use Coordinated Universal Time (UTC)**: All contacts are evaluated against quiet hours using UTC, regardless of their location.

1. Select **Next**.

### Summary

Review all settings on the **Summary** page. To make changes, select **Back** to return to the relevant step.

### File upload

When ready, select **Create**. If you selected **Upload a file** as the intake method, the **File upload** step appears next where you can upload your contact list.

**Supported file formats**: CSV (.csv) and Excel (.xlsx) only.

**File upload constraints**:

- Maximum file size: 10 MB
- The file must include all required columns; additional columns are optional

**Required columns**:

- **UniqueIdentifier**: The value used to identify and upsert the contact record. Must correspond to the **Contact unique identifier** attribute selected in the **Details** step.
- **MobilePhoneNumber**, **BusinessPhoneNumber**, or **HomePhoneNumber**: At least one phone number column is required. Multiple phone number columns can be included.

**Optional named fields**:

Named fields are columns whose names correspond to attributes on the Contact table. Values in these columns are used to create or update the contact record during processing. Any additional columns that do not match a Contact attribute are treated as pass-through data and are made available on the agent desktop during the call.

Data entered in the **Priority** column is used for custom prioritization when the call order is set to **Custom priority ascending** or **Custom priority descending**.

To download a sample file that contains the required columns and formatting, select **Download sample**.

**Processing behavior**:
Records are processed immediately when the file upload begins.

> [!NOTE]
> The uploaded file isn't stored in any form and can't be downloaded after upload. To access delivery results and records, query the relevant tables in Microsoft Dataverse directly. Learn more in [Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md).

**Upload a file to an existing engagement**:

To add a new file to an engagement that's already created, go to **Copilot Service admin center** > **Productivity** > **Proactive engagements**. Select the engagement, and then select **Run from file**. The new file is added to the existing pending deliveries.

Learn more about available outcomes and SIP-based result values in [Outcomes for proactive engagement](proactive-engagement-outcomes.md).

### Related information

[Overview of proactive engagement](overview-proactive-engagement.md)  
[Dial modes for proactive engagement](dial-modes-proactive-engagement.md)  
[Outcomes for proactive engagement](proactive-engagement-outcomes.md)  
[Best practices for proactive engagement campaigns](best-practices-proactive-engagement.md)  
[Overview of conversational journeys](/dynamics365/customer-insights/journeys/conversational-journeys-overview)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
[Use CCaaS_CreateProactiveVoiceDelivery API](../extend/api/ccaas_createproactivevoicedelivery.md)  
[Proactive Outbound dashboard](../use/proactive-outbound-dashboard.md#proactive-outbound-dashboard)
