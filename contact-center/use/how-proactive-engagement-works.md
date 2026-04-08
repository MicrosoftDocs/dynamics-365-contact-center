---
title: How proactive engagement works in Dynamics 365 Contact Center
description: Learn about how proactive engagement works in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 04/07/2026
ms.custom: bap-template
---
 
# How proactive engagement works

The service representative experience in Copilot Service workspace depends on the dial mode and engagement type selected by your administrator. Administrators can configure experience elements like notification templates.

## Representative-led preview dial mode

In representative-led preview dial mode, the representative controls whether to place the outbound call.
 
1. A notification appears on the representative desktop with the proactive engagement name and description.
1. The representative can **Accept** or **Reject** the request.
1. After acceptance, the representative reviews customer details in the session.
1. The call starts based on configuration:
    - Manual start by the representative, or
    - Automatic start after countdown (when enabled).
1. If the customer has multiple phone numbers, the representative can select the number to make the call to. The representative can also cancel the call if they determine there's no longer a need to place the call.
1. During and after the call, the representative can add disposition codes, if enabled, to classify the call outcome.

## Representative-led predictive and progressive dial modes

In representative-led predictive and progressive modes, the system places calls and connects representatives when a customer answers.

1. A notification appears on the representative desktop with the proactive engagement name and description, letting them know that they're going to be included in a proactive engagement session.
1. The system puts the representative on a lobby call to reserve them while outbound calls are in progress. When a representative is in the lobby, they can continue to work on other tabs but aren't assigned any incoming calls.
1. When a live customer answers, the call connects to the representative session with an audible cue. The desktop refreshes to load the details of the customer that was connected.
1. If no live customer is reached and if there are no calls to place, the system unreserves the representative.
1. The representative handles the connected call and captures disposition codes, if enabled, before closing the session.

## AI agent-led dial modes

In AI agent-led copilot, progressive, and predictive modes, the AI agent initiates customer engagement and escalates to  representatives only when necessary.

1. The AI agent engages with the customer first.
1. When the AI agent determines human assistance is needed, it escalates to a representative. A notification appears on the representative's desktop showing the proactive engagement name and description
1. The representative can **Accept** or **Reject** the request (in case of Copilot), and the request is **auto accepted** in case of predictive and progressive.
1. If the representative accepts, they are placed on the call to begin engaging with the customer.
1. If disposition codes are configured, the service representative can select disposition codes to record the interaction outcome. Learn more in [Configure disposition codes](../administer/configure-disposition-codes.md).

### Do not contact

Service representatives can honor customer do-not-contact requests during proactive engagement calls.

- The service representative can mark that a customer requested no further outreach by selecting the out-of-box **Do not contact** disposition code.
- The customer number is added to the do-not-contact table and doesn't receive further outbound calls.

### Related information

[Overview of proactive engagement](../administer/overview-proactive-engagement.md)  
[Dial modes for proactive engagement](../administer/proactive-engagement-dial-modes.md)  
[Configure proactive engagement](../administer/configure-proactive-engagement.md)  