---
title: Configure sensitive variable masking for voice agents
description: Learn how to configure sensitive variable masking for voice agents in Dynamics 365 Contact Center.
ms.date: 09/30/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Configure sensitive variable masking for voice agents

AI agents collect sensitive data during interactions and store it in your organization's tenant. In Copilot Studio, you can use a sensitive variable flag to help protect information such as PINs, account numbers, credit card details, and protected health information (PHI) data, without affecting productivity. Agent authors can mark variables as sensitive per your organizational requirements to improve data security.

  > [!NOTE]
  > [!INCLUDE [cc-sensitive-data-redaction](../includes/cc-sensitive-data-redaction.md)]

## Prerequisites

- [Voice channel is provisioned in Customer Service](/dynamics365/customer-service/administer/voice-channel-install).
- [Set up inbound calling](/dynamics365/customer-service/administer/voice-channel-inbound-calling).
- You have a Copilot Studio voice agent added to a workstream.
- You have the System administrator and Bot author role assigned.

## Configure sensitive data masking

1. Identify the information in your AI agent’s conversational flow that can contain sensitive data. For example, the input to the agent is a credit card number.
2. Create a variable in Copilot Studio or in a question node. Learn more in [Use variables](/microsoft-copilot-studio/authoring-variables-bot?tabs=webApp#use-global-variables)
3. Select **{x}** for the variable. In the **Variable properties** pane, set the **Sensitive data** toggle to **On**.

> [!NOTE]
> - When a sensitive variable is assigned to a nonsensitive variable, the nonsensitive variable is automatically considered as sensitive. For example, if you have a variable called `CreditCardNumber` and you assign it to a nonsensitive variable called `PaymentInfo`, the `PaymentInfo` variable is also considered sensitive.
> - If logging to Application Insights is enabled, make sure that the **Log sensitive activity properties** toggle is turned off. Enabling this setting results in sensitive data being recorded in Application Insights, which may compromise data privacy. Learn more in [Connect your Copilot Studio agent to Application Insights](/microsoft-copilot-studio/advanced-bot-framework-composer-capture-telemetry).

## Runtime experience

When the customer’s conversation with the AI agent enters a section where a sensitive-flagged variable is configured, the AI agent displays a message in transcription "Entered a confidential section of the conversation". The system pauses recording, transcription, and data logging until the conversation moves on to the nonsensitive section.

When the conversation moves past the sensitive information collection, the agent displays a message that says, "Exited a confidential section of the conversation", followed by "Recording and transcription resumed". The system resumes recording, transcription, and data logging for all nonsensitive portions of the interaction.

If the AI agent escalates a conversation to a customer service representative, the transcript and recording don’t contain any instances of the sensitive information captured by the AI agent.

To match the recording to the call's length, the application inserts silence into the recording during the segments that contain the sensitive information.

## Key considerations

- AI agent makers are responsible to mark the variables as sensitive wherever they anticipate sensitive information.

- Copilot Studio doesn’t automatically redact sensitive data from question nodes or message nodes that don’t have sensitive variables assigned to them.

- Sensitive information isn’t removed if a caller unexpectedly shares something sensitive and the variable capturing that response isn’t marked as sensitive.

- AI agent makers should account for potential latency in pausing the recording and transcription.

- Sensitive information redaction is restricted to Copilot Studio. For any external connections from Copilot Studio to Power Automate or connectors, customers are responsible for assessing redacted data with any relevant regulatory or compliance requirements.

- [!INCLUDE [cc-sensitive-data-redaction](../includes/cc-sensitive-data-redaction.md)]

## Supported actions

| **Supported action**                                           | **Data redacted** | **Notes**                                                                                                                                             |
|-----------------------------------------------------------------|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Flag variables as sensitive                                     | Yes                |                                                                                                                                                        |
| Assign a sensitive variable to a nonsensitive variable          | Yes                |                                                                                                                                                        |
| Sensitive variable in question node                             | Yes                |                                                                                                                                                        |
| Sensitive variable in message node                              | Yes                |                                                                                                                                                        |
| Sensitive variable in condition node                            | Yes                |                                                                                                                                                        |
| Using sensitive variable in Power Fx                            | Yes                |                                                                                                                                                        |
| Write sensitive data to Dataverse explicitly                    | No                 | Not redacted.                                                                                                                                           |
| Pass sensitive information in HTTP request                      | Yes                | Sensitive variables aren’t logged in Copilot Studio. Customers are responsible for redacting data from any destination they're sending this data to.  |
| Receive sensitive information from HTTP request                 | Yes                | Not redacted.                                                                                                                                           |
| Passing sensitive information to connectors                     | Yes                | Sensitive variables aren’t logged in Copilot Studio. Customers are responsible for redacting data from any destination they're sending this data to.  |
| Receive sensitive information from connectors                   | No                 | Not redacted.                                                                                                                                           |
| Pass sensitive information to Power Automate flows              | Yes                | The sensitive flag is turned on in Power Automate.                                                                                                    |
| Receive sensitive information from Power Automate               | No                 | Not redacted.                                                                                                                                          |
| Pass sensitive information explicitly in transfer nodes        | No                 | Not redacted.                                                                                                                                          |
| Pass sensitive information to generative AI                            | No                 | Not redacted.                                                                                                                                           |
| Write sensitive data to AppInsights through a custom log event      | No                 | Not redacted.                                                                                                                                           |
| Conversation logs in Dataverse (ConversationTranscripts table)  | Yes                |                                                                                                                                                        |
| Copilot Studio agent transcripts passed to Copilot Service workspace                  | Yes                | Only variables flagged as sensitive are redacted.                                                                                                       |
| Digital/messaging channel                                       | No                 | Sensitive data is redacted from the AI agent transcripts, but is visible in Dynamics 365 Contact Center transcripts.                             |
| Multi-entity                                                    | Yes                | All the entities are flagged as sensitive.                                                                                                             |

## Related information

[Configure IVR agents for voice](/dynamics365/customer-service/administer/voice-channel-pva-bots)  
