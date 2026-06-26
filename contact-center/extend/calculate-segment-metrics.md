---
title: Calculate segment-based queue metrics
description: Learn how to calculate segment-based queue metrics in Dynamics 365 Customer Service. Discover key performance indicators to improve contact center or call center interactions.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection:
ms.date: 06/26/2026
ms.custom:
  - bap-template
---

# Calculate segment-based queue metrics

[!INCLUDE [cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

This article explains the DAX measures used for segment-based queue analytics in Omnichannel dashboards. Instead of using session-level metrics, model conversations as segments by using the `msdyn_queueextension` entity. Each entry, transfer, or exit creates a new segment record that tracks the lifecycle of that queue interaction. Learn more in [Use msdyn_queueextension to calculate segment-based queue metrics](msdyn-queueextension.md).

> [!NOTE]
> All metrics apply to both Omnichannel Real-time and Omnichannel Historical dashboards. Exceptions are noted individually.

The following dashboards are supported:

- Real-time dashboard: Queries the Dataverse SQL directly, so the measures reflect the current state of `msdyn_queueextension` and `msdyn_ocliveworkitem`. Because conversations might still be active, it includes live-only measures such as Segments Waiting Now and Longest Segment Wait Time based on `CurrentWaitTimeInSeconds`.

- Historical dashboard: Loads FactQueueExtension data from Azure Data Lake CSV exports instead of the live Dataverse source. It uses the same measure definitions, with two key differences:

  - Power Query renames queue ID columns with a `_FQE` suffix to avoid conflicts when joining with `DimQueue`.
  - DAX expressions use logical column names, while relationships are configured on the `_FQE` columns.

## Total segments

Count of all inbound segments. Each `msdyn_queueextension` row is one segment. A conversation that transfers across three queues is considered as three segments.

```dax

Total Segments =  CALCULATE(  COUNT(FactQueueExtension\[QueueextensionId\]),  FactQueueExtension\[DirectionCode\] = FALSE())

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_isoutbound |
| Filters | msdyn_ocliveworkitem.msdyn_isoutbound = false (inbound only). |

## Engaged conversation segments

Segments where a customer service representative (service or representative) accepts the conversation. Use the `IsEngaged` flag. Set the flag to true when `AgentAcceptedOn` is populated.

```dax

Engaged Conversation Segments =  
CALCULATE(  
COUNT(FactQueueExtension\[QueueextensionId\]),  
FactQueueExtension\[IsEngaged\] = TRUE(),  
FactQueueExtension\[DirectionCode\] = FALSE()  
)

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_agentacceptedon, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_agentacceptedon isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Abandoned conversation segments

Segments where the customer leaves the conversation before a representative accepts it. Use this segment in abandonment reporting and short-abandon follow-on measures.

```dax

Abandoned Conversation Segments =  
CALCULATE(  
COUNT(FactQueueExtension\[QueueextensionId\]),  
FactQueueExtension\[IsAbandoned\] = TRUE(),  
FactQueueExtension\[DirectionCode\] = FALSE()  
)

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_isabandoned, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_isabandoned = true AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Engaged conversation segments %

Percentage of total segments that a representative engages. This percentage helps determine queue health and staffing quality analysis.

```dax

 Engaged Conversation Segments % =  
 VAR engaged = \[Engaged Conversation Segments\]  
 VAR total = \[Total Segments\]  
 RETURN  
 DIVIDE(engaged, total, BLANK())

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_agentacceptedon, msdyn_isoutbound |
| Filters | None |

## Abandoned conversation segments %

The percentage of conversation segments in which customers abandon the interaction. This percentage is a key KPI for evaluating wait time–driven abandonment and customer responsiveness to wait times.

```dax

 Abandoned Conversation Segments % =  
 VAR abandoned = \[Abandoned Conversation Segments\]  
 VAR total = \[Total Segments\]  
 RETURN  
 DIVIDE(abandoned, total, BLANK())

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_isabandoned, msdyn_isoutbound |
| Filters | None |

## Average Agent Accept Time (Segment) (sec)

The average time in seconds from when the system first offers an assignment to a representative until the representative accepts it, calculated across engaged segments. This metric measures routing-to-acceptance latency, not total queue wait time.

```dax


 Average Speed to Answer (Segment) (sec) =  
 CALCULATE(  
 AVERAGEX(  
 FILTER(  
 FactQueueExtension,  
 NOT ISBLANK(FactQueueExtension\[AgentAcceptedOn\]) &&  
 NOT ISBLANK(FactQueueExtension\[AgentFirstAssignedOn\]) &&  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 ),  
 DATEDIFF(  
 FactQueueExtension\[AgentFirstAssignedOn\],  
 FactQueueExtension\[AgentAcceptedOn\],  
 SECOND  
 )  
 )  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_agentacceptedon, msdyn_agentassignedon, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_agentacceptedon isn't null AND msdyn_queueextension.msdyn_agentassignedon isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Average Speed to Answer (Segment) (sec)

The average of `FirstWaitTimeInSeconds` (precomputed in Dataverse) across all inbound segments. This metric measures the duration from the start of a segment until a conversation is either accepted by a representative or closed.

 
```dax

Average Speed to Answer (Segment) (sec) =  
CALCULATE(  
AVERAGE(FactQueueExtension\[FirstWaitTimeInSeconds\]),
FactQueueExtension\[IsEngaged\] = TRUE(),  
FactQueueExtension\[DirectionCode\] = FALSE()  
)

```

| Element            | Value                                    |
|------------------------|------------------------------------------------|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem     |
| Attributes        | msdyn_firstwaittimeinseconds, msdyn_isoutbound |
| Filters          | msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Segments waiting now (real time only)

*Applies to Omnichannel real-time dashboards.*

The number of inbound segments that aren't closed and belong to conversations that are either open or in an active state awaiting acceptance by a representative. This measure represents customers currently waiting in queue. This measure is specific to the real-time dashboard because it relies on CurrentWaitTimeInSeconds and the live work item status.

```dax 

Segments Waiting Now = 
          CALCULATE(
              COUNT(FactQueueExtension[QueueextensionId]),
              FactQueueExtension[DirectionCode] = FALSE(),
              FactQueueExtension[IsClosed] = FALSE(),
              (
                  FactQueueExtension[ConversationStatusCode] = 1  // Open
                  ||
                  (
                      FactQueueExtension[ConversationStatusCode] = 2  // Active
                      &&
                      (
                          FactQueueExtension[StatusChangeReason] = 192350002
                          || FactQueueExtension[StatusChangeReason] = 192350001
                      )
                  )
              )
          )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_endtime, statuscode, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_endtime is null AND msdyn_ocliveworkitem.statuscode = 1 AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Longest segment wait time (sec)

The maximum CurrentWaitTimeInSeconds across inbound segments.
-  In real-time reporting, it's the longest wait a live customer is experiencing right now. CurrentWaitTimeInSeconds is calculated in Power Query against GETUTCDATE().
- In historical reporting, FirstWaitTimeInSeconds is considered rather than CurrentWaitTimeInSeconds because historical data has no live-waiting segments.


### [Historical analytics](#tab/historicalpage)

```dax

Longest Segment Wait Time (sec) = 
     CALCULATE( 
         MAX(FactQueueExtension[FirstWaitTimeInSeconds]), 
         FactQueueExtension[IsEngaged] = TRUE(), 
         FactQueueExtension[DirectionCode] = FALSE() 
     ) 

```
| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_firstwaittimeinseconds, msdyn_agentacceptedon, msdyn_isoutbound  |
| Filters | msdyn_queueextension.msdyn_agentacceptedon isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |



### [Real-time analytics](#tab/realtimepage)

```dax


 Longest Segment Wait Time (sec) =  
 CALCULATE(  
 MAX(FactQueueExtension\[CurrentWaitTimeInSeconds\]),  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_waitstartedon, msdyn_endtime, statuscode, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_endtime is null AND msdyn_ocliveworkitem.statuscode = 1 AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

---

## InServiceLevel (calculated column)

Indicates whether the service-level agreement is met. This value is TRUE when the segment is engaged and its FirstWaitTimeInSeconds is within the queue's ServiceLevelThreshold. If the threshold isn't set, the system considers the segment within the service level (provided it was engaged).

 
```dax


InServiceLevel =  
 (  
 ISBLANK(RELATED(DimQueue\[ServiceLevelThreshold\])) \|\|  
 FactQueueExtension\[FirstWaitTimeInSeconds\] \<= RELATED(DimQueue\[ServiceLevelThreshold\])  
 ) &&  
 FactQueueExtension\[IsEngaged\] &&  
 NOT FactQueueExtension\[DirectionCode\]

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, queue, msdyn_ocliveworkitem |
| Attributes | msdyn_firstwaittimeinseconds, msdyn_agentacceptedon, msdyn_isoutbound, queue.ServiceLevelThreshold |
| Filters | Evaluated per row; TRUE only when msdyn_queueextension.msdyn_agentacceptedon isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false AND (queue.ServiceLevelThreshold is null OR msdyn_firstwaittimeinseconds \<= queue.ServiceLevelThreshold). |

## Service level met %

Percentage of engaged segments that met the queue's service level. This value is the count of engaged segments where `InServiceLevel` is `TRUE`, divided by the total number of engaged segments.

```dax


 Service Level Met % =  
 VAR sla_met = CALCULATE(  
 COUNT(FactQueueExtension\[QueueextensionId\]),  
 FactQueueExtension\[InServiceLevel\] = TRUE()  
 )  
 VAR engaged = \[Engaged Conversation Segments\]  
 RETURN  
 DIVIDE(sla_met, engaged, BLANK())

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, queue, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_firstwaittimeinseconds, msdyn_agentacceptedon, msdyn_isoutbound, queue.ServiceLevelThreshold |
| Filters | None |

## Segments in service level

The total count of segments where the `InServiceLevel` flag is `TRUE`. Use this count to derive the number of segments in service-level agreements.

```dax


 Segments in Service Level =  
 CALCULATE(  
 COUNT(FactQueueExtension\[QueueextensionId\]),  
 FactQueueExtension\[InServiceLevel\] = TRUE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, queue, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_firstwaittimeinseconds, msdyn_agentacceptedon, msdyn_isoutbound, queue.ServiceLevelThreshold |
| Filters | FactQueueExtension\[InServiceLevel\] = true. |

## IsShortAbandoned (calculated column)

Identifies short abandons based on the ShortAbandonedThreshold. The following values are applicable:
- TRUE when an abandoned or closed inbound segment lasts less than the threshold.
- FALSE for non-abandoned segments.
- BLANK when the threshold isn't configured or context is missing.

```dax



 IsShortAbandoned =  
 VAR Threshold = RELATED(DimQueue\[ShortAbandonedThreshold\])  
 VAR TimeToAbandon =  
 IF (  
 FactQueueExtension\[IsAbandoned\]  
 && FactQueueExtension\[IsClosed\]  
 && NOT FactQueueExtension\[DirectionCode\],  
 DATEDIFF(FactQueueExtension\[SegmentStartTime\], FactQueueExtension\[SegmentClosedOn\], SECOND),  
 BLANK()  
 )  
 RETURN  
 IF (  
 FactQueueExtension\[IsAbandoned\]  
 && NOT FactQueueExtension\[DirectionCode\]  
 && FactQueueExtension\[IsClosed\]  
 && NOT ISBLANK(Threshold)  
 && TimeToAbandon \< Threshold,  
 TRUE,  
 IF (  
 NOT FactQueueExtension\[IsAbandoned\],  
 FALSE,  
 BLANK()  
 )  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, queue, msdyn_ocliveworkitem |
| Attributes | msdyn_isabandoned, msdyn_endtime, msdyn_starttime, msdyn_closedon, msdyn_isoutbound, queue.ShortAbandonedThreshold |
| Filters | Evaluated per row; TRUE when msdyn_queueextension.msdyn_isabandoned = true AND msdyn_queueextension.msdyn_endtime isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false AND queue.ShortAbandonedThreshold isn't null AND (msdyn_closedon - msdyn_starttime) \< queue.ShortAbandonedThreshold. |

## Short abandoned count

The total number of abandoned segments that are classified as short abandons. These instances represent situations where a customer leaves the call quickly and don't typically indicate a queue staffing problem.

```dax

 Short Abandoned Count =  
 CALCULATE(  
 COUNT(FactQueueExtension\[QueueextensionId\]),  
 FactQueueExtension\[IsShortAbandoned\] = TRUE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, queue, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_isabandoned, msdyn_starttime, msdyn_closedon, msdyn_isoutbound, queue.ShortAbandonedThreshold |
| Filters | FactQueueExtension\[IsShortAbandoned\] = true. |

## Short abandoned %

Percentage of abandoned segments that are short abandons. A high percentage indicates that abandons are primarily due to misdials or IVR navigation problems rather than frustration over long wait times.

```dax

 Short Abandoned % =  
 VAR short_abandoned = \[Short Abandoned Count\]  
 VAR total_abandoned = \[Abandoned Conversation Segments\]  
 RETURN  
 DIVIDE(short_abandoned, total_abandoned, BLANK())

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, queue, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_isabandoned, msdyn_starttime, msdyn_closedon, msdyn_isoutbound, queue.ShortAbandonedThreshold |
| Filters | None |

## Average time to abandon (sec)

The average time elapsed from segment start to close, calculated for abandoned and closed inbound segments only. Helps supervisors understand how long customers wait before hanging up.

```dax

 Average Time to Abandon (sec) =  
CALCULATE(  
AVERAGEX(  
 FILTER(  
 FactQueueExtension,  
 FactQueueExtension\[IsAbandoned\] = TRUE() &&  
 FactQueueExtension\[IsClosed\] = TRUE() &&  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 ),  
 DATEDIFF(  
 FactQueueExtension\[SegmentStartTime\],  
 FactQueueExtension\[SegmentClosedOn\],  
 SECOND  
 )  
 )  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_starttime, msdyn_closedon, msdyn_isabandoned, msdyn_endtime, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_isabandoned = true AND msdyn_queueextension.msdyn_endtime isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Average handle time (Segment) (sec)

Average total handle time per engaged segment. This calculation includes talk time, hold time, and wrap-up time. The value is stored in `msdyn_queueextension.msdyn_handletime`.

```dax

 Average Handle Time (Segment) (sec) =  
 CALCULATE(  
 AVERAGE(FactQueueExtension\[HandleTimeInSeconds\]),  
 FactQueueExtension\[IsEngaged\] = TRUE(),  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_handletime, msdyn_agentacceptedon, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_agentacceptedon isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Average talk time (Segment) (sec)

Average cumulative talk time per engaged segment.

```dax



 Average Talk Time (Segment) (sec) =  
 CALCULATE(  
 AVERAGE(FactQueueExtension\[TalkTimeInSeconds\]),  
 FactQueueExtension\[IsEngaged\] = TRUE(),  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_talktime, msdyn_agentacceptedon, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_agentacceptedon isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Average hold time (Segment) (sec)

Average cumulative hold time per engaged segment.

```dax

 Average Hold Time (Segment) (sec) =  
 CALCULATE(  
 AVERAGE(FactQueueExtension\[HoldTimeInSeconds\]),  
 FactQueueExtension\[IsEngaged\] = TRUE(),  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_holdtime, msdyn_agentacceptedon, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_agentacceptedon isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Average wrap up time (Segment) (sec)

Average cumulative active wrap-up time per engaged segment.


```dax


 Average Wrapup Time (Segment) (sec) =  
 CALCULATE(  
 AVERAGE(FactQueueExtension\[ActiveWrapupTimeInSeconds\]),  
 FactQueueExtension\[IsEngaged\] = TRUE(),  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_activewrapuptime, msdyn_agentacceptedon, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_agentacceptedon isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Transfer-in count (Segment)

The number of inbound segments generated from queue transfers. A segment is considered a transfer-in when the `SourceQueueId` field is populated at the time the segment is created.

```dax


 Transfer-in Count (Segment) =  
 CALCULATE(  
 COUNT(FactQueueExtension\[QueueextensionId\]),  
 FactQueueExtension\[IsTransferredIn\] = TRUE(),  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_sourcequeue, msdyn_isoutbound |
| Filters | msdyn_queueextension.msdyn_sourcequeue isn't null AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Transfer-out count (Segment)

The total number of inbound segments that result in a transfer out. A segment is considered transferred out when a `TargetQueueId` is present or when the closure reason is ExternalAgentAccept, ExternalAgentReject, ExternalAgentTransfer, or OverflowQueueTransfer.

```dax

 Transfer-out Count (Segment) =  
 CALCULATE(  
 COUNT(FactQueueExtension\[QueueextensionId\]),  
 FactQueueExtension\[IsTransferredOut\] = TRUE(),  
 FactQueueExtension\[DirectionCode\] = FALSE()  
 )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_targetqueue, msdyn_closurereason, msdyn_isoutbound |
| Filters | (msdyn_queueextension.msdyn_targetqueue isn't null OR msdyn_queueextension.msdyn_closurereason in ('ExternalAgentAccept','ExternalAgentReject','ExternalAgentTransfer','OverflowQueueTransfer')) AND msdyn_ocliveworkitem.msdyn_isoutbound = false. |

## Transfer-in percentage

The percentage of total segments that are transferred in.

```dax

 Transfer-in % =  
 VAR transferred_in = \[Transfer-in Count (Segment)\]  
 VAR total = \[Total Segments\]  
 RETURN  
 DIVIDE(transferred_in, total, BLANK())

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_sourcequeue, msdyn_isoutbound |
| Filters | None |

## Transfer-out percentage

The percentage of total segments that are transferred out.

```dax

 Transfer-out % =  
 VAR transferred_out = \[Transfer-out Count (Segment)\]  
 VAR total = \[Total Segments\]  
 RETURN  
 DIVIDE(transferred_out, total, BLANK())

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_targetqueue, msdyn_closurereason, msdyn_isoutbound |
| Filters | None  |

## Net transfer

The difference between transfer-in and transfer-out counts. A positive value indicates that the queue received more transfers than it sent, while a negative value indicates that the queue transferred out more conversations than it received.

```dax

 Net Transfer =  
 \[Transfer-in Count (Segment)\] - \[Transfer-out Count (Segment)\]

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_queueextensionid, msdyn_sourcequeue, msdyn_targetqueue, msdyn_closurereason, msdyn_isoutbound |
| Filters | Derived from \[Transfer-in Count (Segment)\] - \[Transfer-out Count (Segment)\]. |

## Transfer-in count (Excluding bot transfers)

The number of segments transferred into a queue, excluding transfers initiated by bots, such as bot transfer sessions and bot overflow queue transfers.

```dax

Transfer-in Count (Excl. Bot Transfers) = 
          CALCULATE(
              COUNT(FactQueueExtension[QueueextensionId]),
              FactQueueExtension[IsTransferredIn] = TRUE(),
              NOT FactQueueExtension[CreationReason] IN {"BotTransferSession", "BotOverflowQueueTransfer"}
          )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem|
| Attributes | msdyn_sourcequeue (IsTransferredIn = sourcequeue IS NOT NULL), msdyn_creationreason |
| Filters | msdyn_queueextension.msdyn_sourcequeue is not null AND msdyn_queueextension.msdyn_creationreason NOT IN ('BotTransferSession', 'BotOverflowQueueTransfer') |

## Transfer-out count (excluding bot transfers)

The number of segments transferred out of a queue, excluding transfers that bots initiate, such as bot transfer sessions and bot overflow queue transfers.

```dax

Transfer-out Count (Excl. Bot Transfers) = 

          CALCULATE(
              COUNT(FactQueueExtension[QueueextensionId]),
              FactQueueExtension[IsTransferredOut] = TRUE(),
              NOT FactQueueExtension[ClosureReason] IN {"BotTransferSession", "BotOverflowQueueTransfer"}
          )

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem|
| Attributes | msdyn_targetqueue, msdyn_closurereason |
| Filters | (msdyn_queueextension.msdyn_targetqueue is not null OR msdyn_queueextension.msdyn_closurereason IN ('ExternalAgentAccept', 'ExternalAgentReject', 'ExternalAgentTransfer', 'OverflowQueueTransfer')) AND msdyn_queueextension.msdyn_closurereason NOT IN ('BotTransferSession', 'BotOverflowQueueTransfer') |

## Transfer-in % (excluding bot transfers)

The percentage of inbound segments transferred into a queue or representative, excluding transfers that bots initiate. Calculate this value by dividing Transfer-in Count (Excluding Bot Transfers) by Total Segments.

```dax

Transfer-in % (Excl. Bot Transfers) =

          VAR transferred_in = [Transfer-in Count (Excl. Bot Transfers)]
          VAR total = [Total Segments]
          RETURN
              DIVIDE(transferred_in, total, BLANK())
      
``` 

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_sourcequeue, msdyn_creationreason, msdyn_isoutbound |
| Filters | None |

## Transfer-out % (Excluding bot transfers)

The percentage of inbound segments transferred out, excluding transfers that bots initiate. Calculate this percentage by dividing **Transfer-out Count (Excluding Bot Transfers)** by **Total Segments**.

```dax

Transfer-out % (Excl. Bot Transfers) = 

          VAR transferred_out = [Transfer-out Count (Excl. Bot Transfers)]
          VAR total = [Total Segments]
          RETURN
              DIVIDE(transferred_out, total, BLANK())

```

| Element| Value |
|----|----|
| Dataverse entities | msdyn_queueextension, msdyn_ocliveworkitem |
| Attributes | msdyn_targetqueue, msdyn_closurereason, msdyn_isoutbound  |
| Filters | None |

## Related information

[Calculate conversation metrics](/dynamics365/customer-service/develop/calculate-conversation-metrics?tabs=historicalpage)  
[Calculate session metrics](/dynamics365/customer-service/develop/calculate-session-metrics?tabs=historicalpage)  
[Calculate customer service representative metrics](/dynamics365/customer-service/develop/calculate-representative-metrics?tabs=historicalpage)
