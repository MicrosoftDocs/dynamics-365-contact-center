---
title: Biometric authentication and fraud detection overview (preview)
description: Learn how biometric authentication and fraud detection uses voice biometrics, synthetic-speech detection, and anti-spoofing to verify customer identity in the voice channel.
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
#customer intent: As a contact center administrator, I want to understand what biometric authentication and fraud detection is and how it verifies caller identity so that I can decide whether to adopt it in the voice channel.
---

# Biometric authentication and fraud detection overview (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

[!INCLUDE [bafd-note](../includes/cc-bafd-note.md)]

This article explains what biometric authentication and fraud detection is, why organizations use it, how it verifies identity, detects fraud, and the ways it fits into a voice interaction. It's intended for administrators and decision-makers who are evaluating biometric authentication and fraud detection for Dynamics 365 Contact Center.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Why use biometric authentication 

Biometric authentication is a voice-security service that verifies your customer's identity from their voice during a natural conversation. Alongside knowledge-based questions, PINs, passwords, or one-time passcodes, biometric authentication combines voice biometrics, synthetic-speech detection, and playback detection to confirm that callers are who they claim to be. Because verification happens passively as your customer speaks, biometric authentication reduces friction for your customer and shortens the identity checks that customer service representatives perform on every call. All voiceprints and associated metadata are stored within your Dataverse environment.

Biometric authentication and fraud detection adds a voice-based identity factor to the contact center so that authentication can happen without extra steps for the customer. Organizations typically adopt it for the following reasons:

- **Streamlined authentication in the voice channel.** Identity verification runs automatically as the customer speaks, so callers don't have to answer a series of security questions.
- **Reduced call handle time.** Authentication occurs passively in the background of a normal conversation. Authentication decisions are rendered during call introductions and intent capture. 
- **Higher authentication success rates.** Because verification doesn't depend on PINs, passwords, one-time passcodes, or access to a trusted phone or email, more customers can be authenticated successfully.
- **A better representative experience.** Representatives spend less time asking knowledge-based questions and can focus on resolving the customer's issue.
- **An additional factor for a multifactor strategy.** A voiceprint can serve as one factor alongside other verification methods.
- **Real-time protection against spoofing.** Biometric authentication and fraud detection detects non-natural speech patterns, synthetic (AI-generated) speech, and recorded playback to help block impersonation attempts as they happen.

## Why use fraud detection?

Fraud detection is a voice-security service that compares caller audio to your fraud watchlist, alerting fraud analysts and/or contact center representatives that a potential match has been detected. All fraudster voiceprints are created from a dedicated Dynamics 365 Contact Center biometric authentication and fraud detection user interface by authorized users from your organization. All data resides within your Dataverse tenant.

- **Real-time protection against fraudster attacks.** Fraud detection matches live speaker audio against fraudster voices on your watchlist. It alerts both representatives and fraud analysts in real time when it detects a potential match.
- **Simplified fraud detection performance management.** The service includes a dedicated fraud analyst UI to work fraud alerts, provide human feedback, and create and manage fraudster voiceprints. 

[!INCLUDE [aaa-common-how-it-works](~/../contact-center-ai-shared/shared/aaa-common-how-it-works.md)]

## Authentication decisions and outcomes

After biometric authentication and fraud detection evaluates a call, it produces a decision in real time. In a live conversation, the service shows a pass/fail indicator to the representative. In an automated conversation, it returns a response to the voice agent. Based on the decision, the interaction can:

- **Grant access** when the caller is confidently authenticated.
- **Trigger step-up authentication** when additional authentication is needed.
- **Route the call for manual review** when there is an authentication failure or fraudster match.

[!INCLUDE [aaa-common-interaction-types](~/../contact-center-ai-shared/shared/aaa-common-interaction-types.md)]


## Related information
- [Voice biometrics basics](biometric-authentication-basics.md)
- [Capture consent for biometric authentication and fraud detection](capture-consent-for-voice-enrollment.md)
- [Configure authentication profiles](configure-authentication-profiles.md)
- [Fraud detection overview](fraud-detection-overview.md)
