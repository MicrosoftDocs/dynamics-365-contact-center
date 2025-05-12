---
title: Install and manage Desktop companion application for voice channel (preview)
description: Learn how to install the Desktop companion application for the voice channel.
ms.date: 04/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Install and manage Desktop companion application for voice channel (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

The Desktop companion application serves as a backup system for the Dynamics 365 Customer Service or Dynamics 365 Contact Center web application. It ensures that customer service representatives (service representatives or representatives) can continue customer conversations without interruption during web application issues.

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Install the Desktop companion application

You can install the Desktop companion application on a customer service representative's desktop as follows:

1. [Download and run the Desktop Companion Application for Dynamics 365 Contact Center](https://aka.ms/dca-preview-installer). You must have administrator privileges to install the application on the desktop.
1. Double click the installer file to start the installation process. You can also install the application from the command line. Learn more in [msiexec](/windows-server/administration/windows-commands/msiexec).

> [!NOTE]
> [Microsoft Visual C++ Redistributable package](/cpp/windows/latest-supported-vc-redist) must be installed on the desktop. 

## Manage diagnostic data collection

The diagnostic data collected from Desktop companion application is used to keep the application secure and up-to-date; to detect, diagnose, and fix problems; and to make product improvements. This data doesn't include a user's name or email address, the content of the user's files, or information about apps unrelated to the product. 

Microsoft is dedicated to being transparent with customers about the data collected from client software and providing them with control over their data. Diagnostic data collected from applications as service representatives use their devices is classified as either *Required* or *Optional*. This classification makes it easier for you to make informed choices about their privacy.

The Desktop companion application software doesn't collect optional diagnostic data by default. Learn more about required data and optional data in [Diagnostic data collection](/power-automate/desktop-flows/diagnostic-data?WT.mc_id=powerautomate_inproduct_padconsole#required-data). 

## Related information

[Use the Desktop companion application with the voice channel (preview)](../use/voice-dca-application.md)
