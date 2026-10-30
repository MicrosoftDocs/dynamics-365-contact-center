---
title: Availability metrics reference for Shared Analytics Platform
description: Availability metric definitions and DAX measures for Shared Analytics Platform.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---
# Availability metrics reference for Shared Analytics Platform

Use availability metrics to review service representative presence and availability over time. The metrics aggregate presence status history into 30-minute windows to compare logged-in time, status duration, and status-change frequency.

Use availability metrics to answer workforce management questions such as:

- How long were service representatives logged in?
- How much time did service representatives spend in available, busy, busy-do-not-disturb, away, and offline states?
- How frequently did service representatives change presence status?
- How is presence time distributed across base or custom presence values?

## Metrics

All metrics use `AggAgentAvailability`, sourced from `FactAgentStatusHistory` with `DimPresence`. Each row represents one service representative, presence status, 30-minute UTC window, and business unit.

**Agent login time**, **Busy duration**, **Busy DND duration**, **Away duration**, and **Offline duration** divide `StatusDurationInSeconds` by 3600 to report hours.

### Login duration

Totals the time service representatives spent in non-offline presence states. Use it to assess how long representatives were signed in and able to participate in contact center activities.
<br>

- **Calculation:** `CALCULATE( SUM(AggAgentAvailability[StatusDurationInSeconds]), DimPresence[BasePresenceStatusCode] <> 192360004 )`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Agent login time](#agent-login-time), [Status duration](#status-duration), [Available duration](#available-duration).

### Available duration

Totals the time service representatives spent in the Available presence state. Use it to assess how much logged-in time was available for customer work.
<br>

- **Calculation:** `CALCULATE( SUM(AggAgentAvailability[StatusDurationInSeconds]), DimPresence[BasePresenceStatusCode] = 192360000 )`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Login duration](#login-duration), [Busy duration](#busy-duration), [Away duration](#away-duration).

### Average status changes per 30 minutes

Measures the average number of presence status changes per 30-minute interval. Use it to assess how often service representatives change availability states during the selected period.
<br>

- **Calculation:** `DIVIDE( SUM(AggAgentAvailability[StatusChangeCount]), SUM(AggAgentAvailability[StatusDurationInSeconds]) / 1800, BLANK() )`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Status duration](#status-duration), [Login duration](#login-duration).

### Agent login time

Measures logged-in time in hours. Use it to compare service representative availability across longer reporting periods.
<br>

- **Calculation:** `CALCULATE( SUM(AggAgentAvailability[StatusDurationInSeconds]) / 3600, DimPresence[BasePresenceStatusCode] <> 192360004 )`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Login duration](#login-duration), [Agent login time HH:MM:SS](#agent-login-time-hhmmss).

### Agent login time HH:MM:SS

Shows logged-in time as hours, minutes, and seconds. Hours can exceed 24, so 25 hours appears as `25:00:00`. If no duration is available, the result is blank. The formatted result is text, not a number.
<br>

- **Calculation:**

  ```dax
  VAR Duration =
      CALCULATE(
          SUM(AggAgentAvailability[StatusDurationInSeconds]),
          DimPresence[BasePresenceStatusCode] <> 192360004
      )
  VAR Hours = INT(Duration / 3600)
  VAR Minutes = INT(MOD(Duration, 3600) / 60)
  VAR Seconds = ROUND(MOD(Duration, 60), 0)
  RETURN
      IF(
          ISBLANK(Duration),
          BLANK(),
          FORMAT(Hours, "00") & ":"
              & FORMAT(Minutes, "00") & ":"
              & FORMAT(Seconds, "00")
      )
  ```

- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Login duration](#login-duration), [Agent login time](#agent-login-time).

### Status duration

Totals the time spent in the selected presence status. Apply presence filters to assess how service representatives distribute time across availability states.
<br>

- **Calculation:** `SUM(AggAgentAvailability[StatusDurationInSeconds])`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Available duration](#available-duration), [Busy duration](#busy-duration), [Away duration](#away-duration), [Offline duration](#offline-duration).

### Busy duration

Totals the time spent in the Busy presence state. Use it to assess how long service representatives were unavailable because they were actively working.
<br>

- **Calculation:** `CALCULATE( SUM(AggAgentAvailability[StatusDurationInSeconds]) / 3600, DimPresence[BasePresenceStatusCode] = 192360001 )`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Available duration](#available-duration), [Busy DND duration](#busy-dnd-duration), [Away duration](#away-duration).

### Busy DND duration

Totals the time spent in the Busy Do Not Disturb presence state. Use it to assess how long service representatives worked in a noninterruptible state.
<br>

- **Calculation:** `CALCULATE( SUM(AggAgentAvailability[StatusDurationInSeconds]) / 3600, DimPresence[BasePresenceStatusCode] = 192360002 )`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Busy duration](#busy-duration), [Available duration](#available-duration).

### Away duration

Totals the time spent in the Away presence state. Use it to assess how long service representatives were away from active contact center work.
<br>

- **Calculation:** `CALCULATE( SUM(AggAgentAvailability[StatusDurationInSeconds]) / 3600, DimPresence[BasePresenceStatusCode] = 192360003 )`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Available duration](#available-duration), [Busy duration](#busy-duration), [Offline duration](#offline-duration).

### Offline duration

Totals the time spent in the Offline presence state. Use it to assess time outside logged-in availability.
<br>

- **Calculation:** `CALCULATE( SUM(AggAgentAvailability[StatusDurationInSeconds]) / 3600, DimPresence[BasePresenceStatusCode] = 192360004 )`.
- **Source:** `AggAgentAvailability`.
- **Related metrics:** [Login duration](#login-duration), [Away duration](#away-duration).
