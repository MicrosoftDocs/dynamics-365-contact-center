---
title: Use the real-time adherence tracker
description: Learn how to use the real-time adherence tracker to maintain service levels and operational efficiency for your business.
author: gopalyuvaraj
ms.author: gopalyuvaraj
ms.reviewer: laalexan
ms.topic: how-to
ms.collection:
ms.date: 09/14/2026
ms.custom: bap-template
---

# Use the adherence tracker

## Overview

The adherence tracker helps supervisors monitor the activities of customer service representatives (service representatives or representatives) against their scheduled shifts in real time. This tracker enables the early detection of adherence deviations, so supervisors can take proactive actions to maintain service levels and operational efficiency.

Use the adherence tracker to ensure that service representatives are where they need to be—whether working queues, on break, or attending training sessions—according to the planned schedule.

## Prerequisites

Your administrator installed the [Workforce Management for Customer Service package](../administer/workforce-management-package-installation.md) in the Power Platform admin center app, and then enabled the feature in Copilot Service admin center.

## Access the real-time adherence tracker

In the site map of Copilot Service workspace, go to **Workforce management**, and then select **Adherence tracker**. The **Adherence tracker** page appears.

## Use tracker filters

Use the filters at the top of the tracker to narrow the view.

| Filter | Description |
|---|---|
| **Time zone** | Displays scheduled and actual activity times in the selected time zone. |
| **Planning group** | Displays shift plans associated with the selected planning group. Select **Not applicable** to display shift plans that aren't associated with a planning group. |
| **Shift plan** | Displays representatives associated with the selected shift plan. |

## Real-time adherence views

| Section | Description |
|---|---|
| **Service representative list** | Lists all service representatives scheduled for the shift plan, along with their current state—for example, Available, On break, or In training—**Time in state (mins)**, and **Total scheduled time (mins)**. |
| **Adherence Gantt chart** | Displays each representative's actual activities compared with their scheduled activities on a visual timeline. Out-of-adherence time periods are highlighted as separate segments. |
| **Adherence summary metrics** | Provides key team metrics such as overall adherence percentage, total scheduled time, and total time out of adherence. |

## Related information

[Use planning groups](workforce-management-use-planning-groups.md)  
[Use the adherence history report](workforce-management-use-adherence-history-report.md)  
[Configure shift activity types](../administer/workforce-management-shift-activity-types.md)

