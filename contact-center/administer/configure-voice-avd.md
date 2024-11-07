---
title: Use Microsoft Azure Virtual Desktop to access voice channel
description: Learn how to configure the  Remote Desktop client in your agents remote desktop to enable agents to connect to the voice channel using Azure Virtual Desktop.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: 
ms.date: 09/26/2024
ms.custom: bap-template 
---

# Use Microsoft Azure Virtual Desktop to access voice channel

You can configure the Remote Desktop client in your agents' remote desktops. This enables agents to connect to the voice channel using the Virtual Desktop. 

## Prerequisites

- [Connect to Azure Virtual Desktop with the Remote Desktop client for Windows](/azure/virtual-desktop/users/connect-windows?pivots=remote-desktop-msi#download-and-install-the-remote-desktop-client-msi) to ensure that agents have Virtual Desktop installed on their remote desktop.
- Ensure that [Insider release](/azure/virtual-desktop/users/client-features-windows?pivots=remote-desktop-msi#enable-insider-releases) is enabled for the remote desktop client.
- [Install the multimedia redirection extension](/azure/virtual-desktop/multimedia-redirection) on the agents' browsers. Supported browsers are Microsoft Edge and Google Chrome.

### Access remote desktop

Make sure agents perform the following steps to access the voice channel from the remote desktop after it's installed:

1. Restart the remote desktop client and the agent device.
1. Ensure that agents see **Remote Desktop(Insider)** is displayed on the remote desktop client.
1. Select the **ellipsis** (…) and then select **Subscribe**. 
1. Agents see **SessionDesktop** once they're subscribed. Agents can sign in the Virtual Desktop to use the voice channel.

## Agent experience when local machine disconnects from Virtual Desktop

Agents can communicate with customers on the phone to resolve issues using the voice channel through the Virtual Desktop. The following table describes the scenarios in which the local machine disconnects from the Virtual Desktop instance.

| **Scenario**                                                                 | **Notifications**                                  | **Ongoing phone call**                                                                                                      | **Ongoing non-phone call**                                                                                                 | **Active consult (primary agent disconnected)**                                                                               | **Active consult (secondary agent disconnected)**                                                                          | **Transfer**                                                                                      |
|------------------------------------------------------------------------------|---------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| Agent is disconnected from the Virtual Desktop.                        | Notifications aren't delivered to agent.          | The ongoing call remains assigned to the agent. The customer hears a message that the agent is disconnected and will rejoin the call shortly, followed by wait music. | Non-voice conversations remain assigned to the agent. If the agent is in a chat that is converted to a voice or video call, the voice or video call ends. | The secondary agent hears a message that the primary agent is disconnected.                                                   | The call ends for the secondary agent.                                                                                       | Not applicable                                                                                                   |
| Agent reconnects to the Virtual Desktop instance in less than 30 seconds. | Incoming notifications are displayed to the agent. | Agent is reconnected to the call. The call status, such as hold or mute, remains unchanged.                                  | The agent rejoins the conversation.                                                                                         | Primary agent rejoins the call. The call status remains unchanged.                                                           | The call ends for the secondary agent.                                                                                       | Call is transferred. The agent is connected to the call if the transfer fails.                                                |
| Agent takes more than 30 seconds but less than 2.5 minutes to reconnect.     | Incoming notifications are displayed to the agent. | The call is rerouted.                                                                                                        | Agent rejoins the conversation.                                                                                            | Call gets rerouted to a different agent and the consult ends. The customer remains on hold.                                  | Call ends for the secondary agent.                                                                                           | Call is rerouted if the transfer fails.                                                                                       |
| Agent takes more than 2.5 minutes to reconnect.                              | Incoming notifications are displayed when the agent reconnects. | Call is rerouted.                                                                                                            | Conversation is rerouted.                                                                                                   | Not applicable                                                                                                                          | Consult ends for the secondary agent.                                                                                       | Call is rerouted.                                                                                                             |

### Best practices

Ensure that the agents using the Virtual Desktop have the latest version of the multimedia redirection extension installed on their browsers. If they don't have the latest version, agents see error messages whenever they are in a call.