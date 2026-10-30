---
title: Bot dashboard
description: Learn how to use the bot dashboard in Dynamics 365 Contact Center historical analytics.
ms.date: 10/30/2026
ms.topic: concept-article
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ai-usage: ai-assisted
---

# Bot dashboard

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]

Use the **Bot** dashboard to review how bots and Copilot Studio agents perform across customer conversations. Monitor conversation volume, engagement, resolution, abandonment, deflection, escalation, duration, and customer satisfaction.

A conversation can include multiple bot sessions and more than one bot or topic. To distinguish these measures, the dashboard reports session performance, conversation outcomes, and bot participation separately.

> [!IMPORTANT]
> Standard bot historical analytics reports aggregate data. This report doesn't provide advanced bot analytics, intent analysis, individual conversation and session records, transcripts, transcript downloads, or custom reporting-variable detail. Drill-through opens aggregate detail pages, not individual records.

## Prerequisite

Your administrator must make the report and its reporting data available. Historical data must be processed and the semantic model refreshed before the data appears in the report. 

## Filter the dashboard

On the **Bot** overview page, use these filters to focus the report.

| Filter | Description |
|---|---|
| **Duration** | Select reporting dates within the history already imported into the model. |
| **Time zone** | Select one fixed GMT offset. The default is GMT. Offsets don't adjust for daylight saving time. |
| **Channel** | Filter by communication channel. |
| **Queue** | Filter by queue. |
| **Conversation status** | Filter by conversation status. |
| **Bot** | View results for all bots, or select a specific bot to see its performance. Use **Metrics by bot** to compare performance across bots. |

Your selected time zone applies to all five report pages. Detail pages keep the filters and selections used to open them. Conversation direction and conversation type are part of the underlying data model but aren't available as page filters.

Selecting multiple bots might leave conversation metrics blank. To analyze a topic, select one bot and one topic.

## Key performance indicators

Review conversation-level and session-level KPIs together on the overview page.

| KPI | Grain | Description |
|---|---|---|
| **Total bot conversations** | Conversation | Counts distinct eligible conversations that include a bot. When you select one bot, counts conversations in which that bot participated. |
| **Bot escalation rate** | Conversation | Percentage of bot conversations in which any bot session escalated. The selected bot doesn't have to be the bot that escalated. |
| **Bot deflection rate** | Conversation | Percentage of bot conversations in which no bot session escalated. Includes resolved and abandoned interactions. |
| **Total bot sessions** | Session | Counts bot sessions in the selected period. |
| **Bot engagement rate** | Session | Engaged sessions divided by all bot sessions. |
| **Bot resolution rate** | Session | Resolved sessions divided by all bot sessions. |
| **Bot abandon rate** | Session | Abandoned sessions divided by all bot sessions. |
| **Bot CSAT** | Session | Stored satisfaction-score total divided by the number of scores greater than zero. |

Session outcome rates use all bot sessions, not just engaged sessions, and can differ from similarly named Copilot Studio metrics. Don't assume a blank conversation rate means zero: it can mean there's no eligible population or the selection isn't supported.

Learn more in [Bot metrics reference for Shared Analytics Platform](bot-metrics.md).

## Review trends and terminal outcomes

Use trend and breakdown visuals to review performance changes and terminal outcomes.

| Visualization | Description |
|---|---|
| **Total bot conversations over time** | Deflected and escalated conversation counts by date. |
| **Bot session engagement over time** | Engaged and unengaged session counts by date. |
| **Bot session outcomes over time** | Resolution, abandonment, and escalation rates, each divided by all bot sessions. |
| **Engagement outcome distribution** | Groups conversation counts by the last bot session's outcome. Despite its name, this isn't an engaged-session distribution. |
| **Metrics by last-session outcome** | Conversation counts and percentages by terminal outcome and reason group. |

Don't add engagement and outcome values together because they overlap. Session outcome percentages might not total 100%.

