---
title: Configure agents for AI led proactive engagement
description: Learn how to configure agents for AI led proactive engagement including answering machine detection in Dynamics 365 Contact Center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 03/31/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Configure agents for AI-led proactive engagement


## Detect answering machines

Detection of answering machines is a technology used in telecommunication systems to determine whether a call is answered by a human or an answering machine. Set up the answering machine detection system topic in Copilot Studio to use when you're making outbound voice calls.

### Prerequisite

[Voice is enabled in Copilot Studio](/microsoft-copilot-studio/voice-get-started) or use the voice IVR template to access the answering machine detection system topic.

### Configure answering machine detection system topic

Choose to enable or disable detection of the answering machine. When enabled, the system automatically detects answering machines and proceeds with the configured message flow.

1. Enable the system topic **Answering machine detection**.
1. Select the system topic, and add the node to play the desired message. You can personalize the message based on the context of proactive engagement passed to the IVR agent. If you need to, you can choose to end the call instead of playing the message.

## Pass context to IVR agent

You can pass customer and campaign context to your IVR agent so that it can personalize the conversation. Some data is available out of the box in [context variables for agents in Copilot Studio](/dynamics365/customer-service/administer/context-variables-for-bot#context-variables-for-copilot-agents).

1. Pass the context as input attributes using [CCaaS API](../extend/api/ccaas_createproactivevoicedelivery.md) or as additional columns in a [file upload](configure-proactive-engagement.md#file-upload). All input parameters are added to the conversation context when a delivery is promoted to a conversation.

1. Create a context variable on the outbound workstream that matches the attribute name exactly. For example, if you pass an attribute called `CustomerID`, make sure the context variable is named `CustomerID`. Learn more in [Manage context variables](/dynamics365/customer-service/administer/manage-context-variables?context=/dynamics365/contact-center/context/administer-context).

1. To have your Copilot agent read context variables from Dynamics 365 Contact Center, complete the following steps:

   1. On the **Topics** page, select **Add a topic** > **from blank**. Use a topic that isn't invoked preferably.
   1. Enter a name for your topic, such as **Set context variables**, and save it.
   1. Add a new node to the topic, and select **Variable management** > **Set a variable value**.
   1. In your new node, under **Set variable**, select **Create a new variable**.
   1. Open the **Variable properties** pane by selecting the new variable name. In the pane, set the **Variable name** to match the workstream context variable name exactly (it's case sensitive).
   1. In the **Reference** section, select the vertical ellipses, and then select **Get value from this node if empty**. The Copilot Studio agent retrieves the variable value from this node at runtime.
   1. In the **Usage** section, select **Global (any topic can access)** and **External sources can set values** so that Copilot Studio agent accepts data from omnichannel and this variable can be used in any topic.
   1. Close the **Variable properties** pane.
   1. In your node, enter a default value in **To value** to initialize.
   1. Save and publish the changes.

At runtime, the variable within your Copilot agent is set to the value from Dynamics 365 Contact Center, and you can use it for consumption.

### Related information

[Configure proactive engagement](configure-proactive-engagement.md)  