---
title: Configure screen recording with desktop companion application
description: Learn how screen recording captures customer service representative activity during customer interactions and how authorized users can review recordings.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: 
ms.date: 03/18/2026
ms.custom: bap-template 
---

# Configure screen recording with desktop companion application

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
- The representative's local machine has the desktop companion application installed and running. Learn more in [Install and manage desktop companion application for voice channel](/dynamics365/contact-center/administer/install-manage-desktop-app).

## How screen recording works

Screen recording captures a representative’s on-screen actions while the representative is handling customer interactions. The actions can include navigation across applications, data entry, and workflow steps performed during a support session. 

Recordings are typically associated with customer interactions such as conversations, chats, and cases, and they’re available to authorized roles for review and analysis.

When desktop companion application is used, screen recordings are saved locally before they’re uploaded securely to the organization’s Dataverse environment. After the file is uploaded successfully, the local recording file is deleted automatically. To make sure the file uploads securely to Dataverse, keep the desktop companion application running in the background.

## Enable screen recording for representatives

1. In Copilot Service admin center, go to **Workspaces**.
1. [Create a new experience profile](/dynamics365/customer-service/administer/create-agent-experience-profile). 
1. Select the screen recording option. The screen recording button appears in the productivity pane.


## Types of screen recording

### Automated

Automated screen recording starts when the representative accepts a voice call and stops when the voice call ends. If the  representative switches to a video call, a system notification is shown to the end customer indicating that the video in the call might be recorded for quality and training purposes.

### Manual

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

[Dataverse long term data retention FAQ](/power-apps/maker/data-platform/data-retention-faq)