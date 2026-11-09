---
title: Review fraud cases (preview)
description: Learn how to review, assign, and flag fraud cases and create fraudster voiceprints in the biometric authentication and fraud detection app in Dynamics 365 Contact Center.
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

#customer intent: As a fraud analyst, I want to review incoming calls as cases and flag fraudsters so that future calls from the same voice trigger a suspected-fraud alert for representatives.
---

# Review fraud cases (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Fraud detection records each incoming call as a case in the **Biometric authentication and fraud detection** app. As a fraud analyst, you review these cases to investigate suspicious calls, assign work to the right analyst, and flag callers as fraudsters. When you flag a case as fraud, you help protect your organization from future calls by the same fraudster.

This article shows you how to open a case, review its details, assign an analyst, flag a case as fraud or not fraud, and create a fraudster voiceprint from a case. After you flag a caller as a fraudster, the next call from that voice shows a suspected-fraud banner to the representative after the caller is authenticated.

[!INCLUDE [fraud-detection](../includes/cc-fraud-detection-note.md)]

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- Access to the **Biometric authentication and fraud detection** app.
- The fraud analyst role, or an equivalent role that grants permission to view and update fraud cases.

## Review a case

The **Cases** screen lists each incoming call as a separate case, so you can work through calls that need investigation.

1. In the **Biometric authentication and fraud detection** app, open the **Cases** screen.
1. Select a case in the list to open its details.
1. Review the case details, such as the **Customer ID** and the **date and time the case was created**.

Each case also carries a **Fraud severity** and a **Fraudster score** that help you prioritize your review. Learn more in [Fraud severity and fraud match score](fraud-detection-overview.md#fraud-severity-and-fraud-match-score).

## Assign an analyst to a case

Assign a case to the analyst who owns the investigation so that you can track the work and prevent overlap when multiple analysts work in the **Cases** view. Assigning cases is optional.

1. Open the case from the **Cases** screen.
1. In the **Case assignment** section, go to the **Assigned analyst** dropdown, select the analyst to assign to the case.

## Flag a case as fraud or not fraud

After you investigate a case, flag it so that the outcome is recorded and logged for investigation, compliance, reporting, and operational performance tracking.

1. Open the case from the **Cases** screen.
1. In the **Analyst assessment** dropdown, select **Fraud**, **Not Fraud**, or **Not Reviewed**. 

Analyst assessment outcomes are used in Business performance: Fraud detection to track fraudster detection performance at the system level. They are also used in the **Fraudster watchlist** section to quantify the true-positive and false-positive rates of individual fraudster voiceprints.

## Create a fraudster voiceprint

You can also flag a caller as a fraudster by creating a voiceprint from the case's audio. A voiceprint captures the fraudster's voice so that fraud detection can match it on future calls.

1. Open the case from the **Cases** screen.
1. Select the **Audio Library** tab to view the audio files for the case. 
1. Select the audio file to use, and then select **Create voiceprint**:
    1. Name the voiceprint.
    1. Add it to a watchlist from the Watchlist dropdown.
    1. Select **Create and add to watchlist**.

After you create the voiceprint, the caller is treated as a fraudster. After the fraudster voiceprint is saved to your watchlist, fraud detection compares future calls to the voiceprint and generates an alert if it detects a similar voice.

> [!NOTE]
> To create a fraudster voiceprint, use an audio sample that contains at least 12 seconds of net speech.

## Related information
- [Fraud detection overview](fraud-detection-overview.md)
- [Manage fraudster voiceprints](manage-fraudster-voiceprints.md)
- [Manage fraudster watchlists](manage-fraudster-watchlists.md)
