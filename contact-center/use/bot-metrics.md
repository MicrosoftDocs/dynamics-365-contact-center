---
title: Bot metrics reference for Shared Analytics Platform
description: Bot metric definitions and DAX measures for Shared Analytics Platform in Dynamics 365 Contact Center.
ms.date: 10/30/2026
ms.topic: reference
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-assisted
---

# Bot metrics reference for Shared Analytics Platform

Use bot metrics to review session performance, conversation outcomes, bot and topic participation, escalation attribution, and customer support journeys. Each reports at a different grain, so the counts aren't interchangeable.

> [!IMPORTANT]
> Session rates use all selected bot sessions, not just engaged sessions. Conversation metrics use separate conversation-outcome aggregates rather than a conversation-count column in `AggBotSession`. You can't use `FactBotSession` for supported reports or drill-through; it's private processing state.

## Session metrics

Use [AggBotSession](../extend/analytics/aggbotsession.md) for session measures. The names in the following table are semantic-model measure names.

| Measure | Definition | DAX calculation |
|---|---|---|
| Total Bot Sessions | Counts all selected bot sessions. | `SUM(AggBotSession[BotSessionCount])` |
| Engaged Sessions | Counts sessions whose source engagement is true. False and null contribute zero. | `SUM(AggBotSession[EngagedSessionCount])` |
| Unengaged Sessions | Subtracts engaged sessions from total sessions. | `[Total Bot Sessions] - [Engaged Sessions]` |
| Abandoned Sessions | Counts sessions with `SessionOutcome = 419550003`. | `SUM(AggBotSession[AbandonedSessionCount])` |
| Escalated Sessions | Counts sessions with `SessionOutcome = 419550002`. | `SUM(AggBotSession[EscalatedSessionCount])` |
| Resolved Sessions | Counts sessions with `SessionOutcome = 419550001`. | `SUM(AggBotSession[ResolvedSessionCount])` |
| Bot Engagement Rate (Session) | Divides engaged sessions by all sessions. | `DIVIDE([Engaged Sessions], [Total Bot Sessions], 0)` |
| Unengaged Session Rate | Divides unengaged sessions by all sessions. | `DIVIDE([Unengaged Sessions], [Total Bot Sessions], 0)` |
| Abandon Rate (Session) | Divides abandoned sessions by all sessions. | `DIVIDE([Abandoned Sessions], [Total Bot Sessions], 0)` |
| Escalation Rate (Session) | Divides escalated sessions by all sessions. | `DIVIDE([Escalated Sessions], [Total Bot Sessions], 0)` |
| Resolution Rate (Session) | Divides resolved sessions by all sessions. | `DIVIDE([Resolved Sessions], [Total Bot Sessions], 0)` |
| Avg Bot Time (min) | Measures weighted average bot-session duration, converted from seconds to minutes. | `DIVIDE(SUM(AggBotSession[TotalDurationInSeconds]), SUM(AggBotSession[DurationSessionCount]), BLANK()) / 60` |
| Avg Bot CSAT | Divides the stored score total by the count of scores greater than zero. | `DIVIDE(SUM(AggBotSession[TotalCSATScore]), SUM(AggBotSession[CSATResponseCount]), BLANK())` |

For a zero or blank denominator, session rates return zero; average duration and CSAT return blank.

Bot duration subtracts session start from session end when both timestamps exist. The calculation doesn't require a positive duration or enforce a maximum duration. For CSAT, null source scores contribute zero to the stored total, and the denominator counts scores greater than zero. The calculation doesn't enforce a score range.

Session counts have no additional engagement, closed-only, short-abandon, or queue-overflow restriction. Engagement and outcome series overlap, and outcome rates don't necessarily sum to 100%.

## Conversation metrics

Use conversation metrics to count distinct eligible conversations within the selected participation scope.

| Context | Aggregate used |
|---|---|
| Overall, without a bot restriction. | [AggConversationBotOutcome](../extend/analytics/aggconversationbotoutcome.md). |
| One participating bot. | [AggConversationBotOutcomeByBot](../extend/analytics/aggconversationbotoutcomebybot.md). |
| One participating bot and one topic. | [AggConversationBotOutcomeByBotTopic](../extend/analytics/aggconversationbotoutcomebybottopic.md). |

To be eligible, a conversation must have bot-session contributions and a known canonical conversation-created timestamp. Resolved Entity Records conversations with channel `192350000` and status `6` are excluded; unresolved Entity Records remain eligible. No general closed-only DAX filter applies.

