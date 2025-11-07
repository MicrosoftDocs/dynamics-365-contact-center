---
title: Set up voice agents to use intents
description: Learn how to configure intent-based suggestions for Copilot agents enabled for voice using Customer Intent Agent in Dynamics 365 Contact Center to automate and streamline your contact center.
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.topic: how-to
ms.collection: bap-ai-copilot
ms.date: 11/07/2025
ms.custom: bap-template
---

# Set up voice agents to use intents

Customer Intent Agent for voice uses generative AI to autonomously discover intents in your Dynamics 365 Contact Center instance. It analyzes past interactions between customer service representatives (service representatives or representatives) and customers to create an intent library that enhances dynamic conversations. Intent benefits self-service scenarios by enabling agents to quickly understand customer needs, guide conversations with follow-up questions, and provide tailored solutions in real time.

## Prerequisites

- [Enable Customer Intent Agent](manage-customer-intent-agent.md#enable-customer-intent-agent).
- [Intent discovery is set up](manage-customer-intent-agent.md#manage-intent-discovery-setup) and intents are available in the intent library.
- [Service principal](#create-a-service-principal) for the customer organization is created.
- [Instructions](manage-customer-intent-agent.md#manage-instructions-optional), [connectors](manage-customer-intent-agent.md#manage-connectors-for-ai-agents-optional), and knowledge are configured for intents marked for self-service.
  > [!NOTE]
  > You must share the connection for the custom connector with the following App ID:`d3e4eed9-fdab-4c55-a667-e4d1ffc8bb85`.
- [New Copilot agents](/dynamics365/customer-service/administer/manage-your-bots?context=/dynamics365/contact-center/context/administer-context) are enabled for voice and connected to your contact center environment.

## How it works

- An administrator sets up intent, uses historical data to build the intent library, and enables the library for Copilot agents.

- The IVR agent routes the call to the intent-enabled voice agent via the Customer Intent Agent queue.
- Copilot agent detects customer intent, asks follow-up questions related to the intent, and provides a solution from the configured resources.
- If the conversation is escalated, it's transferred to representatives.
- The application also uses this conversation to detect any updates and discover new intent attributes that can be used in future interviews.
- In the next customer interaction, the Copilot agent can address the issue using the newly-generated knowledge and intent, providing a tailored response without escalating to a representative.

## Configure voice agents

Perform the following steps in Copilot Service admin center.

1. To configure intent for voice agent, on the **AI Agents** page, select a Copilot agent for which the voice status shows as **Connected**.  We recommend that you use a newly-provisioned Copilot agent in this step.

1. Select **Manage type**. On the **Type** dialog, select **Uses AI-generated intents** and **Voice only**.
    > [!NOTE]
    > Configurations that you set for the AI agent in Copilot Studio aren't applicable after you set the type **Uses AI-generated intents**. The runtime logic for the voice agent uses the intents in the intent library only. You can add the voice agent to a workstream as the deflection agent. However, we recommend that you integrate the Customer Intent Agent enabled voice agent with your current IVR system, place the voice agent in a voice queue, and route the calls to it.

    :::image type="content" source="../media/intent-settings-for-voice-agents.png" alt-text="Screenshot of intent settings for voice agent.":::

1. Save and close. The type of the agent changes to **Voice - AI Intents**.

## Configure voice agents to use line of business

Your intent agent might be set up to use multiple lines of businesses. If you're using lines of business, make sure that you set the line of business in conversation context before the intent agent is added to the conversation. This sets the scope for intents and instructions that your intent agent follows during the rest of the conversation.

To set the line of business during the conversation, make sure you set the context variable “va_LineOfBusiness” to the globally unique identifier of the corresponding line of business you want the intent agent to recognize. Make sure your Customer Intent Agent is on a queue and a Copilot agent is the first to answer the call. When escalating to the Customer Intent Agent, make sure your Copilot Agents sets a variable “va_LineOfBusiness” to the value of the target line of business.

Learn about finding the unique ID of the line of business in [Discover line of business unique IDs](manage-customer-intent-agent.md#discover-line-of-business-unique-ids).

:::image type="content" source="../media/context-variable-for-lob.png" alt-text="Screenshot of context variable va_LineOfBusiness configuration.":::

> [!IMPORTANT]
> If you’ve configured lines of business, but don't set the value during the conversation, the voice agent using intent falls back to the first line of business, ordered alphabetically, in your environment.

## Connect voice agents to voice queues or workstreams

To use Customer Intent Agent for voice, you need to connect your **Voice - AI Intents** type agent to a queue or workstream.  If you connect the Customer Intent Agent for voice to a workstream, it handles all the traffic to that workstream. However, it can't set context, and you need to configure the routing logic appropriately. If you need granular control over routing logic, we recommended that you connect the Customer Intent Agent for voice to a queue as shown in the following diagram.  In this configuration, a separate Copilot agent acts as the workstream IVR agent, and then escalates calls to the Customer Intent Agent for voice in a particular queue for the required triggers.

:::image type="content" source="../media/diagram-customer-intent-agent-voice.png" alt-text="Diagram that shows how Customer Intent Agent is integrated with existing voice agents." lightbox="../media/diagram-customer-intent-agent-voice.png":::

Follow these steps to configure the IVR agent to escalate the calls to the Customer Intent Agent for voice in a queue:

1. Create a voice queue and add the Customer Intent Agent for voice to the queue. Learn more in [create a queue](/dynamics365/customer-service/administer/queues-omnichannel).

1. In the existing topic flow for your workstream Copilot IVR agent, where you want to use Customer Intent Agent for voice, save a variable (for example va_AgentTransfer=True) and call the transfer to agent action. Learn more in [Work with variables](/microsoft-copilot-studio/authoring-variables).
1. In the route-to-queue rules of the voice workstream, route to the queue with your Customer Intent Agent based on the **va_AgentTransfer** variable. The Customer Intent Agent is invoked, and if it can't resolve the customer issue, it escalates the call and triggers the queue routing again. When the call is routed the second time, make sure that you configure the rules to route to a queue with a service representative.

## Configure instructions to use custom context for voice agents

Configure your voice agent to use context variables from the conversation and deliver a dynamic, personalized experience. You’ll include these variables in your intent agent instructions. The key steps are as follows:

1. Set any [context variables](/dynamics365/customer-service/administer/manage-context-variables) you want to use prior to engaging the intent agent. For example, the global variables that are created in Copilot Studio are [passed to Dynamics 365 Contact Center](/microsoft-copilot-studio/advanced-hand-off#context-variables-available-upon-handoff) when a conversation is escalated.

1. Author your instructions with replacement slugs to consume the context variables. Within instructions, use the syntax `{@<variable name>}`, for example: “The customer’s name is `{@Customer_Name}`.”

**Example**

1. In your context variables, configure a variable like Customer_Name to capture the customer’s name.
1. Set up your workstream with an agent from Copilot Studio, and add the intent agent to a queue.
1. In the Copilot Studio agent conversation session, capture the customer’s name and set it into a global variable `Customer_Name`. This is handed off to the contact center when you escalate to the intent agent.
1. In your intent instructions, insert the variable placeholder slug where appropriate. Example: The customer's name is {@Customer_Name}. Make sure to refer to the customer by name throughout the conversation.
1. Make sure to follow [best practices](manage-customer-intent-agent.md#how-to-write-clear-instructions) when authoring your instructions.

   > [!NOTE]
   > The intent agent can only read context variables. It can't set context variables.

## General behaviors of Customer Intent Agent for voice

- If the customer asks to be escalated to a representative, the agent complies.
- If the voice agent encounters any error, it escalates to a representative.
- If the customer query is resolved, the agent ends the call.
- If the customer remains silent, the agent ends the call.

### Create a service principal

To recreate the IVR workflows, the voice agent needs to access the connectors through a service principal that you must create for the environment where the customer data is stored.

1. As a user with administrator permissions to access the environment, sign in to [Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer).
1. In the site map, select **API Explorer**, and under **Resources available**, expand **servicePrincipals**, and select [**POST**](https://graph.microsoft.com/v1.0/servicePrincipals).
1. Enter the following JSON in **Request Body**, and select **Run query**:
   { "appId" : "d3e4eed9-fdab-4c55-a667-e4d1ffc8bb85"}

   The service principal is created and displayed in **Response preview**.

### Related information

[Overview of Customer Intent Agent](overview-customer-intent-agent.md)  
[Configure intent-based routing](/dynamics365/customer-service/administer/configure-intent-based-routing?context=/dynamics365/contact-center/context/administer-context)  
[Configure intent-based suggestions for Copilot agents](set-up-intent-agent.md)  
