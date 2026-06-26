---
title: Use msdyn_queueextension to calculate segement-based queue metrics
description: Learn about the msdyn_queueextension table, which uses queue-level conversation segments for analytics and reporting in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: reference
ms.date: 04/24/2026
ms.custom: bap-template 
---

# Use msdyn_queueextension to calculate segement-based queue metrics


The **msdyn_queueextension** table is a Dataverse table that tracks queue-level conversation segments used for analytics and reporting in Dynamics 365 Contact Center.
A record in this table represents a queue interaction (segment). When a conversation is transferred between queues, a new record is created for each queue. This provides a complete, segment-by-segment view of a conversation’s journey across queues, enabling granular reporting on queue flow, wait times, customer service representative engagement, transfers, and abandonment.

## Core identity and relationships

Each queue segment in the table is linked to a parent conversation and the queue where the segment occurred. Source and target queue references indicate transfer events.


| Physical Name              | Logical Name             | Type        | Display Name      | Description                                                                 |
|---------------------------|-------------------------|-------------|-------------------|-----------------------------------------------------------------------------|
| msdyn_QueueExtensionId    | msdyn_queueextensionid  | primarykey  | Queue Extension   | Unique identifier for entity instances.                |
| msdyn_ConversationId      | msdyn_conversationid    | Lookup      | Conversation Id   | Parent conversation id from msdyn_ocliveworkitem.                    |
| msdyn_QueueId             | msdyn_queueid           | Lookup      | Queue Id          | Queue where the segment occurred.                                           |
| msdyn_SourceQueue         | msdyn_sourcequeue       | Lookup      | Source Queue      | Source queue of the segment transfer. |
| msdyn_TargetQueue         | msdyn_targetqueue       | Lookup      | Target Queue      | Target queue of the segment transfer.          |

## Lifecycle and timing fields

The following fields record key timestamps in a segment’s lifecycle, such as queue entry, routing, representative acceptance, and closure. The following measures are used to calculate wait time and handling durations.

| Physical Name              | Logical Name             | Type        | Display Name        | Description                                                                |
|---------------------------|-------------------------|-------------|---------------------|----------------------------------------------------------------------------|
| msdyn_StartTime           | msdyn_starttime         | Datetime    | Start Time          | Segment start. Indicates when the conversation enters the queue.                     |
| msdyn_EndTime             | msdyn_endtime           | Datetime    | End Time            | Segment end. Indicates when the conversation exits the queue.                        |
| msdyn_AgentAssignedOn     | msdyn_agentassignedon   | Datetime    | Agent Assigned On   | Timestamp when the routing assignment was first offered.                           |
| msdyn_AgentAcceptedOn     | msdyn_agentacceptedon   | Datetime    | Agent Accepted On   | Timestamp when a service representative accepts the assignment.                                    |
| msdyn_ClosedOn            | msdyn_closedon          | Datetime    | Closed On           | Timestamp when the segment was closed.

## Status and reason fields

These fields classify segment outcomes and transitions, such as abandonment and transfer.

| Physical Name              | Logical Name             | Type              | Display Name    | Description                                                                 |
|---------------------------|-------------------------|-------------------|-----------------|-----------------------------------------------------------------------------|
| msdyn_IsAbandoned         | msdyn_isabandoned       | bit (Yes/No)      | Is Abandoned    |TRUE when the customer leaves the conversation before a service representative accepts.                        |
| msdyn_CreationReason      | msdyn_creationreason    | nvarchar (text)   | Creation Reason | Reason the segment was created such as, DirectQueueEntry, TransferIn.         |
| msdyn_ClosureReason       | msdyn_closurereason     | nvarchar (text)   | Closure Reason  | Reason the segment ended such as, EndConversation, TransferOut, ExternalAgentTransfer, OverflowQueueTransfer. |
| Statecode                 | Statecode               | State             | Status          | State of the Queue Extension record.                                         |
| Statuscode                | Statuscode              | Status            | Status Reason   | Status reason for the record.                                |

## Time component fields

msdyn_queueextension includes preaggregated duration columns, to support direct aggregation in analytics without other calculations.

| Physical Name                  | Logical Name                 | Type    | Display Name             | Description                                                                 |
|-------------------------------|-----------------------------|---------|--------------------------|-----------------------------------------------------------------------------|
| msdyn_FirstWaitTimeInSeconds  | msdyn_firstwaittimeinseconds| int     | First Wait Time In Seconds| Wait time (in seconds) from segment start until the representative accepts the call or segment closes. |
| msdyn_HandleTime              | msdyn_handletime            | int     | Handle Time              | Total handle time in seconds. This includes talk, hold, and active wrap-up duration.                |
| msdyn_TalkTime                | msdyn_talktime              | int     | Talk Time                | Cumulative talk time in seconds.                                            |
| msdyn_HoldTime                | msdyn_holdtime              | int     | Hold Time                | Cumulative hold time in seconds.                                            |
| msdyn_ActiveTime              | msdyn_activetime            | int     | Active Time              | Cumulative active time in seconds.                                          |
| msdyn_ActiveChatTime          | msdyn_activechattime        | int     | Active Chat Time         | Cumulative active chat time in seconds.                                     |
| msdyn_ActiveWrapupTime        | msdyn_activewrapuptime      | int     | Active Wrapup Time       | Cumulative active wrap-up time in seconds.                                  |
| msdyn_InActiveTime            | msdyn_inactivetime          | int     | Inactive Time            | Cumulative inactive time in seconds.                                        |

## Related information

[Calculate segment-based queue metrics](calculate-segment-metrics.md)  