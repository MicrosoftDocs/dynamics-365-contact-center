---
title: Outcomes for proactive engagement in Dynamics 365 Contact Center
description: Learn about the outcomes for proactive engagement calls in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.collection: bap-ai-copilot
ms.date: 09/29/2026
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

### [Voice](#tab/voice)

Voice outcomes are fixed, system-defined results that describe a proactive call or explain why the customer wasn't called. These results use call information, including SIP diagnostics and early media results from Azure Communication Services. The system stores them as result values in the proactive delivery entity.

> [!NOTE]
> Automatic answering machine detection isn't available in Preview dial mode. However, a Preview delivery can have an **AnsweringMachine** result when its recorded dispositions include the system **Answering machine** disposition. **AnsweringMachineHangup** and **NotAHandset** aren't derived for Preview calls.

| Result | Description | SIP codes |
|--------|-------------|-----------|
| LiveAnswer | The call was answered and classified as a live answer rather than an answering machine. | None |
| AnsweringMachine | The call reached an answering machine. For AI-led calls, the AI agent leaves a message or voicemail when its **Answering Machine Detection** system topic is enabled and configured to leave a message. | None |
| AnsweringMachineHangup | The call reached an answering machine, and the AI agent hung up as configured in its **Answering Machine Detection** system topic without leaving a message or voicemail. | None |
| Undetermined | The call was answered by someone or something, but no interaction or conversation with the AI agent was detected. | None |
| NotAHandset | A tone, such as SIT or fax tone, indicated that the call didn't reach a person or an answering machine. | None |
| BotFailed | The AI agent failed to start or failed during a conversation with the customer after the call was answered. | None|
| CallEnded | In Preview dial mode, the customer answered and the call ended. This result can also occur in other dial modes when the call ended without a more specific outcome. | None|
| NoAnswer | The call to the customer wasn't answered, was declined, or returned a busy signal, as indicated by SIP diagnostic information or early media results from Azure Communication Services. Busy responses are reported as **NoAnswer**. | 486 (Busy Here), 600 (Busy Everywhere), 603 (Decline), 607 (Unwanted) |
| InvalidAddress | The call to the customer failed because the destination phone number or address was invalid, as indicated by diagnostic information or early media results from Azure Communication Services. The customer's call wasn't connected. | 404 (Not Found), 410 (Gone), 484 (Address Incomplete), 485 (Ambiguous), 604 (Does Not Exist Anywhere) |
| CallFailed | The call attempt failed. This result can occur with or without SIP diagnostic information or early media results. In Preview dial mode, it can also occur when the available call information doesn't establish another outcome. | 408 (Request Timeout), 480 (Temporarily Unavailable), 487 (Request Terminated), 500 (Server Internal Error), 502 (Bad Gateway), 503 (Service Unavailable), 504 (Server Time-out) |
| NonRetriableError | A protocol or configuration issue was classified as a nonretriable error. This result doesn't trigger an automatic reattempt. | 401 (Unauthorized), 405 (Method Not Allowed), 407 (Proxy Authentication Required), 415 (Unsupported Media Type), 488 (Not Acceptable Here), 501 (Not Implemented), 505 (Version Not Supported) |
| Abandoned | In representative-led Progressive or Predictive dial mode, the customer answered, but the allowed wait time for a representative was exceeded. | None |
| Terminated | In Preview dial mode, no representative was available or accepted the call before the valid contact window ended. The customer wasn't called. | None |
| CSRCancelled | In Preview dial mode, the representative accepted the call but then selected **Cancel** after reviewing the customer's details, without dialing the customer. | None |
| Unknown | An error left insufficient information about the customer call attempt to determine its outcome. | None |
| Cancelled | The customer wasn't called because there was a request to cancel the delivery. | None |
| Expired | The customer wasn't called because no valid contact window remained or the specified expiration time had passed. | None |
| Error | The customer wasn't called because an invalid configuration or data condition prevented the delivery during the valid contact window. | None |


> [!NOTE]
> Busy responses are recorded as **NoAnswer** for current SIP-derived results. Historical records might contain **Busy**.


### [SMS](#tab/sms)

**Delivery outcomes**

Delivery outcomes are fixed, system-defined outcomes that reflect the lifecycle of the outbound SMS engagement, from sending the message to closing the resulting conversation. The system stores the SMS engagement outcome as the result value in the proactive delivery entity. Outcomes reflect SMS lifecycle events, timeouts, and delivery-processing conditions.

