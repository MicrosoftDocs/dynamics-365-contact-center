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

Make sure that Dynamics 365 Contact Center is available in your region. More information: [International availability](international-availability.md)

### Licenses

To use Dynamics 365 Contact Center with a customer relationship management (CRM) solution of your choice, one or more active subscriptions of the following standalone licenses are required for each channel user.

| Capability | License |
| --- | --- |
| Voice, chat, and digital messaging | Dynamics 365 Contact Center |
| Chat, digital messaging | Dynamics 365 Contact Center Digital |
| Voice | Dynamics 365 Contact Center Voice |

To use Dynamics 365 Contact Center with Dynamics 365 Customer Service Enterprise, one or more active subscriptions of the following add-on licenses are required for each channel user.

| Capability | License |
| --- | --- |
| Voice, chat, and digital messaging | Dynamics 365 Contact Center Add-on for Customer Service Enterprise|
| Chat and digital messaging | Dynamics 365 Contact Center Digital Add-on for Customer Service Enterprise|
| Voice |Dynamics 365 Contact Center Voice Add-on for Customer Service Enterprise |

For information on purchasing add-ins, see [Buy an add-on](/microsoft-365/commerce/buy-or-edit-an-add-on?view=o365-worldwide#buy-an-add-on&preserve-view=true).

For more information about licenses and pricing, see the [Dynamics 365 licensing guide](https://go.microsoft.com/fwlink/p/?LinkId=866544).

## System requirements

The system requirements to use Dynamics 365 Contact Center are as follows. These requirements might vary depending on your configuration size and the applications that you run.

| Area | Requirements |
|----------|----------|
| Contact Center workspace app | Dynamics 365 Contact Center 9.2.21034.00160 or later.  |
| Web browsers | Supported browsers:<li> Microsoft Edge ([Chromium based](https://support.microsoft.com/help/4501095/download-the-new-microsoft-edge-based-on-chromium)); version 79.0.309.65 or later is required for the desktop notifications feature. </li> <li> Google Chrome </li> **Important**<br> Dynamics 365 Contact Center uses third-party cookies for authentication. Make sure that the cookies are not blocked in your browser in any mode so that certain services, such as agent or supervisor presence, can work properly. |
| Azure Communication Services |Required for first-party voice and SMS in the voice channel in production environments. For requirements specific to Azure Communication Services, see [Network recommendations](/azure/communication-services/concepts/voice-video-calling/network-requirements). |
| Hardware | <ul><li>Microphone and speakers for the voice experience.</li><li>**Minimum:** 4 GB of RAM</li><ul> |
| Internet bandwidth for voice and video |<ul><li>**Minimum:** 4-Mbps upload speed; 8-Mbps download speed</li><li>**Recommended:** 8-Mbps upload speed; 16-Mbps download speed</li></ul> |
|Embedded experience| System requirements for the preferred CRM solution |

For other hardware and software requirements, see [Model-driven app requirements](/power-platform/admin/web-application-requirements).

### Supported web browsers for live chat widget<a name="browsers-for-chat"></a>

The customer-facing live chat widget that you display on your portal supports the latest three major releases of the following browsers:

- **Windows:** Chromium-based browser such as Microsoft Edge, Google Chrome, and Mozilla Firefox
- **macOS and iOS:** Safari
- **Android:** Chromium-based browser such as Microsoft Edge and Google Chrome

## Provision Dynamics 365 Contact Center

To enable the omnichannel capabilities in your org, see [Provision channels](provision-channels.md).

> [!NOTE]
> We recommend that you use browsers in normal mode to optimally experience the Contact Center workspace app.

## Allow access to websites

If your organization uses a URL filter to block a category of websites or URLs, ensure that you allow the following websites as an exception for your users so they can access the Contact Center workspace app on the business portal.

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

If your customers are using a URL filter to block a category of websites or URLs, you might have to ask your customers to allow a specific website as an exception. Your customers must allow access to the following URLs from their browsers to use the live chat widget in the portal.

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

Location-specific links that should be made accessible are as follows.

| Geographic location | Links |
|-------------------------------|----------------------------------|
| North America | `oc-cdn-ocprod.azureedge.net/*`|
| Europe | `oc-cdn-public-eur.azureedge.net/*`|
| South America | `oc-cdn-public-sam.azureedge.net/*`|
| United Kingdom | `oc-cdn-public-gbr.azureedge.net/*`|
| Japan | `oc-cdn-public-jpn.azureedge.net/*`|
| Asia-Pacific | `oc-cdn-public-apj.azureedge.net*`|
| Canada | `oc-cdn-public.azureedge.net/*`|
| India | `oc-cdn-public-ind.azureedge.net/*`|
| Australia | `oc-cdn-public-oce.azureedge.net/*`|
| France | `oc-cdn-public-fra.azureedge.net/*`|
| Switzerland | `oc-cdn-public-che.azureedge.net/*` |
| United Arab Emirates | `oc-cdn-ocuae-uae.azureedge.net/*`|

### See also

[Get started with Contact Center workspace](../use/ccw-overview.md)  



