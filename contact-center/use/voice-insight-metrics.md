---
title: Voice insight metrics reference for Contact Center historical analytics
description: Explore voice insight metric definitions and DAX measures for Shared Analytics Platform in Dynamics 365 Contact Center, including speaking speed and talk-to-listen ratio.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---
# Voice insight metrics reference for Contact Center historical analytics

Use voice insight metrics for coaching-oriented analysis when voice conversation insights are available. The metrics provide AI-generated behavioral insights about voice conversations.

Use voice insight metrics to answer conversation quality and engagement questions such as:

- How long did customers speak without interruption?
- How long did service representatives pause before responding?
- How frequently did speakers switch during conversations?
- How quickly did service representatives speak?
- What was the balance between service representative talk time and listen time?
- How many voice insight records contributed to the averages?

## Metrics

All metrics use `AggVoiceConversationInsights`, sourced from `FactVoiceConversationInsights` joined to `FactConversation`. The join supplies queue, channel, status, direction, business unit, and active agent dimensions. Averages divide summed values by `VoiceInsightCount` and return blank when that count is zero or blank.

### Avg longest customer monologue

Measures the average longest uninterrupted customer speech duration in voice conversations. Use it to identify calls where customers speak for long periods without interruption.
<br>

- **Appears on:** Voice insights, coaching, and custom reports.
- **Calculation:** `DIVIDE(SUM(AggVoiceConversationInsights[TotalLongestCustomerMonologueInSeconds]), SUM(AggVoiceConversationInsights[VoiceInsightCount]), BLANK()).`
- **Source:** `AggVoiceConversationInsights`.
- **Related metrics:** [Avg pause before speaking](#avg-pause-before-speaking), [Avg switches per conversation](#avg-switches-per-conversation).

### Avg pause before speaking

Measures the average service representative pause before responding in voice conversations. Use it to identify response delays.
<br>

- **Appears on:** Voice insights, coaching, and custom reports.
- **Calculation:** `DIVIDE(SUM(AggVoiceConversationInsights[TotalPauseBeforeSpeakingInSeconds]), SUM(AggVoiceConversationInsights[VoiceInsightCount]), BLANK()).`
- **Source:** `AggVoiceConversationInsights`.
- **Related metrics:** [Avg longest customer monologue](#avg-longest-customer-monologue), [Avg talk-to-listen ratio](#avg-talk-to-listen-ratio).

### Avg switches per conversation

Measures the average number of speaker turn switches in voice conversations. Use it to assess conversation flow and interaction balance.
<br>

- **Appears on:** Voice insights, coaching, and custom reports.
- **Calculation:** `DIVIDE(SUM(AggVoiceConversationInsights[TotalSwitchesPerConversation]), SUM(AggVoiceConversationInsights[VoiceInsightCount]), BLANK()).`
- **Source:** `AggVoiceConversationInsights`.
- **Related metrics:** [Avg talk-to-listen ratio](#avg-talk-to-listen-ratio), [Avg talking speed](#avg-talking-speed).

### Avg talking speed

Measures the average service representative speaking speed in words per minute. Use it to identify conversations where speaking speed might affect customer understanding.
<br>

- **Appears on:** Voice insights, coaching, and custom reports.
- **Calculation:** `DIVIDE(SUM(AggVoiceConversationInsights[TotalTalkingSpeed]), SUM(AggVoiceConversationInsights[VoiceInsightCount]), BLANK()).`
- **Source:** `AggVoiceConversationInsights`.
- **Related metrics:** [Avg talk-to-listen ratio](#avg-talk-to-listen-ratio), [Avg pause before speaking](#avg-pause-before-speaking).

### Avg talk-to-listen ratio

Measures the average ratio of service representative talk time to listen time. Use it to assess the balance between speaking and listening.
<br>

- **Appears on:** Voice insights, coaching, and custom reports.
- **Calculation:** `DIVIDE(SUM(AggVoiceConversationInsights[TotalTalkToListenRatio]), SUM(AggVoiceConversationInsights[VoiceInsightCount]), BLANK()).`
- **Source:** `AggVoiceConversationInsights`.
- **Related metrics:** [Avg talking speed](#avg-talking-speed), [Avg switches per conversation](#avg-switches-per-conversation).

### Voice insight count

Counts voice insight records used as the denominator for voice insight averages. Use it to see how many voice conversations contributed to coaching-oriented voice insight metrics.
<br>

- **Appears on:** Voice insights, coaching, and custom reports.
- **Calculation:** `SUM(AggVoiceConversationInsights[VoiceInsightCount]).`
- **Source:** `AggVoiceConversationInsights`.
- **Related metrics:** [Avg longest customer monologue](#avg-longest-customer-monologue), [Avg pause before speaking](#avg-pause-before-speaking), [Avg talking speed](#avg-talking-speed).
