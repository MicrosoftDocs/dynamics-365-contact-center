---
title: Provision channels in Dynamics 365 Contact Center
description: Perform the steps in this article to provision and add channels so that you can start using the product.
ms.date: 01/06/2025
ms.topic: how-to
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.custom: bap-template
ms.collection:
---

# Provision channels in Dynamics 365 Contact Center

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

Dynamics 365 Contact Center provides a modern, customizable, high-productivity experience that lets agents help customers across different channels via a unified interface. It lets organizations choose the channel that suits their business needs. It also ensures that a high level of responsive, quality service is received across channels.

To find out if Dynamics 365 Contact Center is available in your region, see [International availability](international-availability.md).

You can provision the following channels:

- [Chat](/dynamics365/customer-service/administer/set-up-chat-widget)
- [Voice](/dynamics365/customer-service/administer/voice-channel)
- [SMS](/dynamics365/customer-service/administer/configure-sms-channel)
- [Social](/dynamics365/customer-service/use/channels)
- [Microsoft Teams](/dynamics365/customer-service/administer/configure-microsoft-teams)

> [!IMPORTANT]
> The channels that you want to provision might require a license. Learn more at [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/p/?LinkId=866544).

## Prerequisites

- See [system requirements for Dynamics 365 Contact Center](system-requirements-contact-center.md) for the required licenses to provision channels.
  
    > [!NOTE]
    > Learn more at [Pricing](https://www.microsoft.com/dynamics-365/products/contact-center/pricing), Dynamics 365 Licensing Guide, and [How to purchase through Volume Licensing](https://www.microsoft.com/en-us/licensing/how-to-buy/how-to-buy).

- Set up the prerequisites mentioned in the system requirements.
- Dynamics 365 System Administrator role on the root business unit for your organization. Learn more at [assign security roles to a user in Power Platform](/power-platform/admin/assign-security-roles) and [Create or edit business units](/power-platform/admin/create-edit-business-units)

## Set up channels

You can set up channels in the Contact Center admin center or Customer Service admin center application. In Power Platform admin center, while you can view existing environments and channels, you can't enable, edit, or delete channels.

> [!NOTE]
> Starting October 2024, the legacy provisioning of channels in Power Platform admin center is deprecated and can't be edited on the **Dynamics 365 apps** page. Learn more in [Deprecations](/dynamics365/customer-service/implement/deprecations-customer-service)

To set up the channels, perform the following steps:

1. Select **Channels** in **Customer Support**. 
1. Select **Manage** for **Manage channels**. The Manage channels page appears. 
1. Select the channels that you want to use. 
    Depending on your licenses, you can view the channels that you can enable. If you don't have the required licenses, the checkboxes for the corresponding channels are disabled. Learn more about licenses [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/p/?LinkId=866544).
1. Select **Save**.

The setup can take several minutes. The application provisions the channel in the background. You can close the window and check after some time or refresh it to see if it's complete. When the setup is complete, the enabled channels appear in your environment.

If the provisioning fails, an error message appears that you can select to view the details.

### Turn off channels

You can turn off a channel if you no longer require it. However, to enable the channel again, you'd need to reconfigure the channel instance.

1. Select  **Customer Support** > **Channels** > **Manage channels**. 
1. Clear the checkbox for the channel that you want to turn off. The application displays a confirmation message. Select **Turn off**.

### Related information

[Create workstreams](/dynamics365/customer-service/administer/create-workstreams)   
[Manage users](/dynamics365/customer-service/administer/users-user-profiles)   


