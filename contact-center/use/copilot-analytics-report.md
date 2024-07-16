---
title: View copilot analytics report
description: Learn how to view and understand Copilot metrics.
author: gandhamm 
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.date: 07/01/2024
ms.custom: bap-template 
ms.collection: bap-ai-copilot
---

# View copilot analytics report

> [!NOTE]
> The feature availability information is as follows.
>
> | Dynamics 365 Contact Center&mdash;embedded | Dynamics 365 Contact Center&mdash;standalone | 
> |----------|----------|
>  | No  | Yes   | 

Copilot helps agents to complete tasks related to conversations and email more easily. With the Copilot report, supervisors and customer service managers can identify the effect that Copilot is having across their customer service operation.


The system stores the copilot interaction data in the [msdyn_copilotinteraction](/dynamics365/customer-service/develop/reference/entities/msdyn_copilotinteraction), [msdyn_copilotinteractiondata](/dynamics365/customer-service/develop/reference/entitiesmsdyn_copilotinteractiondata), [msdyn_copilottranscript](/dynamics365/customer-service/develop/reference/entities/msdyn_copilottranscript), and [msdyn_copilottranscriptdata](/dynamics365/customer-service/develop/reference/entities/msdyn_copilottranscriptdata) tables. You can use the information to build custom metrics in reporting and analytics and understand how Copilot is being used in your organization.

To view the Copilot report, open Customer Service historical analytics and select the **Copilot** tab.

> [!NOTE]
> Case summary isn't available for the Contact Center embedded experience.

## Copilot report

You can use filters to focus on the information that's important to you:

- **Duration**: Filters the data by the selected value of day, week, or month.
- **Time zone**: Filters the data for the selected time zone.

The Copilot report displays the following metrics.

:::image type="content" source="../media/copilot-analytics-report.png" alt-text="A screenshot of the Copilot report for cases.":::

### Usage

| Metric | Description |
|--------|---------|
| Daily active users | The number of unique agents who used Copilot at least once in the last day |
| Total copilot AI responses | The total number of responses that Copilot provided |
| Number of responses used | The number of times that text from a copilot response was copied |
| Percentage of copilot AI responses used | The percentage of responses that were copied |

### Productivity: Conversations

| Metric | Description |
|--------|---------|
| Total conversations | The total number of conversations in which the agent engaged with the customer at least once while Copilot was available; doesn't include email and voice |
| Number of conversations using copilot AI | The number of engaged conversations that used Copilot; lists only conversations that have ended |
| Percentage of conversations using copilot AI | The percentage of engaged conversations that used Copilot |
| Avg conversation handle time | The average time that elapsed after a conversation started until it ended; displays data when Copilot was used and when it wasn't used |
| Conversation throughput | The number of conversations, excluding email and voice, completed on average per day; displays data when Copilot was used and when it wasn't used |

### Satisfaction

| Metric | Description |
| -------|---------|
| Agent ratings | The number of times agents rated a Copilot response positively or negatively |

## Next Steps

You can view the [transcripts of interactions]( /dynamics365/customer-service/develop/download-copilot-transcript-data?context=/dynamics365/contact-center/extend-context) between agents and Copilot. 

### Related information

[Use copilot features](use-copilot-features.md)  
[Configure copilot](../administer/configure-copilot-features.md)  