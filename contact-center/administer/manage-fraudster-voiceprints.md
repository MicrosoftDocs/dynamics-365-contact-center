---
title: Manage fraudster voiceprints (preview)
description: Learn how to view, filter, move, and delete fraudster voiceprints in the biometric authentication and fraud detection app in Dynamics 365 Contact Center.
author: timsavage
ms.author: timsavage
ms.reviewer: puneetsingh
ms.topic: how-to
ms.date: 11/09/2026
ms.custom: 
    - bap-template
    - ai-gen-docs-bap
    - ai-seo-date: 11/09/2026
ai-usage: ai-assisted

#customer intent: As a fraud analyst or contact center administrator, I want to manage the fraudster voiceprints in my inventory so that I can keep my watchlists accurate and act on matching cases.
---

# Manage fraudster voiceprints (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Fraud detection screens incoming callers against fraudsters' voices on your organization's watchlist on an incoming call. In the **Biometric authentication and fraud detection** app, the **Fraudster voiceprint** screen shows all the fraudster voiceprints in your inventory in one place, so you can review them, keep them organized across watchlists, and remove the ones you no longer need.

This article shows you how to view your fraudster voiceprints, open the case that a voiceprint relates to, filter voiceprints by watchlist, move a voiceprint to a different watchlist, and delete a voiceprint.

[!INCLUDE [fraud-detection](../includes/cc-fraud-detection-note.md)]

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

* Access to the **Biometric authentication and fraud detection** app in Dynamics 365 Contact Center.
* At least one watchlist that contains fraudster voiceprints. Learn more in [Manage fraudster watchlists](manage-fraudster-watchlists.md).
* The Fraud supervisor security role required to view, move, and delete fraudster voiceprints.

## View fraudster voiceprints

The **Fraudster voiceprints** screen lists every fraudster voiceprint in your inventory so you can review your full set of voiceprints at a glance.

1. Open the **Biometric authentication and fraud detection** app.
1. In the navigation pane, select **Fraudster voiceprints**.
1. Review the list of voiceprints. Voiceprints that were created earlier from the **Cases** screen also appear here in the watchlist you selected.

## Open the case for a voiceprint

Each voiceprint links back to the case it came from, so you can review the matching cases and listen to the associated audio.

1. On the **Fraudster voiceprint** screen, select a voiceprint.
1. Confirm that the app redirects you to the related **Cases** screen for that voiceprint. 
1. On the **Cases** screen, review the matching cases.
1. Open the **Audio Library** to view and play the matching voiceprint audio. 

## Filter voiceprints by watchlist

If you organize voiceprints across multiple watchlists, filter the list to focus on the voiceprints in a single watchlist.

1. On the **Fraudster voiceprint** screen, open the **Select watchlist** dropdown. 
1. Select the watchlist whose voiceprints you want to see.
1. Confirm that the list now shows only the voiceprints in the selected watchlist.

## Move a voiceprint to a different watchlist

Move a voiceprint when it belongs in a different watchlist—for example, to move it from the **default** watchlist to a **demo** watchlist.

1. On the **Fraudster voiceprint** screen, select the voiceprint you want to move.
1. Select the **Move** option to move the voiceprint to a different watchlist.
1. Choose the destination watchlist, such as **demo**.
1. Select **Move voiceprint** to confirm the move. The voiceprint now appears under the target watchlist.

## Delete a voiceprint

Delete a voiceprint stored within your Dataverse environment when you no longer need it so it stops contributing to fraud detection matches.

1. On the **Fraudster voiceprint** screen, select the voiceprint you want to remove.
1. Select **Delete**. 
1. Select **Delete voiceprint** to confirm the deletion when prompted.

> [!NOTE]
> Deleting a voiceprint stored within your Dataverse environment is a permanent action and can't be undone.

## Related information
* [Fraud detection overview (preview)](fraud-detection-overview.md)
* [Review fraud detection cases (preview)](fraud-detection-review-cases.md)
* [Manage fraudster watchlists (preview)](manage-fraudster-watchlists.md)
