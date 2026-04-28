---
title: Outcomes for proactive engagement in Dynamics 365 Contact Center
description: Learn about the outcomes for proactive engagement calls in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.collection: bap-ai-copilot
ms.date: 04/29/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Outcomes for proactive engagement

Outcomes help determine the next action, such as whether to reattempt outreach or trigger a follow-up business process.

For example, in an appointment reminder campaign:

- If the outcome is **NoAnswer**, you can reattempt the call in the next available time window.
- If the AI agent captures that the customer requested to reschedule, you can trigger a follow-up workflow to create a rescheduling task.
- If a service representative selects a disposition code such as **Payment made**, you can suppress further reminders.

## Outcome types in Dynamics 365 Contact Center

Proactive engagement outcomes for voice and SMS are available from three sources.

### SIP-based outcomes

Applicable to voice only, SIP-based outcomes are fixed, system-defined outcomes from the telephony layer.

Azure Communication Services returns SIP-based early media outcomes, such as LiveAnswer, AnsweringMachine, Busy, and NoAnswer. The system stores these outcomes as result values in the proactive delivery entity.

> [!NOTE]
> In preview dial mode, **AnsweringMachine**, **AnsweringMachineHangup**, and **NotAHandset** outcomes aren't available. In these cases, service representatives must classify whether the call reached an answering machine by using disposition codes.

| Result | Description |
|--------|-------------|
| LiveAnswer | Answered by someone or something and interacted with AI agent. |
| AnsweringMachine | Determined as answering machine. Left message or voicemail if AI agent has answering machine detection topic enabled and configured to leave a message. |
| AnsweringMachineHangup | Determined as answering machine, AI agent hung up as configured in the topic and didn't leave a message or voicemail. |
| Undetermined | Answered by someone or something but didn't interact or have a conversation with AI agent. |
| NotAHandset | Detected as some tone such as SIT or FAX that indicates it's not a service representative or an answering machine. |
| BotFailed | AI agent failed to get started or failed during conversation with customer where phone went off-hook. |
| CallEnded | Preview dial mode call where customer phone went off-hook. |
| Busy | Customer returned busy signal, as indicated by SIP diagnostic information or early media results from Azure Communication Services. Customer phone didn't go off the hook. |
| NoAnswer | Customer phone dial resulted in no answer, SIP diagnostic information, or early media results from Azure Communication Services. Customer phone didn't go off the hook. |
| InvalidAddress | Customer phone dial resulted in invalid address, as indicated by diagnostic information or early media results from Azure Communication Services. Customer phone didn't go off the hook. |
| CallFailed | Customer phone didn't go off the hook and there was no SIP diagnostic information or early media results from Azure Communication Services. |
| Terminated | Preview dial mode call where customer wasn't attempted to be engaged because no representative was available or accepted after launching the call and valid window to contact the customer ended by then. |
| Unknown | Customer phone was attempted to be engaged, but there isn't enough information available about the attempt due to some error condition. |
| Cancelled | Customer wasn't attempted to be engaged because there was a request to cancel the delivery. |
| Expired | There was no more valid time window to engage the customer, or expiration date specified was in the past. Customer wasn't attempted to be engaged. |
| Error | Customer wasn't attempted to be engaged because of invalid configuration or data condition during the valid time window to engage with the customer. |

### AI agent outcomes

Applicable to voice and SMS, the outcomes are data values returned from the AI agent. This applies to connected calls and SMS conversations where the AI agent has an active conversation and sets values that are sent back to Dynamics 365 Contact Center.

Perform the steps in [Send data back from AI agent to Dynamics 365 Contact Center](configure-agentS-for-ai-led-proactive-engagement.md#send-data-back-from-ai-agent-to-dynamics-365-contact-center) to configure the outcomes.

### Representative disposition codes

These outcomes are set by the service representative to classify the result of voice or SMS conversations they handled.

Perform the steps in [Configure disposition codes](configure-disposition-codes.md).

For SMS workstreams, add disposition codes in workstream **Advanced settings** and configure whether workstream-level requirements override global settings.

All three outcome data points are stored centrally in proactive engagement data and can be used together to determine next steps in reporting and orchestration.

### Delivery outcomes

These are fixed, system-defined outcomes that reflect whether the SMS message was successfully delivered to the recipient.

| Result | Description |
| ------ | ----------- |
| Delivered | The SMS message was successfully delivered to the customer's device. |
| Not delivered | The SMS message could not be delivered to the customer's device. |

## Timeout settings for proactive engagement SMS

The system enforces timeout mechanisms at two stages of a proactive SMS engagement: before a conversation is created, and after.

### Pre-conversation: First response timeout

Configured on the proactive engagement SMS settings. The timer starts when the outbound SMS is delivered.

- **If customer replies within timeout**: A conversation is created in contact center.
- **If customer doesn't reply in time**: The delivery times out and no conversation is created.
- **Reply received after timeout**: Is treated as a new anonymous inbound SMS and isn't correlated with the original proactive engagement.

The **First response timeout** is the authoritative boundary for whether an outbound SMS successfully transitions into an active contact center conversation.

### Post-conversation: inactivity and timeout rules

These settings apply only after a conversation is created.

**Auto-close after inactivity**

Configured at the workstream level. Closes a conversation that remains in the waiting state beyond a configured idle threshold. Tune this to avoid premature closure of asynchronous SMS conversations where customers may respond over extended periods. Learn more in [Configure work distribution](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution).

**Agent inactivity timeout**

When a Copilot Studio agent handles the initial SMS conversation, the agent enforces its own inactivity timeout. Configure this to reflect realistic SMS response patterns and align it with the workstream auto-close setting to prevent inconsistent conversation termination. Learn more in [Manage the session lifecycle](/microsoft-copilot-studio/guidance/deploy-agent-teams#manage-the-session-lifecycle).

**Timeout rules**

Configured per workstream. Allow automated actions&mdash;such as sending a message, changing conversation state, or closing&mdash;based on inactivity conditions. Multiple rules can coexist, with action controlled by rule priority. Use timeout rules to customize handling of idle conversations beyond the default auto-close behavior. Learn more in [Configure timeout rules](/dynamics365/customer-service/administer/configure-time-out-rules).

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  
[Dial modes for proactive engagement](proactive-engagement-dial-modes.md)  
[Best practices for proactive engagement campaigns](proactive-engagement-best-practices.md)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
