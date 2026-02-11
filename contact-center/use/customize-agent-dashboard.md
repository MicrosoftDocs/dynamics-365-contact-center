---
title: Customize the bot dashboard
description: Learn more about customizing bot dashboards with filters and metrics to meet your business requirements.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection: 
ms.date: 02/11/2026
ms.custom: bap-template 
---

# Customize the bot dashboard

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]


You can customize the out-of-the-box real-time and historical bot dashboards with more filters and metrics to effectively visualize your bot metrics. For example, perform the steps in [customize visual display](/dynamics365/customer-service/use/customize-reports) to represent **FactSessiontable** data in a visual to show transferred bot conversations.

The table describes the filters and metrics that you can add to the bot dashboards to help visualize key performance indicators (KPI).

## Add filters

Perform the steps in [Add a filter to an entire page](/power-bi/create-reports/power-bi-report-add-filter?tabs=powerbi-desktop#add-a-filter-to-an-entire-page) to add the following filters to the bot dashboard.

| Title |   Definition | Applies to| Channel | Data |
| --------------- | --------------- |------|---------|---------|
| Dialed number identification service (DNIS) | Choose a customer-facing phone number from the list to see bot metrics for that number.<br> You can track call volumes for different campaigns or services, analyze marketing effectiveness, customize Interactive Voice Response (IVR) experiences, and generate detailed reports on call patterns, ultimately helping to optimize resource allocation and improve customer service. | Real time and historical| Voice only | DimPhoneNumber: DNIS |
| Language  | Filter and view bot metrics by the last language used.<br> This metric helps you understand your callers' language preferences and optimize multilingual support.<br> For example, a conversation can start in English before the customer switches to Spanish or a conversation begins and ends in Spanish. If you select Spanish as the last language, the report displays the metrics for all conversations that ended in Spanish. In our example, the dashboard displays metrics for both the conversations.<br>**Note**: In the real-time bot dashboard, setting the Last language filter displays metrics for conversations that were escalated to an agent or an external number and are in the closed state. The metrics aren't updated when the bot conversation is ongoing. | Real time and historical| Chat and voice | DimLanguage: Language |
| Browser  | Filter by browser to analyze the agent's metrics specifically for the selected browser. | Real time and historical| Chat and voice | FactLiveChatContext: Browser |
| Device  | Filter by device to analyze the agent's performance specifically for the selected device. | Real time and historical| Chat and voice | FactLiveChatContext: Device |

:::image type="content" source="../media/realtime-dashboard-mini.png" alt-text="Screenshot of real time bot dashboard with filters." lightbox="../media/oc-realtime-dashboard.png"::: 


## Add fallback action calls

Fallback actions track the number of conversations handled by the system when the AI agent encounters system failures, errors, or can't process user inputs. This prevents conversation breakdown and maintains user engagement.

Perform the steps in [Add visualizations to a report](/power-bi/visuals/power-bi-report-add-visualizations-i#add-visualizations-to-the-report) to represent **FactSession: Failed bot conversation** data in a [Single number card](/power-bi/visuals/power-bi-visualization-types-for-reports-and-q-and-a#single-number) visual for fallback action calls on the bot dashboard.


| Title | Definition | Applies to | Channel | Data |
|-------|------------|------------|---------|------|
| Fallback action calls | The number of bot conversations where the bot applies one of the fallback actions in case of failures:<br><br>• **Prompt and hang-up**: The system plays a [default message](/dynamics365/customer-service/administer/configure-automated-message#preconfigured-automated-message-triggers) and ends the call.<br><br>• **Prompt and transfer to external number**: The system plays the default message and transfers the call to an external number that you enter in the **External phone number** field. Use the E.164 format, with a plus sign (+) followed by the country code and phone number.<br><br>• **Prompt and escalate**: The system plays the default message and connects the call to a service representative.<br><br>• **Wait Music and Escalate**: The system plays wait music and connects the call to a service representative.<br><br>Learn more in [Configure fallback actions for the IVR agent](/dynamics365/contact-center/administer/configure-fallback-actions-ivr-agent) | Real time and historical | Voice only | FactSession: Failed bot conversation |

## Analyze conversation fallout patterns

To analyze conversation fallout patterns, it’s essential to identify the exact point in the dialogue where the fallout occurred. For example, whether it was after intent identification or before the resolution. More details, such as topic, node, speech recognition confidence score, and input mode, should also be logged in the conversation transcript stored in Dataverse.

Administrators in Microsoft Copilot Studio must enable the option to log node-level details into the conversationTranscript JSON file. This file is stored in Dataverse and supports visual customization and data measures on the Omnichannel Historical Bot dashboard. 

:::image type="content" source="../media/node-level-detail-for-custom-variables.png" alt-text="Screenshot showing node-level detail logging enabled for conversation transcripts." lightbox="../media/node-level-detail-for-custom-variables.png":::

### Steps to create custom reports for conversation fallouts

1. In Copilot Service workspace, go to **Omnichannel historical analytics** > **Bot**.
1. Select **Edit report**. This opens the full report where you can view available data measures, tables, and filters.
1. At the bottom of the report’s page list, select the **PVA Topic Detail** tab to work with topic and node‑level data.
1. In the **Data** pane, find the table named **FactBotSessionNodedetail**. This table contains [Question node-level metrics](/dynamics365/customer-service/use/oob-data-models#data-dictionary-4) that track outcomes at each node in the conversation flow. Currently, only question nodes support fallout patterns.
1. Review available fields such as **NodeName**, **AbandonedCount**, and **SuccessCount**.
1. Add a new **Table** visual or select an existing one.
1. Drag **NodeName** to the **Rows** field.
1. Drag metrics such as **AbandonedCount** or **SuccessCount** into the **Columns** or **Values** field, depending on your preferred view.
1. Select **Save**. Wait 1–2 minutes for changes to sync.
1. Select **Publish** to make the report available to viewers.

#### Best practices for using question nodes

- Create custom visualization to show question nodes and their corresponding outcomes, successes, or failures.
- To accurately report success and failure rates for question nodes, rename the default question node in Microsoft Copilot Studio Canvas. Use clear and meaningful names to ensure that dashboards display actionable insights and make it easier to track where breakdowns occur in the conversation flow. This practice supports performance improvements and a better user experience. Examples of effective names include Confirm Order Status, Repeat Account Number, or Repeat Main Menu Options. If the node isn’t renamed, default ambiguous names like Question_eQt5ye appear, making reports harder to interpret.

## Use custom reporting variables

This feature works with classic Copilot Studio bots that require custom variables to tag conversations. Add reporting variables configured in Microsoft Copilot Studio Canvas to enable organized tracking and analysis across key organizational dimensions such as line of business, division, product line, and other custom-defined attributes. Learn more in [Work with variables](/microsoft-copilot-studio/authoring-variables?tabs=webApp). The variables are linked to certain topics and flows, and their use depends on how topics and flows are configured in the Microsoft Copilot Studio Canvas.

You need to [enable advanced historical analytics for voice and chat Copilot agents](/dynamics365/customer-service/administer/oc-historical-analytics-reports#enable-advanced-historical-analytics-for-voice-and-chat-copilot-agents). You can add up to 15 variables across all voice and chat agents used in your organization. 

Once configured, the Omnichannel Historical Bot dashboard can be customized with these user-defined dimensions and metrics, enabling granular analysis of key indicators such as deflection, escalation rate, and containment. This flexibility aligns reporting with organizational goals and eliminates manual parsing of conversation data.

Additionally, you can analyze exit patterns from question nodes and identify root causes of escalations originating from those nodes, providing advanced troubleshooting and diagnostic insights. 

The following example shows how reporting variables are processed and surfaced in analytics. Variables like msdyn_rvSelfServiceStart and msdyn_rvFinalIntent can be configured in Microsoft Copilot Studio Canvas. Based on the conversation flow, the final value of these variables is processed and displayed in the Omnichannel Historical dashboard for visual and data model customization. This information helps create custom reports on intent determination and self-service process status.

:::image type="content" source="../media/variables.png" alt-text="Screenshot showing global reporting variables configured in Microsoft Copilot Studio Canvas." lightbox="../media/variables.png":::

### Best practices for custom variables

- Use the same custom variable name defined in Microsoft Copilot Studio when configuring the Omnichannel Historical Bot dashboard.
- Limit variable values to one or two words. Avoid long descriptive text, as it can impact dashboard performance.
-  For scenarios like business units, use a single variable name. For example, Contoso_Business_Units. The variable can hold multiple values. When a conversation flow passes through a topic related to one of these units, then the variable is assigned or updated. If applied multiple times, only the final value is captured and displayed in the Omnichannel Historical dashboard through visuals or data model customization.

### Related information

[Bot dashboard](/dynamics365/customer-service/use/oc-bot-dashboard?context=/dynamics365/contact-center/use-context)   
[View and understand the bot report in Omnichannel real-time analytics](agent-realtime-dashboard.md)  
