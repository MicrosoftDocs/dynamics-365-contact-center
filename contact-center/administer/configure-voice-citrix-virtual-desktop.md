---
title: Configure settings to improve call quality over Citrix virtual desktop
description: Learn how your representatives can experience better call quality when they use Citrix virtual desktop to access the voice capabilities in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection:
ms.date: 07/24/2025
ms.custom: bap-template
---

# Configure settings to improve call quality over Citrix virtual desktop

You can configure settings to improve the call experience for your representatives when they access the Copilot Service workspace app through Citrix virtual desktop.

## Prerequisites

- Citrix virtual desktop application 
- Create registry key as follows:
  - **Path**: HKLM\Software\WOW6432Node\Citrix\WebSocketService
  - **Key Name**: `ProcessWhitelist`
  - **Key Type**: MULTISZ 
  - **Key Value**: msedge.exe

## Enable the improved call quality experience

1. In the site map of Copilot Service admin center, go to **Support experience** > **Workspaces**.
1. Select **Manage** for **Voice call experiences**.
1. On the page that appears, turn on the **Enable improved call quality for representatives using Citrix virtual desktop** toggle.

## Access Citrix virtual desktop

Representatives can access the voice channel from the Citrix virtual desktop after it's installed by doing the following steps:

1. Open the Citrix workspace.

1. Connect to the virtual desktop.
1. Open a browser window and access Copilot Service workspace.

## Experience for representatives when local device disconnects from the virtual desktop 

Learn about the [experience for representatives when their local device disconnects](../administer/configure-voice-avd.md#rdc-disconnects) from the virtual desktop instance. 

### Related information

[Experience enhanced call quality when using voice through Citrix virtual desktop](../use/voice-channel-agent-experience.md#usecvd)  
[Transfer calls and consult with users in the voice channel](/dynamics365/customer-service/use/voice-channel-transfer-consult)  
