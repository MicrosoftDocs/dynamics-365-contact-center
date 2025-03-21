---
title: Manage Desktop companion application for voice channel (preview)
description: Learn how to install Desktop companion application for the voice channel.
ms.date: 10/30/2024
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Manage Desktop companion application for voice channel (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

The Desktop companion application is a backup system when the Dynamics 365 Customer Service or Dynamics 365 Contact Center web application faces issues, that allows customer service representatives (service representatives or representatives) to continue customer conversations without interruption. 

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Install the Desktop companion application

You can install the Desktop companion application on a customer service representative's desktop as follows:

1. Download and run the Desktop Companion Application for Dynamics 365 Contact Center from [here](https://aka.ms/dca-preview-installer). You must have administrator privileges to install the application on the desktop.
1. Double click the installer file to start the installation process. You can also install the application from the command line. Learn more in [msiexec](/windows-server/administration/windows-commands/msiexec).

> [!NOTE]
> [Microsoft Visual C++ Redistributable package](/cpp/windows/latest-supported-vc-redist?view=msvc-170) must be installed on the desktop. 

## Diagnostic data collection

The diagnostic data collected from Desktop companion application is used to keep the application secure and up-to-date; to detect, diagnose, and fix problems; and to make product improvements. This data doesn't include a user's name or email address, the content of the user's files, or information about apps unrelated to the product. 

Microsoft is dedicated to being transparent with our customers about the data we collect from our client software and giving them more control over their data. As part of this work, diagnostic data collected from our the applications as customer service representatives use their devices is classified as either *Required* or *Optional*. This classification will make it easier for you to make informed choices about their privacy.

The Desktop companion application software doesn't collect optional diagnostic data by default unless the user specified otherwise during the initial installation process or later in the product's settings. Learn more about required data and optional data in [Diagnostic data collection](/power-automate/desktop-flows/diagnostic-data?WT.mc_id=powerautomate_inproduct_padconsole#required-data). 