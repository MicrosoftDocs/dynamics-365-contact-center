---
title: Use industry templates to set up a contact center (preview)
description: Set up an AI-first contact center quickly using industry templates in Service Operations Agent. Discover the steps to automate configuration and run simulations.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.date: 07/29/2026
ms.topic: how-to
ms.collection: bap-ai-copilot
---

# Use industry templates to set up a contact center (preview)

[!INCLUDE [preview-banner](~/../shared-content/shared/preview-includes/preview-banner.md)]

Industry templates in Service Operations Agent help administrators set up an AI-first contact center by using a guided template experience. Administrators can use the industry-template experience for retail and telecom. The setup flow reduces manual configuration across multiple contact center components, such as workstreams, knowledge, real-time voice agent capabilities, and simulation readiness.

Use an industry template when you want a faster path from environment setup to validation. Instead of configuring each component separately, select an industry template and phone number, start the transformation, track setup progress, and run simulations to validate the configured experience.

[!INCLUDE [preview-note](~/../shared-content/shared/preview-includes/preview-note-d365.md)]

## Prerequisites

- [Voice channel](..\implement\provision-channels.md) is provisioned.

- [Phone number is configured](/dynamics365/customer-service/administer/voice-channel-inbound-calling).
- Make sure that the contact center environment is ready for the capabilities that the template provisions, such as phone-number selection, workstreams, knowledge, real-time voice agents, and [simulations](configure-simulation-agent.md).

> [!IMPORTANT]
> The Power Platform [Pay-as-you-go plan](/power-platform/admin/pay-as-you-go-overview) requires the use of an Azure subscription that the system charges when the agent runs. Make sure that you [set up consumption-based billing](/dynamics365/customer-service/administer/setup-pay-as-you-go). Each industry template-based setup run consumes up to eight Microsoft Copilot Studio AI credits. Post setup, the use of the [real-time voice agent](/microsoft-copilot-studio/voice-realtime-voice-agents) and [simulation](configure-simulation-agent.md) incurs extra credits and varies depending on the speed or complexity of the dialogues. Learn about credit consumption in [View credit capacity consumed per environment](/power-platform/admin/manage-copilot-studio-messages-capacity#view-credit-capacity-consumed-per-environment).

## How industry template setup works

Industry template setup uses agentic transformation, a prompt-based setup experience that provisions an AI-first contact center in a guided flow.

The setup flow includes the following stages:

1. **Select an industry template**: Choose **Retail** or **Telecom**.

1. **Choose a phone number**: Select the phone number for the configured experience to use.
1. **Start transformation**: Service Operations Agent provisions the required contact center configuration.
1. **Track setup status**: Backend orchestration completes setup stages and tracks status centrally.
1. **Validate with simulation**: Run simulated calls after setup to verify that the configuration works as expected.

## Use industry template in Service Operations Agent

1. On the home page of Copilot Service admin center, select **Launch** on the **Industry template** tile. Service Operations Agent opens with a default prompt **Setup my contact center using default configurations**.

1. Select the industry template that matches your requirement, and select **Continue**.
1. Select the phone number to use in the setup and select **Submit**. The wizard displays the status of the set up and the features it configures.

   > [!NOTE]
   >
   > - The system creates a new workstream, detaches the selected phone number from the existing workstream settings, and attaches it to the new workstream. 
   > - If you see an error message like "LatestPublishedVersionNotFound", in Copilot Studio, go to **Transformation Agent Chat Bot** and republish the agent.

1. After the setup is complete, run the simulation to test your contact center.
1. You can place a voice call to the number that you set up to experience the behavior of the real-time voice agent.

### Related information

[Overview of Service Operations Agent](overview-service-operations-agent.md)  
[Responsbile AI FAQ for Service Operations Agent](../implement/service-operations-agent-rai-faq.md)  