| Result | Description |
| ------ | ----------- |
| MessageSent | The SMS message was sent to the SMS provider or carrier for delivery to the customer device. This result doesn't confirm that the message reached the customer device. |
| MessageFailed | The SMS provider or carrier failed to deliver the outbound SMS message to the customer device. |
| ResponseTimeout | The customer didn't reply to the outbound SMS message within the configured first response timeout. No conversation is created. |
| ConsumerEngaged | The customer replied to the outbound SMS message and engaged with the AI agent. |
| AgentEscalation | The AI agent escalated the SMS conversation to a service representative. |
| AgentAccepted | A service representative accepted the escalated SMS conversation. |
| ConversationEnded | The customer's response triggered the end of conversation topic in the AI agent. |
| ConversationClosed | The AI agent or service representative closed the SMS conversation, or the system closed it automatically. |
| ConversationCancelled | The SMS conversation was closed because a new proactive engagement was sent to the same customer. |
| ConversationCutoffExceeded | The customer engaged with the outbound SMS message, but the conversation wasn't closed and had no activity for 15 days. |
| ConversationExists | The SMS message wasn't sent because an active conversation already exists between the same sender and recipient. |
| EngagementAbandoned | A new outbound SMS message was sent to the same customer from the same sender before the customer replied, so the previous engagement was abandoned. |
| OptOutReceived | The customer replied with an opt-out request, and the system validated the opt-out with the SMS provider's consent service. |
| Cancelled | The customer wasn't contacted because there was a request to cancel the delivery. |
| Expired | There was no more valid time window to contact the customer, or the specified expiration date was in the past. The customer wasn't contacted. |
| Error | The customer wasn't contacted because of an invalid configuration or data condition during the valid time window to contact the customer. |
| Unknown | There isn't enough information available about the engagement attempt because of an error condition. |

---

**AI agent outcomes**

Applicable to voice and SMS, the outcomes are data values returned from the AI agent. This applies to connected calls and SMS conversations in which the AI agent is actively engaged and sets values that are sent back to Dynamics 365 Contact Center.

Perform the steps in [Send data back from AI agent to Dynamics 365 Contact Center](configure-agentS-for-ai-led-proactive-engagement.md#send-data-back-from-ai-agent-to-dynamics-365-contact-center) to configure the outcomes.

**Representative disposition codes**

These outcomes are set by the service representative to classify the result of voice or SMS conversations they handled.

Perform the steps in [Configure disposition codes](configure-disposition-codes.md).

For SMS workstreams, add disposition codes in workstream **Advanced settings** and configure whether workstream-level requirements override global settings.

All three outcome data points are stored in proactive engagement data tables and can be used together to determine next steps in reporting and orchestration. Learn more in [Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md).

## Timeout settings for proactive SMS engagement

The system enforces timeout mechanisms at two stages of a proactive SMS engagement: before and after a conversation is created.

### Pre-conversation: First response timeout

Configured on the proactive engagement SMS settings. The timer starts when the system sends the outbound SMS message. Carrier delivery confirmation isn't required.

- **If customer replies within timeout**: A conversation is created.
- **If customer doesn't reply in time**: The delivery times out and no conversation is created.
- **Reply received after timeout**: Is treated as a new anonymous inbound SMS and isn't linked to the original proactive engagement.

The **First response timeout** indicates if an outbound SMS successfully transitions into an active contact center conversation.

### Post-conversation: inactivity and timeout rules

These settings apply only after a conversation is created.

**Auto-close after inactivity**

Configured at the workstream level. Closes a conversation that's in the waiting state beyond a configured idle threshold. Configure the setting to avoid premature closure of asynchronous SMS conversations where customers may respond over extended periods. Learn more in [Configure work distribution](/dynamics365/customer-service/administer/create-workstreams#configure-work-distribution).

**Agent inactivity timeout**

When an agent handles the initial SMS conversation, the agent enforces its own inactivity timeout. Configure the agent inactivity timeout to match the SMS response patterns and align it with the workstream auto-close setting to prevent inconsistent conversation termination. Learn more in [Manage the session lifecycle](/microsoft-copilot-studio/guidance/deploy-agent-teams#manage-the-session-lifecycle).

**Timeout rules**

Configured per workstream. Allow automated actions&mdash;such as sending a message, changing conversation state, or closing&mdash;based on inactivity conditions. Multiple rules can coexist, with action controlled by rule priority. Use timeout rules to customize handling of idle conversations beyond the default auto-close behavior. Learn more in [Configure timeout rules](/dynamics365/customer-service/administer/configure-time-out-rules).

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  
[Dial modes for proactive engagement](proactive-engagement-dial-modes.md)  
[Best practices for proactive engagement campaigns](proactive-engagement-best-practices.md)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
