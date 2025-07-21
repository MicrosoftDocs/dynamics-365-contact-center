---
title: Configure Citrix virtual desktop for improved call quality
description: Learn about how your representatives can use Citrix virtual desktop for a better call quality experience and access the voice capabilities in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: 
ms.topic: how-to
ms.collection:
ms.date: 07/22/2025
ms.custom: bap-template
---

# Configure Citrix virtual desktop for improved call quality

You can improve the call experience for your representatives through Citrix virtual desktop. Representatives can connect through the Citrix virtual desktop and remotely access the Copilot Service workspace to make and receive calls and interact with your customers.

## Prerequisites

- Citrix virtual desktop application 
- Create registry key as follows:
  - **Path**: HKLM\Software\WOW6432Node\Citrix\WebSocketService
  - **Key Name**: `ProcessWhitelist`
  - **Key Type**: MULTISZ 
  - **Key Value**: msedge.exe chrome.exe

## Enable the improved call quality experience

1. In the site map of Copilot Service admin center, go to **Support experience** > **Workspaces**.
1. Select **Manage** for **Voice call experiences**.
1. On the page that appears, turn on the **Enable improved call quality for representatives using Citrix virtual desktop** toggle.

## Access Citrix virtual desktop

The representatives can access the voice channel from the Citrix virtual desktop after it's installed by using the following steps:

1. Open the Citrix workspace.

1. Connect to the virtual desktop.
1. Open a browser window and access Copilot Service workspace.

## Experience for representatives when local device disconnects from the virtual desktop 

Learn about the [experience for representatives when their local device disconnects](../administer/configure-voice-avd.md#rdc-disconnects) from the virtual desktop instance. 

### Related information

[Use agent dashboard and call controls in the voice channel](voice-channel-agent-experience.md)  
[Transfer calls and consult with users in the voice channel](/dynamics365/customer-service/use/voice-channel-transfer-consult)  
