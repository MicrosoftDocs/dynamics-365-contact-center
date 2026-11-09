---
title: View biometric authentication and fraud detection business performance (preview)
description: Learn how to use the Business Performance screen to monitor voice enrollment, authentication, and fraud detection metrics in Dynamics 365 Contact Center.
author: timsavage
ms.author: timsavage
ms.reviewer: puneetsingh
ms.topic: how-to
ms.date: 11/09/2026
ms.custom: 
    - bap-template
    - ai-gen-docs-bap
    - ai-seo-date: 11/09/2026
ai-usage: ai-assisted

#customer intent: As a supervisor or analyst, I want to review voice enrollment, authentication, and fraud detection metrics so that I can measure how well the biometric authentication and fraud detection capabilities perform for my organization.
---

# View biometric authentication and fraud detection business performance (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

The **Biometric authentication and fraud detection** app brings your voice enrollment, authentication, and fraud detection reporting together on a single **Business Performance** screen. As a supervisor or analyst, use this screen to see how many customers enrolled their voiceprints, how reliably callers authenticate, and how effectively your team responds to fraud alerts. The metrics help you spot trends, compare authentication profiles, and decide where to focus improvements.

This article shows you how to open the **Business Performance** screen, read each of its three tabs, and filter the data to answer specific questions.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Open the Business Performance screen

The **Business Performance** screen is the reporting home for the **Biometric authentication and fraud detection** app. Open it to reach all three reporting tabs.

1. Sign in to the **Biometric authentication and fraud detection** app.
1. In the navigation pane, select **Business Performance**.
1. Select one of these tabs: **Voice Enrollment**, **Authentication**, or **Fraud Detection**.

> [!NOTE]
> Only Fraud Analyst or Fraud Supervisors can view the **Business Performance** screen.

## Review voice enrollment metrics

The **Voice Enrollment** tab shows how many customers have created a voiceprint and how enrollment is trending. Use it to gauge adoption and to find where customers drop out of the enrollment process.

The tab presents both numeric summaries and graphs for the following metrics:

- **Total voiceprints**: The total number of active voiceprints available for use.
- **Opted out customers**: The total number of customer profiles where consent = N.
- **Time-series New voiceprints created**: Number of new voiceprints created per month.
- **Time-series Opt out rate**: The percentage of end users who opt out compared to all end users who complete the enrollment flow.
- **Time-series Enrollment failures**: The number of enrollment interactions per month where consent is provided, but didn't result in a voiceprint being created. 

## Review authentication metrics

The **Authentication** tab shows how reliably and how quickly customers authenticate when they call your organization. Use it to track the caller experience and to identify authentication profiles that need tuning.

The tab presents the following metrics:

- **Authentication success rate**: The percentage of successful authentication as a function of all authentication attempts since the inception of the solution.
- **Total decisions**: The total number of authentication attempts.
- **Failed authentication**: The number of authentication failures.
- **Successful authentications**: The number of successful authentication attempts.
- **Average authentication time**: Elapsed time in seconds from when authentication is triggered and successful authentication decision is rendered.
- **Time-series Authentication success rate**: The percentage of successful authentications as a function of all authentication attempts per month.
- **Time-series Average authentication time**: The average monthly elapsed time in seconds from when authentication is triggered and successful authentication decision is rendered.
- **Time-series Successful authentications**: The number of successful authentication attempts per month.

## Review fraud detection metrics

The **Fraud Detection** tab shows the volume of fraud alerts and how accurately and thoroughly your team reviews them. Use it to measure fraud coverage and the quality of agent review.

The tab presents the following metrics:

- **Total fraud alerts**: The total number of fraud alerts raised.
- **Real-time fraud alerts**: The number of alerts raised in real time during a call over time. 
- **Percentage of alerts reviewed by Fraud analyst**: The share of alerts that an agent reviewed. 
- **Accuracy rate**: The percentage of alerts that were correct. 
-  **Real-time false fraud rate**: The percentage of false positives.

## Filter and refresh the data

Each tab supports the same filters, so you can narrow any report to a specific period or authentication profile and then update the values.

1. Select a **time frame** to limit the data to a specific period. 
1. Select an **authentication profile**, such as **business banking standard**, to see metrics for that profile only. 
1. Select **Refresh** to update the metrics and graphs with the current data. 

> [!NOTE]
> The filter selections persist across the three tabs when you switch tabs.

## Related information
- [Monitor and optimize system performance (preview)](../administer/monitor-optimize-system-performance.md)
- [Fraud detection overview (preview)](../administer/fraud-detection-overview.md)
- [Authenticate customers during a call (preview)](authenticate-customers-during-call.md)
- [Configure authentication profiles (preview)](../administer/configure-authentication-profiles.md)
