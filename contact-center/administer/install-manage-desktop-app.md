---
title: Install and manage desktop companion application for voice channel 
description: Learn how to install the desktop companion application for the voice channel in Dynamics 365 Contact Center.
ms.date: 03/24/2026
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Install and manage desktop companion application for voice channel

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

The desktop companion application serves as a backup system for the web application for Dynamics 365 Contact Center. The application makes sure that customer service representatives (service representatives or representatives) can continue customer conversations without interruption during web application issues.

## Install the desktop companion application

You can install the desktop companion application on a representative desktop as follows:

1. [Download the Desktop Companion Application for Dynamics 365 Contact Center](https://aka.ms/dca-installer).
1. Double-click the installer file to start the installation process. You can also install the application from the command line. Learn more in [msiexec](/windows-server/administration/windows-commands/msiexec).

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
1: To disable users from manually updating the desktop Companion application.

The registry configuration prevents representatives from selecting update options and manually configuring the desktop companion application to start automatically.

## Configure screen recording with desktop companion application

[!INCLUDE [cc-feature-availability](../includes/cc-feature-availability.md)]

Screen recording captures a customer service representative (service representative or representative) on-screen activity during customer interactions.

It helps organizations support quality, compliance, training, and operational insights by allowing authorized users to review how work is handled in real workflows.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. <br> 
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Prerequisites

Before you can use screen recording, make sure the following requirements are met:

- Security roles
    - Representatives have the **Screen Recorder** role to use the screen recording.
    - You have the **Screen Recording Supervisor** role that allows you to view a list of recordings, but not download the recording file to a local machine.
    - You have the **Screen Recording Administrator** role, that allows you to view a list of screen recordings in the web app and download recording files for review.
- The representative's local machine has the desktop companion application [installed and running](#install-the-desktop-companion-application).

## How screen recording works

Screen recording captures a representative’s on-screen actions while the representative is handling customer interactions. The actions can include navigation across applications, data entry, and workflow steps performed during a support session. 

Recordings are typically associated with customer interactions such as conversations, chats, and cases, and they’re available to authorized roles for review and analysis.

When desktop companion application is used, screen recordings are saved locally before they’re uploaded securely to the organization’s Dataverse environment. After the file is uploaded successfully, the local recording file is deleted automatically. To make sure the file uploads securely to Dataverse, keep the desktop companion application running in the background.

## Enable screen recording for representatives

1. In Copilot Service admin center, go to **Workspaces**.
1. [Create a new experience profile](/dynamics365/customer-service/administer/create-agent-experience-profile). 
1. Select the screen recording option. The screen recording button appears in the productivity pane.


## Types of screen recording

**Automated**

Automated screen recording starts when the representative accepts a voice call and stops when the voice call ends. If the  representative switches to a video call, a system notification is shown to the end customer indicating that the video in the call might be recorded for quality and training purposes.

**Manual**

Manual screen recording is continuous and representatives can't pause the recording. Recordings are capped at two hours. When the limit is reached, the current recording is saved and uploaded securely to Dataverse.

## Review screen recordings

Only authorized users can review recordings to understand how customer interactions were handled. Representatives can’t access or view their own screen recordings.

1. Sign in to Copilot Service admin center with either the **Screen Recording Supervisor** or **Screen Recording Administrator** role.
1. Go to **Screen recordings**.
1. Search for recordings by using filters such as agent, date, or recording type. 
1. Review the list of recordings that match your search criteria. 
1. You can also select and download a recording, as required.

## Manage your screen recordings

Learn how you can configure retention periods for call recordings and Omnichannel transcripts in Dynamics 365 Contact Center. 

Learn more about long-term data retention with Dataverse in [Dataverse long term data retention overview](/power-apps/maker/data-platform/data-retention-overview).


## Related information

[Use the desktop companion application with the voice channel](../use/voice-dca-application.md)  
