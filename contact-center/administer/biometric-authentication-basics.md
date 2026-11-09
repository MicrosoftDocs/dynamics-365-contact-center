---
title: Biometric authentication basics (preview)
description: Learn how biometric authentication works in Dynamics 365 Contact Center, including voiceprints, speaker similarity, anti-spoofing, and net-speech guidance.
author: timsavage
ms.author: timsavage
ms.reviewer: puneetsingh
ms.topic: concept-article
ms.date: 11/09/2026
ms.custom: 
    - bap-template
    - ai-gen-docs-bap
    - ai-seo-date: 11/09/2026
ai-usage: ai-assisted

#customer intent: As a contact center administrator, I want to understand how voice biometrics verifies a caller's identity so that I can configure and reason about authentication behavior.
---

# Voice biometrics basics for biometric authentication and fraud detection (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

> [!IMPORTANT]
>
> You're responsible for configuring and using this biometric authentication and enrollment functionality in compliance with applicable law, including but not limited to biometric and privacy laws (for example, BIPA and the GDPR), including: (i) providing notice to data subjects, including with respect to retention periods and destruction; (ii) obtaining legally sufficient consent from data subjects; and (iii) processing and deleting the biometric data and biometric identifiers. Biometric data and biometric identifiers will have the meanings set forth in applicable biometric and privacy laws and include equivalent terms set forth in any applicable law. You will defend and indemnify Microsoft against any claims made by a third party related to this biometric functionality, including but not limited to the adequacy of consent.

Biometric authentication verifies a caller's identity from the unique characteristics of their speech. In Dynamics 365 Contact Center Intelligence, the biometric authentication service uses voice biometrics to confirm that a caller is who they claim to be and to detect attempts to imitate or replay a voice. Understanding the underlying concepts helps you configure authentication behavior and interpret authentication outcomes with confidence.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

[!INCLUDE [aaa-common-voice-biometrics](~/../contact-center-ai-shared/shared/aaa-common-voice-biometrics.md)]

## Related information
- [Biometric authentication and fraud detection overview](biometric-authentication-fraud-detection-overview.md)
- [Configure authentication profiles](configure-authentication-profiles.md)
- [Manage voice enrollment and authentication](manage-voice-enrollment-authentication.md)
