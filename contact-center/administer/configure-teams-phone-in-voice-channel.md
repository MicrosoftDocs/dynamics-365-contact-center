---
title: Configure Teams Phone in voice channel
description: Learn how to configure Teams Phone in the voice channel to streamline call management and enhance customer support in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection:
ms.date: 02/20/2026
ms.custom:
  - bap-template
  - ai-gen-docs-bap
  - ai-gen-description
  - ai-seo-date:05/02/2025
---

# Configure Teams Phone in voice channel

Integrate your existing Microsoft Teams Phone with Dynamics 365 Contact Center to simplify your voice call configuration.

## Prerequisites

The prerequisites to configure the Teams environment extensibility are as follows:

- Voice channel is configured in Dynamics 365 Contact Center. Learn more in [Provision channels](../implement/provision-channels.md).

- Specific licensing requirements are applicable for both configuring the feature and handling of calls by the representatives. Learn more in [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/?LinkId=866544).
- Enterprise Voice is available as described in [Teams Phone features](/azure/communication-services/concepts/pricing/teams-interop-pricing#teams-phone-features).
- Outbound calling prerequisites are applicable. Learn more at [Outbound calling prerequisites](/azure/communication-services/concepts/interop/tpe/teams-phone-extensibility-connectivity-cost#outbound-calling-prerequisites).
- [**PSTN connectivity**](/microsoftteams/pstn-connectivity): Teams Calling Plan (service numbers only are supported), Operator Connect, or Direct Routing.
- To synchronize the phone number, you need the [Teams Administrator or Teams Telephony Administrator role](/entra/identity-platform/quickstart-configure-app-access-web-apis) and [TeamsResourceAccount.Read.All Graph permission](/graph/permissions-reference).
   - **TeamsResourceAccount.Read.All** (delegated): This permission allows the app to read all Teams resource accounts within the tenant. It is required for the sync operation to access and transfer phone number data from Teams Resource Account to Dynamics 365 Contact Center.
   - Any app registered under the tenant must be granted this delegated permission. Admin consent must be provided in Entra ID to enable the app to act on behalf of the user for resource account access.
   - [Register a new app](/entra/identity-platform/quickstart-register-app#register-an-application) or select an existing one and configure permissions. Under API permissions, add **TeamsResourceAccount.Read.All** and **TeamsResourceAccount.Read** (delegated).
   - Request and grant admin consent for the delegated permission to ensure compliance and operational capability.
    
     > [!NOTE]
     > If you are using a Teams Calling Plan, [service numbers](/microsoftteams/manage-phone-numbers-landing-page) only are supported.

## Create a Teams resource account

In Teams, a resource account is required for every number that's used with Dynamics 365 Contact Center application.

Download the [script](https://github.com/microsoft/Dynamics365-Apps-Samples/blob/master/contact-center/TeamsPhoneSystem-TeamsAdminCenterOnboardScript.ps1) and run it to create and associate the Teams resource account with the Dynamics 365 application.

Alternatively, you can run the following PowerShell cmdlets in the specified order. The Teams resource account is created and associated with the Dynamics 365 application.

As a Teams administrator, run the following Teams PowerShell cmdlets in administrator mode.

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

Complete the steps in [Assign a license](/microsoftteams/manage-resource-accounts#assign-a-license) to assign a license to the Teams resource account.

## Assign service number to Teams resource account

Complete the steps in [Manage phone numbers for users](/microsoftteams/assign-change-or-remove-a-phone-number-for-a-user) to assign a service number through Teams admin center.

Complete the steps in [Assign a phone number](/microsoftteams/manage-resource-accounts#assign-a-phone-number) to assign a calling plan service number to the Teams resource account.

If you're assigning a Direct Routing service phone to the Teams resource account, then use the following steps instead.

1. Run the following Teams PowerShell cmdlet to assign a Direct Routing service phone number to the Teams resource account.
   ```
    Set-CsPhoneNumberAssignment -Identity <TeamsResourceAccountEmailAddress> -PhoneNumber <DirectRoutingPhoneNumberInE164Format> -PhoneNumberType DirectRouting
   ```
1. Run the following Teams PowerShell cmdlet to assign a Direct Routing Policy to the Teams resource account. The Team resource account can then place phone calls in external phone number consult or transfer scenarios.

   ```
   Grant-CsOnlineVoiceRoutingPolicy -Identity <TeamsResourceAccountEmailAddress> -PolicyName "<DirectRoutingPolicyName>"
   ```
   If you want to assign an operator connect service phone to the Teams resource account, then use the following steps instead.

   ```   
   Set-CsPhoneNumberAssignment -Identity <TeamsResourceAccountEmailAddress> -PhoneNumber <OperatorConnectPhoneNumberInE164Format> -PhoneNumberType OperatorConnect
   ```

## Configure Teams Phone in the voice channel

Complete the following steps to configure inbound calling and sync the Teams service phone numbers.

1. In the site map of Copilot Service admin center, select **Channels** in **Customer support**. The **Channels** page appears.

1. Select **Manage** for **Phone numbers**.
1. On the **Phone numbers** page, select **Advanced**.
1. On the **Manage telephony** page, navigate to the **Teams phone system** tab. The **Azure Communication Services resource ID** and **Dynamics App ID** appear.
1. Select **Sync from Teams** to create the phone number record for the Teams service number.
1. [Create a workstream](/dynamics365/customer-service/administer/create-workstreams).
1. Add a voice channel to the workstream for the Teams service phone number by performing the steps in [Set up inbound calling](/dynamics365/customer-service/administer/voice-channel-inbound-calling).

> [!NOTE]
> Learn about [known issues in Teams phone in the voice channel](https://go.microsoft.com/fwlink/p/?linkid=2165393).

## How representatives receive and handle the Teams calls

When a customer calls the Teams Phone number to connect with a representative, the representative receives the call notification on the Copilot Service workspace app. The representative can use the call controls to interact with the customers.

For compliance, when call recording is enabled, an announcement plays to notify participants that the call is being recorded.

### FAQ

**What should I do if the conversation form fails to load after initiating or connecting an outbound call?**

After the system initiates the outbound call, if issues arise in assigning the outbound conversation, the representative receives an alert that the conversation isn't created. The alert suggests that they initiate the outbound call to the customer again.

### Related information

[Call recordings and transcripts](/dynamics365/customer-service/administer/voice-channel-configure-transcripts?context=/dynamics365/contact-center/context/administer-context)   
[Call a customer](/dynamics365/customer-service/use/voice-channel-call-customer?context=/dynamics365/contact-center/context/use-context)  
[Use call controls and representative desktop for voice](../use/voice-channel-agent-experience.md)  