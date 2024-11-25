---
title: Configure a sample voice agent template
description: Learn how to configure a sample voice agent template.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: 
ms.date: 11/25/2024
ms.custom: bap-template
---

# Configure a sample voice agent template

 > [!NOTE]
 > Some examples are for illustration only and are fictitious. No real association is intended or inferred.

This article explains how the Interactive Voice Response (IVR) or voice agent sample that's created in Microsoft Copilot Studio  works when connected with a workstream in Dynamics 365 Contact Center or Customer Service. The sample provides a prebuilt template with the following capabilities for managing customer conversations:

- **Intent detection from conversational phrases**: Identifies the caller's intent by analyzing spoken phrases, ensuring inquiries are routed to the appropriate resources or workflows. The template recognizes customer intent to track order status.

- **Numeric input by voice**: Allows users to provide numeric information through voice input. This streamlines the process for entering data such as account numbers or PINs without using a keypad.

- **Distinguish number entities based on length**: Differentiates between numeric entities based on their length, enhancing accuracy in identifying account numbers, phone numbers, or other relevant data.

- **self-service/account lookup**: Enables callers to access account information or perform self-service tasks without agent assistance, improving efficiency and customer satisfaction.

- **Reprompt/entity validation**: Prompts callers for clarification if the initial input is unclear, validates entities to ensure correct information is captured. This reduces errors and improves the interaction experience.

## Prerequisites

- Dataverse is provisioned in your environment to store and manage tables.
- [Voice channel is provisioned](../implement/provision-channels.md)
- [Procure phone numbers](/dynamics365/customer-service/administer/voice-channel-manage-phone-numbers?context=/dynamics365/contact-center/context/administer-context)
-  [Workstream is set up and the phone number is linked to a voice channel](/dynamics365/customer-service/administer/voice-channel-inbound-calling?context=/dynamics365/contact-center/context/administer-context). 

## Import and configure voice agent template


see [Sample schema for capacity profiles](https://github.com/microsoft/Dynamics365-Apps-Samples/blob/neeranelli-patch-10/contact-center/copilot-agents/ContosoOrderStatusCOS_1_2_0_32.zip)

1. Download the [sample voice agent zip]((https://github.com/microsoft/Dynamics365-Apps-Samples/tree/master/customer-service/unified-routing-sample-schemas/Sample%20schema%20for%20capacity%20profiles.xml)) file and save it to your local machine. You can download the zip file from [here].
1. In Copilot Studio, perform the steps in [import a solution](/microsoft-copilot-studio/authoring-export-import-copilot-components#import-a-solution-to-add-component-collections-to-an-environment) to import the zip file. The template is displayed on the **Scenarios** page.
1. In the Agents page, you see the voice agent. You can modify the agent's workflow setting, topics, and call routing to align with your customer service processes and scenarios.
1. To finish the agent configuration in Dynamics 365 Contact Center or Customer Service, perform the steps in [Set up voice agents in the voice channel](/customer-service/administer/voice-channel-pva-bots)

 > [!NOTE]
 > We recommend you add the agent to the voice workstream in the omnichannel app and test it before you make changes to the topics.

## Contoso Order Status voice agent workflow

The voice agent template is intended to help customers track the status of their orders. When you call the the phone number linked to the workstream the agent is added, the workflow is as follows:

1. The agent greets the customer and asks how it can help.
1. The customer says, "I want to track my order."
1. The agent recognizes the customer's intent to track an order and prompts the customer to provide the order number or phone number. 
1. The customer can either say the order number or enter it using the dialpad. 
1. The agent then validates the order number. If the order number isn't valid, the agent prompts the customer to specify the order number again.  
1. The agent then asks for your zip code. 
1. The customer can either say the zipcode or type it in. The agent validates the zip code. If the zip code isn't valid, the agent prompts the customer to specify the zip code again.
1. The agent retrieves the status and tells you the status of your order.
1. The agent then asks the customer if there's anything else it can help the customer with. Based on the customer's response, the following actions occur:
     - **No**: Call ends. 
     - **Yes**: Call is ongoing, but the agent doesn't engage with the call further. In Copilot Studio, you can add an end conversation topic here to end the call.
1. The agent transfers the customer to a customer service representative based on the workstream configuration, if the customer requests to speak to a service representative at any point during the call. 

