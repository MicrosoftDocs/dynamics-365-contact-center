---
title: Contact Center Admin Workspace overview (preview)
description: Learn how Contact Center Admin Workspace helps you visualize routing and trace conversations in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: overview
ms.date: 11/13/2026
ai-usage: ai-assisted
---

# Contact Center Admin Workspace overview (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Contact Center Admin Workspace is an administration experience for Dynamics 365 Contact Center. Use it to understand and change conversation routing, and to investigate specific conversations.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/production-ready-preview-dynamics365.md)]

## What you can do

| Feature | What it does |
|---|---|
| Visual Designer | Shows channels, channel instances, workstreams, AI agents, classification and route-to-queue rules, queues, overflow, representatives, and user groups on one interactive canvas. Switch to edit mode to change routing in context. Learn more in [Visualize and edit routing with Visual Designer (preview)](visualize-edit-configuration-with-visual-designer.md). |
| Journey Visualization | Traces a past conversation on the same canvas as your configuration, with a timeline of each step. Open classification, route-to-queue, overflow, or assignment decisions to see which rules were evaluated and why. Learn more in [Trace conversations with Journey Visualization (preview)](trace-conversations-with-journey-visualization.md). |

## Prerequisites

[!INCLUDE [admin-workspace-prerequisites](../includes/admin-workspace-prerequisites.md)]

## Open Contact Center Admin Workspace

In Copilot Service admin center, use one of the following options to open the app:

- **Home page**: On the **Home** page, select **Open "New Admin workspace"**.

- **A channel, workstream, or queue**: Open a channel like **Chat** or **Voice**, the **Workstream** page, or the **Advanced queues** page, and select **New admin Workspace**.

The app opens in a new browser tab.

## Navigate Contact Center Admin Workspace

Use the navigation pane to switch among features. On each page, select the **Business unit** that you manage to show only its configuration and conversations. Selecting a parent business unit doesn't include data from its child business units. By default, the **Visual Designer** page opens.

:::image type="content" source="../media/admin-workspace-visual-designer.png" alt-text="Screenshot of Visual Designer, the default page of Contact Center Admin Workspace." lightbox="../media/admin-workspace-visual-designer.png":::

Select **Give feedback** in the app to share what works and what doesn't.

## Use Contact Center Admin Workspace with the Copilot Service admin center

Contact Center Admin Workspace works with Copilot Service admin center. Both apps read and write the same configuration in your Microsoft Dataverse environment, and changes in one app appear in the other. There's no import, synchronization, or migration step.

[!INCLUDE [admin-workspace-settings](../includes/admin-workspace-settings.md)]

Record routing for cases and other records isn't part of Contact Center Admin Workspace. Manage it in the Copilot Service admin center.

## Preview limitations

- Large configurations load progressively. Very large queue memberships are summarized instead of drawn in full on the canvas.
- Journey Visualization shows current queue membership, not membership at the time of the conversation.

## Related information

[Overview of unified routing](/dynamics365/customer-service/administer/overview-unified-routing)
