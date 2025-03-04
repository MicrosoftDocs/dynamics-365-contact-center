---

title: Configure fallback actions for the IVR agent
description: Learn how to configure and manage fallback actions.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.date: 03/04/2025
ms.topic: how-to
ms.collection:
ms.custom: bap-template
---

# Configure fallback actions for the IVR agent

You can configure the AI agent (agent) to handle situations where the customer can't reach the Interactive Voice Response (IVR) agent or when there's a system or network failure. Instead of the call dropping abruptly, the IVR system informs the customer about the issue before hanging up or transferring them to a representative.

## Manage call fallback actions

To manage IVR agent call fallback, update the agent settings in the voice workstream as follows:

1. In the **Bot** section, select **Edit** to open the **Edit bot** pane. 
1. Choose one of options:
    - **Prompt and hang-up**: The system plays a [default message](/dynamics365/customer-service/administer/configure-automated-message#preconfigured-automated-message-triggers) and ends the call.
    - **Prompt and transfer to external number**: The system plays the default message and then transfers the call to an external number that you enter in the **External phone number** field. Use the E.164 format, with a plus sign (+) followed by the country code and phone number.
    - **Prompt and escalate**: The system plays the default message and then connects the call to an agent.
    - **Wait Music and Escalate**: The system plays wait music and then connects the call to an agent.
1.  Select **Save**. 

Instead of the default message, the system plays the [wait music](/dynamics365/customer-service/administer/voice-channel-music#add-hold-and-wait-music-to-the-workstream?context=/dynamics365/contact-center/context/administer-context) or [custom messages](/dynamics365/customer-service/administer/configure-automated-message?context=/dynamics365/contact-center/context/administer-context) if you have configured them.


## View failed calls for agents

You can use the out-of-the-box **Fallback calls** metric in the Omnichannel historical reports bot dashboard and Omnichannel real-time analytics report to view the number of conversations that were initiated by the customer but couldn't be connected due to system challenges. Learn more in [Customize the bot dashboard](../use/customize-agent-dashboard.md)