The last-session breakdown shows the most recent bot session in each conversation, even if it involves a different bot or topic than the one you selected. Reasons include no user engagement, failures, user exit, requested by user, business rule, maximum attempts, maximum silence detected, and resolved.

## Compare metrics by bot

Compare participating bots in **Metrics by bot**, using the **Summary** or **Details** view.

| View | Columns |
|---|---|
| **Summary** | **Bot**, **Total conversations**, **Conversations escalated**, **Bot escalation rate**, **Avg. escalation time (min)**, **Conversations deflected**, **Bot deflection rate**, **Avg. deflection time (min)**, and **Bot CSAT**. |
| **Details** | **Total sessions**, **Bot sessions engaged**, **Engaged session rate**, **Bot sessions escalated**, **Escalated session rate**, **Bot sessions resolved**, **Resolved session rate**, **Bot sessions abandoned**, **Abandoned session rate**, **Bot sessions per conversation**, and **Avg. bot time (min)**. |

A conversation that involves two bots can appear in both bot rows but counts only once in the overall total.
Average escalation and deflection times measure how long linked omnichannel sessions last, from creation to closure. Each session's weight in the average depends on its qualifying bot-session contributions. Average escalation time doesn't necessarily show how long a customer waits for a handoff.

### Open bot details

1. In **Metrics by bot**, select the bot you want.
2. Select the table's **Details** drill-through action.
3. Verify the bot heading and retained filters.

Use the drill-through action, not the table's **Summary** and **Details** view controls, to open **Bot Details**.

On **Bot Details**, review the bot's KPIs, conversation and session trends, terminal-outcome breakdown, and **Metrics by bot topic**. The topic table shows **Bot topic**, **Total Bot Sessions**, **Bot escalation rate**, **Bot resolution rate**, and **Bot abandon rate**. These topic rates use all sessions for the topic.

### Open topic detail

To investigate a topic:

1. On **Bot Details**, select a topic in **Metrics by bot topic**.
2. Select **Details**.
3. Verify the retained bot and topic context.

On **Topic Detail**, review session volume, engagement, resolution, abandonment, conversation deflection and escalation rates, CSAT, and session trends. The page doesn't include a total-conversations card or individual conversation records.

Use **Conversation topics on bot escalation** to identify the topic that performed the last actual bot escalation in conversations involving the selected participant bot and topic. The table shows **Bot escalated topic** and **Total conversations**. The escalation topic can belong to another bot.

An **Unknown** escalation topic means the selected escalation session has missing bot or topic identity. A later non-escalated session doesn't replace the actual escalation, and an earlier known topic doesn't replace that unknown escalation topic.

## Review daily and hourly metrics

In **Bot metrics by date**, choose a conversation **Summary** or session **Details**.

- **Summary** shows conversation counts, escalated and deflected counts and rates, and average escalation and deflection times.
- **Details** shows total sessions and engaged, escalated, resolved, and abandoned session counts and rates.

To open the corresponding hourly page, select a date or data cell, and then select **Hourly details**.

| Page | Time basis | Content |
|---|---|---|
| **Bot hourly conversation** | Conversation creation time. | Conversation counts, escalated and deflected counts and rates, and average durations. |
| **Bot hourly session** | Bot-session time. | Session counts and engaged, resolved, abandoned, and escalated counts and rates. |

Both hourly pages display half-hour intervals, despite their names. Each provides **Bot**, **Channel**, **Queue**, and **Time zone** filters. A session after midnight can appear on a different date from the conversation's creation date.

## Review the customer support journey

Use the customer support journey visual to review transitions such as bot initiation, bot engagement, resolution, escalation, service representative assignment, engagement, and abandonment. It includes both direct connections to service representatives and bot-involved paths.

Each value counts conversations that produce a source-to-destination transition. Don't add all transition values to calculate distinct conversations: one conversation can produce several transitions. The journey uses separate source logic and isn't filtered by bot or topic selection.
