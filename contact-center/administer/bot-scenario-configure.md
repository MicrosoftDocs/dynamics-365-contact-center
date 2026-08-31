---
title: Configure the sample voice agent template
description: Learn how to import and configure the sample voice agent template for a voice workstream in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: bap-ai-copilot
ms.date: 08/27/2026
ms.update-cycle: 180-days
ms.custom: bap-template
---

# Configure the sample voice agent template

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]

Use the Interactive Voice Response (IVR) voice agent sample in Microsoft Copilot Studio to learn how a voice agent connects to a workstream in Dynamics 365 Contact Center or Dynamics 365 Customer Service. The template demonstrates the following capabilities:

- **Intent detection from conversational phrases**: Identifies the caller's intent by analyzing spoken phrases, ensuring inquiries are routed to the appropriate resources or workflows. The template recognizes customer intent to track order status.

- **Numeric input by voice**: Allows users to provide numeric information through voice input. This streamlines the process for entering data such as account numbers or PINs without using a keypad.

- **Generative answers**: If the user specifies a phrase that the AI agent can't handle, the agent uses **Generative Answers** to provide information.

- **Distinguish number entities based on length**: Differentiates between numeric entities based on their length, enhancing accuracy in identifying account numbers, phone numbers, or other relevant data.

- **Self-service/account lookup**: Enables callers to access account information or perform self-service tasks without customer service representative assistance, improving efficiency and customer satisfaction.

- **Reprompt and entity validation**: Prompts callers for clarification if the initial input is unclear and validates entities to make sure the correct information is captured.

## Prerequisites

- Dataverse is provisioned in your environment to store and manage tables. Learn more in:
    - [Improve copilot responses from Microsoft Dataverse](/power-apps/maker/data-platform/data-platform-copilot)
    - [Create low-code plug-ins to use with a copilot (preview)](/power-apps/maker/data-platform/low-code-plugins-copilot-studio)
    - [Add knowledge to an agent](/microsoft-copilot-studio/knowledge-add-existing-copilot)
- [Voice channel is provisioned](../implement/provision-channels.md)
- [Procure phone numbers](/dynamics365/customer-service/administer/voice-channel-manage-phone-numbers?context=/dynamics365/contact-center/context/administer-context)
- [Workstream is set up and the phone number is linked to a voice channel](/dynamics365/customer-service/administer/voice-channel-inbound-calling?context=/dynamics365/contact-center/context/administer-context).

## Import and configure the voice agent template

1. Download the [sample voice agent zip](https://go.microsoft.com/fwlink/?linkid=2297969) file.
1. Save the zip file to your local computer.
1. In Copilot Studio, [import the solution](/microsoft-copilot-studio/authoring-export-import-copilot-components#import-a-solution-to-add-component-collections-to-an-environment). The template appears on the **Scenarios** page.
1. On the **Agents** page, modify the agent's workflow settings, topics, and call routing to align with your customer service processes.
1. In Dynamics 365 Contact Center or Dynamics 365 Customer Service, [set up the voice agent in the voice channel](/dynamics365/customer-service/administer/voice-channel-pva-bots?context=/dynamics365/contact-center/context/administer-context).

 > [!NOTE]
 > Add the agent to the voice workstream in the omnichannel app and test it before you change the topics.

## How the Contoso order status voice agent works

 > [!NOTE]
 > Examples are for illustration only and are fictitious. No real association is intended or inferred.

The voice agent template helps customers track the status of their orders. When a customer calls the phone number linked to the agent's workstream, the workflow is as follows:

1. The agent greets the customer and asks how it can help. The AI agent template has a Dataverse query that replicates an API call which happens at the start of a call. This query returns a holiday sale message for Valentine’s Day. 
   > [!NOTE]
   > The customer can select Spanish-US by selecting * (asterisk). However, the rest of the AI agent's workflow hasn't been translated to Spanish. The agent will continue to respond in English.
1. The customer says, "I want to track my order."
1. The agent recognizes the customer's intent to track an order and prompts the customer to provide the order number or phone number. If the customer says a phrase that the AI agent can't handle, the agent uses **Generative Answers** to provide information. The agent redirects the user to the main menu with the prompt, "What else can I help you with?"
1. The AI agent initiates a Dataverse query to trigger Automatic Number Identification to validate the caller. In this example, the Dataverse table returns sample Automatic Number Identification information to the AI agent. The agent then asks the customer if they want to look up the status of the order associated with that phone number.
1. The customer can either say the order number or enter it using the dialpad. 
1. The agent then validates the order number. If the order number isn't valid, the agent prompts the customer to specify the order number again.  
1. The agent asks for the customer's ZIP code.
1. The customer says or enters the ZIP code. The agent validates it and prompts the customer to try again if it isn't valid.
1. The agent retrieves the status and tells the customer about the order status.
1. The agent then asks the customer if there's anything else it can help the customer with. Based on the customer's response, the following actions occur:
     - **No**: Call ends.
     - **Yes**: Call continues, but the agent doesn't engage with the call further. In Copilot Studio, you can add an end conversation topic to end the call.

The agent transfers the customer to a customer service representative based on the workstream configuration, if the customer requests to speak to a service representative at any point during the call.

## Related information

[Integrate a Copilot agent](/dynamics365/customer-service/administer/configure-bot-virtual-agent)  
