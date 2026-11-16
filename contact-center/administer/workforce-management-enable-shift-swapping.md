---
title: Enable shift swapping
description: Learn how to enable shift swapping and add representatives to the Public WEM request team so customer service representatives can swap shifts with other representatives.
ms.date: 11/16/2026
ms.topic: how-to
author: lalexms
ms.author: laalexan
ms.reviewer: laalexan
search.audienceType:
- admin
- customizer
- enduser
ms.custom:
- dyn365-customerservice
---

# Enable shift swapping

Shift swapping allows supervisors to let customer service representatives (service representatives or representatives) swap shifts with other representatives. An administrator must enable shift swapping before representatives can create shift swap requests.

## Prerequisites

- Complete the steps in [Set up your workforce with roles and skills](workforce-management-user-management.md), including assigning the required security roles and creating a bookable resource for each representative.
- Add representatives to the Public WEM request team. Public shift swap requests are shared only with members of this team. Learn more in [Add representatives to the Public WEM request team](#add-representatives-to-the-public-wem-request-team).

## Add representatives to the Public WEM request team

1. In the site map of Copilot Service admin center, select **Workforce management** in **Operations**. The **Workforce management** page appears.
1. In **Time management**, select **Manage** next to **Shift swapping**.
1. On the **Swapping** page, select the **Power Platform admin center - teams** link. The **Public WEM request** team's members page opens.
1. Select **Add team members**.
1. Select the representatives that you want to add, and then select **Add**.

> [!IMPORTANT]
> Add representatives to the Public WEM request team before they use **Public Post**. Public shift swap requests are shared only with members of this team.

## Enable shift swapping for representatives

To enable shift swapping, complete the following steps:

1. In the site map of Copilot Service admin center, select **Workforce management** in **Operations**. The **Workforce management** page appears.
1. In **Time management**, select **Manage** next to **Shift swapping**.
1. On the **Swapping** page, set the **Enable shift swap** toggle to **On**.
1. In **Shift swap expiry (days)**, enter the number of days after which a shift swap request can no longer be accepted.
1. Select **Save and Close**.

### Related information

[Use shift swapping](../use/workforce-management-use-shift-swapping.md)  
[Set up your workforce with roles and skills](workforce-management-user-management.md)
