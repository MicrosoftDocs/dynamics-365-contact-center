---
title: Configure multilingual voice bots
description: Learn how to configure multilingual Copilot Studio voice bots.
author: gandhamm
ms.author: mgandham 
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---


# Configure multilingual voice bots

You can configure a single voice bot to communicate with customers in different languages, reducing the overhead of creating and maintaining multiple bots in a copilot.

To enable the bot to detect the customer language and respond in same language, configure a workstream with one of the following options:

- Multiple voice channels with different phone numbers for different languages.
- A single voice channel with one phone number that supports multiple languages.

## Prerequisites

- Configure [Voice-enabled bot](/microsoft-copilot-studio/voice-build-from-template) in Copilot Studio.
- Configure the languages the voice channel supports as  primary or secondary languages for the Copilot Studio bot. Learn more in[multilingual capabilities](/microsoft-copilot-studio/multilingual). The bot must support all the languages that the voice channel supports.
- Configure [voice workstream](/dynamics365/customer-service/administer/voice-channel-inbound-calling#set-up-a-voice-workstream?context=/dynamics365/contact-center/context/administer-context) in the Contact Center admin center or Customer Service admin center.
- Define the language-based routing rules. More information: [Configure work classification rulesets for unified routing](/dynamics365/customer-service/administer/configure-work-classification?context=/dynamics365/contact-center/context/administer-context).

## Configure multilingual bots for the workstream

In Contact Center admin center or Customer Service admin center, for a voice channel in a  workstream, perform the following steps:

1. [Add a phone number to the workstream and configure language settings](/dynamics365/customer-service/administer/voice-channel-inbound-calling#add-a-phone-number-to-the-workstream-and-configure-language-settings?context=/dynamics365/contact-center/context/administer-context). The following actions apply:
  - The language of the voice channel must match either the primary or one of the secondary languages of the bot in Copilot Studio. If the languages don't match, the bot uses its primary language.
  -  If you enable transcription for a voice channel, the transcript is displayed in the language the bot detects. However, if the bot switches to a language that the channel doesn't support, the transcript is displayed in the primary language of the channel. There might be a slight delay for the transcript to be updated when the bot changes languages. Some parts of the transcript might be in the previous language.
1. In the **Bots** section of the workstream, add the bot that you want to use. The application displays a warning message if the languages configured in the voice channel don't match the languages supported by the bot.

The application displays a warning if you add a new language that the bot doesn't support to an existing voice channel.


### Examples

**Scenario 1:** 

You have a multilingual bot, Contoso Coffee bot, in Copilot Studio with English as the primary language and Spanish and French as secondary languages.

You have a workstream, Contoso Coffee Shop, with these settings:
 - Two voice channels with different phone numbers. One channel has Spanish as the primary language and the other has German.
 - The Contoso Coffee bot is linked to the workstream. The bot identifies the customer's language based on the primary language of the voice channel.

When a customer calls the phone number for Spanish, the bot responds in Spanish.

When a customer calls the phone number for German, the bot responds in English because German isn't a supported language for the bot. 

**Scenario 2:**

You also have another workstream, Contoso Coffee Beans, with these settings:
 - A voice channel with a single phone number. The primary language is Spanish. French and English are additional languages.
 - The Contoso returns bot is configured as the bot for the workstream. The bot greets the customer in its primary language. Then it asks the customer to choose their preferred language by voice or text input. The options are: one English, two Italian, three Portuguese. The bot switches to the chosen language.

When a customer calls the phone number linked to the voice channel, the bot says hello in Spanish and repeats the options for other languages. If the customer says "English" or presses 1, the bot switches to English and continues in English.

## Escalate the call to a representative

If the bot can't answer the customer's question or if they ask to talk to a human representative, you can set up the bot to transfer the call to either a default queue or a queue that matches their language. To escalate the call to a language-specific queue, you need to create a queue for each language you support.

For the example in **Scenario 1** or **Scenario 2**, to route the call to a language-specific representative, perform the following steps:

- Create three [voice queues](/dynamics365/customer-service/administer/queues-omnichannel?context=/dynamics365/contact-center/context/administer-context)—one each for English, French, and Portuguese—and add representatives who speak those languages.
- In the route-to-queues rule set of the workstream, use **Conversation.CustomerLanguage** as the criterion to route calls to different queues based on what customers select.

## View metrics for multilingual bots

You can see how your multilingual bots perform by using [Omnichannel historical](/dynamics365/customer-service/use/oc-bot-dashboard?context=/dynamics365/contact-center/context/use-context) and [real-time analytics](../use/agent-realtime-dashboard.md) reports. You can filter by Last Language to see metrics for bots based on the language they've used to communicate with the customer. The **Last Language** filter isn't available on the dashboard by default. To add the filter, perform the steps in [customize bot dashboards](../use/customize-agent-dashboard.md).