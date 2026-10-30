---
title: Conversation metrics reference for Shared Analytics Platform
description: Conversation metric definitions and DAX measures for Shared Analytics Platform.
ms.date: 10/30/2026
ms.topic: reference
author: mgandham
ms.author: mgandham
ai-usage: ai-assisted
---

# Conversation metrics reference for Shared Analytics Platform

Use conversation metrics to monitor customer interaction volume, engagement, service performance, and customer experience outcomes over time.

## Conversation metrics

These metrics report at the conversation level, representing a customer interaction and its outcome. They're commonly used in the Conversation dashboard and historical analytics reports to assess overall contact center performance, customer experience, and operational efficiency.

Use them to review conversation demand, interaction trends, and service levels, and to answer questions such as:

- How many customer conversations were received during a specific period?
- How many conversations were engaged, abandoned, or transferred?
- How quickly were customers connected to a service representative?
- Are service-level objectives being met?
- How are customer satisfaction, sentiment, and other experience indicators trending over time?

The following definitions explain what each metric measures and how to interpret it in historical analytics reports.

### Incoming conversations

Counts inbound customer conversations offered to a service representative queue. Use it to measure inbound workload and queue demand, and to calculate service-level, engagement, abandonment, and wait-time metrics. The `IsOffered` flag uses `msdyn_isagentsession = 1` and `ConversationDirectionCode = 0`, excluding outbound and agent-only conversations.

