---
title: Use proactive engagement tables for reporting
description: Learn how to use proactive engagement tables for reporting.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: reference
ms.date: 01/13/2026
ms.collection: bap-ai-copilot
ms.custom: bap-template 
---

# Use proactive engagement tables for reporting

Proactive engagement allows for customer outreach based on configured engagement scenarios and customer data insights.

The `msdyn_proactive_delivery` and `msdyn_proactive_delivery_attribute` tables store the information related to proactive engagement deliveries and associated attributes, providing comprehensive data for reporting and analytics on proactive engagement activities. Organizations can use this data to:

- Track delivery success rates and performance metrics
- Analyze customer engagement patterns and outcomes
- Monitor queue performance and agent productivity

## Prerequisites

Proactive engagement is configured. Learn more in [Configure proactive engagement](../administer/configure-proactive-engagement.md).

## msdyn_proactive_delivery

The `msdyn_proactive_delivery` table contains delivery requests accepted through the [proactive engagement API](api/ccaas_createproactivevoicedelivery.md). The Proactive Engagement service adds records to this table.


| Column | Schema Name | Type | Description |
|--------|-------------|------|-------------|
| Delivery Id | msdyn_delivery_id | Text | Unique identifier for the delivery. |
| Conversation Id | msdyn_conversation_id | Text | Identifier that links the delivery record to the conversation record. |
| Call Id | msdyn_call_id | Text | The `correlationId` of the Azure Communication Services call. This ID is used to track the call. |
| Proactive Engagement Configuration Id | msdyn_proactive_engagement_config_id | Text | The proactive engagement configuration used. |
| Journey Id | msdyn_journey_id | Text | The journey ID populated if Customer Insights journey is used to trigger the call. |
| Journey Run Id | msdyn_journey_run_id | Text | Specific run instance of the journey, if applicable. |
| Contact Id | msdyn_contact_id | Text | Id of the customer contact in Dynamics. |
| Channel | msdyn_channel | Text | Communication channel used. Supports the voice channel only. |
| Status | msdyn_status | Text | Current delivery status: **Pending**, **InProcess**, **Complete**, **Expired**, **Cancelled**, or **Error**. |
| Queue Id | msdyn_queue_id | Text | Identifier for the queue handling the delivery. |
| Tracking Id | msdyn_tracking_id | Text | Custom tracking identifier.|
| Dial Mode Type | msdyn_dialmode_type | Text | The dial mode configuration. The values are: **Copilot**, **Progressive**, **Preview**. |
| To Address | msdyn_to_address | Text | Destination phone number for the outbound call. |
| From Address | msdyn_from_address | Text | Source phone number for the outbound call. |
| Window Start Date | msdyn_window_start_date | Date and Time | The beginning timestamp for the call window in the `yyyy-MM-ddTHH:mm:ss.fffZ` format. |
| Window End Date | msdyn_window_end_date | Date and Time | The end timestamp for the call window in the `yyyy-MM-ddTHH:mm:ss.fffZ` format.|
| Start Date | msdyn_start_date | Date and Time | Actual start time of the call. |
| End Date | msdyn_end_date | Date and Time | Actual end time of the call.|
| Result | msdyn_result | Text | Final outcome of the call: **CallEnded**, **CallFailed**, **BotFailed**, **Expired**, **Cancelled**, or **Error**. |
| Result Date | msdyn_result_date | Date and Time | Timestamp when the result was determined. |
| Disposition Codes | msdyn_disposition_codes | Text | Comma-separated list of quoted disposition codes such as PromiseToPay, SpokeToAgent. |

## msdyn_proactive_delivery_attribute

The `msdyn_proactive_delivery_attribute` table contains name-value pairs associated with each delivery. This table has both the input attributes provided to the API and corresponding responses.

| Column | Schema Name | Type | Description |
|--------|-------------|------|-------------|
| Proactive Delivery | msdyn_proactive_delivery | Lookup | Reference to the parent proactive delivery record. |
| Keyword | msdyn_keyword | Text | Name of the attribute or parameter. |
| Value | msdyn_value | Text | Value associated with the keyword. |
| Type | msdyn_type | Choice | Indicates whether the record corresponds to an input or result attribute. |

### Related information

[Use CCaaS_CreateProactiveVoiceDelivery API](api/ccaas_createproactivevoicedelivery.md)  