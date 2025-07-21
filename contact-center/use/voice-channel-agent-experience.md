---
title: Use agent dashboard and call controls in the voice channel
description: Learn how you can use the agent dashboard, call controls, and make and receive customer calls.
ms.date: 07/22/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Use agent dashboard and call controls in the voice channel


[!INCLUDE[cc-feature-availability-embedded-yes](../includes/cc-feature-availability-embedded-yes.md)]

[!INCLUDE[cc-rebrand-bot-agent](../includes/cc-rebrand-bot-agent.md)]


The voice channel is integrated directly with Dynamics 365 by way of the agent dashboard. The dashboard offers you a consolidated view of the calling interface, the customer summary, case history, and timeline. The dashboard helps you provide quick, effective, and proactive solutions to customer issues. The customer service representative (service representative or representative) experience in the voice channel is similar to the chat and other channels, which reduces service representative training time and costs.

## Make and receive customer calls

You can call a customer by using the phone dialer on the **Active Conversation** page or the **Launch dialer** button on the menu. More information: [Call a customer](/dynamics365/customer-service/use/voice-channel-call-customer?context=/dynamics365/contact-center/context/use-context)

When a customer calls your business, an intelligent agent receives the incoming call. The agent gathers basic information about the customer issue and then transfers the call to you for further action. You receive a notification about the incoming call on your service representative desktop so you can accept it. The following section describes the call controls and other features you can use during your conversation.

## Call controls

The conversation panel in the service representative dashboard includes the following call controls that you can use when you call or answer phone calls from customers.

> [!div class="mx-imgBorder"]
> ![Screenshot of call controls.](../media/voice-channel-call-controls.png)

- **Mute**: Mute your microphone so your voice isn't audible to the customer.
- **Hold**: Puts the customer on hold. The customer hears the hold music. You can keep only one caller on hold at a time. 
To avoid the recording and transcription of what you say while the customer is on hold, your administrator can enable the **Allow automatic pause and resume when representative hold and un-hold the customer** option. With this option, recording and transcription are paused when you put the customer on hold and resumed when you remove the customer from hold. If the option is disabled, you must manually pause and resume the recording and transcription.
- **Consult**: Consult with a participant. You can consult with or bring another representative or supervisor into the call. You can have a *public* consultation, where the customer is actively involved in the conversation. Or you can have a *private* consultation, where you can put the customer on hold before you talk to your peers or supervisor.

  > [!NOTE]
  > -  When you initiate a consult, you are the primary service representative and the new participant has a consult role. Select **Transfer** next to the participant to transfer the call to the consulting service representative or supervisor. Once the call is transferred, you're the consulting service representative and can leave the call without ending the call. The consulting service representative becomes the primary service representative. If the primary service representative leaves the call, the call ends for the customer.
  > - Consulting on a call doesn't affect the collaborating service representative's capacity.
