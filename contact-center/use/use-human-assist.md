---
title: Use Human Assist (preview)
description: Use Human Assist to get real-time resolution steps and suggested replies during customer conversations in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/02/2026
ms.custom: bap-template
ai-usage: ai-assisted
---

# Use Human Assist (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Human Assist provides customer service representatives (service representatives or representatives) with real-time resolution steps and suggested replies during customer conversations by using AI agent and reasoning logic in Copilot Service workspace.

You stay in control of every action. Insert, edit, or ignore suggested replies, and approve tools before they run. Human Assist uses approved knowledge sources to provide consistent guidance, with links to the underlying sources.

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

Before you use Human Assist, your administrator must complete the following setup:

- Create a real-time AI agent with knowledge, tools, and instructions specifically for Human Assist, rather than a self-service scenario. Learn more in [Configure real-time agents](/microsoft-copilot-studio/voice-realtime-configure?tabs=digitalmessagingagent).

- Enable the Human Assist capabilities for representatives through [experience profiles](/dynamics365/customer-service/administer/create-agent-experience-profile).

- Enable Copilot feedback for the tenant to let representatives send feedback to Microsoft.

  - **Basic Copilot feedback** lets representatives submit a thumbs-up or thumbs-down rating with a description. If this setting is off, the rating controls don't appear.
  - **Additional Copilot feedback** lets representatives share prompt and response data with your rating. If this setting is off, the **Share relevant prompts, responses, and diagnostic data?** checkbox doesn't appear.

  Learn more in [Manage tenant settings](/power-platform/admin/tenant-settings).

## Supported channels, languages, and workspaces

Human Assist is available in Copilot Service workspace. The preview supports live chat, voice, SMS, Microsoft Teams, Direct Line, Messaging API, and WhatsApp.

For voice conversations, Human Assist uses the real-time call transcript. It doesn't process audio directly. Email isn't supported.

| Capability | Supported languages |
|---|---|
| Resolution steps | English, Arabic, and Spanish |
| Suggested replies | English only |

Conversations in other languages aren't blocked, but the preview doesn't support those languages.

## Use resolution steps and suggested replies

Open a conversation for a supported channel in Copilot Service workspace. Human Assist provides guidance alongside the conversation.

### Follow resolution steps

Review the recommended workflow for the customer's problem and the supporting rationale. Human Assist grounds the guidance in approved knowledge sources.

As you progress, the checklist automatically tracks steps as **Completed**, **Skipped**, or **Not started**. It warns you when you skip recommended steps.

> [!NOTE]
> Step status is AI-generated and can be incorrect, especially in long, complex workflows. Use the checklist as guidance, not as an authoritative record.

### Review suggested replies

Review the suggested reply and its knowledge source links. Insert the reply, edit it, or ignore it. The customer doesn't receive the reply unless you choose to send it.

### Approve tool runs

When the AI agent requests an action, such as a refund or an account update, approve and trigger the tool run. The AI agent doesn't run tools on its own.

## Review Copilot's reasoning

**Copilot's reasoning** appears inline in the conversation next to the message you sent. Expand it to review the reply Copilot suggested at that point, how long the suggestion took, and which tools ran.

Use this record to compare what Copilot suggested with what you sent.

## Send feedback

When your administrator allows Copilot feedback, rate each suggested reply and the resolution steps for the current intent. Feedback goes to Microsoft to help improve the product.

- Select **Thumbs up** to choose what you liked: **Factually correct**, **Comprehensive response**, **Followed instructions**, **Great formatting**, **Personality / tone**, or **Other**. You can also add a comment.
- Select **Thumbs down** to add an optional comment and, when allowed, choose whether to share relevant prompts, responses, and diagnostic data with Microsoft.

Don't include private or sensitive information in feedback. The form links to information about how Microsoft uses the data and to the Microsoft Privacy Statement.

The system records your rating even if you close the form without a comment and resets the ratings for each new suggestion.

In government clouds, the feedback form doesn't ask for content samples or permission to contact you.

## Review resolution step adherence as a supervisor

In Copilot Service workspace, open the Quality Assurance Agent report in Omnichannel historical analytics to review how closely representatives follow Human Assist resolution steps. Filter the report by time period, channel, queue, and representative.

| Report element | Description |
|---|---|
| **Resolution steps followed** | Shows the number of completed steps out of the total suggested, the percentage followed, and the change from the previous period. |
| **Adherence breakdown** | Shows the split between completed and skipped steps for conversations with suggested resolution steps. |
| **Adherence rate over time** | Shows the adherence trend against a reference threshold to help identify drops. |
| **By Customer Service Representative** | Shows a sortable adherence rate for each representative. The rate is blank for representatives with no suggested resolution steps. |

Adherence metrics cover resolution steps only.

## Known limitations

The following limitations apply to Human Assist.

| Area | Limitation |
|---|---|
| Topics | Topics aren't supported. Deterministic flows, such as question-and-answer nodes with word-for-word suggestions, aren't available. |
| Output format | Suggested replies are text only. Adaptive Cards aren't rendered. |
| Interaction model | Proactive recommendations only are supported. Representative-initiated queries aren't available in preview release. |
| Model | Human Assist uses a fixed model, irrespective of the model selected in the agent canvas. Model selection isn't supported. |
| Access control | Access is managed through experience profiles only. Profiles can't separate voice from digital channels, and representatives can't turn off Human Assist. |
| Conversation context | Human Assist uses the full conversation transcript. Earlier context isn't removed when the customer's intent changes. |
| Context window | The context window is limited to 128K tokens. Keep knowledge articles reasonably sized. |
| Suggested reply analytics | Supervisor and customer-facing analytics aren't available for suggested replies. |

## Related information

[Create and use experience profiles](/dynamics365/customer-service/administer/create-agent-experience-profile)  
