---
title: Customize Copilot conversation summaries
description: Learn how to choose and customize the format that Copilot uses for conversation summaries.
author: gandhamm 
ms.author: mgandham 
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 08/27/2026
ms.update-cycle: 180-days
ms.custom: bap-template 
---

# Customize Copilot conversation summaries

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

Customize the format and information that Copilot uses for conversation summaries to help customer service representatives (service representatives or representatives) review consistent, relevant summaries.

## Choose and customize the conversation summary format

In Copilot Service admin center:

1. Use one of the following navigation options: 
    - **Support Experience** > **Productivity** > **Summaries**
    - **Operations** > **Insights** > **Summaries**
1. In **Summaries**, under **Live conversation summaries**, select **Manage format**.
1. In the **Manage format** pane, select one of the following options:
   - **Paragraph**: Generates the summary in a single paragraph.
   - **Structured**: Generates the summary based on the information you selected.
1. If you select **Structured**, configure the information to include:
   - Select **Add new info** to create a custom summary section. Specify a **Title** for the section heading and provide instructions that tell Copilot which information to extract and summarize.
   - Select **Reset to default info** to remove all custom sections and restore these default options:
     - **Root cause**
     - **Customer issue**
     - **Troubleshooting steps**
     - **Outcome**
     - **Error code**
     > [!NOTE]
     > The error codes you specify are samples for Copilot to find in the conversation. Copilot finds similar error codes in the conversation and includes them in the summary.
   - Move the information to arrange the order in which it appears in the summary.
1. Turn on **Remove information from the summary that can't be found**. Information that isn't in the conversation doesn't appear in the summary. For example, if the customer doesn't provide an error code, the summary doesn't include one.
1. Select **Save**.

     :::image type="content" source="../media/conv-manage-format-mini.png" alt-text="Screenshot of the structured settings for conversation summary" lightbox="../media/conv-manage-format.png":::|

 If you select all available options, the service representative sees the following Copilot conversation summary.

   :::image type="content" source="../media/conv-summary-format-mini.png" alt-text="Screenshot of the structured data format for conversation summary" lightbox="../media/conv-summary-format.png":::|

## Next steps

[Use Copilot to summarize cases and conversations](../use/copilot-use-summary.md)
