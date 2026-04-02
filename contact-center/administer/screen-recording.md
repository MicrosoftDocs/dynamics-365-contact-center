---
title: Configure screen recording with desktop companion application
description: Learn how screen recording captures customer service representative activity during customer interactions and how authorized users can review recordings.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: how-to
ms.collection: 
ms.date: 04/01/2026
ms.custom: bap-template 
---

# Configure screen recording with desktop companion application

[!INCLUDE [cc-feature-availability](../includes/cc-feature-availability.md)]

Screen recording captures a customer service representative (service representative or representative) on-screen activity during customer interactions.

Screen recording helps organizations support quality, compliance, training, and operational insights by allowing authorized users to review how work is handled in real workflows.

> [!IMPORTANT]
> This feature is intended to help customer service managers or supervisors enhance their team's performance and improve customer satisfaction. It isn't intended to be used, and shouldn't be used, to make decisions that affect the employment of an employee or group of employees, including compensation, rewards, seniority, or other rights or entitlements. <br> 
> Customers are solely responsible for using Dynamics 365, this feature, and any associated feature or service in compliance with all applicable laws, including laws that are related to accessing individual employee analytics, and monitoring, recording, and storing communications with users. As part of this compliance, customers must adequately notify users that their communications with customer service representatives (service representatives or representatives) might be monitored, recorded, or stored. As required by applicable laws, customers must also obtain consent from users before they use this feature with them. In addition, customers are encouraged to have a mechanism in place to inform their service representatives that their communications with users might be monitored, recorded, or stored.

## Prerequisites


- Security roles
    - Representatives have the **Screen Recorder** role to record their screen.
    - You have the **Screen Recording Supervisor** role that allows you to view a list of recordings, but not download the recording file to a local machine.
    - You have the **Screen Recording Administrator** role, that allows you to view a list of screen recordings in the web app and download recording files for review.
- The representative's local computer has the desktop companion application installed and running. Learn more in [Install and manage desktop companion application for voice channel](/dynamics365/contact-center/administer/install-manage-desktop-app).

## How screen recording works

Screen recording captures a representative’s on-screen actions while the representative is handling customer interactions. The actions can include navigation across applications, data entry, and workflow steps performed during a support session. 

Recordings are typically associated with customer interactions such as conversations, chats, and cases, and they’re available to authorized roles for review and analysis.

When desktop companion application is used, screen recordings are saved locally before they’re uploaded securely to the organization’s Dataverse environment. After the file is uploaded successfully, the local recording file is deleted automatically. To make sure the file uploads securely to Dataverse, keep the desktop companion application running in the background.

## Enable screen recording for representatives

1. In Copilot Service admin center, go to **Workspaces**.
1. [Create a new experience profile](/dynamics365/customer-service/administer/create-agent-experience-profile) or add to an existing profile.
1. In **Productivity pane**, edit and turn on screen recording. The screen recording icon appears in the productivity pane.

## Types of screen recording

**Automated**

Automated screen recording starts when the representative accepts a voice call and stops when the voice call ends. If the  representative switches to a video call, a system notification is shown to the end customer indicating that the video in the call might be recorded for quality and training purposes.

**Manual**

Manual screen recording is continuous and representatives can't pause the recording. Recordings are capped at two hours. When the limit is reached, the current recording is saved and uploaded securely to Dataverse.

## Review screen recordings

Only authorized users can review recordings to understand how customer interactions were handled. Representatives can’t access or view their own screen recordings.

1. Sign in to Copilot Service workspace with either the **Screen Recording Supervisor** or **Screen Recording Administrator** role.
1. Go to **Screen Recordings**.
1. On the **Active Screen Recordings** page, search for recordings by using filters such as name, agent, session type, or created on. 
1. Review the list of recordings that match your search criteria. 
1. Select a recording to view the recording details download the file, if required.

## Manage your screen recordings

Learn how you can configure retention periods for screen recordings and transcripts.

### Set retention rules for screen recordings and transcripts

You can configure retention rules for screen recordings and transcripts by using **Bulk Record Deletion** jobs. Setting appropriate retention periods helps organizations comply with regulatory requirements and manage storage efficiently. You need to delete the records for the **msdyn_ScreenRecording** and **msdyn_ScreenRecordingLink** entities through the job.

By default, screen recordings and transcripts are retained indefinitely. Microsoft Copilot Studio transcripts are retained for 30 days.

### Set retention period for screen recordings

1. Sign in to your Dynamics 365 environment.
1. In your browser, go to the following URL:
`https://yourURL.crm.dynamics.com/tools/bulkdelete/home_bulkDeletionJobs.aspx` and replace your URL with your organization’s Dynamics 365 URL.
1. On the **Bulk Record Deletion** page, select **New** to start a new bulk delete job.
1. In **Bulk Deletion Wizard**, select **Next**.
1. In **Define search criteria**, in the **Look for** dropdown, select **Screen Recordings**.
1. Select the **Select** hyperlink and then select **Created On**.
1. Set the **Equals** to **Older Than X Days**. Enter the retention period in days (for example, 365 for one year) in the **Choose Date** text box. 
1. Select **Next**.
1. Enter a name for the job, such as **Bulk Delete Screen Recordings Older Than 1 Year**.
1. Schedule the job time for a low-activity period (for example, 3:00 AM).
1. Set the job recurrence (daily or every few days). Optionally, enable email notifications after job completion.
1. Select **Next**.
1. In **Review and Submit Bulk Deletion Details**, review your configuration.
1. Select **Submit** to create the bulk delete job.

[!WARNING]
Deleted screen recordings can’t be recovered. Verify your criteria carefully before submitting the job.

## Set retention for transcripts

To configure retention for transcripts, repeat the same steps used for screen recordings except for the following:

In the **Look for** list, select **Transcripts** instead of **Screen Recordings**.

Learn more about long-term data retention with Dataverse in [Dataverse long term data retention overview](/power-apps/maker/data-platform/data-retention-overview). 

### Related information

[Dataverse long term data retention FAQ](/power-apps/maker/data-platform/data-retention-faq)