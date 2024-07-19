---
title: Provision channels in Dynamics 365 Contact Center
description: Perform the steps in this article to provision and add channels so that can you start using the product.
ms.date: 07/01/2024
ms.topic: how-to
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.custom: bap-template
ms.collection:
---

# Provision channels in Dynamics 365 Contact Center

Dynamics 365 Contact Center provides a modern, customizable, high-productivity experience that lets agents help customers across different channels via a unified interface. It lets organizations choose the channel that suits their business needs. It also ensures that a high level of responsive, quality service is received across channels.

To find out if Dynamics 365 Contact Center is available in your region, see [International availability](international-availability.md).

You can provision the following channels:

- [Chat](/dynamics365/customer-service/administer/set-up-chat-widget)
- [Voice](/dynamics365/customer-service/administer/voice-channel)
- [SMS](/dynamics365/customer-service/administer/configure-sms-channel)
- [Social](/dynamics365/customer-service/use/channels)
- [Microsoft Teams](/dynamics365/customer-service/administer/configure-microsoft-teams)

> [!IMPORTANT]
> The channels that you want to provision might require a license. More information: [Dynamics 365 Licensing Guide](https://go.microsoft.com/fwlink/p/?LinkId=866544).

## Prerequisites

- Obtain an active subscription of one or more of the following:

  - See the [system requirements for Dynamics 365 Contact Center](system-requirements-contact-center.md) for the required licenses to provision channels.
  
    > [!NOTE]
    > More information: [Pricing](https://www.microsoft.com/dynamics-365/products/contact-center/pricing), Dynamics 365 Licensing Guide, and [How to purchase through Volume Licensing](https://www.microsoft.com/en-us/licensing/how-to-buy/how-to-buy).

- Set up the prerequisites mentioned in the system requirements.

- Ensure that the provisioning user has the following permissions:
  - Microsoft 365 Global admin role. More information: [Assign admin roles to user in Microsoft Office 365](/microsoft-365/admin/add-users/assign-admin-roles)
  - Dynamics 365 System Administrator role on the root business unit for your organization. More information: [Assign security roles to a user in Power Platform](/power-platform/admin/assign-security-roles) and [Create or edit business units](/power-platform/admin/create-edit-business-units)
  - Read-Write access in the Client Access License Information (CAL). More information: [Create a Read-Write user account in Power Platform](/power-platform/admin/create-users#create-a-read-write-user-account)

## Set up channels

To set up the channels for configuring and using in Dynamics 365 Contact Center, perform the steps in [Set up Omnichannel for Customer Service](/dynamics365/customer-service/implement/omnichannel-provision-license#set-up-omnichannel-for-customer-service).

## Update Omnichannel for Customer Service application

After the channels are successfully provisioned, you can update the environment by enabling or disabling the required channels in Power Platform admin center. More information: [Update Omnichannel for Customer Service application](/dynamics365/customer-service/implement/omnichannel-provision-license#update-omnichannel-for-customer-service-application)

### Troubleshoot provisioning

[Instance is not available to select on the provisioning application](/troubleshoot/dynamics-365/customer-service/omnichannel-for-customer-service/instance-unavailable-provision-omnichannel)

### Related information

[Create workstreams](/dynamics365/customer-service/administer/create-workstreams)  
[Manage users](/dynamics365/customer-service/administer/users-user-profiles)  


