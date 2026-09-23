---
title: Migrate from Azure Communication Services Direct Routing to Teams Direct Routing
description: Learn how to migrate Azure Communication Services Direct Routing to Microsoft Teams Direct Routing for Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 09/23/2026
ms.topic: how-to
ms.custom: bap-template
---

# Migrate from Azure Communication Services Direct Routing to Teams Direct Routing

This article explains how to move an Azure Communication Services Direct Routing configuration to Microsoft Teams Direct Routing and reconnect the phone numbers to Dynamics 365 Contact Center. You can use a full cutover or a period of coexistence.

Teams Direct Routing requires a Microsoft Teams Phone license for each user or resource account. It also moves administration from the Azure portal to the Microsoft Teams admin center and Microsoft Teams PowerShell.

> [!IMPORTANT]
> [!INCLUDE[Deprecation of Azure Communication Services](../includes/cc-acs-deprecation.md)]

[!INCLUDE[Prepare for the voice migration](../includes/voice-migration-prepare.md)]

## Assess your Direct Routing configuration

Document the following information before you design the target configuration:

- Session border controllers (SBCs), including their fully qualified domain names, capacity, certificates, signaling settings, and firewall rules.
- Voice routes, voice routing policies, dial plans, and phone number ranges.
- Applications, interactive voice response systems, and other workloads that depend on the current routes.
- Critical services and the users, departments, or number ranges to migrate in each phase.

If you're adding the workload to an existing Teams Direct Routing deployment, confirm that the current SBCs have enough capacity for the Dynamics 365 Contact Center traffic.

## Choose a domain transition approach

You can't assign an SBC fully qualified domain name to both Azure Communication Services and Teams Direct Routing at the same time. Choose one of the following approaches:

- **Full cutover**: Remove the SBC configuration from Azure Communication Services, wait for the change to propagate, and then add the same fully qualified domain name to Teams Direct Routing.
- **Coexistence**: Configure a different fully qualified domain name or alias for the Teams trunk. For example, keep `sbc.contoso.com` in Azure Communication Services and use `sbc2.contoso.com` in Teams during the transition.

For coexistence, ensure that the SBC certificate covers both domain names, or use separate certificates.

> [!WARNING]
> A full cutover can cause downtime while the Azure Communication Services change propagates and before the domain is available in Teams Direct Routing.

## Configure Teams Direct Routing

Prepare the Teams configuration while the current service remains available.

1. In the Microsoft Teams admin center, go to **Voice** > **Direct Routing**.
1. Add a trunk for the SBC fully qualified domain name.
1. Configure the Session Initiation Protocol signaling port, typically `5061`, media bypass, and other required trunk settings.
1. In **Voice** > **Voice routing policies** and **Voice** > **Dial plans**, configure the routes and number patterns handled by the SBC.
1. In **Voice** > **Phone numbers**, add individual Direct Routing numbers or upload a comma-separated values file that contains a number range.

Learn more in the following articles:

- [Connect your session border controller to Teams Phone](/microsoftteams/direct-routing-connect-the-sbc)
- [Configure voice routing for Direct Routing](/microsoftteams/direct-routing-voice-routing)
- [Plan Direct Routing](/microsoftteams/direct-routing-plan)

Some configuration requires Microsoft Teams PowerShell. Install the latest Microsoft Teams PowerShell module before you use the Direct Routing cmdlets.

## Update the SBC

Coordinate the following changes with the SBC administrator:

- **Domain and certificate**: Configure the domain name used for Teams Direct Routing. The public certificate must come from an accepted certificate authority and include the domain name in the Subject Alternative Name or Common Name.
- **Signaling**: Configure Session Initiation Protocol signaling to the required Microsoft Teams endpoints, including `sip.pstnhub.microsoft.com` and regional secondary endpoints.
- **Firewall**: Allow signaling on port `5061` and allow the Microsoft Teams media address ranges. Azure Communication Services and Microsoft Teams can use different media address ranges.
- **Carrier routing**: Route the pilot or production phone numbers to the Teams trunk at the appropriate migration stage.

Learn more in [Configure Direct Routing](/microsoftteams/direct-routing-configure).

## Pilot the Teams trunk

Before the production cutover:

1. Assign a test number or a noncritical existing number to the Teams Direct Routing path.
1. Assign the number to a test user or resource account.
1. Test Transport Layer Security connectivity and Session Initiation Protocol options status.
1. Test incoming and outgoing calls.
1. Test emergency calling where applicable.
1. Monitor the signaling flow. Learn more in [Monitor Session Initiation Protocol signaling](/microsoftteams/direct-routing-monitor-sip-ladder).

## Transition production numbers

Complete the following steps during the scheduled maintenance window:

1. For a full cutover that reuses the domain name, remove the SBC from the Azure Communication Services Direct Routing configuration and wait for the change to propagate.
1. Complete or enable the Teams Direct Routing trunk and voice routes.
1. Update carrier routing for the production phone numbers.
1. Assign the phone numbers to the appropriate Microsoft Teams users or resource accounts.
1. Enable the required users for Enterprise Voice and assign custom voice routing policies when your design requires them. Learn more in [Set up Teams Phone in your organization](/microsoftteams/setting-up-your-phone-system).

[!INCLUDE[Connect the migrated numbers to Dynamics 365 Contact Center](../includes/voice-migration-connect-contact-center.md)]

[!INCLUDE[Validate the voice migration](../includes/voice-migration-validate.md)]

Monitor the [Direct Routing Health Dashboard](/microsoftteams/direct-routing-health-dashboard) and call quality analytics during the initial production period. Confirm that the SBC is online and that signaling status is active.

## Decommission the Azure Communication Services configuration

After validation, remove the migrated SBC trunks or disable the migrated voice route patterns in the Azure portal. Release Azure Communication Services phone numbers that you ported out only after you confirm that no workload uses them.

## Related information

- [Plan migration from Azure Communication Services](migrate-from-azure-communication-services.md)
- [Configure Teams Phone in the voice channel](configure-teams-phone-in-voice-channel.md)
