---
title: Set up consult with AI agents during voice conversations (preview)
description: Learn how to configure voice-enabled AI agents that customer service representatives can consult during voice calls for scenarios such as consent capture and identity verification.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 09/04/2026
ms.update-cycle: 180-days
ms.topic: how-to
ms.collection: bap-ai-copilot
---

# Set up consult with AI agents during voice conversations (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Customer service representatives (service representative or representative) can use the consult option to temporarily add a voice-enabled AI agent to a voice call. The AI agent runs a configured workflow, such as providing a mandatory disclosure, capturing explicit consent, or verifying a customer's identity with a PIN. After the workflow is complete, the representative resumes the call. The interaction remains in the same conversation. Recording and transcription behavior depends on the settings that you configure.

> [!NOTE]
> Voice-enabled AI agents can join a call only through the consult option.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/production-ready-preview-dynamics365.md)]

## Prerequisites

- You have the Omnichannel administrator role.
- You configured the [voice channel](/dynamics365/customer-service/administer/voice-channel?context=/dynamics365/contact-center/context/administer-context).
- You configured a [voice-enabled AI agent](#configure-an-ai-agent) with the required workflow for the voice workstream.

## Turn on consult with AI agents

By default, the setting is turned off.

1. In the site map of Copilot Service admin center, go to **Consult and transfer** in **Channels**, and then select **Manage**.
1. Turn on **Consult with AI agents**.
1. Select **Save**.

## Make AI agents available for consult

1. In the site map of Copilot Service admin center, go to **Workspaces** in **Support experience**, and then select **Manage** for **Voice call experiences**.
1. In the **Consult with AI agents (preview)** section, select **New**.
1. Select the voice-enabled AI agent that you want to make available for consult.
1. Set the following options:
   - **Transcription & recording**:
     - **Pause recording and transcription during consult**: Select when you need your customer to share sensitive information.
     - **Continue recording and transcription**
   - **Hold**:
     - **Keep the representative on hold during consult**
     - **Do not place on hold**
1. Select **Save**.

## Configure an AI agent

Use the following steps to configure an AI agent to run a workflow that addresses your business scenario, such as capturing consent.

1. Ensure that the Copilot Studio agent is connected to **Voice** and has a **Connected** status in Copilot Service admin center.
1. In Copilot Studio, open the agent, and then go to **Topics**.
   - Use the built-in **Start** topic, which runs automatically when a conversation begins.
   - Alternatively, create a new topic and call it from the **Start** topic. Learn more in [Create and edit topics](/microsoft-copilot-studio/authoring-create-edit-topics).
1. Add a step to play a message, such as a consent message that asks whether the customer agrees to proceed.
1. Configure the response to capture the customer's answer:
   - Yes
   - No
   - No response within a defined timeout period
1. Add a **Transfer Conversation** node to return the conversation to the representative and end the AI agent consultation after the response is captured.
1. Save and publish the changes.

## What happens during an AI agent consultation

When you turn on **Consult with AI agents**, the **AI Agents** tab becomes available in the consult experience.

1. During an active voice call, a representative selects **Consult**, opens the **AI Agents** tab, and selects a configured AI agent.
1. The AI agent joins the call. If you turn on **Keep the representative on hold during consult**, the representative is put on hold.
1. If you turn on **Pause recording and transcription during consult**, recording and transcription are paused.
1. The AI agent runs its workflow with the customer and then leaves the call. Ensure that you [configure handoff to a representative](/microsoft-copilot-studio/advanced-hand-off) in the agent topic.
1. The system automatically takes the representative off hold, and the representative resumes the conversation.

## Considerations

- If the AI agent is the only consultee in the call, consultation with other representatives isn't available.
- If the representative is consulting with other consultees, the hold, transcription, and recording settings apply to all consultees.
- If the AI agent consultation times out or fails, the system plays a message for the representative.

## Related information

[Enable transfer and consult](/dynamics365/customer-service/administer/enable-transfer-consult)
