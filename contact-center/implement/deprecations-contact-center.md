---
title: Deprecations in Dynamics 365 Contact Center
description: Use this article to get information about the deprecated features in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.date: 09/14/2026
ms.custom: bap-template
ms.collection:
---

# Deprecations in Dynamics 365 Contact Center

The deprecated features in Dynamics 365 Contact Center are listed in this article.

Administrators and IT professionals can use this information to prepare for future releases.

> [!IMPORTANT]
> "Deprecated" means we intend to remove the feature or capability in a major future release. The feature or capability will continue to work and will be fully supported until it's officially removed. This deprecation notification might span a few years. After removal, the feature or capability won't work. We're informing you now to give you enough time to adjust and update your code before the feature or capability is removed.

## WhatsApp channel through Azure Communication Services is deprecated

Microsoft deprecated support for the WhatsApp channel through Azure Communication Services as of September 23, 2026, and will remove it on September 30, 2028. Existing WhatsApp channels configured through Azure Communication Services continue to operate until the removal date.  

For new WhatsApp deployments, consider using WhatsApp through Twilio. Existing WhatsApp channels configured through Twilio aren't affected by this deprecation.

Starting September 23, 2026, new customers of Azure Communication Services can't acquire or port phone numbers into Azure Communication Services. Existing customers of Azure Communication Services can continue to acquire and port numbers into or out of Azure Communication Services during the retirement period. Contact Microsoft Support if you need assistance.

## SMS channel through Azure Communication Services is deprecated

Microsoft deprecated the SMS channel through Azure Communication Services as of September 23, 2026, and will remove it on September 30, 2028. Starting September 23, 2026, customers without an existing Azure Communication Services resource in their tenant can't provision new SMS phone numbers or port existing numbers into Azure Communication Services. Existing customers only can continue to provision and port numbers and operate existing SMS channels through September 30, 2028. For new SMS deployments, use [SMS via Twilio](/dynamics365/customer-service/administer/configure-sms-channel-twilio) or [SMS via Infobip](../administer/configure-sms-channel-infobip.md). With either provider, customers manage number provisioning, carrier registration, and consent settings directly with the provider. Contact Microsoft Support if you need assistance.

## Forecasting in Contact Center to be deprecated

Effective October 30, 2026, forecasting for case and conversation volumes and for customer service representatives for conversations will be deprecated in Dynamics 365 Contact Center. Support ends on October 30, 2026, after which the feature will be removed.

We recommend that you use [forecast scenarios in workforce engagement management](../use/workforce-management-forecast-scenarios.md), which provides more advanced forecasting along with capacity planning, scheduling, and intraday management.

## Apple Messages for Business is deprecated

Onboarding for Apple Messages for Business is deprecated as of July 17, 2026. The removal date for Apple configuration options in Copilot Service admin center is September 30, 2026.

## Post-call survey setting on Language tab of voice workstream is deprecated

Effective August 01, 2025, the post-call survey toggle currently found in the voice workstream > **Language** tab in Copilot Service admin center is deprecated and removed. We recommend that you configure post-call surveys using [Configure feedback surveys using Copilot Studio](../administer/configure-surveys.md#enable-the-post-call-survey-for-the-voice-channel).

## Draft a chat response (preview) is deprecated

The draft a chat response (preview) feature is deprecated as of July 01, 2025. The support for the feature will be removed on July 14, 2025.

## Deprecation of local hosting support for the voice channel

The deprecation schedule of the local hosting capabilities for the legacy voice channel is as follows: 

- **Switzerland**: Effective October 31, 2024
- **India and Japan**: Effective September 09, 2024

For the existing legacy voice installations, the deprecation is the first step toward transitioning to the enhanced voice experience. To continue using the voice channel, you should explore the global cloud deployment option in the nearest geographic location, subject to your country or region laws for using the voice channel in Dynamics 365 Contact Center. Learn more in [Supported cloud locations for voice channel](/dynamics365/customer-service/administer/voice-channel-region-availability).

### Related information

[Deprecations in Customer Service](/dynamics365/customer-service/implement/deprecations-customer-service)  
[Important changes (deprecations) coming in Power Apps, Power Automate](/power-platform/important-changes-coming)  
