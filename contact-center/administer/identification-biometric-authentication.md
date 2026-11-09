---
title: Identification for biometric authentication (preview)
description: Learn how identification differs from authentication in the voice channel and how to choose a robust, unique customer identifier for voice biometrics.
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
#customer intent: As a contact center administrator or architect, I want to understand how identification differs from authentication and how to choose a customer identifier so that I can plan a voice biometrics implementation.
---

# Identification for biometric authentication (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

This article explains how identification and authentication play distinct roles in a voice interaction and how to select your customer identifier that biometric authentication can rely on for consent, voiceprint creation, and authentication. It's intended for administrators and architects who are planning a biometric authentication implementation and need to make these design decisions before deployment.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Identification compared to authentication

In a voice interaction, *identification* determines who the customer claims to be. It typically collects information such as an account number or customer ID and matches it to an existing customer record. *Authentication* is a separate step that verifies the caller is the legitimate owner of that identity. After you identify the caller, authentication challenges validate the caller's identity claim.

- **Identification** answers: Which customer record do you need to access?
- **Authentication** answers: Can you trust that this person is really the customer?

## Choose a customer identifier for biometric authentication

Recording consent, creating a voiceprint, and authenticating a caller all rely on a robust customer identifier. Biometric authentication binds an existing customer identifier to each of these activities:

- **Consent**: Your customer identifier is used to record your customer consented to or declined biometric authentication, for both current and future interactions.
- **Voiceprint creation**: The identifier associates the customer with a specific voiceprint that is saved within your Dataverse environment.
- **Authentication**: The identifier tells the service which voiceprint to retrieve and use.

A good customer identifier has the following characteristics:

- **Unique** to each end user.
- **Non-transferable** between users.
- **Persistent** over time.

Avoid using a telephone number, caller ID, or automatic number identification (ANI) as the customer identifier when an organization has many end users. Multiple end users can share the same number, and telephone numbers can be reassigned to different users over time.

The platform doesn't create end-user identifiers, but it provides tools and integration patterns that automatically render the identifier to the biometric authentication service in real time.

## Related information
- [Biometric authentication and fraud detection overview](biometric-authentication-fraud-detection-overview.md)
- [Voice biometrics basics](biometric-authentication-basics.md)
- [Capture customer consent for voice enrollment](capture-consent-for-voice-enrollment.md)
- [Configure authentication profiles](configure-authentication-profiles.md)
