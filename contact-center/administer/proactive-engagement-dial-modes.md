---
title: Dial modes for proactive engagement
description: Learn about the dial modes available for proactive engagement in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot
ms.date: 01/19/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Dial modes for proactive engagement

Dial modes determine how the system places outbound calls to customers in a proactive engagement. Each mode balances AI agent involvement, service representative utilization, and customer experience differently.

> [!IMPORTANT]
> The use of Copilot, predictive and or progressive dial modes for non-transactional commercial purposes constitutes a violation of Microsoft terms of service.
Regulations governing the use of AI in outbound voice calls vary by country and region. Review applicable regulations based on your organization's and customers' locations before deploying these dial modes.

## Copilot

Use the Copilot dial mode for making announcements, notifications, or any outbound call that can be handled by an IVR agent. A large number of these calls can be made simultaneously. A few examples are payment reminders, service restoration, and delivery notifications.

When a customer picks an outbound call, the AI agent registered on the workstream engages with the customer. The agent can escalate to a service representative if necessary. However, the escalated calls might have wait times similar to calls made by the customer directly to the contact center for assistance.

## Progressive

The progressive dial mode places one call for every service representative who is available in the queue, so that customers get minimal wait times. It supports two engagement types:

- **AI agent led**: As soon as the customer answers the call, a Copilot agent is added to handle preliminary tasks such as verifying that the right person has answered and confirming their availability to talk. Once the preliminary validations are done, the service representative is added to continue the engagement. Using an AI agent to gather this information helps service representatives avoid calls that don't need their presence.
- **Service representative led**: Service representatives are reserved and ready before the call is placed. When the customer answers, the system checks whether the call reached a voicemail. If it did not, the reserved service representative is immediately added to the call.

> [!IMPORTANT]
> The call connection time for service representative-led progressive and predictive dial modes is not compliant with the Telephone Consumer Protection Act (TCPA). Review applicable telecommunications regulations before using service representative-led modes.

## Predictive

A predictive dialer is an automated outbound calling system designed to boost agent efficiency and streamline customer outreach. It initiates calls ahead of CSR availability by forecasting when agents are ready to engage. Using a dynamic algorithm, it calculates the optimal number of simultaneous calls to place based on anticipated CSR  availability. This algorithm factors in key contact center metrics such as abandonment rate, average wait time, queue targets, and other performance indicators to determine the ideal dial volume. The predictive dial mode supports two engagement types:

- **AI agent led**: As soon as the customer answers the call, a Copilot agent is added to handle preliminary tasks such as verifying that the right person has answered and confirming their availability to talk. Once the preliminary validations are done, the service representative is added to continue the engagement. Using an AI agent to gather this information helps service representatives avoid calls that don't need their presence.

- **Service representative led**: Service representatives are reserved and ready before calls are placed. When the customer answers, the system checks whether the call reached a voicemail. If it did not, the reserved service representative is added to the call.

> [!IMPORTANT]
> The call connection time for service representative-led progressive and predictive dial modes is not compliant with the Telephone Consumer Protection Act (TCPA). Review applicable telecommunications regulations before using service representative-led modes.

## Preview

Use the preview dial mode to identify a service representative from the specified queue and then notify them of the request to make the outbound call. The number of simultaneous calls made is dependent on the number of available representatives. If the representative accepts, then the system based on configuration gives the CSR time to review the details and place the outbound call to customer when ready. Representative gets to speak to the customer if they pick up or leave a voicemail. This dial mode prioritizes customer experience over representative use, and is best suited for scenarios that require a personalized experience.

> [!NOTE]
> Timer and early media audio for CSRs for preview calls are available only with Teams Phone Extensibility (TPE) numbers.

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  
[Outcomes for proactive engagement](proactive-engagement-outcomes.md)  
[Overview of proactive engagement](overview-proactive-engagement.md)  