- **Transfer**: Transfer the call to a service representative, queue, a Teams user, or an external phone number. After you transfer the call, the service representative to whom the call is transferred is the primary service representative and you'll no longer be on the call.
    During a transfer to the queue, the customer is automatically put on hold. When you transfer a call to another service representative, your number is displayed on the caller ID. The transcription and recording of transferred calls continue if the administrator enabled the [option](/dynamics365/customer-service/voice-channel-configure-transcripts#enable-call-recording-and-transcription-for-voice?context=/dynamics365/contact-center/context/administer-context). You can disable recording from the dashboard. See: [Transfer and consult scenarios](/dynamics365/customer-service/use/voice-channel-transfer-consult?context=/dynamics365/contact-center/context/use-context)
- **Rejoin**: Rejoin the call. If you're disconnected from the call, you can rejoin the call from the Active Conversation form directly, instead of refreshing the page and then rejoining the call. Only primary service representatives see the **Rejoin** option. If the customer ends the call or the call is rerouted to the next available service representative while you are disconnected, you'll hear a message that the customer ended the call or was rerouted on selecting **Rejoin**.
- **End**: End the call.  To end the call after you select **End**, you must close the session. If you close the session, without selecting **End**, the call is routed back to a queue.
- **Dialpad**: Dial an extension number. If you must use the dial pad to send a response while navigating an IVR, select the dial pad icon next to the external participant in the participant list.
- **Mark spam**: [Report the incoming call as spam](#report-a-phone-number-as-spam). If you happened to accidentally mark a number as spam, you can select the **Unmark as spam** option.
- **Device settings**: Configure your microphone and speaker settings.
- **Take notes**:  Make note of important information or specific details from your conversation with the customer. It's in addition to the call recording and transcription that happen during the conversation. See [take notes specific to the conversation](/dynamics365/customer-service/use/oc-take-notes?context=/dynamics365/contact-center/context/use-context).
- - **Start recording and transcript**: If your administrator enabled the recording and transcription service, you can start recording and transcription of the call.
- **Pause recording and transcription**: If you don't want to capture some details of the conversation—such as bank details, billing, or payment information—you can temporarily pause the transcription and resume it later.
- **Knowledge Articles**: Get a list of knowledge base articles pertaining to the conversation that you can use to resolve the customer issue.
- **Link to conversation**: You can link another conversation, case, customer, or knowledge article to the conversation.

  > [!NOTE]
  > The **Link to conversation** button is disabled after you end the voice call. Open account or contact on a new tab and select **Link to conversation** to link record (customer or case) to conversation.

- **Transcription**: When your administrator enables the transcription and recording service, the conversation between you and the customer is automatically transcribed in real time. This means that you don't need to take notes during the call. This feature also helps your supervisor or service representative (in a call transfer) to see the call history.
   - **Hide Transcript**: You can hide the transcript if you don't want to see it during the call. Select **Show Transcript** to display the transcript again. 
     > [!NOTE]
     > When you select **Hide Transcript** or **Show Transcript**, the setting persists across all calls and sessions. For example, if you hide the transcript in one call, it remains hidden in all subsequent calls until you select **Show Transcript**.
- **Sentiment analysis**: The transcript is used for *live* sentiment analysis. This means that you or your supervisor can instantly view and gauge the customer's mood and feeling via the sentiment icons.

## Report a phone number as spam

You can report a phone number as a spam call while you're on the call by using the call controls on the conversation panel. A notification is then sent to your administrator for review and further action.

To report a phone number as spam, select **Mark spam**.

You can add notes to help your administrator review and block numbers. After you mark a number as spam, it goes into the pending review tab on the **Blocked numbers** page.

<a name="usecvd"></a>

## Use enhanced call quality over Citrix virtual desktop

You can improve the call experience for your representatives who connect to the Copilot Service workspace through Citrix virtual desktop. Learn about it in [Configure Citrix virtual desktop for improved call quality](../administer/configure-citrix-virtual-desktop-for-voice.md).

## Use Azure Virtual Desktop to connect to voice channel

You can use the Microsoft Remote Desktop client to connect to the voice channel using Azure Virtual Desktop. You can learn more about the disconnection scenarios at [Agent experience when local machine disconnects from the Azure Virtual Desktop instance](../administer/configure-voice-avd.md).

## Avoid call disconnection

Avoid the following actions to prevent call drops:

- Open other apps that need access to the microphone. It results in loss of your audio connection, and the customer can't hear you.
- Close the session directly to end call. If you do, the conversation moves from active to wrap up. Then if you close the session, the state goes from wrap up to closed. So, we recommend that you go through the conversation status route and select the **End** button and then close the session to take care of the wrap-up activities.

## Share feedback on call quality

When you end a call, if your administrator has enabled the [Customer service representative call quality feedback survey](/dynamics365/customer-service/administer/configure-end-of-call-survey?context=/dynamics365/contact-center/context/administer-context), the application displays a survey that asks you to rate the call quality on a scale of 1 to 5. The survey can appear after every call or at a frequency set by your administrator. A response of 1 indicates an imperfect call experience and 5 indicates a perfect call.

If you specify a rating between 1 and 4, the application displays a set of predefined options such as, "I couldn't hear any sound", "Volume was low", or "the call ended unexpectedly",  that you can use to provide additional feedback about the call quality

## Best practices

- Make sure that you enabled notifications, and audio and video options in the browser.
- When your shift ends, ensure that you sign out and close your browser through which you access Copilot Service workspace. Doing so helps avoid work items being incorrectly assigned to you.
- When you face network or hardware issues, the application displays error or warning messages on the communication panel. Use the information in the messages to resolve the problems. More information: [Use diagnostic messages to troubleshoot call issues](/troubleshoot/dynamics-365/customer-service/omnichannel-for-customer-service/use-diagnostic-messages-in-call-issues)

### Related information

[Overview of the voice channel](/dynamics365/customer-service/administer/voice-channel?context=/dynamics365/contact-center/context/administer-context) 
[Enable voice consult with Microsoft Teams users](/dynamics365/customer-service/administer/voice-consult-microsoft-teams-user?context=/dynamics365/contact-center/context/administer-context)  
[Call a customer](/dynamics365/customer-service/use/voice-channel-call-customer?context=/dynamics365/contact-center/context/use-context)


