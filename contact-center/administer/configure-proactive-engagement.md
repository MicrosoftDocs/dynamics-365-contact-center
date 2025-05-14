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
- If utilizing Dynamics 365 Customer Insights Journey for your customer journey authoring, you must obtain a Customer Insights Journey license Customer Insights license guidance - Dynamics 365 Customer Insights | Microsoft Learn
- If utilizing Microsoft Copilot Studio agents, you must have a Copilot Studio license Get access to Copilot Studio - Microsoft Copilot Studio | Microsoft Learn


[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]




## Set up an outbound workstream
Outbound workstreams are a new type of workstream that should only be created for calls done through proactive engagement. For agent dialed outbound calls, please see Set up outbound calling in the voice channel | Microsoft Learn
1.	Navigate to the workstreams tab and select New workstream 
2.	Select Outbound as this will be the workstream used for your proactive engagement. 
3.	Select a name for the outbound workstream and setup the fallback queue.
4.	Setup the outbound workstream behaviors
5.	Select the calling number and the caller id number.Only numbers that are available to use will appear here. For more information on buying or bringing in your own phone numbers, please see Manage phone numbers | Microsoft Learn
6.	Setup the language and outbound behaviors. For more information, please see Set up inbound calling for the voice channel | Microsoft Learn
7.	Finish setting up your outbound workstream by configuring work distribution, add a bot to the workstream, and configuring agent notifications. For assistance, please see Create and manage workstreams | Microsoft Learn
8.	Important: For Outbound Workstream, there are new agent notifications available 1) Outbound agent dial and 2) Outbound pre-dial
9.	Outbound agent dial will be used for preview dial mode calls
10. Outbound pre-dial will be use for progressive and copilot dial mode calls

5.	Important: When setting up an outbound workstream, routing rules are already pre-configured for you. 

## Configure settings for proactive engagement

You can navigate to the proactive engagement settings in one of the following ways and then create a proactive engagement.

- In the site map of Copilot Service admin center, select **Productivity** under **Support experience**. Select **Manage** for **Proactive engagements (preview)**, and then select **New**.
- Create an [outbound type of workstream](/dynamics365/customer-service/administer/create-workstreams?context=/dynamics365/contact-center/context/administer-context) for voice, and on the workstream page, select **New proactive engagement**.

1. On **Create new proactive engagement (preview)**, enter the following details in **Engagement details**:
   - **Name**: Enter a name for the proactive engagement.
   - **Description**: Enter a description for the proactive engagement.
   - **Workstream**: Select a workstream.
   - **Channel type**: **Voice** is selected by default and not available for edit.
   - Important: The name and description of the engagement will be seen by the support representatives in the agent notification so it is recommended to use descriptive information to help them understand the call
1. In **Routing details**, enter the following information:
   - **Primary queue**: Select a queue. 
   - **Fallback queue**: This will be pre-populated based on the fallback queue set for the outbound workstream.
   - **Skills**: Select the skills that are required for the proactive engagement.
1. Select **Next**. The **Dialing modes** page appears.
1. Select one of the dialing modes as follows:
   - **Copilot**: The system automatically dials the customer and connects the call to the agent when the customer answers. This mode is used for high-volume outbound calls.
   - **Progressive**: The system starts the call with an agent and then adds a representative after the agent actions are complete.
   - **Preview**: The system add the representative to the call and then dials the customer.
1. Select one of the following priority levels:
   - **Normal**
   - **High**
   - **Critical** 
1. Select the **Max number of concurrent calls for Copilot Mode**. This refers to the maximum number of calls to be made by the bot at the same time. The maximum number you can select is 500 calls.
2. Select the max number of calls that can be assigned to the representative in **Maximum calls per representative**. This setting is available forthe progressive dialing mode. This refers to the maximum amount of customer calls to make per available representative. The lower the number, the more balanced a representative’s call volume may be. The max number of calls you can choose is 5.
1. In **Call order**, select one of the following options:
   - **Earliest Scheduled Date**
   - **Last in First Out**
   - **First in, First Out**
