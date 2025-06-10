---
title: Use Copilot to summarize conversations
description: Learn how customer service representatives can use Copilot to summarize cases and conversations in Copilot Service workspace.
author: gandhamm 
ms.author: mgandham 
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 06/10/2025
ms.custom: bap-template 
---


# Use Copilot to summarize conversations

[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

Copilot conversation summaries provide context and relay the steps that you took to solve the issue. You can summarize chat and transcribed voice conversations.

## Prerequisites

Your administrator enabled the Copilot conversation summary feature.

> [!NOTE]
> If your administrator enabled auto-summarization for ongoing conversations, you get an AI-generated summary of the conversation along with the Copilot-generated conversation summary. The two summaries can be slightly different. [Learn more about auto-summarized conversations](/dynamics365/customer-service/use/cs-ai-generated-summary).

## Navigation

- In Copilot Service workspace, you can select **Summarize conversation** for an ongoing conversation.
- When you sign in to a non-Microsoft CRM, and launch the embedded experience, sign in to your Dynamics account and then select **Summarize conversation** from the communication panel when you're in a conversation with a customer.
  
## View a conversation summary

Based on your administrator's configuration, you see the following options in Copilot Service workspace:

- The Copilot conversation summary generated automatically when you request a consultation with another customer service representative, transfer the conversation, or end the conversation. You can select **Summarize conversation** to generate the summary for an ongoing conversation, based on your administrator's configurations.
- The summary is displayed in a paragraph format or a structured format.
  - The paragraph format summarizes the conversation in a single paragraph.
     :::image type="content" source="../media/copilot-conv-summary.png" alt-text="Screenshot of a Copilot conversation summary.":::
  - The structured format summarizes and organizes the information in the conversation based on the options your administrator selected. <br>
     :::image type="content" source="../media/structured-conv-summary.png" alt-text="Screenshot of a structured Copilot conversation summary.":::

You can perform the following actions:

- Copy the summary.
- Select **Create case** to create a case and populate the description with the summary, if your administrator turned on this feature. This is applicable for Copilot Service workspace.
- Share feedback about the summary.
- Close the summary card.

### View closed conversation summary

You can also view the Copilot generated summary for a closed conversation. In Copilot Service workspace in the **Activities** view, filter by **Conversations** and then select the required conversation. Select the **Summary** tab. The summary for the conversation appears. Learn more in [View conversation transcripts and call recordings](/dynamics365/customer-service/use/voice-channel-call-recordings-transcripts).

## Next steps

[Use Copilot to solve customer issues](use-copilot-features.md)