### Total bot conversations

`Total Bot Conversations` selects the appropriate aggregate for your filter context rather than adding bot or topic rows:

```dax
VAR BotInScope = HASONEVALUE(DimBot[DimBotId])
VAR BotFiltered =
    ISFILTERED(DimBot[Bot])
        || ISFILTERED(DimBot[DimBotId])
VAR SharedTopicFiltered =
    ISCROSSFILTERED(DimBotTopic[BotTopicKey])
VAR SharedTopicInScope =
    SharedTopicFiltered
        && HASONEVALUE(DimBotTopic[BotTopicKey])
VAR SessionTopicFiltered =
    ISFILTERED(AggBotSession[BotTopicKey])
        || ISFILTERED(AggBotSession[BotTopicName])
VAR OutcomeTopicFiltered =
    ISFILTERED(AggConversationBotOutcomeByBotTopic[BotTopicKey])
VAR SessionTopicInScope =
    SessionTopicFiltered
        && HASONEVALUE(AggBotSession[BotTopicKey])
VAR OutcomeTopicInScope =
    OutcomeTopicFiltered
        && HASONEVALUE(AggConversationBotOutcomeByBotTopic[BotTopicKey])
RETURN
    SWITCH(
        TRUE(),
        SharedTopicInScope && BotInScope,
            SUM(AggConversationBotOutcomeByBotTopic[ConversationCount]),
        SharedTopicFiltered,
            BLANK(),
        SessionTopicInScope && BotInScope,
            CALCULATE(
                SUM(AggConversationBotOutcomeByBotTopic[ConversationCount]),
                TREATAS(
                    VALUES(AggBotSession[BotTopicKey]),
                    AggConversationBotOutcomeByBotTopic[BotTopicKey]
                )
            ),
        OutcomeTopicInScope && BotInScope,
            SUM(AggConversationBotOutcomeByBotTopic[ConversationCount]),
        SessionTopicFiltered || OutcomeTopicFiltered,
            BLANK(),
        BotFiltered && NOT(BotInScope),
            BLANK(),
        BotInScope,
            SUM(AggConversationBotOutcomeByBot[ConversationCount]),
        SUM(AggConversationBotOutcome[ConversationCount])
    )
```

Select one bot and one stable topic identity for topic analysis. Explicit multi-bot selections and unsupported topic contexts return blank.

### Conversation outcomes and rates

If any bot session escalated, the whole conversation is `Bot escalated`; otherwise, it's `Bot deflected`. Deflection can include abandonment, so don't interpret it as bot resolution.

`Conversation Deflected` filters all three routing targets by outcome:

```dax
CALCULATE(
    [Total Bot Conversations],
    AggConversationBotOutcome[ConversationOutcome] = "Bot deflected",
    AggConversationBotOutcomeByBot[ConversationOutcome] = "Bot deflected",
    AggConversationBotOutcomeByBotTopic[ConversationOutcome] = "Bot deflected"
)
```

For `Conversation Escalated`, the same calculation uses `"Bot escalated"` in all three filters.

| Measure | Calculation |
|---|---|
| Deflection Rate (Conversation) | `DIVIDE(COALESCE([Conversation Deflected], 0), [Total Bot Conversations], BLANK())` |
| Escalation Rate (Conversation) | `DIVIDE(COALESCE([Conversation Escalated], 0), [Total Bot Conversations], BLANK())` |
| Sessions per Conversation | `DIVIDE([Total Bot Sessions], [Total Bot Conversations], BLANK())` |

For a missing numerator, conversation rates return zero when an eligible denominator exists. A zero or blank denominator returns blank.

Session measures use bot-session time, while conversation measures use conversation creation time. Within a bounded date range, **Sessions per Conversation** doesn't necessarily average the same group of sessions and conversations.

### Average deflection and escalation time

`Avg Deflection Time (min)` divides routed `TotalOCSessionBotTimeMinutes` by routed `OCSessionBotTimeCount`, filtered to `Bot deflected`. `Avg Escalation Time (min)` uses the same division, filtered to `Bot escalated`. The hidden `_Routed Bot Time Minutes` and `_Routed Bot Time Count` measures follow the context routing of **Total Bot Conversations**, including returning blank for unsupported contexts.

For example, average deflection time uses this calculation:

