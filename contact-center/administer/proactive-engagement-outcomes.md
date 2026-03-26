---
title: Outcomes for proactive engagement
description: Learn about the outcomes for proactive engagement calls in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: reference
ms.collection: bap-ai-copilot
ms.date: 01/19/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Outcomes for proactive engagement

Outcomes represent the result of a proactive engagement call. The system stores outcomes as result values in the proactive delivery entity, which you can reference for call status tracking. Customer Insights Journey uses outcomes to support granular branching options, allowing you to define follow-up actions based on specific call results without additional configuration.

Context variables created in Copilot Studio that match a variable name in the workstream are automatically sent to Dynamics 365 in real time. These variables are accessible as disposition codes and for branching logic in Customer Insights Journey.

## SIP-based outcomes

SIP-based early media outcomes such as LiveAnswer, AnsweringMachine, Busy, and NoAnswer are returned by Azure Communication Services and stored as result values in the proactive delivery entity.

| Result | Description |
|--------|-------------|
| LiveAnswer | Answered by someone or something and interacted with Copilot agent or Copilot Studio Agent. |
| AnsweringMachine | Determined as answering machine. Left message or voicemail if Copilot agent or Copilot Studio agent has answering machine detection topic enabled and configured to leave a message. |
| AnsweringMachineHangup | Determined as answering machine, Copilot agent or Copilot Studio agent hung up as configured in the topic and didn't leave a message or voicemail. |
| Undetermined | Answered by someone or something but didn't interact or have a conversation with Copilot agent or Copilot Studio agent. |
| NotAHandset | Detected as some tone such as SIT or FAX that indicates it's not a service representative or an answering machine. |
| BotFailed | Copilot agent or Copilot Studio agent failed to get started or failed during conversation with customer where phone went off-hook. |
| CallEnded | Preview dial mode call where customer phone went off-hook. |
| Busy | Customer returned busy signal, as indicated by SIP diagnostic information or early media results from Azure Communication Services. Customer phone didn't go off the hook. |
| NoAnswer | Customer phone dial resulted in no answer, SIP diagnostic information or early media results from Azure Communication Services. Customer phone didn't go off the hook. |
| InvalidAddress | Customer phone dial resulted in invalid address, as indicated by diagnostic information or early media results from Azure Communication Services. Customer phone didn't go off the hook. |
| CallFailed | Customer phone didn't go off the hook and there was no SIP diagnostic information or early media results from Azure Communication Services. |
| Terminated | Preview dial mode call where customer wasn't attempted to be engaged because no agent was available or accepted after launching the call and valid window to contact the customer ended by then. |
| Unknown | Customer phone was attempted to be engaged, but there isn't enough information available about the attempt due to some error condition. |
| Cancelled | Customer wasn't attempted to be engaged because there was a request to cancel the delivery. |
| Expired | There was no more valid time window to engage the customer, or expiration date specified was in the past. Customer wasn't attempted to be engaged. |
| Error | Customer wasn't attempted to be engaged because there was some invalid configuration or data condition when it was time to engage the customer. |

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  
[Dial modes for proactive engagement](proactive-engagement-dial-modes.md)  
[Use proactive engagement tables for reporting](../extend/proactive-engagement-tables.md)  
