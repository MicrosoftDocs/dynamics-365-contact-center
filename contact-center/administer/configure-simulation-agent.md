---
title: Use AI-generated conversations for agentic simulations in Dynamics 365 Contact Center (preview)
description: Simulate your AI agents in Dynamics 365 Contact Center to validate routing. Ensure accurate voice call handling by running natural language prompts.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 06/23/2026
ms.topic: how-to
ms.collection: bap-ai-copilot
---

# Use AI-generated conversations for agentic simulations (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Agentic simulations help your administrators test and validate configurations, AI agents, and routing flows before they roll out in real time. Business users can describe the simulation they want to run by using natural language prompts.

In preview release, simulations are available for the inbound workstreams of the voice channel only.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- System administrator or Omnichannel administrator.

- Voice channel is [provisioned](../implement/provision-channels.md).

- [Phone number is configured for simulation](/dynamics365/customer-service/administer/voice-channel-inbound-calling?tabs=enhancedvoice).

> [!NOTE]
> Each simulation of three minutes consumes about 40 Microsoft Copilot Studio AI credits. The number of credits can vary depending on the speed or complexity of the dialogues used in the simulated conversations. Learn about credit consumption in [View credit capacity consumed per environment](/power-platform/admin/manage-copilot-studio-messages-capacity#view-credit-capacity-consumed-per-environment). The consumption information is listed under the entry **D365 Contact Center Agentic Simulation** in Power Platform admin center.

## Run a simulation

1. In Copilot Service admin center, on the Home page, select **Launch** on the **Agentic Simulation** tile.

1. On the page that appears, enter a natural language prompt or select a prompt in the prompt library to run a simulation. The prompt library is grouped into suggested, saved, and recent prompts. The simulation process starts. If there's an issue with the prompt, the tool displays the error or asks clarifying questions.

   :::image type="content" source="../media/simulation-page.png" alt-text="Screenshot of the Agentic Simulations page displaying prompt validation and a results pane with metrics like total conversations and average sentiment." lightbox="../media/simulation-page.png":::

1. While the simulation is running, you can view the conversations in the [**Ongoing conversation**](/dynamics365/customer-service/use/realtime-ongoing) report.

1. Use the **Simulation Run History** page to view the simulation results, such as the prompt used, status of the run, and completed runs.

1. View [transcripts and recordings](/dynamics365/customer-service/use/voice-channel-call-recordings-transcripts) in the closed conversation form.

   :::image type="content" source="../media/simulation-run-history.png" alt-text="Screenshot of a table in the Simulation Run History page listing completed runs and their associated metrics." lightbox="../media/simulation-run-history.png":::

## Things to consider

- To run the simulation, in the input prompt, the administrator must provide the phone number associated with the workstream that is intended to receive the incoming call. The caller number of the simulated voice call is a default number for each region and the simulation agent takes care of it.

- A simulation prompt can request up to five conversations. The system can simulate up to two call conversations concurrently.
- For a realistic simulation, configure representatives and routing rules appropriately to handle the simulated calls that you run.
- Simulations are in the English language only.
- A notification timer runs as per the notification template setting.
- Unaccepted calls end after five minutes.
- Maximum allowed duration of the accepted simulated calls is five minutes.
- You can initiate and run one simulation only at a time in one org.
- Dual-tone multi-frequency (DTMF) functionality isn't supported.

### Related information

[Overview of contact center agents](overview-contact-center-agents.md)  
[Use Service Operations Agent](use-service-operations-agent.md)  