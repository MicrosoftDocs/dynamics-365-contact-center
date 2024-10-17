---
title: System requirements for Dynamics 365 Contact Center
description: Learn about the prerequisites, system requirements, and accessible websites for deploying and using Dynamics 365 Contact Center.
ms.date: 07/01/2024
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: conceptual
ms.collection:
ms.custom: bap-template
---

# System requirements for Dynamics 365 Contact Center

This article provides information about the prerequisites and system requirements for deploying Dynamics 365 Contact Center in your organization.

## Prerequisites

This section lists the prerequisites for using Dynamics 365 Contact Center.

### International availability

Make sure that Dynamics 365 Contact Center is available in your region. Learn more in [International availability of Dynamics 365 Contact Center](international-availability.md).

### Licenses

Before you can use Dynamics 365 Contact Center with the customer relationship management (CRM) solution of your choice, each channel user must have one or more active subscriptions for the following standalone licenses.

| Capability | License |
|---|---|
| Voice, chat, and digital messaging | Dynamics 365 Contact Center |
| Chat and digital messaging | Dynamics 365 Contact Center Digital |
| Voice | Dynamics 365 Contact Center Voice |

Before you can use Dynamics 365 Contact Center with Dynamics 365 Customer Service Enterprise, each channel user must have one or more active subscriptions for the following add-on licenses.

| Capability | License |
|---|---|
| Voice, chat, and digital messaging | Dynamics 365 Contact Center Add-on for Customer Service Enterprise |
| Chat and digital messaging | Dynamics 365 Contact Center Digital Add-on for Customer Service Enterprise |
| Voice | Dynamics 365 Contact Center Voice Add-on for Customer Service Enterprise |

Learn how to purchase add-ins in [Buy an add-on](/microsoft-365/commerce/buy-or-edit-an-add-on?view=o365-worldwide#buy-an-add-on&preserve-view=true).

Learn more about licenses and pricing in the [Dynamics 365 licensing guide](https://go.microsoft.com/fwlink/p/?LinkId=866544).

## System requirements

The following table shows the system requirements for using Dynamics 365 Contact Center. These requirements might vary, depending on the size of your configuration and the applications that you run.

| Area | Requirements |
|---|---|
| Contact Center workspace app | Dynamics 365 Contact Center 9.2.21034.00160 or later. |
| Web browsers | <p>Supported browsers:</p><ul><li>Microsoft&nbsp;Edge ([Chromium based](https://support.microsoft.com/help/4501095/download-the-new-microsoft-edge-based-on-chromium)) version 79.0.309.65 or later is required for the desktop notifications feature.</li><li>Google Chrome.</li></ul><p><strong>Important:</strong> Dynamics 365 Contact Center uses third-party cookies for authentication. To ensure that services such as agent or supervisor presence can work correctly, make sure that the cookies aren't blocked in your browser in any mode.</p> |
| Azure Communication Services | Azure Communication Services is required for first-party voice and text (SMS) in the voice channel in production environments. Learn about requirements that are specific to Azure Communication Services in [Network recommendations](/azure/communication-services/concepts/voice-video-calling/network-requirements). |
| Hardware | <ul><li>A microphone and speakers are required for the voice experience.</li><li>**Minimum:** 4 gigabytes (GB) of RAM.</li><ul> |
| Internet bandwidth for voice and video | <ul><li>**Minimum:** 4 megabits per second (Mbps) upload speed, 8 Mbps download speed.</li><li>**Recommended:** 8 Mbps upload speed, 16 Mbps download speed.</li></ul> |
| Embedded experience | System requirements for the preferred CRM solution must be met. |

Learn about other hardware and software requirements in [Model-driven app requirements](/power-platform/admin/web-application-requirements).

### <a name="browsers-for-chat"></a>Supported web browsers for live chat widget

The customer-facing live chat widget that you show in your portal supports the three most recent major releases of the following browsers:

- **Windows:** Chromium-based browser such as Microsoft&nbsp;Edge, Google Chrome, or Mozilla Firefox
- **macOS and iOS:** Apple Safari
- **Android:** Chromium-based browser such as Microsoft&nbsp;Edge or Google Chrome

## Provision Dynamics 365 Contact Center

Learn how to enable the omnichannel capabilities in your organization in [Provision channels](provision-channels.md).

> [!NOTE]
> For an optimal experience in the Contact Center workspace app, we recommend that you use browsers in normal mode.

## Allow access to websites

If your organization uses a URL filter to block a category of websites or URLs, make sure that you allow the following websites as an exception for your users, so that they can access the Contact Center workspace app in the business portal:

- `https://ccaas-embed-prod.azureedge.net`
- `https://*.communication.azure.com`
- `https://login.microsoft.net`
- `https://login.microsoftonline.com`
- `https://login.windows.net`
- `https://browser.pipe.aria.microsoft.com`
- `https://*.teams.microsoft.com`
- `https://plat.teams.microsoft.com`
- `https://authsvc.teams.microsoft.com`
- `https://*.ng.msg.teams.microsoft.com`
- `https://*.notifications.teams.microsoft.com`
- `https://*.trouter.teams.microsoft.com`
- `https://ecs.office.com`
- `https://*.skype.com`
- `https://*.trouter.skype.com`
- `https://*.edge.skype.com`
- `https://aad.skypetoken.skype.com`
- `https://config.edge.skype.com`
- `https://edge.skype.com`
- `https://api.aps.skype.com`
- `https://*.asm.skype.com`
- `https://*.omnichannelengagementhub.com`
- `https://ocsdk-prod.azureedge.net`
- `https://*.service.signalr.net`

If your customers use a URL filter to block a category of websites or URLs, you might have to ask them to allow a specific website as an exception. To use the live chat widget in the portal, your customers must allow access to the following URLs from their browsers:

- `https://*.communication.azure.com`
- `https://*.teams.microsoft.com`
- `https://plat.teams.microsoft.com`
- `https://*.ng.msg.teams.microsoft.com`
- `https://*.notifications.teams.microsoft.com`
- `https://*.trouter.teams.microsoft.com`
- `https://ecs.office.com`
- `https://*.skype.com/*`
- `https://*.asm.skype.com`
- `https://browser.pipe.aria.microsoft.com`
- `https://oc-cdn-ocprod.azureedge.net/livechatwidget`
- `https://cdn.botframework.com/botframework-webchat`
- `https://*.omnichannelengagementhub.com`
- `https://ocsdk-prod.azureedge.net`

### Geo-specific links

The following table shows geographic location–specific links that should be made accessible.

| Geographic location | Links |
|---|---|
| North America | `oc-cdn-ocprod.azureedge.net/*` |
| Europe | `oc-cdn-public-eur.azureedge.net/*` |
| South America | `oc-cdn-public-sam.azureedge.net/*` |
| United Kingdom | `oc-cdn-public-gbr.azureedge.net/*` |
| Japan | `oc-cdn-public-jpn.azureedge.net/*` |
| Asia-Pacific | `oc-cdn-public-apj.azureedge.net*` |
| Canada | `oc-cdn-public.azureedge.net/*` |
| India | `oc-cdn-public-ind.azureedge.net/*` |
| Australia | `oc-cdn-public-oce.azureedge.net/*` |
| France | `oc-cdn-public-fra.azureedge.net/*` |
| Switzerland | `oc-cdn-public-che.azureedge.net/*` |
| United Arab Emirates | `oc-cdn-ocuae-uae.azureedge.net/*` |

## Related information

[Get started with Contact Center workspace](../use/ccw-overview.md)
