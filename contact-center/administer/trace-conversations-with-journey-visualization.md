---
title: Trace conversations with Journey Visualization (preview)
description: Use Journey Visualization in Contact Center Admin Workspace to trace past conversations and review routing decisions, transfers, and outcomes.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.date: 11/13/2026
ai-usage: ai-assisted
---

# Trace conversations with Journey Visualization (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Journey Visualization shows the path of a past conversation on the same canvas as your configuration, from arrival to completion. Use it to investigate what happened to a conversation and why each routing decision was made.

Journey Visualization supports voice and messaging conversations.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/production-ready-preview-dynamics365.md)]

## Prerequisites

[!INCLUDE [admin-workspace-prerequisites](../includes/admin-workspace-prerequisites.md)]

Optionally, to see recorded classification and route-to-queue results, set up conversation diagnostics in Application Insights. Learn more in [Understand conversation diagnostics](/dynamics365/customer-service/administer/conversation-diagnostics-subscenarios).

## Find a conversation

By default, the system displays 50 conversations based on the filter that you select.

1. Open [Contact Center Admin Workspace](contact-center-admin-workspace-overview.md#open-contact-center-admin-workspace), and select **Journey Visualization** in the left navigation pane.

1. In **Business unit**, select the business unit that owns the workstream for the conversation.
1. Find the conversation by ID or by using filters:

   | Search method | Details |
   |---|---|
   | Conversation ID | Enter an ID in **Search by conversation ID**. A full ID opens the trace immediately. |
   | Filters | Use **Time range**, **Channels**, **Queues**, and **Representatives**. Each filter except **Time range** also has an **Unassigned** option. |

1. Select a conversation to trace it.

## Read the trace and routing decisions

The canvas highlights the conversation path and dims the configuration it didn't use. The timeline beside it lists each step in order. Select a decision step in the timeline or on the canvas to see how it was evaluated.

| Step | What you see |
|---|---|
| Arrival | The channel and channel instance where the conversation arrived. |
| Workstream | The workstream and any AI agent who answered first. |
| Classification | Every rule in the rule set, in run order. Each rule shows whether it matched, had no match, or was skipped after a match, with the observed value, condition, and output it sets. Applied enrichment outputs are listed at the end. |
| Route-to-queue | Each rule in order, whether it matched, the observed value compared with the condition, the selected queue, and whether the fallback queue is used. |
| Overflow | Diversion before the conversation entered a queue or a transfer from inside a queue. Decision details show the evaluated condition-action pairs, expected versus observed values, the action taken, and the destination. |
| Assignment | Which representative accepted the conversation. Expand a queue's **Representatives** to see rejected or timed-out offers on each representative's card. |
| Transfers | Queue transfers and representative transfers. |
| Consults | When a consult was requested and when participants joined and left. |
| Outcome |  How the conversation ended. For example, if a representative closed it or customer abandoned it. |

If a representative isn't involved, the trace shows the AI-agent-only path.

:::image type="content" source="../media/journey-visualization-trace.png" alt-text="Screenshot of a journey visualization trace of a conversation." lightbox="../media/journey-visualization-trace.png":::

> [!TIP]
> Select **Switch to vertical layout** if the path is long. Select **View in Visual Designer** on a channel, workstream, queue, or representative to open it in Visual Designer.

## How Journey Visualization uses data

Journey Visualization reads conversation, session, queue assignment, participant, and overflow records from your Dataverse environment. If you set up conversation diagnostics in Application Insights, it also shows the recorded classification and route-to-queue results.

It shows only what was recorded when the conversation happened. If a step wasn't recorded, it's marked as incomplete or unavailable, not inferred.

Queue membership on the canvas reflects current membership, not membership at the time of the conversation.

## Related information

[Contact Center Admin Workspace overview (preview)](contact-center-admin-workspace-overview.md)  
[Visualize and edit routing with Visual Designer (preview)](visualize-edit-configuration-with-visual-designer.md)  
[Understand conversation diagnostics](/dynamics365/customer-service/administer/conversation-diagnostics-subscenarios)  
[Manage overflow of work items in queues](/dynamics365/customer-service/administer/manage-overflow)  
