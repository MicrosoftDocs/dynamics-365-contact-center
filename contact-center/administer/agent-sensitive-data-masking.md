---
title: Configure sensitive variable masking for voice agents
description: Learn how to configure sensitive variable masking for voice agents in Dynamics 365 Contact Center.
ms.date: 08/08/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Configure sensitive variable masking for voice agents

AI Agents collect sensitive data during interactions, storing it across your organization's tenant. Copilot Studio's sensitive variable flag protects PINs, account numbers, credit card details, and protected health information(PHI) data without affecting productivity. Agent authors can mark variables as sensitive per organizational requirements to improve data security.

# Prerequisites

- [Voice channel is provisioned in Customer Service](/dynamics365/customer-service/administer/voice-channel-install).
- [Set up inbound calling](/dynamics365/customer-service/administer/voice-channel-inbound-calling).
- You have a Copilot Studio voice agent added to a workstream.
- You have the System administrator and Bot author role assigned.

# Configure sensitive data masking

Perform the following steps:

1. Identify the information in your AI agent’s conversational flow that can contain sensitive data. For example, the input to the agent is a credit card number.
2. Create a variable in Copilot Studio or in a question node. Learn more in [Use variables](/microsoft-copilot-studio/authoring-variables-bot?tabs=webApp#use-global-variables)
3. Select **{x}** for the variable. In the **Variable properties** pane, set the **Sensitive data** toggle to **On**.

  > [!NOTE]
  > When a sensitive variable is assigned to a nonsensitive variable, the nonsensitive variable is automatically considered as sensitive. For example, if you have a variable called `CreditCardNumber` and you assign it to a nonsensitive variable called `PaymentInfo`, the `PaymentInfo` variable is also considered sensitive.

# Runtime experience

When the customer’s conversation with the AI agent enters a section where a sensitive-flagged variable is configured, the AI agent displays a message in transcription "Entered a confidential section of the conversation". Recording, transcription, and data logging are paused until the conversation moves on to the nonsensitive section.

When the conversation moves past the sensitive information collection, the agent displays a message indicating "Exited a confidential section of the conversation" followed by "Recording and transcription resumed". Recording, transcription, and data logging resumes for all nonsensitive portions of the interaction.

If the conversation is escalated to a customer service representative from the AI agent, the transcript and recording don’t contain any instances of the sensitive information captured by the AI agent.

To match the recording to the call's length, the application inserts silence into the recording.

# Key considerations

- AI Agent makers are responsible to mark the variables as sensitive wherever they anticipate sensitive information.

- Copilot Studio doesn’t automatically redact sensitive data from question nodes or message nodes that don’t have sensitive variables assigned to them.

- Sensitive information isn’t removed if a caller unexpectedly shares something sensitive and the variable capturing that response isn’t marked as sensitive.

- AI Agent makers should account for potential latency in pausing the recording and transcription.

- Sensitive information redaction is restricted to Copilot Studio. For any external connections from Copilot Studio to Power Automate, Connectors, customers are responsible for assessing redacted data with any relevant regulatory or compliance requirements.

- If the customer's response to the first question the voice AI Agent asks is flagged as sensitive, that content might not be redacted, due to a timing issue that affects redaction at the start of the conversation. However, all subsequent responses flagged as sensitive are redacted.

# Supported actions

| **Supported Action **                                           | **Data Redacted ** | **Notes **                                                                                                                                             |
|-----------------------------------------------------------------|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Flag variables as sensitive                                     | Yes                |                                                                                                                                                        |
| Assign a sensitive variable to a nonsensitive variable         | Yes                |                                                                                                                                                        |
| Sensitive variable in question node                             | Yes                |                                                                                                                                                        |
| Sensitive variable in message node                              | Yes                |                                                                                                                                                        |
| Sensitive variable in Condition node                            | Yes                |                                                                                                                                                        |
| Using sensitive variable in Power Fx                            | Yes                |                                                                                                                                                        |
| Write sensitive data to Dataverse explicitly                    | No                 | Not redacted                                                                                                                                           |
| Pass sensitive information in HTTP request                      | Yes                | Sensitive variables aren’t logged in Copilot Studio. Customers are responsible for redacting data from any destination they're sending this data to.  |
| Receive sensitive information from HTTP request                 | Yes                | Not redacted                                                                                                                                           |
| Passing sensitive information to Connectors                     | Yes                | Sensitive variables aren’t logged in Copilot Studio. Customers are responsible for redacting data from any destination they're sending this data to.  |
| Receive sensitive information from Connectors                   | No                 | Not redacted                                                                                                                                           |
| Pass sensitive information to Power Automate flows              | Yes                | The sensitive flag is turned on in Power Automate                                                                                                      |
| Receive sensitive information from Power Automate               | No                 | Not redacted                                                                                                                                           |
| Pass sensitive information explicitly in Transfer nodes        | No                 | Not redacted                                                                                                                                           |
| Pass sensitive information to Generative AI                            | No                 | Not redacted                                                                                                                                           |
| Write sensitive data to AppInsights via a Custom Log Event      | No                 | Not redacted                                                                                                                                           |
| Conversation logs in Dataverse (ConversationTranscripts table)  | Yes                |                                                                                                                                                        |
| Copilot Studio agent transcripts passed to Copilot Service workspace                  | Yes                | Only variables flagged as sensitive are redacted                                                                                                       |
| Digital/Messaging Channel                                       | No                 | Sensitive data is redacted from the AI agent transcripts, but are visible in transcripts                               |
| Multi-entity                                                    | Yes                | All the entities are flagged as sensitive                                                                                                              |


