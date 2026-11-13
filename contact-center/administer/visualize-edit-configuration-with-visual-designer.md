---
title: Visualize and edit configuration with Visual Designer (preview)
description: Use Visual Designer in Contact Center Admin Workspace to explore routing, edit workstream rules and queue settings, and create queues.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.date: 11/13/2026
ai-usage: ai-assisted
---

# Visualize and edit configuration with Visual Designer (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Visual Designer shows channels, channel instances, workstreams, AI agents, classification and route-to-queue rules, queues, overflow, representatives, and user groups on one interactive canvas. Switch to **Edit** to change routing in context.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/production-ready-preview-dynamics365.md)]

## Prerequisites

[!INCLUDE [admin-workspace-prerequisites](../includes/admin-workspace-prerequisites.md)]

## What Visual Designer shows

| Node | What you see |
|---|---|
| Channel | **Voice**, **Live Chat**, and **Async & Other** channels, with the number of channel instances. |
| Channel instance | A specific phone number, chat widget, or messaging account, with its language and the associated workstreams. |
| Workstream | The AI agent that answers first, classification rules, route-to-queue rules, and work distribution settings. |
| Queue | Type, assignment method, priority, operating hours, overflow handling, representatives, and user groups. |
| Representative and user group | The people and groups who receive work from a queue. |

## Explore your routing

1. Open [Contact Center Admin Workspace](contact-center-admin-workspace-overview.md#open-contact-center-admin-workspace). Visual Designer opens by default.

1. In **Business unit**, select the business unit that you want to view. Learn more in [Create or edit business units](/power-platform/admin/create-edit-business-units).
1. Expand a channel to follow the path through the channel instance, workstream, and queues. Each queue shows its overflow, representatives, and user groups.
1. To see the complete configuration, select **Expand all**. To return to a compact view, select **Collapse all**.
1. To find an item, use **Search** or browse your contact center in the left pane. Select a result to bring it into focus on the canvas.
1. Select a node to open its details in the right pane. For a workstream, the tabs show general settings, classification rules, route-to-queue rules in evaluation order, and work distribution.

:::image type="content" source="../media/visual-designer-workstream.png" alt-text="Screenshot of a workstream selected on the Visual Designer canvas, with its details in the right pane." lightbox="../media/visual-designer-workstream.png":::

### Focus on a path

Select a node, and then in **Focus mode**, select **Upstream**, **Downstream**, or **Neighborhood**.

| Mode | What it shows |
|---|---|
| **Upstream** | Every path that can bring a conversation to the node, such as channels and workstreams that route to a queue. |
| **Downstream** | Everywhere work can go from the node. |
| **Neighborhood** | The next hierarchy of the map from the node. |

Select **Clear focus** to return to the full map.

:::image type="content" source="../media/visual-designer-upstream-focus.png" alt-text="Screenshot of upstream focus on a queue, showing every channel and workstream that can route to it." lightbox="../media/visual-designer-upstream-focus.png":::

### Change the layout

Switch between horizontal and vertical layouts. Use the zoom controls and minimap to navigate large configurations. Select **Clear** to reset the canvas.

## Edit routing configuration

Use **Edit** at the top of the page to switch to edit mode. When you select **Save**, you save changes directly to your live configuration in Dataverse.

> [!NOTE]
> Saved changes take effect immediately for new conversations, just like changes in Copilot Service admin center. Review your changes before you save.

### Edit a queue

1. Select **Edit**.

1. Select a queue on the canvas to open its details in the right pane.
1. Change the settings, such as **Assignment method**.
1. Select **Save**.

:::image type="content" source="../media/visual-designer-queue-assignment.png" alt-text="Screenshot of a queue's assignment method in Visual Designer edit mode." lightbox="../media/visual-designer-queue-assignment.png":::

### Edit workstream rules

1. Select **Edit**, and then select a workstream.

1. In the right pane, go to **Classification rules** or **Route-to-queue rules**.
1. Add a rule or edit an existing rule.
1. Select **Save**.

### Create a queue for a workstream

1. Select **Edit**.

1. On the workstream node, select **+**, and then select **Create queue**. The **Queue setup** pane opens on the right.
1. Complete the guided setup. Select **Save and continue** at each step, and then finish the setup.

   | Step | Details |
   |---|---|
   | **Basics** | Enter the name, type, assignment method, priority, service-level and short-abandoned thresholds, description, and operating hours. |
   | **Members** | Add representatives and user groups. |
   | **Route to queue** | Add the route-to-queue rule that sends conversations to the new queue. |

## Considerations

[!INCLUDE [admin-workspace-settings](../includes/admin-workspace-settings.md)]

Your business unit owns queues that you create from a workstream.

## Related information

[Contact Center Admin Workspace overview (preview)](contact-center-admin-workspace-overview.md)  
[Trace conversations with Journey Visualization (preview)](trace-conversations-with-journey-visualization.md)  
[Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams)  
[Create and manage queues for unified routing](/dynamics365/customer-service/administer/queues-omnichannel)  
[Configure work classification rules](/dynamics365/customer-service/administer/configure-work-classification)  
[Configure route-to-queue rules](/dynamics365/customer-service/administer/configure-route-to-queue-rules)
