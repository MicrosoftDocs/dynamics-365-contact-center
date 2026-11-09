---
title: Enable biometric authentication and fraud detection on a workstream (preview)
description: Turn on the biometric authentication and fraud detection behavior for a workstream so the fraud and authentication flow runs on incoming calls in Dynamics 365 Contact Center.
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

#customer intent: As a contact center administrator, I want to enable biometric authentication and fraud detection on a workstream so that the fraud and authentication flow runs on every incoming call for my organization.
---

# Enable biometric authentication and fraud detection on a workstream (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Enable the **Biometric authentication and fraud detection** behavior on a workstream to control how incoming calls to the workstream are handled. When you turn on this behavior and select an authentication profile, every incoming call on the workstream's phone number goes through the configured biometric authentication and fraud detection checks and the outcome is displayed to the contact center representative.

[!INCLUDE [bafd-note-small](../includes/cc-bafd-note-small.md)]

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

* An authentication profile that's already configured for the organization or workstream. To create one, go to [Configure authentication profiles](configure-authentication-profiles.md).
* The appropriate administrator role to edit workstreams in the Copilot Service admin center, such as Omnichannel admin.

## Open the workstream

The workstream shows the phone number that's tied to the organization, along with other details for that organization.

1. Sign in to the **Copilot Service admin center** app. 
1. Select **Workstreams** from the navigation bar.
1. Select the workstream for your organization. Confirm that the phone number and other details shown match the organization you want to enable. 

## Turn on biometric authentication and fraud detection

Turn on the behavior so the biometric authentication and fraud detection flow runs on every incoming call on the organization's workstream.

1. On the workstream, select **Edit**. 
1. Go to the **Behaviors** section. 
1. Turn on the **Biometric authentication and fraud detection** setting. When this setting is on, the configured authentication policy is applied on every incoming call on this organization's workstream.

> [!NOTE]
> The change on the workstream takes effect immediately.

## Select the authentication policy

Select the authentication profile that's required for the organization or workstream so the flow knows how to authenticate callers.

1. In the same **Behaviors** section, select the **Authentication policy** required for the organization or workstream.
1. **Save** your changes.

> [!NOTE]
> If no authentication policy is selected while the **Biometric authentication and fraud detection** setting is on, nothing happens. You need to select an authentication policy for the change to take place.

## Related information
* [Configure authentication profiles](configure-authentication-profiles.md)
* [Biometric authentication and fraud detection overview](biometric-authentication-fraud-detection-overview.md)