1. Under **Operating hours**, select the checkbox if calls can be made outside of queue hours. This setting is available for Copilot dialing mode only.
1. Select the action for how the call needs to be handled if the AI agent fails during the call.
   - **Stop making calls immediately**: No further calls are made.
   - **Continue making calls**:
     - **Rate of failure reaches**: Select a value from the **Percent** dropdown list. The default value is one and the maximum value is five.
1. Rules are also available to set for Copilot and Progressive Mode. These help control the throttling and pacing for the proactive engagement. The following rules are available
a.	   Abandonment rate (Copilot and Progressive Mode). This refers to the percentage of customers who hang up before connecting with a representative.
b.	   Average wait time (Copilot and Progressive Mode). This refers to the average amount of time it takes for customers to connect to representatives.
c.	   Escalation count (Copilot Mode). This refers to the total number of escalations made from the AI agent.
d.	   Open concurrent  escalations (Copilot Mode). This refers to the total number of open escalations that haven't been resolved. 

1. Select **Next**.
1. On the **Outcomes** page, select the outcomes that are available for the proactive engagement, and then select **Next**.
   a.	To add attributes, please add context variables to your outbound workstream Manage context variables | Microsoft Learn
   b.  Make sure to add the context variable you created in your Copilot Studio agent using the same naming. https://learn.microsoft.com/en-us/dynamics365/customer-service/administer/context-variables-for-bot#configure-context-variables-for-copilot-agent
1. The **Summary** page displays the settings that you configured. Review the settings, and then select **Create**.

## Configure proactive engagement with a journey using Customer Insights

To be linked to the Customer Insights documentation.

## Configure proactive engagement with a journey using the API

To configure the proactive engagement with a journey using the API, follow the steps in [Initiate proactive outbound call using API](../extend/api/ccaas_createproactivevoicedelivery.md).

## Dial modes

The dial modes are used to determine how the system will initiate calls to customers. Important: The use of Copilot and/or Progressive dial modes for non-transactional commercial purposes constitutes a violation of Microsoft's terms of service.

- **Copilot**: Use the Copilot dial mode for making announcements, notifications, or any outbound call that can be handled by an IVR agent. A large number of these calls can be made simultaneously. A few examples are payment reminders, service restoration, and delivery notifications. When a customer picks an outbound call, the agent registered on the workstream engages with the customer. The agent can escalate to a service representative if required. However, the wait times might be similar to if the customer had called into the contact center for assistance.

- **Progressive**: Use the progressive dial mode to call the customer first. As soon as the customer picks the call, a Copilot agent is added to the call to perform basic tasks like determining if the right person has answered the call and if they are free to talk. Using an AI agent to gather this information saves service representatives from joining calls that don't need them to be on it further maximizing time spent in helping customers. The number of calls made simultaneously is determined by the number of available agents in the queue specified&mdash;a new call is placed for every representative that gets available ensuring that customers get a good experience with minimal wait times.
 
- **Preview**: Use the preview dial mode to identify a service representative from the specified queue and then notify them of the request to make the outbound call. If the representative accepts, then the system places the outbound call to customer with the representative already on the line. Representative gets to speak to the customer if they pick up or leave a voicemail. This dial mode prioritizes customer experience over representative use, and is best suited for scenarios that require a personalized experience. As a result the amount of simultaneous calls made is dependent on number of available representatives.


## Outcomes

_Need information on how to configure outcomes._ *added it to outcomes section 

## Runtime experience
Customer Service Representatives will see the proactive engagement calls based on notitification template created for the outbound workstream. They will see the Name and the Description that is set for the proactive engagement. 

For preview calls, CSR's will be able to start or reject the call. 
For progressive calls, CSR's will only be able to start the call. 

CSR's will also be able to select disposition codes to record the outcome of the interaction. For more information https://learn.microsoft.com/en-us/dynamics365/contact-center/administer/configure-disposition-codes


## Dataverse Data Models  
As the Proactive Engagement solution, there is a set of Dataverse tables created to monitor the Proactive Engagement.  

