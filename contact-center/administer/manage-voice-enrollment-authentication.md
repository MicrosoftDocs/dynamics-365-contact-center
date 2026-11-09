---
title: Manage voice enrollment and authentication (preview)
description: Learn how biometric authentication and fraud detection enrolls customer voiceprints and authenticates callers in Dynamics 365 Contact Center.
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

#customer intent: As a contact center administrator, I want to configure how voice enrollment and authentication collect and use customer speech so that I can balance authentication accuracy against customer experience.
---

# Manage voice enrollment and authentication (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Biometric authentication uses voice biometrics to enroll your customer's voiceprint stored within your Dataverse environment and then verify your customer's identity on later calls. This article explains how enrollment and authentication collect customer speech, how to tune the amount of speech required for your organization's risk tolerance, and how the design of your bot and agent conversations affects results.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## How enrollment and authentication use speech

Enrollment and authentication both rely on *net speech* — the audio that contains only the customer's voice. Silence, pauses, hold music, and agent or bot speech don't count toward the net-speech totals.

- **Enrollment** collects speech until there's enough usable audio to create a reliable voiceprint stored within your Dataverse environment.
- **Authentication** compares a shorter sample of the customer's voice against the stored voiceprint in your Dataverse to verify identity.

> [!NOTE]
> The amount of net speech that enrollment and authentication collect is configurable rather than a single fixed threshold. You set a **Low**, **Medium**, or **High** speech requirements level on the authentication profile. Higher levels improve authentication, playback, and synthetic-speech detection performance; lower levels reduce enrollment friction.

### Speech requirement level tradeoff

Consider the following tradeoffs when you select a speech requirement level:

- More net speech results in higher correct authentication rates and fewer false accepts.
- Less net speech results in faster enrollment and authentication.

## Configure enrollment

During enrollment, biometric authentication collects your customer's speech until there's enough usable audio to build a voiceprint stored within your Dataverse environment. Configure enrollment requirements to match your organization's risk tolerance and customer-experience goals.

Use the following guidance to set enrollment requirements:

1. Set the **speech requirements** level on the authentication profile. This level is configurable as **Low**, **Medium**, or **High**, and it controls how much net speech enrollment collects. Enrollment ranges from about **6 seconds** of net speech at the Low level to about **12 seconds** at the High level. Only the customer's speech counts toward this total — silence and pauses don't.
1. Weigh accuracy against customer effort. Longer enrollment improves the accuracy of future authentication and strengthens playback and synthetic-speech detection. Voiceprints created from less speech might increase authentication failures on later calls.
1. Set your enrollment target based on that trade-off. Choose a longer target when you prioritize security and fraud resistance, or a shorter target when you prioritize a faster enrollment experience.

> [!NOTE]
> The enrollment requirement is configurable, not a single fixed value. Set the speech requirements level to **Low**, **Medium**, or **High** on the authentication profile to balance security against enrollment friction. As anchor values, the Low level collects about **6 seconds** of net speech and the High level collects about **12 seconds**.

## Authenticate a customer before enrollment

Authenticate a customer with your existing verification method before they enroll, so that the voiceprint is created for the correct person. Customers can use whatever authentication step your organization already has in place as a preliminary check before enrollment begins.

By default, enrollment also runs playback and synthetic-speech checks, so recorded or non-natural speech isn't used to create a voiceprint.

## Configure authentication

Authentication verifies a returning customer's identity by comparing a short sample of their voice against their stored voiceprint. Because it builds on the existing voiceprint, authentication requires substantially less speech than enrollment.

Use the following guidance to set authentication requirements:

1. Set the **speech requirements** level on the authentication profile. Authentication uses the same **Low**, **Medium**, or **High** level and requires about **3 seconds** of net speech at the Low level to about **6 seconds** at the High level. 
1. Weigh accuracy against speed. Longer authentication speech improves accuracy, while less speech might increase authentication failures.
1. Set your authentication target based on that trade-off.

> [!NOTE]
> Biometric authentication uses the authentication speech setting saved in the profile at the time of the authentication attempt. An enrolled voiceprint can always attempt authentication, even if the profile's speech requirements changed after the customer enrolled.


## Collect speech in human-to-human conversations

In a human-to-human conversation, your customer and agent talk naturally, and enrollment and authentication happen passively in the background. Because your customer typically speaks enough during a normal conversation, you usually don't need scripted prompts.

## Interpret authentication outcomes

After authentication runs, biometric authentication and fraud detection returns an outcome that determines how the interaction proceeds. Plan your call flows and agent guidance around these outcomes:

- **Grant access.** The caller's voice matches the stored voiceprint with enough confidence, and your customer proceeds without additional verification.
- **Trigger step-up authentication.** The result is inconclusive, so your customer is prompted for an additional verification method before proceeding. 
- **Route for manual review.** The interaction is sent to an agent or fraud analyst for manual verification. 

## Cancel your customer's enrollment

When your customer withdraws consent or you need to remove their voiceprint, you can cancel your customer's enrollment. Canceling enrollment deletes your customer's stored voiceprint within your Dataverse environment so that it's no longer used for authentication. After you cancel enrollment, your customer must enroll again before voice authentication can be used on future calls.

To manage customer consent and stored voice data, use your customer consent and data management screen. Learn more in [Capture customer consent for biometric authentication and fraud detection](capture-consent-for-voice-enrollment.md).

## Related information
- [Capture customer consent for biometric authentication and fraud detection](capture-consent-for-voice-enrollment.md)
- [Configure authentication profiles](configure-authentication-profiles.md)
- [Voice biometrics basics](biometric-authentication-basics.md)
