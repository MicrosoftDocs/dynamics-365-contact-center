---
title: Configure disposition codes
description: Learn how to configure disposition codes for voice and messaging channels.
ms.date: 03/31/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
---

# Configure disposition codes

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

Disposition codes allow you to categorize and record the outcome of the customers interaction with the customer service representative (service representatives or representatives), helping you to assess and improve customer interactions.

## Enable disposition codes 

1. In the Customer Service admin center or Contact Center admin center, select **Customer settings** in **Customer support**.
1. In the **Customer settings** page, select **Manage** for **Disposition code**.
1. On the **Disposition Code** page, select the **Turn on Disposition Code** checkbox.
1. In the **New Disposition Code** textbox, specify a name for the disposition code, and then select **Add**.
   The disposition code is added to the list of disposition codes. You can add more disposition codes by repeating the previous step.
1. Select a disposition code from the list, and then select **Delete** to remove the disposition code.
  > [!NOTE]
  > Even if you delete a disposition code that is associated with a conversation, the conversation still displays the disposition code. 
6. Select **Save**.

## Runtime experience

When you enable disposition codes, service representatives can't close a session without selecting a disposition code. The disposition code is recorded in the conversation transcript and can be used for reporting and analysis. Learn more in [Disposition codes](/customer-service/use/oc-customer-summary#set-disposition-codes).

## Related information

[View customer information on Active Conversation form](/customer-service/use/oc-customer-summary)   
[Manage sessions in the workspace app](/customer-service/use/oc-manage-sessions)