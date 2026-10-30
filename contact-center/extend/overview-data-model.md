---
title: Understand data model in 
description: Get an overview of data model in Shared Analytics Platform in Dynamics 365 Contact Center.
ms.date: 10/30/2026
author: gandhamm
ms.author: mgandham
ms.reviewer: gandhamm
ms.topic: overview
ms.collection:
ms.custom: bap-template
ai-usage: ai-assisted
---
# Understand data model in Shared Analytics Platform

The Contact Center historical analytics dashboards use the data model in Shared Analytics Platform
Shared Analytics Platform. The model transforms detailed interaction data into reporting-ready metrics.

## Data model architecture

This table summarizes the three primary table types and their role in reporting and analysis.

| Table type | Purpose |
|---|---|
| **Aggregate tables** | Store preaggregated totals and counts optimized for dashboards and trend analysis. |
| **Fact tables** | Store detailed operational and interaction data used for analysis and drill-through. |
| **Dimension tables** | Provide context for filtering, grouping, and interpreting metrics. |

Fact and aggregate tables are partitioned by date for efficient time-window queries. All timestamps are stored in UTC, and reporting tools use the `DimTimeZone` dimension for local time conversion.

## Understand contact center metrics

The following sections group metrics by area and show how each metric maps to its underlying data sources.

### Conversation

Conversation metrics show customer demand and interaction outcomes across channels.

| Aggregate table | Source fact table | Dimensions |
|---|---|---|
| [AggConversation](./analytics/aggconversation.md) | FactConversation | DimBusinessUnit, DimChannel, DimConversationDirection, DimConversationStatus, DimDate, DimQueue, DimTimeZone |

### Bot

Bot metrics show how bots and Copilot Studio agents engage customers, resolve or escalate sessions, deflect conversations, and affect customer satisfaction.

| Aggregate table | Source fact table | Dimensions |
|---|---|---|
| [AggBotSession](./analytics/aggbotsession.md) | [FactBotSession](./analytics/FactBotSession.md) | [DimBot](./analytics/DimBot.md), DimChannel, DimConversationDirection, DimConversationStatus, DimDate, DimQueue, DimTimeZone |

The expanded bot dashboard model separates session metrics, conversation outcomes, and customer-support journey analysis. Its additional table contracts are listed here.

| Table | Dashboard role |
|---|---|
| [AggConversationBotOutcome](./analytics/aggconversationbotoutcome.md) | Overall conversation counts, deflection, escalation, and terminal outcomes. |
| [AggConversationBotOutcomeByBot](./analytics/aggconversationbotoutcomebybot.md) | Conversation measures for one participating bot. |
| [AggConversationBotOutcomeByBotTopic](./analytics/aggconversationbotoutcomebybottopic.md) | Conversation measures for one participating bot and topic. |
| [AggCustomerSupportJourney](./analytics/aggcustomersupportjourney.md) | Source-to-destination journey counts. |
| [DimBotTopic](./analytics/DimBotTopic.md) | Shared topic identity and labels. |
| [DimBotTerminalOutcomeProperty](./analytics/DimBotTerminalOutcomeProperty.md) | Localized terminal outcome, reason, and reason-group labels. |

#### Bot table availability

The baseline bot pipeline schema and registered generators produce `DimBot`, `FactBotSession`, and `AggBotSession`. The preceding table's additional dashboard contracts aren't defined by those generators. The dashboard also expects `ConversationTypeCode`, `BotTopicKey`, and `BotTopicId` on `AggBotSession`, which the baseline pipeline schema doesn't provide.

These references distinguish the generated pipeline schema from the expanded dashboard model contract. They don't establish that your environment provisions or makes available the additional tables or columns for custom reporting. Confirm the published table schemas and supported access before building reports or Fabric integrations.

The dashboard model imports aggregates and dimensions, not `FactBotSession` or a conversation-detail fact. Its date filtering uses a UTC proxy and time-zone conversion path; partition dates aren't direct relationships to `DimDate.Date`. Conversation participation counts aren't additive across bots or topics, so use the model's routed conversation measures.

### Queue

Queue metrics show queue-level performance for wait time, service level, abandonment, and transfers.

| Aggregate table | Source fact table | Dimensions |
|---|---|---|
| [AggQueuePerformance](./analytics/aggqueueperformance.md) | [FactQueueSegment](./analytics/FactQueueSegment.md) | DimBusinessUnit, DimChannel, DimConversationStatus, DimConversationDirection, DimDate, DimQueue, DimTimeZone |

### Service representative performance

These metrics show how service representatives handle sessions and manage workload over time.

| Aggregate table | Source fact table | Dimensions |
|---|---|---|
| [AggAgentPerformance](./analytics/aggagentperformance.md) | FactSession, FactSessionParticipant, FactConversation | DimBusinessUnit, DimChannel, DimConversationDirection, DimConversationStatus, DimDate, DimParticipantMode, DimQueue, DimTimeZone, DimSystemUser |

### Availability and capacity

Availability and capacity metrics show agent readiness and workload capacity to support staffing and operational planning.

| Aggregate table | Source fact table | Dimensions |
|---|---|---|
| [AggAgentAvailability](./analytics/aggagentavailability.md) | FactAgentStatusHistory | DimBusinessUnit, DimDate, DimPresence, DimSystemUser, DimTimeZone |
| [AggAgentCapacity](./analytics/AggAgentCapacity.md) | FactAgentCapacityHistory | DimBusinessUnit, DimCapacityProfile, DimDate, DimTimeZone |

### Voice insights

Voice insight metrics use AI to analyze conversation behavior. Use them primarily for coaching and quality review.

| Aggregate table | Source fact table | Dimensions |
|---|---|---|
| [AggVoiceConversationInsights](./analytics/aggvoiceconversationinsights.md) | FactVoiceConversationInsights, FactConversation | DimBusinessUnit, DimChannel, DimConversationDirection, DimConversationStatus, DimDate, DimQueue, DimTimeZone |

### Quality and sentiment

Quality and sentiment metrics combine survey feedback with AI-derived signals to measure customer experience across interactions. These metrics come from `FactConversation` and appear through aggregate tables such as `AggConversation`, `AggQueuePerformance`, and `AggAgentPerformance`.
