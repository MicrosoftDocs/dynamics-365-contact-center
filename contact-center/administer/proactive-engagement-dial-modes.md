---
title: Dial modes for proactive engagement in Dynamics 365 Contact Center
description: Learn about the dial modes available for proactive engagement in Dynamics 365 Contact Center and how each mode supports different customer engagement scenarios.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: concept-article
ms.collection: bap-ai-copilot
ms.date: 06/05/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Dial modes for proactive engagement

Dial modes determine how the system places outbound calls to customers in a proactive engagement. Each mode balances AI agent involvement, service representative utilization, and customer experience differently.

> [!IMPORTANT]
> - The use of AI agent-led Copilot, progressive, and predictive dial modes or service representative-led progressive and predictive dial modes calls for commercial marketing or sales purposes constitutes a violation of Microsoft terms of service. Review applicable telecommunications regulations before using the dial modes.
> - The call connection time for service representative-led progressive and predictive dial modes isn't compliant with the Telephone Consumer Protection Act (TCPA). Review applicable telecommunications regulations before using service representative-led modes.

## Copilot

Use the Copilot dial mode for making announcements, notifications, or outbound calls that can that an IVR agent can handle. A large number of these calls can be made simultaneously. A few examples are payment reminders, service restoration, and delivery notifications.

When a customer answers the outbound call, the AI agent registered on the workstream engages with the customer. The agent can escalate to a service representative if necessary. However, the escalated calls might have wait times similar to calls made by the customer directly to the contact center for assistance.

## Progressive

The progressive dial mode places one call for every service representative who is available in the queue, so that customers get minimal wait times. It supports two engagement types:

- **AI agent-led**: As soon as the customer answers the call, a Copilot agent is added to handle preliminary tasks such as verifying that the right person answers and confirming their availability to talk. Once the preliminary validations are done, the service representative is added to continue the engagement. Using an AI agent to gather this information helps service representatives avoid calls that don't need their presence.
- **Service representative-led**: Service representatives are reserved and ready before the call is placed. When the customer answers, the system checks whether the call reached a voicemail. If it didn't, the reserved service representative is immediately added to the call.

## Predictive

The predictive dial mode uses a dynamic algorithm to initiate outbound calls before representatives become available, based on when they're forecasted to be free. This approach maximizes representative use while minimizing customer wait times.

> [!NOTE]
> The predictive dial mode requires at least 10 available service representatives at any point. If the number of available service representatives falls below 10, the system operates as progressive, placing only one call per newly available service representative. The system automatically switches back to predictive mode after the number of available service representatives goes back above 10.

The predictive dial mode supports two engagement types:

- **AI agent-led**: When the customer answers the call, an AI agent is added to handle preliminary tasks such as verifying that the right person answers and confirming their availability to talk. Once the preliminary validations are done, the service representative is added to continue the engagement. Using an AI agent to gather this information helps service representatives avoid calls that don't need their presence.

- **Service representative-led**: Service representatives are reserved and ready before calls are placed. When the customer answers, the system checks whether the call reached a voicemail. If it didn't, the reserved service representative is added to the call.

Each engagement type uses a different algorithm to determine the number of calls to place at any moment. Both algorithms calculate continuously in real time.

### AI agent-led predictive algorithm

The algorithm continuously calculates the number of calls to place based on current system conditions. The process works as follows:

1. **Determine a base dialing rate**. The system estimates the number of calls it needs to place per available agent to produce one successful connection. For example, if only half of all dials result in a transfer to a service representative, the system places two calls per agent to compensate.

1. **Adjust based on performance**. The base rate is adjusted depending on how the system is performing against configured thresholds for abandoned rate and customer wait time. If the system is within targets, the rate increases. If thresholds are exceeded, the rate decreases. Built-in limits prevent sudden swings and ensure smooth, gradual changes.

1. **Calculate the number of calls to place**. The adjusted rate is multiplied by the number of available agents and the percentage of agent capacity allocated to the campaign. The result is the number of outbound calls placed at that moment.

### Service representative-led predictive algorithm

The service representative-led algorithm uses customer wait duration as its primary metric - the time between when the customer connects to the call and when a service representative joins. The process works as follows:

1. **Check short-circuit rules**: Before running the full calculation, the system checks two safety conditions. If the exceeded customer wait threshold rate (30-day rolling average) is within 10 percent of the configured suspend threshold, or if the number of available agents is below a minimum threshold, the system reverts to one call per agent to protect customer experience.

1. **Determine a base dialing rate**: The system calculates the base rate as the inverse of the live answer rate (30-day rolling average). For example, if 12 percent of calls are answered live, the base rate is approximately 8.3 calls per agent.

1. **Determine whether to increment or decrement**: The system compares the recent average customer wait duration against a target derived from the configured wait duration threshold. If the actual wait time is below the target, the system increases the rate. If above, it decreases.

1. **Calculate a scale factor**: Based on how far the actual wait time is from the target, the system calculates a scale factor. This factor is constrained between fixed bounds (0.1 to 2.0) to prevent extreme adjustments in either direction.

1. **Calculate the final rate**: The base rate is multiplied by the scale factor to produce a proposed new rate. To ensure smooth transitions, the system limits how much the rate can change from the previous rate within an interval - no more than 35 percent increase or decrease. The resulting value is the final dialing rate.

**Example: Service representative-led rate calculation**

This example illustrates how the algorithm calculates the dialing rate with the following configuration:

- Wait duration threshold: 5 seconds
- Suspend threshold percentage: 3%
- Live answer rate (30-day average): 12%
- Average wait duration (last 5 minutes): 3 seconds
- Available agents: 15
- Existing rate: 3 calls/agent

**Step 1 - Short-circuit checks**: The exceeded customer wait threshold rate (2%) is below 90% of the 3% threshold (2.7%), so no short-circuit is triggered. Available agents (15) are above the minimum threshold (10).

**Step 2 - Increment or decrement**: The target wait duration is 4 seconds (5 × 0.8). The actual wait time (3 seconds) is below the target, so the system increments the rate.

**Step 3 - Scale factor**: The actual wait is 75% of the target (3 ÷ 4). The raw scale factor is 1 ÷ 0.75 = 1.33, which is within the allowed bounds of 0.1 to 2.0.

**Step 4 - Final rate**: The base rate is 1 ÷ 0.12 = 8.33. The proposed rate is 8.33 × 1.33 ≈ 11.1. However, the maximum allowed increase from the existing rate of 3 is 35%, giving a cap of 4.05. The final rate is **4.05 calls per agent**.

## Preview

Use the preview dial mode to identify a service representative from the specified queue and then notify them of the request to make the outbound call. The number of simultaneous calls made is dependent on the number of available representatives. If the representative accepts, then the system based on configuration gives the representative time to review the details and place the outbound call to customer when ready. Representative gets to speak to the customer if they pick up or leave a voicemail. This dial mode prioritizes customer experience over representative use, and is best suited for scenarios that require a personalized experience.

> [!NOTE]
> Timer and early media audio for service representatives for preview calls are available with Teams Phone Extensibility numbers only.

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  
[Outcomes for proactive engagement](proactive-engagement-outcomes.md)  
[Overview of proactive engagement](overview-proactive-engagement.md)  
