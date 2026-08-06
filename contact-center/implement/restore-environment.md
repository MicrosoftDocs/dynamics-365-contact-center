---
title: Manage Dynamics 365 Contact Center environments
description: Learn how to manage Dynamics 365 Contact Center environments by resetting, restoring, recovering, or migrating them to maintain omnichannel capabilities.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection: 
ms.date: 08/03/2026
ms.custom: bap-template

---

# Manage Dynamics 365 Contact Center environments

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

This article explains how to manage Dynamics 365 Contact Center environments by resetting, restoring, recovering, or migrating them. Use these operations to return an environment to a previous state or move it between tenants or geographies.

After you reset or restore an environment, or complete a tenant-to-tenant migration, you must [provision the channels](provision-channels.md) or [enable unified routing](/dynamics365/customer-service/administer/provision-unified-routing) again to use omnichannel capabilities.

## Reset organization

This operation restores the environment to its original state. It can be used to create a new project, free up storage space, and remove an environment containing personal data. In Power Platform admin center, follow the steps in [Reset environment](/power-platform/admin/reset-environment) to reset the environment.

## Restore organization

This process involves returning the environment to a previous state using a backup or restore point to recover data and ensure continuous availability of service. To restore the environment, perform the steps in [Restore environment](/power-platform/admin/backup-restore-environments) in Power Platform admin center.

## Recover organization

You can retrieve a recently deleted omnichannel environment and restore it to its previous state. In Power Platform admin center, perform the steps in [Recover environment](/power-platform/admin/recover-environment) to recover the default settings.

## Migrate from one tenant to another tenant

Use [tenant-to-tenant migration](/power-platform/admin/move-environment-tenant) to transfer an environment from one tenant to another.

## Move contact center from one geo to another

Follow the steps in [Geo-to-geo migrations](/power-platform/admin/geo-to-geo-migrations) to move the contact center from one geo to another. After the move, the contact center is recreated.

### Post-move updates

To update the contact center, complete the following steps. Follow the steps that correspond to the channels you configured in your contact center.

1. **Administration mode**: Remove the organization from [administration mode](/power-platform/admin/admin-mode).
1. **Organization URL**: To sign in to the org that you moved, get the new URL in [Power Platform admin center](https://admin.powerplatform.microsoft.com).
1. **Chat widget**: Copy the updated chat widget code and [re-embed in your customer-facing portal](/dynamics365/customer-service/administer/embed-chat-widget-portal).
1. **Voice**: The Azure Communication Services webhook endpoints change for the new geo. The new values are displayed in Copilot Service admin center.
    1. In the site map, go to **Channels** > **Phone numbers** > **Advanced** > **Manage Azure Communication Services**.
    1. Copy the values from the following fields:
       - **Recording Web Hook Endpoint**
       - **SMS Web Hook Endpoint**
       - **Incoming call Web Hook Endpoint**
    1. Go to the [Azure portal](https://portal.azure.com/) and paste the values in the corresponding event grid subscriptions.

    Learn more in [Connect using an existing Azure resource](/dynamics365/customer-service/administer/voice-channel-connect-existing-resource) and [Set up incoming calls, call recording, and SMS services](/dynamics365/customer-service/administer/voice-channel-configure-services).

1. **Record routing**: No extra steps. Record routing works after you remove the organization from administration mode.

### Related information

[Copy environment with omnichannel capabilities](/dynamics365/customer-service/implement/copy-environment-with-omnichannel)  
