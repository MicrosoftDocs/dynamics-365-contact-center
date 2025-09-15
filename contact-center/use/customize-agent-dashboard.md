---
title: Customize the bot dashboard
description: Learn more about customizing bot dashboards with filters and metrics to meet your business requirements.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to
ms.collection: 
ms.date: 08/14/2025
ms.custom: bap-template 
---

# Customize the bot dashboard

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]


You can customize the out-of-the-box real-time and historical bot dashboards with more filters and metrics to effectively visualize your bot metrics. Learn more in [customize visual display](/dynamics365/customer-service/use/customize-reports).

 The table describes the filters and metrics that you can add to the bot dashboards to help visualize key performance indicators (KPI).

## Add filters

Perform the steps in [Add a filter to an entire page](/power-bi/create-reports/power-bi-report-add-filter?tabs=powerbi-desktop#add-a-filter-to-an-entire-page) to add the following filters to the bot dashboard.

| Title |   Definition | Applies to| Channel | Data |
| --------------- | --------------- |
| Dialed number identification service (DNIS) | Choose a customer-facing phone number from the list to see bot metrics for that number.<br> You can track call volumes for different campaigns or services, analyze marketing effectiveness, customize Interactive Voice Response (IVR) experiences, and generate detailed reports on call patterns, ultimately helping to optimize resource allocation and improve customer service. | Real time and historical| Voice only | DimPhoneNumber: DNIS |
| Language  | Filter and view bot metrics by the last language used.<br> This metric helps you understand your callers' language preferences and optimize multilingual support.<br> For example, a conversation can start in English before the customer switches to Spanish or a conversation begins and ends in Spanish. If you select Spanish as the last language, the report displays the metrics for all conversations that ended in Spanish. In our example, the dashboard displays metrics for both the conversations.<br>**Note**: In the real-time bot dashboard, setting the Last language filter displays metrics for conversations that were escalated to an agent or an external number and are in the closed state. The metrics aren't updated when the bot conversation is ongoing. | Real time and historical| Chat and voice | DimLanguage: Language |
| Browser  | Filter by browser to analyze the agent's metrics specifically for the selected browser. | Real time and historical| Chat and voice | FactLiveChatContext: Browser |
| Device  | Filter by device to analyze the agent's performance specifically for the selected device. | Real time and historical| Chat and voice | FactLiveChatContext: Device |

:::image type="content" source="../media/realtime-dashboard-mini.png" alt-text="Screenshot of real time bot dashboard with filters." lightbox="../media/oc-realtime-dashboard.png"::: 


## Add fallback action calls

Fallback actions track the number of conversations handled by the system when the AI agent encounters system failures, errors, or can't process user inputs. This prevents conversation breakdown and maintains user engagement.

Perform the steps in [Add visualizations to a report](/power-bi/visuals/power-bi-report-add-visualizations-i#add-visualizations-to-the-report) to represent **FactSession : Failed bot conversation** data in a [Single number card](/power-bi/visuals/power-bi-visualization-types-for-reports-and-q-and-a#single-number) visual for fallback action calls on the bot dashboard.

| Title |   Definition | Applies to | Channel | Data |
| --------------- | --------------- |
| Fallback action calls | The number of bot conversations where the bot applies one of the fallback actions in case of failures: <ul><li>**Prompt and hang-up**: The system plays a [default message](/dynamics365/customer-service/administer/configure-automated-message#preconfigured-automated-message-triggers) and ends the call.</li><li>**Prompt and transfer to external number**: The system plays the default message and transfers the call to an external number that you enter in the **External phone number** field. Use the E.164 format, with a plus sign (+) followed by the country code and phone number.</li><li>**Prompt and escalate**: The system plays the default message and connects the call to a service representative.</li><li>**Wait Music and Escalate**: The system plays wait music and connects the call to a service representative.</li></ul> Learn more in [Configure fallback actions for the IVR agent](/dynamics365/contact-center/administer/configure-fallback-actions-ivr-agent)| Real time and historical| Voice only | FactSession: Failed bot conversation|.

## Add bot session level outcome reason

Customer conversations with AI agents can have multiple sessions based on the topics discussed. Each session records both an outcome and an outcome reason that categorizes how the session ended. The outcome shows the overall result of the session. The outcome reason provides specific details about why the session ended.

Based on the value of **Type**, the following **Outcome** and **OutcomeReason** are set for the session:

- **Engaged**: 
 - If the session is engaged, the **Outcome** can be set to the following:
     - **Abandoned**
     - **HandOff**
     - **Resolved**

 - The corresponding **OutcomeReason** can be set to the following:
   - **SystemError**
   - **UserError**
   - **Resolved**
   - **UserExit**
   - **AgentTransferRequestedByUser**
   - **AgentTransferFromQuestionMaxAttempts**
   - **AgentTransferConfiguredByAuthor**. 
- **Unengaged**: Sessions start in an unengaged state and stay unengaged until user input is provided or the session enters custom or escalate topic modes. For unengaged sessions, the **Outcome** is  set to **None** and **OutcomeReason** is **NoError**.

Learn more in [Measuring agent engagement](/microsoft-copilot-studio/guidance/measuring-engagement#engaged-and-unengaged-analytics-sessions).

For example, a customer contacts support to check the order status. The customer also requests to place a new order. This single conversation generates two distinct sessions:
 - Session 1: Check order status with **Outcome** set to Resolved, **outcomeReason** set to Resolved
 - Session 2: Place a new order with **outcome** set to Abandoned, **outcomeReason** set to SystemError
 
Since the conversation generated custom topics, the engagement type is classified as **Engaged.**

Perform the steps in [add a matrix visualization](/power-bi/visuals/power-bi-visualization-matrix-visual#lets-create-a-matrix-visual) to represent **Session level outcome reason** in a matrix visual to view metrics by outcome reason for AI agents to the report.


| Session outcome| Engagement type| Outcome Reason                        | Definition                                                                                                              | Applies to  | Channel         | 
|----------------------------------------|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-----------------|-
|Abandoned | Engaged| UserExit                              | The number of conversations that end either because the customer ends the conversation or the session times out while waiting for the customer's response.                                                                                                                                                                                                                                                                                                                                | Historical  | Chat and voice  | 
|Handoff| Engaged| AgentTransferConfiguredByAuthor        | The number of bot conversations transferred to a service representative or external number based on the AI agent's configuration. For example, an AI agent flow includes "Transfer to an agent". When the user selects "No," the AI agent transfers the conversation without the user requesting escalation, per the AI agent's business rules.                                                                                                    | Historical  | Chat and voice  | 
|Handoff| Engaged | AgentTransferRequestedByUser           | The number of AI agent conversations escalated to a service representative or external number at the user's request.                                                                                                                                                                                                                                                                                                                               | Historical  | Chat and voice  | 
| Handoff | Engaged | AgentTransferFromQuestionMaxAttempts   | The number of agent conversations escalated to a service representative or external number after threshold limit reaches silence detection or when no valid entity is found.                                                                                                                                                                                                                                                               | Historical  | Chat and voice  | 
| Resolved       | Engaged                       | The number of bot conversations that the AI agent resolved.                                                                                                                                                                                                                                                                                                                                                                                        | Historical  | Chat and voice  |
|Abandoned| Engaged | UserError                             | The number of bot conversations that ended because of incorrect AI agent design.                                                                                                                                                                                                                                                                                                                                                                   | Historical  | Chat and voice  | 
|Abandoned| Engaged| SystemError                           | The number of AI agent conversations that ended due to systemic errors within Copilot Studio.                                                                                                                                                                                                                                                                                                                                                      | Historical  | Chat and voice  | 
| None | Unengaged | NoError                              | The number of conversations that didn't have any engagement with AI agents. This can happen when the customer doesn't respond to the AI agent's greeting or when the AI agent doesn't enter a custom topic or Escalate topic due to the structure of the conversation flow.                                                                                                                                                                                                                      | Historical  | Chat and voice  |

### Related information

[Bot dashboard](/dynamics365/customer-service/use/oc-bot-dashboard?context=/dynamics365/contact-center/use-context)   
[View and understand the bot report in Omnichannel real-time analytics](agent-realtime-dashboard.md)  
