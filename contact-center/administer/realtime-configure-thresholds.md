---
title: Configure thresholds
description: Configure thresholds for real-time metrics in Dynamics 365 Contact Center to flag at-risk and critical KPIs. Learn how to set organization and queue-level values.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.date: 10/30/2026
ms.topic: concept-article
ms.custom: bap-template
---

# Configure thresholds

Configure thresholds for real-time metrics to identify metric values that require attention. You can define organization-level defaults and override them for specific queues.

## Prerequisites

To use thresholds, configure privileges for the **Real Time Streaming Analytics Threshold** (`msdyn_ccrtathreshold`) table.

- Use an account with the **System Administrator** role.

- If you use the default Omnichannel administrator and Omnichannel supervisor roles, [create copies of the roles](/power-platform/admin/create-edit-security-role). If you already use custom or copied roles, configure those roles directly.

- Configure the following [table privileges](/power-platform/admin/security-roles-privileges):

    - For the administrator role, set **Create**, **Read**, **Write**, **Delete**, **Append**, and **Append To** to **Organization** access.
    - For the supervisor role, set **Read** to **Organization** access. Set the remaining privileges to **None**.

- [Map the roles to the Admin and Supervisor personas](/dynamics365/customer-service/administer/role-persona-mapping), and [assign the appropriate roles directly to users](/dynamics365/customer-service/implement/add-users-assign-roles). Retain existing persona mappings and other required security roles.

**Configure organization-level thresholds**

Organization-level thresholds apply to all queues that don't have queue-specific overrides.

1. In the Contact Center workspace app, in **Real-time analytics**, select **Configure**.
1. On the **Thresholds** tab, select the key performance indicator (KPI).
1. Under **Organization defaults** > **Threshold configuration**, specify whether **Lower is better** or **Higher is better**.
1. Enter the **At risk** and **Critical** threshold values.
1. Save your changes.

**Configure queue-level thresholds**

Override the organization-level thresholds when a queue requires different values.

1. In the Contact Center workspace app, in **Real-time analytics**, select **Configure**.
1. On the **Thresholds** tab, select the KPI.
1. In the **Queue thresholds** tab, select **Manage queue thresholds** and add or modify the queues that you want to configure.
1. Enter the **At risk** and **Critical** threshold values.
1. Save your changes.

Queues with an override use their queue-specific thresholds. Other queues continue to use the organization-level thresholds.

**Reset thresholds**

You can also reset modified thresholds to restore the default values.

## Related information

[Overview of real-time streaming analytics](../use/realtime-streaming.md)  
[Wallboard](../use/realtime-streaming-wallboard.md)  
[Assisted service](../use/realtime-streaming-assisted-service.md)  
[Queues](../use/realtime-streaming-queues.md)  
[Representatives](../use/realtime-streaming-representatives.md)  
[Conversations (preview)](../use/realtime-streaming-conversations.md)  
[Self-service](../use/realtime-streaming-self-service.md)