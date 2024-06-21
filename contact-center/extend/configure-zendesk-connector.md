---
title: Configure the connector for Zendesk
description: Learn how to use the connector for Zendesk CRM solution to fetch data into Dataverse and use in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection:
ms.date: 07/01/2024
ms.custom: bap-template
---

# Configure the connector for Zendesk

The Zendesk connector allows organizations to engage with their customers using omnichannel capabilities like voice, video, SMS, live chat, and social messaging while keeping their current investments in third-party CRM solutions. The omnichannel add-in works with third-party CRM solutions through data connectors. These connectors help bring the contacts and accounts data from the Zendesk CRM solution into Dataverse.

## Prerequisites 

- [Zendesk](https://[your_subdomain].zendesk.com) instance
- License for Dynamic 365 Contact Center
- Power Platform System administrator permissions
- Basic understanding of how to use Power Automate flows or Power Apps
- The following subscriptions that are a part of the license for Dynamics 365 Contact Center:
    - Power Automate
    - Power Apps 

## Import Power Automate flow 

1. Sign into [Power Apps](https://make.powerapps.com). Make sure that the environment for Power Apps and Power Automate is the same.
1. In the left pane, select **Tables**.