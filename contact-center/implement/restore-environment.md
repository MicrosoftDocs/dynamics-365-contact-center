---
title: Manage omnichannel environments
description: Follow these steps to reset, restore, or recover a Dynamics 365 Contact Center environment that includes omnichannel capabilities.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection: 
ms.date: 12/29/2025
ms.custom: bap-template

---

# Manage omnichannel environments

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

In your omnichannel environments, you can manage various events and operations that are essential to maintain and oversee your organization's environments within specific platforms or systems.

You can reset, restore, or recover your omnichannel environments. After you reset the environment, you must [provision the channels](provision-channels.md) or [enable unified routing](/dynamics365/customer-service/administer/provision-unified-routing) again to use omnichannel capabilities.

## Reset organization

This operation restores the environment to its original state. It can be used to create a new project, free up storage space, and remove an environment containing personal data. In Power Platform admin center, follow the steps in [Reset environment](/power-platform/admin/reset-environment) to reset the environment.

## Restore organization

This process involves returning the environment to a previous state using a backup or restore point to recover data and ensure continuous availability of service. To restore the environment, perform the steps in [Restore environment](/power-platform/admin/backup-restore-environments) in Power Platform admin center.

## Recover organization

You can retrieve a recently deleted omnichannel environment and restore it to its previous state. In Power Platform admin center, perform the steps in [Recover environment](/power-platform/admin/recover-environment) to recover the default settings.

### Related information

[Copy environment with omnichannel capabilities](/dynamics365/customer-service/implement/copy-environment-with-omnichannel)  