Proactive Engagement Configuration: Entity definition  
Dataverse Table Name: msdyn_proactive_engagement_config  
Table Type: Standard  
Column  	Schema name  
Name  	msdyn_name  
Description  	msdyn_description  
Proactive Outreach Type  	msdyn_type  
Workstream  	msdyn_workstream  
Dial Mode Type  	msdyn_dialmode_type  
Ignore Queue Hours  	msdyn_ignore_queue_hours  
Priority  	msdyn_priority  
Processing Order  	msdyn_processing_order  
Maximum Concurrent Calls  	msdyn_max_concurrent_calls  
Maximum Calls Per Agent  	msdyn_max_calls_per_agent  
Reserve Agent Capacity  	msdyn_reserve_agent_capacity  
Bot Failure Treatment Type  	msdyn_bot_failure_treatment_type  
Bot Failure Treatment Rate Threshold  
  	msdyn_bot_failure_treatment_rate_threshold  
Queue  	msdyn_queue  
Throttle Metric  	msdyn_throttle_metric  
Throttle Threshold  	msdyn_throttle_threshold  
Throttle Control Period  
  	msdyn_throttle_control_period  
Throttle Adjustment Percentage  
  	msdyn_throttle_adjustment_percentage  
 
Proactive Engagement Configuration Status: Entity definition  
This is a new 1:1 table with Proactive Engagement Configuration to store the status (suspended or not) of a Proactive Engagement Configuration, and the type of the last change.  
Dataverse Table Name: msdyn_proactive_engagement_config_status  
Column  	Schema name  
Proactive Engagement Configuration  	msdyn_proactive_engagement_config  
Is Active 	msdyn_suspended  
Suspension Type  	msdyn_suspension_type  
 
Proactive Engagement Configuration Characteristic: Entity definition  
This is a new table to store the many-to-many relationship between msdyn_proactive_engagement_config and characteristic (aka Skill)  
Dataverse Table Name: msdyn_proactive_eng_config_characteristic  
Column  	Schema name  
Proactive Engagement Configuration  	msdyn_proactive_engagement_configuration  
Characteristic  	msdyn_characteristic  
 
Proactive Engagement Configuration Attribute: Entity definition  
Dataverse Table Name: msdyn_proactive_engagement_config_attribute  
This is a table with a Many-To-One relationship to the new Proactive Engagement Configuration table.  The data stored here is meant to define some element keywords of the “data contract” that exists between the CIJ Journey and the Bot for result attributes.  
Column  	Schema Name  
Proactive Engagement Configuration  	msdyn_proactive_engagement_config  
Keyword  	msdyn_keyword  
 
Proactive Delivery: Entity definition  
Dataverse Table Name: msdyn_proactive_delivery  
All delivery requests that are accepted via the Proactive Engagement input API will get a row in this table.  
Column  	Schema Name  
Delivery Id  	msdyn_delivery_id  
Conversation Id  	msdyn_conversation_id  
Call Id  	msdyn_call_id  
Proactive Engagement Configuration Id  	msdyn_proactive_engagement_config_id  
Journey Id  	msdyn_journey_id  
Journey Run Id  	msdyn_journey_run_id  
Contact Id  	msdyn_contact_id  
Channel  	msdyn_channel  
Status  	msdyn_status  
Queue Id  	msdyn_queue_id  
Tracking Id  	msdyn_tracking_id  
Dial Mode Type  	msdyn_dialmode_type  
To Address  	msdyn_to_address  
From Address  	msdyn_from_address  
Window Start Date  	msdyn_window_start_date  
Window End Date  	msdyn_window_end_date  
Start Date  	msdyn_start_date  
End Date  	msdyn_end_date  
Result  	msdyn_result  
Result Date  	msdyn_result_date  
Disposition Codes  	msdyn_disposition_codes  
 
Proactive Delivery Attribute: Entity definition  
This table stores all the input and result name value pairs associated with the delivery. 
Dataverse Table Name: msdyn_proactive_delivery_attribute  
Column  	Schema Name  
Proactive Delivery  	msdyn_proactive_delivery  
Keyword  	msdyn_keyword  
Value  	msdyn_value  
Type  	msdyn_type  
 
Conversation Attribute: Entity definition 
This is an Elastic table with Many-To-One relationship to existing Conversation table.  This is where the bot author will write attributes collected during the call flow. 
Column  	Schema Name  
Conversation  	msdyn_conversation_id  
Keyword  	msdyn_keyword  
Value  	msdyn_value  
 


### Related information
