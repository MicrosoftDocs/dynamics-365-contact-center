---
title: Set up Contact Center workspace (preview)
description: Learn how to configure representative access to Contact Center workspace and embed it in a custom host application in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.date: 11/16/2026
ms.topic: how-to
ms.custom: bap-template
ai-usage: ai-assisted
---

# Set up Contact Center workspace (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Contact Center workspace gives Contact Center representatives a conversation-focused experience for voice and digital messaging in Dynamics 365 Contact Center. Representatives can use it in a browser or embedded in a customer relationship management (CRM) application.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

As an administrator, prepare the environment, configure representative access, and, if needed, embed the workspace in a custom host application. Both deployment options use the same channels, queues, routing, presence, and Copilot settings. Learn more about the representative experience in [Contact Center workspace overview (preview)](../use/contact-center-workspace-overview.md).

## Prerequisites

Before you configure access, make sure that you meet the following requirements:

- Use an account with the **System Administrator** security role in your contact center's Dynamics 365 environment.
- Verify regional availability, licensing, hardware, and network requirements. Learn more in [System requirements for Dynamics 365 Contact Center](../implement/system-requirements-contact-center.md).
- Enable the omnichannel capabilities and channels that your representatives need. Learn more in [Provision channels](../implement/provision-channels.md).
- Add each representative as a user in the environment, with a Microsoft Entra ID account in your tenant and a Dynamics 365 Contact Center license. Learn more in [Add users and assign roles](/dynamics365/customer-service/implement/add-users-assign-roles).
- Provide representatives with the [Contact Center workspace URL for your organization's region](../use/contact-center-workspace-overview.md#access-contact-center-workspace). The portal must match your environment and your organization's data boundary.
- Use a current Chromium-based browser, such as Microsoft Edge or Google Chrome. For voice, provide a microphone and speakers, and allow microphone access when the browser prompts.

## Assign security roles and privileges

Assign the **Omnichannel agent** role to representatives and the **Omnichannel supervisor** role to supervisors. Assign both roles to users who perform both tasks, and retain any other roles required for their work. You can also assign Contact Center roles through Microsoft Entra security group teams. Learn more in [Assign security roles](/power-platform/admin/assign-security-roles).

If you use custom roles for additional permissions, retain the **Omnichannel agent** role assignment. A custom role containing only the agent privilege (`prvAgent`) doesn't replace the built-in role. Learn more in [Create or edit a security role](/power-platform/admin/create-edit-security-role) and [Manage personas and custom security roles](/dynamics365/customer-service/administer/role-persona-mapping).

Review the following privileges when you customize representative roles. The workspace displays the related actions only to representatives who have the required privileges.

| Task | Required privileges |
|---|---|
| View the linked customer in **Conversation details**. | **Read** on **Contact** (`prvReadContact`) |
| Link, unlink, edit, or create a contact. | **Read**, **Write**, and **Create** on **Contact** (`prvReadContact`, `prvWriteContact`, and `prvCreateContact`) |
| View notes. | **Read** on **Note** (`prvReadNote`) |
| Take notes. | **Create** on **Note** (`prvCreateNote`) |

Choose access levels that meet your organization's data access requirements. Learn more in [Security roles and privileges](/power-platform/admin/security-roles-privileges).

Representatives don't need read access to the inbox configuration table to use the inbox views configured in their experience profile.

## Configure work distribution and experience profiles

In addition to security roles, configure the following settings for your representatives.

| Configuration | Action |
|---|---|
| Workstreams and queues | Configure channels, routing rules, and queues, and add representatives to the queues they work on. Learn more in [Create and manage workstreams](/dynamics365/customer-service/administer/create-workstreams) and [Create and manage queues](/dynamics365/customer-service/administer/queues-omnichannel). |
| Capacity | Assign a capacity profile for the work the representative handles. Learn more in [Create and manage capacity profiles](/dynamics365/customer-service/administer/capacity-profiles). |
| Outbound voice | Assign a voice capacity profile and an outbound profile to representatives who place calls. Learn more in [Configure outbound and inbound profiles](/dynamics365/customer-service/administer/configure-outbound-inbound-profiles). |
| Experience profiles | Assign an experience profile and configure the inbox views and conversation cards. Learn more in [Create and use experience profiles](/dynamics365/customer-service/administer/create-agent-experience-profile), [Add users to experience profiles](/dynamics365/customer-service/administer/add-profile-default), and [Configure the inbox](/dynamics365/customer-service/administer/configure-inbox). |
| Copilot | Configure the required Copilot features and make them available through the experience profile. Learn more in [Configure Copilot features](configure-copilot-features.md). |

## Review technical considerations

Plan for the following requirements in either deployment option:

- **Network access**: Allow the required Contact Center, authentication, and communication endpoints and the cookies required for authentication and presence. Learn more in [Allow access to websites](../implement/system-requirements-contact-center.md#allow-access-to-websites).
- **Virtual desktops**: Citrix, VMware, and Azure Virtual Desktop environments are supported. Enable media optimization for the best call audio.
- **Desktop companion application**: When connected, the desktop companion application handles call audio. Representatives manage speaker and microphone settings in that application instead of the workspace. Learn more in [Install and manage desktop companion application for voice channel](install-manage-desktop-app.md).
- **Contact search**: Enable Dataverse search if representatives need to search for contacts by name or phone number in the outbound dialer. Learn more in [Configure Dataverse search](/power-platform/admin/configure-relevance-search-organization).

## Verify representative access

Before you embed the workspace or make it available to representatives, test standalone access with a representative account that has the intended security roles:

1. Open the Contact Center workspace portal for your region, and sign in with the representative account.
1. Confirm that the expected inbox views and configured features appear.
1. Set presence to **Available**.
1. Route a test conversation through a configured channel and queue, accept it, and verify that the representative can respond.
1. For voice, test microphone and speaker access. If outbound calling is required, place a test call with the assigned outbound profile.
1. Verify that customer information and note actions match the representative's permissions.

## Embed the workspace in a custom host application

Embed Contact Center workspace in an iframe so that representatives can handle conversations without leaving their primary CRM application. Dynamics 365 Contact Center manages conversations, while the host CRM provides customer records. The workspace layout adapts to the panel or page region that hosts it.

This deployment requires your own host integration. In addition to completing the representative setup, ensure that you have:

- Administrator access to the host CRM and permission to add an iframe, configure trusted URLs, and allow browser permissions.
- The licenses and system requirements for the host CRM, with the application and its dependencies hosted over HTTPS.
- A developer to provide a browser-compatible JavaScript computer telephony integration (CTI) driver if you need CRM record actions, Contact Center events, or click-to-dial integration.

> [!WARNING]
> Your organization or implementation partner is responsible for designing, testing, securing, deploying, maintaining, and supporting its custom CTI driver. Use sample drivers for illustration, and deploy a driver supported by your organization or implementation partner.

### Get the workspace embed URL

> [!NOTE]
> Until general availability, the Contact Center workspace URL isn't available in Copilot Service admin center. Use the URL for your region in [Access Contact Center workspace](../use/contact-center-workspace-overview.md#access-contact-center-workspace).

Use the URL provided by Copilot Service admin center:

1. Open Copilot Service admin center.
1. On the welcome page, under **Your default contact center**, select **Open**.
1. Select the **Conversation widget** tab.
1. Under **Integration into third-party systems**, copy the primary Contact Center workspace URL for your environment.

The URL for the earlier embedded experience is also available and is labeled as legacy.

Keep the environment information in the copied URL. Use Microsoft Entra sign-in for authentication, and keep access tokens, passwords, and client secrets outside the embed URL and CTI driver.

### Configure the host application

Work with your CRM administrator to add the workspace:

1. Add an iframe in the panel or page region where representatives handle conversations.
1. Set its source to the workspace embed URL.
1. If you use a custom CTI driver, set the `useCustomCTI` query parameter to `1`. Use `?` for the first query parameter or `&` to append it to an existing query string.
1. In the host application's trusted URL or content security policy configuration, allow the origin of the workspace URL to load in an iframe. Allow network access to `*.contactcenterai.powerplatform.com` and the required Contact Center endpoints. Learn more in [Allow access to websites](../implement/system-requirements-contact-center.md#allow-access-to-websites).
1. Grant the iframe microphone access for voice and autoplay for audio. Grant clipboard permissions only if the integration uses them.
1. Allow sign-in pop-ups and microphone access in the browser.
1. Give the panel enough space for the conversation controls and any Copilot pane. Test resizing at the screen sizes and zoom levels that representatives use.

> [!IMPORTANT]
> Microsoft Entra sign-in requires a pop-up window or a top-level browser tab. Representatives can sign in through the pop-up window, or sign in to the Dynamics 365 environment in a top-level tab and then reload the CRM page.

The following example grants microphone and autoplay permissions for voice. Replace `WORKSPACE_EMBED_URL` with the copied URL. For a custom driver, append `useCustomCTI=1`, using `?` or `&` as appropriate. Microphone access and communication APIs require an HTTPS secure context.

```html
<iframe
  id="ccaas-frame"
  title="Dynamics 365 Contact Center"
  src="WORKSPACE_EMBED_URL"
  allow="microphone; autoplay"
></iframe>
```

### Configure a custom CTI driver

Deploy the host CRM, workspace iframe, and custom CTI driver independently. The workspace loads the driver from the location you configure in Dataverse. The driver connects the embed SDK to the CRM.

Your developer supplies a single browser-compatible JavaScript file that registers a class on `window.CCaaS.CTIDriver` and implements the following interface:

```typescript
interface ICTIInterface {
  initialize(): Promise<boolean>;
  bindEvents(): void;
}
```

In `bindEvents()`, subscribe to embed SDK events and forward them to the CRM through `window.parent.postMessage`, using a versioned message format and an explicit target origin.

Configure the driver's location through Dataverse application settings:

| Priority | Configuration | Behavior |
|---|---|---|
| First | `msdyn_customCTIFromURL` | Loads the driver from the configured HTTPS URL. |
| Second | `msdyn_enableCustomCTIFromWebresource` set to `true` | Loads the `msdyn_CustomCTIDriver.js` web resource. |
| Default | Driver location unset | The workspace runs independently of a custom CTI driver. |

In [Power Apps](https://make.powerapps.com), select the environment that's specified in the embed URL, and then:

1. Leave `msdyn_customCTIFromURL` unset so the workspace uses the web resource setting.
1. Upload the compiled driver to the existing `msdyn_CustomCTIDriver.js` web resource, verify that its type is **Script (JScript)**, and save and publish your changes. Learn more in [Create or edit a web resource for a solution](/power-apps/maker/model-driven-apps/create-edit-web-resources#create-or-edit-a-web-resource-for-a-solution).
1. Set the environment value of `msdyn_enableCustomCTIFromWebresource` to **Yes**, and save the change. Learn more in [Configure a setting environment value](/power-apps/maker/data-platform/create-edit-configure-settings#setting-environment-value).
1. Include `useCustomCTI=1` in the iframe URL, reload the host application, and test the integration.

### Use the embed SDK

The workspace loads the embed SDK runtime and exposes it to CTI drivers as:

```javascript
const sdk = window.Microsoft.CCaaS.EmbedSDK;
```

Use the SDK modules for the operations your integration needs:

| Module | Operations |
|---|---|
| `sdk.conversation` | Retrieve assigned conversations, conversation data, transcripts, and Copilot summaries, and subscribe to conversation events. |
| `sdk.presence` | Retrieve presence options, get or change representative presence, and subscribe to presence changes. |
| `sdk.notification` | Display notifications and subscribe to conversation offers and other notifications. |
| `sdk.ctiDriver` | Fill the outbound dialer with `clickToDial({ number })` and coordinate the host panel's visibility, width, and height. Click-to-dial fills the number, and the representative places the call. |
| `sdk.dataverse` | Retrieve Dataverse records through `retrieveRecord(entitySetName, id, options)` and `retrieveMultipleRecords(entitySetName, options)`. |

SDK requests run as the signed-in representative and are subject to that user's Dataverse security roles. Request only the records and columns required by the integration.

To link a contact, account, or case record to a conversation, use `Microsoft.Omnichannel.linkToConversation(entityLogicalName, recordId, conversationId?)`. Supply `conversationId` to target a specific conversation, or omit it to use the conversation in focus.

Learn more about the developer integration surface in the [Dynamics 365 Contact Center SDK repository](https://github.com/microsoft/dynamics-365-contact-center).

### Secure the integration

Review these requirements with your integration developer:

- Allow only approved applications to frame Contact Center workspace.
- Set each `postMessage` target origin to the exact origin of the intended recipient. Don't use `"*"` as the target origin in production.
- Validate the origin, source window, schema, and version of every message before acting on it.
- Treat SDK payloads as untrusted input, and encode event data before inserting it into HTML.
- Validate and normalize phone numbers before passing them to click-to-dial.
- Limit logged personal data, including transcripts and phone numbers, to what your business process requires. Apply retention controls to any logs you keep.

### Review parameters from an earlier embedded experience

If you migrate an existing integration, review its query parameters:

| Parameter | Behavior |
|---|---|
| `dynamicsUrl` | Specifies the Dynamics 365 organization URL. |
| `useCustomCTI=1` | Enables loading the custom driver configured in Dataverse. |
| `ctiDriverUrl` | Configure the driver location through Dataverse application settings instead. The workspace reads the location only from those settings. |
| `override_features.EnableConversationNotes` or `EnableNotes` | Turns notes on or off. |
| Other `override_*` feature parameters | The workspace applies only the notes overrides listed in this table. |
| `msdynembedmode` and `msdynauthmode` | The workspace determines layout and sign-in mode independently of these parameters. |
| `tenantId` and `msdynagentexperience` | You can omit these parameters. Sign-in determines the tenant. |

### Verify the embedded experience

Test with a representative account that has the intended security roles:

1. Open the CRM and confirm that the workspace loads in the configured panel.
1. Complete Microsoft Entra sign-in through the pop-up window, and verify the representative's environment and inbox.
1. Set presence to **Available**, route a test conversation, and confirm that the representative can accept and handle it.
1. For voice, test microphone access, incoming audio, and an outbound call if the representative uses outbound calling.
1. Test the CRM actions implemented by your driver, such as opening a customer record or filling the outbound dialer.
1. Test host navigation and panel resizing to make sure that the workspace remains usable during a conversation.

## Related information

[Contact Center workspace overview (preview)](../use/contact-center-workspace-overview.md)  
[Manage users](/dynamics365/customer-service/administer/users-user-profiles)
