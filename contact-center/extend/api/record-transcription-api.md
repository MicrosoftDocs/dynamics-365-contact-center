---
title: Use APIs to pause, resume transcription and recording 
description: Learn how to use APIs to pause and resume transcription and recording in Dynamics 365 Contact Center.
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.topic: reference 
ms.collection: 
ms.date: 11/15/2024
ms.custom: bap-template 
---

# Use APIs to pause, resume transcription and recording 

Dynamics 365 Contact Center provides a set of [APIs](https://github.com/microsoft/dynamics-365-contact-center/blob/main/documentation/Embed%20SDK%20APIs/README.md) to enable seamless integration of several functionalities into both non-Microsoft CRMs and Dynamics environments.

The [Voice module](https://github.com/microsoft/dynamics-365-contact-center/blob/main/documentation/Embed%20SDK%20APIs/classes/VoiceModule.md) has several methods enable you to control call recording and transcription services during customer interactions. These capabilities are essential when handling sensitive information such as payment details, personally identifiable information, or protected health information that shouldn't be captured in recordings for compliance and security reasons.

## Available methods

- **startRecording**: Initiates voice call recording with automatic transcription.
- **pauseRecording**: Temporarily pauses ongoing recording operations.
- **onRecordingOperationCompleted**: Invokes a callback function with event data when the recording operation is completed.
- **startTranscription**: Begins transcription without full recording.
- **pauseTranscription**: Pauses active transcription services.
- **onTranscriptionOperationCompleted**: Invokes a callback function with event data when the transcription operation is completed.

Learn more about the methods in [available methods in voice module](https://github.com/microsoft/dynamics-365-contact-center/blob/main/documentation/Embed%20SDK%20APIs/classes/VoiceModule.md)

## Sample code 

The following is a sample code that pauses the recording of a voice or video call when the customer service representative navigates to a specific tab in a form that contains sensitive information.

```
// Wait until voiceOrVideoCalling is available (retry up to 10 times)
async function waitForVoiceOrVideoCalling(retries = 10, delay = 500) {
    for (let i = 0; i < retries; i++) {
        const vvc = window.Microsoft.CCaaS.CCaaSSdk.voice;
        if (vvc) {
            console.log("voiceCalling is available.");
            return vvc;
        }
        console.log("Waiting for voiceCalling...");
        await new Promise((res) => setTimeout(res, delay));
    }
    console.warn("voiceCalling still not available after retrying.");
    return null;
}
 
// Wait for the focused session and get the conversation ID
async function getCurrentConversation() {
    try {
        console.log("Getting focused session...");
        const focusedSession = Microsoft.Apm.getFocusedSession();
        if (!focusedSession) {
            console.warn("Focused session not available.");
            return null;
        }
 
        const sessionCtx = await focusedSession.getContext();
        console.log("Session context:", sessionCtx);
 
        const conversationId = sessionCtx?.parameters?.LiveWorkItemId;
        console.log("****LiveWorkItemId****:", conversationId);
        return conversationId;
    } catch (error) {
        console.error("Error retrieving conversation ID:", error);
        return null;
    }
}
 
// Called when the tab changes to tab_4
async function onTabChange() {
    try {
        const voiceOrVideoCalling = await waitForVoiceOrVideoCalling();
        if (!voiceOrVideoCalling) return;
 
        const conversationId = await getCurrentConversation();
        if (!conversationId) {
            console.warn("Conversation ID is not available.");
            return;
        }
 
        await voiceOrVideoCalling.pauseRecording({ liveWorkItemId: conversationId });
        console.log("Recording paused for conversation:", conversationId);
    } catch (error) {
        console.error("Error during onTabChange:", error);
    }
}
 
// Called on form load
function onFormLoad(executionContext) {
    try {
        const formContext = executionContext.getFormContext();
        const tab = formContext.ui.tabs.get("tab_4");
 
        if (tab) {
            console.log("Tab found, adding tab change event.");
            tab.addTabStateChange(onTabChange);
        } else {
            console.warn("Tab 'tab_4' not found.");
        }
    } catch (error) {
        console.error("Error in onFormLoad:", error);
    }
}

```