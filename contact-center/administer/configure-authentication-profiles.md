---
title: Configure authentication profiles (preview)
description: Configure voice enrollment, authentication, and fraud detection settings in authentication profiles for Dynamics 365 Contact Center.
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
#customer intent: As a contact center administrator, I want to configure authentication profiles so that I can tailor voice enrollment, authentication, and fraud detection to different customer requirements.
---

# Configure authentication profiles (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

An *authentication profile* is a collection of settings that controls how biometric authentication and fraud detection enrolls, authenticates, and screens callers in the voice channel. Because you configure each profile independently, you can tailor profiles to different customer requirements. For example, use a higher-security profile for high-value transactions and a lower-friction profile for routine calls.

[!INCLUDE [bafd-note-small](../includes/cc-bafd-note-small.md)]

This article shows you how to open the list of authentication profiles, review the settings in a profile, and tune the toggles and thresholds that control voice enrollment, authentication, and fraud detection. It's intended for administrators who manage voice authentication for their contact center.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- An OmniChannel administrator role for the Copilot Service admin center. 

## Open the list of authentication profiles

Manage authentication profiles in the Copilot Service admin center. Follow these steps to view the profiles configured for your organization.

1. Sign in to the **Copilot Service admin center**. 
1. In the left navigation, select the **Biometric authentication and fraud detection** tab. 
1. Select **Manage** to open the list of authentication profiles configured for the organization. 

   The list shows each profile available to your organization. Tailor each profile to different customer requirements.

## Review a profile's settings

Select a profile from the list to open its settings. Each profile has two primary toggles and a set of related settings that control how customers are enrolled, authenticated, and screened for fraud.

1. In the profile list, select the profile you want to review. 
1. Review the two primary toggles:

   - **Voice enrollment and authentication**: Enables enrolling your customer's voiceprint and authenticating your customer against it. The default setting is **High**; For **Voice enrollment**, the default setting is **Strict**; and for **Authentication**, the default setting is **Strict**.

   - **Fraud detection**: Enables checking a caller's voice against your fraudster watchlist. 

## Configure enrollment, authentication, and fraud settings

Beyond the two toggles, each profile includes settings that determine how quickly your customer is enrolled and verified, which of your fraudster watchlist is used, and how strict the matching is. Adjust these settings to match the security level and risk tolerance for the profile.

1. Set the **Sensitivity settings** based on the security level the profile requires.  Higher sensitivity increases security but also imposes a higher matching confidence, increases the chance of enroll or authenticate failing for true users.
1. Review and set the **voice authentication policies** for the profile.


### Tune speech requirements to your risk tolerance

Speech requirements determine how much *net speech* (spoken audio, excluding silence) the service needs before it can enroll or authenticate your customer. You set the amount of net speech through a configurable **speech requirements** level of **Low**, **Medium**, or **High** on the profile—not a free-form number.

Longer settings improve authentication, playback detection, and synthetic-speech detection performance, while shorter enrollment settings reduce customer friction. Choose the level that matches your organization's risk tolerance.

- **Enrollment** requires approximately 6–12 seconds of net speech, depending on the level (**Low** ≈ 6 seconds, **High** ≈ 12 seconds).
- **Authentication** requires approximately 3–6 seconds of net speech, depending on the level (**Low** ≈ 3 seconds, **High** ≈ 6 seconds).

> [!NOTE]
> Biometric authentication uses the profile's authentication speech requirement at the moment of the authentication attempt. Existing voiceprints remain usable even if you change the profile's speech requirements level after your customer enrolls.

## Related information
- [Biometric authentication and fraud detection overview (preview)](biometric-authentication-fraud-detection-overview.md)
- [Enable the biometric authentication and fraud detection workstream (preview)](enable-biometric-authentication-fraud-detection-workstream.md)
- [Manage voice enrollment and authentication (preview)](manage-voice-enrollment-authentication.md)
