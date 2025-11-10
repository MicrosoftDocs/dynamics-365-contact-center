---
title: Configure multilingual voice agents
description: Learn how to configure multilingual Copilot Studio voice agent in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham 
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 11/10/2025
ms.custom: bap-template 
---

# Configure multilingual voice agents

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]

You can configure a single voice agent to communicate with customers in different languages, reducing the overhead of creating and maintaining multiple AI agents (agents) in a copilot.

To enable the agent to detect the customer language and respond in same language, configure a workstream with one of the following options:

- Multiple voice channels with different phone numbers for different languages.
- A single voice channel with one phone number that supports multiple languages.

## Prerequisites

- Configure the [Voice-enabled agent](/microsoft-copilot-studio/voice-build-from-template) in Copilot Studio.
- Configure the languages the voice channel supports as primary or secondary languages for the Copilot Studio agent. Learn more in [Configure and create multilingual agents](/microsoft-copilot-studio/multilingual). The agent must support all the languages that the voice channel supports.
- Configure the [voice workstream](/dynamics365/customer-service/administer/voice-channel-inbound-calling#set-up-a-voice-workstream?context=/dynamics365/contact-center/context/administer-context) in Copilot Service admin center.
- Define the language-based routing rules. Learn more in [Configure work classification rulesets for unified routing](/dynamics365/customer-service/administer/configure-work-classification?context=/dynamics365/contact-center/context/administer-context).

## Configure multilingual agents for the workstream

In Copilot Service admin center, for a voice channel in a workstream, perform the following steps:

1. [Add a phone number to the workstream and configure language settings](/dynamics365/customer-service/administer/voice-channel-inbound-calling#add-a-phone-number-to-the-workstream-and-configure-language-settings?context=/dynamics365/contact-center/context/administer-context). The following actions apply:
   - The voice channel must have a language that matches the Copilot agent's primary language or one of its configured secondary languages. If there's no language match, the AI agent defaults to its primary language.
   -  When transcription is enabled for a voice channel, the transcript appears in the language the AI agent detects. If the AI agent switches to a language that the voice channel doesn't support, the transcript falls back to the channel's primary language. When the AI agent switches between languages, there might be a brief delay before the transcript updates. Some parts of the transcript may still appear in the previous language during this transition.
1. In the **Bots** section of the workstream, add the agent that you want to use. The application displays a warning message if the languages configured in the voice channel don't match the languages supported by the agent.

A warning message appears if you add a new language that the agent doesn't support to an existing voice channel.

### Examples

The following scenarios describe the multilingual AI agent's behavior when linked to a workstream with different language configurations. 

**Scenario 1:** 

You configured a [multilingual voice AI agent](/microsoft-copilot-studio/multilingual) called Contoso Coffee in Copilot Studio with these settings: 

- English is the primary language.
- Spanish and French are secondary languages.

You have a workstream, Contoso Coffee Shop, with these settings:

 - Two [voice channels](/dynamics365/customer-service/administer/voice-channel-inbound-calling#configure-a-voice-channel) with different phone numbers. One channel has Spanish as the primary language and the other has German.
 - The Contoso Coffee agent is linked to the workstream. The AI agent identifies the customer's language based on the [primary language of the voice channel](/dynamics365/customer-service/administer/voice-channel-inbound-calling#add-a-phone-number-to-the-workstream-and-configure-language-settings).

The runtime experience is as follows:

- When a customer calls the phone number for Spanish, the agent responds in Spanish.
- When a customer calls the phone number for German, the agent responds in English because German isn't a supported language for the agent. 

**Scenario 2:**

You also have another workstream, Contoso Coffee Beans, with these settings:
 - A voice channel with a single phone number. The primary language is Spanish. French and English are additional languages.
 - The Contoso returns agent is configured for the workstream, which greets the customer in its primary language. The agent then asks the customer to choose their preferred language by voice or text input. The options are: one English, two Italian, three Portuguese. The agent switches to the chosen language.
 
The runtime experience is as follows:

When a customer calls the phone number linked to the voice channel, the AI agent says hello in Spanish and repeats the options for other languages. If the customer says "English" or presses 1, the agent switches to English and continues in English.

## Escalate the call to a representative

If the agent can't answer the customer's question or if they ask to talk to a human representative, you can set up the agent to transfer the call to either a default queue or a queue that matches their language. To escalate the call to a language-specific queue, you need to create a queue for each language you support.

For the example in **Scenario 1** or **Scenario 2**, to route the call to a language-specific representative, perform the following steps:

- Create three [voice queues](/dynamics365/customer-service/administer/queues-omnichannel?context=/dynamics365/contact-center/context/administer-context)—one each for English, French, and Portuguese—and add representatives who speak those languages.
- In the route-to-queues rule set of the workstream, use **Conversation.CustomerLanguage** as the criterion to route calls to different queues based on what customers select.

## View metrics for multilingual agents

You can see how your multilingual agents perform by using the [Omnichannel historical](/dynamics365/customer-service/use/oc-bot-dashboard?context=/dynamics365/contact-center/context/use-context) report. You can filter by Last Language to see metrics for agents based on the language they've used to communicate with the customer. The **Last Language** filter isn't available on the dashboard by default. To add the filter, perform the steps in [Customize the bot dashboard](../use/customize-agent-dashboard.md).

### Related information

[Integrate a Copilot agent](/dynamics365/customer-service/administer/configure-bot-virtual-agent)  
