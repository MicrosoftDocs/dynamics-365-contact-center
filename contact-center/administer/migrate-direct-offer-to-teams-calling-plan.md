---
title: Migrate from Azure Communication Services Direct Offer to Teams Calling Plan
description: Learn how to migrate Azure Communication Services Direct Offer phone numbers to Microsoft Teams Calling Plan for Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 09/23/2026
ms.topic: how-to
ms.custom: bap-template
---

# Migrate from Azure Communication Services Direct Offer to Teams Calling Plan

This article explains how to move phone numbers from Azure Communication Services Direct Offer to Microsoft Teams Calling Plan and reconnect them to Dynamics 365 Contact Center. The migration is a manual support-assisted process.

> [!IMPORTANT]
> [!INCLUDE[Deprecation of Azure Communication Services](../includes/cc-acs-deprecation.md)]

[!INCLUDE[Prepare for the voice migration](../includes/voice-migration-prepare.md)]

## Check number and license eligibility

Phone number eligibility depends on the country or region, number capabilities, and the suppliers that provide the number for each service. Availability of Teams Calling Plan in a country or region doesn't guarantee that an Azure Communication Services number can be migrated. Contact Microsoft support for guidance.

Before you submit a migration request:

1. Review [Teams Calling Plan availability](/microsoftteams/calling-plan-overview) for the countries or regions where you have phone numbers. For example, migration isn't supported for Azure Communication Services phone numbers in the Asia Pacific region.
1. Confirm that each Azure Communication Services number has capabilities that are available in Teams Calling Plan and that the number supplier supports the migration.
1. Confirm that your Microsoft Teams Phone and Calling Plan licenses support the number type and quantity that you want to migrate. Learn more in the following articles:
   - [Microsoft Teams Calling Plans](/microsoftteams/calling-plans-for-office-365)
   - [How many phone numbers can you get?](/microsoftteams/how-many-phone-numbers-can-you-get)
1. Record whether each number was acquired from Azure Communication Services or ported to Microsoft. The number origin affects license quota. If a number is moved without being identified as a ported number, Teams can treat it as newly acquired and count it against your quota immediately. Clearly identify the origin of every number in the migration request.

## Submit the migration request

No automated process exists to move phone numbers from Azure Communication Services Direct Offer to Teams Calling Plan. Submit a request through the [Microsoft telephone number services portal](https://pstnsd.powerappsportals.com/create-ticket/). If you can't create a ticket, use the portal's chat option.

Provide the following information:

- **Title**: State that you want to move Azure Communication Services phone numbers to Teams Calling Plan.
- **Description**:
  - Phone numbers to migrate. Attach a comma-separated values file for a large number list.
  - Destination Microsoft 365 tenant ID.
  - Teams number type: User, Service, or Toll-free.
  - Teams number capability: User, Voice applications, or Conference, as applicable.
  - Number origin: Ported to or acquired from Azure Communication Services.
- **Customer profile**: Select **Azure Communication Services**.
- Select the country or region of the numbers.
- **Case type**: Select the available option for moving phone numbers between Microsoft 365 and Azure Communication Services. Portal labels can vary, so clearly state that the source is Azure Communication Services and the destination is Teams Calling Plan in the title and description.
- **Type of Number**: Select the Azure Communication Services number type, such as **Toll Free** or **Geographic**.
- **Azure Immutable Resource ID**: Enter the immutable ID of the Azure Communication Services resource.
- **Azure Subscription ID**: Enter the Azure subscription ID.
- **Requested porting Date/Time**: Enter the requested migration date and time.

> [!NOTE]
> Migration requests are processed during Eastern Time operational hours, 9:00 AM through 5:30 PM, Monday through Friday. The support team typically contacts you by the next business day.

## Complete the number migration

1. Work with Microsoft support to confirm eligibility and schedule the migration.
1. Plan for a possible service interruption during the migration window.
1. After support confirms that the migration is complete, sign in to the Microsoft Teams admin center.
1. Go to **Voice** > **Phone numbers**.
1. Select an unassigned number, and then select **Change usage**.
1. Set the number usage required for the destination resource account. Learn more in [Manage the usage of a phone number](/microsoftteams/manage-the-usage-of-a-phone-number).
1. Configure an emergency address for each migrated number. Learn more in [Manage emergency locations for your organization](/microsoftteams/add-change-remove-emergency-location-organization).

[!INCLUDE[Connect the migrated numbers to Dynamics 365 Contact Center](../includes/voice-migration-connect-contact-center.md)]

[!INCLUDE[Validate the voice migration](../includes/voice-migration-validate.md)]

## Related information

[Plan migration from Azure Communication Services](migrate-from-azure-communication-services.md)  
[Configure Teams Phone in the voice channel](configure-teams-phone-in-voice-channel.md)  
