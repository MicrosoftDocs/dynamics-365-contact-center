---
title: Use proactive engagement dashboard in Dynamics 365 Contact Center
description: Learn about the proactive engagement delivery metrics that help you track outbound delivery performance and outcomes in Dynamics 365 Contact Center.
author: Soumyasd27
ms.author: sdas
ms.reviewer: sdas
ms.topic: concept-article
ms.collection: 
ms.date: 07/01/2026
ms.custom: bap-template
---

# Proactive Engagement dashboard

The Proactive Engagement dashboard in Omnichannel real-time analytics gives supervisors a live view of proactive outbound activity so they can monitor in-flight engagements, agent availability, and pacing as it happens. Use the **Proactive engagement**, **QueueName**, **Time zone**, and **Business unit** filters at the top of the dashboard to scope the data to a specific configuration, queue, or organizational unit.

## Prerequisites

- You enabled real-time analytics for proactive engagement. Learn more in [Manage real-time analytics reports](/dynamics365/customer-service/administer/enable-realtime-analytics-dashboard-administrator).
 - You [configured proactive engagement](../administer/configure-proactive-engagement.md).

- You have the Omnichannel Supervisor role.

## Access the dashboard

You can access the dashboard from the Customer Service workspace. Learn more in [Access the dashboards](/dynamics365/customer-service/use/intro-realtime-analytics-dashboard).

### Key performance indicators

The dashboard displays the following KPI tiles for the selected filters:

- **Total unique engagements pending**: The number of unique outbound engagements that are scheduled or queued but not yet attempted.

- **Total engagements in progress**: The number of engagements that are currently active, such as being dialed, ringing, or in an ongoing interaction.

- **Throughput**: The number of proactive deliveries processed over the last hour, reflecting the rate at which outbound work moves through the system.

- **Time remaining**: The estimated time left to clear the pending outbound workload at the current pace.

- **Total completed engagements**: The number of engagements that reached their final intended outcome.

- **Abandoned rate**: The percentage of deliveries that were abandoned out of the total deliveries attempted.

- **Avg. handle time**: The average time spent handling a proactive engagement conversation, including talk, hold, and wrap-up time.

- **Connect rate**: The percentage of deliveries that successfully connected to the customer out of the total deliveries attempted.

Learn more about these measures in [Use proactive engagement metrics](#use-proactive-engagement-metrics).

### Real-time charts

- The **Pending engagements by attempt** chart breaks down pending engagements by attempt number, such as 2nd Attempt, 3rd Attempt, and No Attempt.

- The **Pending engagements per queue** bar chart shows how pending engagements are distributed across queues, helping you balance workload.

- The **Agent availability status** donut chart shows the share of agents in each presence state, such as Available and Do not disturb.

- The **Conversation time** chart shows the time spent on active proactive engagement conversations.

- The **Total completed engagements** chart breaks down completed engagements by attempt outcome, such as 1st Attempt, 2nd Attempt, 3rd Attempt, and Unreachable.

## Use proactive engagement metrics

[!INCLUDE[cc-feature-availability-cc-only](../includes/cc-feature-availability-cc-only.md)]

This section explains the proactive engagement delivery metrics available in Dynamics 365 Contact Center. Use these metrics to track outbound delivery performance, monitor key performance indicators (KPIs), and improve the outcomes of your proactive outreach.

These metrics are part of the `FactPEDeliveryMetrics` model and appear on the Proactive engagement dashboard. For more information, see [Proactive engagement dashboard](proactive-outbound-dashboard.md).

## Abandoned rate %

The percentage of proactive deliveries that you abandoned out of the total deliveries you attempted. A delivery is abandoned when the customer connects but the interaction ends before a representative can be added to the call. 

## Completed attempt value

The total value of completed delivery attempts. It aggregates the attempts that reached a final completed state, so you can measure the overall effort that resulted in successful outreach.

## Completed deliveries count

The total number of proactive deliveries that completed successfully. A delivery is completed when it reaches its final intended outcome, such as connecting to and engaging the customer or end of attempts.

## Connect rate %

The percentage of proactive deliveries that successfully connected to the customer out of the total deliveries attempted. It measures how often outreach reaches the intended customer, so you can assess number quality, dialing strategy, and reachability.

## Deliveries in progress

The number of proactive deliveries that are currently active and not yet in a final state. These deliveries are being dialed, ringing, or in an ongoing interaction, so you get real-time visibility into current outbound workload.

## Live person deliveries

The number of proactive deliveries that connect to a live person rather than to voicemail, an answering machine, or no answer. This metric helps you understand how much outreach reaches an actual customer.

## PE Abandoned conversations

The total number of proactive engagement conversations that were abandoned. Unlike abandoned rate, this metric is the raw count of abandoned conversations rather than a percentage.

## PE Avg. handle time (hh:mm:ss)

The average time spent handling a proactive engagement conversation, expressed in hours, minutes, and seconds. Handle time includes talk time, hold time, and wrap-up time, providing a full view of representative effort per interaction.

## PE Avg. handle time (sec)

The average time spent handling a proactive engagement conversation, expressed in seconds. This measure is the same as average handle time, reported in seconds for finer-grained comparison and reporting.

## PE Avg. hold time (sec)

The average time a customer is placed on hold during a proactive engagement conversation, expressed in seconds. Long hold times can negatively affect customer experience, so this metric helps identify where waits occur.

## PE Avg. talk time (sec)

The average time spent talking with the customer during a proactive engagement conversation, expressed in seconds. It reflects the active conversation time, excluding hold and wrap-up.

## PE Avg. wrap time (sec)

The average time spent wrapping up a proactive engagement conversation after the interaction ends, expressed in seconds. Wrap-up covers post-call activities such as logging notes and updating records.

## Pending attempt value

The total value of delivery attempts that are pending - scheduled or queued but not yet attempted. Use this value to understand the size of the upcoming outbound workload.

## Throughput

The number of proactive deliveries processed over the last hour. It reflects the rate at which outbound deliveries move through the system, helping you measure capacity and pacing.

## Time to completion (hh:mm:ss)

The average time taken to complete a proactive delivery, expressed in hours, minutes, and seconds. It measures the duration from when a delivery starts to when it reaches a completed state, including reattempts.

## Total completed (all attempts)

The total number of completed proactive deliveries across all attempts, including deliveries that succeeded after one or more reattempts. Use this value to see total successful outreach over the full retry lifecycle.

## Total pending (all attempts)

The total number of pending proactive deliveries across all attempts. It counts deliveries awaiting an initial attempt or a scheduled reattempt, giving a complete view of outstanding outbound work.

### Related information

[Proactive Outbound dashboard](proactive-outbound-dashboard.md)  
[Overview of proactive engagement](../administer/overview-proactive-engagement.md)  
[Configure proactive engagement](../administer/configure-proactive-engagement.md) 