- **Calculation:** `SUM([IncomingConversations])`.
- **Source:** `AggConversation`; Column: `IncomingConversations = SUM(CASE IsOffered = 1)`. Fact-level derivation: `IsOffered` is based on `msdyn_isagentsession = 1` and `ConversationDirectionCode = 0`.
- **Related metrics:** [Engaged conversations](#engaged-conversations), Abandoned conversations, [Service level %](#service-level-), [Engagement rate](#engagement-rate), Abandon rate, [Avg wait time](#avg-wait-time).

### Engaged conversations

Counts inbound conversations accepted by a service representative. Use it to measure how much inbound demand reached a representative and to calculate handling-time and responsiveness averages.

- **Calculation:** `SUM([EngagedConversations])`.
- **Source:** `AggConversation`; Column: `EngagedConversations = SUM(CASE IsEngaged = 1)`. Fact-level derivation: `IsEngaged` is based on `IsOffered = 1` and `IsAgentAccepted = 1`.
- **Related metrics:** [Incoming conversations](#incoming-conversations), Abandoned conversations, [Engagement rate](#engagement-rate), [Avg handle time](#avg-handle-time), [Avg speed of answer](#avg-speed-of-answer).

### Bot conversations

The total number of conversations where an agent participated at any point. Use this metric to understand automation volume, including conversations handled by an agent, escalated from an agent to a service representative, or handled by both.

- **Calculation:** `SUM([BotConversations])`.
- **Source:** `AggConversation`; Column: `BotConversations = SUM(CASE IsBotInvolved = 1)`.
- **Related metrics:** [Incoming conversations](#incoming-conversations), [Engaged conversations](#engaged-conversations), [Callback conversations](#callback-conversations).

### Callback conversations

Counts conversations routed to a callback because of overflow. Use it to see how often capacity, routing, or overflow settings move customers from waiting in a queue to a callback.

- **Calculation:** `SUM([CallbackConversations])`.
- **Source:** `AggConversation`; Column: `CallbackConversations = SUM(CASE IsCallback = 1)`. Derived from overflow/session extension logic in the fact layer.
- **Related metrics:** [Incoming conversations](#incoming-conversations), Callbacks offered, Callbacks opted in, Callbacks answered.

### Outgoing conversations

Counts outbound conversations started by a service representative. Track this proactive or follow-up work separately from inbound queue demand.

- **Calculation:** `SUM([OutgoingConversations])`.
- **Source:** `AggConversation`; Column: `OutgoingConversations = SUM(CASE ConversationDirectionCode = 1)`.
- **Related metrics:** [Incoming conversations](#incoming-conversations), Total conversations.

### Service level %

The percentage of incoming conversations that met the configured service-level threshold. Use this metric to measure whether customers who entered service representative routing were answered within the expected wait-time target.

- **Calculation:** `[InSLAConversations] / [Incoming Conversations]`.
- **Source:** `AggConversation`; Column: `InSLAConversations = SUM(CASE IsInServiceLevel = 1)`. Queue threshold comes from DimQueue at ETL time.
- **Related metrics:** [Incoming conversations](#incoming-conversations), [Engaged conversations](#engaged-conversations), [Avg speed of answer](#avg-speed-of-answer), [Service level including abandons %](#service-level-including-abandons-), [Conversations answered in X sec](#conversations-answered-in-x-sec).

### Transfer rate

Shows the percentage of incoming conversations transferred at least once. Use it to identify routing complexity, missing skills, incorrect queue assignments, or journeys that require multiple queues or service representatives.

- **Calculation:** `[TransferredConversations] / [Incoming Conversations]`.
- **Source:** `AggConversation`; Column: `TransferredConversations = SUM(CASE TransferCount > 0)`.
- **Related metrics:** Transferred conversations, [Incoming conversations](#incoming-conversations), [Avg handle time](#avg-handle-time).

### Engagement rate

Shows the percentage of incoming conversations accepted by a service representative. Use it to compare inbound demand that connected to a representative with demand that was abandoned or not engaged.

- **Calculation:** `[Engaged Conversations] / [Incoming Conversations]`.
- **Source:** `AggConversation`.
- **Related metrics:** [Incoming conversations](#incoming-conversations), [Engaged conversations](#engaged-conversations), Abandoned conversations, Abandon rate.

### Avg speed of answer

Measures the average time from queue entry to first acceptance by a service representative for engaged conversations. Use it to assess how quickly customers reach a representative after entering a queue.

- **Calculation:** `[TotalSpeedToAnswerInSeconds] / [Engaged Conversations]`.
- **Source:** `AggConversation`; Column: `TotalSpeedToAnswerInSeconds = SUM(SpeedToAnswerTimeInSeconds)`.
- **Related metrics:** [Service level %](#service-level-), [Avg wait time](#avg-wait-time), Abandon rate.

### Avg handle time

Measures the average handling duration for engaged conversations. Use it to assess the effort needed to complete interactions and identify complexity, coaching needs, or process gaps.

- **Calculation:** `[TotalHandleTimeInSeconds] / [Engaged Conversations]`.
- **Source:** `AggConversation`; Column: `TotalHandleTimeInSeconds = SUM(HandleTimeInSeconds)`.
- **Related metrics:** [Avg talk time](#avg-talk-time), [Avg hold time](#avg-hold-time), [Avg wrapup time](#avg-wrapup-time), [Engaged conversations](#engaged-conversations).

### Avg talk time

Measures the average voice talk time for engaged conversations. This is active speaking time between customers and service representatives, separate from hold and wrap-up time.

- **Calculation:** `[TotalTalkTimeInSeconds] / [Engaged Conversations]`.
- **Source:** `AggConversation`; Column: `TotalTalkTimeInSeconds = SUM(TalkTimeInSeconds)`.
- **Related metrics:** [Avg handle time](#avg-handle-time), [Avg hold time](#avg-hold-time).

### Avg hold time

Measures the average customer hold time during engaged voice conversations. Use it to identify delays while service representatives research information, wait for help, or complete related tasks.

- **Calculation:** `[TotalHoldTimeInSeconds] / [Engaged Conversations]`.
- **Source:** `AggConversation`; Column: `TotalHoldTimeInSeconds = SUM(HoldTimeInSeconds)`.
- **Related metrics:** [Avg talk time](#avg-talk-time), [Avg handle time](#avg-handle-time).

### Avg wrapup time

Measures the average post-interaction wrap-up time for engaged conversations. This covers work after a conversation, such as notes, disposition, classification, or case updates.

- **Calculation:** `[TotalWrapupTimeInSeconds] / [Engaged Conversations]`.
- **Source:** `AggConversation`; Column: `TotalWrapupTimeInSeconds = SUM(WrapupTimeInSeconds)`.
- **Related metrics:** [Avg handle time](#avg-handle-time), [Avg active wrapup time](#avg-active-wrapup-time).

### Avg wait time

Measures the average customer wait time for incoming conversations. Assess queue responsiveness alongside service level, speed of answer, and abandonment metrics.

- **Calculation:** `[TotalWaitTimeInSeconds] / [Incoming Conversations]`.
- **Source:** `AggConversation`.
- **Related metrics:** [Avg speed of answer](#avg-speed-of-answer), Abandon rate, [Service level %](#service-level-).

### Avg response time

Measures the average service representative response time across customer-to-representative message exchanges. For digital messaging, use it to assess ongoing responsiveness after engagement.

- **Calculation:** `[TotalResponseTimeInSeconds] / [MessageBlockCount]`.
- **Source:** `AggConversation`; Columns: `TotalResponseTimeInSeconds` and `MessageBlockCount`.
- **Related metrics:** [Avg first response time](#avg-first-response-time), [Incoming messages](#incoming-messages), [Outgoing messages](#outgoing-messages).

### Avg first response time

Measures the average time to the first service representative response. For digital messaging, use it to assess how quickly customers receive a reply after the interaction starts.

- **Calculation:** `[TotalFirstResponseTimeInSeconds] / [RespondedConversations]`.
- **Source:** `AggConversation`; Column: `TotalFirstResponseTimeInSeconds = SUM(FirstResponseTimeInSeconds)`. `RespondedConversations` counts conversations where the service representative sent a response.
- **Related metrics:** [Avg response time](#avg-response-time), Responded conversations.

### Avg customer effort

Measures the average customer effort duration for engaged conversations. Use it to identify interactions that require more customer time or effort and might indicate friction in the service journey.

- **Calculation:** `[TotalCustomerEffortInSeconds] / [Engaged Conversations]`.
- **Source:** `AggConversation`; Column: `TotalCustomerEffortInSeconds = SUM(CustomerEffortInSeconds)`.
- **Related metrics:** [Avg handle time](#avg-handle-time), [Engaged conversations](#engaged-conversations).

### Customer satisfaction

Measures the average CSAT score from survey responses. It reflects satisfaction for conversations where customers submitted feedback.

- **Calculation:** `[Survey_TotalCSATScore] / [Survey_CSATResponseCount]`.
- **Source:** `AggConversation`; Columns: `Survey_TotalCSATScore` and `Survey_CSATResponseCount`.
- **Related metrics:** [Net promoter score](#net-promoter-score), [Avg sentiment pulse](#avg-sentiment-pulse), [Avg survey sentiment](#avg-survey-sentiment).

### Net promoter score

Measures the average NPS from survey responses. It reflects customer advocacy or likelihood to recommend for conversations with submitted NPS feedback.

- **Calculation:** `[Survey_TotalNPSScore] / [Survey_NPSResponseCount]`.
- **Source:** `AggConversation`; Columns: `Survey_TotalNPSScore` and `Survey_NPSResponseCount`.
- **Related metrics:** [Customer satisfaction](#customer-satisfaction), [Avg sentiment pulse](#avg-sentiment-pulse), [Avg survey sentiment](#avg-survey-sentiment).

### Avg sentiment pulse

Measures the average AI-derived sentiment pulse across conversations. Treat it as a directional indicator of customer sentiment and compare it with survey-based CSAT and NPS.

- **Calculation:** `[TotalSentimentPulse] / [SentimentPulseCount]`.
- **Source:** `AggConversation`; Columns: `TotalSentimentPulse` and `SentimentPulseCount`.
- **Related metrics:** [Customer satisfaction](#customer-satisfaction), [Net promoter score](#net-promoter-score), [Avg survey sentiment](#avg-survey-sentiment).

### Avg survey sentiment

Measures the average sentiment from survey responses. Use it to relate structured post-conversation feedback to broader quality trends.

- **Calculation:** `[Survey_TotalSentimentScore] / [Survey_SentimentScoreCount]`.
- **Source:** `AggConversation`; Columns: `Survey_TotalSentimentScore` and `Survey_SentimentScoreCount`.
- **Related metrics:** [Customer satisfaction](#customer-satisfaction), [Net promoter score](#net-promoter-score), [Avg sentiment pulse](#avg-sentiment-pulse).

### Avg active chat time

Measures the average active chat time for engaged conversations: how long service representatives actively engage with customers in chat.

- **Calculation:** `[TotalActiveChatTimeInSeconds] / [Engaged Conversations]`.
- **Source:** `AggConversation`; Column: `TotalActiveChatTimeInSeconds = SUM(ActiveChatTimeInSeconds)`.
- **Related metrics:** [Avg handle time](#avg-handle-time), [Incoming messages](#incoming-messages), [Outgoing messages](#outgoing-messages).

### Avg active wrapup time

Measures the average active wrap-up time for engaged conversations. Use it to assess how wrap-up activity affects service representative capacity after conversations end.

- **Calculation:** `[TotalActiveWrapupTimeInSeconds] / [Engaged Conversations]`.
- **Source:** `AggConversation`; Column: `TotalActiveWrapupTimeInSeconds = SUM(ActiveWrapupTimeInSeconds)`.
- **Related metrics:** [Avg wrapup time](#avg-wrapup-time), [Avg handle time](#avg-handle-time).

### Incoming messages

Counts incoming customer messages in conversations. For digital channels, use it to assess customer message volume and workload intensity.

- **Calculation:** `SUM([TotalIncomingMessages])`.
- **Source:** `AggConversation`; Column: `TotalIncomingMessages`.
- **Related metrics:** [Outgoing messages](#outgoing-messages), [Avg response time](#avg-response-time).

### Outgoing messages

Counts outgoing service representative messages in conversations. For digital channels, use it to assess representative response volume.

- **Calculation:** `SUM([TotalOutgoingMessages])`.
- **Source:** `AggConversation`; Column: `TotalOutgoingMessages`.
- **Related metrics:** [Incoming messages](#incoming-messages), [Avg response time](#avg-response-time).

### Service level including abandons %

The percentage of incoming conversations answered within the SLA target while accounting for abandoned conversations. Use this metric when you need a stricter measure of service-level performance.

- **Calculation:** `[InSLAConversations] / [Incoming Conversations]`.
- **Source:** `AggConversation`.
- **Related metrics:** [Service level %](#service-level-), [Incoming conversations](#incoming-conversations), Abandoned conversations.

### Conversations answered in X sec

Counts engaged conversations answered within a specific threshold, such as 10, 20, 30, 40, 50, 60, or 120 seconds. Compare the wait-time buckets to assess the answer-time distribution.

- **Calculation:** `SUM([AnsweredInXSec])`—7 count measures.
- **Source:** `AggConversation`; Columns: `AnsweredIn10Sec`, `AnsweredIn20Sec`, `AnsweredIn30Sec`, `AnsweredIn40Sec`, `AnsweredIn50Sec`, `AnsweredIn60Sec`, `AnsweredIn120Sec`.
- **Related metrics:** [Service level at X sec %](#service-level-at-x-sec-), [Avg speed of answer](#avg-speed-of-answer).

### Service level at X sec %

Shows the percentage of engaged conversations answered within a selected threshold bucket. Compare the thresholds to assess responsiveness.

- **Calculation:** `[Conversations Answered in X Sec] / [Engaged Conversations]`—7 rate measures.
- **Source:** `AggConversation`.
- **Related metrics:** [Conversations answered in X sec](#conversations-answered-in-x-sec), [Service level %](#service-level-).

### Short abandon rate

Shows the percentage of incoming conversations abandoned within the short-abandon threshold. Use it to distinguish quick disconnects from longer waits that might need operational action.

- **Calculation:** `[Short Abandoned Conversations] / [Incoming Conversations]`.
- **Source:** `AggConversation`; Column: `ShortAbandonedConversations = SUM(CASE IsShortAbandoned = 1)`.
- **Related metrics:** Short abandoned conversations, Abandon rate, [Incoming conversations](#incoming-conversations).

### Incoming conversations excluding short abandons

Counts incoming conversations after removing short-abandoned conversations. Use it when your reporting policy excludes short abandons from abandonment analysis.

- **Calculation:** `[Incoming Conversations] - [Short Abandoned Conversations]`.
- **Source:** `AggConversation`.
- **Related metrics:** [Incoming conversations](#incoming-conversations), Short abandoned conversations, Abandon rate excluding short abandons.
