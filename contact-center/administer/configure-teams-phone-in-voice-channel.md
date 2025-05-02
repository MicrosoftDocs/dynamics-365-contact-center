---
title: Configure Teams Phone in voice channel (preview)
description: Learn how to configure Teams Phone in the voice channel to streamline call management and enhance customer support.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: null
ms.date: 05/02/2025
ms.custom:
  - bap-template
  - ai-gen-docs-bap
  - ai-gen-description
  - ai-seo-date:05/02/2025
---

# Configure Teams Phone in voice channel (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Integrate your existing Microsoft Teams Phone with Dynamics 365 Contact Center to simplify your voice call configuration.

The high-level process to configure the Teams Phone is as follows:

1. Verify prerequisites.
1. Enable voice channel.
1. Create Teams resource account for the Dynamics 365 application ID and associate Teams resource account with the Dynamics organization’s Azure Communication Services resource.
1. Assign license to Teams resource account.
1. Assign service number to Teams resource account.
1. Configure inbound calling.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- Teams tenant with [Teams Phone license](/microsoftteams/teams-phone-licensing#teams-phone-licensing) with Teams Calling Plan, Teams Direct Routing, or Teams Operator Connect [PSTN connectivity](/microsoftteams/pstn-connectivity) options.
- [Service phone number](/microsoftteams/manage-phone-numbers-landing-page#service-numbers).
    - We recommend that you use a non-production service phone number for testing Teams Phone.
    - Create a resource account for the service number when you enable the Dynamics 365 organization for Teams Phone system.
- Dynamics 365 Contact Center or Dynamics 365 Customer Service premium license with the [voice channel provisioned](../implement/provision-channels.md#set-up-channels) and configured.
- User with License Administrator role and Teams administrator role.
  - A user with License Administrator, Teams administrator, and Skype for Business Administrator roles is needed for creating the Teams resource account and for assigning a Teams calling license to the Teams resource account.
  - The Teams Phone in Dynamics 365 Contact Center voice channel also requires the latest Microsoft Teams PowerShell module installed in the user’s machine.
    - [Install Microsoft Teams PowerShell module](/microsoftteams/teams-powershell-install#installing-using-the-powershellgallery) in the user’s system if it is not yet installed.
    - [Update the Microsoft Teams PowerShell module](/microsoftteams/teams-powershell-install#update-teams-powershell-module) if it's already installed.
  - To synchronize the phone number, the Teams Administrator or Teams Telephony Administrator role and [TeamsResourceAccount.Read.All Graph permission](/graph/permissions-reference).
  - At runtime, the service representatives assigned to the voice queue need a Teams calling license.

## Enable the voice channel

Perform the following steps to configure the Teams Phone in the admin center of Dynamics 365 Customer Service:

Provision the voice channel by performing the steps in provision channels. An Azure Communication Services resource is provisioned when the voice channel is provisioned.

The Teams administrator requires the Azure Communication Service immutable resource ID and Dynamics Application ID to create the Teams resource account and connect it with the organization’s Azure Communication Services resource. 
1.	In the site map of Copilot Service admin center, select **Channels** in **Customer support**. The **Channels** page appears.
1.	Select **Manage** for **Phone numbers**.
1.	On the **Phone numbers** page, select the **Advanced** button
1.	On the **Manage telephony** page, navigate to the **Teams telephony** tab. You’ll see the Azure Communication Service immutable resource ID with a Dynamics 365 Application ID.

## Create a Teams resource account

In Teams, a resource account is required for every number that's used with Dynamics 365 Contact Center application.

Download the [script](https://github.com/microsoft/Dynamics365-Apps-Samples/blob/neeranelli-patch-11/contact-center/TeamsPhoneSystem-TeamsAdminCenterOnboardScript.ps1) and run it to create and associate the Teams resource account with the Dynamics 365 application.

Alternatively, you can run the following PowerShell cmdlets  in the specified order to create and associate the Teams resource account with the Dynamics 365 application.

As a Teams administrator, run the following Teams PowerShell cmdlets.

1. To sign in.
   ```
   Connect-MicrosoftTeams
   ``` 
1. To create the Teams resource account for the Dynamics 365 application ID.
   ```
   New-CsOnlineApplicationInstance -UserPrincipalName <NewTeamsResourceAccountEmailAddress> -DisplayName "<NewTeamsResourceAccountDisplayName>" -ApplicationID "GUID"
   ```
1. Copy the Object ID of the new Teams resource account. You need it for running the next cmdlets.

1. Associate the organization's Azure Communication Services resource with the Teams resource account.
   ```
   Set-CsOnlineApplicationInstance -Identity <TeamsResourceAccountObjectId> -ApplicationId "4b8f0dce-d7d5-47a3-a27c-1764b90505e2" -AcsResourceId "<OrganizationAzureCommunicationServiceImmutableResourceID>"
   
   Sync-CsOnlineApplicationInstance -ObjectId <TeamsResourceAccountObjectId> -ApplicationId "4b8f0dce-d7d5-47a3-a27c-1764b90505e2" -AcsResourceId "<OrganizationAzureCommunicationServiceImmutableResourceID >"
   ```

## Assign license to Teams resource account

Assign license to Teams resource account by performing the steps in [Assign a license](/microsoftteams/manage-resource-accounts#assign-a-license).

## Assign service number to Teams resource account

To assign a service nunber through Teams admin center, perform the steps in [Manage phone numbers for users](/microsoftteams/assign-change-or-remove-a-phone-number-for-a-user)

For assigning a Calling plan service number to the Teams resource account, perform the steps in [Assign a phone number](/microsoftteams/manage-resource-accounts#assign-a-phone-number).

If you're assigning a Direct Routing service phone to the Teams resource account, then use the following steps instead.

1. Run the following Teams PowerShell cmdlet to assign a Direct Routing service phone number to the Teams resource account.
   ```
    Set-CsPhoneNumberAssignment -Identity <TeamsResourceAccountEmailAddress> -PhoneNumber <DirectRoutingPhoneNumberInE164Format> -PhoneNumberType DirectRouting
   ```
1. Run the following Teams PowerShell cmdlet to assign a Direct Routing Policy to the Teams resource account. This enables the Team resource account to place phone calls in external phone number consult or transfer scenarios.

   ```
   Grant-CsOnlineVoiceRoutingPolicy -Identity <TeamsResourceAccountEmailAddress> -PolicyName "<DirectRoutingPolicyName>"
   ```
   If you want to assign an operator connect service phone to the Teams resource account, then use the following steps instead.

   ```   
   Set-CsPhoneNumberAssignment -Identity <TeamsResourceAccountEmailAddress> -PhoneNumber <OperatorConnectPhoneNumberInE164Format> -PhoneNumberType OperatorConnect
   ```
 
## Configure inbound calling

Perform the following steps to configure inbound calling and sync Teams service phone numbers.

1. In the site map of Copilot Service admin center, select **Channels** in **Customer support**. The **Channels** page appears.
1. Select **Manage** for **Phone numbers**.
1. On the **Phone numbers** page, select **Advanced**.
1. On the **Manage telephony** page, navigate to the **Teams telephony** tab.
1. Select **Sync** to create the phone number record for the Teams service number. 
1. Create a workstream, and then add a voice channel to the workstream for the Teams service phone number by performing the steps in [Set up inbound calling](/dynamics365/customer-service/administer/voice-channel-inbound-calling).

## How representatives receive and handle the Teams calls

When a customer calls the Teams Phone number to connect with a representative, the representative receives the call notification on both the Copilot Service workspace app and Teams desktop or web app. The representative needs to accept the call notification on the Copilot Service workspace app. The representative can use the call controls to interact with the customers.

### Related information

[Call recordings and transcripts](/dynamics365/customer-service/administer/voice-channel-configure-transcripts?context=/dynamics365/contact-center/context/administer-context)   
[Call a customer](/dynamics365/customer-service/use/voice-channel-call-customer?context=/dynamics365/contact-center/context/use-context)  
[Use call controls and representative desktop for voice](../use/voice-channel-agent-experience.md)  
[Transfer calls and consult with users](/dynamics365/customer-service/use/voice-channel-transfer-consult?context=/dynamics365/contact-center/context/use-context)  


