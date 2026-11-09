---
title: Manage fraudster watchlists (preview)
description: Learn how to create, edit, and delete fraudster watchlists in the biometric authentication and fraud detection app for Dynamics 365 Contact Center.
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
#customer intent: As a fraud analyst, I want to manage fraudster watchlists so that I can group fraudster voiceprints for monitoring and matching.
---

# Manage fraudster watchlists (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

A *fraudster watchlist* is a list of fraudster voiceprints stored within your Dataverse environment that Dynamics 365 Contact Center uses for monitoring and matching. When an incoming call matches a voiceprint on your watchlist, the service can generate alerts for customer service representatives and fraud analysts. As a fraud analyst, you manage your watchlists to organize voiceprints and control which groups are used to screen calls.

This article shows you how to create, edit, and delete fraudster watchlists in the **Biometric authentication and fraud detection** app.

[!INCLUDE [fraud-detection](../includes/cc-fraud-detection-note.md)]

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- Access to the **Biometric authentication and fraud detection** app.
- Fraud supervisor permission to manage fraud detection settings.

## Open the Fraudster watchlist screen

The **Fraudster watchlist** screen is where you view and manage all watchlists.

1. Sign in to the **Biometric authentication and fraud detection** app.
1. In the navigation pane, select **Fraudster watchlist**. 

   The screen lists the existing watchlists, including a default watchlist that's already created for you.

> [!NOTE]
> The default watchlist can be renamed but can't be deleted.

## Create a watchlist

Create a watchlist when you want to group a new set of fraudster voiceprints for monitoring and matching.

1. On the **Fraudster watchlist** screen, select **+ New watchlist**.
1. Enter a name for the watchlist, such as **Demo watchlist**.
1. Add desciption for the watchlist, if required.
1. Select **Create watchlist**.

   The new watchlist appears in the list.

## Edit a watchlist

Edit a watchlist to change its details, such as renaming it.

1. On the **Fraudster watchlist** screen, select the watchlist that you want to change.
1. Select **Edit**.
1. Update the watchlist name or description.
1. **Save** your changes.

## Delete a watchlist

Delete a watchlist when you no longer need it.

1. On the **Fraudster watchlist** screen, select the watchlist that you want to remove.
1. Select **Delete**.
1. Select **Delete watchlist** to confirm the deletion. 

> [!NOTE]
> When you delete your watchlist, you permanently remove your watchlist and all its voiceprints stored within your Dataverse environment. This action can't be undone. Before you delete your watchlist, move voiceprints to a different watchlist if you want to keep them.

## Related information
- [Fraud detection overview](fraud-detection-overview.md)
- [Manage fraudster voiceprints](manage-fraudster-voiceprints.md)
