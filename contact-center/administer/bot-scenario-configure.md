---
title: Configure a sample IVR bot template
description: Learn how to configure a sample IVR bot template.
author: rhanajoy #Required; your GitHub user alias, with correct capitalization.
ms.author: rhcassid #Required; your Microsoft alias; optional team alias.
ms.reviewer: kfend #Required; Microsoft alias of content publishing team member.
ms.topic: how-to #Required; don't change.
ms.collection: get-started #Required; If this isn't a getting started article, don't remove the attribute, but leave the value blank. The values for this attribute will be updated over time.
ms.date: 11/06/2024
ms.custom: bap-template #Required; don't change.
---

# Configure a sample IVR bot template

This topic provides the steps to import the Interactive Voice Response (IVR) agent sample template and then connect the agent to a workstream in Dynamics 365 Contact Center or Customer Service. The sample provides a pre-built template with the following IVR capabilities for managing customer conversations:

- **Intent Detection from Conversational Phrase**: Identifies the caller's intent by analyzing spoken phrases, ensuring inquiries are routed to the appropriate resources or workflows. The template recognizes customer intent to track order status.

- **Numeric Input by Voice**: Allows users to provide numeric information through voice input, streamlining the process for entering data such as account numbers or PINs without using a keypad.

- **Distinguish Number Entities Based on Length**: Differentiates between numeric entities based on their length, enhancing accuracy in identifying account numbers, phone numbers, or other relevant data.

- **Self-Service/Account Lookup**: Enables callers to access account information or perform self-service tasks without agent assistance, improving efficiency and customer satisfaction.

- **Re-Prompt/Entity Validation**: Re-prompts callers for clarification if the initial input is unclear, validating entities to ensure correct information is captured, reducing errors and improving the interaction experience.

## Prerequisites

- Dynamics 365 Contact Center or Customer Service license
- Microsoft Copilot Studio license.
- Voice channel is provisioned and you have procured phone numbers.
- Workstream is set up and the phone number is linked to a voice channel. 


## Import and configure the IVR bot template

1. Download the zip file and save it to your local machine.
1. In Copilot Studio, perform the steps in [import a solution](/microsoft-copilot-studio/authoring-export-import-copilot-components#import-a-solution-to-add-component-collections-to-an-environment) to import the zip file. The template is displayed on the **Scenarios** page.
1. In the Copilots page, you'll see the IVR bot. You can modify the bot's workflow setting, bot topics, and call routing to align with your customer service processes and scenarios.
1. Perform the steps in [Set up IVR bots in the voice channel](/customer-service/administer/voice-channel-pva-bots) to finish the bot configuration in Dynamics 365 Contact Center or Customer Service.

 > [!NOTE]
 >  We recommend you add the bot to the voice workstream in the omnichannel app and test it before you make changes to the bot topics.

## Contoso Order Status bot workflow

The IVR bot template is intended to help customers track the status of their orders. When you call the the phone number linked to the workstream the bot is added, the bot workflow is as follows:

1. Bot greets you and asks  how it can help.
1. You say, "I want to track my order."
1. The bot recognizes the your intent to track an order and prompts you to provide the order number or phone number. 
1. You can either say the order number or enter it using the dialpad. In this example, can use: 12345678911234. The bot then validates the order number. If the order number is not valid, the bot prompts you to specify the order number again.  
1. The bot then asks for your zip code. You can either say the zipcode or type it in. In this example, use 90210. The bot validates the zip code. If the zip code is not valid, the bot prompts you to specify the zip code again.
1. The bot retrieves and tells you the status of your order.
1.  The bot then asks if you want text updates and if there is anything else it can help you with. If you say No, the call ends.
1. At any point in the call, if you say "speak to an agent" the it bot transfers you to a customer service representative based on the workstream configuration.
 

## Next steps
