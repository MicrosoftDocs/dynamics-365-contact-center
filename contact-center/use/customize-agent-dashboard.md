---
title: Customize the bot dashboard
description: Learn more about customizing bot dashboards with additional filters and metrics to meet your business requirements.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: conceptual 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---

# Customize the bot dashboard

You can customize the out-of-the-box realtime and historical bot dashboards with additional filters and metrics to effectively visualize your bot metrics. Learn more at [customize visual display](/dynamics365/customer-service/use/customize-reports)

 The table describes the filters and metrics that you can add to the bot dashboards to help visualize key performance indicators(KPI).

## Filters

Perform the steps in [Add a filter to an entire page](/power-bi/create-reports/power-bi-report-add-filter?tabs=powerbi-desktop#add-a-filter-to-an-entire-page) to add the following filters to the bot dashboard.

| Title |   Definition | Applicable to | Channel | Data |
| --------------- | --------------- |
| Dialed number identification service (DNIS) | Choose a customer-facing phone number from the list to see bot metrics for that number.<br> You can track call volumes for different campaigns or services, analyze marketing effectiveness, customize IVR experiences, and generate detailed reports on call patterns, ultimately helping to optimize resource allocation and improve customer service. | Real time and historical| Voice only | DimPhoneNumber: DNIS |
| Last language  | Filter and view bot metrics by the last language used.<br> This metric helps you understand your callers' language preferences and optimize multilingual support.<br> For example, a conversation can start in English before the customer switches to Spanish or a conversation begins and ends in Spanish. If you select Spanish as the last language, the report displays the metrics for all conversations that ended in Spanish. In our example, the dashboard displays metrics for both the conversations.<br>**Note**: In the real-time bot dashboard, setting the Last language filter displays metrics for conversations that were escalated to an agent or an external number and are in the closed state. The metrics aren't updated when the bot conversation is ongoing. | Real time and historical| Chat and voice | DimLanguage: Language |

## Failed calls

Perform the steps in [Add visualizations to a report](/power-bi/visuals/power-bi-report-add-visualizations-i#add-visualizations-to-the-report) to represent **FactSession : Failed bot conversation** data in a [Single number card](/power-bi/visuals/power-bi-visualization-types-for-reports-and-q-and-a#single-number) visual for failed calls to the bot dashboard.

| Title |   Definition | Applicable to | Channel | Data |
| --------------- | --------------- |
| Failed calls | The number of conversations that were initiated by the customer but couldn't be connected to a bot due to a system failure. The application registers a call only after the classification rules in the workstream run and the work distribution system routes the call to the bot. This indicates that a bot was assigned to the call. Calls that fail before this step don't appear on the dashboard.| Real time and historical| Chat and voice | FactSession : Failed bot conversation|

## Outcome reason

Perform the steps in [add a matrix visualization](/power-bi/visuals/power-bi-visualization-matrix-visual#lets-create-a-matrix-visual) to represent **Outcome reason** in a matrix visual to view metrics by outcome reason for bots to the report.

| Title |   Definition | Applicable to | Channel | Data |
| --------------- | --------------- |
|  Metrics by outcome reason|  The number of engaged conversations grouped by the outcome reason. <br><ul><li>**User exit**: The number of conversations that end either because the customer ends the conversation or the session times out while waiting for the customer's response.</li> <li> **AgentTransferConfiguredByAuthor**: The number of bot conversations transferred to an agent or external number based on the bot's configuration. For example, if a topic ends with "Transfer to an agent" when the user selects "No," the bot will transfer the conversation without the user requesting escalation, per the bot's business rules.</li><li>**Resolved**: The number of bot conversations that were resolved by the bot. </li><li>**User error**: The number of bot conversations that ended because of incorrect bot design.</li></ul> | Historical | Chat and voice | Outcome reason |