```dax
DIVIDE(
    CALCULATE(
        [_Routed Bot Time Minutes],
        AggConversationBotOutcome[ConversationOutcome] = "Bot deflected",
        AggConversationBotOutcomeByBot[ConversationOutcome] = "Bot deflected",
        AggConversationBotOutcomeByBotTopic[ConversationOutcome] = "Bot deflected"
    ),
    CALCULATE(
        [_Routed Bot Time Count],
        AggConversationBotOutcome[ConversationOutcome] = "Bot deflected",
        AggConversationBotOutcomeByBot[ConversationOutcome] = "Bot deflected",
        AggConversationBotOutcomeByBotTopic[ConversationOutcome] = "Bot deflected"
    ),
    BLANK()
)
```

Use `"Bot escalated"` in all filters for average escalation time.

Each qualifying contribution uses the linked omnichannel session's creation-to-closure duration, converted to whole minutes before summation. The denominator counts qualifying bot-session contribution rows, not distinct conversations or omnichannel sessions. Repeated contributions each retain their duration weight. If either timestamp is missing, the contribution is excluded from both the total and the count.

Interpret these values as weighted linked-session durations, not necessarily elapsed time until handoff. A zero or blank duration denominator returns blank.

## Terminal outcome metrics

Terminal outcome describes the latest bot session in the whole conversation. Sessions are ordered by source creation time descending, effective start time descending, and `BotSessionId` descending. The terminal session can belong to a different bot or topic than the selected participant.

| Measure | DAX calculation |
|---|---|
| Terminal Outcome Conversations | `[Total Bot Conversations]` |
| Terminal Outcome Conversation % | `DIVIDE([Terminal Outcome Conversations], CALCULATE([Terminal Outcome Conversations], ALLSELECTED(DimBotTerminalOutcomeProperty)), 0)` |

Interpret the percentage as the category's share of the externally selected terminal population, not necessarily all bot conversations. A zero or blank denominator returns zero.

Don't equate terminal outcome and reason codes with session outcome codes in `AggBotSession`. Learn more in [DimBotTerminalOutcomeProperty table reference](../extend/analytics/DimBotTerminalOutcomeProperty.md).

## Escalation-topic metric

Use `Escalated Topic Conversations` to count conversations involving the selected participant bot and topic. Results are grouped by the topic that performed the last qualifying escalation:

```dax
VAR OneBot = HASONEVALUE(DimBot[DimBotId])
VAR OneTopic = HASONEVALUE(DimBotTopic[BotTopicKey])
VAR ExplicitBot = ISFILTERED(DimBot[DimBotId]) || ISFILTERED(DimBot[Bot])
VAR ExplicitTopic = ISFILTERED(DimBotTopic[BotTopicKey]) || ISFILTERED(DimBotTopic[BotTopicName])
RETURN
IF(OneBot && OneTopic && ExplicitBot && ExplicitTopic, SUM(AggBotEscalationTopic[ConversationCount]), BLANK())
```

Explicitly select exactly one bot and one topic; otherwise, the measure returns blank. The escalation target can belong to another bot. A later non-escalated session doesn't replace the last qualifying escalation. If the target identity is missing, it remains **Unknown**.

## Journey metric

Use `Journey Conversations` to measure the selected source-to-destination edge:

```dax
SUM(AggCustomerSupportJourney[ConversationCount])
```

The result is an edge weight, not report-wide distinct conversation volume; one conversation can produce several edges. The journey includes direct service representative paths and uses independent source logic. Bot and topic selections don't filter it.

Learn more in [AggCustomerSupportJourney table reference](../extend/analytics/aggcustomersupportjourney.md).

## Interpret totals, filters, and dates

Count scope matters: overall counts are distinct conversations, bot participation counts are distinct within each bot, and topic participation counts are distinct within each bot and topic. One conversation can appear under multiple participants. Don't sum participant rows to reconstruct overall totals or average their rates. Null-topic contributions also prevent named topic rows from reconstructing bot totals.

Conversation dimensions use the latest canonical conversation attributes, not those of the earliest bot session. Distinguish complete-conversation escalation from terminal outcome and the actual escalation topic.

All reporting uses a selected fixed GMT offset without daylight saving adjustments. Conversation and journey metrics use conversation creation time; session metrics use bot-session time. Use `_AggregationDate` as an import partition field, not a relationship to `DimDate.Date`.

The semantic model imports a rolling 24-month window with a two-month incremental refresh period. These settings don't guarantee producer data retention. Changing the report's date filter doesn't extend imported history.
