---
title: Authenticate customers during a call (preview)
description: Learn how to accept calls, register and enroll customers for voice authentication, and respond to authentication and fraud results in Dynamics 365 Contact Center.
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

#customer intent: As a customer service representative, I want to enroll and verify callers by voice during a call so that I can confirm their identity without asking security questions.
---

# Authenticate customers during a call (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

As a customer service representative, you can confirm a caller's identity by voice while you talk to them. Biometric authentication listens to your customer's voice during the conversation, compares it to the voiceprint that your customer enrolled earlier, which is stored within your Dataverse environment, and shows you whether the caller is authenticated. If a caller's voice matches a fraudster on your organization's watchlist and real-time fraudster alerting is enabled, you also see a fraud alert so that you can follow your organization's escalation process.

This article shows you how to accept an incoming call, register and enroll a new customer for voice authentication, and read the authentication and fraud results on later calls. You do this work from the Copilot Service workspace.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- Permissions required to access the Copilot Service workspace as a customer service representative.
- The voice workstream behavior has biometric authentication enabled. Learn more in [Enable biometric authentication and fraud detection on a workstream](../administer/enable-biometric-authentication-fraud-detection-workstream.md).
- Your queue is configured to route inbound calls to you.

## Accept an incoming call

When a call is routed to you, you receive a notification about the incoming call on your representative desktop. Accept the notification to connect to the caller. Learn more in [Make and receive customer calls](voice-channel-agent-experience.md#make-and-receive-customer-calls).

After you accept the call, your customer's session and the authentication controls open in your workspace.

## Register a new customer

If the caller isn't already a known contact, you're prompted to create your customer record before you can start voice authentication. Registering the contact links the call to a customer that the authentication service can enroll and recognize.

1. When you're prompted to create a new customer, select **New contact**.
1. Enter the caller's details, and then save the contact.
1. Confirm that the new contact is now associated with the active call.

## Enroll your customer for voice authentication

After the contact exists, you can enroll your customer so that the system can recognize their voice on later calls. Enrollment requires your customer's consent and a short voice sample.

1. Select the option to enroll your customer for voice authentication.
1. Ask your customer for consent to create a voiceprint, and confirm their agreement as required by your organization's policy.
1. Ask your customer to speak for a few seconds so the system can capture a voice sample.
1. Wait for confirmation that enrollment succeeded.

## Review authentication results on later calls

On later calls, the system automatically compares the caller's voice to their enrolled voiceprint and marks them as authenticated without any extra steps from you. You see a pass or fail indicator so you know whether the caller's identity was verified.

1. Accept the call from an enrolled customer as described in [Accept an incoming call](#accept-an-incoming-call).
1. As the customer speaks, watch for the authentication indicator to update.
1. Read the result:
   - A **pass** indicator means the caller's voice matched their enrolled voiceprint.
   - A **fail** indicator means the voice didn't match. Follow your organization's fallback process to verify identity another way.

## Respond to a suspected fraud alert

If the caller's voice matches a fraudster on your organization's watchlist, a suspected fraud banner appears after authentication runs. Use it as a signal to follow your organization's fraud-handling process.

1. After authentication completes, check for a **suspected fraud** banner in the call.
1. If the banner appears, follow your organization's escalation and verification procedure.

## Related information

- [Use agent dashboard and call controls in the voice channel](voice-channel-agent-experience.md)
- [Biometric authentication and fraud detection overview](../administer/biometric-authentication-fraud-detection-overview.md)
- [View biometric authentication and fraud detection business performance](biometric-authentication-fraud-detection-business-performance.md)
