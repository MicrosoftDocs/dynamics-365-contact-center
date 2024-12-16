---
title: Use Microsoft Azure Virtual Desktop to access voice channel
description: Learn how to configure the  Remote Desktop client in your service representatives' remote desktop to enable representatives to connect to the voice channel using Azure Virtual Desktop.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: how-to 
ms.collection: 
ms.date: 12/16/2024
ms.custom: bap-template 
---

# Use Microsoft Azure Virtual Desktop to access voice channel

You can configure the Remote Desktop client in your customer service representatives' (service representative or representative) remote desktops. This enables service representatives to connect to the voice channel using the Virtual Desktop. 

## Prerequisites

- [Connect to Azure Virtual Desktop with the Remote Desktop client for Windows](/azure/virtual-desktop/users/connect-windows?pivots=remote-desktop-msi#download-and-install-the-remote-desktop-client-msi) to ensure that representatives have Virtual Desktop installed on their remote desktop.
- Ensure that [Insider release](/azure/virtual-desktop/users/client-features-windows?pivots=remote-desktop-msi#enable-insider-releases) is enabled for the remote desktop client.
- [Install the multimedia redirection extension](/azure/virtual-desktop/multimedia-redirection) on the service representatives' browsers. Supported browsers are Microsoft Edge and Google Chrome.

### Access remote desktop

Make sure representatives perform the following steps to access the voice channel from the remote desktop after it's installed:

1. Restart the remote desktop client and the service representative's device.
1. Ensure that service representatives see **Remote Desktop(Insider)** is displayed on the remote desktop client.
1. Select the **ellipsis** (…) and then select **Subscribe**. 
1. Agents see **SessionDesktop** once they're subscribed. Agents can sign in the Virtual Desktop to use the voice channel.

## Agent experience when local machine disconnects from Virtual Desktop

Agents can communicate with customers on the phone to resolve issues using the voice channel through the Virtual Desktop. The following table describes the scenarios in which the local machine disconnects from the Virtual Desktop instance.

| **Scenario**                                                                 | **Notifications**                                  | **Ongoing phone call**                                                                                                      | **Ongoing non-phone call**                                                                                                 | **Active consult (primary service representative disconnected)**                                                                               | **Active consult (secondary service representative disconnected)**                                                                          | **Transfer**                                                                                      |
|------------------------------------------------------------------------------|---------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| Service representative is disconnected from the Virtual Desktop.                        | Notifications aren't delivered to service representative.          | The ongoing call remains assigned to the service representative. The customer hears a message that the service representative is disconnected and will rejoin the call shortly, followed by wait music. | Non-voice conversations remain assigned to the service representative. If the representative is in a chat that is converted to a voice or video call, the voice or video call ends. | The secondary representative hears a message that the primary representative is disconnected.                                                   | The call ends for the secondary representative.                                                                                       | Not applicable                                                                                                   |
| Service representative reconnects to the Virtual Desktop instance in less than 30 seconds. | Incoming notifications are displayed to the represerntative. | Agent is reconnected to the call. The call status, such as hold or mute, remains unchanged.                                  | The representative rejoins the conversation.                                                                                         | Primary service representative rejoins the call. The call status remains unchanged.                                                           | The call ends for the secondary service representative.                                                                                       | Call is transferred. The representative is connected to the call if the transfer fails.                                                |
| Service representative takes more than 30 seconds but less than 2.5 minutes to reconnect.     | Incoming notifications are displayed to the representative. | The call is rerouted.                                                                                                        | Agent rejoins the conversation.                                                                                            | Call gets rerouted to a different representative and the consult ends. The customer remains on hold.                                  | Call ends for the secondary representative.                                                                                           | Call is rerouted if the transfer fails.                                                                                       |
| Service representative takes more than 2.5 minutes to reconnect.                              | Incoming notifications are displayed when the representative reconnects. | Call is rerouted.                                                                                                            | Conversation is rerouted.                                                                                                   | Not applicable                                                                                                                          | Consult ends for the secondary service representative.                                                                                       | Call is rerouted.                                                                                                             |

### Best practices

Ensure that the service representatives using the Virtual Desktop have the latest version of the multimedia redirection extension installed on their browsers. If they don't have the latest version, representatives see error messages whenever they are in a call.