---
title: Use Human Assist (preview)
description: Use Human Assist to get real-time resolution steps and suggested replies during customer conversations in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/16/2026
ms.custom: bap-template
ai-usage: ai-assisted
---

# Use Human Assist (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Human Assist provides customer service representatives (service representatives or representatives) with real-time resolution steps and suggested replies during customer conversations by using an AI agent and reasoning logic in Copilot Service workspace.

You stay in control of every action. Insert, edit, or ignore suggested replies, and approve tools before they run. Human Assist uses approved knowledge sources to provide consistent guidance, with links to the underlying sources.

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

Before you use Human Assist, your administrator must complete the following setup:

- Create a real-time AI agent with knowledge, tools, and instructions specifically for Human Assist, rather than a self-service scenario. Learn more in [Configure real-time agents](/microsoft-copilot-studio/voice-realtime-configure?tabs=digitalmessagingagent).

- When you configure connectors and tools, give each input parameter a clear name and description. Human Assist relies on these descriptions to map details from the conversation, such as a card number or account number, to the correct parameter. Generic parameters, such as a Dataverse connector's row item, can't be mapped correctly. To work with Dataverse, use a Power Automate flow that exposes clearly defined inputs and performs the Dataverse operation internally, rather than calling the Dataverse connector directly.

- Enable the Human Assist capabilities for representatives through [experience profiles](/dynamics365/customer-service/administer/create-agent-experience-profile). In the experience profile, ensure that every channel that you plan to use is enabled, including the voice channel.


- Enable Copilot feedback for the tenant to let representatives send feedback to Microsoft.

  - **Basic Copilot feedback** lets representatives submit a thumbs-up or thumbs-down rating with a description. If this setting is off, the rating controls don't appear.
  - **Additional Copilot feedback** lets representatives share prompt and response data with your rating. If this setting is off, the **Share relevant prompts, responses, and diagnostic data?** checkbox doesn't appear.

  Learn more in [Manage tenant settings](/power-platform/admin/tenant-settings).

## Supported channels, languages, and workspaces

Human Assist is available in Copilot Service workspace. The preview supports live chat, voice, SMS, Microsoft Teams, Direct Line, Messaging API, and WhatsApp.

For voice conversations, Human Assist uses the real-time call transcript. It doesn't process audio directly, so it doesn't work when transcription is turned off. Email isn't supported.

| Capability | Supported languages |
|---|---|
| Resolution steps | English, Arabic, and Spanish |
| Suggested replies | English only |

Conversations in other languages aren't blocked, but the preview doesn't support those languages.

## Use resolution steps and suggested replies

Open a conversation for a supported channel in Copilot Service workspace. Human Assist provides guidance alongside the conversation after the customer sends at least three messages.

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

## Guidance for administrators and agent designers

How well Human Assist performs depends mostly on how its AI agent is designed: the processes it knows, the knowledge it can use, the tools it can suggest, and how its instructions are written. The following recommendations come from early deployments. They aren't step-by-step instructions, but they help administrators and designers of the Human Assist AI agent get started in the right direction.

### Plan before you build

