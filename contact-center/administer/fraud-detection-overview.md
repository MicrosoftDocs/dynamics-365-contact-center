---
title: Fraud detection overview (preview)
description: Learn how fraud detection uses voice biometrics to detect known fraudsters on incoming calls in Dynamics 365 Contact Center.
author: timsavage
ms.author: timsavage
ms.reviewer: puneetsingh
ms.topic: overview
ms.date: 11/09/2026
ms.custom: 
    - bap-template
    - ai-gen-docs-bap
    - ai-seo-date: 11/09/2026
ai-usage: ai-assisted

#customer intent: As a fraud analyst or contact center administrator, I want to understand how fraud detection identifies known fraudsters so that I can protect my organization and its customers from fraudulent calls.
---

# Fraud detection overview (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

[!INCLUDE [bafd-note-small](../includes/cc-bafd-note-small.md)]

Fraud detection is a voice-biometric capability that compares the voice of each caller against your organization's watchlist of fraudster voiceprints stored within your Dataverse environment and raises an alert when it finds a potential match, so you can respond before a fraudster completes a fraudulent transaction.

[!INCLUDE [fraud-detection](../includes/cc-fraud-detection-note.md)]

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## How fraud detection works

Voice-biometric fraud detection follows three core steps. Together, they turn a single identified fraudulent call into ongoing protection against the same fraudster on future calls.

1. **Detect a fraudulent call.** A fraud analyst reviews interactions in Fraud Management Cases and detects a call that was made by a fraudster.
1. **Create a fraudster voiceprint.** From that call, the fraud analyst creates a fraudster voiceprint, saves it within your Dataverse environment and adds it to your organization's watchlist.
1. **Generate fraud alerts.** For incoming calls where fraud detection is enabled, each caller is checked against the watchlist. When a caller's voice matches a fraudster on your organization's watchlist, the system generates an alert for customer service representatives, fraud analysts, or both.

## Key concepts

Understanding a few core terms helps you work with fraud detection and the related management tasks.

### Watchlist

A watchlist is a list or group of fraudster voiceprints that fraud detection uses to monitor and match incoming callers. Your organization starts with an empty default watchlist, and your fraud analysts can create additional watchlists to organize voiceprints in a way that fits how different types of calls are distributed within your organization.

### Fraudster voiceprint

A fraudster voiceprint is a secure mathematical representation of the distinctive characteristics of your fraudster's speech. It's a mathematical model of your fraudster's speech rather than the audio itself. Fraudster voiceprints are stored within your Dataverse environment. Fraud detection compares the voice on an incoming call against the voiceprints in your organization's watchlist and generates a fraud alert when it detects a similar voice. 

Your organization's fraud analysts create fraudster voiceprints through a dedicated Fraud Management Cases UI.

### Fraud severity and fraud match score

Each case carries a **Fraud severity** and a **Fraudster score**:

- **Fraud severity** shows the potential risk of the interaction. If fraud severity is green or low, your customer is authenticated. If it's red or medium, your customer failed authentication. If it's purple or high, your customer matched the fraudster on the watch list.
- **Fraudster score** shows how closely a caller's voice matches a fraudster voiceprint on your watchlist. A higher score means a stronger match. 

## Roles and separation of duties

Fraud detection supports separation of duties so that the work of investigating fraud is divided among distinct roles. It introduces a **Fraud analyst** role, which investigates calls and manages voiceprints, and a **Fraud supervisor** role, which oversees the fraud analysts' work, deletes fraudster voiceprints, and curates watchlists to improve the overall fraud detection performance.

## Related information
- [Review fraud cases](fraud-detection-review-cases.md)
- [Manage fraudster watchlists](manage-fraudster-watchlists.md)
- [Manage fraudster voiceprints](manage-fraudster-voiceprints.md)
