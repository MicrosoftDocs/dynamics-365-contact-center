---
title: Monitor and optimize system performance for biometric authentication and fraud detection (preview)
description: Use the System optimization screen to monitor voice-biometric decisioning performance and tune authentication, playback, and synthetic-speech thresholds in Dynamics 365 Contact Center.
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

#customer intent: As a contact center administrator, I want to monitor voice-biometric decisioning performance and tune thresholds so that I can balance security and customer experience for my organization.
---

# Monitor and optimize system performance (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

The **System optimization** screen in the **Biometric authentication and fraud detection** app helps administrators, compliance officers, and risk managers understand how individual factors and thresholds affect voice-biometric decisioning performance. Use it to see how secure your current configuration is and to predict the effect of a threshold change before you apply it.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- Access to the **Biometric authentication and fraud detection** app.

## Open the System optimization screen

1. Sign in to the **Biometric authentication and fraud detection** app. 
1. In the navigation pane, select **System optimization**. 

## Review decisioning-volume metrics

The screen shows the volume of voice-biometric checks so that you can see how often each control runs:

- **Voice verifications**: The number of voice authentication attempts.
- **Playback checks**: The number of authentication attempts that use playback detection.
- **Synthetic speech checks**: The number of authentication attempts that use synthetic-speech detection.
- **Authentication outcomes**: The proportion of successful and unsuccessful voice authentication attempts.

## Review alert rates

The **Alert rates** section shows how your current configuration performs against imposters and spoofing.

> [!NOTE]
> The Alert rates metrics require a minimum of 1,000 successful authentications before they display results. Smaller sample sizes can be inaccurate and statistically insignificant.

- **False accepts**: The actual false-accept rate observed in your environment. To measure this rate, biometric authentication and fraud detection runs background *imposter tests*: after a voiceprint authenticates a caller, a parallel process uses the caller's audio to attempt authentication against a voiceprint that isn't theirs. None of these tests should succeed, so any success is counted as a false accept. This metric lets you see how secure your current configuration is at any time.
- **Synthetic speech**: The percentage of enrollment and authentication interactions that exceeded the synthetic-speech threshold.
- **Playback**: The percentage of enrollment and authentication interactions that exceeded the playback threshold.

## Tune thresholds

The **Tune thresholds** section predicts the effect of a threshold change by using your production data. Enter a target rate, and the tool calculates the configuration threshold needed to achieve it.

1. Select the threshold type to tune: 
   - **False accepts** (voice authentication)
   - **Synthetic speech** (voice authentication and enrollment)
   - **Playback alert rate**
1. Enter your target rate to see the corresponding threshold.
1. Select **Apply threshold** to update the configuration thresholds used in real-time decisions. 

## Related information
- [Configure authentication profiles (preview)](configure-authentication-profiles.md)
- [View biometric authentication and fraud detection business performance (preview)](../use/biometric-authentication-fraud-detection-business-performance.md)