---
title: Install and manage desktop companion application for voice channel 
description: Learn how to install the desktop companion application for the voice channel in Dynamics 365 Contact Center.
ms.date: 02/13/2026
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Install and manage desktop companion application for voice channel

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

The Desktop companion application serves as a backup system for the web application for Dynamics 365 Contact Center. The application makes sure that customer service representatives (service representatives or representatives) can continue customer conversations without interruption during web application issues.

## Install the desktop companion application

You can install the desktop companion application on a representative desktop as follows:

1. [Download the Desktop Companion Application for Dynamics 365 Contact Center](https://aka.ms/dca-installer).
1. Double click the installer file to start the installation process. You can also install the application from the command line. Learn more in [msiexec](/windows-server/administration/windows-commands/msiexec).

    > [!NOTE]
    > [Microsoft Visual C++ Redistributable package](/cpp/windows/latest-supported-vc-redist) must be installed on the desktop.

1. Download and install the browser extensions by following these steps:
    - Chrome: [Desktop companion app for Dynamics 365 Contact Center Extension ](https://chromewebstore.google.com/detail/desktop-companion-app-for/kejpacmiikcnjccejioofncknckcpcpa?authuser=0&hl=en)
    - Edge: [Desktop companion app for Dynamics 365 Contact Center](https://microsoftedge.microsoft.com/addons/detail/desktop-companion-app-for/ifonlckhhfkfainkbngfbjhodbkeafbg)
1. Select the ellipses in the browser window and then select **Extensions**. If the extension is already available, select pin to add the extension to the top of the tool bar.
1. Select **Manage Extensions** and then turn on the toggle for **Desktop companion app for Dynamics 365 Contact Center Extension**.
1. Close the browser and restart it to apply the changes.

## Manage diagnostic data collection

The diagnostic data collected from the desktop companion application is used to keep the application secure and up-to-date; to detect, diagnose, and fix problems; and to make product improvements. This data doesn't include a user name or email address, the content of the user files, or information about apps unrelated to the product.

Microsoft is dedicated to being transparent with customers about the data collected from client software and providing them with control over their data. Diagnostic data collected from applications as service representatives use their devices is classified as either *Required* or *Optional*. This classification makes it easier for you to make informed choices about their privacy.

By default, the desktop companion application software doesn't collect optional diagnostic data. Learn more about required data and optional data in [Diagnostic data collection](/power-automate/desktop-flows/diagnostic-data?WT.mc_id=powerautomate_inproduct_padconsole#required-data).

## Restrict users from updating the desktop companion application

Configure a registry entry that restricts users from manually updating the desktop companion application.

| Hive | Key | Name | Type |
| ---- | --- | ---- | ---- |
| HKLM | Software\Microsoft\msdyn-companionapp | DisableUserUpdates | DWORD |

Value
1: To disable users from manually updating the Desktop Companion application.

The registry configuration prevents representatives from selecting update options and manually configuring the desktop companion application to start automatically.

## Related information

[Use the desktop companion application with the voice channel](../use/voice-dca-application.md)  
