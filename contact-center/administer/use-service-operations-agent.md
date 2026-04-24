---
title: Use Service Operations Agent in Dynamics 365 Contact Center (preview)
description: Learn about Service Operations Agent and how you can use it to configure and administer features in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 04/24/2026
ms.topic: how-to
---

# Use Service Operations Agent (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Service Operations Agent in Dynamics 365 Contact Center is a self-service AI agent that supports administrators with configuration, validation, and troubleshooting tasks. The agent helps streamline onboarding and ongoing maintenance, making administrator workflows more efficient.

Service Operations Agent supports conversational setup of Dataverse tables such as queues and workstreams.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

> [!NOTE]
> Service Operations Agent is only available in the United States and in English.

## Supported capabilities

**Configure channels**

- Help set up channels and workstreams.
- Sync phone numbers with Azure Communication Services and Teams.
- Provide guidance on best practices for contact center configuration.

**Manage queues**

- Assign users to specific queues.
- Create skills and assign them to users.
- Check queue details.
- Set up operating hours.

**Query capabilities and troubleshoot issues**

- Query the agent about contact center capabilities.
- Questions about the environment
- Diagnostics for supported channels

## Prerequisites

- Omnichannel administrator role
- The Power Platform [Pay-as-you-go plan](/power-platform/admin/pay-as-you-go-overview) mandates the usage of an Azure subscription the system charges when the agent runs. Make sure you [Set up consumption-based billing](/dynamics365/customer-service/administer/setup-pay-as-you-go).
- For Service Operations Agent to troubleshooting issues during set up:
  - [Application Insights is configured](/azure/azure-monitor/app/create-workspace-resource?tabs=portal#create-an-application-insights-resource)
  - [Application Insights is connected with Dynamics 365 Contact Center](/power-platform/admin/conversation-diagnostics-application-insights#set-up-a-connection-with-azure-application-insights)

## Conversational setup

Use natural language to set up your contact center, and watch your Service Operations Agent run the steps while keeping a human in the loop.

### Steps to access

In Copilot Service admin center, select **Launch** in the **Conversational Setup** tile. The **Service Operations Agent (Preview)** page appears. As a one-time authorization, it asks you to connect to Dataverse via the MCP server. Select **Allow once**.

### Examples 

We recommend using clear, detailed prompts and explicitly specifying the relevant channel or topic to reduce the risk of inaccurate or unreliable answers. The following are a few examples of prompts.

**Configuration and setup**

- Can you help me create a voice workstream?
- Please create a voice workstream with the name `<Insert Name>` and use the `<Queue name\>`queue as the default queue.

**Queue Management**

- Which voice queues are available?
- Which queues aren't connected to workstreams?

**Knowledge and troubleshooting**

- Is there an active Azure Communication Services resource in this organization?
- List the phone numbers associated with the Azure Communication Services resource.
- What is my organization ID?

### Related information

[Overview of autonomous service agents](autonomous-agents-overview.md)   
[Customer Intent Agent](overview-customer-intent-agent.md)   