---
title: Capture customer consent for voice enrollment (preview)
description: Capture voice-biometric consent in biometric authentication and fraud detection for human-to-human conversations before a voiceprint is created.
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
#customer intent: As a contact center administrator, I want to capture customer consent before a voiceprint is created so that voice enrollment complies with voice-biometric regulations.
---

# Capture customer consent for voice enrollment (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Voice-biometric regulations in many jurisdictions require explicit customer consent before a voiceprint is created and stored within your Dataverse environment. Biometric authentication captures this consent during enrollment, and enrollment proceeds only after your customer grants consent. You must obtain legally sufficient consent from your customer. 

The exact consent experience can be customized to match your organization's requirements. This article shows you how biometric authentication captures consent in a human-to-human conversation with your customer service representative (service representative or representative). 

Use this article to understand the consent flow in each channel and to help your representatives and voice agent respond correctly.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- Biometric authentication is enabled for the voice channel in your environment. 
- Your customer's consent status is undefined. 
- Representatives have access to the Copilot Service workspace.

## Capture consent in a human-to-human conversation

In a human-to-human conversation, the representative presents the consent statement to the customer and records the customer's response in the Copilot Service workspace. Enrollment proceeds only when the customer grants consent.

1. Provide consent capture instructions to your representatives.
1. Record the customer's consent status in the Copilot Service workspace. Select the **Consent** button to set your customer's consent status to Yes, or select the **Opt Out** button to set it to No.
1. Confirm that the recorded status matches the customer's response before you continue.

When the customer grants consent, biometric authentication and fraud detection allows enrollment to proceed. When the customer declines, enrollment doesn't start, and the customer continues to be verified through your organization's alternative authentication methods.

## Opt out and cancel enrollment

Your customer can decline consent at any time, and your customer who previously consented can withdraw consent later. Setting your customer's consent status to No stops voice enrollment from being offered on future interactions. It doesn't delete the stored voiceprint within your Dataverse environment.

Deleting the voiceprint stored within your Dataverse environment is a separate operation:

- In a human-to-human conversation, the representative deletes the voiceprint from the biometric authentication and fraud detection widget.
- A supervisor can delete the voiceprint at any time from the customer consent screen.

To change your customer's consent status or delete a voiceprint after the initial interaction, use your customer consent management screen. Learn more in [Manage customer consent and voice-authentication data](manage-customer-consent-data.md).

## Related information
- [Manage customer consent data](manage-customer-consent-data.md)
- [Manage voice enrollment and authentication](manage-voice-enrollment-authentication.md)
- [Biometric authentication and fraud detection overview](biometric-authentication-fraud-detection-overview.md)
