---
title: Use Copilot to summarize cases and conversations
description: Learn how agents can use Copilot to get cases and conversation summaries in Dynamics 365 Contact Center.
author: gandhamm 
ms.author: mgandham 
ms.reviewer: neeranelli 
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 07/01/2024
ms.custom: bap-template 
---

# Summarize cases in non-Microsoft CRMs

[!INCLUDE[cc-feature-availability-embed-only](../includes/cc-feature-availability-embed-only.md)]

Copilot case summaries help you quickly understand the context of a case and resolve customer issues more efficiently. In a non-Microsft CRM, the case summary appears as a card on the **Ask a question** tab in the Copilot help pane. 

> [!IMPORTANT]
> - Case summary is a preview feature in Microsoft 365 Copilot for Service.
> - Preview features aren’t meant for production use and might have restricted functionality. These features are available before an official release so that customers can get early access and provide feedback.

## Navigation

When you sign in to a non-Microsoft CRM, you can generate case summary as follows:
   - Launch the embedded experience and then login to your Dynamics account.
   - In the Copilot help pane that appears, select **Ask a question**.
   - Select the Copilot icon and then then select **Summarize case**.

## Generate case summaries

Copilot generates case summaries based on the following case information for the corresponding CRMs:

**Salesforce**: Copilot generates the case summary based on the case fields and activities associated with the case. The case summary includes the following information:

  - **Case fields**: case ID, description, subject, priority, type, customer name, case URL, email, and product name if the service representative has access.
  - **Text post**: ID, Title, body, createddate
  - **Comment**: Id, body, createddate
  - **Email**: ID, body, lastmodifieddate, fromaddress, toaddress.

**ServiceNow**: Copilot generates the case summary based on the incident data and activities that are attached with the incident. The case summary includes the following information:

 - **Incident data** : incident ID, description, short description, priority, type, customer name, incident URL, email, and notes.
 - **Work notes and comments**: ID, TextContext, Created Date.
 - **Email**: Id, Body, Created Date, FromAddress, ToAddress

In the non-Microsoft CRM, you can generate the case summary as follows:

- Select the required case or incident.
- Select **Microsoft contact center**. The Copilot help pane appears.
- In the **Ask a question** tab, select **Summarize case**. The case summary appears in the help pane.

You can copy the summary, refresh it, and provide feedback.

## Next steps

[Use Copilot to solve customer issues](use-copilot-features.md)  

