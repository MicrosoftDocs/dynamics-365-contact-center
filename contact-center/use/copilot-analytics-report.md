---
title: View Copilot analytics report
description: Learn how to access and interpret the Copilot analytics report in Dynamics 365 Customer Service.
author: gandhamm 
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.date: 12/09/2025
ms.update-cycle: 180-days
ms.custom: bap-template 
ms.collection: bap-ai-copilot
---

# View Copilot analytics report

> [!NOTE]
> The feature availability information is as follows.
>
> | Dynamics 365 Contact Center&mdash;embedded | Dynamics 365 Contact Center&mdash;standalone |
> |----------|----------|
>  | No  | Yes   |

Copilot enables customer service representatives (service representatives or representatives) to efficiently complete tasks related to conversations and email. With the Copilot report, supervisors and customer service managers can identify the effect that Copilot has across their customer service operation.

The system stores the Copilot interaction data in the [msdyn_copilotinteraction](/dynamics365/customer-service/develop/reference/entities/msdyn_copilotinteraction), [msdyn_copilotinteractiondata](/dynamics365/customer-service/develop/reference/entities/msdyn_copilotinteractiondata), [msdyn_copilottranscript](/dynamics365/customer-service/develop/reference/entities/msdyn_copilottranscript), and [msdyn_copilottranscriptdata](/dynamics365/customer-service/develop/reference/entities/msdyn_copilottranscriptdata) tables. You can use the information to build custom metrics in reporting and analytics and understand how your organization is using Copilot.

### Access the report

To view the Copilot analytics report, users must have a security role with Read privileges on the Copilot Analytics entity (msdyn_dataanalyticsreport_copilot). By default, System Administrator and Supervisor roles can access analytics. Administrators can grant access to other users by creating or editing a role in Power Platform admin center and adding Read permissions for the analytics entities. Learn more in [Configure user access to analytics and dashboards](/dynamics365/customer-service/administer/configure-customer-service-analytics-insights-csh).

Your administrator must enable Copilot analytics in the Copilot Service admin center app. Learn more in [Manage Copilot analytics](/dynamics365/customer-service/administer/copilot-analytics).

To view the Copilot report, select **Copilot analytics** from the Copilot Service workspace menu.

> [!NOTE]
> Case summary isn't available for the Contact Center embedded experience.

## Copilot report filters and metrics

You can use filters to focus on the information that's important to you:

- **Duration**: Filters the data by the selected value of day, week, or month.
- **Time zone**: Filters the data for the selected time zone.

The Copilot report displays the following metrics.

:::image type="content" source="../media/copilot-analytics-report.png" alt-text="A screenshot of the Copilot report for cases.":::

### Usage

| Metric | Description |
|--------|---------|
| Daily active users | The number of unique service representatives who used Copilot at least once in the last day. |
| Total Copilot AI responses | The total number of responses that Copilot provided. |
| Number of responses used | The number of times that text from a Copilot response was copied. |
| Percentage of Copilot AI responses used | The percentage of responses that were copied. |

### Productivity: Conversations

| Metric | Description |
|--------|---------|
| Total conversations | The total number of conversations in which the service representative engaged with the customer at least once while Copilot was available; doesn't include email and voice. |
| Number of conversations using Copilot AI | The number of engaged conversations that used Copilot; lists only conversations that have ended. |
| Percentage of conversations using Copilot AI | The percentage of engaged conversations that used Copilot. |
| Avg conversation handle time | The average time that elapsed after a conversation started until it ended. Displays data about when Copilot was used and when it wasn't used. |
| Conversation throughput | The number of conversations, excluding email and voice, completed on average per day. Displays data about when Copilot was used and when it wasn't used. |

### Satisfaction

| Metric | Description |
| -------|---------|
| Agent ratings | The number of times service representatives rated a Copilot response positively or negatively. |

## Next Steps

You can view the [transcripts of interactions]( /dynamics365/customer-service/develop/download-copilot-transcript-data?context=/dynamics365/contact-center/extend-context) between service representatives and Copilot.

### Related information

[Manage Copilot features](../administer/configure-copilot-features.md)  
