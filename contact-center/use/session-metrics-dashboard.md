---
title: Session metrics reference for Contact Center historical analytics
description: Explore session metric definitions and DAX measures for Shared Analytics Platform in Dynamics 365 Contact Center, including session outcomes and handling times.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---
# Session metrics reference for Contact Center historical analytics

Use session metrics to review service representative performance in primary, consult, and monitor sessions. Track session-offer outcomes, handling and response times, consultation and monitoring activity, and callback progress.

Use session metrics to answer operational questions such as:

- How many sessions were accepted, rejected, timed out, or handled?
- How much time did service representatives spend handling, talking, holding, and wrapping up sessions?
- How quickly did service representatives respond in digital sessions?
- How often were consult and monitor modes used?
- How did callback offers progress from offer to customer connection?

## Metrics

All metrics in this section use `AggAgentPerformance`.

### Total sessions handled

The total number of accepted primary sessions. Use this metric to understand how many conversations service representatives handled in the selected period.
<br>

- **Calculation:** `CALCULATE(SUM(AggAgentPerformance[AcceptedSessions]), AggAgentPerformance[ParticipantModeCode] = 192350002)`.
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Accepted sessions](#accepted-sessions), [Rejected sessions](#rejected-sessions), [Timed out sessions](#timed-out-sessions), [Avg handle time](#avg-handle-time).

### Accepted sessions

The number of sessions accepted by a service representative. Use this metric to measure accepted conversations before reviewing handling time or response time.
<br>

- **Calculation:** `SUM(AggAgentPerformance[AcceptedSessions]).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Total sessions handled](#total-sessions-handled), [Rejected sessions](#rejected-sessions), [Timed out sessions](#timed-out-sessions), [Avg handle time](#avg-handle-time).

### Rejected sessions

Counts sessions rejected by a service representative. Compare rejected, accepted, and timed-out sessions to assess session-offer outcomes.
<br>

- **Calculation:** `SUM(AggAgentPerformance[RejectedSessions]).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Accepted sessions](#accepted-sessions), [Timed out sessions](#timed-out-sessions), [Total sessions handled](#total-sessions-handled).

### Timed out sessions

Counts sessions that timed out before acceptance. Compare timed-out, rejected, and accepted sessions to assess session-offer outcomes.
<br>

- **Calculation:** `SUM([TimedOutSessions]).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Accepted sessions](#accepted-sessions), [Rejected sessions](#rejected-sessions), [Total sessions handled](#total-sessions-handled).

### Avg handle time

Measures the average handling time for completed sessions accepted by a primary service representative. Use it to assess the time representatives spend handling session work.
<br>

- **Calculation:**

  ```dax
  CALCULATE(
      DIVIDE(
          SUM(AggAgentPerformance[TotalHandleTimeInSeconds]),
          SUM(AggAgentPerformance[AcceptedSessions]),
          BLANK()
      ),
      AggAgentPerformance[ParticipantModeCode] = 192350002,
      AggAgentPerformance[SessionStatusCode] = 2
  )
  ```

- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Accepted sessions](#accepted-sessions), [Avg talk time](#avg-talk-time), [Avg hold time](#avg-hold-time), [Avg wrapup time](#avg-wrapup-time).

The handle, talk, hold, and wrap-up averages in this section include only completed sessions accepted by a primary service representative. They return blank when the accepted-session count is zero or blank.

### Avg talk time

The average talk time for completed sessions accepted by a primary service representative. For voice interactions, use this metric to understand active speaking time. The calculation doesn't apply a voice-channel filter.
<br>

- **Calculation:**

  ```dax
  CALCULATE(
      DIVIDE(
          SUM(AggAgentPerformance[TotalTalkTimeInSeconds]),
          SUM(AggAgentPerformance[AcceptedSessions]),
          BLANK()
      ),
      AggAgentPerformance[ParticipantModeCode] = 192350002,
      AggAgentPerformance[SessionStatusCode] = 2
  )
  ```

- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Avg handle time](#avg-handle-time), [Avg hold time](#avg-hold-time).

### Avg hold time

The average hold time for completed sessions accepted by a primary service representative. Use this metric to identify voice-session delays while the customer is on hold.
<br>

- **Calculation:**

  ```dax
  CALCULATE(
      DIVIDE(
          SUM(AggAgentPerformance[TotalHoldTimeInSeconds]),
          SUM(AggAgentPerformance[AcceptedSessions]),
          BLANK()
      ),
      AggAgentPerformance[ParticipantModeCode] = 192350002,
      AggAgentPerformance[SessionStatusCode] = 2
  )
  ```

- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Avg talk time](#avg-talk-time), [Avg handle time](#avg-handle-time).

### Avg wrapup time

The average wrap-up time for completed sessions accepted by a primary service representative. Use this metric to understand after-session work such as notes, disposition, or case updates.
<br>

- **Calculation:**

  ```dax
  CALCULATE(
      DIVIDE(
          SUM(AggAgentPerformance[TotalWrapupTimeInSeconds]),
          SUM(AggAgentPerformance[AcceptedSessions]),
          BLANK()
      ),
      AggAgentPerformance[ParticipantModeCode] = 192350002,
      AggAgentPerformance[SessionStatusCode] = 2
  )
  ```

- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Avg handle time](#avg-handle-time), [Avg consult wrapup time](#avg-consult-wrapup-time).

### Avg response time

Measures the average service representative response time across message exchange cycles. For digital messaging, use it to assess ongoing responsiveness after a session becomes active.
<br>

- **Calculation:** `DIVIDE(SUM(AggAgentPerformance[TotalResponseTimeInSeconds]), SUM(AggAgentPerformance[MessageBlockCount]), BLANK()).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Avg first response time](#avg-first-response-time), [Accepted sessions](#accepted-sessions).

### Avg first response time

Measures the average time to the first service representative response in a session. For digital messaging, use it to assess initial responsiveness.
<br>

- **Calculation:** `DIVIDE(SUM(AggAgentPerformance[TotalFirstMessageResponseTimeInSeconds]), SUM(AggAgentPerformance[FirstMessageResponseCount]), BLANK()).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Avg response time](#avg-response-time), [Accepted sessions](#accepted-sessions).

### Consult sessions

Counts consult-mode sessions. Use it to see how often service representatives bring another representative into a session for consultation.
<br>

- **Calculation:** `CALCULATE(SUM(AggAgentPerformance[TotalSessions]), AggAgentPerformance[ParticipantModeCode] = 192350003).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Avg consult wrapup time](#avg-consult-wrapup-time), [Monitor sessions](#monitor-sessions).

### Avg consult wrapup time

Measures the average wrap-up time for closed consult-mode sessions. Use it to assess post-consult effort.
<br>

- **Calculation:** `CALCULATE([TotalWrapupTime] / [Acceptedsessions], Mode = Consult, Status = Closed).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Consult sessions](#consult-sessions), [Avg wrapup time](#avg-wrapup-time).

### Monitor sessions

Counts monitor-mode sessions. Use it to see how often supervisors monitor sessions.
<br>

- **Calculation:** `CALCULATE(SUM(AggAgentPerformance[TotalSessions]), AggAgentPerformance[ParticipantModeCode] = 192350004).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Avg monitor time](#avg-monitor-time), [Consult sessions](#consult-sessions).

### Avg monitor time

Measures the average monitor duration for closed monitor-mode sessions. Use it to assess how long monitored sessions last.
<br>

- **Calculation:** `CALCULATE([TotalHandleTime] / [Accepted], Mode = Monitor, Status = Closed).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Monitor sessions](#monitor-sessions).

### Callbacks offered

Counts callback offers to customers. Use it to see how often customers receive a callback option.
<br>

- **Calculation:** `SUM(AggAgentPerformance[CallbacksOffered]).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Callbacks opted in](#callbacks-opted-in), [Callbacks initiated](#callbacks-initiated), [Callbacks answered](#callbacks-answered).

### Callbacks opted in

Counts callback offers accepted by customers. Use it to see how often customers choose the callback option.
<br>

- **Calculation:** `SUM(AggAgentPerformance[CallbacksOptedIn]).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Callbacks offered](#callbacks-offered), [Callbacks initiated](#callbacks-initiated).

### Callbacks initiated

Counts callbacks initiated after opt-in. Use it to assess callback execution volume.
<br>

- **Calculation:** `SUM(AggAgentPerformance[CallbacksInitiated]).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Callbacks opted in](#callbacks-opted-in), [Callbacks accepted by agent](#callbacks-accepted-by-agent).

### Callbacks accepted by agent

Counts callback sessions accepted by a service representative. Use it to assess how many initiated callbacks representatives accepted and handled.
<br>

- **Calculation:** `SUM(AggAgentPerformance[CallbacksAcceptedByAgent]).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Callbacks initiated](#callbacks-initiated), [Callbacks answered](#callbacks-answered).

### Callbacks answered

Counts callbacks answered by customers. Use it to assess completed callback connections.
<br>

- **Calculation:** `SUM(AggAgentPerformance[CallbacksAnswered]).`
- **Source:** `AggAgentPerformance`.
- **Related metrics:** [Callbacks accepted by agent](#callbacks-accepted-by-agent), [Callbacks initiated](#callbacks-initiated).
