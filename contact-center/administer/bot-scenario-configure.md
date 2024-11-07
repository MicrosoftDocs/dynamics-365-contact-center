---
title: How-to topic template #Required; page title displayed in search results. Don't enclose in quotation marks.
description: How-to description #Required; article description that's displayed in search results. Don't enclose in quotation marks. Do end with a period.
author: rhanajoy #Required; your GitHub user alias, with correct capitalization.
ms.author: rhcassid #Required; your Microsoft alias; optional team alias.
ms.reviewer: kfend #Required; Microsoft alias of content publishing team member.
ms.topic: how-to #Required; don't change.
ms.collection: get-started #Required; If this isn't a getting started article, don't remove the attribute, but leave the value blank. The values for this attribute will be updated over time.
ms.date: 11/06/2024
ms.custom: bap-template #Required; don't change.
---

# Sample bot template

The Interactive Voice Response (IVR) agent sample template provides a pre-built template for managing customer phone interactions. By importing this template, you can quickly set up automated call handling to direct customers to the right resources and streamline your support operations.
This topic provides the steps to import the sample template and then connect the bot to a workstream in Dynamics 365 Conatct Center or Customer Service.
 Once configured, the bot helps reduce response times, automate common inquiries, and allow your support team to focus on complex customer needs.

## Prerequisites

- Dynamics 365 Contact Center or Customer Service license
- Microsoft Copilot Studio license

## Key IVR features

- Intent Detection from Conversational Phrase:This feature enables the IVR system to accurately identify the caller's intent by analyzing their spoken phrases, ensuring that inquiries are routed to the appropriate resources or workflows.
The current template is built to recognize the customer’s intent to track the status of their order.

- Numeric Input by Voice: Allowing users to provide numeric information through voice input streamlines the interaction process, making it easier for callers to enter data such as account numbers or PINs without needing to use a keypad. 

Distinguish Number Entities Based on Length: The IVR can differentiate between numeric entities based on their length, enhancing accuracy in identifying account numbers, phone numbers, or other relevant data, ensuring that the correct information is processed. DTMF?

Self-Service/Account Lookup: This functionality empowers callers to access their account information or perform self-service tasks without the need for agent assistance, improving efficiency and customer satisfaction.

Re-Prompt/Entity Validation: The system can re-prompt callers for clarification if the initial input is unclear, validating entities to ensure that the correct information is captured before proceeding, thereby reducing errors and improving the overall interaction experience.

## Deployment steps

1. Download the zip file and save it to your local machine.
1. In Copilot Studio, perform the steps in [import a solution](/microsoft-copilot-studio/authoring-export-import-copilot-components#import-a-solution-to-add-component-collections-to-an-environment) to import the zip file. The template is displayed on the **Scenarios** page.
1. In the Copilots page, you'll see the IVR bot template.
1. Perform the steps in [Set up IVR bots in the voice channel](/customer-service/administer/voice-channel-pva-bots) to finish the bot configuration in Dynamics 365 Contact Center or Customer Service.


## Next steps
