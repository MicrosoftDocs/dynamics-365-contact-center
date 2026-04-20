---
title: Use Service Operations Agent in Dynamics 365 Contact Center (preview)
description: Learn about Service Operations Agent and how you can use it to configure and administer features in Dynamics 365 Contact Center
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 04/20/2026
ms.topic: how-to
---

# Use Service Operations Agent (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Service Operations Agent is a self-service AI agent designed to support adminisrator users in Dynamics 365 Contact Center with configuration, validation, and troubleshooting tasks. It helps streamline onboarding and ongoing maintenance, making administrator workflows more efficient.

Service Operations Agent supports conversational setup of Dataverse tables such as queues and workstreams and builds a fully autonomous contact center for selected industries. It also lets you perform limited simulations.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

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

**Manage knowledge and troubleshoot issues**

- Query the agent about contact center capabilities

- Questions about the environment

- Diagnostics for supported channels

## Prerequisites

- Omnichannel administrator role

- For Service Operations Agent to troubleshooting issues during set up:
  - [Application Insights is configured](/azure/azure-monitor/app/create-workspace-resource?tabs=portal#create-an-application-insights-resource)
  - [Application Insights is connected with Dynamics 365 Contact Center](/power-platform/admin/conversation-diagnostics-application-insights#set-up-a-connection-with-azure-application-insights)
  - Monitoring Reader role to your app to access Application Insights data.

## Conversational setup

Use natural language to set up your contact center, and watch your Service Operations Agent run the steps while keeping a human in the loop.

### Steps to access

In Copilot Service admin center, select **Launch** in the **Conversational Setup** tile. The **Service Operations Agent (Preview)** page appears. As a one-time authorization, it asks you to connect to Dataverse via the MCP server. Select **Allow once**.

### Troubleshoot

If you ask the agent to create entities such as queues and workstreams, and the agent says it can’t create the queue but provides instructions, that means the MCP server connection isn’t set up properly. Go to Copilot Studio and open the agent. Under Tools, ensure the connection is set up correctly. The connection should be set to an admin user, instead of “D365 Contact Center Admin MCP”.

1. If the admin user connection is selected, but the issue is persisting, you can try deleting the “D365 Contact Center Admin MCP” connection in the Make Power Apps portal

1. Find and open the “D365 Contact Center Admin AI Agent” in Microsoft Copilot Studio agent list. On the right panel, we can send test messages to this copilot. Please click the “···”, then enable “Show activity map when testing”. Then on the left panel, we can see the activity map. It shows the details of each activity. If there are any issues, please share the error details from activity map.

1. Providing clear, detailed prompts to the agent helps reduce the risk of inaccurate or unreliable answers. We recommend specifying the relevant channel or topic clearly in the prompt. See examples below.

Configuration and setup

- Can you help me create a voice workstream?

- Please create a voice workstream with the name `<Insert Name>` and use the `<Queue name\>`queue as the default queue.

Queue Management

- Which voice queues are available?

- Which queues are not connected to workstreams?

Knowledge and troubleshooting

- Is there an active Azure Communication Services resource in this organization?

- List the phone numbers associated with the Azure Communication Services resource.

- What is my organization ID?

### Related information
