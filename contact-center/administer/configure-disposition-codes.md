---
title: Configure disposition codes
description: Learn how to configure disposition codes for voice and messaging channels.
ms.date: 02/09/2026
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
---

# Configure disposition codes

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

Disposition codes allow you to categorize and record the outcome of the customer interaction with the customer service representative (service representative or representative), and help you assess and improve customer interactions.

## Prerequisites

- You have the Omnichannel Administrator security role to configure and use disposition codes. The Omnichannel Agent is required to use disposition codes during conversations.
- If you have custom security roles, make sure that the roles have the following privileges to manage disposition codes. Learn more in [Security roles and privileges](/power-platform/admin/security-roles-privileges).

  ### [Administrators](#tab/administrators)

   For administrators to create and manage disposition codes, the following privileges are assigned:

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

  ### [Customer service representatives](#tab/customerservicerepresentatives)

   For service representatives to view and use disposition codes during conversations, the following privileges are assigned:

    - prvReadmsdyn_ocdispositioncode  
    - prvAppendTomsdyn_ocdispositioncode  
    - prvReadmsdyn_dispositioncodecategory  
    - prvReadmsdyn_conversationdispositioncodemap  
    - prvCreatemsdyn_conversationdispositioncodemap  
    - prvWritemsdyn_conversationdispositioncodemap  
    - prvDeletemsdyn_conversationdispositioncodemap  
    - prvAppendmsdyn_conversationdispositioncodemap  
    - prvAppendTomsdyn_conversationdispositioncodemap

---

## Enable disposition codes

1. In the Copilot Service admin center, select **Customer settings** in **Customer support**.
1. On the **Customer settings** page, select **Manage** for **Disposition code**.
1. On the **Disposition Code** page, enable the **Turn on Disposition Code** toggle. The **Require disposition code to close session** checkbox appears. 
1. If you select **Require disposition code to close session**, service representative must select a disposition code before closing a session. This checkbox isn't selected by default. 
1. In **Max disposition codes allowed**, specify the maximum number of disposition codes a representative can enter per conversation. You can specify up to 12 disposition codes. The default value is two. In transfer scenarios, the maximum number of disposition codes allowed is applicable per primary representative involved in the conversation journey.

## Manage disposition codes

You can add, edit, or delete disposition codes that are available globally. Do the following steps in the **Disposition Code** page.

1. Select **New Disposition Code**. The **New Disposition Code** panel appears.
1. Specify a name for the disposition code, category, workstream, and then select **Add**. The disposition code is added to the list of disposition codes. You can add more disposition codes by repeating the previous step.
1. To edit a disposition code, do the following:
      - Select the disposition code and then select **Edit**. On the **Edit Disposition Code** panel, make the changes.
      - You can also select multiple disposition codes to edit the category and workstream.
1. To delete a disposition code, select the disposition code, and then select **Delete**. You can also select multiple disposition codes to delete.
  > [!NOTE]
  > After you use a disposition code for a conversation, it's displayed for the conversation even if you delete the disposition code.

  :::image type="content" source="../media/add-disposition-codes.png" alt-text="Screenshot of disposition codes" :::

## Add disposition code to workstreams

You can add disposition codes to a chat or voice workstream so that service representatives can select workstream-specific codes when they close a session.
1. On the **Workstream** page, select the required workstream, and expand **Advanced settings**. You can turn on one of the following settings for disposition codes at the workstream level.

    -  **Use global settings for requiring disposition code**: When enabled, the system uses the disposition codes defined at the global level. If you turn off the toggle, the system uses the disposition codes defined at the workstream level.
    - **Require disposition code to close session**: If enabled, service representatives must select a disposition code before closing a session. This checkbox is enabled only when the **Use global settings for requiring disposition code** toggle is turned off.

1. To add new disposition codes, select **New Disposition Code**, and then perform the steps in the **Enable disposition codes** section of this article to add disposition codes to the workstream.
 
  > [!NOTE]
  > You can manage workstream-specific disposition codes within the workstream settings only.

:::image type="content" source="../media/work-stream-disposition-code.png" alt-text="Screenshot of workstream specific disposition codes" :::

## Runtime experience

When you enable **Require disposition code to close session**, service representatives can't close a session without selecting a disposition code. The disposition code is recorded in the conversation transcript and can be used for reporting and analysis. Learn more in [Disposition codes](/dynamics365/customer-service/use/oc-customer-summary#set-disposition-codes).

## Related information

[View customer information on Active Conversation form](/dynamics365/customer-service/use/oc-customer-summary)   
[Manage sessions in the workspace app](/dynamics365/customer-service/use/oc-manage-sessions)