- **Start with a few well-defined processes.** For the first pilot, pick two or three high-volume conversation types with a clear outcome, such as a booking, a refund, or a change of details. Add more processes after these work well.
- **Map each process as representatives work it today.** List the steps in order, the system each step happens in, the details collected, and the step that completes the request. Note which steps a tool can perform and which steps stay manual.
- **Identify the source of truth for facts.** Prices, policies, opening hours, deadlines, and service levels must come from approved knowledge. Identify gaps before you build, not after the first test.
- **Agree on scope.** Decide which channels and languages are in the pilot, and which group of representatives uses it first. Learn more in [Supported channels, languages, and workspaces](#supported-channels-languages-and-workspaces).

### Set up for success

- **Confirm the AI agent type early.** Ensure the Human Assist AI agent is a real-time agent before you start authoring, so you don't have to redo the work in a new agent.
- **Ground the AI agent in approved knowledge only.** Connect knowledge for every factual question that the processes raise, and limit the AI agent to that knowledge rather than general model knowledge. Keep articles focused: one topic per article, a consistent structure across similar articles, and a version for each language you support.
- **Keep tools few, focused, and well described.** Give each tool one clear purpose, name and describe inputs in business terms, and return small results that the representative can relay. When a record should be linked to the conversation, pass the conversation context to the tool rather than asking the representative for it.
- **Roll out in stages.** Start with a pilot experience profile. Check that every channel in scope is enabled and, for voice, that transcription is turned on. Widen access after the pilot results are stable.

### Design the AI agent's instructions

- **Remember who reads what.** A suggested reply is meant to reach the customer as written, either sent by the representative in a digital conversation or spoken by the representative on a call. Keep customer-facing wording separate from guidance for the representative. Put instructions for the representative in the steps, never in text that can become a reply. For voice, keep replies short and easy to say aloud.
- **Match the structure to the complexity.** One AI agent is enough for a single, simple process. For several processes, use a main AI agent that identifies the request and one child agent for each process. Give each child agent a short description of what it handles and what it doesn't. Human Assist uses that description to route the conversation.
- **Write each process as small, specific steps.** Include one action or one piece of information per step, in order, and name the system or tool involved. Vague steps, such as "follow the usual process," and steps that combine several actions are hard to track and coach.
- **Separate running a tool from sharing its result.** Use one step to run the tool and another step to tell the customer the outcome, so each step can be tracked on its own.
- **Make completed work visible in the conversation.** Human Assist tracks resolution steps from the conversation, or from the transcript on a call. When a representative works in another application, a short message to the customer after the step is done, such as "I've found your booking," lets Human Assist recognize the step as completed. A promise, such as "I'll check that now," isn't evidence that the step happened.
- **Use what the customer already said.** Instruct the AI agent to read the whole conversation and not to ask again for details the customer already gave, including details given to a self-service agent before the handoff.
- **Don't let the AI agent guess facts.** When knowledge doesn't cover a question, the AI agent should suggest a holding reply and let the representative confirm, rather than invent a price, date, availability, or policy.
- **Describe content, not layout.** Human Assist decides how to present replies and steps. Prescribing a reply format or template tends to crowd out the guidance.
- **Write for the languages in scope.** Resolution steps support English, Arabic, and Spanish. Suggested replies support English only. Test every language you plan to use.

### Test and improve

- **Test with scripted conversations** for each process, channel, and language in scope, with one person as the customer and one as the representative. Suggestions start after the customer's third message.
- **Include hard cases.** For example, the customer gives every detail up front, changes their request and comes back to it, replies "thanks" or "ok" mid-process, or asks something the knowledge doesn't cover. Also test when a tool returns no result or fails.
- **Check each run** for the right process, no repeated questions, replies that are ready to send or say, no invented facts, recorded tool steps, and manual steps that end as completed rather than skipped.
- **Change one thing at a time.** Republish, and then rerun the full set of test conversations, not just the case you fixed.
- **Use the pilot's signals.** Review Copilot's reasoning, representative feedback, and the adherence report. A step that's often skipped usually points to a design issue, such as a vague step or work done without telling the customer, rather than to the representatives.

### Troubleshoot common issues

| Symptom | Likely cause | Where to look |
|---|---|---|
| The AI agent suggests asking again for details the customer already gave. | The instructions don't say to reuse earlier details. | AI agent instructions |
| Steps show as skipped while the representative works on them in another application. | Completion isn't visible in the conversation or call transcript. | Confirmation messages for manual steps |
| A step stays in progress. | The representative promised the action instead of confirming it was done. | Confirmation wording |
| A suggested reply contains instructions meant for the representative. | Representative guidance is mixed with customer-facing wording. | AI agent instructions |
| A reply states a price or policy that isn't in your knowledge. | No knowledge covers the question, or general knowledge is allowed. | Knowledge sources and AI agent settings |
| A tool runs with the wrong values. | Tool inputs are generic or poorly described. | Tool and flow input descriptions |
| The wrong process is suggested. | Child agent descriptions overlap. | Child agent descriptions |
| Steps are long, vague, or hard to follow. | The instructions contain compound or generic steps. | Process steps in the AI agent instructions |
| Nothing appears at the start of a conversation. | This behavior is expected. Suggestions start after the customer's third message. | No action needed |
| Nothing appears on voice. | Transcription is turned off, or the voice channel provider isn't enabled in the experience profile. | Experience profile and voice settings |

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
| Minimum customer messages | Human Assist generates suggestions only after the customer sends at least three messages to the representative. |
| Voice transcription | On voice, Human Assist doesn't work when transcription is turned off. |

## Related information

[Create and use experience profiles](/dynamics365/customer-service/administer/create-agent-experience-profile)  
