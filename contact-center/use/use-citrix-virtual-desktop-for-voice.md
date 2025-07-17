---
title: Use Citrix virtual desktop to access voice capabilities
description: Learn about how your representatives can use Citrix virtual desktop to access voice capabilities in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: 
ms.topic: how-to
ms.collection:
ms.date: 07/22/2025
ms.custom: bap-template
---

# Use Citrix virtual desktop to access voice capabilities

You can configure the voice channel to be available to your customer service representatives through the Citrix virtual desktop. Representatives can connect through the Citrix virtual desktop and remotely access the Copilot Service workspace to make and receive calls and interact with your customers.

## Prerequisites

- The feature is enabled by your administrator in Copilot Service admin center > **Support experience** > **Workspaces** > **Voice call experiences** > **Enable improved call quality for representatives using Citrix virtual desktop**.

- Citrix virtual desktop application 
- Create registry key as follows:
  - **Path**: HKLM\Software\WOW6432Node\Citrix\WebSocketService
  - **Key Name**: `ProcessWhitelist`
  - **Key Type**: MULTISZ 
  - **Key Value**: msedge.exe chrome.exe

## Access Citrix virtual desktop

The representatives can access the voice channel from the Citrix virtual desktop after it's installed by using the following steps:

1. Open the Citrix workspace.

1. Connect to the virtual desktop.
1. Open a browser window and access Copilot Service workspace.

### Related information

[Use agent dashboard and call controls in the voice channel](voice-channel-agent-experience.md)  
[Transfer calls and consult with users in the voice channel](/dynamics365/customer-service/use/voice-channel-transfer-consult)  
