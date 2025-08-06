---
title: Use Copilot to summarize conversations
description: Learn how customer service representatives can use Copilot to summarize conversations.
author: gandhamm 
ms.author: mgandham 
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 07/14/2025
ms.update-cycle: 180-days
ms.custom: bap-template 
---


# Use Copilot to summarize conversations

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability.md)]

[!INCLUDE[cc-conv-summary-intro](../../shared/cc-conv-summary-intro.md)]

## Prerequisites

Your administrator enabled the Copilot conversation summary feature.

> [!NOTE]
> If your administrator enabled auto-summarization for ongoing conversations, you get an AI-generated summary of the conversation along with the Copilot-generated conversation summary. The two summaries can be slightly different. [Learn more about auto-summarized conversations](/dynamics365/customer-service/use/cs-ai-generated-summary).

## Navigation

In Copilot Service workspace, you can select **Summarize conversation** for an ongoing conversation.
  
## View a conversation summary

Based on your administrator's configuration, you see the following options in Copilot Service workspace:

[!INCLUDE[cc-conv-summary-actions](../../shared/cc-conv-summary-actions.md)]

- Select **Create case** to create a case and populate the description with the summary, if your administrator turned on this feature.
  > [!NOTE]
  > You can see **Create case** only if case management is configured.

### [Paragraph format](#tab/paragraphformat)

 :::image type="content" source="../media/copilot-conv-summary.png" alt-text="Screenshot of a Copilot conversation summary.":::

### [Structured format](#tab/structuredformat)

  :::image type="content" source="../media/structured-conv-summary.png" alt-text="Screenshot of a structured Copilot conversation summary.":::

---

### View summary for a closed conversation

You can also view the Copilot generated summary for a closed conversation. In Copilot Service workspace in the **Activities** view, filter by **Conversations** and then select the required conversation. Select the **Summary** tab. The summary for the conversation appears. Learn more in [View conversation transcripts and call recordings](/dynamics365/customer-service/use/voice-channel-call-recordings-transcripts).

## Next steps

[Use Copilot to solve customer issues](use-copilot-features.md)

