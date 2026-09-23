---
title: Migrate from Azure Communication Services Direct Routing to Operator Connect
description: Learn how to migrate Azure Communication Services Direct Routing to Microsoft Teams Operator Connect for Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 09/23/2026
ms.topic: how-to
ms.custom: bap-template
---

# Migrate from Azure Communication Services Direct Routing to Operator Connect

This article explains how to move public switched telephone network connectivity from Azure Communication Services Direct Routing to Microsoft Teams Operator Connect and reconnect the phone numbers to Dynamics 365 Contact Center.

With Operator Connect, a certified operator manages the carrier connection and session border controllers (SBCs). You manage operators, phone numbers, and assignments in the Microsoft Teams admin center. Choose this path if you want a carrier-managed service and don't want to operate SBCs for the migrated numbers.

> [!IMPORTANT]
> [!INCLUDE[Deprecation of Azure Communication Services](../includes/cc-acs-deprecation.md)]

[!INCLUDE[Prepare for the voice migration](../includes/voice-migration-prepare.md)]

## Choose an operator migration path

Choose a path based on whether your current carrier participates in Operator Connect:

- **Keep the current carrier**: Ask the carrier to move your existing number ranges to its Operator Connect service. This path reduces number-porting complexity.
- **Change carriers**: Select another participating Operator Connect provider and port the phone numbers from the current carrier. For large number ranges, plan staged ports and map each stage to a pilot group.

Review provider coverage and service availability in [Plan Operator Connect](/microsoftteams/operator-connect-plan).

## Confirm user and routing requirements

Before you enable the operator:

- Confirm that users who use Operator Connect are in TeamsOnly mode, which means that Teams is their only client for calls and chats.
- Identify Direct Routing voice routing policies that currently apply to the users or resource accounts.
- Decide how long Azure Communication Services Direct Routing and Operator Connect must coexist.
- Confirm emergency calling requirements with the selected operator.

> [!IMPORTANT]
> Don't assign Direct Routing voice routes to users or resource accounts that should use only Operator Connect. A global voice routing policy can unintentionally send Operator Connect or Teams Calling Plan calls to a Direct Routing trunk. Use targeted custom policies only for users who require Direct Routing.

## Enable the operator

Go to Microsoft Teams admin center, and complete the steps in [Configure Operator Connect](/microsoftteams/operator-connect-configure) to enable the operator.

## Move the phone numbers

Use the procedure for your selected carrier path.

### Keep the current carrier

1. Confirm that your carrier can move the existing number ranges from the current Direct Routing service to Operator Connect.
1. Agree on the migration date, coexistence period, and emergency address process.
1. Keep the Azure Communication Services Direct Routing configuration active until the Operator Connect numbers are available.
1. Have the operator upload the numbers to your tenant.

### Change carriers

1. Agree on a porting plan with the new Operator Connect provider.
1. For large ranges, schedule staged ports and identify pilot groups.
1. Coordinate interim routing with the current and destination carriers to reduce service interruption.
1. Have the new operator upload each ported number range to your tenant.

Learn more in [Get phone numbers with Operator Connect](/microsoftteams/get-phone-numbers-with-operator-connect).

## Assign and verify the numbers

1. Go to Microsoft Teams admin center, and follow the steps in [Manage phone numbers](/microsoftteams/assign-change-or-remove-a-phone-number-for-a-user) to assign the numbers.

1. Confirm that the migrated numbers appear and that the **Provider** column shows the selected Operator Connect provider.
1. Remove Direct Routing voice routing policies from users or resource accounts that now use only Operator Connect.

Learn more in [Considerations for Operator Connect](/microsoftteams/considerations-operator-connect).

[!INCLUDE[Connect the migrated numbers to Dynamics 365 Contact Center](../includes/voice-migration-connect-contact-center.md)]

[!INCLUDE[Validate the voice migration](../includes/voice-migration-validate.md)]

## Verify Operator Connect status

In the Microsoft Teams admin center, confirm that:

- **Voice** > **Operators** shows the operator as **Enabled** for the required countries or regions.
- **Voice** > **Phone numbers** shows the expected provider for each migrated number.
- Emergency calling follows the configured operator and organizational policies.

After validation, remove obsolete Azure Communication Services Direct Routing routes and session border controller configuration for the migrated numbers.

## Related information

[Plan migration from Azure Communication Services](migrate-from-azure-communication-services.md)  
[Configure Teams Phone in the voice channel](configure-teams-phone-in-voice-channel.md)  
