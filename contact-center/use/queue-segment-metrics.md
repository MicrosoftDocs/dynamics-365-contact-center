---
title: Queue segment metrics reference for Shared Analytics Platform
description: Queue segment metric definitions and DAX measures for Shared Analytics Platform.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---
# Queue segment metrics reference for Shared Analytics Platform

Use queue segment metrics to track how work moves through queues and how efficiently each queue handles customer demand. A queue segment runs from the time a conversation enters a queue until it exits. One conversation can create multiple segments as it moves between queues.

Use queue segment metrics to answer operational questions such as:

- How much work entered each queue, and how much was engaged or abandoned?
- Are queues meeting service-level and responsiveness targets?
- How much work is transferred into or out of each queue?
- How much time do service representatives spend handling, talking, holding, and wrapping up work?
- How do customer satisfaction and Net Promoter Score (NPS) compare across queues?

## Metrics

All metrics in this section use `AggQueuePerformance`.

**Service level %** uses engaged segments as its denominator, not all incoming segments. For a zero or blank denominator, the rate and average calculations return blank, except **Avg handle time**, which returns zero.

### Incoming segments

Counts queue segments that entered a queue during the selected period. One conversation can contribute multiple segments as it moves between queues. Use the count to assess queue demand and workload distribution across queues.
<br>

- **Calculation:** `SUM(AggQueuePerformance[TotalSegments])`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Engaged segments, Abandoned segments, Engagement rate, Abandon rate.

### Engaged segments

Counts queue segments accepted by a service representative. Use it to assess how much queue demand resulted in handled work.
<br>

- **Calculation:** `SUM(AggQueuePerformance[EngagedSegments])`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Incoming segments, Engagement rate, Service level %, Avg handle time.

### Abandoned segments

Counts queue segments that ended before a service representative accepted the interaction. Use it to identify unhandled demand and assess queue performance.
<br>

- **Calculation:** `SUM(AggQueuePerformance[AbandonedSegments])`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Incoming segments, Abandon rate, Short abandoned segments.

### Engagement rate

Shows the percentage of queue segments accepted by a service representative. Use it to assess the share of queue demand that became handled work.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[EngagedSegments]), SUM(AggQueuePerformance[TotalSegments]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Incoming segments, Engaged segments, Abandon rate.

### Abandon rate

Shows the percentage of queue segments abandoned before acceptance. Use it to identify queues where customers leave before connecting with a service representative.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[AbandonedSegments]), SUM(AggQueuePerformance[TotalSegments]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Abandoned segments, Incoming segments, Short abandoned segments %.

### Service level %

Shows the percentage of engaged queue segments answered within the configured SLA target. Use it to assess queue responsiveness and whether queues meet service-level objectives.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[InSLASegments]), SUM(AggQueuePerformance[EngagedSegments]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Engaged segments, Avg speed of answer, Abandon rate.

### Avg speed of answer

Measures the average time from queue entry to connection with a service representative. Use it to assess queue responsiveness.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[TotalFirstWaitTimeInSeconds]), SUM(AggQueuePerformance[WaitTimeCount]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Service level %, Abandon rate.

### Avg handle time

Measures the average handling duration for engaged queue segments. Use it to assess the effort needed to resolve work routed through a queue.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[TotalHandleTimeInSeconds]), SUM(AggQueuePerformance[EngagedSegments]), 0 )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Avg talk time, Avg hold time, Avg wrapup time.

### Transferred out segments

Counts queue segments transferred from the queue to another queue. Use it to assess transfer-out volume and identify queues that frequently reroute work.
<br>

- **Calculation:** `SUM(AggQueuePerformance[TransferredOutSegments])`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Transferred out %, Transferred in segments.

### Transferred in segments

Counts queue segments received from another queue. Use it to assess how much queue demand comes from transfers.
<br>

- **Calculation:** `SUM(AggQueuePerformance[TransferredInSegments])`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Transferred in %, Transferred out segments.

### Transferred out %

Shows the percentage of queue segments transferred out of the queue. Use it to assess how frequently work is routed elsewhere.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[TransferredOutSegments]), SUM(AggQueuePerformance[TotalSegments]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Transferred out segments, Transferred in %.

### Transferred in %

Shows the percentage of queue segments transferred into the queue. Use it to assess how much workload comes from other queues.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[TransferredInSegments]), SUM(AggQueuePerformance[TotalSegments]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Transferred in segments, Transferred out %.

### Avg response time

Measures the average service representative response time for digital interactions associated with queue segments. Use it to assess ongoing responsiveness within a queue.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[TotalResponseTimeInSeconds]), SUM(AggQueuePerformance[MessageBlockCount]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Avg first response time.

### Avg first response time

Measures the average time to the first service representative response. Use it to assess initial responsiveness for digital interactions routed through a queue.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[TotalFirstResponseTimeInSeconds]), SUM(AggQueuePerformance[FirstResponseTimeCount]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Avg response time.

### Avg CSAT

Measures the average customer satisfaction score associated with queue segments. Compare the scores to assess satisfaction across queues.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[Survey_TotalCSATScore]), SUM(AggQueuePerformance[Survey_CSATResponseCount]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** NPS

### NPS

Measures the average Net Promoter Score associated with queue segments. Use it to assess customer advocacy and loyalty across queues.
<br>

- **Calculation:** `DIVIDE( SUM(AggQueuePerformance[Survey_TotalNPSScore]), SUM(AggQueuePerformance[Survey_NPSResponseCount]), BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Avg CSAT.

### Short abandoned segments

Counts queue segments abandoned within the configured short-abandon threshold. Use it to distinguish brief disconnects from longer queue waits.
<br>

- **Calculation:** `SUM(AggQueuePerformance[ShortAbandonedSegments])`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Short abandoned segments %, Abandon rate.

### Short abandoned segments %

Shows the percentage of incoming queue segments abandoned within the short-abandon threshold. Use it to assess how much queue demand ended quickly after queue entry.
<br>

- **Calculation:** `DIVIDE( [Short Abandoned Segments], [Incoming Segments], BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Short abandoned segments, Abandon rate.

### Avg talk time

Measures the average active speaking time during engaged voice queue segments. It shows how much time service representatives spend actively speaking with customers.
<br>

- **Calculation:** `DIVIDE( SUM([TotalTalkTimeInSeconds]), [Engaged Segments], BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Avg hold time, Avg handle time.

### Avg hold time

Measures the average customer hold time during engaged voice queue segments. Use it to identify delays caused by research, collaboration, or process bottlenecks.
<br>

- **Calculation:** `DIVIDE( SUM([TotalHoldTimeInSeconds]), [Engaged Segments], BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Avg talk time, Avg handle time.

### Avg wrapup time

Measures the average wrap-up duration after queue interactions end. Use it to assess post-interaction effort, such as documentation, disposition updates, or follow-up work.
<br>

- **Calculation:** `DIVIDE( SUM([TotalActiveWrapupTimeInSeconds]), [Engaged Segments], BLANK() )`.
- **Source:** `AggQueuePerformance`.
- **Related metrics:** Avg handle time.
