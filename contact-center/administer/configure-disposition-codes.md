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

## Prerequisites

- You have the Omnichannel Agent or Omnichannel Administrator security roles to configure and use disposition codes.
- If you have custom security roles, make sure that the roles have the following privileges to manage disposition codes. Learn more in [Security roles and privileges](/power-platform/admin/security-roles-privileges).
    - For service representatives to view and use disposition codes during conversations, the following privileges are assigned:
      - prvReadmsdyn_ocdispositioncode  
      - prvAppendTomsdyn_ocdispositioncode  
      - prvReadmsdyn_dispositioncodecategory  
      - prvReadmsdyn_conversationdispositioncodemap  
      - prvCreatemsdyn_conversationdispositioncodemap  
      - prvWritemsdyn_conversationdispositioncodemap  
      - prvDeletemsdyn_conversationdispositioncodemap  
      - prvAppendmsdyn_conversationdispositioncodemap  
      - prvAppendTomsdyn_conversationdispositioncodemap
    - For administrators to create and manage disposition codes, the following privileges are assigned:
      - prvReadmsdyn_ocdispositioncode
      - prvCreatemsdyn_ocdispositioncode
      - prvWritemsdyn_ocdispositioncode
      - prvDeletemsdyn_ocdispositioncode
      - prvAppendmsdyn_ocdispositioncode
      - prvAppendTomsdyn_ocdispositioncode
      - prvReadmsdyn_dispositioncodecategory
      - prvCreatemsdyn_dispositioncodecategory
      - prvWritemsdyn_dispositioncodecategory
      - prvDeletemsdyn_dispositioncodecategory
      - prvAppendmsdyn_dispositioncodecategory
      - prvAppendTomsdyn_dispositioncodecategory
      - prvReadmsdyn_conversationdispositioncodemap
      - prvCreatemsdyn_conversationdispositioncodemap
      - prvWritemsdyn_conversationdispositioncodemap
      - prvDeletemsdyn_conversationdispositioncodemap
      - prvAppendmsdyn_conversationdispositioncodemap
      - prvAppendTomsdyn_conversationdispositioncodemap

## Enable disposition codes 

1. In the Copilot Service admin center, select **Customer settings** in **Customer support**.
1. On the **Customer settings** page, select **Manage** for **Disposition code**.
1. On the **Disposition Code** page, select the **Turn on Disposition Code** checkbox. The **Require disposition code to close session** checkbox appears and is enabled by default. This indicates that the service representative must select a disposition code before closing a session.
1. In **Max disposition codes allowed**, specify the maximum number of disposition codes a representative can enter per conversation.
1. Select **New Disposition Code**. The **New Disposition Code** panel appears.
1. In the **New Disposition Code** panel, specify a name for the disposition code, and then select **Add**.
   The disposition code is added to the list of disposition codes. You can add more disposition codes by repeating the previous step.
  > [!NOTE]
  > Even if you delete a disposition code that is associated with a conversation, the conversation still displays the disposition code.  
1. Select **Save**.

## Add disposition code to workstream

You can add disposition codes to a chat or voice workstream so that service representatives can select workstream specific codes when they close a session.
1. On the **Workstream** page, select the required workstream.
1. Turn on the **Use global settings for requiring disposition code** toggle to use the global settings for disposition codes. If you don't turn on the toggle, the system uses the workstream specific settings for disposition codes.
1. Select the **Require disposition code to close session** checkbox. This indicates that the service representative must select a disposition code before closing a session.
1. Select **New Disposition Code** and then Perform the steps in **Enable disposition codes** section to add disposition codes to the workstream.

## Runtime experience

When you enable disposition codes, service representatives can't close a session without selecting a disposition code. The disposition code is recorded in the conversation transcript and can be used for reporting and analysis. Learn more in [Disposition codes](/dynamics365/customer-service/use/oc-customer-summary#set-disposition-codes).

## Related information

[View customer information on Active Conversation form](/dynamics365/customer-service/use/oc-customer-summary)   
[Manage sessions in the workspace app](/dynamics365/customer-service/use/oc-manage-sessions)